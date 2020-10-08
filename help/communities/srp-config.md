---
title: Configuração de armazenamento
seo-title: Configuração de armazenamento
description: Como acessar o console de configuração do Armazenamento
seo-description: Como acessar o console de configuração do Armazenamento
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---


# Configuração de armazenamento {#storage-configuration}

A configuração do armazenamento é o meio de identificar o armazenamento escolhido para o conteúdo da comunidade, também conhecido como conteúdo gerado pelo usuário (UGC).

Essa configuração informa o código da AEM Communities sobre qual implementação do SRP (armazenamento resource provider, Provedor de recursos do servidor) deve ser usada ao acessar o UGC e deve refletir a topologia estabelecida quando o AEM foi implantado.

Para obter uma discussão sobre opções de armazenamento e topologias de implantação, visite:

* [Armazenamento de conteúdo da comunidade](working-with-srp.md)
* [Topologias recomendadas](topologies.md)

## Console de configuração do armazenamento {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

No ambiente do autor, para acessar o console de configuração do armazenamento.

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > Configuração do **[!UICONTROL Armazenamento]**

Para selecionar uma opção de armazenamento diferente do JCR padrão:

* Selecionar uma opção
* Configurar apropriadamente

   * Consulte os detalhes para [selecionar MSRP](msrp.md#select-msrp)
   * Consulte os detalhes para [selecionar o DSRP](dsrp.md#select-dsrp)
   * Consulte os detalhes para [selecionar o ASRP](asrp.md#select-asrp)

* Selecione **[!UICONTROL Enviar]**.

### Sobre o Armazenamento JCR {#about-jcr-storage}

Observe que se nenhuma seleção for feita, o padrão será o repositório AEM, JCR.

O JCR *não* é uma loja comum compartilhada pelos ambientes de autor e publicação. O conteúdo da comunidade estará visível somente do ambiente do autor ou publicação no qual foi criado.

Visite a [JCR Store](jsrp.md) para obter mais informações.

>[!NOTE]
>
>A ausência do nó `srpc` em `/etc/socialconfig` indica o armazenamento [padrão](jsrp.md)JCR.
