---
title: Introdução à sequência de formulários em várias etapas
description: Com o AEM Forms, você pode definir uma sequência de painéis de formulário em que deseja que os usuários naveguem e preencham um formulário adaptável.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 26%

---

# Introdução à sequência de formulários em várias etapas{#introduction-to-multi-step-form-sequence}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve uma abordagem mais antiga para a criação do Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | Este artigo |


Os formulários adaptáveis permitem que os autores de formulários criem uma experiência de captura de dados em várias etapas com grande facilidade. Eles possuem suporte integrado para criar vários painéis e associar cada painel a diferentes padrões de navegação. Os autores do formulário podem agrupar campos de formulário em seções lógicas e representar um grupo como um painel. A navegação geral entre painéis é controlada com o layout do painel. Os autores podem optar por organizar painéis em diferentes layouts, por exemplo, colocando sequencialmente usando o layout Assistente ou de maneira ad-hoc usando o layout com guias. Para obter informações sobre layouts de painel, consulte [Recursos de layout de formulários adaptáveis](../../forms/using/layout-capabilities-adaptive-forms.md).

Em uma experiência típica de preenchimento de formulário, há mais etapas envolvidas do que apenas capturar dados. O envio completo de um formulário pode incluir outras etapas, como assinar o formulário digitalmente, verificar as informações preenchidas no formulário e processar os pagamentos. Há diferenças de caso para caso.

Se seu caso de uso exigir um conjunto de etapas para a captura de dados ou se houver regulamentos que precisem de determinadas etapas a serem seguidas, o AEM Forms fornece uma maneira de aplicar essa estrutura comum em todos os formulários. A implementação premeditada de uma estrutura de formulário define a sequência de etapas de um formulário. ![Exemplo de uma sequência de formulário em várias etapas](assets/formpipeline.png)

Exemplo de uma sequência de formulário em várias etapas

Considere um caso de uso em que você precisa criar uma sequência para etapas de preenchimento, verificação, assinatura e confirmação de um formulário. Para criar essa sequência, siga estas etapas:

1. Defina um modelo de formulário e adicione o painel necessário a ele. Deve haver um painel para cada etapa na sequência. No entanto, é possível incluir subpainéis dentro de um painel.

   Neste exemplo, os seguintes painéis podem ser adicionados:

   * **Preenchimento**: contém campos de formulários para capturar dados. Aqui, você pode incluir subpainéis aninhados para criar seções para diferentes tipos de informações, como pessoal, familiar e financeira.

   * **Verificar**: contém o **Verificar** que pode ser usado em um formulário adaptável baseado em XFA. Ele exibe as informações capturadas no painel Preenchimento no modo somente leitura para verificação.

   * **Assinatura eletrônica**: contém o **Sign** que pode ser usado em um formulário adaptável baseado em XFA. ele fornece os seguintes serviços de assinatura:

      * Serviços de assinatura eletrônica da Adobe Document Cloud
      * Assinatura escrita

   * **Confirmação**: contém o componente **Resumo** que exibe uma mensagem confirmando o envio do formulário depois que um usuário o assina e atinge a etapa de Confirmação (Resumo) da sequência. Os autores podem configurar o texto do componente Resumo, mostrar uma mensagem de agradecimento, mostrar um link para o PDF gerado e assim por diante.

1. Selecione o layout do painel raiz como **[!UICONTROL Assistente]**.
1. Complete as etapas restantes para criar o modelo de formulário. Consulte [Criação de um modelo de formulário adaptável personalizado](../../forms/using/custom-adaptive-forms-templates.md).

Depois de definir a sequência de formulários no modelo de formulário, você pode usá-la para criar formulários que tenham a estrutura básica definida como a sequência no lugar. Você sempre pode personalizar o formulário para atender aos seus requisitos.
