---
title: Experiência de Home page do [!DNL Assets]
description: Personalize [!DNL Experience Manager Assets] a página inicial para obter uma experiência avançada em tela de boas-vindas, incluindo um instantâneo de atividades recentes sobre ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Experiência do home page {#aem-assets-home-page-experience}

Personalize o [!DNL Adobe Experience Manager Assets] home page para obter uma excelente experiência de tela de boas-vindas, incluindo um instantâneo de atividades recentes sobre ativos.

[!DNL Assets] O home page fornece uma experiência de tela de boas-vindas rica e personalizada, que inclui um instantâneo de atividades recentes, como ativos que foram visualizados ou carregados recentemente.

O [!DNL Assets] home page é desativado por padrão. Para ativá-lo, execute as seguintes etapas:

1. Abra o [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço Gravador **[!UICONTROL do Evento CQ DAM]** Day.
1. Selecione **[!UICONTROL Ativar este serviço]** para ativar a gravação de atividade.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Na lista **[!UICONTROL Tipos de evento]** , selecione os eventos a serem gravados e salve as alterações.

   >[!CAUTION]
   >
   >Ativar as opções visualizadas Ativo visualizado, Projetos visualizados e Coleções aumenta significativamente o número de eventos registrados.

1. Abra o serviço Sinalizador **[!UICONTROL do recurso Home page do ativo]** DAM no Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selecione a `isEnabled.name` opção para ativar o recurso [!DNL Assets] Home page. Salve as alterações.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra a caixa de diálogo Preferências **[!UICONTROL de]** usuário e selecione **[!UICONTROL Ativar Home page]** de ativos. Salve as alterações.

   ![Habilitar home page de ativos na caixa de diálogo Preferências de usuário](assets/Annotation-color.png)

Depois de ativar o [!DNL Assets] Home page, navegue até a interface do [!DNL Assets] usuário na página Navegação ou acesse-o diretamente do URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar o link de experiência na interface do usuário do Assets](assets/config-experience-link.png)

Clique aqui para **[!UICONTROL configurar o link]** de experiência para adicionar o nome de usuário, a imagem de plano de fundo e a imagem do perfil.

O [!DNL Assets] Home page inclui as seguintes seções:

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

**Atividade**: Nesta seção, o widget **[!UICONTROL Minha Atividade]** exibe atividades recentes executadas pelo usuário conectado com ativos (incluindo ativos sem representações), como uploads de ativos, downloads, criação de ativos, edições, comentários, anotações e compartilhamentos.

**Recente**: O widget **[!UICONTROL Visualizado]** recentemente nesta seção exibe entidades acessadas recentemente pelo usuário conectado, incluindo pastas, coleções e projetos.

**Discover**: O widget **[!UICONTROL Novo]** nesta seção exibe os ativos e as execuções carregados recentemente para a [!DNL Assets] implantação.

Para ativar a remoção de dados de atividade do usuário, ative o Serviço **[!UICONTROL de Expurgação de Eventos]** DAM do Configuration Manager. Após habilitar esse serviço, as atividades do usuário conectado que excederem um número especificado serão excluídas pelo sistema.

A tela de boas-vindas fornece ferramentas de navegação fáceis, por exemplo ícones na barra de ferramentas para acessar pastas, coleções e catálogos.

>[!NOTE]
>
>Habilitar os serviços Recorder [!UICONTROL do Evento CQ DAM] Day e Expurgação [!UICONTROL do Evento] DAM aumenta as operações de gravação no JCR e a indexação de pesquisa, o que aumenta significativamente a carga no [!DNL Experience Manager] servidor. A carga adicional no [!DNL Experience Manager] servidor pode afetar seu desempenho.

>[!CAUTION]
>
>Capturar, filtrar e expurgar atividades de usuário necessárias para o [!DNL Assets] home page impõem uma sobrecarga no desempenho. Portanto, os administradores devem configurar o Home page de forma eficiente para os usuários do público alvo.
>
>O Adobe recomenda que os administradores e usuários que executam operações em massa evitem usar o recurso Home page de ativos para evitar o aumento das atividades do usuário. Além disso, os administradores podem excluir atividades de gravação para usuários específicos ao configurar o Gravador [!UICONTROL de Eventos] Day CQ DAM do [!UICONTROL Configuration Manager].
>
>Se você usar o recurso, o Adobe recomenda agendar a frequência de expurgação com base na carga do servidor.
