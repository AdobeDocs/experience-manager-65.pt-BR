---
title: '[!DNL Assets] Experiência da página inicial'
description: Personalize a [!DNL Experience Manager Assets] Página inicial para obter uma experiência avançada de tela de boas-vindas, incluindo um instantâneo das atividades recentes em torno dos ativos.
contentOwner: AG
feature: Ferramentas de desenvolvedor, Gerenciamento de ativos
role: Administrador, profissional
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Experiência da página inicial  {#aem-assets-home-page-experience}

Personalize a página inicial [!DNL Adobe Experience Manager Assets] para obter uma experiência de tela de boas-vindas rica, incluindo um instantâneo das atividades recentes em torno dos ativos.

[!DNL Assets] a página inicial fornece uma experiência de tela de boas-vindas rica e personalizada, que inclui um instantâneo de atividades recentes, como ativos que foram visualizados ou carregados recentemente.

A página inicial [!DNL Assets] é desativada por padrão. Para habilitá-lo, execute as seguintes etapas:

1. Abra [!DNL Experience Manager] Gerenciador de Configuração `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço **[!UICONTROL Day CQ DAM Event Recorder]**.
1. Selecione **[!UICONTROL Ativar este serviço]** para ativar a gravação de atividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Na lista **[!UICONTROL Tipos de evento]**, selecione os eventos a serem registrados e salve as alterações.

   >[!CAUTION]
   >
   >Ativar as opções de ativo visualizado, Projetos visualizados e Coleções visualizadas aumenta significativamente o número de eventos gravados.

1. Abra o serviço **[!UICONTROL Sinalizador de recurso da página inicial do ativo DAM]** no Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selecione a opção `isEnabled.name` para ativar o recurso [!DNL Assets] Página inicial. Salve as alterações.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra a caixa de diálogo **[!UICONTROL Preferências do usuário]** e selecione **[!UICONTROL Ativar a Página inicial dos ativos]**. Salve as alterações.

   ![Ativar a página inicial de ativos na caixa de diálogo Preferências do usuário](assets/Annotation-color.png)

Depois de habilitar a página inicial [!DNL Assets], navegue até a interface do usuário [!DNL Assets] na página Navegação ou acesse-a diretamente do URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar o link de experiência na interface do usuário do Assets](assets/config-experience-link.png)

Clique no **[!UICONTROL Clique aqui para configurar seu link de experiência]** para adicionar seu nome de usuário, imagem de plano de fundo e imagem de perfil.

A página inicial [!DNL Assets] inclui as seguintes seções:

* Seção de boas-vindas
* Seção de widget

**Seção de boas-vindas**

Se o seu perfil existir, a seção Welcome exibirá uma mensagem de boas-vindas endereçada a você. Além disso, ele exibe a imagem do perfil e uma imagem de boas-vindas (se configurada já).

Se o seu perfil estiver incompleto, a seção Welcome exibirá uma mensagem de boas-vindas genérica e um espaço reservado para a imagem do seu perfil.

**Seção de widget**

Esta seção aparece abaixo da seção de Boas-vindas e exibe os widgets prontos para uso nas seguintes seções:

* Atividade
* Recentes
* Descobrir

**Atividade**: Nesta seção, o  **[!UICONTROL widget Minha]** atividade exibe as atividades recentes executadas pelo usuário conectado com ativos (incluindo ativos sem representações), por exemplo, uploads de ativos, downloads, criação de ativos, edições, comentários, anotações e compartilhamentos.

**Recente**: O widget  **[!UICONTROL Recentemente]** exibido nesta seção exibe entidades acessadas recentemente pelo usuário conectado, incluindo pastas, coleções e projetos.

**Discover**: O  **** Newwidget nesta seção exibe os ativos e as representações carregados recentemente na  [!DNL Assets] implantação.

Para habilitar a limpeza dos dados de atividade do usuário, habilite o **[!UICONTROL DAM Event Purge Service]** no Configuration Manager. Após habilitar esse serviço, as atividades do usuário conectado que excedem um número especificado são excluídas pelo sistema.

A tela de Boas-vindas fornece recursos de navegação fáceis, por exemplo, ícones na barra de ferramentas para acessar pastas, coleções e catálogos.

>[!NOTE]
>
>Habilitar os serviços [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL DAM Event Purge] aumenta as operações de gravação no JCR e a indexação de pesquisa, o que aumenta significativamente a carga no servidor [!DNL Experience Manager]. A carga adicional no servidor [!DNL Experience Manager] pode afetar seu desempenho.

>[!CAUTION]
>
>Capturar, filtrar e limpar atividades do usuário necessárias para a [!DNL Assets] página inicial impõem uma sobrecarga no desempenho. Portanto, os administradores devem configurar a Página inicial de maneira eficaz para os usuários do público-alvo.
>
>O Adobe recomenda que os administradores e usuários que realizam operações em massa evitem usar o recurso Página inicial do ativo para evitar o aumento das atividades do usuário. Além disso, os administradores podem excluir as atividades de gravação de usuários específicos configurando [!UICONTROL Day CQ DAM Event Recorder] do [!UICONTROL Configuration Manager].
>
>Se você usar o recurso , o Adobe recomenda agendar a frequência de limpeza com base na carga do servidor.
