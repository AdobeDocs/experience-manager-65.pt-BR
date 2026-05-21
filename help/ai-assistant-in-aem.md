---
title: Assistente de IA no AEM 6.5
description: Use o Assistente de IA para ajudar a encontrar respostas e solucionar problemas das soluções disponíveis no Adobe Experience Manager.
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
autotag-review: '2026-05-18T18:36:07.915Z'
TQID: 'https://experienceleague.adobe.com/dlFmrtn05S20z96wtAfkpGliITeVJhVkofqPix6QMxk'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1379
ht-degree: 93%

---

# Assistente de IA no AEM 6.5 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>Os clientes do AEM 6.5 e do AEM 6.5 LTS que não usam o Cloud Manager/Experience Hub devem entrar em contato com o engenheiro de sucesso do cliente da Adobe para solicitar acesso ao Assistente de IA.

O AI Assistant no AEM 6.5/AEM 6.5 LTS oferece uma interface conversacional projetada para simplificar a localização de respostas para suas consultas relacionadas ao Adobe Experience Manager. Ele ajuda a obter respostas instantâneas para perguntas sobre produtos do AEM (*disponíveis para todos os usuários*) e a automatizar a criação de tíquetes de suporte (*disponíveis para Admins de suporte*).

O Assistente de IA é compatível com o AEM as a Cloud Service, incluindo as seguintes soluções:

* Página de visão geral do Experience Hub
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


Ele é incorporado diretamente no AEM e acessível a partir do AEM Experience Hub, Cloud Manager e da interface do autor.

O vídeo a seguir de 3 minutos e 25 segundos oferece uma apresentação passo-a-passo do Assistente de IA no AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## Obter acesso ao Assistente de IA no AEM{#get-access}

Para obter acesso ao Assistente de IA no AEM, os clientes devem ter o seguinte:

* Permissão para usar o Assistente de IA no AEM para conhecimento sobre produtos. Essa permissão possibilita fazer perguntas relacionadas ao produto no chat do Assistente de IA. Essa permissão deve ser habilitada.
* Permissão para abrir tíquetes de suporte, o que requer a função de **Admin de suporte**.

>[!NOTE]
>
>As solicitações do Assistente de IA no AEM são autenticadas por meio dos Serviços de gerenciamento de identidade da Adobe (IMS). Para obter detalhes, consulte a [visão geral dos Serviços de gerenciamento de identidade da Adobe](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf).

**Para obter acesso ao Assistente de IA no AEM:**

1. Os clientes devem ter um contrato adicional em vigor para acessar a maioria dos recursos agênticos e viabilizados por IA no Adobe Experience Manager. Entre em contato com o representante da Adobe para obter mais detalhes.

1. Para usar o Assistente de IA no AEM, é obrigatória a permissão para acessar o conhecimento sobre produtos por meio do Assistente de IA. Essa permissão está ativada por padrão.

   Para controlar quem pode acessar o conhecimento do produto, envie um email para [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) a partir do endereço de email associado à sua Adobe ID. A Adobe pode habilitar o controle de acesso no nível do usuário. Quando estiver habilitado, o Admin poderá conceder acesso de nível de usuário seguindo as etapas em [Configurar o Assistente de IA no AEM](/help/ai-assistant-in-aem-admin.md).


## Escopo {#scope}

O escopo atual do Assistente de IA no AEM se concentra em abordar perguntas de conhecimento do produto para o AEMr. as a Cloud Service. Esse escopo inclui suporte abrangente para áreas importantes. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **Superfícies**: disponível no AEM Experience Hub, interface do autor, Cloud Manager.
* **Recursos**: conhecimento do produto e a primeira parada para solução de problemas e orientação, criação automatizada de tíquetes de suporte e pesquisa.
* **Valor**: economiza tempo, acelera o aprendizado e o tempo para obtenção de valor, reduz a necessidade de criar tíquetes de suporte manualmente e melhora a eficiência na criação de tíquetes de suporte.

## Privacidade, segurança e governança{#privacy-security-governance}

O Assistente de IA no AEM foi projetado com forte ênfase em privacidade, segurança e governança.

Este artigo descreve os recursos baseados na confiança que você pode esperar do Assistente de IA no AEM:

* Nenhum dado pessoal é usado pelo Assistente de IA no AEM, inclusive para fins de treinamento.
* O Assistente de IA no AEM não tem acesso aos dados do consumidor.
* A permissão explícita é necessária para interagir com o Assistente de IA no AEM.
* Os prompts fornecidos pelo usuário (perguntas, consultas e assim por diante) não são compartilhados com outros clientes.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Conheça o Assistente de IA no AEM para obter conhecimento sobre produtos e criação automatizada de tíquetes de suporte {#ai-prod-insights}

O conhecimento sobre produtos abrange conceitos e tópicos derivados da documentação da Adobe Experience League. Essas perguntas podem ser categorizadas nos seguintes subgrupos:


| Conhecimento sobre produtos | Disponível para todos os usuários<br>Exemplos |
| :--- | :--- |
| Aprendizado direcionado | <ul><li>O que é o editor universal?</li><li>Como criar um programa no Cloud Manager?</li></ul> |
| Abrir descoberta | <ul><li>Como usar o editor universal?</li><li>Existe uma maneira de copiar o conteúdo de um ambiente para outro?</li></ul> |
| Resolução de problemas | <ul><li>Por que não posso acessar o editor universal?</li><li>Por que meu pipeline está falhando?</li></ul> |
| **Criação de tíquetes de suporte** | **Disponível somente para Admins de suporte **<br>**Exemplos** |
| Criação automatizada de tíquetes de suporte, capturando o histórico e o contexto do chat do Assistente de IA | <ul><li>Crie um tíquete de suporte para mim.</li></ul> |
| Obtenha o status do tíquete de suporte | <ul><li>Mostre-me todos os tíquetes de suporte que abri.</li><li>Mostre-me o status do tíquete &quot;E-----------&quot;</li></ul> |

{style="table-layout:auto"}


## Como criar perguntas eficazes {#ai-craft-questions}

Para receber as respostas mais precisas do Assistente de IA no AEM, é importante formular as perguntas com clareza e contexto. Use as seguintes dicas para garantir que as consultas sejam claras e bem estruturadas:

* Indique claramente a tarefa ou pergunta de forma concisa.
* Evite textos e palavras ambíguos ou sintaxes excessivamente complexas para melhorar a compreensão.
* Inclua um contexto relevante para a tarefa ou pergunta, pois essa abordagem ajuda o Assistente de IA no AEM a fornecer respostas mais precisas e relevantes.
Por exemplo, no prompt, é útil nomear a solução do AEM em que você está trabalhando - Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager ou Forms.

### Exemplos de perguntas incompatíveis {#ai-unsupported-questions}

| Área | Exemplos |
| --- | --- |
| Insights operacionais | <ul><li>Quantos ambientes de desenvolvimento existem no meu locatário?</li><li>Quem iniciou o mais recente pipeline de produção?</li></ul> |
| Resolução de problemas | <ul><li>Por que meu pipeline de produção está falhando?</li></ul> |
| Tarefa e automação | <ul><li>Configure um pipeline de qualidade de código de uma ramificação de desenvolvimento para mim.</li></ul> |


## Usar o Assistente de IA no AEM {#ai-use}

<!--
UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md).
-->


### Iniciar uma conversa com o Assistente de IA no AEM

É possível redefinir o Assistente de IA no AEM e iniciar uma nova conversa quando quiser trocar de tópico. Essa capacidade é especialmente útil ao solucionar problemas de consultas que estão falhando ou fornecendo informações incorretas.

**Para iniciar uma conversa com o Assistente de IA no AEM:**

1. Próximo ao canto superior direito da interface do AEM (nas páginas do Cloud Manager ou na instância de criação dos ambientes do AEM), clique no ícone **Assistente de IA**.

   ![Ícone do Assistente de IA na barra de ferramentas](/help/assets/assets-ai/ai-assistant-icon.png)

1. Na caixa de texto do painel **Assistente de IA** próxima à parte inferior, digite a pergunta ou o prompt e pressione `Enter` ou clique no ![ícone Enviar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   >[!NOTE]
   >
   >Dados pessoais não devem ser incluídos nas entradas, pois são desnecessários para usar essa ferramenta.

   ![Caixa de texto na parte inferior do painel Assistente de IA](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. Para iniciar uma nova conversa (novo tópico ou uma mudança no tópico), clique em ![Ícone de mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **Iniciar nova conversa**.

   ![Iniciar uma nova conversa no Assistente de IA a partir do ícone de reticências](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### Descobrir prompts por categoria

O Assistente de IA no AEM inclui um recurso de descoberta para ajudar a explorar tópicos e categorias compatíveis.

**Para descobrir prompts por categoria:**

1. No painel Assistente de IA, clique no ![ícone Aprender](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) para ativar o painel de descoberta de prompts.

   ![Painel que permite explorar prompts por categoria no Assistente de IA](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *Painel mostrando categorias de prompts no Assistente de AI.*

1. Selecione uma categoria para exibir uma lista de prompts relacionados.
1. Selecione um prompt para ver exemplos dos tipos de perguntas que o Assistente de IA pode responder.

1. Para ocultar o painel de descoberta de prompts, clique novamente no ![ícone Aprender](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).

### Compartilhe feedback sobre o Assistente de IA no AEM

Sua entrada ajuda a Adobe a melhorar o Assistente de IA para obter melhor desempenho e precisão.

Compartilhe feedback sobre a sua experiência com o Assistente de IA no AEM usando as seguintes opções:

![Polegar para cima, polegar para baixo e ícones de sinalizador](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| Clique em | Descrição |
| --- | --- |
| ![Ícone de contorno de polegar para cima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Indique o que deu certo e compartilhe feedback positivo. |
| ![Ícone de contorno de polegar para baixo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Forneça sugestões para aprimoramento. Adicione comentários específicos sobre sua experiência, que são revisados diariamente. |
| ![Ícone de sinalizador](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Relate preocupações ou forneça feedback detalhado sobre a interação com o Assistente de IA no AEM. |

## Perguntas frequentes sobre o Assistente de IA no AEM {#ai-faq}

Estas são as respostas para algumas perguntas comuns sobre o Assistente de IA:

* **As informações fornecidas pelo Assistente de IA no AEM são em tempo real?**\
  Não. O Assistente de IA origina seu conteúdo da documentação da Adobe Experience League. As atualizações do conteúdo podem levar algum tempo para gerar efeito nas respostas.
* **A quais aplicativos da Adobe o Assistente de IA no AEM oferece suporte?**\
  Atualmente, o Assistente de IA é compatível com consultas de conhecimento de produto no AEM as a Cloud Service, incluindo Sites, Assets, Dynamic Media, Cloud Manager e Forms.
* **Quais são os recursos do Assistente de IA no AEM?**\
  O Assistente de IA do AEM foi projetado para responder a consultas relacionadas ao conhecimento do produto Adobe.
* **O Assistente de IA no AEM usa informações pessoais para dados de treinamento?**\
  Não. O Assistente de IA no AEM não usa informações pessoais para fins de treinamento. Evite compartilhar informações pessoais sobre você ou outras pessoas, incluindo nomes ou detalhes de contato, com o Assistente de IA no AEM.

<!--
IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

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
