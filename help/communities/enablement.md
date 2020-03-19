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
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

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

* **Gerentes** da comunidade Para comunidades de ativação, somente os membros do grupo de `Community Enablement Managers` usuários podem receber a função de `Community Site Enablement Manager`, cujas permissões podem incluir criação de conteúdo, atribuições e gerenciamento de membros no ambiente de publicação.

Configuração opcional de:

* **A** integração do Adobe Analytics com o Adobe Analytics adiciona recursos abrangentes de relatório e oferece suporte à adição do Video Heartbeat ao Analytics.

* **Dispatcher**

## Etapas de configuração {#configuration-steps}

Veja a seguir as etapas necessárias para ativar as comunidades.

Cada etapa vincula-se à documentação que fornece os detalhes necessários.

**Em todas as instâncias de autor/publicação:**

1. **[Instale o driver JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**Use Web Console (pacotes):*http://localhost:4502/system/console/bundles*instalar *antes*de instalar o pacote SCORM

1. **[Instale o pacote](deploy-communities.md#scorm-package)**SCORM Use o Gerenciador de pacotes:*http://localhost:4502/crx/packmgr/*

**Em qualquer servidor:**

1. **[Instalar MySQL, MySQL Workbench](mysql.md)**

1. **[Instalar bancos de dados](mysql.md#database-setup)**MySQL Executar scripts SQL baixados da instância do autorUsar MySQL Workbench

**Na mesma instância do autor de hospedagem do servidor:**

1. **[Instalar FFmpeg](ffmpeg.md)**

**Em todas as instâncias de autor/publicação:**

1. **[Configure o pool](mysql.md#configure-jdbc-connections)**de Conexões JDBCuse o Console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[Configurar o serviço](mysql.md#aem-communities-scormengine-service)**de mecanismo SCORMusar o Console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[Configurar filtros](mysql.md#adobe-granite-csrf-filter)**CSRFusar o Console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

**Na instância do autor:**

1. (*Opcional*) **[Configurar o serviço](analytics.md)**do Analytics Use Ferramentas, Implantação, console Serviços em nuvem:*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurar o console Fluxo de Trabalho/Modelos do FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**Use

1. **[Habilitar Serviço](deploy-communities.md#tunnel-service-on-author)**de TúnelUsar Console da Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[Criar administradores](users.md#creating-community-members)**da comunidade Para o ambiente do autor, use o console de segurança da interface clássica:*http://localhost:4502/useradmin*criar usuário(s) com caminho = /home/users/community

   * Adicione membros aos seguintes grupos:

      * Gerentes de habilitação da comunidade
      * Administradores de comunidades

## Dispatcher {#dispatcher}

Quando a implantação inclui o Dispatcher [do](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)AEM, para que os recursos de ativação funcionem corretamente, as seções `clientheader` e `filter` as seções precisam ser modificadas. Consulte [Configuração do Dispatcher para Comunidades](dispatcher.md#enablement).
