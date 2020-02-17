---
title: JSRP - Provedor de recursos de armazenamento JCR
seo-title: JSRP - Provedor de recursos de armazenamento JCR
description: O JSRP é geralmente mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor
seo-description: O JSRP é geralmente mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: aa2c75e061e00ba74d54843a5f35bb7d82d12a92

---


# JSRP - Provedor de recursos de armazenamento JCR {#jsrp-jcr-storage-resource-provider}

## Sobre o JSRP {#about-jsrp}

Quando o AEM Communities usa o JSRP como sua opção de armazenamento (o padrão), o conteúdo da comunidade é armazenado no JCR e o conteúdo gerado pelo usuário (UGC) é acessível somente da instância do autor ou publicação na qual foi publicado.

Devido à simplicidade da implantação, o JSRP é geralmente mais adequado para ambientes de demonstração ou desenvolvimento de uma instância de publicação e uma instância de autor.

Consulte também [Características das Opções](working-with-srp.md#characteristics-of-srp-options) de SRP e [Topologias](topologies.md)recomendadas.

## Configuração {#configuration}

### Selecionar JSRP {#select-jsrp}

Por padrão, o JSRP é a opção de armazenamento para UGC.

O console [Configuração de](srp-config.md) armazenamento permite a seleção da configuração de armazenamento padrão, que identifica qual implementação do SRP usar.

No ambiente do autor, para acessar o console Configuração de armazenamento

* Da navegação global: **[!UICONTROL Ferramentas > Comunidades > Configuração de armazenamento]**

![chlimage_1-234](assets/chlimage_1-234.png)

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**
* Selecione **[!UICONTROL Enviar]**

### Publicar a configuração {#publishing-the-configuration}

Embora o JSRP seja a configuração padrão, para garantir que a configuração idêntica seja definida no ambiente de publicação:

* Autor:

   * Da navegação global: **[!UICONTROL Ferramentas > Implantação > Replicação]**
   * Selecionar **[!UICONTROL Ativar árvore]**
   * **[!UICONTROL Caminho de início]**:

      * Navegue até `/conf/global/settings/community/srpc/`
   * Selecionar **[!UICONTROL Ativar]**


## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, perfis *de* usuários e grupos *de* usuários, geralmente inseridos no ambiente de publicação, visite

* [Sincronização do usuário](sync.md)
* [Gerenciamento de usuários e grupos de usuários](users.md)

## Resolução de Problemas{#troubleshooting}

### UGC não visível no JCR {#ugc-not-visible-in-jcr}

Verifique se o JSRP foi configurado para ser o provedor padrão ao verificar a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é JSRP.

Em todas as instâncias do autor e publicação do AEM, reveja o console Configuração de armazenamento ou verifique o repositório do AEM:

* no JCR, if [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Não contém um nó [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) , significa que o provedor de armazenamento é JSRP
   * Se o nó srpc existir e contiver a configuração [padrão](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)do nó, as propriedades da configuração padrão deverão definir o JSRP como o provedor padrão

### UGC não visível na instância do autor {#ugc-not-visible-on-author-instance}

Isto não é um bug. Uma característica do JSRP é que o conteúdo da comunidade inserido no ambiente de publicação estará visível somente no ambiente de publicação.

### UGC não visível na instância de publicação {#ugc-not-visible-on-publish-instance}

Se uma única instância de publicação ou se um cluster de publicação estiver implantado, siga as instruções para [UGC não visível no JCR](#ugc-not-visible-in-jcr).

Se um farm de publicação for implantado, uma característica do JSRP é que o conteúdo da comunidade estará visível somente na instância de publicação na qual foi publicado.

Para que o UGC fique visível de qualquer instância de publicação, é necessário um cluster de publicação.
