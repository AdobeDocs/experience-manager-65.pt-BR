---
title: Configuração de opções de internacionalização
seo-title: Configuração de opções de internacionalização
description: Saiba como especificar a localidade usada para renderizar formulários e como especificar o conjunto de caracteres usado para codificar o fluxo de saída.
seo-description: Saiba como especificar a localidade usada para renderizar formulários e como especificar o conjunto de caracteres usado para codificar o fluxo de saída.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# Definição de opções de internacionalização{#setting-internationalization-options}

## Especifique a localidade usada para renderizar formulários {#specify-the-locale-used-to-render-forms}

É possível especificar a localidade usada ao renderizar um formulário PDF. Os campos em um formulário PDF usam a localidade especificada para exibir dados. Por exemplo, se a localidade estiver definida como alemão, o formulário usará separadores decimais alemães para valores numéricos. A localidade também é usada para enviar mensagens de validação para dispositivos cliente, como navegadores da Web, como parte das transformações HTML.

1. No console de administração, clique em Serviços > Forms.
1. Em Internacionalização, na lista Idioma, selecione a localidade usada para renderizar um formulário. O valor padrão é inglês (Estados Unidos).
1. Clique em Salvar.

## Especifique o conjunto de caracteres usado para codificar o fluxo de saída {#specify-the-character-set-used-to-encode-the-output-stream}

1. Em Internacionalização, na lista Conjunto de caracteres, selecione um conjunto de caracteres. Essa configuração depende da API usada, renderizeHTMLForm ou renderizePDFForm. Para especificar um conjunto de caracteres diferente dos listados, selecione Personalizado e especifique um valor de codificação na caixa exibida.

   Para transformações HTML, AEM formulários oferecem suporte a valores de codificação de caracteres definidos pelo pacote `java.nio.charset`. Se sFormPreference for PDFForm, somente conjuntos de caracteres específicos serão suportados. O conjunto de caracteres deve ser um nome canônico válido. O valor padrão é ISO-8859-1.

1. Clique em Salvar.

