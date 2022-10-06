---
title: Alterar o conjunto de caracteres
seo-title: Change the character set
description: Você pode especificar o conjunto de caracteres usado para codificar o fluxo de saída. Saiba como alterar o conjunto de caracteres.
seo-description: You can specify the character set used to encode the output stream. Learn how you can change the character set.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# Alterar o conjunto de caracteres {#change-the-character-set}

Você pode especificar o conjunto de caracteres usado para codificar o fluxo de saída.

1. No console de administração, clique em **[!UICONTROL Serviços > saída]**.
1. Em Internacionalização, na lista Conjunto de caracteres, selecione um conjunto de caracteres. Essa configuração depende do `TransformationFormat` e `PrintFormat` especificado por meio da API. Para especificar um conjunto de caracteres diferente daqueles listados, selecione Personalizado e especifique um valor de codificação na caixa exibida.

   If `TransformationFormat` é PDF e PDF/A ou `PrintFormat` é PCL, PostScript, rótulo Zebra, IPL, DPL, TPCL, GenericColorPCL ou GenericPSLevel3, somente conjuntos de caracteres específicos são suportados.

   O conjunto de caracteres deve ser um nome canônico válido. O valor padrão é ISO-8859-1.

1. Clique em **[!UICONTROL Salvar]**.
