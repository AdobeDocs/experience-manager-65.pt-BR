---
title: Definição de opções de internacionalização
seo-title: Setting internationalization options
description: Saiba como especificar o local usado para renderizar formulários e como especificar o conjunto de caracteres usado para codificar o fluxo de saída.
seo-description: Learn how to specify the locale used to render forms and how to specify the character set used to encode the output stream.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 1%

---

# Definição de opções de internacionalização{#setting-internationalization-options}

## Especificar a localidade usada para renderizar formulários {#specify-the-locale-used-to-render-forms}

Você pode especificar o local usado ao renderizar um formulário PDF. Os campos em um formulário PDF usam a localidade especificada para exibir dados. Por exemplo, se a localidade estiver definida como alemão, o formulário usará separadores decimais alemães para valores numéricos. A localidade também é usada para enviar mensagens de validação para dispositivos clientes, como navegadores da Web, como parte das transformações de HTML.

1. No console de administração, clique em Serviços > Forms.
1. Em Internacionalização, na lista Idioma, selecione o local usado para renderizar um formulário. O valor padrão é inglês (Estados Unidos).
1. Clique em Salvar.

## Especifique o conjunto de caracteres usado para codificar o fluxo de saída {#specify-the-character-set-used-to-encode-the-output-stream}

1. Em Internacionalização, na lista Conjunto de caracteres, selecione um conjunto de caracteres. Essa configuração depende da API usada, seja renderHTMLForm ou renderPDFForm. Para especificar um conjunto de caracteres diferente daqueles listados, selecione Personalizado e especifique um valor de codificação na caixa exibida.

   Para transformações de HTML, os formulários AEM oferecem suporte para valores de codificação de caracteres definidos pela variável `java.nio.charset` pacote. Se sFormPreference for PDFForm, somente conjuntos de caracteres específicos serão suportados. O conjunto de caracteres deve ser um nome canônico válido. O valor padrão é ISO-8859-1.

1. Clique em Salvar.
