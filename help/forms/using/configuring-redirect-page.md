---
title: Configuração da página de redirecionamento
seo-title: Configuração da página de redirecionamento
description: Depois de preencher um formulário adaptável, os usuários podem ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
seo-description: Depois de preencher um formulário adaptável, os usuários podem ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Configuração da página de redirecionamento{#configuring-redirect-page}

Os autores de formulários podem configurar uma página para cada formulário, para a qual os usuários do formulário são redirecionados após o envio de um formulário.

1. No modo de edição, selecione um componente, clique em nível ![de](assets/field-level.png) campo > Contêiner **de formulário** adaptável e, em seguida, clique em ![cmppr](assets/cmppr.png).

1. Na barra lateral, clique em **Enviar**.

1. Forneça o URL da página de redirecionamento em Página de agradecimento na seção Envio.
1. Opcionalmente, em Enviar ação, para a ação de ponto de extremidade Enviar para REST, você pode configurar o parâmetro a ser passado para a página de redirecionamento.

![Redirecionar configuração da página](assets/thank-you-setting-1.png)

Redirecionar configuração da página

Os autores de formulários podem usar os seguintes parâmetros que são passados para a página de Agradecimentos. Para todas as ações de envio disponíveis, `status` e os `owner` parâmetros são enviados. Além desses dois parâmetros, alguns parâmetros adicionais são passados para as seguintes ações de envio:

* **Ação** de armazenamento de conteúdo (obsoleto): `contentPath`—o caminho do nó no repositório onde os dados enviados são armazenados é passado.

* **Ação** de armazenamento em PDF (obsoleto): `contentPath`—dos dados enviados e do caminho até o nó que armazena o arquivo PDF no repositório—é passado.

* **Enviar para fluxo de trabalho** do Forms: Parâmetros de saída retornados do fluxo de trabalho de formulários são enviados.

* **Enviar para o ponto de extremidade** REST: Parâmetros adicionados para mapeamento de parâmetro em campo são passados. `status` e `owner` os parâmetros não são passados nesta ação de envio. Para obter mais informações, consulte [Configuração da ação](../../forms/using/configuring-submit-actions.md)Enviar para o terminal REST.

