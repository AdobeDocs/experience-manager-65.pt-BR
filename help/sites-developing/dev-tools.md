---
title: Ferramentas de desenvolvimento
seo-title: Ferramentas de desenvolvimento
description: Para desenvolver seus aplicativos JCR, Apache Sling ou AEM, vários conjuntos de ferramentas estão disponíveis
seo-description: Para desenvolver seus aplicativos JCR, Apache Sling ou AEM, vários conjuntos de ferramentas estão disponíveis
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 2%

---


# Ferramentas de desenvolvimento{#development-tools}

Para desenvolver seus aplicativos JCR, Apache Sling ou AEM, os seguintes conjuntos de ferramentas estão disponíveis:

* um conjunto que consiste em [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) e WebDAV. O CRXDE Lite está incorporado ao CRX/AEM e permite que você execute tarefas de desenvolvimento padrão no navegador. Com o CRXDE Lite, você pode criar e editar arquivos (como .jsp e .java), pastas, modelos, componentes, caixas de diálogo, nós, propriedades e pacotes enquanto faz logon e integração com o SVN.

   O CRXDE Lite é recomendado quando você não tem acesso direto ao servidor CRX/AEM, quando desenvolve um aplicativo, estendendo ou modificando os componentes predefinidos e os pacotes Java ou quando não precisa de um depurador dedicado, finalização de código e realce de sintaxe.

* um conjunto composto por um Ambiente de desenvolvimento integrado (por exemplo: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) ou [IntelliJ](/help/sites-developing/ht-intellij.md)), uma ferramenta de compilação (por exemplo: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault que foi desenvolvido pela Adobe para mapear um repositório para um sistema de arquivos, um sistema de controle de versão (por exemplo: Subversão), um sistema de rastreamento de erros (por exemplo: Jira), um sistema central de gestão de dependência (por exemplo: Apache Archiva) e um sistema de automação de construção (por exemplo: Apache Continuum).

   Esta configuração permite integrar totalmente seu aplicativo (conteúdo, código, configuração) em qualquer ambiente e processo de desenvolvimento. O link entre os diferentes elementos é a representação do sistema de arquivos do repositório pelo FileVault, já que todas as ferramentas de desenvolvimento mencionadas anteriormente podem funcionar com arquivos.

## Extensões para Ambientes de desenvolvimento integrados {#extensions-for-integrated-development-environments}

O Adobe lançou as seguintes extensões:

* [AEM Extensão Eclipse](/help/sites-developing/aem-eclipse.md)
* [Extensão dos colchetes AEM](/help/sites-developing/aem-brackets.md)
* [AEM extensão](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)  IntelliJ (de cabo)

### Outras ferramentas {#other-tools}

AEM navios com outras ferramentas que facilitem o desenvolvimento:

* [Editor de diálogo](/help/sites-developing/dialog-editor.md)
* [Uso do tradutor para gerenciar dicionários](/help/sites-developing/i18n-translator.md)
* [Gerenciamento De Pacotes Usando O Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Como desenvolver projetos AEM usando o Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Como desenvolver projetos AEM usando o IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Como usar a ferramenta VLT](/help/sites-developing/ht-vlttool.md)
* [Como usar a ferramenta Servidor proxy](/help/sites-developing/ht-proxy-server.md)
* [Ferramenta de conversão de diálogo](/help/sites-developing/dialog-conversion.md)
* [Ferramenta AEM Repo](/help/sites-developing/aem-repo-tool.md)

Ferramentas que facilitam a criação de novos projetos:

* [Arquétipo de projeto do AEM](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Modelos AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>O tutorial a seguir pode ser de interesse para iniciar um novo projeto AEM:
>[Introdução ao AEM Sites Parte 1 - Configuração do projeto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

