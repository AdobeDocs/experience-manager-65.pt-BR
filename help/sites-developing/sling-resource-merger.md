---
title: Uso da Fusão de recursos do Sling no AEM
seo-title: Using the Sling Resource Merger in AEM
description: O Sling Resource Merger fornece serviços para acessar e mesclar recursos
seo-description: The Sling Resource Merger provides services to access and merge resources
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 1%

---

# Uso da Fusão de recursos do Sling no AEM{#using-the-sling-resource-merger-in-aem}

## Propósito {#purpose}

O Sling Resource Merger fornece serviços para acessar e mesclar recursos. Ela fornece mecanismos de diferenciação para:

* **[Sobreposições](/help/sites-developing/overlays.md)** de recursos usando o [caminhos de pesquisa configurados](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **Substituições** das caixas de diálogo do componente para a interface habilitada para toque (`cq:dialog`), usando a hierarquia de tipo de recurso (por meio da propriedade `sling:resourceSuperType`).

Com o Sling Resource Merger, os recursos e/ou propriedades de sobreposição/substituição são mesclados com os recursos/propriedades originais:

* O conteúdo da definição personalizada tem uma prioridade mais alta que a do original (ou seja, ela *sobreposições* ou *sobreposições* it).

* Se necessário, [propriedades](#properties) definido na personalização, indique como o conteúdo mesclado do original deve ser usado.

>[!CAUTION]
>
>O Sling Resource Merger e métodos relacionados só podem ser usados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso também significa que ele só é apropriado para a interface padrão habilitada para toque; em particular, as substituições definidas dessa maneira são aplicáveis somente para a caixa de diálogo habilitada para toque de um componente.
>
>Sobreposições/substituições para outras áreas (incluindo outros aspectos de um componente habilitado para toque ou a interface clássica) envolvem copiar o nó e a estrutura apropriados do original para onde a personalização será definida.

### Metas para o AEM {#goals-for-aem}

As metas para usar a Fusão de recursos do Sling no AEM são:

* certifique-se de que as alterações de personalização não sejam feitas no `/libs`.
* reduzir a estrutura que é replicada de `/libs`.

  Ao usar a Fusão de recursos do Sling, não é recomendável copiar toda a estrutura de `/libs` como isso resultaria em muitas informações mantidas na personalização (geralmente `/apps`). Duplicar informações aumenta desnecessariamente a chance de problemas quando o sistema é atualizado de alguma forma.

>[!NOTE]
>
>As substituições não dependem dos caminhos de pesquisa, elas usam a propriedade `sling:resourceSuperType` para fazer a conexão.
>
>No entanto, as sobreposições geralmente são definidas em `/apps`, como prática recomendada no AEM, definir personalizações em `/apps`; isso ocorre porque você não deve alterar nada em `/libs`.

>[!CAUTION]
>
>Você ***deve*** não alterar nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído ao aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recriar o item necessário (ou seja, como ele existe em `/libs`) em `/apps`
>
>1. Fazer alterações em `/apps`
>

### Propriedades {#properties}

A fusão de recursos oferece as seguintes propriedades:

* `sling:hideProperties` ( `String` ou `String[]`)

  Especifica a propriedade, ou lista de propriedades, a ser ocultada.

  O curinga `*` oculta tudo.

* `sling:hideResource` ( `Boolean`)

  Indica se os recursos devem ser completamente ocultos, incluindo seus filhos.

* `sling:hideChildren` ( `String` ou `String[]`)

  Contém o nó filho, ou lista de nós filhos, a ser ocultado. As propriedades do nó serão mantidas.

  O curinga `*` oculta tudo.

* `sling:orderBefore` ( `String`)

  Contém o nome do nó irmão no qual o nó atual deve ser posicionado.

Essas propriedades afetam como os recursos/propriedades correspondentes/originais (de `/libs`) são usados pela sobreposição/substituição (geralmente em `/apps`).

### Criação da estrutura {#creating-the-structure}

Para criar uma sobreposição ou sobreposição, é necessário recriar o nó original, com a estrutura equivalente, no destino (geralmente `/apps`). Por exemplo:

* Sobreposição

   * A definição da entrada de navegação do console Sites, como mostrado no painel, é definida em:

     `/libs/cq/core/content/nav/sites/jcr:title`

   * Para sobrepor isso, crie o seguinte nó:

     `/apps/cq/core/content/nav/sites`

     Em seguida, atualize a propriedade `jcr:title` conforme necessário.

* Substituir

   * A definição da caixa de diálogo habilitada para toque do console de Textos está definida em:

     `/libs/foundation/components/text/cq:dialog`

   * Para substituir isso, crie o seguinte nó - por exemplo:

     `/apps/the-project/components/text/cq:dialog`

Para criar qualquer uma dessas opções, basta recriar a estrutura do esqueleto. Para simplificar a recriação da estrutura, todos os nós intermediários podem ser do tipo `nt:unstructured` (elas não precisam refletir o tipo de nó original; por exemplo, em `/libs`).

Portanto, no exemplo de sobreposição acima, os seguintes nós são necessários:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Ao usar o Sling Resource Merger (ou seja, ao lidar com a interface padrão habilitada para toque), não é recomendável copiar toda a estrutura de `/libs` como resultaria em um excesso de informações mantidas em `/apps`. Isso pode causar problemas quando o sistema é atualizado de alguma forma.

### Casos de uso {#use-cases}

Eles, juntamente com a funcionalidade padrão, permitem:

* **Adicionar uma propriedade do**

  A propriedade não existe no `/libs` definição, mas é obrigatório na variável `/apps` sobrepor/substituir.

   1. Crie o nó correspondente em `/apps`
   1. Criar a nova propriedade neste nó &quot;

* **Redefinir uma propriedade (não propriedades criadas automaticamente)**

  A propriedade é definida em `/libs`, mas um novo valor é necessário no `/apps` sobrepor/substituir.

   1. Crie o nó correspondente em `/apps`
   1. Crie a propriedade correspondente neste nó (em / `apps`)

      * A propriedade terá uma prioridade com base na configuração do Sling Resource Resolver.
      * Não há suporte para a alteração do tipo de propriedade.

        Se você usar um tipo de propriedade diferente daquele usado em `/libs`, o tipo de propriedade definido será usado.

  >[!NOTE]
  >
  >Não há suporte para a alteração do tipo de propriedade.

* **Redefinir uma propriedade criada automaticamente**

  Por padrão, as propriedades criadas automaticamente `jcr:primaryType`) não estão sujeitos a uma sobreposição/substituição para garantir que o tipo de nó atualmente em `/libs` é respeitado. Para impor uma sobreposição/substituição, é necessário recriar o nó em `/apps`, oculte explicitamente a propriedade e redefina-a:

   1. Crie o nó correspondente em `/apps` com o desejado `jcr:primaryType`
   1. Criar a propriedade `sling:hideProperties` nesse nó, com o valor definido como aquele da propriedade criada automaticamente; por exemplo, `jcr:primaryType`

      Essa propriedade, definida em `/apps`, terá prioridade sobre a definida em `/libs`

* **Redefinir um nó e seus filhos**

  O nó e seus filhos são definidos em `/libs`, mas uma nova configuração é necessária na variável `/apps` sobrepor/substituir.

   1. Combine as ações de:

      1. Ocultar filhos de um nó (mantendo as propriedades do nó)
      1. Redefinir a propriedade/as propriedades

* **Ocultar uma propriedade**

  A propriedade é definida em `/libs`, mas não obrigatório no `/apps` sobrepor/substituir.

   1. Crie o nó correspondente em `/apps`
   1. Criar uma propriedade do `sling:hideProperties` do tipo `String` ou `String[]`. Use esta opção para especificar as propriedades que devem ser ocultas/ignoradas. Curingas também podem ser usados. Por exemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar um nó e seus filhos**

  O nó e seus filhos são definidos em `/libs`, mas não obrigatório no `/apps` sobrepor/substituir.

   1. Crie o nó correspondente em /apps
   1. Criar uma propriedade do `sling:hideResource`

      * tipo: `Boolean`
      * valor: `true`

* **Ocultar filhos de um nó (enquanto mantém as propriedades do nó)**

  O nó, suas propriedades e seus filhos são definidos em `/libs`. O nó e suas propriedades são necessários na variável `/apps` sobrepor/substituir, mas alguns ou todos os nós secundários não são necessários no `/apps` sobrepor/substituir.

   1. Crie o nó correspondente em `/apps`
   1. Criar a propriedade `sling:hideChildren`:

      * tipo: `String[]`
      * value: uma lista de nós filhos (conforme definido em `/libs`) para ocultar/ignorar

      O curinga &amp;ast; pode ser usado para ocultar/ignorar todos os nós filhos.

* **Reordenar nós**

  O nó e seus irmãos são definidos em `/libs`. Uma nova posição é necessária para que o nó seja recriado na `/apps` sobrepor/substituir, onde a nova posição é definida em referência ao nó irmão apropriado em `/libs`.

   * Use o `sling:orderBefore` propriedade:

      1. Crie o nó correspondente em `/apps`
      1. Criar a propriedade `sling:orderBefore`:

         Isso especifica o nó (como em `/libs`) que o nó atual deve ser posicionado antes:

         * tipo: `String`
         * valor: `<before-SiblingName>`

### Chamar o Sling Resource Merger a partir de seu código {#invoking-the-sling-resource-merger-from-your-code}

O Sling Resource Merger inclui dois provedores de recursos personalizados, um para sobreposições e outro para substituições. Cada um desses pode ser chamado dentro do código usando um ponto de montagem:

>[!NOTE]
>
>Ao acessar o recurso, é recomendável usar o ponto de montagem apropriado.
>
>Isso garante que o Sling Resource Merger seja chamado e que o recurso totalmente mesclado seja retornado (reduzindo a estrutura que precisa ser replicada do `/libs`).

* Sobreposição:

   * finalidade: mesclar recursos com base no caminho de pesquisa
   * ponto de montagem: `/mnt/overlay`
   * uso: `mount point + relative path`
   * exemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Substituir:

   * finalidade: mesclar recursos com base em seu supertipo
   * ponto de montagem: `/mnt/overide`
   * uso: `mount point + absolute path`
   * exemplo:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Exemplo de uso {#example-of-usage}

Alguns exemplos são abordados:

* Sobreposição:

   * [Personalização dos Consoles](/help/sites-developing/customizing-consoles-touch.md)
   * [Personalização da criação de página](/help/sites-developing/customizing-page-authoring-touch.md)

* Substituir:

   * [Configuração das propriedades da página](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
