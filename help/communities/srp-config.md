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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '213'
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

Se nenhuma seleção for feita, o padrão será o repositório do AEM, JCR.

O JCR *não* é um armazenamento comum compartilhado pelos ambientes Autor e Publicação. O conteúdo da comunidade é visível somente no ambiente de Autor ou Publicação em que foi criado.

Visite a [Loja JCR](jsrp.md) para obter mais informações.

>[!NOTE]
>
>A ausência do nó `srpc` em `/etc/socialconfig` indica o [armazenamento JCR](jsrp.md) padrão.
