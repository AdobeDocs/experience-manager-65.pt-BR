---
title: Utilização da fusão de recursos Sling em AEM
seo-title: Utilização da fusão de recursos Sling em AEM
description: A fusão Sling Resource presta serviços de acesso e fusão de recursos
seo-description: A fusão Sling Resource presta serviços de acesso e fusão de recursos
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 1%

---


# Usando a Fusão de Recursos Sling em AEM{#using-the-sling-resource-merger-in-aem}

## Propósito {#purpose}

A fusão Sling Resource presta serviços de acesso e fusão de recursos. Fornece mecanismos de diferenciação (diferenciação) para ambos:

* **[Sobreposição](/help/sites-developing/overlays.md)** de recursos usando os caminhos [ de pesquisa ](/help/sites-developing/overlays.md#configuring-the-search-paths)configurados.

* **Substituições** das caixas de diálogo do componente para a interface habilitada para toque (`cq:dialog`), usando a hierarquia do tipo de recurso (por meio da propriedade  `sling:resourceSuperType`).

Com a Fusão de recursos Sling, os recursos de sobreposição/sobreposição e/ou as propriedades são unidos aos recursos/propriedades originais:

* O conteúdo da definição personalizada tem uma prioridade mais alta do que a do original (isto é, *sobreposições* ou *sobreposições*).

* Quando necessário, [propriedades](#properties) definidas na personalização, indique como o conteúdo unido do original deve ser usado.

>[!CAUTION]
>
>A Fusão de Recursos Sling e os métodos relacionados só podem ser usados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso também significa que ele é apropriado apenas para a interface padrão e habilitada para toque; em particular, as substituições definidas dessa maneira são aplicáveis somente à caixa de diálogo habilitada para toque de um componente.
>
>As sobreposições/substituições para outras áreas (incluindo outros aspectos de um componente ativado por toque ou da interface clássica) envolvem a cópia do nó e da estrutura apropriados do original para onde a personalização será definida.

### Metas para AEM {#goals-for-aem}

Os objetivos da utilização da fusão Sling Resource em AEM são os seguintes:

* verifique se as alterações de personalização não foram feitas em `/libs`.
* reduza a estrutura que é replicada de `/libs`.

   Ao usar a Fusão de recursos Sling, não é recomendável copiar toda a estrutura de `/libs`, pois isso resultaria na retenção de informações demais na personalização (normalmente `/apps`). A duplicação de informações aumenta desnecessariamente a chance de problemas quando o sistema é atualizado de alguma forma.

>[!NOTE]
>
>As substituições não dependem dos caminhos de pesquisa, elas usam a propriedade `sling:resourceSuperType` para fazer a conexão.
>
>No entanto, as substituições são frequentemente definidas em `/apps`, já que a prática recomendada no AEM é definir personalizações em `/apps`; isso ocorre porque você não deve alterar nada em `/libs`.

>[!CAUTION]
>
>Você ***deve*** não alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (isto é, como ele existe em `/libs`) em `/apps`
   >
   >
1. Faça quaisquer alterações em `/apps`

>



### Propriedades {#properties}

A fusão de recursos fornece as seguintes propriedades:

* `sling:hideProperties` ( `String` ou  `String[]`)

   Especifica a propriedade, ou lista de propriedades, a ser ocultada.

   O caractere curinga `*` oculta tudo.

* `sling:hideResource` ( `Boolean`)

   Indica se os recursos devem estar completamente ocultos, incluindo seus filhos.

* `sling:hideChildren` ( `String` ou  `String[]`)

   Contém o nó filho, ou lista de nós filhos, a ser ocultado. As propriedades do nó serão mantidas.

   O caractere curinga `*` oculta tudo.

* `sling:orderBefore` (  `String`)

   Contém o nome do nó irmão no qual o nó atual deve ser posicionado na frente.

Essas propriedades afetam como os recursos/propriedades correspondentes/originais (de `/libs`) são usados pela sobreposição/substituição (geralmente em `/apps`).

### Criação da estrutura {#creating-the-structure}

Para criar uma sobreposição ou sobreposição, é necessário recriar o nó original, com a estrutura equivalente, sob o destino (normalmente `/apps`). Por exemplo:

* Sobreposição

   * A definição da entrada de navegação para o console Sites, como mostrado no painel, é definida em:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Para sobrepor isso, crie o seguinte nó:

      `/apps/cq/core/content/nav/sites`

      Em seguida, atualize a propriedade `jcr:title`, conforme necessário.

* Substituir

   * A definição da caixa de diálogo habilitada para toque para o console Textos é definida em:

      `/libs/foundation/components/text/cq:dialog`

   * Para substituir isso, crie o seguinte nó - por exemplo:

      `/apps/the-project/components/text/cq:dialog`

Para criar qualquer um desses, basta recriar a estrutura do esqueleto. Para simplificar a recriação da estrutura, todos os nós intermediários podem ser do tipo `nt:unstructured` (eles não precisam refletir o tipo de nó original; por exemplo, em `/libs`).

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
>Ao usar a Fusão de recursos Sling (isto é, ao lidar com a interface de usuário padrão, habilitada para toque), não é recomendado copiar toda a estrutura de `/libs`, pois isso resultaria na retenção de muitas informações em `/apps`. Isso pode causar problemas quando o sistema é atualizado de alguma forma.

### Casos de uso {#use-cases}

Eles, juntamente com a funcionalidade padrão, permitem que você:

* **Adicionar uma propriedade**

   A propriedade não existe na definição `/libs`, mas é necessária na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Crie a nova propriedade neste nó &quot;

* **Redefinir uma propriedade (não propriedades criadas automaticamente)**

   A propriedade é definida em `/libs`, mas um novo valor é necessário na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Criar a propriedade correspondente neste nó (em / `apps`)

      * A propriedade terá uma prioridade com base na configuração do Sling Resource Resolver.
      * A alteração do tipo de propriedade é suportada.

         Se você usar um tipo de propriedade diferente daquele usado em `/libs`, o tipo de propriedade definido será usado.
   >[!NOTE]
   >
   >A alteração do tipo de propriedade é suportada.

* **Redefinir uma propriedade criada automaticamente**

   Por padrão, as propriedades criadas automaticamente (como `jcr:primaryType`) não estão sujeitas a uma sobreposição/substituição para garantir que o tipo de nó atualmente em `/libs` seja respeitado. Para impor uma sobreposição/sobreposição, é necessário recriar o nó em `/apps`, ocultar explicitamente a propriedade e redefini-la:

   1. Crie o nó correspondente em `/apps` com o `jcr:primaryType` desejado
   1. Crie a propriedade `sling:hideProperties` nesse nó, com o valor definido para o da propriedade criada automaticamente; por exemplo, `jcr:primaryType`

      Essa propriedade, definida em `/apps`, terá prioridade sobre a definida em `/libs`

* **Redefinir um nó e seus filhos**

   O nó e seus filhos são definidos em `/libs`, mas uma nova configuração é necessária na sobreposição/substituição `/apps`.

   1. Combine as ações de:

      1. Ocultar filhos de um nó (mantendo as propriedades do nó)
      1. Redefinir a propriedade/propriedades

* **Ocultar uma propriedade**

   A propriedade é definida em `/libs`, mas não é exigida na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Crie uma propriedade `sling:hideProperties` do tipo `String` ou `String[]`. Use esta opção para especificar as propriedades que serão ocultadas/ignoradas. Caracteres curinga também podem ser usados. Por exemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar um nó e seus filhos**

   O nó e seus filhos são definidos em `/libs`, mas não são obrigatórios na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em /apps
   1. Criar uma propriedade `sling:hideResource`

      * tipo: `Boolean`
      * valor: `true`

* **Ocultar filhos de um nó (mantendo as propriedades do nó)**

   O nó, suas propriedades e seus filhos são definidos em `/libs`. O nó e suas propriedades são necessários na sobreposição/substituição `/apps`, mas alguns ou todos os nós filhos não são necessários na sobreposição/substituição `/apps`.

   1. Criar o nó correspondente em `/apps`
   1. Crie a propriedade `sling:hideChildren`:

      * tipo: `String[]`
      * valor: uma lista dos nós secundários (conforme definido em `/libs`) para ocultar/ignorar

      O caractere curinga &amp;ast; pode ser usado para ocultar/ignorar todos os nós filhos.


* **Reordenar nós**

   O nó e seus irmãos são definidos em `/libs`. Uma nova posição é necessária para que o nó seja recriado na sobreposição/substituição `/apps`, onde a nova posição é definida em referência ao nó irmão apropriado em `/libs`.

   * Use a propriedade `sling:orderBefore`:

      1. Criar o nó correspondente em `/apps`
      1. Crie a propriedade `sling:orderBefore`:

         Isso especifica o nó (como em `/libs`) que o nó atual deve ser posicionado antes:

         * tipo: `String`
         * valor: `<before-SiblingName>`

### Invocando a Fusão de Recursos Sling de seu código {#invoking-the-sling-resource-merger-from-your-code}

A Fusão de recursos Sling inclui dois provedores de recursos personalizados - um para sobreposições e outro para substituições. Cada uma dessas opções pode ser invocada em seu código usando um ponto de montagem:

>[!NOTE]
>
>Ao acessar seu recurso, é recomendável usar o ponto de montagem apropriado.
>
>Isso garante que a Fusão de Recursos Sling seja invocada e que o recurso totalmente mesclado seja devolvido (reduzindo a estrutura que precisa ser replicada de `/libs`).

* Sobreposição:

   * objetivo: mesclar recursos com base em seu caminho de pesquisa
   * ponto de montagem: `/mnt/overlay`
   * usage: `mount point + relative path`
   * exemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Substituir:

   * objetivo: mesclar recursos com base em seu super tipo
   * ponto de montagem: `/mnt/overide`
   * uso: `mount point + absolute path`
   * exemplo:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Exemplo de uso {#example-of-usage}

Alguns exemplos são abordados:

* Sobreposição:

   * [Personalização dos consoles](/help/sites-developing/customizing-consoles-touch.md)
   * [Personalização da criação de página](/help/sites-developing/customizing-page-authoring-touch.md)

* Substituir:

   * [Configuração das propriedades da página](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

