---
title: Configuração de armazenamento
seo-title: Configuração de armazenamento
description: Como acessar o console de configuração de armazenamento
seo-description: Como acessar o console de configuração de armazenamento
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuração de armazenamento {#storage-configuration}

A configuração de armazenamento é o meio de identificar o armazenamento escolhido para o conteúdo da comunidade, também conhecido como conteúdo gerado pelo usuário (UGC).

Essa configuração informa o código AEM Communities sobre qual implementação do SRP (Storage Resource Provider [fornecedor de recursos de armazenamento]) deve ser usada ao acessar o UGC e deve refletir a topologia estabelecida quando o AEM foi implantado.

Para obter uma discussão sobre opções de armazenamento e topologias de implantação, visite

* [Armazenamento de conteúdo da comunidade](working-with-srp.md)
* [Topologias recomendadas](topologies.md)

## Console de configuração de armazenamento {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

No ambiente do autor, para acessar o console de configuração de armazenamento

* Da navegação global: **[!UICONTROL Ferramentas > Comunidades > Configuração de armazenamento]**

Para selecionar uma opção de armazenamento diferente do JCR padrão:

* selecionar uma opção
* Configurar apropriadamente

   * Consulte os detalhes para [selecionar MSRP](msrp.md#select-msrp)
   * Consulte os detalhes para [selecionar o DSRP](dsrp.md#select-dsrp)
   * Consulte os detalhes para [selecionar o ASRP](asrp.md#select-asrp)

* Selecione **[!UICONTROL Enviar]**

### Sobre o armazenamento JCR {#about-jcr-storage}

Observe que se nenhuma seleção for feita, o padrão será o repositório do AEM, JCR.

O JCR *não* é uma loja comum compartilhada pelos ambientes de autor e publicação. O conteúdo da comunidade estará visível somente do ambiente do autor ou publicação no qual foi criado.

Visite a [JCR Store](jsrp.md) para obter mais informações.

>[!NOTE]
>
>A ausência do nó `srpc`em `/etc/socialconfig` indica o armazenamento [padrão](jsrp.md)JCR.

