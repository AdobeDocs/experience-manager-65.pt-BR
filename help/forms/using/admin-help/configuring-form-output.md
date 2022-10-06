---
title: Configuração da saída de formulário
seo-title: Configuring form output
description: Saiba como configurar a saída do formulário.
seo-description: Learn how to configure form output.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---

# Configuração da saída de formulário{#configuring-form-output}

## Especifique o tipo de saída de HTML retornado ao navegador da Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. No console de administração, clique em Serviços > formulários.
1. Em Saída de formulário, na lista Tipo de saída, selecione uma das seguintes opções:

   **HTML completo:** Para renderizar o formulário em tags HTML completas (uma página HTML completa). Esse é o valor padrão.

   **Corpo do formulário:** Para renderizar o formulário no `<BODY>` tags (não é uma HTML page completa).

1. Clique em Salvar.

## Especifique o local onde o conteúdo do PDF é renderizado {#specify-the-location-where-pdf-content-is-rendered}

1. Em Saída de formulário, na lista Renderizar em , selecione uma das seguintes opções:

   **Cliente:** Para renderizar PDF forms no Adobe Acrobat ou Adobe Reader. A renderização do lado do cliente melhora o desempenho de formulários de AEM e se aplica somente à transformação PDFForm.

   **Servidor:** Para renderizar PDF forms no servidor de aplicativos.

   **Automático:** Para renderizar o formulário PDF no local especificado pela variável `dynamicRender` valor de configuração do arquivo XDP. Esse é o valor padrão.

1. Clique em Salvar.

## Configuração da invocação de scripts personalizados antes do envio de formulário {#configuring-invocation-of-custom-scripts-before-form-submit}

Execute as seguintes etapas para ativar o recurso:

1. Faça logon no console de administração.
1. Ir para **Serviços** > **formulários**.
1. Especifique o Tipo de saída como Corpo do formulário.
1. Salve as configurações.
1. Declare uma variável JavaScript, __CUSTOM_SCRIPTS_VERSION, na seção head do código de HTML e defina seu valor como 1.

   >[!NOTE]
   >
   >*Para desativar o recurso, é possível remover a variável JavaScript ou definir seu valor como 0.*
