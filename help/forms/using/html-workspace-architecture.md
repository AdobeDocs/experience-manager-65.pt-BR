---
title: Arquitetura do AEM Forms Workspace
seo-title: AEM Forms Workspace Architecture
description: Informações conceituais e visão geral da arquitetura do LiveCycle AEM Forms workspace.
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

O AEM Forms workspace é um aplicativo web hospedado no CRX™. Quando o espaço de trabalho é aberto em um navegador, um recurso CRX é acessado e o aplicativo é renderizado como HTML no navegador.

O aplicativo acessa o servidor AEM Forms em pontos de extremidade REST para fazer o seguinte:

* Buscar tarefas do usuário, pontos de partida do processo, histórico do processo e informações do usuário
* Executar ação em tarefas
* Tarefas de consulta no banco de dados
* Atualizar preferências do usuário e muito mais

O servidor do AEM Forms acessa o banco de dados AEM Forms por meio do JDBC. O banco de dados persiste tarefas, processos e suas instâncias, usuários e informações relacionadas.

A área de trabalho do AEM Forms é projetada em componentes modulares do JavaScript™ que podem ser personalizados individualmente e reutilizados em outros aplicativos da Web. Os componentes são baseados no BackBone, que é uma biblioteca de JavaScript que oferece estrutura para aplicativos da Web. Um artigo detalhado que descreve a interação de componentes com o BackBone é [here](/help/forms/using/backbone-interaction.md). A organização dos componentes na estrutura da pasta CRX é discutida em [this](/help/forms/using/folder-structure.md) artigo 10. o

Pacotes fornecidos para a área de trabalho do AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: É o pacote CRX, ou seja, ele pode ser implantado no CRX usando o Gerenciador de Pacotes.
* `adobe-lc-workspace-<version>-src.zip`: É um arquivo que contém código completo do espaço de trabalho e scripts do AEM Forms para criar os pacotes de implantação — Entrega, Depuração e Pacotes de Desenvolvimento.
