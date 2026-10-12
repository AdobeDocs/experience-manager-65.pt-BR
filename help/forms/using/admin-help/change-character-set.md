---
title: Alterar o conjunto de caracteres
description: Você pode especificar o conjunto de caracteres usado para codificar o fluxo de saída. Saiba como alterar o conjunto de caracteres.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
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
source-wordcount: '144'
ht-degree: 1%
---
# Alterar o conjunto de caracteres {#change-the-character-set}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Você pode especificar o conjunto de caracteres usado para codificar o fluxo de saída.

1. No console de administração, clique em **[!UICONTROL Serviços > saída]**.
1. Em Internacionalização, na lista Conjunto de caracteres, selecione um conjunto de caracteres. Esta configuração depende do `TransformationFormat` e do `PrintFormat` especificados por meio da API. Para especificar um conjunto de caracteres diferente dos listados, selecione Personalizado e especifique um valor de codificação na caixa exibida.

   Se `TransformationFormat` for PDF e PDF/A ou `PrintFormat` for PCL, PostScript, Rótulo Zebra, IPL, DPL, TPCL, GenericColorPCL ou GenericPSLevel3, somente conjuntos de caracteres específicos serão suportados.

   O conjunto de caracteres deve ser um nome canônico válido. O valor padrão é ISO-8859-1.

1. Clique em **[!UICONTROL Salvar]**.
