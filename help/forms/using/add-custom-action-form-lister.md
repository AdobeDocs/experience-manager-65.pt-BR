---
title: Adicionar ação personalizada em itens do lister de formulários
seo-title: Adicionar ação personalizada em itens do lister de formulários
description: Os desenvolvedores de formulários podem adicionar mais ações à listagem de formulários na página do portal de formulários. Por padrão, a lista de formulários permite acessar o formulário, preenchê-lo e enviá-lo.
seo-description: Os desenvolvedores de formulários podem adicionar mais ações à listagem de formulários na página do portal de formulários. Por padrão, a lista de formulários permite acessar o formulário, preenchê-lo e enviá-lo.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Adicionar ação personalizada em itens do lister de formulários{#adding-custom-action-on-form-lister-items}

No AEM Forms, é possível criar uma página de portal que lista os formulários disponíveis. Por padrão, você pode pesquisar e lista formulários em uma página do portal. Você pode abrir formulários para preencher e enviar suas informações. Somente as ações de renderização são fornecidas prontamente para formulários listados em uma página do portal. Para saber mais sobre as ações disponíveis em uma página de portal, consulte [Criar uma página](../../forms/using/creating-form-portal-page.md)de portal de formulários.

É possível adicionar outras opções à página do portal. Essas opções ou ações podem ser personalizadas personalizando o modelo do portal de formulários.

Este artigo mostra como criar um botão para enviar o link de um formulário, diretamente de uma página do portal de formulários. Esta personalização requer a atualização do modelo para o componente de Pesquisa e Lister.

O código necessário para adicionar a ação ao modelo está disponível abaixo. O `onclick` atributo no trecho de código tem um script para enviar um link de um formulário por email.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

É possível adicionar ações semelhantes no modelo personalizado. Para definir uma função JavaScript, adicione a função em um script de nível de página e vincule-a ao elemento HTML necessário. No exemplo acima, a `onclick` expressão é a função vinculada.

Depois de fazer as edições no modelo, a página do portal de amostra contém um botão para enviar o link do formulário por email, como mostrado abaixo.

![email](assets/email.png)

