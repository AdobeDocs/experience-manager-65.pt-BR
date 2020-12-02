---
title: Especificação de opções de configuração XCI
seo-title: Especificação de opções de configuração XCI
description: Saiba como especificar opções de configuração XCI.
seo-description: Saiba como especificar opções de configuração XCI.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---


# Especificação de opções de configuração XCI {#specifying-xci-configuration-options}

O Forms permite que você especifique um arquivo XCI personalizado que ele usará para renderização. (Consulte [Configuração de locais para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Por padrão, a Forms substitui algumas das opções especificadas no arquivo XCI, incluindo as seguintes:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Você pode selecionar opções que cancelam a substituição para as opções listadas acima, caso em que a Forms usará os valores especificados no arquivo XCI personalizado.

1. No console de administração, clique em Serviços > Forms.
1. Marque ou desmarque a caixa de seleção Usar opções XCI padrão do sistema. Quando essa opção é selecionada, a Forms usa seus valores padrão para as configurações de pacotes, criador, produtor e compressObjectStream. Quando essa opção é desmarcada, a Forms usa os valores especificados no arquivo XCI personalizado.
1. Clique em Salvar.

