---
title: Configurar mensagens de validação
description: Saiba como especificar como as mensagens de validação são exibidas e sua localização relativa ao formulário retornado no navegador da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Configurar mensagens de validação {#configuring-validation-messages}

Para formulários renderizados como HTML, os erros de validação de formulário que ocorrem são exibidos para o usuário. Você pode personalizar como as mensagens de validação são exibidas. Dependendo de onde as mensagens de validação forem exibidas, você também poderá controlar o local da mensagem no formulário e o tamanho da borda do quadro.

## Especificar como as mensagens de validação são exibidas {#specify-how-validation-messages-are-displayed}

1. No console de administração, clique em Serviços > Formulários.
1. Em Saída de Validação, na lista Relatório, selecione uma das seguintes opções:

   **Caixa de mensagem:** Para exibir mensagens de validação em uma caixa de diálogo separada.

   **Quadro:** Para exibir mensagens de validação em um quadro da mesma janela.

   **Sem quadro:** Para exibir mensagens de validação na mesma janela. Esse valor é o padrão.

   **Pela API (com dados):** Para retornar as mensagens de validação por meio da API (com dados). As mensagens de validação não são exibidas na tela.

   **Pela API (com formulário):** Para retornar as mensagens de validação por meio da API (com o formulário ). As mensagens de validação não são exibidas na tela.

   **Nenhum:** Para não exibir mensagens de validação.

1. Clique em Salvar.

## Especifique o local das mensagens de validação relativas ao formulário retornado no navegador da Web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Quando Relatórios estiver definido como Quadro ou Sem Quadro, você poderá especificar o local das mensagens de validação.

1. Em Saída de Validação, na lista Posição, selecione uma das seguintes opções:

   **Esquerda:** Para exibir mensagens de validação no lado esquerdo do navegador da Web.

   **Direita:** Para exibir mensagens de validação no lado direito do navegador da Web.

   **Topo**: Para exibir mensagens de validação na parte superior do navegador da Web. Esse valor é o padrão.

   **Inferior**: Para exibir mensagens de validação na parte inferior do navegador da Web.

1. Clique em Salvar.

## Especificar o tamanho da borda do quadro {#specify-the-frame-border-size}

Quando a opção Relatório está definida como Quadro, é possível especificar o tamanho da borda do quadro.

1. Em Saída de validação, na caixa Tamanho da Borda, digite o tamanho da borda do quadro, em pixels.

   O tamanho da borda deve ser igual ou maior que 0. O valor padrão é 1.

1. Clique em Salvar.
