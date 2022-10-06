---
title: Mapeamento de dados do componente com propriedades do Adobe Analytics
seo-title: Mapping Component Data with Adobe Analytics Properties
description: Saiba como mapear dados de componentes com propriedades de SiteCatalyst.
seo-description: Learn how to map component data with SiteCatalyst properties.
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 1%

---

# Mapeamento de dados do componente com propriedades do Adobe Analytics{#mapping-component-data-with-adobe-analytics-properties}

Adicione componentes à estrutura que coleta os dados para enviar ao Adobe Analytics. Os componentes projetados para coletar dados do Analytics armazenam os dados no **Variável CQ**. Quando você adiciona esse componente a uma estrutura, a estrutura exibe a lista de variáveis CQ para que você possa cada uma delas para as **Variável do Analytics**.

![aa-11](assets/aa-11.png)

Quando a variável **AEM exibição** é aberta e as variáveis do Analytics são exibidas no localizador de conteúdo.

![aa-12](assets/aa-12.png)

Você pode mapear várias variáveis do Analytics com o mesmo **Variável CQ**.

![chlimage_1-68](assets/chlimage_1-68.png)

Os dados mapeados são enviados para o Adobe Analytics quando a página é carregada e as seguintes condições são atendidas:

* A página está associada à estrutura.
* A página usa os componentes adicionados à estrutura.

Use o procedimento a seguir para mapear variáveis de componente CQ com propriedades de relatório do Adobe Analytics.

1. No **AEM exibição**, arraste um componente de rastreamento do sidekick para a estrutura. Por exemplo, arraste a **Página** componente do **Geral** categoria .

   ![aa-13](assets/aa-13.png)

   Há vários grupos de componentes padrão: **Geral**, **Comércio**, **Comunidades** e **Outras**. A instância de AEM pode ser configurada para exibir diferentes grupos e componentes.

1. Para mapear variáveis do Adobe Analytics com variáveis definidas no componente, arraste um **Variável do Analytics** do localizador de conteúdo para um campo no componente de rastreamento. Por exemplo, arraste `Page Name (pageName)` para `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >A ID do conjunto de relatórios (RSID) selecionada para a estrutura determina as variáveis do Adobe Analytics que aparecem no localizador de conteúdo.

1. Repita as duas etapas anteriores para outros componentes e variáveis.

   >[!NOTE]
   >
   >É possível mapear várias variáveis do Analytics (por exemplo, `props`, `eVars`, `events`) para a mesma variável CQ (por exemplo, `pagedata.title`)

   >[!CAUTION]
   >
   >Recomenda-se que:
   >
   >* `eVars` e `props` são mapeadas para variáveis CQ começando com `pagedata.X` ou `eventdata.X`
   >* considerando que os eventos devem ser mapeados para variáveis que começam com `eventdata.events.X`


1. Para disponibilizar a estrutura na instância de publicação do site, abra o **Página** guia do sidekick e clique em **Ativar Estrutura.**

## Mapeamento de variáveis relacionadas ao produto {#mapping-product-related-variables}

O AEM usa uma convenção para nomear variáveis relacionadas ao produto e eventos que devem ser mapeados para propriedades relacionadas ao produto do Adobe Analytics:

| Variável CQ | Variável do Analytics | Descrição |
|--- |--- |--- |
| `product.category` | `product.category` (variável de conversão) | A categoria do produto. |
| `product.sku` | `product.sku` (variável de conversão) | O SKU do produto. |
| `product.quantity` | `product.quantity` (variável de conversão) | O número de produtos que estão sendo comprados. |
| `product.price` | `product.price` (variável de conversão) | O preço do produto. |
| `product.events.<eventName>` | Os eventos bem-sucedidos para associar ao produto em seu relatório. | `product.events` é o prefixo de eventos nomeados *eventName.* |
| `product.evars.<eVarName>` | As variáveis(s) de conversão ( `eVar`) para associar ao produto. | `product.evars` é o prefixo das variáveis de eVar nomeadas *eVarName.* |

Vários componentes AEM Commerce usam esses nomes de variáveis.

>[!NOTE]
>
>Não mapeie a propriedade Produtos do Adobe Analytics para uma variável CQ. A configuração de mapeamentos relacionados ao produto, conforme descrito na tabela, equivale efetivamente ao mapeamento da variável Produtos.

### Verificação de relatórios no Adobe Analytics {#checking-reports-on-adobe-analytics}

1. Faça logon no site do Adobe Analytics usando as mesmas credenciais fornecidas ao AEM.
1. Certifique-se de que o RSID selecionado é o usado nas etapas anteriores.
1. Em **Relatórios** (no lado esquerdo da página) selecione **Conversão personalizada**, em seguida **Conversão personalizada 1-10** e selecione a variável correspondente a `eVar7`

1. Dependendo da versão do Adobe Analytics que você estiver usando, é necessário aguardar em média 45 minutos para que o relatório seja atualizado com o termo de pesquisa usado; Por exemplo, beringela no exemplo

## Uso do Localizador de conteúdo (cf#) com estruturas da Adobe Analytics {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

Inicialmente, ao abrir uma estrutura do Adobe Analytics, o localizador de conteúdo contém variáveis predefinidas do Analytics em:

* Tráfego
* Conversão
* Eventos

Quando um RSID é selecionado, todas as variáveis pertencentes a esse RSID são adicionadas à lista.\
O `cf#` é necessário para mapear variáveis do Analytics para as variáveis CQ presentes nos diferentes componentes de rastreamento. Consulte Configuração de uma estrutura para rastreamento básico.

Dependendo da exibição selecionada para a estrutura, o localizador de conteúdo será preenchido pelas variáveis do Analytics (na exibição AEM) ou CQ (na exibição do Analytics).

A lista pode ser manipulada das seguintes maneiras:

1. Quando em **AEM exibição**, a lista pode ser filtrada dependendo do tipo de variável selecionado usando os três botões de filtro:

   * If *botão sem* for selecionada, a lista mostrará a lista completa.
   * Se a variável **Tráfego** for selecionado, a lista mostrará apenas as variáveis pertencentes à seção Tráfego .
   * Se a variável **Conversão** for selecionado, a lista mostrará apenas as variáveis pertencentes à seção Conversão .
   * Se a variável **Eventos** for selecionado, a lista mostrará apenas as variáveis pertencentes à seção Events .

   >[!NOTE]
   >
   >Somente um botão de filtro pode estar ativo ao mesmo tempo.

   1. A lista também tem um recurso de pesquisa, que filtra os elementos de acordo com o texto inserido no campo de pesquisa.
   1. Se uma opção de filtro for ativada durante a pesquisa por elementos na lista, os resultados exibidos também serão filtrados de acordo com o botão ativo.
   1. A lista pode ser recarregada a qualquer momento usando o botão de setas giratórias.
   1. Se vários RSIDs forem selecionados na estrutura, todas as variáveis na lista serão exibidas usando todos os rótulos usados nos RSIDs selecionados.


1. Quando estiver na visualização do Adobe Analytics, o Localizador de conteúdo exibe todas as variáveis CQ pertencentes aos componentes de rastreamento arrastados na visualização CQ.

   * por exemplo, no caso de a variável **Baixar componente** é *somente um arrastado* na exibição CQ (que tem duas variáveis mapeáveis) *eventdata.downloadLink* e *eventdata.events.startDownload*), o Localizador de conteúdo terá esta aparência ao alternar para a exibição do Adobe Analytics:

   ![aa-22](assets/aa-22.png)

   * As variáveis podem ser arrastadas e soltas em qualquer variável do Adobe Analytics pertencente a uma das três seções da variável (**Tráfego**, **Conversão** e **Eventos**).

   * Ao arrastar um novo componente de rastreamento para a estrutura na exibição do CQ, as variáveis do CQ pertencentes ao componente são automaticamente adicionadas ao Localizador de conteúdo (cf#) na exibição do Adobe Analytics.
   >[!NOTE]
   >
   >Somente uma variável CQ pode ser mapeada para uma variável Adobe Analytics em qualquer momento.

## Uso da visualização AEM e do Analytics {#using-aem-view-and-analytics-view}

A qualquer momento, os usuários têm a opção de alternar entre duas maneiras de visualizar os mapeamentos do Adobe Analytics em uma página de estrutura. As 2 visualizações fornecem uma visão geral melhor dos mapeamentos dentro do quadro, a partir de duas perspectivas distintas.

### Exibição de AEM {#aem-view}

![aa-23](assets/aa-23.png)

Tomando a imagem acima como exemplo, a variável **AEM exibição** tem as seguintes propriedades:

1. Essa é a exibição padrão quando a estrutura é aberta.
1. Lado esquerdo: o localizador de conteúdo (cf#) é preenchido pelas variáveis do Adobe Analytics com base nos RSID(s) selecionados.
1. Cabeçalhos de tabulação (**AEM exibição** e **Exibição do Analytics**): use-os para alternar entre as duas exibições.

1. **Visualização AEM**:

   1. Se a estrutura tiver componentes herdados de seu pai, eles serão listados aqui, juntamente com as variáveis mapeadas para os componentes.

      1. Os componentes herdados estão bloqueados.
      1. Para desbloquear um componente herdado, clique duas vezes no cadeado ao lado do nome do componente
      1. Para reverter a herança, você deve excluir o componente desbloqueado; depois disso, recuperará seu status bloqueado.
   1. **Arraste os componentes aqui para incluí-los na estrutura de análise**: Os componentes podem ser arrastados do Sidekick e soltos aqui.
   1. Você pode encontrar todos os componentes incluídos atualmente na estrutura de análise:

      1. Para adicionar um componente, arraste um da guia Componentes do sidekick
      1. Para excluir um componente e todos os mapeamentos, selecione Excluir no menu de contexto do componente e aceite a exclusão na caixa de diálogo de confirmação.
      1. Lembre-se de que um componente só pode ser excluído da estrutura em que foi criado e não pode ser excluído das estruturas secundárias no sentido tradicional (elas só podem ser substituídas).


### Exibição do Analytics {#analytics-view}

![aa-24](assets/aa-24.png)

1. Essa exibição pode ser acessada ao alternar para a variável **Exibição do Analytics** na estrutura.
1. Lado esquerdo: Localizador de conteúdo (cf#) preenchido pelas variáveis CQ com base nos componentes arrastados para a estrutura na visualização CQ.
1. Cabeçalhos de tabulação (**AEM exibição** e **Exibição do Analytics**): use-os para alternar entre as duas exibições.

1. As três tabelas (Tráfego, Conversão, Evento) listam todas as variáveis disponíveis do Adobe Analytics. pertencente ao(s) RSID(s) selecionado(s). Os mapeamentos mostrados aqui devem ser os mesmos da exibição de AEM:

   * **Tráfego**:

      * Variável de tráfego ( `prop1`) mapeada para uma variável CQ ( `eventdata.downloadLink`)

      * Quando o componente tem um Cadeado ao lado dele, isso significa que ele é herdado de uma estrutura principal e, portanto, não pode ser editado
   * **Conversão**:

      * Variável de conversão ( `eVar1`) mapeada para uma variável CQ ( `pagedata.title`)

      * Variável de conversão ( `eVar3`) mapeado para uma expressão javascript adicionada em linha ao clicar duas vezes no campo da variável CQ e inserir o código manualmente
   * **Evento**:

      * Variável de evento ( `event1`) mapeado para um evento CQ ( `eventdata.events.pageView`)



>[!NOTE]
>
>A coluna de variável CQ de qualquer tabela também pode ser preenchida em linha, clicando duas vezes no campo e adicionando texto a ele. Esses campos aceitam o javascript como entrada.
>
>Por exemplo, ao lado de `prop3` você pode adicionar:
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
para enviar o *título* de uma página concatenada com seu *sitesection* usar *:* (dois pontos) e com prefixo *Adobe* as `prop3`

>[!CAUTION]
Somente uma variável CQ pode ser mapeada para uma variável Adobe Analytics em qualquer momento.
