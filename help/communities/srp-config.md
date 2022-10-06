---
title: Configuração de armazenamento
seo-title: Storage Configuration
description: Como acessar o Console de Configuração de Armazenamento
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 4%

---

# Configuração de armazenamento {#storage-configuration}

A configuração de armazenamento é o meio de identificar o armazenamento escolhido para o conteúdo da comunidade, também conhecido como conteúdo gerado pelo usuário (UGC).

Essa configuração informa o código AEM Communities sobre qual implementação do SRP (Storage Resource Provider, provedor de recursos de armazenamento) deve ser usada ao acessar o UGC e deve refletir a topologia estabelecida quando o AEM foi implantado.

Para uma discussão sobre opções de armazenamento e topologias de implantação, visite:

* [Armazenamento de conteúdo da comunidade](working-with-srp.md)
* [Topologias recomendadas](topologies.md)

## Console de configuração de armazenamento {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

No ambiente de criação, para acessar o console de configuração de armazenamento.

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuração de armazenamento]**

Para selecionar uma opção de armazenamento diferente do JCR padrão:

* Selecionar uma opção
* Configurar adequadamente

   * Veja detalhes para [selecionando o MSRP](msrp.md#select-msrp)
   * Veja detalhes para [selecionando DSRP](dsrp.md#select-dsrp)
   * Veja detalhes para [selecionando ASRP](asrp.md#select-asrp)

* Selecione **[!UICONTROL Enviar]**.

### Sobre o armazenamento JCR {#about-jcr-storage}

Esteja ciente de que se nenhuma seleção for feita, o padrão será o repositório AEM, o JCR.

JCR é *not* uma loja comum compartilhada pelos ambientes de criação e publicação. O conteúdo da comunidade será visível somente no ambiente de criação ou publicação em que foi criado.

Visita [Loja JCR](jsrp.md) para obter mais informações.

>[!NOTE]
>
>A ausência do nó `srpc` under `/etc/socialconfig` indica o padrão [Loja JCR](jsrp.md).
