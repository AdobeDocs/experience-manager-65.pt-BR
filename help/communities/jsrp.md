---
title: JSRP - Provedor de recurso de armazenamento JCR
seo-title: JSRP - JCR Storage Resource Provider
description: O JSRP geralmente é mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor
seo-description: JSRP is generally best suited for demonstration or development environments of one publish instance and one author instance
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# JSRP - Provedor de recurso de armazenamento JCR {#jsrp-jcr-storage-resource-provider}

## Sobre o JSRP {#about-jsrp}

Quando o AEM Communities usa o JSRP como sua opção de armazenamento (o padrão), o conteúdo da comunidade é armazenado no JCR e o conteúdo gerado pelo usuário (UGC) pode ser acessado somente a partir da instância de autor ou publicação na qual foi postado.

Devido à simplicidade de implantação, o JSRP geralmente é mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor.

Consulte também [Características das opções de SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias recomendadas](topologies.md).

## Configuração {#configuration}

### Selecionar JSRP {#select-jsrp}

Por padrão, JSRP é a opção de armazenamento para UGC.

A variável [Console de configuração de armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação de SRP usar.

No ambiente de criação, para acessar o console de Configuração de armazenamento

* Na navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Communities]** > **[!UICONTROL Configuração de armazenamento]**

* Selecionar **[!UICONTROL Provedor de recurso de armazenamento JCR (JSRP)]**

* Selecione **[!UICONTROL Enviar]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publicar a configuração {#publishing-the-configuration}

Embora o JSRP seja a configuração padrão, para garantir que a configuração idêntica seja definida no ambiente de publicação:

* Na navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**
* Selecionar **[!UICONTROL Ativar árvore]** > **[!UICONTROL Caminho inicial]**:

   * Navegue até `/conf/global/settings/community/srpc/`

* Selecionar **[!UICONTROL Ativar]**

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuário* e *grupos de usuários*, frequentemente inseridos no ambiente de publicação, visitem:

* [Sincronização de usuário](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Resolução de problemas {#troubleshooting}

### UGC não visível no JCR {#ugc-not-visible-in-jcr}

Verifique se o JSRP foi configurado para ser o provedor padrão, verificando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é JSRP.

Em todas as instâncias de criação e publicação do AEM, revise o console Configuração de armazenamento ou verifique o repositório AEM:

* No JCR, se [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Não contém um [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), as propriedades defaultconfiguration devem definir o JSRP como o provedor padrão.

### UGC não visível na instância do autor {#ugc-not-visible-on-author-instance}

Isso não é um erro. Uma característica do JSRP é que o conteúdo da comunidade inserido no ambiente de publicação só será visível no ambiente de publicação.

### UGC não visível na instância de publicação {#ugc-not-visible-on-publish-instance}

Se uma única instância de publicação ou se um cluster de publicação estiver implantado, siga as instruções para [UGC não visível no JCR](#ugc-not-visible-in-jcr).

Se um farm de publicação for implantado, uma característica do JSRP é que o conteúdo da comunidade só estará visível na instância de publicação em que foi postado.

Para que o UGC seja visível de qualquer instância de publicação, é necessário um cluster de publicação.
