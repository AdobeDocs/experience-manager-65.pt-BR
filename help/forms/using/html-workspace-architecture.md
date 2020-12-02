---
title: Arquitetura do AEM Forms Workspace
seo-title: Arquitetura do AEM Forms Workspace
description: Informações conceituais e visão geral da arquitetura da área de trabalho do LiveCycle AEM Forms.
seo-description: Informações conceituais e visão geral da arquitetura da área de trabalho do LiveCycle AEM Forms.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Arquitetura do AEM Forms Workspace {#aem-forms-workspace-architecture}

A área de trabalho AEM Forms é um aplicativo da Web hospedado no CRX™. Quando o espaço de trabalho é aberto em um navegador, um recurso CRX é acessado e o aplicativo é renderizado como página HTML no navegador.

O aplicativo acessa o servidor AEM Forms em pontos de extremidade REST para fazer o seguinte:

* Buscar tarefas do usuário, pontos de partida do processo, histórico do processo e informações do usuário
* Executar ação no tarefa
* Tarefas do query no banco de dados
* Atualize as preferências do usuário e muito mais

O servidor AEM Forms acessa o banco de dados AEM Forms por meio do JDBC. O banco de dados persiste tarefas, processos e suas instâncias, usuários e informações relacionadas.

A área de trabalho do AEM Forms é projetada para componentes modulares do JavaScript™ que podem ser personalizados e reutilizados individualmente em outros aplicativos da Web. Os componentes são baseados no BackBone, que é uma biblioteca JavaScript que fornece estrutura para aplicativos da Web. Um artigo detalhado que descreve a interação de componentes com o BackBone é [here](/help/forms/using/backbone-interaction.md). A organização de componentes na estrutura de pastas CRX é discutida no artigo [this](/help/forms/using/folder-structure.md).

Pacotes entregues para a área de trabalho do AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: É um pacote CRX, ou seja, pode ser implantado no CRX usando o Gerenciador de pacotes.
* `adobe-lc-workspace-<version>-src.zip`: É um arquivo que contém o código completo da área de trabalho e scripts da AEM Forms para criar os pacotes de implantação — Envio, Depuração e Desenvolvimento.
