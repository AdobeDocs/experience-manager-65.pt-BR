---
title: Seleção da interface
description: Para conveniência de criação de usuários, a interface habilitada para toque permite alternar para a interface clássica quando necessário.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Seleção da interface{#selecting-your-ui}

Como a interface habilitada para toque substitui a interface clássica, o usuário ou administrador da instância do AEM deve tomar uma decisão ativa para continuar usando a interface clássica. Como a interface clássica não é mais mantida, não há como o usuário de criação simplesmente alternar da interface clássica para o equivalente na interface habilitada para toque.

Para conveniência de criação de usuários, a interface habilitada para toque permite alternar para a interface clássica quando necessário. Consulte a [Seleção da interface](/help/sites-authoring/select-ui.md) na Documentação de criação padrão para obter detalhes.

>[!NOTE]
>
>As instâncias atualizadas de uma versão anterior manterão a interface clássica para a criação de páginas.
>
>Depois da atualização, a criação de página não será alternada automaticamente para a interface habilitada para toque, mas você poderá configurá-la usando o[Configuração OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de modo de interface do usuário de criação do WCM** ( `AuthoringUIMode` serviço). Consulte [Substituições da interface do usuário para o editor](#uioverridesfortheeditor).

## Configuração da interface do usuário padrão para sua instância {#configuring-the-default-ui-for-your-instance}

Um administrador do sistema pode configurar a interface do usuário exibida na inicialização e no logon usando [Mapeamento de raiz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Isso pode ser substituído pelos padrões do usuário ou pelas configurações da sessão.
