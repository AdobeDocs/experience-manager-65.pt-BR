---
title: Configuração da saída de formulário
description: Saiba como configurar a saída de formulários. Para configurar a saída do formulário e habilitar o recurso, use os scripts personalizados antes de enviar o formulário.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Configuração da saída de formulário{#configuring-form-output}

## Especifique o tipo de saída de HTML retornado para o navegador da Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. No console de administração, clique em Serviços > Formulários.
1. Em Saída de formulário, na lista Tipo de saída, selecione uma das seguintes opções:

   **HTML completo:** para renderizar o formulário em marcas de HTML completo (uma página de HTML completa). Esse valor é o padrão.

   **Corpo do formulário:** Para renderizar o formulário em `<BODY>` marcas (não é uma página de HTML completa).

1. Clique em Salvar.

## Especificar o local onde o conteúdo do PDF é renderizado {#specify-the-location-where-pdf-content-is-rendered}

1. Em Saída de formulário, na lista Renderizar em, selecione uma das seguintes opções:

   **Cliente:** Para renderizar PDF forms no Adobe Acrobat ou Adobe Reader. A renderização do lado do cliente melhora o desempenho de formulários AEM e se aplica somente à transformação de PDForm.

   **Servidor:** Para renderizar PDF forms no servidor de aplicativos.

   **Auto:** Para renderizar o formulário PDF no local especificado pelo valor de configuração `dynamicRender` do arquivo XDP. Esse valor é o padrão.

1. Clique em Salvar.

## Configuração da invocação de scripts personalizados antes do envio do formulário {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Execute as seguintes etapas para ativar o recurso:

1. Faça logon no console de administração.
1. Vá para **Serviços** > **formulários**.
1. Especifique o Tipo de saída como Corpo do formulário.
1. Salve as configurações.
1. Declare uma variável JavaScript, __CUSTOM_SCRIPTS_VERSION, na seção de cabeçalho do código HTML e defina seu valor como 1.

   >[!NOTE]
   >
   >*Para desabilitar o recurso, você pode remover a variável JavaScript ou definir seu valor como 0.*
