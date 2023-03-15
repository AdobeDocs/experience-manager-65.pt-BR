---
title: Regulamentos de proteção e privacidade de dados - Disponibilidade do Adobe Experience Manager
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; such as GDPR, CCPA, etc
description: Saiba mais sobre o suporte Adobe Experience Manager a vários Regulamentos de proteção e privacidade de dados; incluindo o Regulamento Geral sobre a Proteção de Dados da UE (GDPR), a Lei de Privacidade do Consumidor da Califórnia, e como estar em conformidade com elas ao implementar um novo projeto AEM
seo-description: Learn about Adobe Experience Manager support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM project.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 60%

---

# Regulamentos de disponibilidade para proteção e privacidade de dados do Adobe Experience Manager {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não se destina a substituir tal aconselhamento.
>
>Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre as regras de proteção e privacidade de dados.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a questões de privacidade, e o que isso significa para você como cliente da Adobe, consulte o [Centro de privacidade da Adobe](https://www.adobe.com/br/privacy.html).

A Adobe está fornecendo documentação e procedimentos (com APIs, quando disponíveis), para o administrador de privacidade do cliente ou administrador AEM lidar com solicitações de proteção e privacidade de dados e ajudar nossos clientes a cumprir essas regulamentações. Os procedimentos documentados permitirão que os clientes executem as solicitações normativas manualmente ou chamando APIs, quando disponíveis, de um portal ou serviço externo.

>[!CAUTION]
>
>Os detalhes documentados aqui estão restritos à Adobe Experience Manager.
>
>Dados de outro Serviço sob demanda do Adobe, juntamente com quaisquer solicitações de privacidade relacionadas, exigirão que ações sejam tomadas nesse serviço.
>
>Para mais informações, consulte o [Centro de privacidade da Adobe](https://www.adobe.com/br/privacy.html).

## Introdução {#introduction}

As instâncias do Adobe Experience Manager e os aplicativos que as executam são de propriedade e operadas por nossos clientes.

Como consequência, as regulamentações de proteção de dados, como GDPR, CCPA e outras, são em grande parte de responsabilidade dos clientes.

Como uma breve introdução, os regulamentos relativos à privacidade e proteção de dados incluem novas regras que devem ser seguidas pelas funções de:

* Entidades de Negócios (CCPA) e/ou Controladores de Dados (GDPR)

* Fornecedores de serviços (CCPA) e/ou Processadores de dados (GDPR)

As principais disposições desses regulamentos são as seguintes:

1. Definição ampliada de dados pessoais para incluir todas as IDs exclusivas; como nos dados direta e indiretamente identificáveis.

2. Requisitos de consentimento reforçados.

3. Aumento do foco nos direitos de exclusão (eliminação de dados).

4. Recusar a venda de dados.

Para Adobe Experience Manager:

* As instâncias e os aplicativos que são executados nelas pertencem e são operadas pelo cliente.

   * Isso significa que o cliente gerencia as funções normativas, incluindo Entidades de negócios e Provedor de serviços, Controlador de dados e Processador de dados, entre outras.

   * O Adobe Experience Platform Privacy Service não fará parte do fluxo de trabalho do AEM, conforme ilustrado no diagrama abaixo.

* O AEM inclui documentação e procedimentos para o administrador de privacidade do cliente e/ou o administrador AEM executarem as solicitações de regulamento de privacidade, seja manualmente ou por meio de APIs, quando disponível.

* Nenhum novo serviço ou interface foi adicionado.

   * Em vez disso, os procedimentos e as APIs estão documentados para uso pelas interfaces/portais do cliente que lidam com solicitações de regulamento de privacidade.

* O AEM não incluirá nenhuma ferramenta pronta para uso para suportar o fluxo de trabalho de solicitações de privacidade.

   * A Adobe fornecerá documentação e procedimentos para o administrador de privacidade do cliente e/ou administrador AEM, permitindo que eles executem manualmente solicitações relacionadas a regulamentos de privacidade.

A Adobe está fornecendo procedimentos para lidar com solicitações de privacidade relacionadas ao Acesso, Exclusão e Não participação no Adobe Experience Manager. Em alguns casos, há APIs disponíveis que podem ser chamadas de um portal desenvolvido pelo cliente ou scripts para ajudar na automação.

O diagrama a seguir ilustra um fluxo de trabalho de solicitação de privacidade (ilustrado com o Adobe Experience Manager 6.5):

![Proteção e privacidade de dados](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager e disponibilidade de regulamentação {#aem-and-regulatory-readiness}

Consulte as seções abaixo para obter a documentação regulamentar para as áreas de produtos de AEM.

## AEM Foundation {#aem-foundation}

Consulte [Lidar com solicitações de proteção e privacidade de dados para a AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM Aceitando Coleta de Estatísticas de Uso Agregado {#aem-opting-into-aggregate-usage-statistics-collection}

Consulte [Coleta de Estatísticas de Uso Agregado](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulte [AEM Sites - Disponibilidade para proteção e privacidade de dados.](/help/sites-administering/gdpr-compliance-sites.md)

## Comércio AEM {#aem-commerce}

Consulte [Comércio AEM - Disponibilidade para proteção e privacidade de dados](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Consulte [AEM Mobile - Disponibilidade para proteção e privacidade de dados](/help/mobile/aem-mobile-gdpr-compliance.md).

## Integração do AEM com a Adobe Target e a Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Essas integrações do Adobe Experience Manager estão com serviços prontos para proteção e privacidade de dados (por exemplo, GDPR ou CCPA). Nenhum dado pessoal do Adobe Target ou Adobe Analytics é armazenado no AEM em relação às integrações.
Para obter mais informações, consulte:

* [Adobe Target - Visão geral sobre a privacidade](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html?lang=pt-BR)

* [Fluxo de trabalho da Privacidade de dados do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=pt-BR)

## AEM Communities {#aem-communities}

O AEM Communities concede aos titulares de dados o direito de sua portabilidade de dados, o direito de acesso e o direito de ser esquecido por meio de [APIs prontas para uso](/help/communities/user-ugc-management-service.md). Essas APIs permitem a exclusão em massa e a exportação em massa de conteúdo gerado pelo usuário e a desativação de contas de usuário identificadas por meio de suas IDs autorizáveis. No entanto, a exclusão permanente da conta de usuário é realizável por meio da exclusão do nó do usuário no CRXDE Lite, que atende à necessidade de fácil recusa do sistema.

Além disso, a AEM Communities oferece privacidade por design devido ao seu console de Moderação em massa, que permite que membros privilegiados encontrem e excluam as contribuições e os detalhes dos usuários. O console de gerenciamento Membros permite limitar ao ponto de banir um colaborador. Além disso, autoriza os titulares dos dados a suprimir as contribuições por eles autorizadas.

## AEM Forms {#aem-forms}

O AEM Forms inclui componentes e fluxos de trabalho que capturam, processam e armazenam dados para orquestrar processos de negócios e concluir transações digitais. Componentes diferentes usam armazenamentos de dados diferentes e permitem a integração com armazenamentos de dados personalizados. A documentação a seguir explica os procedimentos e diretrizes para acessar e manipular dados do usuário para dar suporte à proteção de dados e aos fluxos de trabalho de privacidade (por exemplo, GDPR ou CCPA) de um componente.

* [Portal do Forms](/help/forms/using/forms-portal-handling-user-data.md)
* [Gerenciamento de correspondência](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integração com o Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Fluxos de trabalho centrados na Forms no OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Fluxos de trabalho Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (Somente AEM Forms JEE)
* [Segurança de documento](/help/forms/using/document-security-handling-user-data.md) (Somente AEM Forms JEE)
* [Gerenciamento de usuários](/help/forms/using/user-management-handling-user-data.md) (Somente AEM Forms JEE)
