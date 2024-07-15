---
title: JSRP - Provedor de recurso de armazenamento JCR
description: O JSRP é mais adequado para ambientes de demonstração ou desenvolvimento de uma instância do Publish e uma instância do Author
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# JSRP - Provedor de recurso de armazenamento JCR {#jsrp-jcr-storage-resource-provider}

## Sobre o JSRP {#about-jsrp}

Quando o AEM Communities usa o JSRP como sua opção de armazenamento (o padrão), o conteúdo da comunidade é armazenado no JCR e o conteúdo gerado pelo usuário (UGC) pode ser acessado somente a partir da instância de autor ou publicação na qual foi postado.

Devido à simplicidade de implantação, o JSRP é mais adequado para ambientes de demonstração ou desenvolvimento de uma instância do Publish e uma instância do Author.

Consulte também [Características das Opções SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias Recomendadas](topologies.md).

## Configuração {#configuration}

### Selecionar JSRP {#select-jsrp}

Por padrão, JSRP é a opção de armazenamento para UGC.

O [console de Configuração de Armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação de SRP usar.

No ambiente de criação, para acessar o console de Configuração de armazenamento

* Da navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuração de Armazenamento]**

* Selecionar **[!UICONTROL Provedor de Recurso de Armazenamento JCR (JSRP)]**

* Selecionar **[!UICONTROL Enviar]**

![configuração-jsrp](assets/jsrp-configuration.png)

### Publicar a configuração {#publishing-the-configuration}

Embora o JSRP seja a configuração padrão, para garantir que a configuração idêntica seja definida no ambiente de publicação:

* Da navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**
* Selecione **[!UICONTROL Ativar Árvore]** > **[!UICONTROL Caminho Inicial]**:

   * Navegar até `/conf/global/settings/community/srpc/`

* Selecionar **[!UICONTROL Ativar]**

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuários* e *grupos de usuários*, inseridos com frequência no ambiente de publicação, visite:

* [Sincronização de usuário](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Resolução de problemas {#troubleshooting}

### UGC não visível no JCR {#ugc-not-visible-in-jcr}

Verifique se o JSRP foi configurado para ser o provedor padrão, verificando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é JSRP.

Em todas as instâncias do Author e do Publish AEM, revisite o console de Configuração de armazenamento ou verifique o repositório do AEM:

* No JCR, se [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Ele não contém um nó [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), as propriedades defaultconfiguration deverão definir JSRP como o provedor padrão.

### UGC não visível na instância do autor {#ugc-not-visible-on-author-instance}

Isso não é um erro. Uma característica do JSRP é que o conteúdo da comunidade inserido no ambiente de publicação só é visível no ambiente do Publish.

### UGC não visível na instância do Publish {#ugc-not-visible-on-publish-instance}

Se uma única instância do Publish ou se um cluster de publicação estiver implantado, siga as instruções para [UGC Não Visível no JCR](#ugc-not-visible-in-jcr).

Se um farm de publicação for implantado, uma característica do JSRP é que o conteúdo da comunidade só estará visível na instância do Publish na qual foi postado.

Para que o UGC seja visível de qualquer instância do Publish, é necessário um cluster de publicação.
