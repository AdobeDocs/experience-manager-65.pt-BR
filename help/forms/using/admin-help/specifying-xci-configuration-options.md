---
title: Especificação das opções de configuração XCI
description: Saiba como especificar as opções de configuração de XCI. Você pode especificar valores personalizados de arquivos XCI para o Formulário adaptável, de modo que ele possa ser usado durante a renderização do formulário.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '149'
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
