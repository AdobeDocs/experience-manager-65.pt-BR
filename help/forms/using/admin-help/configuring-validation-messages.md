---
title: Configuração de mensagens de validação
seo-title: Configuração de mensagens de validação
description: Saiba como especificar como as mensagens de validação são exibidas e seu local relativo ao formulário retornado no navegador da Web.
seo-description: Saiba como especificar como as mensagens de validação são exibidas e seu local relativo ao formulário retornado no navegador da Web.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---


# Configurando mensagens de validação {#configuring-validation-messages}

Para formulários renderizados como HTML, os erros de validação de formulário que ocorrem são exibidos para o usuário. Você pode personalizar como as mensagens de validação são exibidas. Dependendo de onde as mensagens de validação são exibidas, também é possível controlar o local da mensagem no formulário e o tamanho da borda do quadro.

## Especificar como as mensagens de validação são exibidas {#specify-how-validation-messages-are-displayed}

1. No console de administração, clique em Serviços > formulários.
1. Em Saída de validação, na lista do Relatórios, selecione uma das seguintes opções:

   **Caixa de mensagem:** Para exibir mensagens de validação em uma caixa de diálogo separada.

   **Quadro:** Para exibir mensagens de validação em um quadro da mesma janela.

   **Sem quadro:** Para exibir mensagens de validação na mesma janela. Esse valor é o padrão.

   **Por meio da API (com dados):** Para retornar as mensagens de validação por meio da API (com dados). As mensagens de validação não são exibidas na tela.

   **Por meio da API (com formulário):** Para retornar as mensagens de validação por meio da API (com o formulário). As mensagens de validação não são exibidas na tela.

   **Nenhum:** Para não exibir mensagens de validação.

1. Clique em Salvar.

## Especifique o local das mensagens de validação relativas ao formulário retornado no navegador da Web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Quando o Relatórios é definido como Quadro ou Sem quadro, você pode especificar o local das mensagens de validação.

1. Em Saída de validação, na lista Posição, selecione uma das seguintes opções:

   **Esquerda:** Para exibir mensagens de validação no lado esquerdo do navegador da Web.

   **Direita:** para exibir mensagens de validação no lado direito do navegador da Web.

   **Parte superior**: Para exibir mensagens de validação na parte superior do navegador da Web. Esse valor é o padrão.

   **Parte inferior**: Para exibir mensagens de validação na parte inferior do navegador da Web.

1. Clique em Salvar.

## Especificar o tamanho da borda do quadro {#specify-the-frame-border-size}

Quando o Relatórios é definido como Quadro, você pode especificar o tamanho da borda do quadro.

1. Em Saída de validação, na caixa Tamanho da borda, digite o tamanho da borda do quadro, em pixels.

   O tamanho da borda deve ser igual ou maior que 0. O valor padrão é 1.

1. Clique em Salvar.

