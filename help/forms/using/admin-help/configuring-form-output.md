---
title: Configurar saída de formulário
seo-title: Configurar saída de formulário
description: Saiba como configurar a saída do formulário.
seo-description: Saiba como configurar a saída do formulário.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# Configurar saída de formulário{#configuring-form-output}

## Especifique o tipo de saída HTML retornado ao navegador da Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. No console de administração, clique em Serviços > formulários.
1. Em Saída de formulário, na lista Tipo de saída, selecione uma das seguintes opções:

   **HTML completo:** para renderizar o formulário com tags HTML completas (uma página HTML completa). Esse valor é o padrão.

   **Corpo do formulário:** Para renderizar o formulário dentro de  `<BODY>` tags (não uma página HTML completa).

1. Clique em Salvar.

## Especifique o local onde o conteúdo PDF é renderizado {#specify-the-location-where-pdf-content-is-rendered}

1. Em Saída de formulário, na Renderização na lista, selecione uma das seguintes opções:

   **Cliente:** para renderizar PDF forms no Adobe Acrobat ou Adobe Reader. A renderização no cliente melhora o desempenho de formulários AEM e se aplica somente à transformação PDFForm.

   **Servidor:** para renderizar PDF forms no servidor de aplicativos.

   **Automático:** para renderizar o formulário PDF no local especificado pelo valor de  `dynamicRender` configuração do arquivo XDP. Esse valor é o padrão.

1. Clique em Salvar.

## Configurar a invocação de scripts personalizados antes do envio de formulários {#configuring-invocation-of-custom-scripts-before-form-submit}

Execute as seguintes etapas para ativar o recurso:

1. Faça logon no console de administração.
1. Vá para **Serviços** > **formulários**.
1. Especifique o tipo de Saída como corpo do formulário.
1. Salve as configurações.
1. Declare uma variável JavaScript, __CUSTOM_SCRIPTS_VERSION, na seção head do código HTML e defina seu valor como 1.

   >[!NOTE]
   >
   >*Para desativar o recurso, você pode remover a variável JavaScript ou definir seu valor como 0.*

