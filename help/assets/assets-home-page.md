---
title: Experiência da página inicial [!DNL Assets]
description: Personalize a [!DNL Experience Manager Assets] Página inicial para obter uma experiência avançada de tela de boas-vindas, incluindo um instantâneo das atividades recentes relacionadas aos ativos.
contentOwner: AG
feature: Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---

# Experiência da página inicial [!DNL Adobe Experience Manager Assets] {#aem-assets-home-page-experience}

Personalize a página inicial do [!DNL Adobe Experience Manager Assets] para obter uma experiência avançada em tela de boas-vindas, incluindo um instantâneo das atividades recentes relacionadas aos ativos.

A página inicial do [!DNL Assets] fornece uma experiência em tela de boas-vindas avançada e personalizada, que inclui um instantâneo de atividades recentes, como ativos que foram visualizados ou carregados recentemente.

A home page [!DNL Assets] está desabilitada por padrão. Para ativá-lo, execute as seguintes etapas:

1. Abra o [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço **[!UICONTROL Day CQ DAM Event Recorder]**.
1. Selecione **[!UICONTROL Habilitar este serviço]** para habilitar a gravação de atividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Na lista **[!UICONTROL Tipos de Evento]**, selecione os eventos a serem gravados e salve as alterações.

   >[!CAUTION]
   >
   >Ativar as opções Ativo exibido, Projetos exibidos e Coleções visualizadas aumenta significativamente o número de eventos registrados.

1. Abra o serviço **[!UICONTROL Sinalizador do Recurso da Página Inicial do Ativo DAM]** no Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selecione a opção `isEnabled.name` para habilitar o recurso de Página Inicial [!DNL Assets]. Salve as alterações.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra a caixa de diálogo **[!UICONTROL Preferências do Usuário]** e selecione **[!UICONTROL Habilitar Página Inicial do Assets]**. Salve as alterações.

   ![Habilitar a página inicial dos ativos na caixa de diálogo Preferências do Usuário](assets/Annotation-color.png)

Depois de habilitar a Página Inicial [!DNL Assets], navegue até a interface de usuário [!DNL Assets] na página Navegação ou acesse-a diretamente da URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar link de experiência na interface do usuário do Assets](assets/config-experience-link.png)

Clique no **[!UICONTROL Clique aqui para configurar o link da sua experiência]** para adicionar seu nome de usuário, imagem de plano de fundo e imagem de perfil.

A Home page [!DNL Assets] inclui as seguintes seções:

* Seção de boas-vindas
* Seção do widget

**Seção de Boas-vindas**

Se seu perfil existir, a seção Bem-vindo exibirá uma mensagem de boas-vindas endereçada a você. Além disso, exibe a imagem do seu perfil e uma imagem de boas-vindas (se já estiver configurada).

Se o seu perfil estiver incompleto, a seção Bem-vindo exibirá uma mensagem de boas-vindas genérica e um espaço reservado para sua imagem de perfil.

**Seção do widget**

Esta seção aparece abaixo da seção Bem-vindo e exibe widgets prontos para uso nas seguintes seções:

* Atividade
* Recentes
* Descobrir

**Atividade**: nesta seção, o widget **[!UICONTROL Minha Atividade]** exibe atividades recentes executadas pelo usuário conectado com ativos (incluindo ativos sem representações), por exemplo, uploads de ativos, downloads, criação de ativos, edições, comentários, anotações e compartilhamentos.

**Recente**: o widget **[!UICONTROL Recentemente visualizado]** nesta seção exibe entidades acessadas recentemente pelo usuário conectado, incluindo pastas, coleções e projetos.

**Descoberta**: o widget **[!UICONTROL Novo]** desta seção exibe os ativos e as representações carregados recentemente na implantação do [!DNL Assets].

Para habilitar a limpeza de dados de atividade do usuário, habilite o **[!UICONTROL Serviço de Limpeza de Eventos do DAM]** no Configuration Manager. Após habilitar este serviço, as atividades do usuário conectado que excedem um número especificado são excluídas pelo sistema.

A tela de boas-vindas fornece ajudas de navegação fáceis, por exemplo, ícones na barra de ferramentas para acessar pastas, coleções e catálogos.

>[!NOTE]
>
>Habilitar os serviços [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL DAM Event Purge] aumenta as operações de gravação no JCR e a indexação de pesquisa, o que aumenta significativamente a carga no servidor [!DNL Experience Manager]. A carga adicional no servidor [!DNL Experience Manager] pode afetar seu desempenho.

>[!CAUTION]
>
>A captura, a filtragem e a limpeza das atividades de usuário necessárias para a página inicial [!DNL Assets] impõem uma sobrecarga no desempenho. Portanto, os administradores devem configurar a Página inicial de forma eficaz para usuários-alvo.
>
>A Adobe recomenda que os administradores e usuários que executam operações em massa evitem usar o recurso Página inicial do ativo para evitar o aumento das atividades do usuário. Além disso, os administradores podem excluir atividades de gravação para usuários específicos configurando o [!UICONTROL Day CQ DAM Event Recorder] no [!UICONTROL Configuration Manager].
>
>Se você usar o recurso, o Adobe recomenda que você programe a frequência de limpeza com base na carga do servidor.
