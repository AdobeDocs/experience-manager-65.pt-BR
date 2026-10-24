---
title: Criar um índice personalizado para referências de formulário adaptável
description: Saiba como criar um índice Lucene marcado para consultas de referência de formulário adaptável no AEM Forms para evitar consultas de passagem ao publicar Fragmentos de experiência.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 9240de61985dc32f17593f416e5d054cadb8a392
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%
---

# Criar um índice personalizado para referências de formulário adaptáveis {#create-custom-index-for-adaptive-forms-references}

Crie um índice Lucene marcado para evitar consultas de passagem quando o Adobe Experience Manager (AEM) Forms resolver referências de formulário adaptáveis. Sem um índice adequado, a publicação de um Fragmento de experiência que contenha uma referência de formulário adaptável pode produzir um aviso `Traversal query (query without index)` nos logs.

No AEM Forms 6.5.24.0 e posterior, a consulta de referência usa a marca de índice `aemformsAFReferences`. Essas versões incluem a alteração da consulta, mas você deve criar um índice personalizado com essa tag. Este artigo mostra como definir e implantar o índice.

Para o AEM Forms 6.5 LTS, consulte [Criar um índice personalizado para referências de formulário adaptável no AEM Forms 6.5 LTS](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65-lts/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references).

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem:

* AEM Forms 6.5.24.0 ou posterior, com o complemento Forms correspondente instalado.
* Acesso para criar um índice em `/oak:index` na instância do autor.
* Um projeto do AEM com um módulo `ui.apps` se você implantar o índice por meio de um pacote de conteúdo ou acessar o CRXDE Lite para a alternativa de desenvolvimento.

Teste o índice em um ambiente de desenvolvimento ou de preparo antes de implantá-lo na produção. [A compilação de um índice pode demorar em um repositório grande](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes).

## Definir o índice personalizado {#define-the-custom-index}

Criar o índice em `/oak:index/customAFReferenceLuceneIndex-1`. Você pode escolher um nome de nó de índice diferente, mas mantenha a marca `aemformsAFReferences` inalterada para que a consulta de referência do Forms possa selecionar o índice.

Use a definição a seguir. Ele indexa `sling:resourceType` em `nt:unstructured` nós em `/content`.

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

Não adicionar `analyzed=true`. A consulta de referência usa restrições de propriedade em vez de uma condição `contains` de texto completo, de modo que a configuração é desnecessária.

## Implantar o índice com um pacote de conteúdo {#deploy-the-index-with-a-content-package}

Use um pacote de conteúdo para implantações de produção.

1. No módulo `ui.apps` do projeto do AEM, crie `ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`.
1. Crie `.content.xml` nesse diretório com a seguinte definição:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. Adicione o filtro a seguir dentro do elemento `workspaceFilter` existente em `ui.apps/src/main/content/META-INF/vault/filter.xml`. Mantenha os outros filtros do projeto inalterados.

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. Crie o projeto usando a configuração de compilação existente e instale o pacote de conteúdo resultante na instância do autor. Para obter instruções sobre carregamento e instalação de pacotes, consulte [Gerenciador de Pacotes](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system).
1. Confirme se `/oak:index/customAFReferenceLuceneIndex-1` existe. Permitir que a indexação assíncrona seja concluída antes de verificar o plano de consulta.

Se você escolher um nome de índice diferente, use esse nome de forma consistente no diretório, filtro e caminho do repositório.

## Criar o índice com o CRXDE Lite {#create-the-index-with-crxde-lite}

Use essa alternativa em um ambiente de desenvolvimento, em vez do método do pacote de conteúdo.

Use as seguintes propriedades ao criar o nó de índice:

| Propriedade | Tipo | Valor |
| --- | --- | --- |
| `selectionPolicy` | String | `tag` |
| `compatVersion` | Longo | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | String | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | Booleano | `true` |
| `reindex` | Booleano | `false` |

`String[]` significa uma propriedade de Cadeia de Caracteres de vários valores, mesmo quando contém apenas um valor.

1. Abra `http://localhost:4502/crx/de/index.jsp`. Substitua o host e a porta pelas da instância do autor.
1. Vá até `/oak:index`. Clique com o botão direito do mouse no nó e selecione [!UICONTROL Criar] > [!UICONTROL Criar Nó].
1. Criar `customAFReferenceLuceneIndex-1` com tipo `oak:QueryIndexDefinition`.
1. Adicione as propriedades da tabela acima ao nó do índice.
1. No nó do índice, crie a seguinte hierarquia de nó secundário. Defina cada tipo de nó filho como `nt:unstructured`:

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. Em `resourceType`, adicione `name` (String) com o valor `sling:resourceType` e `propertyIndex` (Booleano) com o valor `true`.
1. Selecione [!UICONTROL Salvar tudo] e permitir que a indexação assíncrona seja concluída.

## Verificar se a consulta usa o índice {#verify-that-the-query-uses-the-index}

Verifique o plano de consulta para confirmar se a consulta de referência seleciona o índice personalizado.

1. Confirme se a indexação assíncrona foi concluída. Use o [Gerenciador de Índices](/help/sites-administering/operations-dashboard.md#the-index-manager) para inspecionar o status do índice.
1. Abra [!UICONTROL Ferramentas] > [!UICONTROL Operações] > [!UICONTROL Diagnóstico] > [!UICONTROL Desempenho da Consulta] e selecione [!UICONTROL Explicar Consulta]. Selecione o idioma de consulta XPath e insira:

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. Selecione [!UICONTROL Explicar]. Confirme se o plano usa `lucene:customAFReferenceLuceneIndex-1` e `/oak:index/customAFReferenceLuceneIndex-1`, ou o nome de índice escolhido, para as ramificações da consulta em vez de um plano de travessia. Para obter detalhes, consulte [Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query).
1. Repita a operação de publicação do Fragmento de experiência que produziu o aviso. Verificar `error.log` em busca de novos avisos de passagem de `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences`.

Se o plano não selecionar o índice personalizado, verifique a marca, a hierarquia `indexRules` e a definição de propriedade `sling:resourceType` em relação aos exemplos acima. Para obter mais diagnósticos, consulte [Solução de problemas de índices do Oak](/help/sites-deploying/troubleshooting-oak-indexes.md).

## Tarefas relacionadas {#related-tasks}

Para obter mais informações sobre o desempenho da consulta e a configuração do índice, consulte:

* [Consultas e indexação do Oak](/help/sites-deploying/queries-and-indexing.md)
* [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Solução de problemas de consultas lentas](/help/sites-developing/troubleshooting-slow-queries.md)
