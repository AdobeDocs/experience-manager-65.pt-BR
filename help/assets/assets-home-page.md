---
title: "[!DNL Assets] Experiência de página inicial"
description: Personalize o [!DNL Experience Manager Assets] Home page para obter uma experiência avançada em tela de boas-vindas, incluindo um instantâneo de atividades recentes sobre ativos.
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] Experiência da página inicial {#aem-assets-home-page-experience}

Personalize o [!DNL Adobe Experience Manager Assets] home page para obter uma rica experiência de tela de boas-vindas, incluindo um instantâneo de atividades recentes sobre ativos.

[!DNL Assets] A página inicial do fornece uma experiência avançada e personalizada de tela de boas-vindas, que inclui um instantâneo de atividades recentes, como ativos que foram visualizados ou carregados recentemente.

A variável [!DNL Assets] a página inicial está desativada por padrão. Para ativá-lo, execute as seguintes etapas:

1. Abertura [!DNL Experience Manager] Gerenciador de configurações `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o **[!UICONTROL Gravador de eventos DAM CQ do dia]** serviço.
1. Selecione o **[!UICONTROL Habilitar este serviço]** para ativar a gravação da atividade.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. No **[!UICONTROL Tipos de evento]** selecione os eventos a serem gravados e salve as alterações.

   >[!CAUTION]
   >
   >Ativar as opções Ativo exibido, Projetos exibidos e Coleções visualizadas aumenta significativamente o número de eventos registrados.

1. Abra o **[!UICONTROL Sinalizador do recurso Página inicial do ativo DAM]** serviço do Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selecione o `isEnabled.name` opção para ativar o [!DNL Assets] Recurso da página inicial. Salve as alterações.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra o **[!UICONTROL Preferências do usuário]** e selecione **[!UICONTROL Ativar a página inicial dos ativos]**. Salve as alterações.

   ![Habilitar a página inicial de ativos na caixa de diálogo Preferências do usuário](assets/Annotation-color.png)

Depois de ativar o [!DNL Assets] Home page, navegue até o [!DNL Assets] interface do usuário na página Navegação ou acesse-a diretamente do URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar link de experiência na interface do Assets](assets/config-experience-link.png)

Clique em **[!UICONTROL Clique aqui para configurar seu link de experiência]** para adicionar seu nome de usuário, imagem de fundo e imagem de perfil.

A variável [!DNL Assets] A página inicial inclui as seguintes seções:

* Seção de boas-vindas
* Seção do widget

**Seção de boas-vindas**

Se seu perfil existir, a seção Bem-vindo exibirá uma mensagem de boas-vindas endereçada a você. Além disso, exibe a imagem do seu perfil e uma imagem de boas-vindas (se já estiver configurada).

Se o seu perfil estiver incompleto, a seção Bem-vindo exibirá uma mensagem de boas-vindas genérica e um espaço reservado para sua imagem de perfil.

**Seção do widget**

Esta seção aparece abaixo da seção Bem-vindo e exibe widgets prontos para uso nas seguintes seções:

* Atividade
* Recentes
* Descobrir

**Atividade**: nesta seção, o **[!UICONTROL Minha atividade]** O widget exibe atividades recentes executadas pelo usuário conectado com os ativos (incluindo ativos sem representações), por exemplo, uploads de ativos, downloads, criação de ativos, edições, comentários, anotações e compartilhamentos.

**Recente**: A variável **[!UICONTROL Visualizado recentemente]** O widget nesta seção exibe entidades acessadas recentemente pelo usuário conectado, incluindo pastas, coleções e projetos.

**Descobrir**: A variável **[!UICONTROL Novo]** nessa seção exibe os ativos e as representações carregados recentemente na página [!DNL Assets] implantação.

Para ativar a limpeza de dados de atividade do usuário, ative a opção **[!UICONTROL Serviço de limpeza de eventos do DAM]** do Gerenciador de configurações. Após habilitar este serviço, as atividades do usuário conectado que excedem um número especificado são excluídas pelo sistema.

A tela de boas-vindas fornece ajudas de navegação fáceis, por exemplo, ícones na barra de ferramentas para acessar pastas, coleções e catálogos.

>[!NOTE]
>
>Habilitando o [!UICONTROL Gravador de eventos DAM CQ do dia] e [!UICONTROL Limpeza de evento DAM] aumenta as operações de gravação no JCR e a indexação de pesquisa, o que aumenta significativamente a carga no [!DNL Experience Manager] servidor. A carga adicional no [!DNL Experience Manager] pode afetar seu desempenho.

>[!CAUTION]
>
>Captura, filtragem e limpeza das atividades de usuário necessárias para o [!DNL Assets] página inicial impõem uma sobrecarga no desempenho. Portanto, os administradores devem configurar a Página inicial de forma eficaz para usuários-alvo.
>
>A Adobe recomenda que os administradores e usuários que executam operações em massa evitem usar o recurso Página inicial do ativo para evitar o aumento das atividades do usuário. Além disso, os administradores podem excluir atividades de gravação para usuários específicos configurando [!UICONTROL Gravador de eventos DAM CQ do dia] de [!UICONTROL Gerenciador de configurações].
>
>Se você usar o recurso, o Adobe recomenda que você programe a frequência de limpeza com base na carga do servidor.
