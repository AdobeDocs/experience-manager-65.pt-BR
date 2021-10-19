---
title: Uso da Fusão de Recursos do Sling em AEM
seo-title: Using the Sling Resource Merger in AEM
description: A Sling Resource Merger fornece serviços para acessar e mesclar recursos
seo-description: The Sling Resource Merger provides services to access and merge resources
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: c07fa148054b69b0da7bb402ef96a50d0895abfa
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 1%

---

# Uso da Fusão de Recursos do Sling em AEM{#using-the-sling-resource-merger-in-aem}

## Propósito {#purpose}

A Sling Resource Merger fornece serviços para acessar e mesclar recursos. Ela fornece mecanismos de diferenciação (diferenciação) para ambos:

* **[Sobreposições](/help/sites-developing/overlays.md)** dos recursos que utilizam [caminhos de pesquisa configurados](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **Substituições** das caixas de diálogo do componente para a interface habilitada para toque (`cq:dialog`), usando a hierarquia do tipo de recurso (por meio da propriedade `sling:resourceSuperType`).

Com a Fusão de Recursos do Sling, os recursos de sobreposição/sobreposição e/ou as propriedades são mesclados com os recursos/propriedades originais:

* O conteúdo da definição personalizada tem uma prioridade mais alta do que o original (ou seja, ele *sobreposições* ou *substituições* a).

* Se necessário, [propriedades](#properties) definido na personalização, indique como o conteúdo unido do original será usado.

>[!CAUTION]
>
>O Sling Resource Merger e os métodos conexos só podem ser utilizados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso também significa que ela é adequada apenas para a interface de usuário padrão habilitada para toque; em particular, as substituições definidas dessa maneira são aplicáveis somente à caixa de diálogo habilitada para toque de um componente.
>
>As sobreposições/sobreposições para outras áreas (incluindo outros aspectos de um componente habilitado para toque ou da interface clássica) envolvem a cópia do nó e da estrutura apropriados do original para o local em que a personalização será definida.

### Metas para AEM {#goals-for-aem}

Os objetivos da utilização da fusão de recursos Sling em AEM são:

* garantir que as alterações de personalização não sejam feitas em `/libs`.
* reduzir a estrutura replicada de `/libs`.

   Ao usar o Sling Resource Merger, não é recomendável copiar toda a estrutura de `/libs` como isso resultaria na retenção de informações demais na personalização (normalmente `/apps`). A duplicação de informações aumenta desnecessariamente a chance de problemas quando o sistema é atualizado de alguma forma.

>[!NOTE]
>
>As substituições não dependem dos caminhos de pesquisa, elas usam a propriedade `sling:resourceSuperType` para fazer a conexão.
>
>No entanto, as substituições geralmente são definidas em `/apps`, já que a prática recomendada no AEM é definir personalizações em `/apps`; isso ocorre porque você não deve alterar nada em `/libs`.

>[!CAUTION]
>
>Você ***must*** não altere nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs`) `/apps`
>
>1. Faça quaisquer alterações no `/apps`

>


### Propriedades {#properties}

A fusão de recursos fornece as seguintes propriedades:

* `sling:hideProperties` ( `String` ou `String[]`)

   Especifica a propriedade, ou lista de propriedades, a ser ocultada.

   O curinga `*` oculta tudo.

* `sling:hideResource` ( `Boolean`)

   Indica se os recursos devem ser completamente ocultos, incluindo seus filhos.

* `sling:hideChildren` ( `String` ou `String[]`)

   Contém o nó filho ou a lista de nós filhos a serem ocultados. As propriedades do nó serão mantidas.

   O curinga `*` oculta tudo.

* `sling:orderBefore` ( `String`)

   Contém o nome do nó irmão que o nó atual deve ser posicionado na frente.

Essas propriedades afetam como os recursos/propriedades correspondentes/originais (de `/libs`) são usados pela sobreposição/sobreposição (geralmente em `/apps`).

### Criar a estrutura {#creating-the-structure}

Para criar uma sobreposição ou sobreposição, é necessário recriar o nó original, com a estrutura equivalente, no destino (normalmente `/apps`). Por exemplo:

* Sobreposição

   * A definição da entrada de navegação para o console Sites , conforme mostrado no painel, é definida em:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Para sobrepor isso, crie o seguinte nó:

      `/apps/cq/core/content/nav/sites`

      Em seguida, atualize a propriedade `jcr:title` conforme necessário.

* Substituir

   * A definição da caixa de diálogo habilitada para toque para o console Textos é definida em:

      `/libs/foundation/components/text/cq:dialog`

   * Para substituir isso, crie o seguinte nó - por exemplo:

      `/apps/the-project/components/text/cq:dialog`

Para criar qualquer um desses, você só precisa recriar a estrutura do esqueleto. Para simplificar a recriação da estrutura, todos os nós intermediários podem ser do tipo `nt:unstructured` (não têm de refletir o tipo de nó original; por exemplo, em `/libs`).

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
>Ao usar o Sling Resource Merger (ou seja, ao lidar com a interface padrão habilitada para toque), não é recomendável copiar toda a estrutura do `/libs` uma vez que resultaria na retenção de demasiadas informações em `/apps`. Isso pode causar problemas quando o sistema for atualizado de qualquer maneira.

### Casos de uso {#use-cases}

Isso, junto com a funcionalidade padrão, permite:

* **Adicionar uma propriedade**

   A propriedade não existe no `/libs` , mas é obrigatório na variável `/apps` sobrepor/sobrepor.

   1. Crie o nó correspondente em `/apps`
   1. Crie a nova propriedade neste nó &quot;

* **Redefinir uma propriedade (não propriedades criadas automaticamente)**

   A propriedade é definida em `/libs`, mas um novo valor é necessário na variável `/apps` sobrepor/sobrepor.

   1. Crie o nó correspondente em `/apps`
   1. Crie a propriedade correspondente neste nó (em / `apps`)

      * A propriedade terá uma prioridade com base na configuração do Resolvedor de Recursos do Sling.
      * A alteração do tipo de propriedade é suportada.

         Se você usar um tipo de propriedade diferente daquele usado em `/libs`, em seguida, será usado o tipo de propriedade definido.
   >[!NOTE]
   >
   >A alteração do tipo de propriedade é suportada.

* **Redefinir uma propriedade criada automaticamente**

   Por padrão, as propriedades criadas automaticamente (como `jcr:primaryType`) não estão sujeitas a uma sobreposição/sobreposição para garantir que o tipo de nó esteja atualmente em `/libs` for respeitada. Para impor uma sobreposição/sobreposição, é necessário recriar o nó em `/apps`, oculte explicitamente a propriedade e a redefina:

   1. Crie o nó correspondente em `/apps` com o `jcr:primaryType`
   1. Criar a propriedade do `sling:hideProperties` nesse nó, com o valor definido como o da propriedade criada automaticamente; por exemplo, `jcr:primaryType`

      Essa propriedade, definida em `/apps`, agora terá prioridade sobre o definido em `/libs`

* **Redefinir um nó e seus filhos**

   O nó e seus filhos são definidos em `/libs`, mas uma nova configuração é necessária no `/apps` sobrepor/sobrepor.

   1. Combine as ações de:

      1. Ocultar filhos de um nó (mantendo as propriedades do nó)
      1. Redefinir a propriedade/propriedades

* **Ocultar uma propriedade**

   A propriedade é definida em `/libs`, mas não é obrigatório no `/apps` sobrepor/sobrepor.

   1. Crie o nó correspondente em `/apps`
   1. Criar uma propriedade do `sling:hideProperties` de tipo `String` ou `String[]`. Use esta opção para especificar as propriedades a serem ocultadas/ignoradas. Também é possível usar curingas. Por exemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar um nó e seus filhos**

   O nó e seus filhos são definidos em `/libs`, mas não é obrigatório no `/apps` sobrepor/sobrepor.

   1. Crie o nó correspondente em /apps
   1. Criar uma propriedade do `sling:hideResource`

      * tipo: `Boolean`
      * valor: `true`

* **Ocultar filhos de um nó (ao manter as propriedades do nó)**

   O nó , suas propriedades e seus filhos são definidos em `/libs`. O nó e suas propriedades são necessárias na variável `/apps` sobreposição/sobreposição, mas alguns ou todos os nós filhos não são necessários no `/apps` sobrepor/sobrepor.

   1. Crie o nó correspondente em `/apps`
   1. Criar a propriedade do `sling:hideChildren`:

      * tipo: `String[]`
      * valor: uma lista dos nós secundários (conforme definido em `/libs`) para ocultar/ignorar

      O curinga &amp;ast; pode ser usado para ocultar/ignorar todos os nós filhos.


* **Reordenar nós**

   O nó e seus irmãos são definidos em `/libs`. Uma nova posição é necessária para que o nó seja recriado na função `/apps` sobreposição/sobreposição, em que a nova posição é definida como referência ao nó irmão apropriado em `/libs`.

   * Use o `sling:orderBefore` propriedade:

      1. Crie o nó correspondente em `/apps`
      1. Criar a propriedade do `sling:orderBefore`:

         Isso especifica o nó (como em `/libs`) que o nó atual deve ser posicionado antes de:

         * tipo: `String`
         * valor: `<before-SiblingName>`

### Chamando a Fusão de Recursos do Sling do seu código {#invoking-the-sling-resource-merger-from-your-code}

A Sling Resource Merger inclui dois provedores de recursos personalizados - um para sobreposições e outro para substituições. Cada um desses pode ser chamado em seu código usando um ponto de montagem:

>[!NOTE]
>
>Ao acessar o recurso, é recomendável usar o ponto de montagem apropriado.
>
>Isso garante que o Sling Resource Merger seja chamado e o recurso totalmente mesclado seja devolvido (reduzindo a estrutura que precisa ser replicada de `/libs`).

* Sobreposição:

   * finalidade: mesclar recursos com base em seu caminho de pesquisa
   * ponto de montagem: `/mnt/overlay`
   * usage: `mount point + relative path`
   * exemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Substituir:

   * finalidade: mesclar recursos com base em seu super tipo
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

   * [Configurar as propriedades da página](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
