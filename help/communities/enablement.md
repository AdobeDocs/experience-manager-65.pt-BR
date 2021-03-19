---
title: Configuração dos recursos de ativação
seo-title: Configuração dos recursos de ativação
description: Configurar recursos de ativação em Comunidades
seo-description: Configurar recursos de ativação em Comunidades
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---


# Configurar recursos de ativação {#configuring-enablement-features}

## Visão geral {#overview}

Os recursos de ativação fornecem a capacidade de criar [comunidades de ativação](overview.md#enablement-community).

* Esse recurso requer licenciamento adicional para uso em um ambiente de produção.

O uso dos recursos de ativação exige o seguinte:

Instalação de:

* **SCORM**

   O Sharable Content Object Reference Model (SCORM) é uma coleção de padrões e especificações para e-learning. O SCORM também define como o conteúdo pode ser empacotado em um arquivo ZIP transferível.

* **MySQL**

   O MySQL é um banco de dados relacional usado principalmente para rastreamento e relatórios de SCORM para Ativação, bem como tabelas para rastrear o progresso do vídeo. O pacote de recursos SCORM for enablement requer o driver JDBC do MySQL.

* **FFmpeg**

   FFmpeg é uma solução para converter e transmitir áudio e vídeo e, quando instalado, é usado para a transcodificação adequada do [Video Assets](../../help/sites-authoring/default-components-foundation.md#video). Para comunidades de ativação, ele é usado no ambiente de criação para obter metadados para recursos carregados, bem como gerar uma miniatura para exibição ao listar o recurso.

Configuração de:

* **Gerentes da comunidade**

   Para comunidades de ativação, somente os membros do grupo de usuários `Community Enablement Managers` podem receber a função de `Community Site Enablement Manager`, cujas permissões podem incluir criação de conteúdo, atribuições e gerenciamento de membros no ambiente de publicação.

Configuração opcional de:

* **Adobe Analytics**

   A integração com o Adobe Analytics adiciona recursos abrangentes de relatório e oferece suporte à adição do Video Heartbeat ao Analytics.

* **Dispatcher**

## Etapas de configuração {#configuration-steps}

Veja a seguir as etapas necessárias para ativar as comunidades.

Cada etapa vincula-se à documentação que fornece os detalhes necessários.

**Em todas as instâncias de autor/publicação:**

1. **[Instale o driver JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Use o Console da Web (pacotes): *http://localhost:4502/system/console/bundles*

   Instale *antes de* instalar o pacote SCORM

1. **[Instalar pacote SCORM](deploy-communities.md#scorm-package)**


   Usar o Gerenciador de Pacotes: *http://localhost:4502/crx/packmgr/*

**Em qualquer servidor:**

1. **[Instalar MySQL, MySQL Workbench](mysql.md)**

1. **[Instalar bancos de dados MySQL](mysql.md#database-setup)**

   Executar scripts SQL baixados da instância do autor

   Usar o MySQL Workbench

**Na mesma instância do autor de hospedagem do servidor:**

1. **[Instalar FFmpeg](ffmpeg.md)**

**Em todas as instâncias de autor/publicação:**

1. **[Configurar pool de conexões JDBC](mysql.md#configure-jdbc-connections)**

   Usar o Console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurar o serviço de mecanismo SCORM](mysql.md#aem-communities-scormengine-service)**

   Usar o Console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurar filtros CSRF](mysql.md#adobe-granite-csrf-filter)**

   Usar o Console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

**Na instância do autor:**

1. (*Opcional*) **[Configurar o serviço do Analytics](analytics.md)**

   Use Ferramentas, Implantação, console Cloud Services: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurar FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Usar o console Fluxo de trabalho/Modelos

1. **[Ativar serviço de túnel](deploy-communities.md#tunnel-service-on-author)**

   Usar o Console da Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Criar administradores da comunidade](users.md#creating-community-members)**

   Para o ambiente do autor, use o console de segurança da interface clássica: *http://localhost:4502/useradmin*

   Crie usuários com caminho = /home/users/community

   * Adicione membros aos seguintes grupos:

      * Gerentes de ativação da comunidade
      * Administradores das Comunidades

## Dispatcher {#dispatcher}

Quando a implantação inclui [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), para que os recursos de ativação funcionem corretamente, as seções `clientheader` e `filter` precisam de modificação. Consulte [Configuração do Dispatcher para Comunidades](dispatcher.md#enablement).
