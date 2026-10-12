---
title: Especificação das opções de configuração XCI
description: Saiba como especificar as opções de configuração de XCI. Você pode especificar valores personalizados de arquivos XCI para o Formulário adaptável, de modo que ele possa ser usado durante a renderização do formulário.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%
---
# Especificação das opções de configuração XCI {#specifying-xci-configuration-options}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

O Forms permite especificar um arquivo XCI personalizado que pode ser usado para renderização. (Consulte [Configuração de locais para o Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Por padrão, o Forms substitui algumas das opções especificadas no arquivo XCI, incluindo o seguinte:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Você pode selecionar opções que cancelam a substituição das opções listadas acima, nesse caso, o Forms usa os valores especificados no arquivo XCI personalizado.

1. No console de administração, clique em **Serviços** > **Forms**.
1. Marque ou desmarque a caixa de seleção Usar opções XCI padrão do sistema. Quando essa opção é selecionada, o Forms usa seus valores padrão para as configurações packets, creator, producer e compressObjectStream. Quando essa opção é desmarcada, o Forms usa os valores especificados no arquivo XCI personalizado.
1. Clique em **Salvar**.
