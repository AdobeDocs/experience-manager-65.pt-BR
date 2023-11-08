---
title: Criação e edição de aplicativos usando o console Aplicativos
description: Siga esta página para saber como criar e editar aplicativos usando o console de aplicativos.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '2685'
ht-degree: 0%

---

# Criação e edição de aplicativos usando o console Aplicativos{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O processo de desenvolvimento de aplicativos móveis para AEM reconhece que usuários de diferentes especialidades contribuem para o desenvolvimento de aplicativos móveis. O mapa de processos a seguir ilustra a ordem geral na qual os autores de conteúdo e desenvolvedores de aplicativos executam tarefas.

![chlimage_1-10](assets/chlimage_1-10.gif)

As informações sobre como executar as tarefas do profissional de marketing são exibidas nesta página. Para obter informações sobre as tarefas do desenvolvedor, consulte Criação de aplicativos PhoneGap.

## A estrutura dos aplicativos móveis {#the-structure-of-mobile-applications}

A AEM Mobile fornece o blueprint do aplicativo Phonegap para a criação de aplicativos móveis. O blueprint define a estrutura dos aplicativos que você cria. Os aplicativos consistem nos seguintes itens:

* A página raiz.
* As variações de idioma do aplicativo.
* A página inicial da variação de idioma.

### A raiz de um aplicativo Phonegap {#the-root-of-a-phonegap-app}

A página raiz dos aplicativos móveis criados no AEM é exibida no console Aplicativos.

A página raiz é armazenada abaixo da propriedade Destination Path do aplicativo que foi especificado na criação do aplicativo (o caminho padrão é /content/phonegap/apps). O nome da página é a propriedade Name do aplicativo. Por exemplo, o URL padrão da página raiz do site chamado `myphonegapapp` é `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### A variação de idioma de um aplicativo PhoneGap {#the-language-variation-of-a-phonegap-app}

As primeiras páginas secundárias da página raiz são as variações de idioma do aplicativo. O nome de cada página é o idioma para o qual o aplicativo é criado. Por exemplo, inglês é o nome da variação em inglês do aplicativo.

**Nota:** O blueprint padrão do PhoneGap cria apenas um aplicativo em inglês. Seu desenvolvedor pode modificar o blueprint para que ele possa criar mais variações de idioma.

![chlimage_1-147](assets/chlimage_1-147.png)

A página de idioma tem dois propósitos:

* O conteúdo da página é a página inicial da variação de idioma do aplicativo.
* As propriedades da página controlam vários aspectos de design do aplicativo, como o URL a ser usado para solicitar atualizações de conteúdo e informações sobre a conexão com a build da nuvem e a integração dos Serviços Adobe Analytics.

![chlimage_1-148](assets/chlimage_1-148.png)

### A Página Inicial {#the-home-page}

A página inicial ou index.html de uma variação de idioma de um aplicativo é exibida quando o aplicativo é aberto. A página inicial fornece aos usuários um menu de links para várias páginas no aplicativo. O sistema de parágrafo permite adicionar componentes à página para criar conteúdo.

## Criação de um aplicativo para dispositivos móveis {#creating-a-mobile-application}

Os aplicativos móveis são baseados em um blueprint que define a estrutura e as propriedades da página. Você pode configurar as seguintes propriedades do aplicativo:

* **Título:** O título do aplicativo.
* **Caminho de destino:** O local no repositório onde o aplicativo está armazenado. Deixe o padrão para criar um caminho com base no nome do aplicativo.

* **Nome:** O valor padrão é o valor da propriedade Title com caracteres de espaço removidos. O nome é usado no CQ para fazer referência ao aplicativo, por exemplo, para o nó do repositório que representa o aplicativo.
* **Descrição:** Uma descrição do aplicativo.
* **URL do servidor:** O URL que fornece atualizações de conteúdo OTA (Over-the-Air) para o aplicativo. O valor padrão é o URL do servidor de publicação da instância usada para criar um aplicativo (retirado do serviço do externalizador). Observe que essa deve ser uma instância do servidor de publicação, em vez de um autor, o que requer autenticação.

Você também pode fornecer um arquivo de imagem para usar como miniatura do aplicativo, selecionar a configuração de PhoneGap Build a ser usada e selecionar a configuração de análise do aplicativo móvel a ser usada. Essa imagem só é usada como uma miniatura para representar seu aplicativo móvel no console de aplicativos móveis no Experience Manager.

Existem guias adicionais (e opcionais) para o serviço de nuvem de build e para integrar o plug-in SDK do Adobe Mobile Services ao seu aplicativo.

* Build: clique em gerenciar configurações e configure o serviço de build build.phonegap.com aqui. Em seguida, no menu suspenso, é possível selecionar o serviço de nuvem do PhoneGap Build recém-criado.
* Analytics: clique em gerenciar configurações e configure seu [SDK do Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) serviços na nuvem. Em seguida, no menu suspenso, é possível selecionar o Mobile Service recém-criado para integrar ao aplicativo móvel.

>[!NOTE]
>
>Os desenvolvedores podem usar o AEM PhoneGap Starter Kit para criar aplicativos e adicioná-los ao console.

O procedimento a seguir usa a interface para toque para criar um aplicativo para dispositivos móveis.

1. No painel, clique em Aplicativos.
1. Clique no ícone Criar.

   ![O ícone Criar indicado por um sinal de mais dentro de um quadrado.](do-not-localize/chlimage_1-7.png)

1. (Opcional) Na guia Avançado, forneça uma descrição para o aplicativo e altere o URL do servidor, se necessário.
1. (Opcional) Se estiver usando PhoneGap Build para compilar o aplicativo, na guia Criar, selecione a Configuração a ser usada.

   Para criar uma configuração de criação do PhoneGap, clique em Gerenciar configurações.

1. (Opcional) Se estiver usando o SiteCatalyst para rastrear a atividade do aplicativo, na guia Analytics, selecione a configuração a ser usada.

   Para criar uma configuração de aplicativo móvel, clique em Gerenciar configurações.

1. (Opcional) Para fornecer um ícone de aplicativo, clique no botão Procurar, selecione o arquivo de imagem no sistema de arquivos e clique em Abrir.
1. Clique em Criar.

### Alterando as Propriedades de um Aplicativo Móvel {#changing-the-properties-of-a-mobile-application}

Após criar um aplicativo para dispositivos móveis, você pode alterar as propriedades.

#### Alterar o título, a descrição e o ícone {#change-the-title-description-and-icon}

1. No painel, clique ou toque em Aplicativos.
1. Selecione o aplicativo a ser configurado e clique no ícone Propriedades da página de exibição.

   ![O ícone Exibir propriedades da página indicado pela letra I dentro de um círculo.](do-not-localize/chlimage_1-8.png)

1. Para alterar os valores de propriedade, clique ou toque no ícone Editar.

   ![O ícone Edit indicado por um lápis.](do-not-localize/chlimage_1-9.png)

1. Configure as propriedades Básicas e Avançadas e clique ou toque no ícone Concluído.

   ![O ícone Concluído indicado por um símbolo de marca de seleção.](do-not-localize/chlimage_1-10.png)

#### Configurar uma variação de idioma do aplicativo {#configure-a-language-variation-of-the-application}

1. No painel, clique em Aplicativos.
1. Clique para fazer drill-into no aplicativo móvel que deseja editar no Admin Console de aplicativos. Selecione a versão do idioma do aplicativo a ser configurado e clique no ícone Exibir propriedades do aplicativo.

   ![O ícone Exibir Propriedades do Aplicativo indicado pela letra I dentro de um círculo.](do-not-localize/chlimage_1-11.png)

1. Para alterar os valores de propriedade, clique ou toque no ícone Editar.

   ![O ícone Edit indicado por um lápis.](do-not-localize/chlimage_1-12.png)

1. Configure as propriedades nas guias Básico, Avançado, Criar e Analytics e clique ou toque no ícone Concluído.

   ![O ícone Concluído indicado por um símbolo de marca de seleção.](do-not-localize/chlimage_1-13.png)

### Criação do conteúdo de um aplicativo móvel {#authoring-the-content-of-a-mobile-application}

Depois de criar o aplicativo móvel, adicione o conteúdo que é usado como a interface do usuário do aplicativo.

1. No painel, clique ou toque em Aplicativos.
1. Clique ou toque no aplicativo e, em seguida, em inglês.
1. Edite a Home page ou adicione páginas secundárias conforme necessário.

### Mover conteúdo para aplicativos móveis {#moving-content-to-mobile-applications}

O cache da sincronização de conteúdo na instância de publicação do AEM é usado como um repositório de conteúdo para aplicativos móveis:

* O conteúdo do cache da Sincronização de conteúdo é incluído no aplicativo quando os desenvolvedores o compilam.
* O conteúdo no cache está disponível para aplicativos móveis instalados para atualizar o conteúdo do aplicativo.

Os aplicativos móveis incluem um comando Atualizações que baixa e instala o conteúdo atualizado do aplicativo. Quando uma instância do aplicativo envia uma solicitação de atualização, a Sincronização de conteúdo determina qual conteúdo foi alterado desde a última vez que o aplicativo foi atualizado ou instalado e fornece o novo conteúdo.

![chlimage_1-149](assets/chlimage_1-149.png)

Para disponibilizar o conteúdo atualizado para os aplicativos, atualize o cache da Sincronização de Conteúdo. Na primeira vez que você atualizar o cache, todo o conteúdo publicado será adicionado. Atualizações subsequentes adiciona somente o conteúdo publicado que foi alterado desde a atualização anterior.

A Sincronização de conteúdo também rastreia quando as atualizações ocorrem. Com essas informações, a Sincronização de conteúdo pode determinar qual atualização de cache enviar para um aplicativo móvel.

Execute o procedimento a seguir na instância em que deseja atualizar o cache. Por exemplo, se o aplicativo solicitar atualizações da instância de publicação, execute o procedimento na instância de publicação.

1. No painel, clique ou toque em Aplicativos e, em seguida, clique ou toque no aplicativo.
1. Selecione a página inicial e clique ou toque no ícone Atualizar cache.

   ![O ícone Atualizar cache indicado por um barrell listrado com um símbolo de reciclagem sobre ele.](do-not-localize/chlimage_1-14.png)

### Utilização de modelos de aplicativo {#using-app-templates}

Este é um recurso que está disponível no Feature Pack 2 do Apps 6.1 e fornece uma maneira fácil de usar os modelos de aplicativo existentes para a criação de novos aplicativos no AEM.

O que é um modelo de aplicativo? Pense nisso como uma coleção de modelos de página e componentes que representam uma linha de base ou base de um aplicativo.
Ao criar um aplicativo com base no modelo de outro aplicativo, você obterá um aplicativo que tem um ponto de partida representativo do aplicativo no qual ele foi criado.

Você deve ter um modelo de aplicativo móvel existente (ou um aplicativo instalado que tenha um modelo de aplicativo) para usar este recurso.

O pacote de amostras mais recente do AEM Apps 6.1 inclui uma versão atualizada do Geometrixx com um modelo de aplicativo. Como alternativa, você pode instalar o StarterKit, que também fornece um template.

Etapas para criar um aplicativo com base em um modelo de aplicativo:

1. Verifique se você tem o pacote de recursos e os pacotes de amostras de referência do AEM Apps 6.1 mais recentes instalados
1. Clique em Aplicativos no painel esquerdo.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Clique no botão + Criar na parte superior e selecione Criar aplicativo.
1. Depois de receber a lista de Modelos de aplicativo, selecione um:

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Clique em Avançar.
1. Forneça uma ID e um título do aplicativo, mas convém incluir também um Nome e uma Descrição.

   1. Além disso, você pode fornecer um PNG (formato de ícone do PhoneGap compatível) como um ícone navegando pelos ativos do AEM.
   1. Lembre-se de que você pode editar todos esses campos após a criação do aplicativo no bloco Gerenciar aplicativo. Com exceção da ID do aplicativo, após a definição da ID do aplicativo, você não poderá alterá-la.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Clique no botão criar e 2 opções serão exibidas, Concluído (voltar para a exibição do catálogo de aplicativos) ou Gerenciar aplicativo (abre o painel do aplicativo).
1. Depois de criado, você deve ver o novo aplicativo listado no Catálogo de aplicativos:

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Clique no aplicativo para abri-lo; você criou um novo aplicativo com base no modelo de um aplicativo existente.

>[!NOTE]
>
>Se você desinstalar o pacote de aplicativo de referência Geometrixx Outdoors do AEM e criar um aplicativo com base em seu modelo, esse aplicativo não estará mais funcional. O aplicativo Geometrixx Outdoors pode ser removido, no entanto, o modelo de aplicativo deve permanecer se for usado por outros aplicativos móveis.

## Explorar o aplicativo de amostra Geometrixx Outdoors {#exploring-the-sample-geometrixx-outdoors-app}

O aplicativo Geometrixx Outdoors é um aplicativo PhoneGap de amostra que demonstra os recursos do blueprint padrão do aplicativo PhoneGap e os componentes móveis de amostra.

Para abrir o aplicativo, no painel, clique em Aplicativos móveis e selecione Geometrixx Outdoors.

### Recursos comuns da página - Aplicativo para dispositivos móveis Geometrixx {#common-page-features-geometrixx-mobile-app}

Cada página do aplicativo móvel inclui os seguintes recursos:

* Um botão Voltar para retornar à página principal. O botão Voltar não é exibido na página inicial.
* Um painel dispensável que oferece um menu de comandos e links:

   * Abra a página Locais.
   * Abra o carrinho.
   * Fazer logon.
   * Atualize o aplicativo.

* O sistema de parágrafo, para adicionar componentes e criar conteúdo.

### A página inicial - Aplicativo para dispositivos móveis Geometrixx {#the-home-page-geometrixx-mobile-app}

O conteúdo da página inicial é composto pelas seguintes ferramentas de navegação:

* Um componente Lista de menus que fornece links para as páginas secundárias Engrenagem, Revisões, Notícias e Sobre nós.
* Um componente Carrossel de deslizamento que mostra as páginas secundárias.

### A página de engrenagens - Aplicativo para dispositivos móveis Geometrixx {#the-gear-page-geometrixx-mobile-app}

A página de engrenagem fornece aos usuários acesso às páginas de produtos. Um componente de lista de menus fornece acesso às páginas secundárias da página de engrenagens. As páginas secundárias são categorias de produtos que o site apresenta.

* Temporada
* Vestuário
* Sexo
* Atividade

Cada página de categoria usa a mesma estrutura de conteúdo que a página de engrenagem. O carrossel fornece acesso a páginas secundárias que são subcategorias de produtos. As páginas de subcategoria contêm listas de produtos que fornecem links para páginas de produtos.

### A página de produtos - Aplicativo móvel Geometrixx {#the-products-page-geometrixx-mobile-app}

A página Produtos e sua hierarquia de páginas secundárias implementam um sistema de classificação para páginas de produtos. As páginas inferiores em cada ramificação da hierarquia são uma página de produto que contém um componente Produto ng.

A página Produtos não está disponível para usuários do aplicativo. A página de engrenagens fornece acesso a cada página de produto.

### A página de revisões - Aplicativo móvel Geometrixx {#the-reviews-page-geometrixx-mobile-app}

Contém um botão Voltar. O sistema de parágrafo permite adicionar componentes.

Ao usar o aplicativo, a página Revisões está disponível no carrossel da página em inglês.

### A página de notícias - Aplicativo para dispositivos móveis Geometrixx {#the-news-page-geometrixx-mobile-app}

Contém um botão Voltar. O sistema de parágrafo permite adicionar componentes.

Ao usar o aplicativo, a página Notícias está disponível no carrossel da página em inglês.

### A página Quem somos - Aplicativo para dispositivos móveis Geometrixx {#the-about-us-page-geometrixx-mobile-app}

A página Sobre nós contém vários componentes Linha de duas colunas. Cada coluna contém um componente Imagem ou Texto. Os componentes são editáveis e o sistema de parágrafos permite adicionar componentes.

Ao usar o aplicativo, a página Sobre nós está disponível no carrossel da página em inglês.

### A página de locais - Aplicativo móvel Geometrixx {#the-locations-page-geometrixx-mobile-app}

A página Locais contém um componente de Locais.

Ao usar o aplicativo, a página Locais está disponível na lista de menus da página em inglês.

## Componentes móveis de exemplo {#sample-mobile-components}

Vários componentes estão imediatamente disponíveis no Sidekick ao criar as páginas de um aplicativo móvel. Os componentes pertencem ao grupo de componentes PhoneGap.

### Carrossel de troca {#swipe-carousel}

O componente Carrossel de deslizamento é uma ferramenta para exibir e navegar pelas páginas do site. O componente inclui um carrossel que circula por imagens para as páginas acima de uma lista de links de página. Edite o componente para especificar as páginas a serem expostas e o comportamento do carrossel.

Observe que as imagens são exibidas no carrossel para páginas associadas a uma imagem de uma maneira específica. Quando as páginas não estão associadas a imagens, somente a lista de links é exibida.

![chlimage_1-151](assets/chlimage_1-151.png)

**Guia Propriedades do carrossel**

Configure o comportamento do carrossel:

* Velocidade de reprodução: o tempo em milissegundos que cada imagem é exibida antes de mostrar a próxima imagem.
* Tempo de transição: a duração da animação, em milissegundos, das transições de imagem.
* Estilo de controles: o tipo de controles que são fornecidos para a movimentação entre imagens.

**Guia Propriedades da lista**

Especifique como a lista de páginas é gerada:

* Uso da lista de criação: o método a ser usado para especificar as páginas a serem incluídas no carrossel. Consulte Criação da lista de páginas.
* Ordenar por: selecione uma propriedade de página a ser usada para classificar a lista de páginas. Por exemplo, selecione jcr:title para classificar páginas alfabeticamente por título.
* Limite: o número máximo de páginas a serem incluídas. Essa propriedade é adequada para métodos baseados em pesquisa para criar a lista de páginas.

#### Criação da lista de páginas {#building-the-page-list}

O componente Carrossel de deslizamento fornece os seguintes valores para a propriedade Uso da lista de construção. A caixa de diálogo de edição é alterada de acordo com o valor selecionado:

**Páginas secundárias**

O componente lista todas as páginas secundárias de uma página específica. Após selecionar esse valor, selecione a página na guia Páginas secundárias ou não especifique nenhum valor para listar as secundárias da página atual.

**Lista fixa**

Especifique uma lista de páginas de inclusão. Após selecionar esse valor, configure a lista na guia Lista fixa que aparece ao selecionar Lista fixa:

* Para adicionar uma página, clique em Adicionar item e procure a página.
* Use os ícones de seta para cima e para baixo para mover a página dentro da lista.
* Clique no botão Remover para remover uma página da lista.

A propriedade Order By não afeta a ordem das listas fixas.

**Pesquisar**

Preencha a lista usando os resultados de uma pesquisa por palavra-chave. A pesquisa é executada nos filhos de uma página especificada por você:

1. Para especificar a página raiz da pesquisa, use a propriedade Iniciar em para selecionar o caminho da página. Não especifique nenhum caminho para pesquisar abaixo da página atual.
1. Na propriedade Pesquisar consulta, digite as palavras-chave de pesquisa.

**Pesquisa avançada**

Preencha a lista usando um [Querybuilder](/help/sites-developing/querybuilder-api.md) consulta.

### Imagem {#image}

Adicione uma imagem ao conteúdo do aplicativo.

### Texto {#text}

Adicione rich text ao conteúdo do aplicativo.

### Armazenar locais {#store-locations}

O componente de Locais de loja fornece aos usuários ferramentas para encontrar pontos de venda de negócios:

* Pesquisar
* Listas de locais próximos ou distantes das coordenadas GPS do dispositivo.

O componente exige que o repositório contenha informações de localização para cada armazenamento. Os locais de amostra são instalados no nó /etc/commerce/locations/adobe. ![chlimage_1-152](assets/chlimage_1-152.png)

### Linha de duas colunas {#two-column-row}

Permite adicionar componentes lado a lado a uma página.

![chlimage_1-153](assets/chlimage_1-153.png)
