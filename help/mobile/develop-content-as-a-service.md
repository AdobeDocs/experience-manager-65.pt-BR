---
title: Entrega de conteúdo
seo-title: Entrega de conteúdo
description: Entrega de conteúdo
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Entrega de conteúdo{#content-delivery}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos móveis devem poder usar todo e qualquer conteúdo no AEM, conforme necessário, para fornecer a experiência direcionada do aplicativo.

Isso inclui o uso de ativos, conteúdo do site, conteúdo de CaaS (over-the-air) e conteúdo personalizado que pode ter sua própria estrutura.

>[!NOTE]
>
>**O** conteúdo ao ar pode vir de qualquer um dos acima por meio dos manipuladores do ContentSync. Ele pode ser usado para fazer o pacote em lote e o delivery via zips, bem como para manter atualizações ou esses pacotes.

Existem três tipos principais de material que os Serviços de conteúdo fornecem:

1. **Assets**
1. **Conteúdo HTML empacotado (HTML/CSS/JS)**
1. **Conteúdo independente de canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

As coleções de ativos são AEM construções que contêm referências a outras coleções.

Uma coleção de Ativos pode ser exposta por meio dos Serviços de conteúdo. Chamar uma coleção de ativos em uma solicitação retorna um objeto que é uma lista de ativos, incluindo seus URLs. Os ativos são acessados por meio de um URL. O URL é fornecido em um objeto. Por exemplo:

* Uma entidade de página retorna JSON (objeto de página) que inclui uma referência de imagem. A referência da imagem é um URL usado para obter o binário de ativo da imagem.
* Uma solicitação de uma lista de ativos em uma pasta retorna JSON com detalhes sobre todas as entidades nessa pasta. Essa lista é um objeto. O JSON tem referências de URL que são usadas para obter o binário de ativo para cada ativo nessa pasta.

### Otimização de ativos {#asset-optimization}

Um valor importante dos Serviços de conteúdo é a capacidade de retornar ativos que são otimizados para o dispositivo. Isso reduz as necessidades de armazenamento de dispositivos locais e melhora o desempenho do aplicativo.

A otimização de ativos será uma função do lado do servidor, com base nas informações fornecidas na solicitação da API. Sempre que possível, as representações de ativos devem ser armazenadas em cache, de modo que solicitações semelhantes não exijam uma regeração da representação de ativos.

### Fluxo de trabalho dos ativos {#assets-workflow}

O fluxo de trabalho do ativo é o seguinte:

1. Referência de ativo disponível AEM pronto para uso
1. Criar Entidade de Referência de Ativos, de acordo com seu modelo
1. Editar entidade

   1. Selecionar ativo ou coleção de ativos
   1. Personalizar renderização JSON

O diagrama a seguir mostra o **Fluxo de trabalho de referência do Assets**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Gerenciar ativos {#managing-assets}

Os Serviços de conteúdo fornecem acesso a AEM ativos gerenciados que podem não ser referenciados por meio de outro conteúdo AEM.

#### Ativos gerenciados existentes {#existing-managed-assets}

Um usuário existente do AEM Sites e do Assets está usando o AEM Assets para gerenciar todo o material digital de todos os canais. Eles estão desenvolvendo um aplicativo móvel nativo e precisam usar vários ativos gerenciados pela AEM Assets. Por exemplo, logotipos, imagens de fundo, ícones de botão etc.

Atualmente, elas são espalhadas pelo repositório de Ativos. Os arquivos que o aplicativo precisa referenciar são:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Acessar entidades do CS Asset {#accessing-cs-asset-entities}

Vamos deixar de lado as etapas de como a página é disponibilizada por meio da API por enquanto (ela será coberta pela descrição da interface do usuário do AEM) e supor que ela tenha sido feita. As entidades de ativos foram criadas e adicionadas ao espaço &quot;appImages&quot;. Pastas adicionais foram criadas no espaço para fins de organização. Assim, as entidades de ativos são armazenadas no JCR AEM como:

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### Obter uma lista de entidades de ativos disponíveis {#getting-a-list-of-available-asset-entities}

Um desenvolvedor de aplicativos pode obter uma lista de quais ativos estão disponíveis, recuperando as entidades de ativos. O endpoint de espaço dos Serviços de conteúdo pode fornecer essas informações por meio do SDK da API do serviço da Web.

O resultado seria um objeto em um formato JSON que forneceria uma lista dos ativos na pasta &quot;ícones&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obter uma imagem {#getting-an-image}

O JSON fornece um URL para cada imagem, gerada pelos Serviços de conteúdo para a imagem.

Para obter o binário da imagem do &quot;carrinho&quot;, a biblioteca do cliente é usada mais uma vez.

## Conteúdo HTML empacotado {#packaged-html-content}

O conteúdo HTML é necessário para os clientes que precisam manter o layout do conteúdo. Isso é útil para aplicativos nativos que estão usando um contêiner da Web, como uma webview do Cordova, para exibir o conteúdo.

Os AEM Content Services poderão fornecer conteúdo HTML ao aplicativo móvel por meio da API. Os clientes que desejam expor AEM conteúdo como HTML criarão uma entidade de página HTML que aponte para a fonte de conteúdo AEM.

As seguintes opções são consideradas:

* **Arquivo zip:** para ter a melhor chance de ser exibido corretamente no dispositivo, todo o material referenciado da página - css, JavaScript, ativos etc. - será incluído em um único arquivo compactado com a resposta. As referências na página HTML serão ajustadas para usar um caminho relativo para esses arquivos.
* **Streaming:** obter um manifesto dos arquivos necessários do AEM. Em seguida, use esse manifesto para solicitar todos os arquivos (HTML, CSS, JS etc.) com solicitações subsequentes.

![chlimage_1-157](assets/chlimage_1-157.png)

## Conteúdo independente de canal {#channel-independent-content}

O conteúdo independente do canal é uma maneira de expor construções de conteúdo AEM - como páginas - sem se preocupar com layout, componentes ou outras informações específicas do canal.

Essas entidades de conteúdo são geradas usando um modelo de conteúdo para traduzir as estruturas de AEM em um formato JSON. Os dados JSON resultantes contêm informações sobre os dados do conteúdo, que são dissociados do repositório AEM. Isso inclui o retorno de metadados e AEM links de referência para ativos, bem como as relações entre estruturas de conteúdo - incluindo a hierarquia de entidade.

### Gerenciamento de conteúdo independente de canal {#managing-channel-independent-content}

O conteúdo pode acessar o aplicativo de várias maneiras.

1. Conteúdo do GET ZIPS via AEM Over-the-Air

   * Os manipuladores de Sincronização de conteúdo podem atualizar o pacote zip diretamente ou chamando os renderizadores de conteúdo existentes

      * Manipuladores de plataforma
      * Manipuladores de AEM
      * Manipuladores personalizados

1. GET de conteúdo diretamente por meio de renderizadores de conteúdo

   * Renderizadores de sling padrão integrados
   * Renderizadores de conteúdo do AEM Mobile/Content Services
   * Renderizações personalizadas

