---
title: Configuração da segmentação com o ContextHub
seo-title: Configuração da segmentação com o ContextHub
description: Saiba como configurar a segmentação com o Context Hub.
seo-description: Saiba como configurar a segmentação com o Context Hub.
uuid: 196cfb18-317c-443d-b6f1-f559e4221baa
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 6cade87c-9ed5-47d7-9b39-c942268afdad
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Configuração da segmentação com o ContextHub{#configuring-segmentation-with-contexthub}

>[!NOTE]
>
>Esta seção descreve como configurar a segmentação ao usar o ContextHub. Se você estiver usando a funcionalidade Contexto do cliente, consulte a documentação relevante para [configurar a segmentação para Contexto](/help/sites-administering/campaign-segmentation.md)do cliente.


A segmentação é uma consideração importante ao criar uma campanha. Consulte [Gerenciamento de públicos-alvo](/help/sites-authoring/managing-audiences.md) para obter informações sobre como a segmentação funciona e os termos-chave.

Dependendo das informações que você já coletou sobre os visitantes do site e as metas que deseja atingir, será necessário definir os segmentos e as estratégias necessárias para o conteúdo direcionado.

Esses segmentos são usados para fornecer a um visitante conteúdo direcionado especificamente. Esse conteúdo é mantido na seção [Personalização](/help/sites-authoring/personalization.md) do site. [As atividades](/help/sites-authoring/activitylib.md) definidas aqui podem ser incluídas em qualquer página e definir para qual segmento de visitante o conteúdo especializado se aplica.

O AEM permite que você personalize facilmente a experiência de seus usuários. Também permite verificar os resultados das definições de segmento.

## Acessar segmentos {#accessing-segments}

O console [Públicos](/help/sites-authoring/managing-audiences.md) é usado para gerenciar segmentos para o ContextHub ou o Contexto do cliente, bem como públicos-alvo para sua conta do Adobe Target. Esta documentação cobre o gerenciamento de segmentos para o ContextHub. Para segmentos [de contexto do](/help/sites-administering/campaign-segmentation.md) cliente e segmentos do Adobe Target, consulte a documentação relevante.

Para acessar seus segmentos, na navegação global, selecione **Navegação > Personalização > Públicos**.

![chlimage_1-310](assets/chlimage_1-310.png)

## Editor do segmento {#segment-editor}

O Editor **de** segmentos permite modificar facilmente um segmento. Para editar um segmento, selecione um segmento na [lista de segmentos](/help/sites-administering/segmentation.md#accessing-segments) e clique no botão **Editar** .

![editor de segmentos](assets/segmenteditor.png)

Usando o navegador de componentes, você pode adicionar contêineres **AND** e **OR** para definir a lógica do segmento, em seguida, adicionar componentes adicionais para comparar propriedades e valores ou scripts de referência e outros segmentos para definir os critérios de seleção (consulte [Criação de um novo segmento](#creating-a-new-segment)) para definir o cenário exato para a seleção do segmento.

Quando a declaração inteira for avaliada como true, o segmento será resolvido. Se vários segmentos forem aplicáveis, o fator de **aumento** também será usado. Consulte [Criação de um novo segmento](#creating-a-new-segment) para obter detalhes sobre o fator de [aumento.](/help/sites-administering/campaign-segmentation.md#boost-factor)

>[!CAUTION]
>
>O editor de segmentos não verifica se há referências circulares. Por exemplo, o segmento A faz referência a outro segmento B, que por sua vez faz referência ao segmento A. É necessário garantir que seus segmentos não contenham nenhuma referência circular.

### Containers {#containers}

Os seguintes contêineres estão disponíveis prontamente e permitem agrupar comparações e referências para avaliação booleana. Eles podem ser arrastados do navegador de componentes para o editor. Consulte a seção a seguir [Usando contêineres E e OU](/help/sites-administering/segmentation.md#using-and-and-or-containers) para obter mais informações.

<table>
 <tbody>
  <tr>
   <td>Contêiner E<br /> </td>
   <td>O operador AND booleano<br /> </td>
  </tr>
  <tr>
   <td>Contêiner OU<br /> </td>
   <td>O operador OR booleano</td>
  </tr>
 </tbody>
</table>

### Comparações {#comparisons}

As seguintes comparações de segmentos estão disponíveis prontamente para avaliar as propriedades do segmento. Eles podem ser arrastados do navegador de componentes para o editor.

<table>
 <tbody>
  <tr>
   <td>Valor da propriedade<br /> </td>
   <td>Compara uma propriedade de uma loja com um valor definido<br /> </td>
  </tr>
  <tr>
   <td>Propriedade-Propriedade</td>
   <td>Compara uma propriedade de uma loja com outra propriedade<br /> </td>
  </tr>
  <tr>
   <td>Referência do segmento de propriedade</td>
   <td>Compara uma propriedade de uma loja com outro segmento referenciado<br /> </td>
  </tr>
  <tr>
   <td>Referência do script de propriedade</td>
   <td>Compara uma propriedade de uma loja com os resultados de um script<br /> </td>
  </tr>
  <tr>
   <td>Referência do segmento - Referência do script</td>
   <td>Compara um segmento referenciado com os resultados de um script<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Ao comparar valores, se o tipo de dados da comparação não estiver definido (isto é, definido para detecção automática), o mecanismo de segmentação do ContextHub simplesmente comparará os valores como javascript faria. Não converte valores em seus tipos esperados, o que pode levar a resultados enganosos. Por exemplo:
>
>`null < 30 // will return true`
>
>Portanto, ao [criar um segmento](/help/sites-administering/segmentation.md#creating-a-new-segment), você deve selecionar um tipo **de** dados sempre que os tipos de valores comparados forem conhecidos. Por exemplo:
>
>Ao comparar a propriedade `profile/age`, você já sabe que o tipo comparado será **número**, portanto, mesmo que não `profile/age` esteja definido, uma comparação `profile/age` menor que 30 retornará **falso**, como você esperaria.

### Referências {#references}

As referências a seguir estão disponíveis prontamente para vinculação direta a um script ou outro segmento. Eles podem ser arrastados do navegador de componentes para o editor.

<table>
 <tbody>
  <tr>
   <td>Referência do segmento<br /> </td>
   <td>Avaliar o segmento referenciado</td>
  </tr>
  <tr>
   <td>Referência de scripts</td>
   <td>Avalie o script referenciado. Consulte a seção a seguir <a href="/help/sites-administering/segmentation.md#using-script-references">Usando referências</a> de script para obter mais informações.</td>
  </tr>
 </tbody>
</table>

## Criação de um novo segmento {#creating-a-new-segment}

Para definir seu novo segmento:

1. Depois de [acessar os segmentos](/help/sites-administering/segmentation.md#accessing-segments), clique ou toque no botão Criar e selecione **Criar segmento** do ContextHub.

   ![chlimage_1-311](assets/chlimage_1-311.png)

1. No **Novo segmento** ContextHub, digite um título para o segmento, bem como um valor de aumento, se necessário, e toque ou clique em **Criar**.

   ![chlimage_1-312](assets/chlimage_1-312.png)

   Cada segmento tem um parâmetro de aumento que é usado como fator de ponderação. Um número mais alto indica que o segmento será selecionado de preferência a um segmento com um número menor em instâncias onde vários segmentos são válidos.

   * Minimum value: `0`
   * Maximum value: `1000000`

1. Arraste uma comparação ou referência para o editor de segmentos que aparecerá no contêiner AND padrão.
1. Clique duas vezes ou toque na opção de configuração da nova referência ou segmento para editar os parâmetros específicos. Neste exemplo, estamos testando pessoas em San Jose.

   ![screen_shot_2012-02-02at103135am](assets/screen_shot_2012-02-02at103135ama.png)

   Sempre defina um Tipo **de** dados, se possível, para garantir que suas comparações sejam avaliadas corretamente. Consulte [Comparações](/help/sites-administering/segmentation.md#comparisons) para obter mais informações.

1. Click **OK** to save your definition:
1. Adicione mais componentes conforme necessário. Você pode formular expressões booleanas usando os componentes do contêiner para comparações E e OU (consulte [Usando contêineres](/help/sites-administering/segmentation.md#using-and-and-or-containers) E e Ou abaixo). Com o editor de segmentos, é possível excluir componentes que não são mais necessários ou arrastá-los para novas posições na declaração.

### Uso de contêineres E e OU {#using-and-and-or-containers}

Usando os componentes de contêiner AND e OR, é possível construir segmentos complexos no AEM. Ao fazer isso, ajuda a ter em mente alguns pontos básicos:

* O nível superior da definição é sempre o contêiner AND criado inicialmente. Isso não pode ser alterado, mas não afeta o restante da definição do segmento.
* Verifique se o aninhamento do contêiner faz sentido. Os contêineres podem ser exibidos como colchetes da sua expressão booleana.

O exemplo a seguir é usado para selecionar visitantes que são considerados em nosso grupo principal:

Masculino e entre os 30 e os 59 anos

OU

Feminino com idade entre 30 e 59 anos

Você começa colocando um componente de contêiner OR no contêiner AND padrão. No contêiner OR, você adiciona dois contêineres AND e em ambos é possível adicionar a propriedade ou os componentes de referência.

![screen_shot_2012-02-02at105145am](assets/screen_shot_2012-02-02at105145ama.png)

### Uso de referências de script {#using-script-references}

Usando o componente de Referência de script, a avaliação de uma propriedade de segmento pode ser delegada a um script externo. Depois que o script é configurado corretamente, ele pode ser usado como qualquer outro componente de uma condição de segmento.

#### Definição de um script para referência {#defining-a-script-to-reference}

1. Adicione o arquivo ao `contexthub.segment-engine.scripts` clientlib.
1. Implemente uma função que retorne um valor. Por exemplo:

   ```
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. Registre o script com `ContextHub.SegmentEngine.ScriptManager.register`.

Se o script depender de propriedades adicionais, ele deverá chamar `this.dependOn()`. Por exemplo, se o script depender de `profile/age`:

```
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### Referência a um script {#referencing-a-script}

1. Criar segmento ContextHub.
1. Adicione o componente de referência **de** script no local desejado do segmento.
1. Abra a caixa de diálogo de edição do componente Referência **de** script. Se [corretamente configurado](/help/sites-administering/segmentation.md#defining-a-script-to-reference), o script deverá estar disponível no menu suspenso de nome **do** Script.

## Teste da aplicação de um segmento {#testing-the-application-of-a-segment}

Depois que o segmento é definido, os resultados potenciais podem ser testados com a ajuda do **[ContextHub](/help/sites-authoring/ch-previewing.md).**

1. Visualizar uma página
1. Clique no ícone ContextHub para revelar a barra de ferramentas do ContextHub
1. Selecione uma pessoa que corresponda ao segmento criado
1. O ContextHub resolverá os segmentos aplicáveis para a persona selecionada

Por exemplo, nossa simples definição de segmento para identificar usuários em nosso grupo principal é uma simples definição de segmento com base na idade e no sexo do usuário. O carregamento de uma pessoa específica que corresponde a esses critérios mostra se o segmento foi resolvido com êxito:

![screen_shot_2012-02-02at105926am](assets/screen_shot_2012-02-02at105926am.png)

Ou se não for resolvido:

![screen_shot_2012-02-02at110019am](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>Todas as características são resolvidas imediatamente, embora a maioria só seja alterada no recarregamento da página.

Esses testes também podem ser executados em páginas de conteúdo e em combinação com conteúdo direcionado e **Atividades** e **Experiências** relacionadas.

Se você configurou uma atividade e experiência usando o exemplo de segmento de grupo de idade principal acima, você pode testar facilmente seu segmento com a atividade. Para obter detalhes sobre como configurar uma atividade, consulte a [documentação relacionada sobre como criar conteúdo](/help/sites-authoring/content-targeting-touch.md)direcionado.

1. No modo de edição de uma página onde você configurou o conteúdo direcionado, é possível ver que o conteúdo é direcionado por meio do ícone de seta no conteúdo.

   ![chlimage_1-313](assets/chlimage_1-313.png)

1. Alterne para o modo de visualização e, usando o hub de contexto, alterne para uma pessoa que não corresponde à segmentação configurada para a experiência.

   ![chlimage_1-314](assets/chlimage_1-314.png)

1. Alterne para uma pessoa que não corresponda à segmentação configurada para a experiência e veja se a experiência muda de acordo.

   ![chlimage_1-315](assets/chlimage_1-315.png)

## Usando seu segmento {#using-your-segment}

Os segmentos são usados para direcionar o conteúdo real visto por públicos-alvo específicos. Consulte [Gerenciamento de públicos-alvo](/help/sites-authoring/managing-audiences.md) para obter mais informações sobre públicos-alvo e segmentos e [Criação de conteúdo](/help/sites-authoring/content-targeting-touch.md) direcionado sobre como usar públicos-alvo e segmentos para direcionar o conteúdo.
