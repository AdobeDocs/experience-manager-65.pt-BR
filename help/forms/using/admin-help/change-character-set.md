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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 1%

---

# Alterar o conjunto de caracteres {#change-the-character-set}

Você pode especificar o conjunto de caracteres usado para codificar o fluxo de saída.

1. No console de administração, clique em **[!UICONTROL Serviços > saída]**.
1. Em Internacionalização, na lista Conjunto de caracteres, selecione um conjunto de caracteres. Essa configuração depende da configuração `TransformationFormat` e `PrintFormat` especificado por meio da API. Para especificar um conjunto de caracteres diferente dos listados, selecione Personalizado e especifique um valor de codificação na caixa exibida.

   Se `TransformationFormat` é PDF e PDF/A ou `PrintFormat` for PCL, PostScript, rótulo Zebra, IPL, DPL, TPCL, GenericColorPCL ou GenericPSLevel3, somente conjuntos de caracteres específicos serão suportados.

   O conjunto de caracteres deve ser um nome canônico válido. O valor padrão é ISO-8859-1.

1. Clique em **[!UICONTROL Salvar]**.
