---
title: Entrega de conteúdo
description: Saiba mais sobre como usar todo o conteúdo do Adobe Experience Manager para fornecer a experiência direcionada do aplicativo.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# Entrega de conteúdo{#content-delivery}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos móveis devem poder usar todo o conteúdo no AEM conforme necessário para fornecer a experiência do aplicativo direcionado.

Isso inclui o uso de ativos, conteúdo do site, conteúdo do CaaS (ao ar) e conteúdo personalizado que pode ter sua própria estrutura.

>[!NOTE]
>
>**Conteúdo Over-the-Air** pode vir de qualquer uma das opções acima por meio de manipuladores ContentSync. Ele pode ser usado para empacotar e entregar em lote por meio de zips e manter atualizações desses pacotes.

Há três tipos principais de material que os Serviços de conteúdo fornecem:

1. **Assets**
1. **Conteúdo de HTML empacotado (HTML/CSS/JS)**
1. **Conteúdo independente de canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

Coleções de ativos são construções AEM que contêm referências a outras coleções.

Uma coleção de ativos pode ser exposta por meio dos Serviços de conteúdo. Chamar uma coleção de ativos em uma solicitação retorna um objeto que é uma lista dos ativos, incluindo seus URLs. Os ativos são acessados por meio de um URL. O URL é fornecido em um objeto. Por exemplo:

* Uma entidade de página retorna o JSON (objeto de página) que inclui uma referência de imagem. A referência da imagem é um URL usado para obter o binário do ativo para a imagem.
* Uma solicitação de lista de ativos em uma pasta retorna o JSON com detalhes sobre todas as entidades nessa pasta. Essa lista é um objeto. O JSON tem referências de URL que são usadas para obter o binário do ativo para cada ativo nessa pasta.

### Otimização de ativos {#asset-optimization}

Um valor importante dos Content Services é a capacidade de retornar ativos otimizados para o dispositivo. Isso reduz as necessidades de armazenamento do dispositivo local e melhora o desempenho do aplicativo.

A otimização de ativos é uma função do lado do servidor, com base nas informações fornecidas na solicitação da API. Sempre que possível, as representações de ativos devem ser armazenadas em cache para que solicitações semelhantes não exijam a regeneração da representação do ativo.

### Fluxo de trabalho dos ativos {#assets-workflow}

O fluxo de trabalho do ativo é o seguinte:

1. A referência do ativo está disponível no AEM pronto para uso
1. Criar uma entidade de referência de ativo de acordo com seu modelo
1. Editar entidade

   1. Escolha um ativo ou uma coleção de ativos
   1. Personalizar renderização de JSON

O diagrama a seguir mostra as **Fluxo de trabalho de referência do Assets**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Gerenciamento de ativos {#managing-assets}

Os Content Services fornecem acesso a ativos gerenciados pelo AEM que podem não ser referenciados por meio de outro conteúdo AEM.

#### Ativos gerenciados existentes {#existing-managed-assets}

Um usuário do AEM Sites e do Assets está usando o AEM Assets para gerenciar todo o seu material digital para todos os canais. Eles estão desenvolvendo um aplicativo móvel nativo e devem usar vários ativos gerenciados pela AEM Assets. Por exemplo, logotipos, imagens de fundo e ícones de botão.

Atualmente, eles estão distribuídos pelo repositório de ativos. Os arquivos que o aplicativo deve mencionar estão no seguinte:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Acesso às entidades do CS Asset {#accessing-cs-asset-entities}

Vamos deixar de lado as etapas de como a página é disponibilizada por meio da API por enquanto (ela é coberta pela descrição da interface do usuário do AEM) e supor que isso tenha sido feito. As entidades de ativos foram criadas e adicionadas ao espaço &quot;appImages&quot;. Pastas adicionais foram criadas no espaço para fins de organização. Portanto, as entidades de ativo são armazenadas no AEM JCR como:

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### Obter uma lista de entidades de ativos disponíveis {#getting-a-list-of-available-asset-entities}

Um desenvolvedor de aplicativos pode obter uma lista de quais ativos estão disponíveis, recuperando as entidades do ativo. O endpoint de espaço do Content Services pode fornecer essas informações por meio do SDK da API do serviço da Web.

O resultado seria um objeto em formato JSON que forneceria uma lista dos ativos na pasta &quot;ícones&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obter uma imagem {#getting-an-image}

O JSON fornece um URL para cada imagem gerada pelos Serviços de conteúdo para a imagem.

Para obter o binário da imagem do &quot;carrinho&quot;, a biblioteca do cliente é usada novamente.

## Conteúdo de HTML empacotado {#packaged-html-content}

O conteúdo em HTML é necessário para clientes que precisam manter o layout do conteúdo. Isso é útil para aplicativos nativos que estão usando um contêiner da Web - como uma visualização da Web no Cordova - para exibir o conteúdo.

O AEM Content Services fornece conteúdo de HTML para o aplicativo móvel por meio da API. Os clientes que desejam expor conteúdo AEM como HTML podem criar uma entidade de página HTML que aponte para a fonte de conteúdo AEM.

As seguintes opções são consideradas:

* **Arquivo zip:** Para ter a melhor chance de exibir corretamente no dispositivo, o material-css, o JavaScript, os ativos e assim por diante referenciados da página são incluídos em um único arquivo compactado com a resposta. As referências na página HTML podem ser ajustadas para usar um caminho relativo para esses arquivos.
* **Transmissão:** Obter um manifesto dos arquivos necessários do AEM. Em seguida, use esse manifesto para solicitar todos os arquivos (HTML, CSS, JS e assim por diante) com solicitações subsequentes.

![chlimage_1-157](assets/chlimage_1-157.png)

## Conteúdo independente de canal {#channel-independent-content}

O conteúdo independente de canal é uma maneira de expor construções de conteúdo AEM, como páginas, sem se preocupar com layout, componentes ou outras informações específicas do canal.

Essas entidades de conteúdo são geradas usando um modelo de conteúdo para traduzir as estruturas AEM em um formato JSON. Os dados JSON resultantes contêm informações sobre os dados do conteúdo que são dissociados do repositório AEM. Isso inclui o retorno de metadados e links de referência de AEM para ativos e os relacionamentos entre estruturas de conteúdo, incluindo a hierarquia da entidade.

### Gerenciamento de conteúdo independente de canal {#managing-channel-independent-content}

O conteúdo pode chegar ao aplicativo de várias maneiras.

1. GET ZIPS por meio de AEM Over-the-Air

   * Os manipuladores de sincronização de conteúdo podem atualizar o pacote zip diretamente ou chamando renderizadores de conteúdo existentes

      * Manipuladores de plataforma
      * Manipuladores de AEM
      * Manipuladores personalizados

1. GET conteúdo diretamente por meio de renderizadores de conteúdo

   * Renderizadores Sling padrão prontos para uso
   * AEM Mobile/Renderizadores de conteúdo do Content Services
   * Renderizações personalizadas
