---
title: Renderização do SPA e do servidor
description: Saiba mais sobre o SPA e a renderização do lado do servidor no Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 1%

---

# Renderização do SPA e do servidor{#spa-and-server-side-rendering}

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização no lado do cliente baseada na estrutura SPA (por exemplo, React ou Angular).

>[!NOTE]
>
>O Adobe Experience Manager (AEM) 6.5.1.0 ou posterior é necessário para usar os recursos de renderização do lado do servidor SPA, conforme descrito neste documento.

## Visão geral {#overview}

Os aplicativos de página única (SPA) podem oferecer ao usuário uma experiência avançada e dinâmica que reage e se comporta de maneiras familiares, geralmente como um aplicativo nativo. [Isso é feito confiando no cliente para carregar o conteúdo antecipadamente e, em seguida, fazer o trabalho pesado de lidar com a interação do usuário](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) e, portanto, minimizar a quantidade de comunicação necessária entre o cliente e o servidor, tornando o aplicativo mais reativo.

No entanto, isso pode levar a tempos de carregamento inicial mais longos, especialmente se o SPA for grande e rico em conteúdo. Para otimizar os tempos de carregamento, parte do conteúdo pode ser renderizado no lado do servidor. O uso da renderização do lado do servidor (SSR) pode acelerar a carga inicial da página e, em seguida, passar a renderização adicional para o cliente.

## Quando usar o SSR {#when-to-use-ssr}

O SSR não é necessário em todos os projetos. Embora AEM seja totalmente compatível com JS SSR para SPA, o Adobe não recomenda implementá-lo sistematicamente para cada projeto.

Ao decidir implementar o SSR, você deve primeiro estimar a complexidade, o esforço e o custo adicionais que a adição do SSR representa realisticamente para o projeto, incluindo a manutenção a longo prazo. Uma arquitetura SSR só deve ser escolhida quando o valor acrescentado exceder claramente os custos estimados.

O SSR geralmente fornece algum valor quando há um claro &quot;sim&quot; para qualquer uma das seguintes perguntas:

* **SEO:** O SSR ainda é necessário para que seu site seja indexado corretamente pelos mecanismos de pesquisa que trazem tráfego? Lembre-se de que os principais rastreadores de mecanismo de pesquisa agora avaliam o JS.
* **Velocidade da página:** O SSR oferece uma melhoria mensurável na velocidade em ambientes reais e contribui para a experiência geral do usuário?

Somente quando pelo menos uma dessas duas perguntas for respondida com um claro &quot;sim&quot; para o seu projeto, o Adobe recomenda a implementação do SSR. As seções a seguir descrevem como fazer isso usando o Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se você [estão confiantes de que seu projeto requer a implementação do SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), a solução Adobe recomendada é usar o Adobe I/O Runtime.

Para obter mais informações sobre o Adobe I/O Runtime, consulte o seguinte:

* [https://developer.adobe.com/runtime/](https://developer.adobe.com/runtime/) - para obter uma visão geral do serviço
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs/) - para obter a documentação detalhada sobre a plataforma

As seções a seguir detalham como o Adobe I/O Runtime pode ser usado para implementar o SSR para o SPA em dois modelos diferentes:

* [Fluxo de comunicação orientado por AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Fluxo de comunicação orientado pela Adobe I/O Runtime](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>A Adobe recomenda um espaço de trabalho do Adobe I/O Runtime separado por ambiente (preparo, produção, teste e assim por diante). Isso permite padrões típicos de SDLC (Systems Development Life Cycle, ciclo de vida de desenvolvimento de sistemas) com diferentes versões de um único aplicativo implantado em diferentes ambientes. Consulte o documento [CI/CD para aplicativos do Construtor de aplicativos do Project](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) para obter mais informações.
>
>Um espaço de trabalho separado não é necessário por instância (autor, publicação), a menos que haja diferenças na implementação em tempo de execução por tipo de instância.

## Configuração do renderizador remoto {#remote-renderer-configuration}

O AEM deve saber onde o conteúdo renderizado remotamente pode ser recuperado. Independentemente de [que modelo você escolhe implementar para SSR,](#adobe-i-o-runtime), é necessário especificar ao AEM como acessar esse serviço de renderização remota.

Isso é feito por meio da **RemoteContentRenderer - Serviço OSGi de Fábrica de Configurações**. Procure a cadeia de caracteres &quot;RemoteContentRenderer&quot; no console Configuração do console da Web em `http://<host>:<port>/system/console/configMgr`.

![Configuração do renderizador](assets/rendererconfig.png)

Os seguintes campos estão disponíveis para a configuração:

* **Padrão do caminho de conteúdo** - Expressão regular para corresponder a uma parte do conteúdo, se necessário
* **URL do ponto de extremidade remoto** - O URL do endpoint responsável pela geração do conteúdo
   * Use o protocolo HTTPS seguro se não estiver na rede local.
* **Cabeçalhos de solicitação adicionais** - Cabeçalhos adicionais a serem adicionados à solicitação enviada para o ponto de extremidade remoto
   * Padrão: `key=value`
* **Tempo limite da solicitação** - Tempo limite de solicitação do host remoto em milissegundos

>[!NOTE]
>
>Independentemente de você optar por implementar o [Fluxo de comunicação orientado por AEM](#aem-driven-communication-flow) ou o [Fluxo orientado pela Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) você deve definir uma configuração remota de renderizador de conteúdo.
>
>Essa configuração também deve ser definida se você optar por [usar um servidor Node.js personalizado.](#using-node-js)

>[!NOTE]
>
>Essa configuração usa o [Renderizador remoto de conteúdo,](#remote-content-renderer) que tem opções adicionais de extensão e personalização disponíveis.

## Fluxo de comunicação orientado por AEM {#aem-driven-communication-flow}

Ao utilizar o SSR, a variável [fluxo de trabalho de interação de componente](/help/sites-developing/spa-overview.md#workflow) SPA O do AEM inclui uma fase em que o conteúdo inicial do aplicativo é gerado no Adobe I/O Runtime.

1. O navegador solicita o conteúdo SSR do AEM.

1. AEM posta o modelo no Adobe I/O Runtime.

1. O Adobe I/O Runtime retorna o conteúdo gerado.

1. O AEM serve o HTML retornado pelo Adobe I/O Runtime por meio do modelo HTL do componente de página de back-end.

![renderização do lado do servidor-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Fluxo de comunicação orientado pela Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

A seção anterior descreve a implementação padrão e recomendada da renderização no lado do servidor em relação ao SPA AEM, onde o AEM executa o bootstrapping e a veiculação de conteúdo.

Como alternativa, o SSR pode ser implementado para que o Adobe I/O Runtime seja responsável pela inicialização, revertendo efetivamente o fluxo de comunicação.

Ambos os modelos são válidos e suportados pelo AEM. No entanto, deve-se considerar as vantagens e desvantagens de cada um antes de implementar um modelo específico.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <th><strong>por meio do AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM gerencia a a injeção de bibliotecas onde necessário</li>
     <li>Manter recursos somente no AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possivelmente desconhecido do desenvolvedor de SPA<br /> </li>
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
     <li>Os recursos do Clientlib necessários para o aplicativo, como CSS e JavaScript, devem ser disponibilizados pelo desenvolvedor do AEM por meio do <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> propriedade<br /> </li>
     <li>Os recursos devem ser sincronizados entre o AEM e o Adobe I/O Runtime<br /> </li>
     <li>Para habilitar a criação do SPA, pode ser necessário um servidor proxy para o Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planejamento para SSR {#planning-for-ssr}

Somente parte de um aplicativo deve ser renderizada no lado do servidor. O exemplo comum é o conteúdo exibido acima da dobra no carregamento inicial da página que é renderizado no lado do servidor. Isso economiza tempo fornecendo ao cliente conteúdo já renderizado. Conforme o usuário interage com o SPA, o conteúdo adicional é renderizado pelo cliente.

Ao considerar implementar a renderização do lado do servidor para o seu SPA, analise quais partes do aplicativo são necessárias.

## Desenvolvimento de um SPA usando SSR {#developing-an-spa-using-ssr}

Os componentes do SPA podem ser renderizados pelo cliente (no navegador) ou pelo servidor. Quando renderizadas no lado do servidor, as propriedades do navegador, como tamanho e localização da janela, não estão presentes. Portanto, os componentes SPA devem ser isomorfos, não fazendo suposições sobre onde serão renderizados.

Para usar o SSR, implante seu código no AEM e no Adobe I/O Runtime, que é responsável pela renderização do lado do servidor. A maioria do código será o mesmo. No entanto, tarefas específicas do servidor serão diferentes.

## RSS para AEM no SPA {#ssr-for-spas-in-aem}

O SSR para AEM no SPA exige o Adobe I/O Runtime, que é chamado para a renderização do lado do servidor de conteúdo do aplicativo. No HTL do aplicativo, um recurso no Adobe I/O Runtime é chamado para renderizar o conteúdo.

Assim como o AEM suporta as estruturas SPA do Angular e do React prontas para uso, a renderização no lado do servidor também é compatível com os aplicativos Angular e React. Consulte a documentação do NPM para ambas as estruturas para obter mais detalhes.

* React: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Para obter um exemplo simples, consulte [Aplicativo We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Ele renderiza todo o lado do servidor de aplicativos. Embora este não seja um exemplo real, ilustra o que é necessário para implementar a RSS.

>[!CAUTION]
>
>A variável [Aplicativo We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) O é somente para fins de demonstração e, portanto, usa Node.js como um exemplo simples, em vez do Adobe I/O Runtime recomendado. Não use este exemplo para nenhum trabalho do projeto.

>[!NOTE]
>
>Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Usar Node.js {#using-node-js}

O Adobe I/O Runtime é a solução recomendada para implementar o SSR para o SPA no AEM.

Para instâncias AEM no local, também é possível implementar o SSR usando uma instância personalizada do Node.js da mesma forma descrita acima. Embora isso seja suportado pelo Adobe, não é recomendado.

>[!NOTE]
>
>O Node.js não é compatível com instâncias AEM hospedadas em Adobe.

>[!NOTE]
>
>Se o SSR precisar ser implementado por meio do Node.js, o Adobe recomenda uma instância do Node.js separada para cada ambiente AEM (autor, publicação, preparo e assim por diante).

## Renderizador remoto de conteúdo {#remote-content-renderer}

A variável [Configuração do renderizador de conteúdo remoto](#remote-content-renderer-configuration) que é necessário para usar o SSR com seu AEM no SPA se encaixa em um serviço de renderização mais generalizado que pode ser estendido e personalizado para atender às suas necessidades.

### ServiçoDeRenderizaçãoDeConteúdoRemoto {#remotecontentrenderingservice}

`RemoteContentRenderingService` O é um serviço OSGi para recuperar conteúdo renderizado em um servidor remoto, como do Adobe I/O. O conteúdo enviado para o servidor remoto se baseia no parâmetro de solicitação transmitido.

`RemoteContentRenderingService` pode ser inserido por inversão de dependência em um modelo Sling personalizado ou servlet quando for necessária manipulação de conteúdo adicional.

Este serviço é usado internamente pelo [ServletManipuladordeSolicitaçãodeRenderizadorDeConteúdoRemoto](#remotecontentrendererrequesthandlerservlet).

### ServletManipuladordeSolicitaçãodeRenderizadorDeConteúdoRemoto {#remotecontentrendererrequesthandlerservlet}

A variável `RemoteContentRendererRequestHandlerServlet` pode ser usado para definir programaticamente a configuração da solicitação. `DefaultRemoteContentRendererRequestHandlerImpl`, a implementação do manipulador de solicitações padrão fornecida, permite criar várias configurações de OSGi para mapear um local na estrutura de conteúdo para um endpoint remoto.

Para adicionar um Manipulador de solicitação personalizado, implemente o `RemoteContentRendererRequestHandler` interface. Certifique-se de definir a variável `Constants.SERVICE_RANKING` propriedade de componente a um inteiro maior que 100, que é a classificação da variável `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurar o OSGi do manipulador padrão {#configure-default-handler}

A configuração do manipulador padrão deve ser definida conforme descrito na seção [Configuração do renderizador de conteúdo remoto](#remote-content-renderer-configuration).

### Uso do renderizador de conteúdo remoto {#usage}

Para fazer um servlet buscar e retornar algum conteúdo que possa ser inserido na página:

1. Certifique-se de que o servidor remoto esteja acessível.
1. Adicione um dos seguintes trechos ao modelo HTL de um componente AEM.
1. Opcionalmente, crie ou modifique as configurações do OSGi.
1. Navegar pelo conteúdo do site

Normalmente, o modelo HTL de um componente de página é o principal destinatário desse recurso.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos {#requirements}

Os servlets usam o Exportador de modelo Sling para serializar os dados do componente. Por padrão, as duas `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` são compatíveis como adaptadores do Modelo do Sling. Se necessário, você pode adicionar classes às quais a solicitação deve ser adaptada usando o `RemoteContentRendererServlet` e a aplicação da `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. As classes adicionais devem estender o `ComponentExporter`.
