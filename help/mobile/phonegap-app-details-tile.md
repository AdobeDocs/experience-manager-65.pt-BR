---
title: Gerenciar mosaico do aplicativo
description: Saiba mais sobre o bloco "Gerenciar aplicativo" no painel do aplicativo que fornece o permite editar detalhes sobre o aplicativo.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: bf99ad3710638ec823d3b17967e1c750d0405c77
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 1%

---

# Gerenciar mosaico do aplicativo{#manage-app-tile}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

A variável **`Manage App`** O bloco no Painel do aplicativo permite editar detalhes sobre o aplicativo. Para abrir a página Detalhes, clique no link **`Manage App`** link de detalhes do bloco. De dentro do **`Manage App`** você pode editar as configurações de configuração do aplicativo PhoneGap (config.xml) e preparar seu aplicativo para envio a várias lojas de aplicativos.

![chlimage_1-116](assets/chlimage_1-116.png)

## Compreender o `Manage App` bloco {#understanding-the-manage-app-tile}

Você pode detalhar cada bloco na **`Manage App`** mosaico para exibir ou editar detalhes clicando em &quot;...&quot; no canto inferior direito.

### A guia Básico {#the-basic-tab}

É possível editar a variável **Nome**, **Autor**, **Descrição curta**, e o **Descrição** para seu aplicativo nesta guia.

![chlimage_1-117](assets/chlimage_1-117.png)

### A guia Avançado {#the-advanced-tab}

Cada plataforma de aplicativo móvel descreve quais dados são coletados, direcionando especificamente cada loja de aplicativos.

As plataformas exibidas são orientadas pelo conteúdo config.xml do PhoneGap:

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Cada loja de aplicativos de fornecedor — por exemplo, Apple App Store ou Google Play Store — requer uma ou mais capturas de tela do aplicativo móvel para exibir os detalhes do aplicativo aos clientes. Essas capturas de tela podem ter requisitos rigorosos em relação a dimensões e conteúdo (basicamente, elas devem realmente representar o aplicativo). O aplicativo AEM é compatível com a seleção e o gerenciamento dessas capturas de tela para as plataformas compatíveis e a visualização de dimensões de porta conforme exigido pelo armazenamento de aplicativos de cada fornecedor.

>[!NOTE]
>
>O aplicativo AEM Verify permite enviar capturas de tela diretamente para os detalhes do aplicativo no AEM.
>
>Consulte [Verificação de Quickstart para AEM em dispositivo móvel](/help/mobile/phonegap-mobile-quickstart.md) para obter mais detalhes.

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadados {#metadata}

>[!NOTE]
>
>Depois de conhecer o **`Manage App`** bloco, consulte [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md) para exibir e editar os metadados.

#### Metadados comuns {#common-metadata}

Cada aplicativo deve ter metadados associados que ajudam a configurar diferentes aspectos do aplicativo. A página Gerenciar aplicativo é separada em duas áreas diferentes relacionadas à coleção de metadados. Metadados específicos da plataforma e metadados comuns.

Há configurações e metadados comuns para todas as plataformas.

Nesta seção, você define o URL do Content Update Server, a página de aterrissagem do aplicativo móvel, a versão do PhoneGap para compilação, a versão do aplicativo, o nome, a descrição e muito mais.

**Versão do aplicativo** é a versão em funcionamento do aplicativo. Uma prática recomendada é usar uma notação 3 decimal e começar abaixo de 1.0.0 antes da primeira versão.

**Versão do PhoneGap** é a versão na qual você deseja compilar seu aplicativo com PhoneGap. A prática recomendada é acompanhar a versão atual para garantir que você obtenha os melhores e mais recentes recursos e correções de erros.

**URL do servidor de atualização de conteúdo** é o URL que seu aplicativo usa para chamar para atualizações do ContentSync. Ele deve ser definido como o URL do Dispatcher ou, se não estiver usando um Dispatcher, como uma das instâncias de publicação usadas para fornecer atualizações do ContentSync ao aplicativo.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Esta seção pode parecer vazia, a menos que haja dados preenchendo os campos.
>
>Na parte superior da visualização de detalhes, em Application Version, PhoneGap Version e Update URL, cada um desses valores pode ser definido na seção Common Metadata. No entanto, a ID do aplicativo não pode ser editada.

#### Metadados da plataforma {#platform-metadata}

Todas as plataformas definidas no config.xml do PhoneGap podem conter propriedades de plataforma personalizadas. Um desenvolvedor de AEM deve contribuir com a estrutura de conteúdo para capturar essas propriedades. Um exemplo fornecido de propriedades específicas da plataforma pode ser encontrado para o iOS.

Os metadados de todas as plataformas configuradas agora são exibidos ao mesmo tempo na guia Avançado do `Manage App` bloco.

>[!NOTE]
>
>As seções de metadados da plataforma não são usadas pelo PhoneGap durante uma CLI ou criação de um PhoneGap remoto. Em vez disso, o AEM tenta capturar metadados para plataformas de modo que eles possam ser usados posteriormente ao enviar para a loja de aplicativos do fornecedor direcionado.

Para plataformas não compreendidas pelo AEM, ainda é possível que um desenvolvedor AEM estenda a interface do usuário para capturar esses metadados, que posteriormente podem ser exportados e usados durante o processo de envio do aplicativo.

#### Metadados do iOS {#ios-metadata}

A AppStore da Apple requer metadados adicionais para enviar seu aplicativo para distribuição. A seção de metadados do iOS tenta coletar as informações necessárias que podem ser usadas pela ferramenta iTMSTransporter da Apple para publicar os metadados na conta do desenvolvedor do Apple associado.

Para obter os metadados específicos do Apple, crie seu aplicativo em [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Ao criar seu aplicativo, o Apple gera metadados que são exigidos pela seção de metadados do iOS se você quiser usar a ferramenta Apple TMSTransporter para validar e fazer upload dos metadados para itunesconnect.apple.com. Se quiser obter os metadados a coletar, não é necessário preencher os metadados específicos do iOS. Você ainda pode exportar os metadados que mesclam o iOS e os metadados comuns e coletar todas as capturas de tela em um arquivo zip que pode ser baixado a qualquer momento.

O arquivo zip baixado contém um arquivo itmsp que pode ser inspecionado quanto ao arquivo metadata.xml. O arquivo itmsp contém os metadados exportados (dentro do arquivo metadata.xml ), juntamente com todas as capturas de tela associadas.

A funcionalidade de exportação é usada para fornecer uma maneira conveniente de coletar as capturas de tela e os metadados que podem ser transmitidos ao editor do aplicativo para entrada na loja de aplicativos específica do fornecedor.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Metadados do Android™ {#android-metadata}

Ao selecionar a plataforma Android™, não há metadados personalizados no momento que possam ser definidos. Ao clicar no botão de download, um arquivo zip é gerado com um arquivo de propriedades que contém todos os metadados e capturas de tela associadas.

A funcionalidade de exportação é usada para fornecer uma maneira conveniente de coletar as capturas de tela e os metadados que podem ser transmitidos ao editor do aplicativo para entrada na loja de aplicativos específica do fornecedor.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL do servidor para atualização de conteúdo {#content-update-server-url}

Um dos principais recursos dos aplicativos AEM é a capacidade de ter um aplicativo móvel solicitando novo conteúdo por meio do ContentSync, em que o conteúdo pode ser recursos html, páginas, vídeo, imagens, texto e muito mais. Depois que um autor de conteúdo atualiza o conteúdo e, em seguida, publica esse conteúdo, o servidor disponibiliza a atualização de conteúdo para o aplicativo móvel baixar.

A propriedade URL do Servidor de atualização de conteúdo é o URL que deve apontar para uma instância de publicação, diretamente ou por meio do Dispatcher ou do CDN. O formato do URL é simplesmente:

`https://[hostname]:[port]`

>[!NOTE]
>
>Se a instância do servidor do autor estiver replicando para muitas instâncias do servidor de publicação (arquitetura comum para AEM), cada servidor de publicação terá o mesmo conteúdo de atualização. O motivo é que a atualização é criada no autor e replicada em todas as instâncias de publicação. Basicamente, o balanceamento de carga e o failover são totalmente compatíveis.

### A aba Plug- ins {#the-plugins-tab}

A variável **Plug-ins** A guia descreve os plug-ins associados ao seu aplicativo. Essas informações são usadas para recuperar o plug-in apropriado durante uma criação.

![chlimage_1-122](assets/chlimage_1-122.png)

### A página de Capturas de Tela {#the-screenshots-tab}

A variável **Capturas de tela** A guia exibe as resoluções de captura de tela compatíveis em diferentes plataformas.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Para adicionar e remover capturas de tela, consulte [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md).

### A guia Autenticação {#the-authentication-tab}

A variável **Autenticação** permite que você selecione um cliente OAuth para associar ao aplicativo e permite que um desenvolvedor use a autenticação OAuth do Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Próximas etapas {#the-next-steps}

Depois de saber mais sobre como Gerenciar o bloco do aplicativo no painel do aplicativo, consulte os seguintes recursos para outras funções de criação:

* [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md)
* [Definições do aplicativo](/help/mobile/phonegap-app-definitions.md)
* [Criação de um novo aplicativo usando o Assistente para criação de aplicativo](/help/mobile/phonegap-create-new-app.md)
* [Importar um aplicativo híbrido existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Outros recursos {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento do Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
