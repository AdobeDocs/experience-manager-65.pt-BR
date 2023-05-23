---
title: Configuração do rastreamento de links para o Adobe Analytics
seo-title: Configuring Link Tracking for Adobe Analytics
description: Saiba como configurar o rastreamento de links para o SiteCatalyst.
seo-description: Learn about configuring link tracking for SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 1%

---

# Configuração do rastreamento de links para o Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Quando os usuários clicam em links nas páginas do seu site, você pode capturar informações relacionadas no Adobe Analytics. Por exemplo, use o rastreamento de link para saber como os usuários interagem com o seu site, rastreie downloads de arquivos e rastreie links de saída.

## Configuração do rastreamento de links para uma estrutura do Adobe Analytics {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Usar **Navegação**, ir via **Implantação**, **Cloud Services** para o **Adobe Analytics** seção.

1. Usar **Exibir configurações**, abra a estrutura necessária do Adobe Analytics.
1. Expanda a **Configuração de rastreamento de link** e configure conforme necessário (esta página fornece mais detalhes):

   ![aa-08](assets/aa-08.png)

## Rastreamento de downloads de arquivos {#tracking-file-downloads}

Configure a estrutura do Adobe Analytics para que os arquivos baixados de páginas associadas sejam rastreados automaticamente como downloads no Adobe Analytics. Quando você habilita o rastreamento de downloads, somente os tipos de arquivo especificados são rastreados.

Os downloads dos seguintes tipos de arquivos são rastreados por padrão:

* exe
* zip
* wav
* mp3
* mov
* mpg
* avi
* wmv
* doc
* pdf
* xls

Por exemplo, com o rastreamento de download habilitado para arquivos PDF, sempre que os usuários clicam em links para arquivos PDF, o download do PDF é rastreado.

As propriedades de rastreamento de download da estrutura são implementadas como código na `analytics.sitecatalyst.js` arquivo gerado para uma página. A amostra de código a seguir representa a configuração padrão de rastreamento de download:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Para ativar o rastreamento de download para sua estrutura do Adobe Analytics:

1. [Abra a estrutura do Adobe Analytics e expanda a seção Configuração de rastreamento de link](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Ativar **Rastrear downloads**.
1. No **Fazer download dos tipos de arquivo** digite as extensões de nome de arquivo para os tipos de arquivos que deseja rastrear.

## Rastreamento de links externos {#tracking-external-links}

Você pode rastrear o clique em links externos (links de saída) nas suas páginas.

Para rastrear links externos para sua estrutura do Adobe Analytics:

1. [Abra a estrutura do Adobe Analytics e expanda a **Configuração de rastreamento de link** seção](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure as propriedades a seguir de acordo com seus requisitos.

Propriedades para rastrear quando links externos são clicados:

* **Rastrear externo**
Ativa o rastreamento de links externos.

* **Filtros externos**
(Opcional) Define filtros para corresponder aos URLs externos dos destinos de links. Quando os destinos do link correspondem ao filtro, o link é rastreado. Os filtros externos são úteis para rastrear apenas alguns dos links externos nas suas páginas.

   Para especificar os links externos a serem rastreados, digite todo o URL ou parte do destino do link. Separe vários filtros com uma vírgula. Coloque os literais de string entre aspas simples. Nenhum valor (o valor padrão de `''`, duas aspas simples) faz com que todos os links externos sejam rastreados.

* **Filtros internos**
Define filtros para corresponder aos URLs de links internos. Quando o link é direcionado a URLs que correspondem a esse filtro, o link não é rastreado. O valor padrão é um comando javascript que retorna o nome do host do URL do endereço da janela atual.

   Para especificar os links internos que não são rastreados, digite todo o URL interno do destino do link ou parte dele. Separe vários filtros com uma vírgula. Coloque os literais de string entre aspas simples.

   O valor padrão é `'javascript:,'+window.location.hostname`

* **Deixar sequência de consulta**
Inclui parâmetros de URL ao avaliar correspondências com filtros internos e externos.

   Permite incluir parâmetros de URL ao avaliar URLs de destino de link em relação a filtros externos e internos.

As propriedades de rastreamento de link externo são implementadas como código no `analytics.sitecatalyst.js` arquivo gerado para uma página. O código de exemplo a seguir é gerado para uma página associada a uma estrutura que ativou o rastreamento de links externos com a seguinte configuração:

* O filtro externo é `'google.com'`
* O filtro interno é o valor padrão de `'javascript:,'+window.location.hostname`
* As sequências de consulta não são incluídas ao avaliar o destino do link em relação aos filtros.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Envio de dados variáveis com cliques em links {#sending-variable-data-with-link-clicks}

Você pode configurar o AEM para enviar dados de eventos e variáveis para o Adobe Analytics quando um usuário clicar em um link. A variável **Configuração de rastreamento de link** As propriedades permitem que você especifique os eventos e as variáveis do Adobe Analytics a serem rastreados quando ocorrerem cliques em links.

Os mapeamentos da estrutura determinam o evento e os valores da variável. Você pode mapear variáveis do Adobe Analytics para as variáveis dos componentes de conteúdo que armazenam os dados que você deseja rastrear quando os links são clicados.

Para enviar dados variáveis com cliques em links:

1. [Abra a estrutura do Adobe Analytics e expanda a seção Configuração de rastreamento de link](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure as propriedades a seguir de acordo com seus requisitos.

Propriedades para enviar dados variáveis com cliques em links:

* **Vincular eventos de rastreamento**
Insira as variáveis de evento do Adobe Analytics que deseja usar para contar cliques em links.

   Separe vários nomes de variáveis com uma vírgula.

   O valor padrão de `None` não causa nenhum rastreamento de evento.

* **Vars de rastreamento de link**
Insira as variáveis do Adobe Analytics que você deseja enviar para o Adobe Analytics quando os links forem clicados. Separe vários nomes de variáveis com uma vírgula.

   O valor padrão de `None` faz com que nenhum dado variável seja enviado.

Quando você especifica os eventos e as variáveis a serem enviados, a configuração é implementada como código na `analytics.sitecatalyst.js` arquivo gerado para uma página. O código de exemplo a seguir é gerado para uma página quando a estrutura rastreia a variável `event10` e o evento `prop4` propriedade:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Exemplo de configuração de rastreamento de link {#example-link-tracking-configuration}

Execute os procedimentos a seguir para explorar o comportamento de rastreamento de link da integração do Adobe Analytics. Os procedimentos mostram resultados de [Adobe Marketing Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

### Configuração geral {#general-configuration}

Este exemplo ilustra como o mapeamento funciona no contexto do rastreamento e do depurador:

1. Abra a estrutura que foi associada a uma página da Web.
1. Arraste o **Página** componente à área mapeamentos da estrutura. A variável **Página** o componente pertence à **Geral** grupo de componentes no Sidekick.

   >[!NOTE]
   >
   >O componente que você deve usar em um cenário da vida real depende do componente herdado de (se for o caso).
   >
   >Caso contrário, você deve ter seu próprio componente exposto lá (definindo um subnó do Analytics em seu componente de página).

   Configure o mapeamento de acordo com a tabela a seguir, arrastando a variável do Analytics (SiteCatalyst) do painel lateral esquerdo:

<table>
 <tbody>
  <tr>
   <th>Variável CQ<br /> </th>
   <th>Entrada no navegador de variáveis<br /> </th>
   <th>Variável do Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>EVar Personalizado 1 (eVar 1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personalizado 1 (event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Arraste o componente Pesquisa para a área mapeamentos da estrutura. O componente de Pesquisa pertence ao grupo de componentes Geral no Sidekick. Configure o mapeamento de acordo com a tabela a seguir, arrastando a variável do Analytics (SiteCatalyst) do painel lateral esquerdo:

<table>
 <tbody>
  <tr>
   <th>Variável CQ<br /> </th>
   <th>Entrada no navegador de variáveis</th>
   <th>Variável do Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>EVar personalizado 2 (eVar 2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>EVar Personalizado 3 (eVar 3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personalizado 2 (event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configurar o rastreamento de link externo {#configure-external-link-tracking}

1. Em sua estrutura, expanda a variável **Configuração de rastreamento de link** área.
1. Desmarcar **Rastrear downloads**.

1. Selecionar **Rastrear externo**.
1. Desmarcar **Deixar sequência de consulta**.
1. Use o seguinte valor para o **Filtros externos** para identificá-la como um URL externo:

   `‘yahoo.com’`

1. Adicione o seguinte valor ao **Vincular eventos de rastreamento** campo:

   ```
       event1,event2
   ```

1. Adicione o seguinte valor ao **Vincular vars de rastreamento** campo:

   ```
       eVar1,eVar2
   ```

1. Na página associada à estrutura, adicione uma **Texto** componente. Dentro do **Texto** adicione um hiperlink que aponte para o seguinte endereço:

   `https://search.yahoo.com/?p=this`

1. Alternar para **Modo de visualização** e clique no link.

A chamada feita terá esta aparência quando visualizada com o Adobe Marketing Cloud Debugger:

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>O URL não contém a sequência de consulta: `?p=this`

### Incluir o parâmetro de URL {#include-the-url-parameter}

1. Na estrutura, expanda a variável **Configuração de rastreamento de link** área.
1. Ativar **Deixar sequência de consulta**.
1. Recarregue a visualização da página e clique no link.

Os detalhes da chamada exibidos no Adobe Marketing Cloud Debugger são semelhantes ao seguinte exemplo:

![aa-leavequerysearch-ative](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Desta vez, o URL não contém a sequência de consulta: `?p=this`

## Rastreamento de link ad-hoc {#ad-hoc-link-tracking}

O rastreamento de link ad-hoc permite que os autores de conteúdo configurem o rastreamento de link para um componente. A configuração do componente substitui a configuração **Configuração de rastreamento de link** do framework, por exemplo, em páginas associadas ao framework, **Texto** Os componentes do podem ser configurados para rastreamento de link de URLs.

O rastreamento de link ad-hoc permite rastrear links de download, links externos, juntamente com dados de evento e variáveis.

Para habilitar o rastreamento de link ad-hoc, é necessário:

* [Associe a página que contém o **Texto** componente com a estrutura](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configure a estrutura do Adobe Analytics para habilitar o rastreamento de link ad-hoc](#enabling-ad-hoc-link-tracking).
* [Configurar o rastreamento de links para um componente de Texto](#configuring-link-tracking-for-a-text-component).

### Ativar o rastreamento de link ad-hoc {#enabling-ad-hoc-link-tracking}

Configure sua estrutura do Adobe Analytics para ativar o rastreamento de links ad-hoc.

1. Abra a estrutura do Adobe Analytics e expanda a **Configuração de rastreamento de link** seção.

1. Ativar **Rastreamento de link ad-hoc**.

   >[!NOTE]
   >
   >Nem todos os tipos de usuários têm acesso a essa caixa de seleção. Entre em contato com o administrador do site se precisar de acesso.

>[!NOTE]
>
>A configuração do XSS Antisamy agora está no SLING no caminho **/libs/sling/xss.config.xml** e as seguintes regras precisam ser adicionadas a para que a vinculação ad hoc funcione:

#### Extensão de regra de tag de âncora {#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### Configuração do rastreamento de links para um componente de Texto {#configuring-link-tracking-for-a-text-component}

Antes de configurar o rastreamento de link ad-hoc para o **Texto** componentes, as seguintes configurações já devem ter sido implementadas:

* A variável [A estrutura do Adobe Analytics está configurada para habilitar o rastreamento de link ad-hoc](#enabling-ad-hoc-link-tracking).
* A variável [página que contém a **Texto** está associado à estrutura](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Use o procedimento a seguir para configurar o rastreamento de links para um **Texto** componente:

1. Abra a página no modo de edição e edite o **Texto** componente.

1. Selecione o texto que deseja usar como hipertexto e clique no botão Hiperlink.

   ![](do-not-localize/chlimage_1.png)

1. Adicione o URL de destino na caixa Link para e expanda a área Rastreamento de link.

   >[!NOTE]
   >
   >O rastreamento de link personalizado está visível como uma ação separada, ao lado da ação Vincular/Desvincular (ícone do Analytics).
   >
   >Ele só será ativado quando você selecionar um link válido no RTE.

   ![aa-17](assets/aa-17.png)

1. Ativar **Rastreamento de link personalizado** para substituir a configuração de rastreamento de link da estrutura do Adobe Analytics e ativar o rastreamento de link para o link atual.

1. (Opcional) Para rastrear eventos com o clique em links, adicione nomes de eventos do Adobe Analytics na **Incluir variáveis do Adobe Analytics** campo. Separe o nome de vários eventos com vírgulas, por exemplo

   `event1, event22`.

1. (Opcional) Para rastrear dados de variáveis com o clique em links, adicione variáveis do Adobe Analytics no **Incluir variáveis do Adobe Analytics** campo. Use um dos seguintes formatos:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`‘CONSTANT'`*

   Os exemplos a seguir ilustram cada formato:

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   Separe vários valores com uma vírgula.

1. Selecionar **OK**.
