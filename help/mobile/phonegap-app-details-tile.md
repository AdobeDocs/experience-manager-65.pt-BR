---
title: Gerenciar mosaico do aplicativo
seo-title: Manage App Tile
description: Siga esta página para saber mais sobre Gerenciar o bloco do aplicativo no painel do aplicativo, que fornece a capacidade de modificar detalhes sobre o aplicativo.
seo-description: Follow this page to learn about the Manage App Tile on the app dashboard that provides the ability to modify details about the Application.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 1%

---

# Gerenciar mosaico do aplicativo{#manage-app-tile}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O **Gerenciar aplicativo** O mosaico no painel do aplicativo fornece a capacidade de modificar detalhes sobre o aplicativo. Para abrir a página Detalhes, clique no link Gerenciar detalhes do bloco do aplicativo. Na página Gerenciar aplicativo, é possível editar as configurações do PhoneGap Application Configuration (config.xml) e preparar seu aplicativo para envio para as várias lojas de aplicativos.

![chlimage_1-116](assets/chlimage_1-116.png)

## Noções básicas sobre o gerenciamento do mosaico do aplicativo {#understanding-the-manage-app-tile}

Você pode detalhar cada bloco no **Gerenciar aplicativo** bloco para exibir ou editar detalhes clicando em &#39;...&#39; no canto inferior direito.

### A guia Básico {#the-basic-tab}

Você pode editar o **Nome**, **Autor**, **Descrição curta** e o **Descrição** para seu aplicativo nesta guia.

![chlimage_1-117](assets/chlimage_1-117.png)

### A guia Avançado {#the-advanced-tab}

Cada plataforma de aplicativo móvel descreve quais dados são coletados, direcionando cada loja de aplicativos especificamente.

As plataformas exibidas são orientadas pelo conteúdo PhoneGap config.xml:

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Cada loja de aplicativos de fornecedor, como Apple App Store ou Google Play Store, por exemplo, requer uma ou mais capturas de tela do aplicativo móvel para exibir os detalhes do aplicativo aos clientes. Essas capturas de tela podem ter requisitos estritos em torno de dimensões e conteúdo (basicamente, elas devem realmente representar o aplicativo). AEM Apps oferece suporte para selecionar e gerenciar essas capturas de tela para as plataformas compatíveis e exibir as dimensões da porta conforme necessário para a loja de aplicativos de cada fornecedor.

>[!NOTE]
>
>O aplicativo AEM Verify fornece a capacidade de enviar capturas de tela diretamente para os detalhes do aplicativo no AEM.
>
>Consulte [Início rápido móvel para verificação de AEM](/help/mobile/phonegap-mobile-quickstart.md) para obter mais detalhes.

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadados {#metadata}

>[!NOTE]
>
>Depois de conhecer o **Gerenciar aplicativo** bloco, consulte [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md) para exibir e editar os metadados.

#### Metadados comuns {#common-metadata}

Cada Aplicativo deve ter metadados associados que auxiliam na configuração de diferentes aspectos do aplicativo. A página Gerenciar aplicativo é separada em duas áreas diferentes relacionadas à coleta de metadados. Metadados específicos da plataforma e metadados comuns.

Há configurações e metadados comuns para todas as plataformas.

Nesta seção, você define o URL do Servidor de atualização de conteúdo, a página de aterrissagem para seu aplicativo móvel, a versão PhoneGap para compilação, a versão do aplicativo, o nome, a descrição e muito mais.

**Versão do aplicativo** é a versão funcional do seu aplicativo. A prática recomendada comum é usar uma notação de 3 casas decimais e começar abaixo de 1.0.0 antes da primeira versão.

**Versão do PhoneGap** é a versão em que você deseja compilar seu aplicativo com o PhoneGap. A prática recomendada é acompanhar a versão atual para garantir que você obtenha os recursos e as correções de erros mais recentes e melhores.

**URL do Servidor de Atualização de Conteúdo** é o URL que seu aplicativo usará para chamar pelas atualizações do ContentSync. Ele deve ser definido para o URL do dispatcher ou, se não estiver usando um dispatcher, para uma de suas instâncias de publicação que será usada para fornecer atualizações do ContentSync ao seu aplicativo.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Essa seção pode parecer vazia, a menos que haja dados preenchendo os campos.
>
>Na parte superior da exibição de detalhes, você verá Versão do aplicativo, Versão do PhoneGap e URL de atualização, cada um desses valores pode ser definido na seção Metadados comuns . No entanto, a ID do aplicativo não pode ser editada.

#### Metadados da plataforma {#platform-metadata}

Todas as plataformas definidas no arquivo config.xml do PhoneGap podem conter propriedades personalizadas de plataforma. Um desenvolvedor de AEM deve contribuir com a estrutura de conteúdo para capturar essas propriedades. Um exemplo fornecido de propriedades específicas da plataforma pode ser encontrado no iOS.

Os metadados para todas as plataformas configuradas agora são exibidos ao mesmo tempo na guia Avançado do bloco Gerenciar aplicativo .

>[!NOTE]
>
>As seções de metadados da plataforma não são usadas pelo PhoneGap durante uma build CLI ou Remote PhoneGap, mas AEM tentativas de capturar metadados para plataformas, de modo que possam ser usados posteriormente ao enviar para o armazenamento de aplicativos do fornecedor de destino.

Para plataformas que não são compreendidas pela AEM, ainda é possível que um desenvolvedor AEM estenda a interface do usuário para capturar esses metadados, que posteriormente podem ser exportados e usados durante o processo de envio do aplicativo.

#### Metadados do iOS {#ios-metadata}

A Apple AppStore requer metadados adicionais para enviar seu aplicativo para distribuição. A seção de metadados do iOS tenta coletar as informações necessárias que podem ser usadas pela ferramenta Apple TMSTransporter para publicar os metadados na conta de desenvolvedor do Apple associada.

Para obter os metadados específicos do Apple, primeiro é necessário criar o aplicativo em [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Ao criar seu aplicativo, o Apple gerará metadados que são exigidos pela seção de metadados do iOS se você quiser usar a ferramenta Apple TMSTransporter para validar e fazer upload dos metadados para itunesconnect.apple.com. Caso deseje apenas obter os metadados para coletar, não é necessário preencher os metadados específicos do iOS. Você ainda pode exportar os metadados que mesclarão o iOS e os metadados comuns e coletar todas as capturas de tela em um arquivo zip que pode ser baixado a qualquer momento.

O arquivo zip baixado contém um arquivo itmsp que pode ser inspecionado para localizar o metadata.xml. O arquivo itmsp contém os metadados exportados (dentro do arquivo metadata.xml), juntamente com todas as capturas de tela associadas.

A funcionalidade de exportação é usada para fornecer uma maneira conveniente de coletar capturas de tela e metadados que podem ser passados para o editor do aplicativo para entrada na loja de aplicativos específica do fornecedor.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Metadados do Android {#android-metadata}

Ao selecionar a plataforma Android, não há metadados personalizados neste ponto que possam ser definidos. Ao clicar no botão de download como arquivo zip será gerado com um arquivo de propriedades que contenha todos os metadados e capturas de tela associadas.

A funcionalidade de exportação é usada para fornecer uma maneira conveniente de coletar capturas de tela e metadados que podem ser passados para o editor do aplicativo para entrada na loja de aplicativos específica do fornecedor.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL do servidor para atualização de conteúdo {#content-update-server-url}

Um dos principais recursos AEM aplicativos é a capacidade de ter um aplicativo móvel para solicitar novo conteúdo por meio do ContentSync, onde o conteúdo pode ser recursos html, páginas, vídeo, imagens, texto e muito mais. Depois que um autor de conteúdo tiver atualizado o conteúdo e, em seguida, publicar esse conteúdo, o servidor disponibilizará a atualização de conteúdo para o aplicativo móvel baixar.

A propriedade Content Update Server URL é o URL que deve apontar para uma instância de publicação; diretamente ou através do dispatcher ou CDN. O formato do URL é simplesmente:

`https://[hostname]:[port]`

>[!NOTE]
>
>Se a instância do servidor Autor estiver sendo replicada para várias instâncias do servidor de publicação (arquitetura comum para AEM), cada servidor de publicação terá o mesmo conteúdo de atualização, pois a atualização é criada no autor e replicada para todas as instâncias de publicação. Basicamente, o balanceamento de carga e o failover são totalmente compatíveis.

### A guia Plug-ins {#the-plugins-tab}

O **Plug-ins** descreve os plug-ins associados ao seu aplicativo. Essas informações serão usadas para recuperar o plug-in apropriado durante uma criação.

![chlimage_1-122](assets/chlimage_1-122.png)

### A guia Capturas de tela {#the-screenshots-tab}

O **Capturas de tela** exibe as resoluções de captura de tela suportadas em plataformas diferentes.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Para adicionar e remover capturas de tela, consulte [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md).

### A guia Autenticação {#the-authentication-tab}

O **Autenticação** A guia permite selecionar um cliente OAuth para ser associado ao seu aplicativo e permite que um desenvolvedor utilize a autenticação OAuth da Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Próximas etapas {#the-next-steps}

Depois de saber mais sobre Gerenciamento de blocos de aplicativos no painel de aplicativos, consulte os seguintes recursos para outras funções de criação:

* [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md)
* [Definições do aplicativo](/help/mobile/phonegap-app-definitions.md)
* [Criação de um novo aplicativo usando o Assistente para criação de aplicativo](/help/mobile/phonegap-create-new-app.md)
* [Importar um aplicativo híbrido existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento para Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
