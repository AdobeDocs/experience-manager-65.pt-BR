---
title: Assistente de IA no AEM
description: Use o Assistente de IA para ajudar você a encontrar respostas e solucionar problemas das soluções disponíveis no Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
source-git-commit: 78ba3c9a8c2636eebdeac08c54ad3d0b1d0e8249
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 1%

---

# Assistente de IA no AEM {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>Os clientes do AEM 6.5 e do AEM 6.5 LTS que não usam o Cloud Manager/Experience Hub devem entrar em contato com o engenheiro de sucesso do cliente da Adobe para solicitar acesso ao Assistente de IA.


O Assistente de IA no AEM 6.5/AEM 6.5 LTS oferece uma interface conversacional projetada para simplificar a busca de respostas para suas dúvidas relacionadas ao Adobe Experience Manager. Ele ajuda você a obter respostas instantâneas para suas perguntas sobre produtos da AEM (*disponíveis para todos os usuários*) e a automatizar a criação de tíquetes de suporte (*disponíveis para Administradores de Suporte*).

O Assistente de IA é compatível com o AEM as a Cloud Service, incluindo as seguintes soluções:

* Página de visão geral do Experience Hub
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


Ele é diretamente incorporado ao AEM e acessível no AEM Experience Hub, Cloud Manager e na interface do usuário do autor.

O vídeo de 39 segundos a seguir, com duração de 3 minutos, fornece uma apresentação passo a passo do Assistente de IA no AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3470354?learn=on)

## Obter acesso ao Assistente de IA no AEM{#get-access}

Para conceder aos usuários acesso ao Assistente de IA no AEM, o Administrador do Adobe deve configurar as seguintes permissões personalizadas para os perfis que exigem acesso no **Adobe Admin Console**:

* **Acesso ao Assistente de IA** - Permissão para usar o Assistente de IA no AEM para obter conhecimento sobre o produto, permitindo que os usuários façam perguntas relacionadas ao produto no chat do Assistente de IA. Essa permissão deve ser ativada.
* **Acesso ao suporte** - Os usuários também devem ter permissão para abrir tíquetes de suporte, o que requer a função de **Administrador de Suporte**.

As solicitações do Assistente de IA no AEM são autenticadas por meio do Adobe Identity Management Services (IMS). Para obter detalhes, consulte a [visão geral dos Serviços Identity Management da Adobe](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf).

**Para obter acesso ao Assistente de IA no AEM:**

1. Os clientes devem ter um contrato adicional em vigor para acessar a maioria dos recursos de IA e agentes no Adobe Experience Manager. Entre em contato com seu representante da Adobe para obter mais detalhes.

<!-- OLD STEP 1 [Customers must sign the Gen AI rider with Adobe](https://fieldreadiness-adobe.highspot.com/items/665f831c9f831b011aeda057#1). 

    The GenAI Rider is a legal agreement between a customer and Adobe, required to use most AI and agentic capabilities. Contact Adobe Customer Care to learn more. -->

1. O administrador do AEM configura o Assistente de IA para uso em sua organização. Consulte [Configurar o Assistente de IA no AEM](/help/ai-assistant-in-aem-admin.md).

<!--
>[!IMPORTANT]
>Be sure you have reviewed and submitted the user agreement so Adobe can enable the AI Assistant feature for you to test out and participate in the private beta program.
>
>For any questions, send an email to [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) from your email address associated with your Adobe ID. -->

## Escopo {#scope}

O escopo atual do Assistente de IA no AEM se concentra em abordar questões de conhecimento do produto para o AEMr. as a Cloud Service. Esse escopo inclui suporte abrangente para áreas importantes. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **Superfícies**: disponível no AEM Experience Hub, IU do autor, Cloud Manager.
* **Recursos**: conhecimento sobre produtos e primeira parada para solução de problemas e orientação, criação automática de tíquetes de suporte e pesquisa.
* **Valor**: economiza tempo, acelera o aprendizado e o tempo de retorno, reduz a necessidade de criar tíquetes de suporte manualmente e melhora a eficiência na criação de tíquetes de suporte.

## Privacidade, segurança e governança{#privacy-security-governance}

O Assistente de IA do AEM foi projetado com forte ênfase em privacidade, segurança e governança.

Este artigo descreve os recursos centralizados na confiança que você pode esperar do Assistente de IA no AEM:

* Nenhum dado pessoal é usado pelo Assistente de IA no AEM, inclusive para fins de treinamento.
* O Assistente de IA no AEM não tem acesso aos dados do consumidor.
* A permissão explícita é necessária para interagir com o Assistente de IA no AEM.
* Os prompts fornecidos pelo usuário (perguntas, consultas e assim por diante) não são compartilhados com outros clientes.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Conheça o Assistente de IA no AEM para obter conhecimento sobre produtos e criação automatizada de tíquetes de suporte {#ai-prod-insights}

O conhecimento do produto abrange conceitos e tópicos derivados da documentação da Adobe Experience League. Essas perguntas podem ser categorizadas nos seguintes subgrupos:


| Conhecimento do produto | Disponível para todos os usuários<br>Exemplos |
| :--- | :--- |
| Aprendizado apontado | <ul><li>O que é o Editor Universal?</li><li>Como criar um programa no Cloud Manager?</li></ul> |
| Abrir descoberta | <ul><li>Como usar o Universal Editor?</li><li>Existe uma maneira de copiar o conteúdo de um ambiente para outro?</li></ul> |
| Resolução de problemas | <ul><li>Por que não posso acessar o Universal Editor?</li><li>Por que meu pipeline está falhando?</li></ul> |
| **Criação do tíquete de suporte** | **Disponível somente para Administradores de Suporte &#x200B;**<br>**Exemplos** |
| Criação automatizada de tíquetes de suporte, capturando o histórico e o contexto do bate-papo do Assistente de IA | <ul><li>Crie um tíquete de suporte para mim.</li></ul> |
| Recuperar status do tíquete de suporte | <ul><li>Mostre-me todos os tíquetes de suporte que abri.</li><li>Mostre-me o status do tíquete &quot;E—&quot;</li></ul> |

{style="table-layout:auto"}


## Como criar perguntas eficazes {#ai-craft-questions}

Para receber as respostas mais precisas do Assistente de IA no AEM, é importante formular suas perguntas com clareza e contexto. Use as seguintes dicas para garantir que suas consultas sejam claras e bem estruturadas:

* Indique claramente a sua tarefa ou pergunta de maneira concisa.
* Evite textos ambíguos ou sintaxes excessivamente complexas para melhorar a compreensão.
* Inclua um contexto relevante sobre sua tarefa ou pergunta, pois essa abordagem ajuda o Assistente de IA do AEM a fornecer respostas mais precisas e relevantes.
Por exemplo, no seu prompt, é útil nomear a solução da AEM em que você está trabalhando - Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager ou Forms.

### Exemplos de perguntas não suportadas {#ai-unsupported-questions}

| Área | Exemplos |
| --- | --- |
| Insights operacionais | <ul><li>Quantos ambientes de desenvolvimento existem no meu locatário?</li><li>Quem iniciou o último pipeline de produção?</li></ul> |
| Resolução de problemas | <ul><li>Por que meu pipeline de produção está falhando?</li></ul> |
| Tarefa e automação | <ul><li>Configurar um pipeline de qualidade de código de uma ramificação dev para mim.</li></ul> |


## Usar o assistente de IA no AEM {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use the AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Iniciar um assistente de IA em uma conversa no AEM

Você pode redefinir o Assistente de IA no AEM e iniciar uma nova conversa quando quiser alterar tópicos. Essa capacidade é especialmente útil ao solucionar problemas de consultas que estão falhando ou ao fornecer informações incorretas.

**Para iniciar um Assistente de IA em uma conversa do AEM:**

1. Próximo ao canto superior direito da interface do usuário do AEM (nas páginas do Cloud Manager ou na instância de autor dos ambientes do AEM), clique no ícone **Assistente de IA**.

   ![Ícone do Assistente de IA na barra de ferramentas](/help/assets/assets-ai/ai-assistant-icon.png)

1. Na caixa de texto do painel **Assistente de IA** próxima à parte inferior, digite a pergunta ou o prompt e pressione `Enter` ou clique em ![Ícone Enviar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   >[!NOTE]
   >
   >Dados pessoais não devem ser incluídos em suas entradas, pois são desnecessários para usar essa ferramenta.

   ![Caixa de texto na parte inferior do painel do Assistente de IA](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. Para iniciar uma nova conversa (novo tópico ou uma alteração no tópico), clique em ![Ícone de Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **Iniciar nova conversa**.

   ![Iniciar uma nova conversa no Assistente de IA a partir do ícone de reticências](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### Descobrir prompts por categoria

O Assistente de IA no AEM inclui um recurso de descoberta para ajudar você a explorar tópicos e categorias compatíveis.

**Descobrir prompts por categoria:**

1. No painel Assistente de IA, clique no ![ícone Aprender](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) para ativar o painel de descoberta de prompts.

   ![Painel que permite explorar prompts por categoria no Assistente de IA](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *Painel mostrando as categorias de prompt no Assistente do AI.*

1. Selecione uma categoria para exibir uma lista de prompts relacionados.
1. Selecione um prompt para ver exemplos dos tipos de perguntas que o Assistente de IA pode responder.

1. Para ocultar o painel de descoberta de prompts, clique novamente no ![ícone Aprender](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).

### Compartilhe seu feedback sobre o Assistente de IA no AEM

Sua entrada ajuda a Adobe a melhorar o Assistente de IA para obter melhor desempenho e precisão.

Compartilhe seu feedback sobre a sua experiência com o Assistente de IA no AEM usando as seguintes opções:

![Polegar para cima, polegar para baixo e ícones de sinalizador](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| Clique em | Descrição |
| --- | --- |
| ![Ícone de estrutura de tópicos para cima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Indique o que deu certo e compartilhe feedback positivo. |
| ![Ícone de estrutura de tópicos com miniaturas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Forneça sugestões para aprimoramento. Adicione comentários específicos sobre sua experiência, que são revisados diariamente. |
| ![Ícone de sinalizador](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Relate dúvidas ou forneça feedback detalhado sobre sua interação com o Assistente de IA no AEM. |

## Perguntas frequentes sobre o Assistente de IA no AEM {#ai-faq}

Estas são as respostas para algumas perguntas comuns sobre o Assistente de IA:

* **As informações fornecidas pelo Assistente de IA estão no AEM em tempo real?**\
  Não. O Assistente de IA origina seu conteúdo da documentação da Adobe Experience League. As atualizações do conteúdo podem levar algum tempo para refletir em suas respostas.
* **A quais aplicativos do Adobe o Assistente de IA oferece suporte no AEM?**\
  Atualmente, o Assistente de IA oferece suporte a consultas de conhecimento de produtos na AEM as a Cloud Service, incluindo Sites, Assets, Dynamic Media, Cloud Manager e Forms.
* **Quais são os recursos do Assistente de IA no AEM?**\
  O Assistente de IA do AEM foi projetado para responder a consultas relacionadas ao conhecimento do produto Adobe.
* **O Assistente de IA no AEM usa informações pessoais para dados de treinamento?**\
  Não. O Assistente de IA no AEM não usa informações pessoais para fins de treinamento. Evite compartilhar informações pessoais sobre você ou outras pessoas, incluindo nomes ou detalhes de contato, com o Assistente de IA no AEM.

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
