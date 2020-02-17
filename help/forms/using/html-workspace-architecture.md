---
title: Arquitetura do AEM Forms Workspace
seo-title: Arquitetura do AEM Forms Workspace
description: Informações conceituais e visão geral da arquitetura do espaço de trabalho do LiveCycle AEM Forms.
seo-description: Informações conceituais e visão geral da arquitetura do espaço de trabalho do LiveCycle AEM Forms.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Arquitetura do AEM Forms Workspace {#aem-forms-workspace-architecture}

A área de trabalho do AEM Forms é um aplicativo da Web hospedado no CRX™. Quando o espaço de trabalho é aberto em um navegador, um recurso CRX é acessado e o aplicativo é renderizado como página HTML no navegador.

O aplicativo acessa o servidor AEM Forms em pontos de extremidade REST para fazer o seguinte:

* Buscar tarefas do usuário, pontos de partida do processo, histórico do processo e informações do usuário
* Executar ação em tarefas
* Tarefas de consulta no banco de dados
* Atualizar preferências do usuário e muito mais

O servidor do AEM Forms acessa o banco de dados do AEM Forms em JDBC. O banco de dados persiste tarefas, processos e suas instâncias, usuários e informações relacionadas.

A área de trabalho do AEM Forms é projetada para componentes modulares do JavaScript™ que podem ser personalizados e reutilizados individualmente em outros aplicativos da Web. Os componentes são baseados no BackBone, que é uma biblioteca JavaScript que fornece estrutura para aplicativos da Web. Um artigo detalhado que descreve a interação de componentes com o BackBone está [aqui](/help/forms/using/backbone-interaction.md). A organização de componentes na estrutura de pastas CRX é discutida [neste](/help/forms/using/folder-structure.md) artigo.

Pacotes entregues para a área de trabalho do AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: É um pacote CRX, ou seja, pode ser implantado no CRX usando o Gerenciador de pacotes.
* `adobe-lc-workspace-<version>-src.zip`: É um arquivo que contém o código completo da área de trabalho e scripts do AEM Forms para criar os pacotes de implantação — remessa, depuração e desenvolvimento.

**[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)**
