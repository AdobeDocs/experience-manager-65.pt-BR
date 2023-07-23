---
title: Configuração da página de redirecionamento
seo-title: Configuring redirect page
description: Após preencher um formulário adaptável, os usuários podem ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 5%

---

# Configuração da página de redirecionamento{#configuring-redirect-page}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html) |
| AEM 6.5 | Este artigo |

Os autores de formulários podem configurar uma página para cada formulário, para a qual os usuários são redirecionados após enviarem um formulário.

1. No modo de edição, selecione um componente e clique em ![nível de campo](assets/field-level.png) > **Contêiner de formulário adaptável** e clique em ![cmppr](assets/cmppr.png).

1. Na barra lateral, clique em **Envio**.

1. Forneça o URL da página de redirecionamento em Página de agradecimento na seção Envio.
1. Como opção, em Enviar ação, para a ação de endpoint Enviar para REST, é possível configurar o parâmetro a ser transmitido para a página de redirecionamento.

![Redirecionar configuração de página](assets/thank-you-setting-1.png)

Redirecionar configuração de página

Os autores de formulário podem usar os seguintes parâmetros que são passados para a página Thank you. Para todas as ações de envio disponíveis, `status` e `owner` parâmetros são transmitidos. Além desses dois parâmetros, alguns parâmetros adicionais são transmitidos para as seguintes ações de envio:

* **Ação de armazenamento de conteúdo** (obsoleto): `contentPath`— o caminho do nó no repositório onde os dados enviados estão armazenados — é transmitido.

* **Ação de PDF de armazenamento** (obsoleto): `contentPath`—dos dados enviados e do caminho para o nó que armazena o arquivo de PDF no repositório—é enviado.

* **Enviar para fluxo de trabalho do Forms**: os parâmetros de saída retornados do workflow de formulários são passados.

* **Enviar para endpoint REST**: os parâmetros adicionados para o mapeamento no campo para o parâmetro são transmitidos. `status` e `owner` Os parâmetros do não são transmitidos nesta ação de envio. Para obter mais informações, consulte [Configuração da ação de envio Enviar para endpoint REST](../../forms/using/configuring-submit-actions.md).
