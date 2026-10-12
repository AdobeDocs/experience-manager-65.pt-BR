---
title: Adição de ação personalizada em itens de lista de formulários
description: Os desenvolvedores de formulários podem adicionar mais ações à listagem de formulários na página do portal de formulários. Por padrão, a listagem de formulários permite acessar o formulário, preenchê-lo e enviá-lo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
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
source-wordcount: '265'
ht-degree: 0%
---
# Adição de ação personalizada em itens de lista de formulários{#adding-custom-action-on-form-lister-items}

No AEM Forms, você pode criar uma página de portal listando os formulários disponíveis. Por padrão, você pode pesquisar e listar formulários em uma página do portal. É possível abrir formulários para preencher e enviar suas informações. Somente as ações de renderização são fornecidas prontamente para os formulários listados em uma página do portal. Para saber mais sobre as ações disponíveis em uma página de portal, consulte [Criando uma página de portal de formulários](../../forms/using/creating-form-portal-page.md).

Você pode adicionar outras opções à página do portal. Essas opções ou ações podem ser personalizadas personalizando o template do portal de formulários.

Este artigo mostra como criar um botão para enviar o link de um formulário, diretamente de uma página do portal de formulários. Esta personalização requer a atualização do modelo para o componente de Pesquisa e Lister.

O código necessário para adicionar a ação ao modelo está disponível abaixo. O atributo `onclick` no trecho de código tem um script para enviar um link de um formulário por email.

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

Você pode adicionar ações semelhantes em seu modelo personalizado. Para definir uma função JavaScript, adicione a função a um script de nível de página e vincule-a ao elemento de HTML necessário. No exemplo acima, a expressão `onclick` é a função vinculada.

Depois de fazer as edições no template, a página do portal de exemplo contém um botão para enviar o link do formulário por email, conforme mostrado abaixo.

![email](assets/email.png)
