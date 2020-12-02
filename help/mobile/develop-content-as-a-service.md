---
title: Delivery de conteúdo
seo-title: Delivery de conteúdo
description: 'null'
seo-description: nulo
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---


# Delivery de conteúdo{#content-delivery}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos móveis devem ser capazes de usar todo e qualquer conteúdo no AEM, conforme necessário, para oferecer a experiência do aplicativo direcionado.

Isso inclui o uso de ativos, conteúdo do site, conteúdo de CaaS (over-the-air) e conteúdo personalizado que pode ter sua própria estrutura.

>[!NOTE]
>
>**O Over-the-Air** Contentare pode vir de qualquer um dos itens acima por meio de manipuladores ContentSync. Ele pode ser usado para fazer o lote do pacote e do delivery via zips, além de manter atualizações ou pacotes.

Há três tipos principais de material que os Serviços de conteúdo fornecem:

1. **Assets**
1. **Conteúdo HTML empacotado (HTML/CSS/JS)**
1. **conteúdo independente do canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

As coleções de ativos são construções AEM que contêm referências a outras coleções.

Uma coleção de ativos pode ser exposta por meio dos Serviços de conteúdo. Chamar uma coleção de ativos em uma solicitação retorna um objeto que é uma lista dos ativos - incluindo seus URLs. Os ativos são acessados por meio de um URL. O URL é fornecido em um objeto. Por exemplo:

* Uma entidade de página retorna JSON (objeto de página) que inclui uma referência de imagem. A referência de imagem é um URL usado para obter o binário de ativo da imagem.
* Uma solicitação de lista de ativos em uma pasta retorna o JSON com detalhes sobre todas as entidades dessa pasta. Essa lista é um objeto. O JSON tem referências de URL que são usadas para obter o binário de ativos para cada ativo nessa pasta.

### Otimização de ativos {#asset-optimization}

Um valor importante dos Serviços de conteúdo é a capacidade de retornar ativos otimizados para o dispositivo. Isso reduz as necessidades de armazenamento do dispositivo local e melhora o desempenho do aplicativo.

A otimização de ativos será uma função do lado do servidor, com base nas informações fornecidas na solicitação da API. Sempre que possível, as representações de ativos devem ser armazenadas em cache, de modo que solicitações semelhantes não exijam uma regeração da representação de ativos.

### Fluxo de trabalho de ativos {#assets-workflow}

O fluxo de trabalho do ativo é o seguinte:

1. Referência de ativos disponível AEM pronto
1. Criar entidade de referência de ativo, considerando seu modelo
1. Editar entidade

   1. Selecionar ativo ou coleção de ativos
   1. Personalizar renderização JSON

O diagrama a seguir mostra o **Fluxo de trabalho de referência de ativos**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Gerenciar ativos {#managing-assets}

Os Serviços de conteúdo fornecem acesso a ativos gerenciados AEM que podem não ser referenciados por meio de outro conteúdo AEM.

#### Ativos gerenciados existentes {#existing-managed-assets}

Um usuário existente do AEM Sites e do Assets está usando o AEM Assets para gerenciar todo o material digital para todos os canais. Eles estão desenvolvendo um aplicativo móvel nativo e precisam usar vários ativos gerenciados pela AEM Assets. Por exemplo, logotipos, imagens de fundo, ícones de botão etc.

Atualmente, esses valores são distribuídos no repositório Ativos. Os arquivos que o aplicativo precisa referenciar estão em:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Acessar Entidades de Ativos do CS {#accessing-cs-asset-entities}

Vamos deixar de lado as etapas de como a página é disponibilizada por meio da API por enquanto (ela será coberta pela descrição da interface do usuário AEM) e assumir que foi feita. As entidades de ativos foram criadas e adicionadas ao espaço &quot;appImages&quot;. Pastas adicionais foram criadas no espaço para fins de organização. Portanto, as entidades do ativo são armazenadas no JCR AEM como:

* /content/entity/appImages/logos/logo_light
* /content/entity/appImages/logos/logo_escuro
* /content/entity/appImages/bkgnd/gray_blue
* /content/entity/appImages/icons/carrinho
* /content/entity/appImages/icons/home

#### Obtendo uma lista de entidades de ativos disponíveis {#getting-a-list-of-available-asset-entities}

Um desenvolvedor de aplicativos pode obter uma lista de quais ativos estão disponíveis, recuperando as entidades de ativos. O terminal de espaço do Content Services pode fornecer essas informações por meio do SDK da API do serviço da Web.

O resultado seria um objeto em um formato JSON que forneceria uma lista dos ativos na pasta &quot;ícones&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obtendo uma imagem {#getting-an-image}

O JSON fornece um URL para cada imagem, gerada pelos Serviços de conteúdo para a imagem.

Para obter o binário para a imagem do &quot;carrinho&quot;, a biblioteca do cliente é usada novamente.

## Conteúdo HTML empacotado {#packaged-html-content}

O conteúdo HTML é necessário para clientes que precisam manter o layout do conteúdo. Isso é útil para aplicativos nativos que estão usando um container da Web - como uma visualização da Web do Cordova - para exibir o conteúdo.

AEM Content Services poderá fornecer conteúdo HTML para o aplicativo móvel por meio da API. Os clientes que desejam expor AEM conteúdo como HTML criarão uma entidade de página HTML que aponte para a fonte de conteúdo AEM.

As seguintes opções são consideradas:

* **Arquivo Zip:** para ter a melhor chance de exibir corretamente no dispositivo, todo o material referenciado da página - css, JavaScript, ativos etc. - será incluído em um único arquivo compactado com a resposta. As referências na página HTML serão ajustadas para usar um caminho relativo para esses arquivos.
* **Streaming:** obter um manifesto dos arquivos necessários da AEM. Em seguida, use esse manifesto para solicitar todos os arquivos (HTML, CSS, JS etc.) com solicitações subsequentes.

![chlimage_1-157](assets/chlimage_1-157.png)

## Conteúdo independente do canal {#channel-independent-content}

O conteúdo independente do canal é uma forma de expor construções de conteúdo AEM - como páginas - sem se preocupar com layout, componentes ou outras informações específicas do canal.

Essas entidades de conteúdo são geradas usando um modelo de conteúdo para traduzir as estruturas AEM em um formato JSON. Os dados JSON resultantes contêm informações sobre os dados do conteúdo, que são dissociados do repositório AEM. Isso inclui o retorno de metadados e links de referência AEM para ativos, bem como as relações entre estruturas de conteúdo - incluindo hierarquia de entidades.

### Gerenciando conteúdo independente do Canal {#managing-channel-independent-content}

O conteúdo pode acessar o aplicativo de várias maneiras.

1. Conteúdo de GET ZIPS via AEM Over-the-Air

   * Os manipuladores de Sincronização de conteúdo podem atualizar o pacote zip diretamente ou chamando os renderizadores de conteúdo existentes

      * Manipuladores de plataforma
      * Manipuladores de AEMM
      * Manipuladores personalizados

1. conteúdo de GET diretamente por meio de renderizadores de conteúdo

   * Renderizadores padrão prontos para uso
   * Renderizadores de conteúdo do AEM Mobile/Content Services
   * Renderizações personalizadas

