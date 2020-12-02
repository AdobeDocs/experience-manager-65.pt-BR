---
title: '[!DNL Assets] experiência do home page'
description: Personalize o Home page [!DNL Experience Manager Assets] para obter uma experiência avançada em tela de boas-vindas, incluindo um instantâneo de atividades recentes sobre ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Experiência do home page  {#aem-assets-home-page-experience}

Personalize o home page [!DNL Adobe Experience Manager Assets] para obter uma excelente experiência de tela de boas-vindas, incluindo um instantâneo de atividades recentes sobre ativos.

[!DNL Assets] O home page fornece uma experiência de tela de boas-vindas rica e personalizada, que inclui um instantâneo de atividades recentes, como ativos que foram visualizados ou carregados recentemente.

O home page [!DNL Assets] está desativado por padrão. Para ativá-lo, execute as seguintes etapas:

1. Abra [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço **[!UICONTROL Day CQ DAM Evento Recorder]**.
1. Selecione **[!UICONTROL Ativar este serviço]** para ativar a gravação de atividade.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Na lista **[!UICONTROL Tipos de evento]**, selecione os eventos a serem gravados e salve as alterações.

   >[!CAUTION]
   >
   >Ativar as opções visualizadas Ativo visualizado, Projetos visualizados e Coleções aumenta significativamente o número de eventos registrados.

1. Abra o serviço **[!UICONTROL Sinalizador do recurso Home page do ativo DAM]** do Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selecione a opção `isEnabled.name` para ativar o recurso de Home page [!DNL Assets]. Salve as alterações.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra a caixa de diálogo **[!UICONTROL Preferências de usuário]** e selecione **[!UICONTROL Ativar Home page de ativos]**. Salve as alterações.

   ![Habilitar home page de ativos na caixa de diálogo Preferências de usuário](assets/Annotation-color.png)

Depois de ativar o Home page [!DNL Assets], navegue até a interface do usuário [!DNL Assets] na página Navegação ou acesse-a diretamente do URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar o link de experiência na interface do usuário do Assets](assets/config-experience-link.png)

Clique em **[!UICONTROL Clique aqui para configurar seu link de experiência]** para adicionar seu nome de usuário, imagem de plano de fundo e imagem de perfil.

O Home page [!DNL Assets] inclui as seguintes seções:

* Seção de boas-vindas
* Seção do Widget

**Seção de boas-vindas**

Se o seu perfil existir, a seção Boas-vindas exibirá uma mensagem de boas-vindas endereçada a você. Além disso, exibe a imagem do perfil e uma imagem de boas-vindas (se já estiver configurada).

Se o perfil estiver incompleto, a seção Bem-vindo exibirá uma mensagem genérica de boas-vindas e um espaço reservado para a imagem do perfil.

**Seção do Widget**

Esta seção é exibida abaixo da seção Boas-vindas e exibe os widgets predefinidos nas seguintes seções:

* Atividade
* Recentes
* Descobrir

**Atividade**: Nesta seção, o  **[!UICONTROL My]** Ativitywidget exibe atividades recentes executadas pelo usuário conectado com ativos (incluindo ativos sem representações), como uploads de ativos, downloads, criação de ativos, edições, comentários, anotações e compartilhamentos.

**Recente**: O widget  **[!UICONTROL Visualizado]** recentemente nesta seção exibe entidades acessadas recentemente pelo usuário conectado, incluindo pastas, coleções e projetos.

**Discover**: O  **** Newwidget desta seção exibe os ativos e as execuções carregados recentemente na  [!DNL Assets] implantação.

Para habilitar a remoção de dados de atividade do usuário, ative o **[!UICONTROL serviço de remoção de Evento DAM]** do Configuration Manager. Após habilitar esse serviço, as atividades do usuário conectado que excederem um número especificado serão excluídas pelo sistema.

A tela de boas-vindas fornece ferramentas de navegação fáceis, por exemplo ícones na barra de ferramentas para acessar pastas, coleções e catálogos.

>[!NOTE]
>
>Habilitar os serviços [!UICONTROL Day CQ DAM Evento Recorder] e [!UICONTROL DAM Evento Purge] aumenta as operações de gravação no JCR e a indexação de pesquisa, o que aumenta significativamente a carga no servidor [!DNL Experience Manager]. A carga adicional no servidor [!DNL Experience Manager] pode afetar seu desempenho.

>[!CAUTION]
>
>A captura, filtragem e remoção de atividades de usuário necessárias para o home page [!DNL Assets] impõem uma sobrecarga no desempenho. Portanto, os administradores devem configurar o Home page de forma eficiente para os usuários do público alvo.
>
>O Adobe recomenda que os administradores e usuários que executam operações em massa evitem usar o recurso Home page de ativos para evitar o aumento das atividades do usuário. Além disso, os administradores podem excluir atividades de gravação para usuários específicos configurando [!UICONTROL Gravador de Eventos Day CQ DAM] do [!UICONTROL Configuration Manager].
>
>Se você usar o recurso, o Adobe recomenda agendar a frequência de expurgação com base na carga do servidor.
