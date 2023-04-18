---
title: Selecionar sua interface do usuário
description: Para a conveniência dos usuários de criação, a interface habilitada para toque permite alternar para a interface clássica quando necessário.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Selecionar sua interface do usuário{#selecting-your-ui}

Como a interface habilitada para toque substitui a interface clássica, o usuário ou o administrador da instância de AEM deve tomar uma decisão ativa para continuar usando a interface clássica. Como a interface clássica não é mais mantida, não há como o usuário de criação simplesmente alternar da interface clássica para o equivalente na interface habilitada para toque.

Para a conveniência dos usuários de criação, a interface habilitada para toque permite alternar para a interface clássica quando necessário. Consulte a [Selecionar sua interface do usuário](/help/sites-authoring/select-ui.md) na documentação de criação padrão para obter detalhes.

>[!NOTE]
>
>As instâncias atualizadas de uma versão anterior manterão a interface clássica para a criação de página.
>
>Após a atualização, a criação de página não será alternada automaticamente para a interface habilitada para toque, mas você pode configurá-la usando a variável[Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de Modo de Interface do Usuário de Criação de WCM** ( `AuthoringUIMode` serviço). Consulte [Substituições da interface do usuário para o Editor](#uioverridesfortheeditor).

## Configuração da interface de usuário padrão para sua instância {#configuring-the-default-ui-for-your-instance}

Um administrador do sistema pode configurar a interface do usuário vista na inicialização e logon usando [Mapeamento de raiz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Isso pode ser substituído pelos padrões do usuário ou pelas configurações da sessão.
