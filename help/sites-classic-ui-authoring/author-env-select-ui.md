---
title: Selecionar sua IU
seo-title: Selecionar sua interface do usuário
description: Para a praticidade dos usuários de criação, a interface do usuário habilitada para toque permite alternar para a interface do usuário clássica quando necessário.
seo-description: Para a praticidade dos usuários de criação, a interface do usuário habilitada para toque permite alternar para a interface do usuário clássica quando necessário.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 60%

---


# Selecionar sua interface do usuário{#selecting-your-ui}

Como a interface habilitada para toque substitui a interface clássica, o usuário ou o administrador da instância AEM deve tomar uma decisão ativa para continuar usando a interface clássica. Como a interface clássica não é mais mantida, não há como o usuário de criação simplesmente alternar da interface clássica para o equivalente na interface habilitada para toque.

Para a praticidade dos usuários de criação, a interface do usuário habilitada para toque permite alternar para a interface do usuário clássica quando necessário. Consulte a documentação de criação padrão [Selecionar sua interface do usuário](/help/sites-authoring/select-ui.md) para obter detalhes.

>[!NOTE]
>
>As instâncias atualizadas de uma versão anterior manterão a interface clássica para a criação de página.
>
>Após a atualização, a criação de página não será alternada automaticamente para a interface habilitada para toque, mas você pode configurá-la usando a configuração [OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de modo de interface de criação do WCM** ( `AuthoringUIMode` serviço). Consulte [Substituições da interface do usuário para o Editor](#uioverridesfortheeditor).

## Configuração da interface de usuário padrão para a sua instância {#configuring-the-default-ui-for-your-instance}

Um administrador do sistema pode configurar a interface do usuário que é vista na inicialização e logon usando um [Mapeamento de raiz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Isso pode ser substituído pelos padrões do usuário ou configurações de sessão.
