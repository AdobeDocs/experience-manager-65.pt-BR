---
title: Configuração da página de redirecionamento
description: Após preencher um formulário adaptável, os usuários podem ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: be1a774f-5681-443f-b195-28e89a020547
solution: Experience Manager, Experience Manager Forms
role: User, Developer
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
source-wordcount: '342'
ht-degree: 7%
---
# Configuração da página de redirecionamento{#configuring-redirect-page}

A Adobe <span class="preview"> recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html) |
| AEM 6.5 | Este artigo |

Os autores de formulários podem configurar uma página para cada formulário, para a qual os usuários são redirecionados após enviarem um formulário.

1. No modo de edição, selecione um componente e clique em ![nível do campo](assets/field-level.png) > **Contêiner de formulário adaptável** e clique em ![cmppr](assets/cmppr.png).

1. Na barra lateral, clique em **Envio**.

1. Forneça o URL da página de redirecionamento em Página de agradecimento na seção Envio.
1. Como opção, em Enviar ação, para a ação de endpoint Enviar para REST, é possível configurar o parâmetro a ser transmitido para a página de redirecionamento.

![Redirecionar configuração de página](assets/thank-you-setting-1.png)

Redirecionar configuração de página

Os autores de formulário podem usar os seguintes parâmetros que são passados para a página Thank you. Para todas as ações de envio disponíveis, `status` e `owner` parâmetros são passados. Além desses dois parâmetros, alguns parâmetros adicionais são transmitidos para as seguintes ações de envio:

* **Ação de conteúdo de repositório** (obsoleto): `contentPath`—o caminho do nó no repositório onde os dados enviados estão armazenados—é passado.

* **Ação de armazenamento do PDF** (desaprovada): `contentPath`—dos dados enviados e do caminho para o nó que armazena o arquivo PDF no repositório—é transmitido.

* **Enviar para fluxo de trabalho do Forms**: os parâmetros de saída retornados do fluxo de trabalho de formulários são passados.

* **Enviar para ponto de extremidade REST**: os parâmetros adicionados para o campo ao mapeamento de parâmetros são passados. Os parâmetros `status` e `owner` não são passados nesta ação de envio. Para obter mais informações, consulte [Configurando a ação de envio Enviar para ponto de extremidade REST](../../forms/using/configuring-submit-actions.md).
