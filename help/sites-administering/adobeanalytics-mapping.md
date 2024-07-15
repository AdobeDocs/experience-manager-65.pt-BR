---
title: Mapeamento de dados do componente com propriedades do Adobe Analytics
description: Saiba como mapear dados de componentes com propriedades do SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 0%

---

# Mapeamento de dados do componente com propriedades do Adobe Analytics{#mapping-component-data-with-adobe-analytics-properties}

Adicione componentes à estrutura que coletam os dados para enviar ao Adobe Analytics. Componentes projetados para coletar dados de análise e armazená-los na **variável CQ** apropriada. Ao adicionar esse componente a uma estrutura, ela exibe a lista de variáveis CQ para que cada uma delas possa ser adicionada à **variável do Analytics** apropriada.

![aa-11](assets/aa-11.png)

Quando a **exibição AEM** está aberta, as variáveis do Analytics são exibidas no localizador de conteúdo.

![aa-12](assets/aa-12.png)

Você pode mapear várias variáveis do Analytics com a mesma **variável CQ**.

![chlimage_1-68](assets/chlimage_1-68.png)

Os dados mapeados são enviados para o Adobe Analytics quando a página é carregada e as seguintes condições são atendidas:

* A página está associada à estrutura.
* A página usa os componentes adicionados à estrutura.

Use o procedimento a seguir para mapear variáveis de componente CQ com propriedades de relatório do Adobe Analytics.

1. Na **exibição AEM**, arraste um componente de rastreamento do sidekick para a estrutura. Por exemplo, arraste o componente **Página** da categoria **Geral**.

   ![aa-13](assets/aa-13.png)

   Há vários grupos de componentes padrão: **Geral**, **Commerce**, **Comunidades** e **Outros**. A instância do AEM pode ser configurada para exibir grupos e componentes diferentes.

1. Para mapear variáveis do Adobe Analytics com variáveis definidas no componente, arraste uma **variável do Analytics** do localizador de conteúdo para um campo no componente de rastreamento. Por exemplo, arraste `Page Name (pageName)` para `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >A ID do conjunto de relatórios (RSID) selecionada para a estrutura determina as variáveis do Adobe Analytics que aparecem no localizador de conteúdo.

1. Repita as duas etapas anteriores para outros componentes e variáveis.

   >[!NOTE]
   >
   >Você pode mapear várias variáveis do Analytics (por exemplo, `props`, `eVars`, `events`) para a mesma variável do CQ (por exemplo, `pagedata.title`)

   >[!CAUTION]
   >
   >É altamente recomendável que:
   >
   >* `eVars` e `props` estão mapeados para variáveis CQ começando com `pagedata.X` ou `eventdata.X`
   >* considerando que os eventos devem ser mapeados para variáveis que começam com `eventdata.events.X`

1. Para disponibilizar a estrutura na instância de publicação do seu site, abra a guia **Página** do sidekick e clique em **Ativar Estrutura.**

## Mapeamento de variáveis relacionadas ao produto {#mapping-product-related-variables}

O AEM usa uma convenção para nomear variáveis e eventos relacionados a produtos que devem ser mapeados para propriedades relacionadas a produtos do Adobe Analytics:

| Variável CQ | Variável do Analytics | Descrição |
|--- |--- |--- |
| `product.category` | `product.category` (variável de conversão) | A categoria do produto. |
| `product.sku` | `product.sku` (variável de conversão) | O SKU do produto. |
| `product.quantity` | `product.quantity` (variável de conversão) | O número de produtos sendo comprados. |
| `product.price` | `product.price` (variável de conversão) | O preço do produto. |
| `product.events.<eventName>` | Os eventos bem-sucedidos a serem associados ao produto em seu relatório. | `product.events` é o prefixo de eventos denominado *eventName.* |
| `product.evars.<eVarName>` | As variáveis de conversão ( `eVar`) a serem associadas ao produto. | `product.evars` é o prefixo das variáveis de eVar denominadas *eVarName.* |

Vários componentes do AEM Commerce usam esses nomes de variáveis.

>[!NOTE]
>
>Não mapeie a propriedade Produtos do Adobe Analytics para uma variável do CQ. Configurar mapeamentos relacionados ao produto conforme descrito na tabela é efetivamente equivalente a mapear a variável Products.

### Verificação de relatórios no Adobe Analytics {#checking-reports-on-adobe-analytics}

1. Faça logon no site da Adobe Analytics usando as mesmas credenciais fornecidas para o AEM.
1. Certifique-se de que a RSID selecionada é a utilizada nas etapas anteriores.
1. Em **Relatórios** (no lado esquerdo da página), selecione **Conversão personalizada**, depois **Conversão personalizada 1-10** e selecione a variável correspondente a `eVar7`

1. Dependendo da versão do Adobe Analytics que você está usando, é necessário aguardar em média 45 minutos para que o relatório seja atualizado com o termo de pesquisa usado; por exemplo, berinjela no exemplo

## Uso do Localizador de conteúdo (cf#) com estruturas Adobe Analytics {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

Inicialmente, ao abrir uma estrutura do Adobe Analytics, o localizador de conteúdo contém variáveis predefinidas do Analytics em:

* Tráfego
* Conversão
* Eventos

Quando uma RSID é selecionada, todas as variáveis pertencentes a essa RSID são adicionadas à lista.\
O `cf#` é necessário para mapear variáveis do Analytics para as variáveis CQ presentes nos diferentes componentes de rastreamento. Consulte Configuração de uma estrutura para rastreamento básico.

Dependendo da exibição selecionada para a estrutura, o localizador de conteúdo será preenchido pelas variáveis do Analytics (na exibição AEM) ou pelas variáveis CQ (na exibição do Analytics).

A lista pode ser manipulada das seguintes maneiras:

1. Quando estiver no **modo de exibição AEM**, a lista poderá ser filtrada, dependendo do tipo de variável selecionado com os três botões de filtro:

   * Se *nenhum botão* for selecionado, a lista mostrará a lista completa.
   * Se o botão **Tráfego** for selecionado, a lista mostrará somente as variáveis pertencentes à seção Tráfego.
   * Se o botão **Conversão** for selecionado, a lista mostrará somente as variáveis pertencentes à seção Conversão.
   * Se o botão **Eventos** estiver selecionado, a lista mostrará somente as variáveis pertencentes à seção Eventos.

   >[!NOTE]
   >
   >Somente um botão de filtro pode estar ativo de uma vez.

   1. A lista também tem um recurso de pesquisa, que filtra os elementos de acordo com o texto inserido no campo de pesquisa.
   1. Se uma opção de filtro estiver ativada ao procurar elementos na lista, os resultados exibidos também serão filtrados de acordo com o botão ativo.
   1. A lista pode ser recarregada a qualquer momento usando o botão de setas giratórias.
   1. Se várias RSIDs forem selecionadas na estrutura, todas as variáveis na lista serão exibidas usando todos os rótulos usados nas RSIDs selecionadas.

1. Quando estiver na exibição do Adobe Analytics, o Localizador de conteúdo exibe todas as variáveis CQ pertencentes aos componentes de rastreamento arrastados na exibição do CQ.

   * Por exemplo, caso o **componente de Download** seja o *único arrastado* na exibição do CQ (que tem duas variáveis mapeáveis *eventdata.downloadLink* e *eventdata.events.startDownload*), o Localizador de Conteúdo terá esta aparência ao alternar para a exibição do Adobe Analytics:

   ![aa-22](assets/aa-22.png)

   * As variáveis podem ser arrastadas e soltas em qualquer variável do Adobe Analytics que pertença a uma das três seções de variáveis (**Tráfego**, **Conversão** e **Eventos**).

   * Ao arrastar um novo componente de rastreamento para a estrutura na exibição do CQ, as variáveis do CQ pertencentes ao componente são adicionadas automaticamente ao Localizador de conteúdo (cf#) na exibição do Adobe Analytics.

   >[!NOTE]
   >
   >Somente uma variável do CQ pode ser mapeada para uma variável do Adobe Analytics em um determinado momento.

## Uso da visualização do AEM e do Analytics {#using-aem-view-and-analytics-view}

A qualquer momento, os usuários podem alternar entre duas maneiras de visualizar os mapeamentos do Adobe Analytics em uma página de estrutura. As duas visualizações fornecem uma melhor visão geral dos mapeamentos dentro da estrutura, a partir de duas perspectivas distintas.

### Visualização AEM {#aem-view}

![aa-23](assets/aa-23.png)

Usando a imagem acima como exemplo, a **exibição do AEM** tem as seguintes propriedades:

1. Essa é a exibição padrão quando a estrutura é aberta.
1. Lado esquerdo: o localizador de conteúdo (cf#) é preenchido pelas variáveis do Adobe Analytics com base nas RSID(s) selecionadas.
1. Cabeçalhos de guia (**exibição de AEM** e **exibição do Analytics**): use-os para alternar entre as duas exibições.

1. **exibição do AEM**:

   1. Se a estrutura tiver componentes herdados de seu pai, eles serão listados aqui, juntamente com as variáveis mapeadas para os componentes.

      1. Os componentes herdados estão bloqueados.
      1. Para desbloquear um componente herdado, clique duas vezes no cadeado ao lado do nome do componente
      1. Para reverter a herança, exclua o componente desbloqueado; depois disso, ele recuperará o status de bloqueado.

   1. **Arraste componentes aqui para incluí-los na estrutura de análise**: os componentes podem ser arrastados do Sidekick e soltos aqui.
   1. Você pode encontrar todos os componentes incluídos atualmente na estrutura de análise:

      1. Para adicionar um componente, arraste um da guia Componentes do sidekick
      1. Para excluir um componente e todos os seus mapeamentos, selecione Excluir no menu de contexto do componente e aceite a exclusão na caixa de diálogo de confirmação.
      1. Lembre-se de que um componente só pode ser excluído da estrutura em que foi criado e não pode ser excluído de estruturas secundárias no sentido tradicional (eles só podem ser substituídos).

### Exibição do Analytics {#analytics-view}

![aa-24](assets/aa-24.png)

1. Esta exibição pode ser acessada alternando para a guia **Exibição do Analytics** na estrutura.
1. Lado esquerdo: Localizador de conteúdo (cf#) preenchido por variáveis do CQ com base nos componentes arrastados para a estrutura na exibição do CQ.
1. Cabeçalhos de guia (**exibição de AEM** e **exibição do Analytics**): use-os para alternar entre as duas exibições.

1. As três tabelas (Tráfego, Conversão, Evento) listam todas as variáveis do Adobe Analytics disponíveis. pertencentes às RSIDs selecionadas. Os mapeamentos mostrados aqui devem ser os mesmos da exibição AEM:

   * **Tráfego**:

      * Variável de tráfego ( `prop1`) mapeada para uma variável do CQ ( `eventdata.downloadLink`)

      * Quando o componente tem um Cadeado ao lado dele, significa que é herdado de uma estrutura principal e, portanto, não pode ser editado

   * **Conversão**:

      * Variável de conversão ( `eVar1`) mapeada para uma variável do CQ ( `pagedata.title`)

      * Variável de conversão ( `eVar3`) mapeada para uma expressão JavaScript adicionada em linha ao clicar duas vezes no campo de variável CQ e inserir o código manualmente

   * **Evento**:

      * Variável de evento ( `event1`) mapeada para um evento CQ ( `eventdata.events.pageView`)

>[!NOTE]
>
>A coluna da variável CQ de qualquer tabela também pode ser preenchida em linha, clicando duas vezes no campo e adicionando texto a ele. Esses campos aceitam o JavaScript como uma entrada.
>
>Por exemplo, próximo a `prop3` você pode adicionar:
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
>para enviar o *título* de uma página concatenada com sua *seção de site* usando *:* (dois pontos) e com o prefixo *Adobe* como `prop3`
>

>[!CAUTION]
>
>Somente uma variável do CQ pode ser mapeada para uma variável do Adobe Analytics em um determinado momento.
