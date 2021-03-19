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
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---


# Introdução à sequência de formulário de várias etapas{#introduction-to-multi-step-form-sequence}

Formulários adaptáveis permitem que os autores de formulários criem uma experiência de captura de dados em várias etapas com grande facilidade. Ele é fornecido com suporte integrado para criar vários painéis e associar cada painel a diferentes padrões de navegação. Os Autores do formulário podem agrupar campos de formulário em seções lógicas e representar um grupo como um painel. A navegação geral entre painéis é controlada com o layout do painel. Os autores podem optar por organizar painéis em diferentes layouts, por exemplo, colocando sequencialmente usando o layout do Assistente ou de maneira ad hoc usando o layout de Tabelas. Para obter informações sobre layouts de painel, consulte [Recursos de layout de formulários adaptáveis](../../forms/using/layout-capabilities-adaptive-forms.md).

Em uma experiência típica de preenchimento de formulário, há mais etapas envolvidas do que apenas capturar dados. Um envio de formulário completo pode incluir outras etapas, como a assinatura digital do formulário, a verificação das informações preenchidas no formulário, o processamento de pagamentos e assim por diante. Difere de caso para caso.

Se o seu caso de uso determinar um conjunto de etapas para a captura de dados ou houver regulamentos que precisam de determinadas etapas a serem seguidas, a AEM Forms fornecerá uma maneira de aplicar essa estrutura comum em todos os formulários. A implementação premeditada da estrutura do formulário define a sequência de etapas para um formulário. ![Exemplo de uma sequência de formulário em várias etapas](assets/formpipeline.png)

Exemplo de uma sequência de formulário em várias etapas

Use um caso de uso em que é necessário criar uma sequência para preencher, verificar, assinar e confirmar as etapas de um formulário. As etapas para criar essa sequência são as seguintes:

1. Defina um modelo de formulário e adicione o painel necessário a ele. Observe que deve haver um painel para cada etapa na sequência. No entanto, é possível incluir subpainéis dentro de um painel.

   Neste exemplo, podemos adicionar os seguintes painéis:

   * **Preencha**: Ele contém campos de formulários para capturar dados. Aqui, você pode incluir subpainéis aninhados para criar seções para diferentes tipos de informações, como pessoais, familiares, financeiras e assim por diante.

   * **Verificar**: Ele contém o componente  **** Verificador que pode ser usado em um formulário adaptável baseado em XFA. Ele exibe as informações capturadas no painel Preenchimento no modo somente leitura para verificação.

   * **Assinatura** eletrônica: Ele contém o componente de  **** sinalização que pode ser usado em um formulário adaptável baseado em XFA. ela fornece os seguintes serviços de assinatura:

      * Serviços de eSign da Adobe Document Cloud
      * Assinatura
   * **Confirmação**: Ele contém o componente  **** Resumo que exibe uma mensagem confirmando o envio do formulário depois que um usuário assina o formulário e alcança a etapa Confirmação (Resumo) na sequência. Os autores podem configurar o texto do componente Resumo, mostrar uma mensagem de agradecimento, mostrar um link para o PDF gerado e assim por diante.


1. Selecione o layout do painel raiz como **[!UICONTROL Assistente]**.
1. Complete as etapas restantes para criar o template de formulário. Para obter mais informações, consulte [Criação de um modelo de formulário adaptável personalizado](../../forms/using/custom-adaptive-forms-templates.md).

Depois de definir a sequência de formulário no modelo de formulário, é possível usá-lo para criar formulários que terão a estrutura básica definida como a sequência em vigor, embora seja sempre possível personalizar o formulário para atender às suas necessidades.

