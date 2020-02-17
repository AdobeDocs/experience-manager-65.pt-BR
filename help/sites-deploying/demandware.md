---
title: Salesforce Commerce Cloud
seo-title: Salesforce Commerce Cloud / Demandware
description: Saiba como implantar o eCommerce com a Salesforce Commerce Cloud / Demandware.
seo-description: Saiba como implantar o eCommerce com a Salesforce Commerce Cloud / Demandware.
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Salesforce Commerce Cloud{#salesforce-commerce-cloud}

A implantação dos pacotes necessários de comércio eletrônico proporcionará a funcionalidade completa da estrutura de comércio eletrônico, juntamente com uma implementação de referência da funcionalidade de comércio eletrônico, conforme fornecida com uma implementação da Salesforce Commerce Cloud / Demandware (incluindo um catálogo de demonstração).

## Pacotes necessários para comércio eletrônico com a Salesforce Commerce Cloud {#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}

Para instalar a funcionalidade de comércio eletrônico, é necessário:

* Estrutura de comércio eletrônico do AEM:

   * isso é parte de uma instalação padrão do AEM

* Pacote de conteúdo do AEM Demandware Commerce

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>Essa integração oferece suporte às instâncias da Salesforce Commerce Cloud / Demandware configuradas para usar a versão 17.6 ou posterior do OCAPI.

### Instalação do comércio eletrônico com a Salesforce Commerce Cloud {#installation-of-ecommerce-with-salesforce-commerce-cloud}

Para instalar o AEM com uma configuração de integração do Demandware Commerce (usando o catálogo de demonstração, Geometrixx Outdoors), as etapas básicas são:

1. [Instale o AEM](/help/sites-deploying/deploy.md).
1. Instale o pacote de conteúdo usando o gerenciador de [pacotes](/help/sites-administering/package-manager.md):
1. [Crie](/help/sites-authoring/page-authoring.md) quaisquer páginas suplementares que você precisar no AEM.

>[!NOTE]
>
>Para baixar os pacotes, navegue até [Compartilhamento](/help/sites-administering/package-manager.md#package-share)de pacotes.

A conexão do servidor entre o AEM e o Demandware Sandbox precisa ser configurada. A maior parte da configuração já está pré-configurada para funcionar com o pacote de conteúdo de demonstração do SiteGenisis fornecido usando caminhos padrão, bibliotecas e assim por diante. Se o conector for usado com outros sites e bibliotecas, será necessário atualizar essa configuração.

1. Navegue até [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Clique em **Demandware Client**.
1. Digite o nome do host ou o ip do ponto de extremidade da **Instância** , conforme necessário.

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Clique em **Salvar**.
1. Clique em Plug-in **Demandware TransportHandler para WebDAV**.
1. Defina o usuário **** WebDAV e a senha **do usuário** WebDAV.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Clique em **Salvar**.

#### Replicação {#replication}

A replicação deve ser ativada após a instalação do pacote, você pode verificar se: [https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>O agente de replicação está configurado para o nível de log de informações por padrão. Se desejar mais informações, você pode alternar o nível de log para depurar.

#### OAuth {#oauth}

O cliente OAuth está configurado para funcionar com uma instância de caixa de proteção Demandware. Para fins de teste, não é necessária nenhuma alteração.

Para sistemas de armazenamento temporário e de produção, os clientes OAuth precisam ser configurados com a ID do cliente e a senha apropriadas.

1. Navegue até [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Clique em **Demandware Access Token Provider (Provedor** de token de acesso Demandware).

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. Modifique os valores conforme necessário e clique em **Salvar**.

### Salesforce Commerce Cloud Sandbox {#salesforce-commerce-cloud-sandbox}

A caixa de proteção Demandware deve estar configurada para executar o novo mecanismo de modelo Velocity.

>[!NOTE]
>
>O seguinte assistente não faz parte do conector AEM Demandware. Ele é fornecido como parte do pacote de conteúdo de demonstração para ajudar na configuração rápida das páginas de demonstração do SiteGenesis.

1. Navegue até [https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html).
1. Clique em **Editar.**
1. Verifique os valores e clique em **OK**.
1. Clique em **Inicializar**.
1. Vá para a pasta WebDAV e verifique se há arquivos de modelo publicados, por exemplo em `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`.

   >[!NOTE]
   >
   >A extensão será `.vs`.

1. Verifique também se há arquivos JS e CSS exportados, por exemplo em `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`.

