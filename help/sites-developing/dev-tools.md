---
title: Ferramentas de desenvolvimento
description: Para desenvolver aplicativos JCR, Apache Sling ou Adobe Experience Manager, vários conjuntos de ferramentas estão disponíveis.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 4%
---
# Ferramentas de desenvolvimento{#development-tools}

Para desenvolver aplicativos JCR, Apache Sling ou Adobe Experience Manager (AEM), os seguintes conjuntos de ferramentas estão disponíveis:

* um conjunto formado por [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) e WebDAV. O CRXDE Lite está incorporado ao CRX/AEM e permite executar tarefas de desenvolvimento padrão no navegador. Com o CRXDE Lite, você pode criar e editar arquivos (como .jsp e .java), pastas, modelos, componentes, caixas de diálogo, nós, propriedades e pacotes, ao fazer logon e integrar com o SVN.

  O CRXDE Lite é recomendado quando você não tem acesso direto ao servidor CRX/AEM, quando desenvolve um aplicativo estendendo ou modificando os componentes prontos para uso e pacotes Java™ ou quando não precisa de um depurador dedicado, autocompletar de código e realce de sintaxe.

* Um conjunto constituído pelo seguinte:
  * Um ambiente de desenvolvimento integrado. Por exemplo, [Eclipse](/help/sites-developing/howto-projects-eclipse.md) ou [IntelliJ](/help/sites-developing/ht-intellij.md).
  * Uma ferramenta de criação. Por exemplo, [Apache Maven](/help/sites-developing/ht-projects-maven.md).
  * FileVault, que foi desenvolvido pela Adobe para mapear um repositório em um sistema de arquivos, um sistema de controle de versão. Por exemplo, Subversion.
  * Um sistema de rastreio de erros. Por exemplo, Jira.
  * Um sistema central de gerenciamento de dependências. Por exemplo, Apache Archiva.
  * E um sistema de automação de construção. Por exemplo, Apache Continuum.

  Essa configuração permite integrar totalmente o aplicativo (conteúdo, código, configuração) em qualquer ambiente e processo de desenvolvimento. O link entre os diferentes elementos é a representação do repositório no sistema de arquivos por meio do FileVault, já que todas as ferramentas de desenvolvimento mencionadas anteriormente podem funcionar com arquivos.

## Extensões para ambientes de desenvolvimento integrados {#extensions-for-integrated-development-environments}

A Adobe lançou as seguintes extensões:

* [Extensão do AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Extensão AEM Brackets](/help/sites-developing/aem-brackets.md)

### Outras ferramentas {#other-tools}

O AEM é fornecido com outras ferramentas que facilitam o desenvolvimento:

* [Editor de caixa de diálogo](/help/sites-developing/dialog-editor.md)
* [Usar o Translator para gerenciar dicionários](/help/sites-developing/i18n-translator.md)
* [Gerenciamento de pacotes usando o Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Como desenvolver projetos do AEM usando o Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Como criar projetos do AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Como desenvolver projetos do AEM usando o IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Como usar a ferramenta VLT](/help/sites-developing/ht-vlttool.md)
* [Como usar a ferramenta Servidor proxy](/help/sites-developing/ht-proxy-server.md)
* [Ferramentas de Modernização do AEM](/help/sites-developing/modernization-tools.md)
* [Ferramenta AEM Repo](/help/sites-developing/aem-repo-tool.md)

Ferramentas que facilitam a criação de novos projetos:

* [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
* [Modelos do AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>O tutorial a seguir pode ser de interesse para iniciar um novo projeto do AEM:
>[Introdução ao AEM Sites Parte 1 - Configuração do projeto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
