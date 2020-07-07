---
title: Configuração dos recursos de ativação
seo-title: Configuração dos recursos de ativação
description: Configurar recursos de ativação nas Comunidades
seo-description: Configurar recursos de ativação nas Comunidades
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: ce21755263a2e8a3f0e97acb7f586e32cedde83a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---


# Configuração dos recursos de ativação {#configuring-enablement-features}

## Visão geral {#overview}

Os recursos de ativação fornecem a capacidade de criar comunidades [de](overview.md#enablement-community)ativação.

* Este recurso requer licenciamento adicional para uso em um ambiente de produção.

O uso dos recursos de ativação exige o seguinte:

Instalação de:

* **SCORM**

   O Sharable Content Object Reference Model (SCORM) é uma coleção de padrões e especificações para e-learning. O SCORM também define como o conteúdo pode ser empacotado em um arquivo ZIP transferível.

* **MySQL**

   O MySQL é um banco de dados relacional usado principalmente para rastreamento SCORM e dados de relatórios para Ativação, bem como tabelas para rastrear o progresso do vídeo. O SCORM para o pacote de recursos de ativação requer o driver JDBC MySQL.

* **FFmpeg**

   FFmpeg é uma solução para conversão e streaming de áudio e vídeo e, quando instalada, é usada para transcodificação adequada dos ativos [de](../../help/sites-authoring/default-components-foundation.md#video)vídeo. Para comunidades de ativação, é usado no ambiente do autor para obter metadados para recursos carregados, bem como para gerar uma miniatura para exibição ao listar o recurso.

Configuração de:

* **Gerentes da comunidade**

   Para comunidades de ativação, somente os membros do grupo de `Community Enablement Managers` usuários podem receber a função de `Community Site Enablement Manager`, cujas permissões podem incluir criação de conteúdo, atribuições e gerenciamento de membros no ambiente de publicação.

Configuração opcional de:

* **Adobe Analytics**

   A integração com o Adobe Analytics adiciona recursos abrangentes do relatórios e oferece suporte à adição do Video Heartbeat ao Analytics.

* **Dispatcher**

## Etapas de configuração {#configuration-steps}

Veja a seguir as etapas necessárias para ativar as comunidades.

Cada etapa vincula-se à documentação que fornece os detalhes necessários.

**Em todas as instâncias de autor/publicação:**

1. **[Instale o driver JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Usar o Console da Web (pacotes): *http://localhost:4502/system/console/bundles*

   Instale *antes* de instalar o pacote SCORM

1. **[Instalar pacote SCORM](deploy-communities.md#scorm-package)**


   Use o Gerenciador de pacotes: *http://localhost:4502/crx/packmgr/*

**Em qualquer servidor:**

1. **[Instalar MySQL, MySQL Workbench](mysql.md)**

1. **[Instalar bancos de dados MySQL](mysql.md#database-setup)**

   Executar scripts SQL baixados da instância do autor

   Usar o MySQL Workbench

**Na mesma instância do autor de hospedagem do servidor:**

1. **[Instalar FFmpeg](ffmpeg.md)**

**Em todas as instâncias de autor/publicação:**

1. **[Configurar pool de conexões JDBC](mysql.md#configure-jdbc-connections)**

   Usar console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurar o serviço de mecanismo SCORM](mysql.md#aem-communities-scormengine-service)**

   Usar console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurar filtros CSRF](mysql.md#adobe-granite-csrf-filter)**

   Usar console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

**Na instância do autor:**

1. (*Opcional*) **[Configurar o serviço Analytics](analytics.md)**

   Use Ferramentas, Implantação, console Cloud Service: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurar FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Usar console Fluxo de trabalho/Modelos

1. **[Ativar serviço de túnel](deploy-communities.md#tunnel-service-on-author)**

   Usar console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Criar administradores da comunidade](users.md#creating-community-members)**

   Para o ambiente do autor, use o console de segurança da interface clássica: *http://localhost:4502/useradmin*

   Criar usuário(s) com caminho = /home/users/community

   * Adicione membros aos seguintes grupos:

      * Gerentes de habilitação da comunidade
      * Administradores de comunidades

## Dispatcher {#dispatcher}

Quando a implantação inclui o Dispatcher [do](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)AEM, para que os recursos de ativação funcionem corretamente, as seções `clientheader` e `filter` as seções precisam ser modificadas. Consulte [Configuração do Dispatcher para comunidades](dispatcher.md#enablement).
