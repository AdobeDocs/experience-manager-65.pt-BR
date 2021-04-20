---
title: JSRP - Provedor de recursos de armazenamento JCR
seo-title: JSRP - Provedor de recursos de armazenamento JCR
description: O JSRP geralmente é mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor
seo-description: O JSRP geralmente é mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# JSRP - Provedor de recursos de armazenamento JCR {#jsrp-jcr-storage-resource-provider}

## Sobre o JSRP {#about-jsrp}

Quando o AEM Communities usa o JSRP como sua opção de armazenamento (o padrão), o conteúdo da comunidade é armazenado no JCR e o conteúdo gerado pelo usuário (UGC) é acessível somente a partir da instância de autor ou publicação na qual foi publicado.

Devido à simplicidade da implantação, o JSRP geralmente é mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor.

Consulte também [Características das Opções de SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias recomendadas](topologies.md).

## Configuração {#configuration}

### Selecione JSRP {#select-jsrp}

Por padrão, o JSRP é a opção de armazenamento para UGC.

O [console Configuração de Armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação do SRP usar.

No ambiente de criação, para acessar o console Configuração de armazenamento

* Na navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuração de Armazenamento]**

* Selecione **[!UICONTROL Provedor de Recursos de Armazenamento JCR (JSRP)]**

* Selecione **[!UICONTROL Enviar]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publicar a configuração {#publishing-the-configuration}

Embora o JSRP seja a configuração padrão, para garantir que a configuração idêntica seja definida no ambiente de publicação:

* Na navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**
* Selecione **[!UICONTROL Ativar árvore]** > **[!UICONTROL Iniciar caminho]**:

   * Navegue até `/conf/global/settings/community/srpc/`

* Selecione **[!UICONTROL Ativar]**

## Gerenciando dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuário* e *grupos de usuários*, normalmente inseridos no ambiente de publicação, visite:

* [Sincronização de usuários](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Resolução de problemas {#troubleshooting}

### UGC não visível no JCR {#ugc-not-visible-in-jcr}

Verifique se o JSRP foi configurado para ser o provedor padrão verificando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é o JSRP.

Em todas as instâncias de criação e publicação AEM, revise o console Configuração de armazenamento ou verifique o repositório AEM:

* No JCR, se [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Não contém um nó [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), as propriedades da configuração padrão deverão definir o JSRP para ser o provedor padrão.

### UGC não visível na instância do autor {#ugc-not-visible-on-author-instance}

Isso não é um erro. Uma característica do JSRP é que o conteúdo da comunidade inserido no ambiente de publicação só estará visível no ambiente de publicação.

### UGC não visível na instância de publicação {#ugc-not-visible-on-publish-instance}

Se uma única instância de publicação ou se um cluster de publicação estiver implantado, siga as instruções para [UGC Not Visible in JCR](#ugc-not-visible-in-jcr).

Se um farm de publicação for implantado, uma característica do JSRP é que o conteúdo da comunidade só será visível na instância de publicação em que foi publicado.

Para que o UGC fique visível de qualquer instância de publicação, é necessário um cluster de publicação.
