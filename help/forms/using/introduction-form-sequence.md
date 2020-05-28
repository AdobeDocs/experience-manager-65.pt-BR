---
title: Introdução à sequência de formulários em várias etapas
seo-title: Introdução à sequência de formulários em várias etapas
description: Com o AEM Forms, é possível definir uma sequência de painéis de formulário na qual os usuários devem navegar e preencher um formulário adaptável.
seo-description: Com o AEM Forms, é possível definir uma sequência de painéis de formulário na qual os usuários devem navegar e preencher um formulário adaptável.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Introdução à sequência de formulários em várias etapas{#introduction-to-multi-step-form-sequence}

Formulários adaptáveis permitem que os autores de formulários criem uma experiência de captura de dados em várias etapas com grande facilidade. Ele é fornecido com suporte integrado para a criação de vários painéis e a associação de cada painel a diferentes padrões de navegação. Os autores de formulário podem agrupar campos de formulário em seções lógicas e representar um grupo como um painel. A navegação geral entre painéis é controlada usando o layout do painel. Os autores podem optar por organizar os painéis em diferentes layouts, por exemplo, colocando sequencialmente usando o layout Assistente ou de forma ad hoc usando o layout com guias. Para obter informações sobre layouts de painel, consulte Recursos de [layout de formulários](../../forms/using/layout-capabilities-adaptive-forms.md)adaptáveis.

Em uma experiência típica de preenchimento de formulário, há mais etapas envolvidas do que apenas capturar dados. Um envio de formulário completo pode incluir outras etapas, como assinar o formulário digitalmente, verificar as informações preenchidas no formulário, processar pagamentos e assim por diante. É diferente de caso a caso.

Se o caso de uso determinar um conjunto de etapas para a captura de dados ou se houver regulamentos que precisam de determinadas etapas a serem seguidas, o AEM Forms fornece uma forma de aplicar essa estrutura comum em todos os formulários. A implementação premeditada da estrutura do formulário define a sequência de etapas para um formulário. ![Exemplo de uma sequência de formulário em várias etapas](assets/formpipeline.png)

Exemplo de uma sequência de formulário em várias etapas

Caso seja necessário criar uma sequência para preencher, verificar, assinar e confirmar as etapas de um formulário, usaremos um caso de uso. As etapas para criar tal sequência são as seguintes:

1. Defina um modelo de formulário e adicione o painel necessário a ele. Observe que deve haver um painel para cada etapa da sequência. Entretanto, é possível incluir subpainéis dentro de um painel.

   Neste exemplo, podemos adicionar os seguintes painéis:

   * **Preencher**: Ele contém campos de formulários para capturar dados. Aqui, você pode incluir subpainéis aninhados para criar seções para diferentes tipos de informações, como pessoais, familiares, financeiras e assim por diante.

   * **Verificar**: Ele contém o componente **Verificar** que pode ser usado em um formulário adaptável baseado em XFA. Ele exibe as informações capturadas no painel Preencher no modo somente leitura para verificação.

   * **Assinar** eletronicamente: Ele contém o componente **Sign** que pode ser usado em um formulário adaptável baseado em XFA. ele fornece os seguintes serviços de assinatura:

      * Serviços eSign da Adobe Documento Cloud
      * Assinatura
   * **Confirmação**: Ele contém o componente **Resumo** que exibe uma mensagem confirmando o envio do formulário depois que um usuário assina o formulário e atinge a etapa Confirmação (Resumo) na sequência. Os autores podem configurar o texto do componente Resumo, mostrar uma mensagem de agradecimento, mostrar um link para o PDF gerado e assim por diante.


1. Selecione o layout do painel raiz como **[!UICONTROL Assistente]**.
1. Complete as etapas restantes para criar o modelo de formulário. Para obter mais informações, consulte [Criação de um modelo](../../forms/using/custom-adaptive-forms-templates.md)de formulário adaptável personalizado.

Depois de definir a sequência de formulários no modelo de formulário, é possível usá-la para criar formulários que terão a estrutura básica definida como a sequência no lugar, embora seja possível personalizar o formulário de acordo com seus requisitos.

