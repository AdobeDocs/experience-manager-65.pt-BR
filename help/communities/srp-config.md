---
title: Configuração de armazenamento
description: Saiba mais sobre o console Configuração de armazenamento como um meio de identificar o armazenamento escolhido para o conteúdo da comunidade, também conhecido como conteúdo gerado pelo usuário.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 4%

---

# Configuração de armazenamento {#storage-configuration}

A configuração de armazenamento é o meio de identificar o armazenamento escolhido para o conteúdo da comunidade, também conhecido como conteúdo gerado pelo usuário (UGC).

Essa configuração informa o código AEM Communities sobre qual implementação do SRP (provedor de recursos de armazenamento) é usada ao acessar o UGC. Deve refletir a topologia estabelecida quando o Adobe Experience Manager (AEM) foi implantado.

Para uma discussão sobre opções de armazenamento e topologias de implantação, visite:

* [Armazenamento de conteúdo da comunidade](working-with-srp.md)
* [Topologias recomendadas](topologies.md)

## Console de configuração de armazenamento {#storage-configuration-console}

![configuração-jsrp](assets/jsrp-configuration.png)

No ambiente do Author, para acessar o console de configuração de armazenamento.

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuração de Armazenamento]**

Para selecionar uma opção de armazenamento diferente do JCR padrão:

* Selecione uma opção
* Configurar adequadamente

   * Veja detalhes para [selecionar MSRP](msrp.md#select-msrp)
   * Veja detalhes para [selecionar DSRP](dsrp.md#select-dsrp)
   * Veja detalhes para [selecionar ASRP](asrp.md#select-asrp)

* Selecione **[!UICONTROL Enviar]**.

### Sobre o armazenamento JCR {#about-jcr-storage}

Se nenhuma seleção for feita, o padrão será o repositório AEM, JCR.

O JCR *não* é um armazenamento comum compartilhado pelos ambientes do Autor e do Publish. O conteúdo da comunidade é visível somente no ambiente Autor ou Publish em que foi criado.

Visite a [Loja JCR](jsrp.md) para obter mais informações.

>[!NOTE]
>
>A ausência do nó `srpc` em `/etc/socialconfig` indica o [armazenamento JCR](jsrp.md) padrão.
