---
title: Renderização do SPA e do servidor
seo-title: Renderização do SPA e do servidor
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
source-git-commit: 9f0eebfa0c5d2449dcc2977c7085b11a48a10eb9

---


# Renderização do SPA e do servidor{#spa-and-server-side-rendering}

>[!NOTE]
>
>O Editor SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em estrutura SPA (por exemplo, Reagir ou Angular).

>[!NOTE]
>
>AEM 6.5.1.0 ou posterior é necessário para usar os recursos de renderização do lado do servidor SPA, conforme descrito neste documento.

## Visão geral {#overview}

Aplicativos de página única (SPAs) podem oferta ao usuário uma experiência rica e dinâmica que reage e se comporta de maneiras familiares, geralmente como um aplicativo nativo. [Isso é feito contando com o cliente para carregar o conteúdo antecipadamente e, em seguida, fazer um pesado levantamento da manipulação da interação](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) do usuário, minimizando a quantidade de comunicação necessária entre o cliente e o servidor, tornando o aplicativo mais reativo.

No entanto, isso pode levar a tempos de carregamento iniciais mais longos, especialmente se o SPA for grande e rico em seu conteúdo. Para otimizar o tempo de carregamento, parte do conteúdo pode ser renderizada no lado do servidor. O uso da renderização no lado do servidor (SSR) pode acelerar a carga inicial da página e passar a renderização para o cliente.

## Quando usar o SSR {#when-to-use-ssr}

A SSR não é necessária em todos os projetos. Embora o AEM seja totalmente compatível com o JS SSR para SPA, a Adobe não recomenda implementá-lo sistematicamente para cada projeto.

Ao decidir implementar a SSR, você deve primeiro estimar o que a complexidade adicional, o esforço e a adição de custo representa realisticamente para o projeto, incluindo a manutenção de longo prazo. Uma arquitetura de SSR só deve ser escolhida se o valor acrescentado exceder claramente os custos estimados.

A SSR geralmente fornece algum valor quando há um claro &quot;sim&quot; a qualquer uma das seguintes perguntas:

* **SEO:** O SSR ainda é necessário para que seu site seja indexado corretamente pelos mecanismos de pesquisa que trazem tráfego? Lembre-se de que os principais rastreadores de mecanismo de pesquisa agora avaliam o JS.
* **Velocidade da página:** A SSR fornece uma melhoria mensurável da velocidade em ambientes reais e adiciona à experiência geral do usuário?

Somente quando pelo menos uma dessas duas perguntas for respondida com um claro &quot;sim&quot; para o seu projeto a Adobe recomenda a implementação da SSR. As seções a seguir descrevem como fazer isso usando o Adobe I/O Runtime.

## Tempo de execução de E/S da Adobe {#adobe-i-o-runtime}

Se você [estiver confiante de que seu projeto requer a implementação da SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), a solução recomendada da Adobe é usar o tempo de execução de E/S da Adobe.

Para obter mais informações sobre o tempo de execução de E/S da Adobe, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - para obter uma visão geral do serviço
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - para obter a documentação detalhada sobre a plataforma

As seções a seguir detalham como o Adobe I/O Runtime pode ser usado para implementar o SSR para seu SPA em dois modelos diferentes:

* [Fluxo de comunicação orientado pelo AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Fluxo de comunicação direcionado ao tempo de execução de E/S da Adobe](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>A Adobe recomenda uma instância separada do Tempo de execução de E/S da Adobe para cada ambiente AEM (autor, publicação, estágio etc.).

## Configuração do Renderizador Remoto {#remote-renderer-configuration}

O AEM deve saber onde o conteúdo renderizado remotamente pode ser recuperado. Independentemente do modelo [que você escolher implementar para SSR,](#adobe-i-o-runtime) será necessário especificar ao AEM como acessar esse serviço de renderização remota.

Isso é feito via **RemoteContentRenderer - serviço** OSGi de fábrica de configuração. Procure a string &quot;RemoteContentRenderer&quot; no console Configuração do console da Web em `http://<host>:<port>/system/console/configMgr`.

![Configuração do renderizador](assets/rendererconfig.png)

Os seguintes campos estão disponíveis para a configuração:

* **Padrão** do caminho do conteúdo - expressão regular para corresponder a uma parte do conteúdo, se necessário
* **URL** de ponto de extremidade remoto - URL do ponto de extremidade responsável pela geração do conteúdo
   * Use o protocolo HTTPS protegido se não estiver na rede local.
* **Cabeçalhos** de solicitação adicionais - Cabeçalhos adicionais a serem adicionados à solicitação enviada ao terminal remoto
   * Padrão: `key=value`
* **Tempo limite** da solicitação - Tempo limite da solicitação de host remoto em milissegundos

>[!NOTE]
>
>Independentemente de você optar por implementar o fluxo [de comunicação controlado pelo](#aem-driven-communication-flow) AEM ou o fluxo controlado pelo [Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) é necessário definir uma configuração de renderizador de conteúdo remoto.
>
>Essa configuração também deve ser definida se você optar por [usar um servidor Node.js personalizado.](#using-node-js)

>[!NOTE]
>
>Essa configuração aproveita o [Remote Content Renderer,](#remote-content-renderer) que tem opções adicionais de extensão e personalização disponíveis.

## Fluxo de comunicação orientado pelo AEM {#aem-driven-communication-flow}

Ao usar o SSR, o fluxo de trabalho [de interação do](/help/sites-developing/spa-overview.md#workflow) componente dos SPAs no AEM inclui uma fase na qual o conteúdo inicial do aplicativo é gerado no Adobe I/O Runtime.

1. O navegador solicita o conteúdo SSR do AEM.

1. O AEM publica o modelo no Adobe I/O Runtime.

1. O tempo de execução de E/S da Adobe retorna o conteúdo gerado.

1. O AEM serve o HTML retornado pelo Adobe I/O Runtime através do modelo HTL do componente de página de backend.

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Fluxo de comunicação direcionado ao tempo de execução de E/S da Adobe {#adobe-i-o-runtime-driven-communication-flow}

A seção anterior descreve a implementação padrão e recomendada da renderização do lado do servidor em relação aos SPAs no AEM, onde o AEM executa o carregamento automático e a disponibilização de conteúdo.

Como alternativa, a SSR pode ser implementada para que o Adobe I/O Runtime seja responsável pelo carregamento automático, revertendo efetivamente o fluxo de comunicação.

Ambos os modelos são válidos e são suportados pelo AEM. No entanto, é preciso considerar as vantagens e desvantagens de cada um antes de implementar um modelo específico.

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
     <li>O AEM gerencia bibliotecas injetáveis onde necessário</li>
     <li>Os recursos só precisam ser mantidos no AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possivelmente estranho para o desenvolvedor SPA<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Mais familiar para desenvolvedores de SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Os recursos clientlib exigidos pelo aplicativo, como CSS e JavaScript, precisarão ser disponibilizados pelo desenvolvedor do AEM por meio da <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> propriedade<br /> </li>
     <li>Os recursos devem ser sincronizados entre o AEM e o Adobe I/O Runtime<br /> </li>
     <li>Para habilitar a criação do SPA, pode ser necessário um servidor proxy para o Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planejamento para SSR {#planning-for-ssr}

Geralmente, apenas parte de um aplicativo precisa ser renderizada no lado do servidor. O exemplo comum é o conteúdo que será exibido acima da dobra na carga inicial da página que é renderizada no lado do servidor. Isso economiza tempo fornecendo ao cliente conteúdo já renderizado. Conforme o usuário interage com o SPA, o conteúdo adicional é renderizado pelo cliente.

Ao considerar implementar a renderização do lado do servidor para o SPA, é necessário verificar quais partes do aplicativo serão necessárias.

## Desenvolvimento de um SPA usando SSR {#developing-an-spa-using-ssr}

Os componentes SPA podem ser renderizados pelo cliente (no navegador) ou pelo servidor. Quando o servidor renderizado, as propriedades do navegador, como tamanho e localização da janela, não estão presentes. Por conseguinte, os componentes do SPA devem ser isomórficos, não assumindo qualquer hipótese quanto ao local em que serão apresentados.

Para aproveitar a SSR, será necessário implantar seu código no AEM, bem como no Adobe I/O Runtime, que é responsável pela renderização no servidor. A maioria do código será o mesmo, no entanto, tarefas específicas do servidor serão diferentes.

## SSR para SPAs no AEM {#ssr-for-spas-in-aem}

O SSR para SPAs no AEM requer o tempo de execução de E/S da Adobe, chamado para a renderização do lado do servidor de conteúdo do aplicativo. No HTL do aplicativo, um recurso no Adobe I/O Runtime é chamado para renderizar o conteúdo.

Da mesma forma que o AEM suporta as estruturas SPA Angular e Reata prontas para uso, a renderização no lado do servidor também é compatível com aplicativos Angular e React. Consulte a documentação do NPM para obter mais detalhes sobre ambas as estruturas.

* Reagir: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Para obter um exemplo simplista, consulte o aplicativo de Journal [We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Ele renderiza todo o lado do servidor de aplicativos. Embora este não seja um exemplo real, ele ilustra o que é necessário para implementar a SSR.

>[!CAUTION]
>
>O aplicativo [Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) We.Retail é apenas para fins de demonstração e, portanto, usa Node.js como um exemplo simples em vez do tempo de execução de E/S recomendado pela Adobe. Este exemplo não deve ser usado para nenhum trabalho de projeto.

>[!NOTE]
>
>Todos os projetos de SPA no AEM devem se basear no [Maven Archetype for SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype).

## Uso de Node.js {#using-node-js}

O tempo de execução de E/S da Adobe é a solução recomendada para implementar o SSR para SPAs no AEM.

Para instâncias do AEM presenciais, também é possível implementar o SSR usando uma instância do Node.js personalizada da mesma forma como descrito acima. Embora seja suportado pela Adobe, isso não é recomendado.

>[!NOTE]
>
>Node.js não é compatível com instâncias AEM hospedadas pela Adobe.

>[!NOTE]
>
>Se o SSR precisar ser implementado via Node.js, a Adobe recomenda uma instância diferente de Node.js para cada ambiente AEM (autor, publicação, estágio etc.).

## Renderizador de conteúdo remoto {#remote-content-renderer}

A Configuração [do renderizador de conteúdo](#remote-content-renderer-configuration) remoto necessária para usar o SSR com seu SPA no AEM se encaixa em um serviço de renderização mais generalizado que pode ser estendido e personalizado para atender às suas necessidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` é um serviço OSGi para recuperar conteúdo renderizado em um servidor remoto, como de E/S da Adobe. O conteúdo enviado para o servidor remoto é baseado no parâmetro de solicitação passado.

`RemoteContentRenderingService` pode ser inserido por inversão de dependência em um modelo Sling personalizado ou servlet quando for necessária manipulação de conteúdo adicional.

Esse serviço é usado internamente pelo [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

O `RemoteContentRendererRequestHandlerServlet` pode ser usado para definir programaticamente a configuração da solicitação. `DefaultRemoteContentRendererRequestHandlerImpl`, a implementação do manipulador de solicitações padrão fornecido permite que você crie várias configurações OSGi para mapear um local na estrutura do conteúdo para um terminal remoto.

Para adicionar um Manipulador de solicitações personalizado, implemente a `RemoteContentRendererRequestHandler` interface. Certifique-se de definir a propriedade do `Constants.SERVICE_RANKING` componente para um número inteiro superior a 100, que é a classificação do `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurar a configuração OSGi do manipulador padrão {#configure-default-handler}

A configuração do manipulador padrão deve ser configurada conforme descrito na seção Configuração [do renderizador de conteúdo](#remote-content-renderer-configuration)remoto.

### Uso do Renderizador de Conteúdo Remoto {#usage}

Para obter um servlet e retornar algum conteúdo que possa ser inserido na página:

1. Verifique se o servidor remoto está acessível.
1. Adicione um dos seguintes trechos ao modelo HTL de um componente AEM.
1. Como opção, crie ou modifique as configurações do OSGi.
1. Procurar o conteúdo do site

Normalmente, o modelo HTL de um componente de página é o recipient principal desse recurso.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos {#requirements}

Os servlets aproveitam o Exportador do Modelo Sling para serializar os dados do componente. Por padrão, os adaptadores `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` são suportados como Sling Model. Se necessário, é possível adicionar classes para as quais a solicitação deve ser adaptada para usar o `RemoteContentRendererServlet` e implementar o `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. As classes adicionais devem estender o `ComponentExporter`.
