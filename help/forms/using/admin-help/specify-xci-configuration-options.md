---
title: Especificar opções de configuração XCI
seo-title: Especificar opções de configuração XCI
description: Saiba como especificar opções de configuração XCI.
seo-description: Saiba como especificar opções de configuração XCI.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 1%

---


# Especificar opções de configuração XCI {#specify-xci-configuration-options}

A saída permite especificar um arquivo XCI personalizado que ele usa para renderização. (Consulte [Especificar locais de arquivos para Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) Por padrão, a Saída substitui algumas das opções especificadas no arquivo XCI, incluindo as seguintes:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Você pode selecionar opções que cancelam a substituição para as opções listadas acima, caso em que a Saída usa os valores especificados no arquivo XCI personalizado.

1. No console de administração, clique em Serviços > saída.
1. Marque ou desmarque a caixa de seleção Usar opções XCI padrão do sistema. Quando essa opção é selecionada, o Output usa seus valores padrão para as configurações de pacotes, criador, produtor e compressObjectStream. Quando essa opção é desmarcada, a Saída usa os valores especificados no arquivo XCI personalizado.
1. Clique em Salvar.

