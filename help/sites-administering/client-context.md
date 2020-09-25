---
title: ClientContext
seo-title: ClientContext
description: Saiba como usar o Contexto do cliente no AEM.
seo-description: Saiba como usar o Contexto do cliente no AEM.
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 0%

---


# ClientContext{#client-context}

>[!NOTE]
>
>O Contexto do cliente foi substituído pelo ContextHub. Para obter mais detalhes, consulte a documentação relacionada []configurationch-configuring.md) e [desenvolvedor](/help/sites-developing/contexthub.md) .

O Contexto do cliente é um mecanismo que fornece determinadas informações sobre a página e o visitante atuais. Ele pode ser aberto usando **Ctrl-Alt-c** (windows) ou **control-option-c** (Mac):

![](assets/clientcontext_alisonparker.png)

No ambiente [publish e author, ele mostra informações](#propertiesavailableintheclientcontext) sobre:

* O visitante; dependendo da sua instância, determinadas informações são solicitadas ou derivadas.
* Tags de página e o número de vezes que essas tags foram acessadas pelo visitante atual (isso é mostrado quando você move o mouse sobre uma tag específica).
* Informações da página.
* Informações sobre o ambiente técnico; como endereço IP, navegador e resolução de tela.
* Todos os segmentos que estão resolvidos no momento.

Os ícones (disponíveis apenas no ambiente do autor) permitem que você configure os detalhes do contexto do cliente:

![](do-not-localize/clientcontext_icons.png)

* **Editar** Uma nova página será aberta permitindo que você [edite, adicione ou remova uma propriedade](#editingprofiledetails)de perfil.

* **Carregamento** Você pode [selecionar uma lista de perfis e carregar o perfil](#loading-a-new-user-profile) que deseja testar.

* **Redefinir** Você pode [redefinir o perfil](#resetting-the-profile-to-the-current-user) para o do usuário atual.

## Componentes de contexto do cliente disponíveis {#available-client-context-components}

O Contexto do cliente pode mostrar as seguintes propriedades ([dependendo do que foi selecionado usando Editar](#adding-a-property-component)):

**Informações** sobre a busca mostra as seguintes informações do lado do cliente:

* o endereço **IP**
* **palavras-chave** usadas para referência do mecanismo de pesquisa
* o **navegador** que está sendo usado
* o **SO** (sistema operacional) que está sendo usado
* a **resolução da tela**
* a posição X **do** mouse
* a posição Y **do** mouse

**Fluxo** de atividadesFornece informações sobre a atividade social do usuário em várias plataformas; por exemplo, fóruns de AEM, blogs, classificações etc.

**Campanha** Permite que os autores simulem uma experiência específica para uma campanha. Este componente substitui a resolução de campanha normal e a seleção de experiência para permitir o teste de várias permutações.

A resolução da campanha normalmente se baseia na propriedade priority da campanha. A experiência é normalmente selecionada com base na segmentação.

**Carrinho** Mostra informações do carrinho de compras incluindo entradas do produto (título, quantidade, preçoFormatado etc.), promoções resolvidas (título, mensagem etc.) e vales (código, descrição, etc.).

O armazenamento de sessão de carrinho também notifica o servidor sobre alterações de promoção resolvidas (com base em alterações de segmentação) usando o ClientContextCartServlet.

**Loja** genérica é um componente genérico que exibe o conteúdo de uma loja. É uma versão de nível inferior do componente Propriedades genéricas de armazenamento.

O Arquivo Genérico deve ser configurado com um renderizador JS que exibirá os dados de maneira personalizada.

**Propriedades** de armazenamento genéricas É um componente genérico que exibe o conteúdo de uma loja. É uma versão de nível superior do componente de Loja genérica.

O componente Propriedades genéricas de armazenamento inclui um renderizador padrão que lista as propriedades configuradas (junto com uma miniatura).

**Localização geográfica** Mostra a latitude e a longitude do cliente. Ele usa a API de geolocalização HTML5 para query do navegador para o local atual. Isso resulta na exibição de um pop-up ao visitante, onde o navegador pergunta se ele concorda em compartilhar sua localização.

Quando exibido na Context Cloud, o componente usa uma API do Google para exibir um mapa como miniatura. O componente está sujeito aos limites [de](https://developers.google.com/maps/documentation/staticmaps/intro#Limits)uso da API do Google.

>[!NOTE]
>
>No AEM 6.1, o armazenamento Geolocation não fornece mais o recurso de geocodificação reversa. Portanto, o armazenamento Localização geográfica não recupera mais detalhes sobre o local atual, como o nome da cidade ou o código do país. Os segmentos que usam esses dados de armazenamento não funcionarão corretamente. O armazenamento Localização geográfica contém apenas a latitude e a longitude de um local.

**Loja** JSONP Um componente que exibe conteúdo que depende de sua instalação.

O padrão JSONP é um complemento do JSON que permite a evasão da mesma política de origem (impossibilitando que um aplicativo da Web se comunique com servidores que estão em outro domínio). Consiste em vincular o objeto JSON em uma chamada de função para poder carregá-lo como um `<script>` de outro domínio (que é uma exceção permitida para a mesma política de origem).

A loja JSONP é como qualquer outra loja, mas carrega informações que vêm de outro domínio sem a necessidade de ter um proxy para essas informações no domínio atual. Consulte o exemplo em [Armazenamento de dados no contexto do cliente via JSONP](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>A loja JSONP não armazena as informações em cache no cookie, mas recupera os dados em cada carregamento de página.

**Dados** do perfil Mostra as informações coletadas no perfil do usuário. Por exemplo, gênero, idade, endereço de email, entre outros.

**Segmentos** resolvidos Mostra quais segmentos são resolvidos no momento (geralmente dependendo de outras informações mostradas no contexto do cliente). Isso é de interesse ao configurar uma campanha.

Por exemplo, se o mouse está atualmente sobre a parte esquerda ou direita da janela. Este segmento é usado principalmente para testes, já que as alterações podem ser vistas imediatamente.

**Gráfico** social Mostra o gráfico social dos amigos e seguidores do usuário.

>[!NOTE]
>
>Atualmente, este é um recurso de demonstração que depende de um conjunto de dados pré-configurado nos nós do perfil de nossos usuários de demonstração. Por exemplo, consulte:
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => propriedade friends

**Nuvem** de tags Mostra as tags definidas na página atual e as obtidas durante a navegação no site. Mover o mouse sobre uma tag mostra o número de vezes que o usuário atual acessou páginas que mantêm essa tag específica.

>[!NOTE]
As tags definidas nos ativos DAM exibidos nas páginas visitadas não serão contadas.

**Loja** de tecnográficos Este componente depende da sua instalação.

**Produtos** visualizadosAcompanha os produtos que o comprador visualizou. Pode ser consultado para o produto visualizado mais recentemente ou para o produto visualizado mais recentemente que ainda não está no carrinho.

Este armazenamento de sessão não tem componente de contexto de cliente padrão.

Para obter informações adicionais, consulte Contexto [do cliente em Detalhe](/help/sites-developing/client-context.md).

>[!NOTE]
Os Dados da página não estão mais no contexto do cliente como um componente padrão. Se necessário, é possível adicionar isso editando o contexto do cliente, adicionando o componente Propriedades **da loja** genérica e configurando-o para definir a **Loja** como `pagedata`.

## Alteração do Perfil de contexto do cliente {#changing-the-client-context-profile}

O Contexto do cliente permite alterar os detalhes interativamente:

* Alterar o perfil que está sendo usado no Contexto do cliente permite que você veja as diferentes experiências que vários usuários verão para a página atual.
* Além de alterar o perfil do usuário, você pode alterar alguns detalhes do perfil para ver como a experiência da página difere sob várias condições.

### Carregando um novo Perfil de usuário {#loading-a-new-user-profile}

Você pode alterar o perfil:

* [usando o ícone de carregamento](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [usando o controle deslizante de seleção](#loadinganewvisitorprofilewiththeselectionslider)

Quando terminar, você poderá [redefinir o perfil](#resetting-the-profile-to-the-current-user).

#### Carregando um novo Perfil de Visitante com o ícone Carregar Perfil {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. Clique no ícone Carregar Perfil:

   ![](do-not-localize/clientcontext_loadprofile.png)

1. Isso abrirá a caixa de diálogo, onde você pode selecionar o perfil que deseja carregar:

   ![](assets/clientcontext_profileloader.png)

1. Click **OK** to load.

#### Carregando um novo Perfil de usuário com o controle deslizante de seleção {#loading-a-new-user-profile-with-the-selection-slider}

Você também pode selecionar um perfil com o controle deslizante de seleção:

1. Clique com o duplo no ícone que representa o usuário atual. O seletor abrirá, use as setas para navegar e ver as perfis disponíveis:

   ![](assets/clientcontext_profileselector.png)

1. Clique no perfil que deseja carregar. Quando os detalhes tiverem sido carregados, clique fora do seletor para fechar.

#### Redefinição do Perfil para o usuário atual {#resetting-the-profile-to-the-current-user}

1. Use o ícone de redefinição para retornar o perfil no Contexto do cliente ao do usuário atual:

   ![](do-not-localize/clientcontext_resetprofile.png)

### Alteração da plataforma do navegador {#changing-the-browser-platform}

1. Clique com o duplo no ícone que representa a plataforma do navegador. O seletor será aberto, use as setas para navegar e ver as plataformas/navegadores disponíveis:

   ![](assets/clientcontext_browserplatform.png)

1. Clique no navegador da plataforma que deseja carregar. Quando os detalhes tiverem sido carregados, clique fora do seletor para fechar.

### Alteração da localização geográfica {#changing-the-geolocation}

1. Clique com o duplo no ícone de geolocalização. Um mapa expandido será aberto, aqui você pode arrastar o marcador para um novo local:

   ![](assets/clientcontext_geomocationrelocate.png)

1. Clique fora do mapa para fechar.

### Alteração da seleção de tags {#changing-the-tag-selection}

1. Clique com o duplo na seção Nuvem de tags do Contexto do cliente. A caixa de diálogo será aberta, onde você pode selecionar as tags:

   ![](assets/clientcontext_tagselection.png)

1. Clique em OK para carregar no Contexto do cliente.

## Editar o contexto do cliente {#editing-the-client-context}

A edição de um contexto de cliente pode ser usada para definir (ou redefinir) os valores de determinadas propriedades, adicionar uma nova propriedade ou remover uma que não seja mais necessária.

### Editando detalhes da propriedade {#editing-property-details}

A edição de um contexto de cliente pode ser usada para definir (ou redefinir) os valores de determinadas propriedades. Isso permite testar cenários específicos (especialmente úteis para [segmentação](/help/sites-administering/campaign-segmentation.md) e [campanhas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)).

![](assets/clientcontext_alisonparker_edit.png)

### Adicionar um componente de propriedade {#adding-a-property-component}

Depois de abrir a página **de design do** ClientContext, você também pode **Adicionar** uma propriedade completamente nova usando os componentes disponíveis (os componentes são listados no sidekick ou na caixa de diálogo **Inserir novo componente** , aberta após um clique do duplo na caixa **Arrastar componentes ou ativos aqui** ):

![](assets/clientcontext_alisonparker_new.png)

### Remoção de um componente de propriedade {#removing-a-property-component}

Depois de abrir a página **de design do** ClientContext, também é possível **Remover** uma propriedade se não for mais necessário. Inclui propriedades fornecidas prontamente; **Se tiverem sido removidos, a redefinição** os reinstalará.

## Armazenamento de dados no contexto do cliente via JSONP {#storing-data-in-client-context-via-jsonp}

Siga este exemplo para usar o componente de armazenamento de contexto da loja JSONP para adicionar dados externos ao Contexto do cliente. Em seguida, crie um segmento com base nas informações desses dados. O exemplo usa o serviço JSONP fornecido pelo WIPmania.com. O serviço retorna informações de localização geográfica com base no endereço IP do cliente Web.

Este exemplo usa o site de amostra de Geometrixx Outdoors para acessar o Contexto do cliente e testar o segmento criado. Você pode usar um site diferente, desde que a página tenha ativado o Contexto do cliente. (Consulte [Adicionar o contexto do cliente a uma página](/help/sites-developing/client-context.md#adding-client-context-to-a-page).)

### Adicionar o componente da loja JSONP {#add-the-jsonp-store-component}

Adicione o componente da loja JSONP ao Contexto do cliente e use-o para recuperar e armazenar informações de localização geográfica sobre o cliente Web.

1. Abra o home page em inglês do site de Geometrixx Outdoors na instância do autor AEM. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Para abrir o Contexto do cliente, pressione Ctrl-Alt-c (windows) ou control-option-c (Mac).
1. Clique no ícone de edição na parte superior do Contexto do cliente para abrir o Designer de contexto do cliente.

   ![](do-not-localize/chlimage_1.png)

1. Arraste o componente JSONP Store para o Contexto do cliente.

   ![](assets/chlimage_1-4.jpeg)

1. Clique no componente com o duplo do mouse para abrir a caixa de diálogo de edição.
1. Na caixa URL do serviço JSONP, digite o seguinte URL e clique em Buscar armazenamento:

   `https://api.wipmania.com/jsonp?callback=${callback}`

   O componente chama o serviço JSONP e lista todas as propriedades que os dados retornados contêm. As propriedades que estão na lista são aquelas que estarão disponíveis no Contexto do cliente.

   ![](assets/chlimage_1-40.png)

1. Clique em OK.
1. Retorne ao home page Geometrixx Outdoors e atualize a página. O Contexto do cliente agora inclui as informações do componente da loja JSONP.

   ![](assets/chlimage_1-41.png)

### Criar o segmento {#create-the-segment}

Use os dados do armazenamento de sessão que você criou usando o componente de armazenamento JSONP. O segmento usa a latitude do armazenamento da sessão e a data atual para determinar se é a hora de inverno no local do cliente.

1. Abra o console Ferramentas no navegador da Web (`https://localhost:4502/miscadmin#/etc`).
1. Na árvore de pastas, clique na pasta Ferramentas/Segmentação e, em seguida, clique em Novo > Nova pasta. Especifique os seguintes valores de propriedade e clique em Criar:

   * Nome: mysegment
   * Título: Meus segmentos

1. Selecione a pasta Meus segmentos e clique em Nova > Nova página:

   1. Para o Título, digite Winter.
   1. Selecione o modelo de Segmento.
   1. Clique em Criar.

1. Clique com o botão direito do mouse no segmento de inverno e clique em Abrir.
1. Arraste a propriedade Loja genérica para o container AND padrão.

   ![](assets/chlimage_1-5.jpeg)

1. Clique no componente com o duplo do mouse para abrir a caixa de diálogo de edição, especifique os seguintes valores de propriedade e clique em OK:

   * Loja: wipmania
   * Nome da propriedade: latitude
   * Operador: é maior que
   * Valor da propriedade: 30

1. Arraste o componente Script para o mesmo container AND e abra a caixa de diálogo de edição. Adicione o seguinte script e clique em OK:

   `3 < new Date().getMonth() < 12`

