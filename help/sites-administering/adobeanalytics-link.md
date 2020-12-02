---
title: Configuração do rastreamento de links para Adobe Analytics
seo-title: Configuração do rastreamento de links para Adobe Analytics
description: Saiba mais sobre como configurar o rastreamento de links para o SiteCatalyst.
seo-description: Saiba mais sobre como configurar o rastreamento de links para o SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---


# Configurando o rastreamento de link para Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Quando os usuários clicam em links nas páginas do seu site, você pode capturar informações relacionadas no Adobe Analytics. Por exemplo, use o rastreamento de link para saber como os usuários interagem com seu site, rastrear downloads de arquivos e links de saída.

## Configurando o rastreamento de link para um Adobe Analytics Framework {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Usando **Navegação**, vá pela seção **Implantação**, **Cloud Services** até a seção **Adobe Analytics**.

1. Usando **Mostrar configurações**, abra a estrutura Adobe Analytics necessária.
1. Expanda a seção **Configuração de rastreamento de link** e configure conforme necessário (esta página fornece mais detalhes):

   ![aa-08](assets/aa-08.png)

## Acompanhamento de downloads de arquivos {#tracking-file-downloads}

Configure a estrutura do Adobe Analytics para que os arquivos baixados das páginas associadas sejam rastreados automaticamente como downloads no Adobe Analytics. Quando você ativa o rastreamento de downloads, somente os tipos de arquivos especificados são rastreados.

Por padrão, os downloads dos seguintes tipos de arquivo são rastreados:

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

Por exemplo, com o rastreamento de download ativado para arquivos PDF, sempre que os usuários clicam em links para arquivos PDF, o download do PDF é rastreado.

As propriedades de rastreamento de download da estrutura são implementadas como código no arquivo `analytics.sitecatalyst.js` gerado para uma página. A amostra de código a seguir representa a configuração padrão de rastreamento de download:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Para ativar o rastreamento de download para sua estrutura do Adobe Analytics:

1. [Abra a estrutura do Adobe Analytics e expanda a seção](#configuring-link-tracking-for-an-adobe-analytics-framework) Configuração de rastreamento de link.
1. Ative **Rastrear downloads**.
1. Na caixa **Baixar tipos de arquivo**, digite as extensões de nome de arquivo para os tipos de arquivos que você deseja rastrear.

## Rastrear links externos {#tracking-external-links}

Você pode rastrear os cliques de links externos (links de saída) em suas páginas.

Para rastrear links externos para sua estrutura do Adobe Analytics:

1. [Abra a estrutura do Adobe Analytics e expanda a seção  **Configuração de rastreamento de** link](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure as seguintes propriedades de acordo com seus requisitos.

Propriedades para rastreamento quando links externos são clicados:

* **Rastrear**
externoHabilita o rastreamento de link externo.

* **Filtros**
 externos (Opcional) Define filtros para corresponder aos URLs externos dos públicos alvos do link. Quando os públicos alvos de link correspondem ao filtro, o link é rastreado. Filtros externos são úteis para rastrear apenas alguns links externos em suas páginas.

   Para especificar os links externos a serem rastreados, digite todo o URL ou parte do URL do público alvo do link. Separe vários filtros com uma vírgula. Inclua literais de string entre aspas simples. Nenhum valor (o valor padrão de `''`, duas aspas simples) faz com que todos os links externos sejam rastreados.

* **Filtros internosDefine filtros para corresponder aos URLs de links internos.**
Quando o link público alvo URLs que correspondem a esse filtro, o link não é rastreado. O valor padrão é um comando javascript que retorna o nome do host do URL para o endereço da janela atual.

   Para especificar os links internos que não são rastreados, digite parte ou a totalidade do URL interno do público alvo do link. Separe vários filtros com uma vírgula. Inclua literais de string entre aspas simples.

   O valor padrão é `'javascript:,'+window.location.hostname`

* **Deixe o Query**
StringInclui parâmetros de URL ao avaliar correspondências com filtros internos e externos.

   Permita a inclusão de parâmetros de URL ao avaliar URLs de públicos alvos de links em relação a filtros externos e internos.

As propriedades de rastreamento de link externo são implementadas como código no arquivo `analytics.sitecatalyst.js` gerado para uma página. O código de exemplo a seguir é gerado para uma página associada a uma estrutura que habilitou o rastreamento de link externo com a seguinte configuração:

* O filtro externo é `'google.com'`
* O filtro interno é o valor padrão de `'javascript:,'+window.location.hostname`
* As strings de query não são incluídas ao avaliar o público alvo do link em relação aos filtros.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Envio de dados de variável com cliques em links {#sending-variable-data-with-link-clicks}

Você pode configurar AEM para enviar dados de eventos e variáveis à Adobe Analytics quando um usuário clicar em um link. As propriedades **Configuração de rastreamento de link** permitem que você especifique os eventos e as variáveis do Adobe Analytics para rastrear quando ocorrerem cliques em links.

Os mapeamentos de estrutura determinam os valores de evento e variável. Você pode mapear variáveis do Adobe Analytics para as variáveis dos componentes de conteúdo que armazenam os dados que deseja rastrear quando os links são clicados.

Para enviar dados variáveis com cliques em links:

1. [Abra a estrutura do Adobe Analytics e expanda a seção](#configuring-link-tracking-for-an-adobe-analytics-framework) Configuração de rastreamento de link.
1. Configure as seguintes propriedades de acordo com seus requisitos.

Propriedades para enviar dados variáveis com cliques em links:

* **Vincular**
eventos de rastreamentoDigite as variáveis do evento Adobe Analytics que você deseja usar para contar cliques em links.

   Separe vários nomes de variáveis com uma vírgula.

   O valor padrão de `None` não causa rastreamento de eventos.

* **Link Track**
VarsInsira as variáveis do Adobe Analytics que você deseja enviar para o Adobe Analytics quando os links forem clicados. Separe vários nomes de variáveis com uma vírgula.

   O valor padrão de `None` faz com que nenhum dado variável seja enviado.

Quando você especifica os eventos e as variáveis a serem enviados, a configuração é implementada como código no arquivo `analytics.sitecatalyst.js` que é gerado para uma página. O código de exemplo a seguir é gerado para uma página quando a estrutura rastreia o evento `event10` e a propriedade `prop4`:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Exemplo de configuração de rastreamento de link {#example-link-tracking-configuration}

Execute os seguintes procedimentos para explorar o comportamento de rastreamento de link da integração com o Adobe Analytics. Os procedimentos mostram os resultados do [Adobe Marketing Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).

### Configuração geral {#general-configuration}

Este exemplo ilustra como o mapeamento funciona no contexto do rastreamento e do depurador:

1. Abra a estrutura que foi associada a uma página da Web.
1. Arraste o componente **Page** para a área de mapeamentos da estrutura. O componente **Page** pertence ao grupo de componentes **Geral** no Sidekick.

   >[!NOTE]
   >
   >O componente que você deve usar em um cenário real depende do componente herdado (se for o caso).
   >
   >Caso contrário, você deve ter seu próprio componente exposto ali (definindo um subnó de análise em seu componente de página).

   Configure o mapeamento de acordo com a tabela a seguir, arrastando a variável do Analytics (SiteCatalyst) do painel lateral esquerdo:

<table>
 <tbody>
  <tr>
   <th>Variável CQ<br /> </th>
   <th>Entrada no navegador de variáveis<br /> </th>
   <th>Variável Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>EVar personalizado 1 (eVar 1)</td>
   <td>eVar 1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personalizado 1 (evento 1)</td>
   <td>evento1</td>
  </tr>
 </tbody>
</table>

1. Arraste o componente de Pesquisa para a área de mapeamentos da estrutura. O componente de Pesquisa pertence ao grupo de componentes Geral no Sidekick. Configure o mapeamento de acordo com a tabela a seguir, arrastando a variável do Analytics (SiteCatalyst) do painel lateral esquerdo:

<table>
 <tbody>
  <tr>
   <th>Variável CQ<br /> </th>
   <th>Entrada no navegador de variáveis</th>
   <th>Variável Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>EVar personalizado 2 (eVar 2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>EVar personalizado 3 (eVar 3)</td>
   <td>eVar 3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personalizado 2 (evento 2)</td>
   <td>evento2</td>
  </tr>
 </tbody>
</table>

### Configurar rastreamento de link externo {#configure-external-link-tracking}

1. Em sua estrutura, expanda a área **Configuração de rastreamento de link**.
1. Desmarque **Rastrear downloads**.

1. Selecione **Rastrear Externo**.
1. Desmarque **Sair da cadeia de caracteres do Query**.
1. Use o seguinte valor para a lista **Filtros externos** para identificá-la como um URL externo:

   `‘yahoo.com’`

1. Adicione o seguinte valor ao campo **Eventos de rastreamento de link**:

   ```
       event1,event2
   ```

1. Adicione o seguinte valor ao campo **Vincular vars de rastreamento**:

   ```
       eVar1,eVar2
   ```

1. Na página que está associada à estrutura, adicione um componente **Text**. No componente **Text**, adicione um hiperlink que aponte para o seguinte endereço:

   `https://search.yahoo.com/?p=this`

1. Alterne para **modo de Pré-visualização** e clique no link.

A chamada feita terá a seguinte aparência quando exibida com o Adobe Marketing Cloud Debugger:

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>O URL não contém a string de Query: `?p=this`

### Incluir o parâmetro de URL {#include-the-url-parameter}

1. Na estrutura, expanda a área **Configuração de rastreamento de link**.
1. Ative **Sair da cadeia de caracteres do Query**.
1. Recarregue a pré-visualização da página e clique no link.

Os detalhes da chamada que aparecem no Adobe Marketing Cloud Debugger são semelhantes ao seguinte exemplo:

![aa-leavequerysearch-ative](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Desta vez, o URL contém a string do Query: `?p=this`

## Rastreamento de link ad-hoc {#ad-hoc-link-tracking}

O rastreamento de link ad-hoc permite que autores de conteúdo configurem o rastreamento de link para um componente. A configuração do componente substitui a **Configuração de rastreamento de link** da estrutura, portanto, nas páginas associadas à estrutura, os componentes **Texto** podem ser configurados para rastreamento de links de URLs.

O rastreamento de link ad-hoc permite rastrear links de download, links externos, juntamente com dados de eventos e variáveis.

Para ativar o rastreamento de links ad-hoc, é necessário:

* [Associe a página que contém o  **** Textcomponent à estrutura](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configure a estrutura do Adobe Analytics para ativar o rastreamento](#enabling-ad-hoc-link-tracking) de links ad-hoc.
* [Configurar o rastreamento de link para um componente](#configuring-link-tracking-for-a-text-component) de texto.

### Habilitar rastreamento de link Ad-hoc {#enabling-ad-hoc-link-tracking}

Configure sua estrutura do Adobe Analytics para ativar o rastreamento de links ad-hoc.

1. Abra a estrutura do Adobe Analytics e expanda a seção **Configuração de rastreamento de link**.

1. Ative **Rastreamento de link ad-hoc**.

   >[!NOTE]
   >
   >Nem todos os tipos de usuários têm acesso a essa caixa de seleção. Entre em contato com o administrador do site se precisar de acesso.

>[!NOTE]
>
>A configuração do XSS Antisamy está agora no SLING no caminho **/libs/sling/xss.config.xml** e as seguintes regras precisam ser adicionadas para que a vinculação ad-hoc funcione:

#### Extensão da regra de tag âncora {#anchor-tag-rule-extension}

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

### Configurando o rastreamento de link para um componente de texto {#configuring-link-tracking-for-a-text-component}

Antes de configurar o rastreamento de link ad-hoc para os componentes **Text**, as seguintes configurações já devem ter sido implementadas:

* A estrutura [Adobe Analytics está configurada para ativar o rastreamento de link ad-hoc](#enabling-ad-hoc-link-tracking).
* A página [que contém o componente **Text** está associada à estrutura](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Use o seguinte procedimento para configurar o rastreamento de link para um componente **Text**:

1. Abra a página no modo de edição e edite o componente **Texto**.

1. Selecione o texto que deseja usar como hipertexto e clique no botão Hiperlink.

   ![](do-not-localize/chlimage_1.png)

1. Adicione o URL do público alvo na caixa Link para e expanda a área Rastreamento de link.

   >[!NOTE]
   >
   >O rastreamento de link personalizado é visível como uma ação separada, ao lado da ação Vincular/Desvincular (Ícone do Analytics).
   >
   >Ela só será ativada quando você tiver selecionado um Link válido no RTE.

   ![aa-17](assets/aa-17.png)

1. Ative **Acompanhamento de link personalizado** para substituir a configuração de rastreamento de link da estrutura do Adobe Analytics e ativar o rastreamento de link para o link atual.

1. (Opcional) Para rastrear eventos com o clique no link, adicione nomes de eventos Adobe Analytics no campo **Incluir variáveis Adobe Analytics**. Separe o nome de vários eventos com vírgulas, por exemplo

   `event1, event22`.

1. (Opcional) Para rastrear dados variáveis com o clique do link, adicione variáveis Adobe Analytics no campo **Incluir variáveis Adobe Analytics**. Use um dos seguintes formatos:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*:  *`‘CONSTANT'`*

   Os exemplos a seguir ilustram cada formato:

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   Separe vários valores com uma vírgula.

1. Selecione **OK**.

