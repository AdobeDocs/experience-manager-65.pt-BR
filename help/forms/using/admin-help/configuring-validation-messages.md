---
title: Configurar mensagens de validação
description: Saiba como especificar como as mensagens de validação são exibidas e sua localização relativa ao formulário retornado no navegador da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 14314383-5228-4904-98c1-586f48a1142c
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
source-wordcount: '364'
ht-degree: 1%
---
# Configurar mensagens de validação {#configuring-validation-messages}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Para formulários renderizados como HTML, os erros de validação de formulário que ocorrem são exibidos para o usuário. Você pode personalizar como as mensagens de validação são exibidas. Dependendo de onde as mensagens de validação forem exibidas, você também poderá controlar o local da mensagem no formulário e o tamanho da borda do quadro.

## Especificar como as mensagens de validação são exibidas {#specify-how-validation-messages-are-displayed}

1. No console de administração, clique em Serviços > Formulários.
1. Em Saída de Validação, na lista Relatório, selecione uma das seguintes opções:

   **Caixa de mensagem:** para exibir mensagens de validação em uma caixa de diálogo separada.

   **Quadro:** Para exibir mensagens de validação em um quadro da mesma janela.

   **Sem Quadro:** Para exibir mensagens de validação na mesma janela. Esse valor é o padrão.

   **Via API (com dados):** Para retornar as mensagens de validação pela API (com dados). As mensagens de validação não são exibidas na tela.

   **Via API (com formulário):** Para retornar as mensagens de validação por meio da API (com o formulário). As mensagens de validação não são exibidas na tela.

   **Nenhum:** Para não exibir mensagens de validação.

1. Clique em Salvar.

## Especifique o local das mensagens de validação relativas ao formulário retornado no navegador da Web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Quando Relatórios estiver definido como Quadro ou Sem Quadro, você poderá especificar o local das mensagens de validação.

1. Em Saída de Validação, na lista Posição, selecione uma das seguintes opções:

   **Esquerda:** Para exibir mensagens de validação no lado esquerdo do navegador da Web.

   **Direito:** para exibir mensagens de validação no lado direito do navegador da Web.

   **Superior**: para exibir mensagens de validação na parte superior do navegador da Web. Esse valor é o padrão.

   **Parte Inferior**: para exibir mensagens de validação na parte inferior do navegador da Web.

1. Clique em Salvar.

## Especificar o tamanho da borda do quadro {#specify-the-frame-border-size}

Quando a opção Relatório está definida como Quadro, é possível especificar o tamanho da borda do quadro.

1. Em Saída de validação, na caixa Tamanho da Borda, digite o tamanho da borda do quadro, em pixels.

   O tamanho da borda deve ser igual ou maior que 0. O valor padrão é 1.

1. Clique em Salvar.
