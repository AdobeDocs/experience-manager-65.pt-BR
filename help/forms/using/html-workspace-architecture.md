---
title: Arquitetura do AEM Forms Workspace
seo-title: AEM Forms Workspace Architecture
description: Informações conceituais e visão geral da arquitetura do espaço de trabalho do LiveCycle AEM Forms.
seo-description: Conceptual information and overview of the architecture of LiveCycle AEM Forms workspace.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Arquitetura do AEM Forms Workspace {#aem-forms-workspace-architecture}

O espaço de trabalho do AEM Forms é um aplicativo web hospedado no CRX™. Quando o espaço de trabalho é aberto em um navegador, um recurso CRX é acessado e o aplicativo é renderizado como página HTML no navegador.

O aplicativo acessa o servidor do AEM Forms nos endpoints REST para fazer o seguinte:

* Buscar tarefas do usuário, pontos de partida do processo, histórico do processo e informações do usuário
* Executar ação em tarefas
* Tarefas de consulta no banco de dados
* Atualizar preferências do usuário e muito mais

O servidor do AEM Forms acessa o banco de dados do AEM Forms pelo JDBC. O banco de dados mantém tarefas, processos e suas instâncias, usuários e informações relacionadas.

O espaço de trabalho do AEM Forms é projetado em componentes modulares JavaScript™ que podem ser personalizados e reutilizados individualmente em outras aplicações web. Os componentes são baseados no BackBone, uma biblioteca JavaScript que fornece estrutura para aplicações Web. Um artigo detalhado descrevendo a interação de componentes com o BackBone é [aqui](/help/forms/using/backbone-interaction.md). A organização dos componentes na estrutura de pastas do CRX é discutida em [este](/help/forms/using/folder-structure.md) artigo.

Pacotes entregues para o espaço de trabalho do AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: é um pacote CRX, ou seja, ele pode ser implantado no CRX usando o Gerenciador de pacotes.
* `adobe-lc-workspace-<version>-src.zip`: é um arquivo que contém o código completo do espaço de trabalho e scripts do AEM Forms para criar os pacotes de implantação — pacotes de Entrega, Depuração e Desenvolvimento.
