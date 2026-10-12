---
title: Definir a mensagem do dia
description: A mensagem do dia permite definir uma mensagem para ser exibida na página de Boas-vindas na interface do usuário do Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d8bab1c4-b830-4491-9486-d7e7f4dc2c99
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
source-wordcount: '186'
ht-degree: 0%
---
# Definir a mensagem do dia {#setting-the-message-of-the-day}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Você pode definir a exibição de uma mensagem na página de Boas-vindas da interface do Workspace.

Se necessário, você pode usar as tags HTML suportadas pelo Adobe Flash® Player para formatar a aparência do texto:

* &lt;a> Marca de âncora
* &lt;b> Tag em negrito
* &lt;br> Quebrar tag
* &lt;font> Marca de fonte
* &lt;img> Marca de imagem
* &lt;i> Marca em itálico
* &lt;li> Marca de item de lista
* &lt;p> Tag de parágrafo
* &lt;span> Marca de extensão
* &lt;textformat> Marca de formato de texto
* &lt;u> Marca de sublinhado

Para obter mais informações sobre as marcas com suporte, consulte a definição da propriedade `htmlText` para a classe TextField na [Referência de Idioma do Flex](https://flex.apache.org/).

## Definir a mensagem do dia {#set-the-message-of-the-day}

1. No console de administração, clique em Serviços > Workspace > Mensagem do dia.
1. Na caixa Mensagem do dia, forneça o texto a ser exibido na tela de boas-vindas.
1. Clique em Salvar.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão do AEM Forms.
