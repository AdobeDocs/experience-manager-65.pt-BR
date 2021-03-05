---
title: Renderização de SPAs e do servidor
seo-title: Renderização de SPAs e do servidor
description: 'null'
seo-description: 'null'
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
translation-type: tm+mt
source-git-commit: 41e30a668c8c02f2c43e509ed708c4b9fa39a269
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 1%

---


# Renderização de SPA e do servidor{#spa-and-server-side-rendering}

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do lado do cliente com base na estrutura do SPA (por exemplo, Reagir ou Angular).

>[!NOTE]
>
>O AEM 6.5.1.0 ou posterior é necessário para usar os recursos de renderização do lado do servidor SPA, conforme descrito neste documento.

## Visão geral {#overview}

Aplicativos de página única (SPAs) podem oferecer ao usuário uma experiência rica e dinâmica que reage e se comporta de formas familiares, geralmente como um aplicativo nativo. [Isso é feito contando com o cliente para carregar o conteúdo antecipadamente e, em seguida, fazer o trabalho pesado de lidar com a ](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) interação do usuário e, assim, minimizar a quantidade de comunicação necessária entre o cliente e o servidor, tornando o aplicativo mais reativo.

No entanto, isso pode levar a tempos de carregamento iniciais mais longos, especialmente se o SPA for grande e rico em seu conteúdo. Para otimizar os tempos de carregamento, parte do conteúdo pode ser renderizado no lado do servidor. O uso da renderização do lado do servidor (SSR) pode acelerar a carga inicial da página e, em seguida, transmitir mais renderização para o cliente.

## Quando utilizar o SSR {#when-to-use-ssr}

A RSS não é necessária em todos os projetos. Embora o AEM seja totalmente compatível com JS SSR para SPA, a Adobe não recomenda implementá-lo sistematicamente para cada projeto.

Ao decidir implementar a SSR, você deve primeiro estimar qual complexidade adicional, esforço e custo adicional a SSR representa realisticamente para o projeto, incluindo a manutenção de longo prazo. Uma arquitetura RSS só deve ser escolhida quando o valor acrescentado exceder claramente os custos estimados.

O SSR geralmente fornece algum valor quando há um claro &quot;sim&quot; para qualquer uma das seguintes perguntas:

* **SEO:** o SSR ainda é necessário para que seu site seja indexado corretamente pelos mecanismos de pesquisa que trazem tráfego? Lembre-se de que os principais rastreadores de mecanismo de pesquisa agora avaliam o JS.
* **Velocidade da página:** o SSR fornece uma melhoria de velocidade mensurável em ambientes reais e adiciona à experiência geral do usuário?

Somente quando pelo menos uma dessas duas perguntas for respondida com um &quot;sim&quot; claro para o seu projeto a Adobe recomenda a implementação do SSR. As seções a seguir descrevem como fazer isso usando a Adobe I/O Runtime.

## Tempo de execução do Adobe I/O {#adobe-i-o-runtime}

Se você [estiver confiante de que seu projeto requer a implementação do SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), a solução recomendada da Adobe é usar o Adobe I/O Runtime.

Para obter mais informações sobre o Adobe I/O Runtime, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  - para obter uma visão geral do serviço
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  - para obter a documentação detalhada sobre a plataforma

As seções a seguir detalham como o Adobe I/O Runtime pode ser usado para implementar o SSR para seu SPA em dois modelos diferentes:

* [Fluxo de comunicação orientado pelo AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Fluxo de comunicação orientado por tempo de execução de E/S da Adobe](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>A Adobe recomenda uma instância separada da Adobe I/O Runtime para cada ambiente AEM (autor, publicação, estágio etc.).

## Configuração do Renderizador Remoto {#remote-renderer-configuration}

O AEM deve saber onde o conteúdo renderizado remotamente pode ser recuperado. Independentemente de [qual modelo você escolhe implementar para SSR,](#adobe-i-o-runtime) você precisará especificar para o AEM como acessar esse serviço de renderização remota.

Isso é feito por meio do **RemoteContentRenderer - Serviço OSGi de Fábrica de Configuração**. Procure a string &quot;RemoteContentRenderer&quot; no console Configuração do console da Web em `http://<host>:<port>/system/console/configMgr`.

![Configuração do renderizador](assets/rendererconfig.png)

Os seguintes campos estão disponíveis para a configuração:

* **Padrão de caminho de conteúdo**  - Expressão regular para corresponder a uma parte do conteúdo, se necessário
* **URL do endpoint remoto**  - URL do endpoint responsável pela geração do conteúdo
   * Use o protocolo HTTPS seguro se não estiver na rede local.
* **Cabeçalhos de solicitação adicionais**  - Cabeçalhos adicionais a serem adicionados à solicitação enviada ao endpoint remoto
   * Padrão: `key=value`
* **Tempo limite da solicitação**  - Tempo limite da solicitação do host remoto em milissegundos

>[!NOTE]
>
>Independentemente de você optar por implementar o [fluxo de comunicação orientado pelo AEM](#aem-driven-communication-flow) ou o [fluxo orientado pelo Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) você deve definir uma configuração de renderizador de conteúdo remoto.
>
>Essa configuração também deve ser definida se você optar por [usar um servidor Node.js personalizado.](#using-node-js)

>[!NOTE]
>
>Essa configuração aproveita o [Renderizador de conteúdo remoto,](#remote-content-renderer) que tem opções adicionais de extensão e personalização disponíveis.

## Fluxo de comunicação orientado pelo AEM {#aem-driven-communication-flow}

Ao usar o SSR, o [fluxo de trabalho de interação do componente](/help/sites-developing/spa-overview.md#workflow) de SPAs no AEM inclui uma fase na qual o conteúdo inicial do aplicativo é gerado na Adobe I/O Runtime.

1. O navegador solicita o conteúdo SSR do AEM.

1. O AEM posta o modelo para a Adobe I/O Runtime.

1. O Adobe I/O Runtime retorna o conteúdo gerado.

1. O AEM serve o HTML retornado pelo Adobe I/O Runtime por meio do modelo HTL do componente de página de back-end.

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Fluxo de comunicação orientado pela Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

A seção anterior descreve a implementação padrão e recomendada da renderização do lado do servidor com relação aos SPAs no AEM, onde o AEM executa o bootstrapping e o fornecimento de conteúdo.

Como alternativa, o SSR pode ser implementado para que o Adobe I/O Runtime seja responsável pelo bootstrapping, revertendo efetivamente o fluxo de comunicação.

Ambos os modelos são válidos e compatíveis com o AEM. No entanto, deve-se considerar as vantagens e desvantagens de cada um antes de implementar um modelo específico.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <th><strong>via AEM</strong><br /> </th>
   <td>
    <ul>
     <li>O AEM gerencia bibliotecas injetáveis onde for necessário</li>
     <li>Os recursos só precisam ser mantidos no AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possivelmente desconhecido do desenvolvedor do SPA<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Mais familiar aos desenvolvedores de SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Os recursos clientlib exigidos pelo aplicativo, como CSS e JavaScript, precisarão ser disponibilizados pelo desenvolvedor do AEM por meio da propriedade <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code><br /> </li>
     <li>Os recursos devem ser sincronizados entre o AEM e o Adobe I/O Runtime<br /> </li>
     <li>Para habilitar a criação do SPA, pode ser necessário um servidor proxy para a Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planejamento para SSR {#planning-for-ssr}

Geralmente, apenas parte de um aplicativo precisa ser renderizada no lado do servidor. O exemplo comum é o conteúdo que será exibido acima da dobra no carregamento inicial da página que é renderizada no lado do servidor. Isso economiza tempo fornecendo ao cliente conteúdo já renderizado. Conforme o usuário interage com o SPA, o conteúdo adicional é renderizado pelo cliente.

Ao considerar a implementação da renderização do lado do servidor para seu SPA, é necessário verificar quais partes do aplicativo serão necessárias.

## Desenvolvimento de um SPA usando SSR {#developing-an-spa-using-ssr}

Os componentes de SPA podem ser renderizados pelo cliente (no navegador) ou pelo lado do servidor. Quando renderizado no lado do servidor, as propriedades do navegador, como tamanho e local da janela, não estarão presentes. Por conseguinte, os componentes de SPA devem ser fictícios, não assumindo qualquer hipótese sobre onde serão renderizados.

Para usar o SSR, será necessário implantar seu código no AEM, bem como na Adobe I/O Runtime, responsável pela renderização do lado do servidor. A maioria do código será o mesmo, no entanto, as tarefas específicas do servidor serão diferentes.

## SSR para SPAs no AEM {#ssr-for-spas-in-aem}

O SSR para SPAs no AEM requer a Adobe I/O Runtime, chamada para a renderização do lado do servidor de conteúdo do aplicativo. No HTL do aplicativo, um recurso no Adobe I/O Runtime é chamado para renderizar o conteúdo.

Assim como o AEM suporta as estruturas Angular e React SPA prontas para uso, a renderização do lado do servidor também é compatível com aplicativos Angular e React. Para obter mais detalhes, consulte a documentação do NPM para ambas as estruturas.

* Reagir: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Para obter um exemplo simplista, consulte o [aplicativo We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Ele renderiza todo o lado do servidor de aplicativos. Embora este não seja um exemplo real, ele ilustra o que é necessário para implementar o SSR.

>[!CAUTION]
>
>O [aplicativo We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) é somente para fins de demonstração e, portanto, usa o Node.js como um exemplo simples, em vez do Adobe I/O Runtime recomendado. Este exemplo não deve ser usado para qualquer trabalho de projeto.

>[!NOTE]
>
>Qualquer projeto do AEM deve aproveitar o [Arquétipo de projeto do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos do SPA usando React ou Angular e aproveita o SDK do SPA.

## Uso de Node.js {#using-node-js}

O Adobe I/O Runtime é a solução recomendada para implementar o SSR para SPAs no AEM.

Para instâncias do AEM no local, também é possível implementar o SSR usando uma instância Node.js personalizada da mesma forma como descrito acima. Embora isso seja suportado pela Adobe, não é recomendado.

>[!NOTE]
>
>O Node.js não é compatível com instâncias do AEM hospedadas pela Adobe.

>[!NOTE]
>
>Se o SSR precisar ser implementado via Node.js, a Adobe recomenda uma instância diferente de Node.js para cada ambiente AEM (autor, publicação, estágio etc.).

## Renderizador de conteúdo remoto {#remote-content-renderer}

A [Configuração do renderizador de conteúdo remoto](#remote-content-renderer-configuration) que é necessária para usar o SSR com seu SPA no AEM se encaixa em um serviço de renderização mais generalizado que pode ser estendido e personalizado para atender às suas necessidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` é um serviço OSGi para recuperar conteúdo renderizado em um servidor remoto, como do Adobe I/O. O conteúdo enviado para o servidor remoto é baseado no parâmetro de solicitação transmitido.

`RemoteContentRenderingService` pode ser inserido por inversão de dependência em um modelo Sling personalizado ou servlet, quando for necessária manipulação de conteúdo adicional.

Esse serviço é usado internamente pelo [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

O `RemoteContentRendererRequestHandlerServlet` pode ser usado para definir programaticamente a configuração da solicitação. `DefaultRemoteContentRendererRequestHandlerImpl`, a implementação do manipulador de solicitação padrão fornecida permite criar várias configurações de OSGi para mapear um local na estrutura de conteúdo a um terminal remoto.

Para adicionar um Manipulador de solicitação personalizado, implemente a interface `RemoteContentRendererRequestHandler`. Certifique-se de definir a propriedade do componente `Constants.SERVICE_RANKING` para um número inteiro superior a 100, que é a classificação do `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configure a configuração OSGi do manipulador padrão {#configure-default-handler}

A configuração do manipulador padrão deve ser configurada conforme descrito na seção [Configuração do Renderizador de Conteúdo Remoto](#remote-content-renderer-configuration).

### Uso do renderizador de conteúdo remoto {#usage}

Para ter uma busca de servlet e retornar algum conteúdo que possa ser inserido na página:

1. Verifique se o servidor remoto está acessível.
1. Adicione um dos seguintes trechos ao modelo HTL de um componente do AEM.
1. Opcionalmente, crie ou modifique as configurações do OSGi.
1. Procurar o conteúdo do seu site

Normalmente, o modelo HTL de um componente de página é o principal recipient de tal recurso.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos {#requirements}

Os servlets usam o Exportador de Modelo do Sling para serializar os dados do componente. Por padrão, os adaptadores `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` são compatíveis como Sling Model. Se necessário, você pode adicionar classes para as quais a solicitação deve ser adaptada ao uso de `RemoteContentRendererServlet` e implementar o `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. As classes adicionais devem estender o `ComponentExporter`.
