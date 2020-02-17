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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuração dos recursos de ativação {#configuring-enablement-features}

## Visão geral {#overview}

Os recursos de ativação fornecem a capacidade de criar comunidades [de](overview.md#enablement-community)ativação.

* Este recurso requer licenciamento adicional para uso em um ambiente de produção.

O uso dos recursos de ativação exige o seguinte:

Instalação de:

* **SCORM** Sharable Content Object Reference Model (SCORM) é uma coleção de padrões e especificações para e-learning. O SCORM também define como o conteúdo pode ser empacotado em um arquivo ZIP transferível.

* **MySQL** MySQL é um banco de dados relacional usado principalmente para rastreamento SCORM e dados de relatório para Ativação, bem como tabelas para rastrear o progresso do vídeo. O SCORM para o pacote de recursos de ativação requer o driver JDBC MySQL.

* **FFmpeg** FFmpeg é uma solução para conversão e transmissão de áudio e vídeo e, quando instalada, é usada para transcodificação adequada dos ativos [de](../../help/sites-authoring/default-components-foundation.md#video)vídeo. Para comunidades de ativação, é usado no ambiente do autor para obter metadados para recursos carregados, bem como para gerar uma miniatura para exibição ao listar o recurso.

Configuração de:

* **Gerentes** da comunidade Para comunidades de ativação, somente os membros do grupo de `Community Enablement Managers` usuários podem receber a função de `*Community Site* Enablement Manager`, cujas permissões podem incluir criação de conteúdo, atribuições e gerenciamento de membros no ambiente de publicação.

Configuração opcional de:

* **A** integração do Adobe Analytics com o Adobe Analytics adiciona recursos abrangentes de relatório e oferece suporte à adição do Video Heartbeat ao Analytics.

* **Dispatcher**

## Etapas de configuração {#configuration-steps}

Veja a seguir as etapas necessárias para ativar as comunidades.

Cada etapa vincula à documentação que fornece os detalhes necessários.

**Em todas as instâncias de autor/publicação:**

1. **[instale o driver JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**Use Web Console (pacotes):*http://localhost:4502/system/console/bundles*instalar *antes*de instalar o pacote SCORM

1. **[instale o pacote](deploy-communities.md#scorm-package)**SCORM Use Package Manager:*http://localhost:4502/crx/packmgr/*

**Em qualquer servidor:**

1. **[instalar MySQL, MySQL Workbench](mysql.md)**

1. **[instalar bancos de dados](mysql.md#database-setup)**MySQL Executar scripts SQL baixados da instância do autorUsar MySQL Workbench

**Na mesma instância do autor de hospedagem do servidor:**

1. **[instalar FFmpeg](ffmpeg.md)**

**Em todas as instâncias de autor/publicação:**

1. **[configurar o pool](mysql.md#configure-jdbc-connections)**de Conexões JDBC Usar Console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[configurar o serviço](mysql.md#aem-communities-scormengine-service)**de mecanismo SCORMusar o Console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[configurar filtros](mysql.md#adobe-granite-csrf-filter)**CSRFusar o Console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

**Na instância do autor:**

1. (*opcional*) **[configure o serviço](analytics.md)**Analytics Use Ferramentas, Implantação, console Serviços em nuvem:*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[configurar o console](ffmpeg.md#configure-ffmpeg-transcoding-service)**Usar Fluxo de Trabalho/Modelos

1. **[habilitar o serviço](deploy-communities.md#tunnel-service-on-author)**de túnel Usar o console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[criar administradores](users.md#creating-community-members)**da comunidade Para o ambiente do autor, use o console de segurança da interface clássica:*http://localhost:4502/useradmin*criar usuários com caminho = /home/users/community

   * Adicione membros aos seguintes grupos:

      * Gerentes de habilitação da comunidade
      * Administradores de comunidades

## Dispatcher {#dispatcher}

Quando a implantação inclui o Dispatcher [do](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)AEM, para que os recursos de ativação funcionem corretamente, as `clientheader`seções `filter`e os recursos precisam ser modificados. Consulte [Configuração do Dispatcher para Comunidades](dispatcher.md#enablement).
