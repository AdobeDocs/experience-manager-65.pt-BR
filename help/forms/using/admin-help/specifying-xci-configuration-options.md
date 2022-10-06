---
title: Especificação das opções de configuração XCI
seo-title: Specifying XCI configuration options
description: Saiba como especificar opções de configuração de XCI.
seo-description: Learn how to specify XCI configuration options.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# Especificação das opções de configuração XCI {#specifying-xci-configuration-options}

O Forms permite especificar um arquivo XCI personalizado que será usado para renderização. (Consulte [Configuração de localizações para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Por padrão, o Forms substitui algumas das opções especificadas no arquivo XCI, incluindo as seguintes:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Você pode selecionar opções que cancelam a substituição das opções listadas acima, nesse caso, o Forms usará os valores especificados no arquivo XCI personalizado.

1. No console de administração, clique em Serviços > Forms.
1. Marque ou desmarque a caixa de seleção Usar opções de XCI padrão do sistema . Quando essa opção é selecionada, o Forms usa os valores padrão para as configurações de pacotes, criador, produtor e compressObjectStream. Quando essa opção é desmarcada, o Forms usa os valores especificados no arquivo XCI personalizado.
1. Clique em Salvar.
