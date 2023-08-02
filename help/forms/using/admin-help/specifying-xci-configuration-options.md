---
title: Especificação das opções de configuração XCI
description: Saiba como especificar opções de configuração XCI.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# Especificação das opções de configuração XCI {#specifying-xci-configuration-options}

O Forms permite especificar um arquivo XCI personalizado que pode ser usado para renderização. (Consulte [Configuração de locais para o Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Por padrão, o Forms substitui algumas das opções especificadas no arquivo XCI, incluindo o seguinte:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Você pode selecionar opções que cancelam a substituição das opções listadas acima, nesse caso, o Forms usa os valores especificados no arquivo XCI personalizado.

1. No console de administração, clique em **Serviços** > **Forms**.
1. Marque ou desmarque a caixa de seleção Usar opções XCI padrão do sistema. Quando essa opção é selecionada, o Forms usa seus valores padrão para as configurações packets, creator, producer e compressObjectStream. Quando essa opção é desmarcada, o Forms usa os valores especificados no arquivo XCI personalizado.
1. Clique em **Salvar**.
