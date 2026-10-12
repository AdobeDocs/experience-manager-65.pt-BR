---
title: Configuração de opções de internacionalização
description: Saiba como especificar a localidade usada para renderizar formulários e como especificar o conjunto de caracteres usado para codificar o fluxo de saída.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
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
source-wordcount: '236'
ht-degree: 0%
---
# Configuração de opções de internacionalização{#setting-internationalization-options}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

## Especificar a localidade usada para renderizar formulários {#specify-the-locale-used-to-render-forms}

Você pode especificar a localidade usada ao renderizar um formulário do PDF. Os campos em um formulário do PDF usam o local especificado para exibir dados. Por exemplo, se o local estiver definido como Alemão, o formulário usará separadores decimais alemães para valores numéricos. O local também é usado para enviar mensagens de validação para dispositivos clientes, como navegadores da Web, como parte das transformações do HTML.

1. No console de administração, clique em Serviços > Forms.
1. Em Internacionalização, na lista Idioma, selecione o local usado para renderizar um formulário. O valor padrão é inglês (Estados Unidos).
1. Clique em Salvar.

## Especifique o conjunto de caracteres usado para codificar o fluxo de saída {#specify-the-character-set-used-to-encode-the-output-stream}

1. Em Internacionalização, na lista Conjunto de caracteres, selecione um conjunto de caracteres. Essa configuração depende da API usada, renderHTMLForm ou renderPDFForm. Para especificar um conjunto de caracteres diferente dos listados, selecione Personalizado e especifique um valor de codificação na caixa exibida.

   Para transformações de HTML, os formulários AEM são compatíveis com valores de codificação de caracteres definidos pelo pacote `java.nio.charset`. Se sFormPreference for PDFForm, somente conjuntos de caracteres específicos serão suportados. O conjunto de caracteres deve ser um nome canônico válido. O valor padrão é ISO-8859-1.

1. Clique em Salvar.
