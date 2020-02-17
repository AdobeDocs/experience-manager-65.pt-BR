---
title: Experiência da página inicial do AEM Assets
description: Personalize a página inicial dos ativos AEM para obter uma experiência avançada em tela de boas-vindas, incluindo um instantâneo das atividades recentes em torno dos ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Experiência da página inicial do AEM Assets {#aem-assets-home-page-experience}

Personalize a página inicial dos ativos Adobe Experience Manager (AEM) para obter uma excelente experiência de boas-vindas na tela, incluindo um instantâneo das atividades recentes em torno dos ativos.

A página inicial dos ativos AEM fornece uma experiência de tela de boas-vindas avançada e personalizada, que inclui um instantâneo de atividades recentes, como ativos que foram exibidos ou carregados recentemente.

A página inicial Ativos está desativada por padrão. Para ativá-lo, execute as seguintes etapas:

1. Abra o AEM Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço Gravador **[!UICONTROL de Eventos CQ DAM do]** Dia.
1. Selecione **[!UICONTROL Ativar este serviço]** para ativar a gravação de atividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Na lista Tipos **[!UICONTROL de]** evento, selecione os eventos a serem gravados e salve as alterações.

   >[!CAUTION]
   >
   >Ativar as opções visualizadas Ativo, Projetos visualizados e Coleções aumenta significativamente o número de eventos gravados.

1. Abra o serviço Sinalizador **[!UICONTROL do recurso da página inicial do ativo]** DAM no Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selecione a `isEnabled.name` opção para ativar o recurso Página inicial de ativos. Salve as alterações.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra a caixa de diálogo Preferências **[!UICONTROL de]** usuário e selecione **[!UICONTROL Ativar a página]** inicial de ativos. Salve as alterações.

   ![Ativar a página inicial de ativos na caixa de diálogo Preferências de usuário](assets/Annotation-color.png)

Depois de ativar a página inicial de Ativos, navegue até a interface do usuário de Ativos na página Navegação ou acesse-a diretamente do URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar o link de experiência na interface do usuário do Assets](assets/config-experience-link.png)

Toque/clique no link **[!UICONTROL Clique aqui para configurar seu link]** de experiência para adicionar seu nome de usuário, imagem de plano de fundo e imagem de perfil.

A Página inicial de Ativos inclui as seguintes seções:

* Seção de boas-vindas
* Seção do Widget

**Seção de boas-vindas**

Se o seu perfil existir, a seção Boas-vindas exibirá uma mensagem de boas-vindas endereçada a você. Além disso, exibe a imagem do seu perfil e uma imagem de boas-vindas (se já estiver configurado).

Se o seu perfil estiver incompleto, a seção Boas-vindas exibirá uma mensagem genérica de boas-vindas e um espaço reservado para a imagem do seu perfil.

**Seção do Widget**

Esta seção é exibida abaixo da seção Boas-vindas e exibe os widgets predefinidos nas seguintes seções:

* Atividade
* Recentes
* Descobrir

**Atividade**: Nesta seção, o widget **[!UICONTROL Minha atividade]** exibe atividades recentes executadas pelo usuário conectado com ativos (incluindo ativos sem representações), por exemplo, uploads de ativos, downloads, criação de ativos, edições, comentários, anotações e compartilhamentos.

**Recente**: O widget **[!UICONTROL Visualizado]** recentemente nesta seção exibe entidades acessadas recentemente pelo usuário conectado, incluindo pastas, coleções e projetos.

**Discover**: O widget **[!UICONTROL Novo]** nesta seção exibe os ativos e as execuções carregados recentemente na instância AEM Assets.

Para ativar a remoção de dados de atividade do usuário, ative o Serviço **[!UICONTROL de Expurgação de Evento do]** DAM no Configuration Manager. Após habilitar esse serviço, as atividades do usuário conectado que excedem um número especificado são excluídas pelo sistema.

A tela de boas-vindas fornece ferramentas de navegação fáceis, por exemplo ícones na barra de ferramentas para acessar pastas, coleções e catálogos.

>[!NOTE]
>
>Habilitar os serviços de Gravação [!UICONTROL e Expurgação] de Evento do CQ  Day DAM aumenta as operações de gravação no JCR e a indexação de pesquisa, o que aumenta significativamente a carga no servidor AEM. A carga adicional no servidor AEM pode afetar seu desempenho.

>[!CAUTION]
>
>A captura, filtragem e expurgação das atividades do usuário necessárias para a página inicial dos Ativos impõem uma sobrecarga no desempenho. Portanto, os administradores devem configurar a Página inicial de forma eficiente para os usuários-alvo.
>
>A Adobe recomenda que os administradores e usuários que executam operações em massa evitem usar o recurso Página inicial do ativo para evitar o aumento das atividades do usuário. Além disso, os administradores podem excluir atividades de gravação para usuários específicos ao configurar o Gravador [!UICONTROL de eventos] Day CQ DAM do [!UICONTROL Configuration Manager].
>
>Se você usar o recurso, a Adobe recomenda programar a frequência de expurgação com base na carga do servidor.
