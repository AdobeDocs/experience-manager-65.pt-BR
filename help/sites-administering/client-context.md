---
title: ClientContext
seo-title: Client Context
description: Saiba como usar o Contexto do Cliente no AEM.
seo-description: Learn how to use the Client Context in AEM.
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: 02afc4eb78acaacc40d3ba1830ccb1e9c3907d0f
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 0%

---

# ClientContext{#client-context}

>[!NOTE]
>
>O Contexto do Cliente foi substituído pelo ContextHub. Para obter mais detalhes, consulte os [configuração](/help/sites-developing/ch-configuring.md) e [desenvolvedor](/help/sites-developing/contexthub.md) documentação.

O Contexto do Cliente é um mecanismo que fornece determinadas informações sobre a página atual e o visitante. Ele pode ser aberto usando **Ctrl-Alt-c** (janelas) ou **control-option-c** (Mac):

![](assets/clientcontext_alisonparker.png)

Em ambas as [ambiente de publicação e criação, ele mostra informações](#propertiesavailableintheclientcontext) sobre:

* O visitante; dependendo da sua instância, determinadas informações são solicitadas ou derivadas.
* Tags de página e o número de vezes que essas tags foram acessadas pelo visitante atual (isso é mostrado quando você move o mouse sobre uma tag específica).
* Informações da página.
* Informações sobre o ambiente técnico; como endereço IP, navegador e resolução de tela.
* Qualquer segmento que esteja resolvido no momento.

Os ícones (disponíveis apenas no ambiente do autor) permitem configurar os detalhes do contexto do cliente:

![](do-not-localize/clientcontext_icons.png)

* **Editar**
Uma nova página será aberta permitindo que você [editar, adicionar ou remover uma propriedade do perfil](#editingprofiledetails).

* **Carregar**
Você pode [selecione de uma lista de perfis e carregue o perfil](#loading-a-new-user-profile) você quer testar.

* **Redefinir**
Você pode [redefinir o perfil](#resetting-the-profile-to-the-current-user) ao do usuário atual.

## Componentes de contexto de cliente disponíveis {#available-client-context-components}

O Contexto do Cliente pode mostrar as seguintes propriedades ([dependendo do que foi selecionado usando Editar](#adding-a-property-component)):

**Informações de surfer** Mostra as seguintes informações do lado do cliente:

* o **Endereço IP**
* **palavras-chave** usado para referência do mecanismo de pesquisa
* o **navegador** em uso
* o **SO** (sistema operacional) em uso
* a tela **resolution**
* o **mouse X** position
* o **mouse Y** position

**Fluxo de atividade** Isso fornece informações sobre a atividade social do usuário em várias plataformas; por exemplo, os fóruns de AEM, blogs, classificações etc.

**Campanha** Permite que os autores simulem uma experiência específica para uma campanha. Esse componente substitui a resolução normal da campanha e a seleção da experiência para permitir o teste de várias permutas.

A resolução da campanha é normalmente baseada na propriedade priority da campanha. A experiência é normalmente selecionada com base na segmentação.

**Carrinho** Mostra informações do carrinho de compras, incluindo entradas do produto (título, quantidade, preço Formatado etc.), promoções resolvidas (título, mensagem etc.) e vales (código, descrição, etc.).

O armazenamento de sessão de carrinho também notifica o servidor sobre alterações de promoção resolvidas (com base em alterações de segmentação) usando o ClientContextCartServlet.

**Loja genérica** É um componente genérico que exibe o conteúdo de uma loja. É uma versão de nível inferior do componente Propriedades da loja genérica .

A Loja genérica deve ser configurada com um renderizador JS que exibirá os dados de maneira personalizada.

**Propriedades da Loja Genérica** É um componente genérico que exibe o conteúdo de uma loja. É uma versão de nível superior do componente de Loja Genérica.

O componente Propriedades da loja genérica inclui um renderizador padrão que lista as propriedades configuradas (junto com uma miniatura).

**Geolocalização** Mostra a latitude e a longitude do cliente. Ela usa a API de geolocalização do HTML5 para consultar o navegador quanto ao local atual. Isso resulta na exibição de um pop-up ao visitante, onde o navegador pergunta se ele concorda em compartilhar sua localização.

Quando exibido na Nuvem de contexto, o componente usa uma API do Google para exibir um mapa como miniatura. O componente está sujeito à API do Google [limites de uso](https://developers.google.com/maps/documentation/staticmaps/intro#Limits).

>[!NOTE]
>
>No AEM 6.1, o armazenamento Geolocation não fornece mais o recurso de geocodificação reversa. Portanto, o armazenamento de Geolocalização não recupera mais detalhes sobre a localização atual, como o nome da cidade ou o código do país. Os segmentos que usam esses dados de armazenamento não funcionarão corretamente. O armazenamento Geolocation contém apenas a latitude e a longitude de um local.

**Loja JSONP** Um componente que exibe conteúdo que depende de sua instalação.

O padrão JSONP é um complemento do JSON que permite contornar a mesma política de origem (impossibilitando que um aplicativo da Web se comunique com servidores que estão em outro domínio). Consiste em vincular o objeto JSON em uma chamada de função para poder carregá-lo como um `<script>` do outro domínio (que é uma exceção permitida para a mesma política de origem).

A Loja JSONP é como qualquer outra loja, mas carrega informações que vêm de outro domínio sem a necessidade de ter um proxy para essas informações no domínio atual. Veja o exemplo em [Armazenamento de dados no contexto do cliente via JSONP](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>A Loja JSONP não armazena as informações em cache no cookie, mas recupera esses dados em cada carregamento de página.

**Dados do perfil** Mostra as informações coletadas no perfil do usuário. Por exemplo, gênero, idade, endereço de email, entre outros.

**Segmentos resolvidos** Mostra quais segmentos atualmente são resolvidos (geralmente dependendo de outras informações mostradas no contexto do cliente). Isso é de interesse ao configurar uma campanha.

Por exemplo, se o mouse está atualmente sobre a parte esquerda ou direita da janela. Esse segmento é usado principalmente para testes, pois as alterações podem ser vistas imediatamente.

**Gráfico social** Mostra o gráfico social dos amigos e seguidores do usuário.

>[!NOTE]
>
>Atualmente, esse é um recurso de demonstração que depende de dados pré-configurados definidos nos nós de perfil dos nossos usuários de demonstração. Por exemplo, consulte:
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => propriedade friends

**Nuvem de tags** Mostra tags definidas na página atual e as obtidas durante a navegação no site. Mover o mouse sobre uma tag mostra o número de vezes que o usuário atual acessou páginas que contêm essa tag específica.

>[!NOTE]
As tags definidas em ativos DAM exibidos nas páginas visitadas não serão contadas.

**Armazenamento de recursos técnicos** Esse componente depende da sua instalação.

**Produtos visualizados** Mantém o controle dos produtos que o comprador visualizou. Pode ser consultado para o produto visualizado mais recentemente ou para o produto visualizado mais recentemente, que ainda não está no carrinho.

Este armazenamento de sessão não tem nenhum componente de contexto de cliente padrão.

Para obter mais informações, consulte [Contexto do cliente em detalhes](/help/sites-developing/client-context.md).

>[!NOTE]
Os dados da página não estão mais no contexto do cliente como um componente padrão. Se necessário, é possível adicionar isso editando o contexto do cliente, adicionando a variável **Propriedades da Loja Genérica** , em seguida, configure-o para definir a variável **Loja** as `pagedata`.

## Alteração do perfil de contexto do cliente {#changing-the-client-context-profile}

O Contexto do Cliente permite que você altere os detalhes interativamente:

* Alterar o perfil que está sendo usado no Contexto do Cliente permite que você veja as diferentes experiências que vários usuários verão para a página atual.
* Além de alterar o perfil do usuário, você pode alterar alguns detalhes do perfil para ver como a experiência da página difere sob várias condições.

### Carregar um novo perfil de usuário {#loading-a-new-user-profile}

Você pode alterar o perfil ao:

* [usando o ícone carregar](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [usando o controle deslizante de seleção](#loadinganewvisitorprofilewiththeselectionslider)

Quando terminar, você poderá [redefinir o perfil](#resetting-the-profile-to-the-current-user).

#### Carregamento de um novo perfil de visitante com o ícone Carregar perfil {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. Clique no ícone Carregar perfil :

   ![](do-not-localize/clientcontext_loadprofile.png)

1. Isso abrirá a caixa de diálogo , onde você pode selecionar o perfil que deseja carregar:

   ![](assets/clientcontext_profileloader.png)

1. Clique em **OK** para carregar.

#### Carregamento de um novo perfil de usuário com o controle deslizante de seleção {#loading-a-new-user-profile-with-the-selection-slider}

Você também pode selecionar um perfil com o controle deslizante de seleção:

1. Clique duas vezes no ícone que representa o usuário atual. O seletor será aberto, use as setas para navegar e ver os perfis disponíveis:

   ![](assets/clientcontext_profileselector.png)

1. Clique no perfil que deseja carregar. Quando os detalhes tiverem sido carregados, clique fora do seletor para fechar.

#### Redefinir o perfil para o usuário atual {#resetting-the-profile-to-the-current-user}

1. Use o ícone de redefinição para retornar o perfil no Contexto do Cliente para o do usuário atual:

   ![](do-not-localize/clientcontext_resetprofile.png)

### Alteração da plataforma do navegador {#changing-the-browser-platform}

1. Clique duas vezes no ícone que representa a plataforma do navegador. O seletor será aberto, use as setas para navegar e ver as plataformas/navegadores disponíveis:

   ![](assets/clientcontext_browserplatform.png)

1. Clique no navegador da plataforma que você deseja carregar. Quando os detalhes tiverem sido carregados, clique fora do seletor para fechar.

### Alterar a localização geográfica {#changing-the-geolocation}

1. Clique duas vezes no ícone de geolocalização. Um mapa expandido será aberto, aqui você pode arrastar o marcador para um novo local:

   ![](assets/clientcontext_geomocationrelocate.png)

1. Clique fora do mapa para fechar.

### Alterar a seleção de tag {#changing-the-tag-selection}

1. Clique duas vezes na seção Nuvem de tags do Contexto do Cliente. A caixa de diálogo será aberta, aqui você pode selecionar tags:

   ![](assets/clientcontext_tagselection.png)

1. Clique em OK para carregar no Contexto do Cliente.

## Editar o contexto do cliente {#editing-the-client-context}

A edição de um contexto de cliente pode ser usada para definir (ou redefinir) os valores de determinadas propriedades, adicionar uma nova propriedade ou remover uma que não seja mais necessária.

### Editar detalhes da propriedade {#editing-property-details}

A edição de um contexto de cliente pode ser usada para definir (ou redefinir) os valores de determinadas propriedades. Isso permite testar cenários específicos (especialmente úteis para [segmentação](/help/sites-administering/campaign-segmentation.md) e [campanhas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)).

![](assets/clientcontext_alisonparker_edit.png)

### Adicionar um componente de propriedade {#adding-a-property-component}

Após ter aberto o **Página de design do ClientContext**, você também pode **Adicionar** uma propriedade completamente nova usando os componentes disponíveis (os componentes são listados no sidekick ou do **Inserir novo componente** que é aberta depois de um clique duplo na **Arraste componentes ou ativos aqui** caixa):

![](assets/clientcontext_alisonparker_new.png)

### Remover um componente de propriedade {#removing-a-property-component}

Após ter aberto o **Página de design do ClientContext**, você também pode **Remover** uma propriedade, se não for mais necessária. Inclui propriedades fornecidas prontas para uso; **Redefinir** O reinstalará se tiverem sido removidas.

## Armazenamento de dados no contexto do cliente via JSONP {#storing-data-in-client-context-via-jsonp}

Siga este exemplo para usar o componente de armazenamento de contexto da Loja JSONP para adicionar dados externos ao Contexto do Cliente. Em seguida, crie um segmento com base nas informações desses dados. O exemplo usa o serviço JSONP fornecido por WIPmania.com. O serviço retorna informações de localização geográfica com base no endereço IP do cliente Web.

Esse exemplo usa o site de amostra do Geometrixx Outdoors para acessar o Contexto do Cliente e testar o segmento criado. Você pode usar um site diferente, desde que a página tenha ativado o Contexto do Cliente. (Consulte [Adicionar contexto do cliente a uma página](/help/sites-developing/client-context.md#adding-client-context-to-a-page).)

### Adicionar o componente da loja JSONP {#add-the-jsonp-store-component}

Adicione o componente Loja JSONP ao Contexto do Cliente e use-o para recuperar e armazenar informações de geolocalização sobre o cliente da Web.

1. Abra a página inicial em inglês do site Geometrixx Outdoors na instância do autor do AEM. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Para abrir o Contexto do Cliente, pressione Ctrl-Alt-c (windows) ou control-option-c (Mac).
1. Clique no ícone de edição na parte superior do Contexto do Cliente para abrir o Designer de Contexto do Cliente.

   ![](do-not-localize/chlimage_1.png)

1. Arraste o componente Loja JSONP para o Contexto do Cliente.

   ![](assets/chlimage_1-4.jpeg)

1. Clique duas vezes no componente para abrir a caixa de diálogo de edição.
1. Na caixa URL do serviço JSONP, digite o seguinte URL e clique em Buscar armazenamento:

   `https://api.wipmania.com/jsonp?callback=${callback}`

   O componente chama o serviço JSONP e lista todas as propriedades que os dados retornados contêm. As propriedades que estão na lista são aquelas que estarão disponíveis no Contexto do Cliente.

   ![](assets/chlimage_1-40.png)

1. Clique em OK.
1. Retorne à página inicial do Geometrixx Outdoors e atualize a página. O Contexto do Cliente agora inclui as informações do componente Loja JSONP.

   ![](assets/chlimage_1-41.png)

### Criar o segmento {#create-the-segment}

Use os dados do armazenamento de sessão que você criou usando o componente de armazenamento JSONP. O segmento usa a latitude do armazenamento de sessão e a data atual para determinar se é a hora de inverno no local do cliente.

1. Abra o console Ferramentas no navegador da Web (`https://localhost:4502/miscadmin#/etc`).
1. Na árvore de pastas, clique na pasta Ferramentas/Segmentação e em Nova > Nova pasta. Especifique os seguintes valores de propriedade e clique em Criar:

   * Nome: mysegments
   * Título: Meus segmentos

1. Selecione a pasta Meus segmentos e clique em Nova > Nova página:

   1. Para o Título, digite Inverno.
   1. Selecione o modelo Segmento .
   1. Clique em Criar.

1. Clique com o botão direito do mouse no segmento Winter e clique em Open (Abrir).
1. Arraste a propriedade Generic Store para o contêiner AND padrão.

   ![](assets/chlimage_1-5.jpeg)

1. Clique duas vezes no componente para abrir a caixa de diálogo de edição, especifique os seguintes valores de propriedade e clique em OK:

   * Conservar: wipmania
   * Nome da propriedade: latitude
   * Operador: é maior que
   * Valor da propriedade: 30º

1. Arraste o componente Script para o mesmo contêiner AND e abra a caixa de diálogo de edição. Adicione o script a seguir e clique em OK:

   `3 < new Date().getMonth() < 12`
