---
title: Regulamentos de proteção de dados e privacidade de dados - prontidão da Adobe Experience Manager
seo-title: Adobe Experience Manager Prontidão para proteção de dados e regulamentos de privacidade de dados; como RGPD, CCPA etc
description: 'Saiba mais sobre o suporte da Adobe Experience Manager para os vários Regulamentos de proteção de dados e privacidade de dados; incluindo o Regulamento Geral da UE sobre Proteção de Dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e o modo de cumprir ao implementar um novo projeto AEM. '
seo-description: 'Saiba mais sobre o suporte da Adobe Experience Manager para os vários Regulamentos de proteção de dados e privacidade de dados; incluindo o Regulamento Geral da UE sobre Proteção de Dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e o modo de cumprir ao implementar um novo projeto AEM. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---


# Adobe Experience Manager Ready for Data Protection and Data Privacy Regulations {#aem-readiness-for-data-protection-and-data-privacy-regulations} (Disponibilidade para proteção de dados e regulamentos de privacidade de dados)

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não substitui o aconselhamento jurídico.
>
>Consulte o departamento jurídico da sua empresa para obter informações sobre as regulamentações de Proteção de Dados e Privacidade de Dados.

>[!NOTE]
>
>Para obter mais informações sobre o que isso significa em relação a problemas de privacidade, consulte [Centro de Privacidade do Adobe](https://www.adobe.com/privacy.html)Adobe.

A Adobe está fornecendo documentação e procedimentos (com APIs quando disponíveis), para o administrador de privacidade do cliente ou administrador de AEM para lidar com solicitações de proteção de dados e privacidade e ajudar nossos clientes a cumprir essas regulamentações. Os procedimentos documentados permitirão que os clientes executem as solicitações normativas manualmente ou chamando as APIs, quando disponíveis, de um portal ou serviço externo.

>[!CAUTION]
>
>Os detalhes documentados aqui estão restritos à Adobe Experience Manager.
>
>Os dados de outro Serviço sob demanda do Adobe, juntamente com quaisquer solicitações de privacidade relacionadas, exigirão ações nesse serviço.
>
>Para obter mais informações, consulte o Centro de Privacidade do Adobe[.](https://www.adobe.com/privacy.html)

## Introdução {#introduction}

As instâncias da Adobe Experience Manager e os aplicativos que são executados nelas são de propriedade e operados por nossos clientes.

Como consequência, regulamentos de proteção de dados, como o RGPD, o CCPA e outros, são em grande parte da responsabilidade dos clientes.

Como introdução muito breve, os regulamentos relativos à privacidade e proteção de dados incluem novas regras que devem ser seguidas pelas funções de:

* Entidades de Negócios (CCPA) e/ou Controladores de Dados (RGPD)

* provedores de serviço (CCPA) e/ou processadores de dados (RGPD)

As principais disposições desses regulamentos são as seguintes:

1. Definição ampliada de dados pessoais para incluir todas as IDs exclusivas; como nos dados direta e indiretamente identificáveis.

2. Requisitos de consentimento reforçados.

3. Aumento do foco nos direitos de exclusão (eliminação de dados).

4. Recusar a venda de dados.

Para Adobe Experience Manager:

* As instâncias e os aplicativos que são executados nelas são de propriedade e operados pelo cliente.

   * Isso significa que o cliente gerencia efetivamente as funções normativas, incluindo as Entidades de negócios e o Provedor de serviço, o Controlador de dados e o Processador de dados, entre outros.

   * O Adobe Experience Platform Privacy Service não fará parte do fluxo de trabalho do AEM, conforme ilustrado no diagrama abaixo.

* AEM inclui documentação e procedimentos para o administrador de privacidade do cliente e/ou AEM administrador executar as solicitações de regulamentação de privacidade; manualmente ou por meio de APIs, quando disponível.

* Nenhum novo serviço ou interface de usuário foi adicionado.

   * Em vez disso, os procedimentos e as APIs são documentados para uso pelas interfaces de usuário/portais do cliente que lidam com solicitações de regulamentação de privacidade.

* AEM não incluirá nenhuma ferramenta pronta para uso para suportar o fluxo de trabalho de solicitações de privacidade.

   * O Adobe fornecerá documentação e procedimentos para o administrador de privacidade do cliente e/ou AEM administrador, permitindo que ele execute manualmente solicitações relacionadas às regras de privacidade.

O Adobe está fornecendo procedimentos para lidar com solicitações de privacidade relacionadas ao Access, Delete e Opt-Out para Adobe Experience Manager. Em alguns casos, há APIs disponíveis que podem ser chamadas de um portal desenvolvido pelo cliente ou scripts para ajudar na automação.

O diagrama a seguir ilustra a aparência de um fluxo de trabalho de solicitação de privacidade (ilustrado com o Adobe Experience Manager 6.5):

![Proteção de dados e privacidade](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager e disponibilidade normativa {#aem-and-regulatory-readiness}

Consulte as seções abaixo para obter a documentação normativa das áreas de produtos de AEM.

## AEM Foundation {#aem-foundation}

Consulte [Tratamento de solicitações de proteção e privacidade de dados para a AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM Optando pela Coleta de Estatísticas de Uso de Agregação {#aem-opting-into-aggregate-usage-statistics-collection}

Consulte [Coleta de Estatísticas de Uso Agregado](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulte [AEM Sites - Proteção de Dados e Disponibilidade de Privacidade.](/help/sites-administering/gdpr-compliance-sites.md)

## Comércio AEM {#aem-commerce}

Consulte [Comércio AEM - Proteção de dados e prontidão para privacidade](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Consulte [AEM Mobile - Proteção de dados e prontidão para privacidade](/help/mobile/aem-mobile-gdpr-compliance.md).

## Integração AEM com Adobe Target e Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Essas integrações Adobe Experience Manager estão com proteção de dados e serviços de privacidade (por exemplo, RGPD ou CCPA) prontos. Nenhum dado pessoal da Adobe Target ou Adobe Analytics é armazenado em AEM em relação às integrações.
Para obter mais informações, consulte:

* [Adobe Target - Visão geral de privacidade](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Fluxo de trabalho de privacidade de dados da Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

A AEM Communities concede às pessoas de dados o direito de portabilidade de dados, o direito de acesso e o direito de serem esquecidos por meio de [APIs prontas para uso](/help/communities/user-ugc-management-service.md). Essas APIs permitem a exclusão em massa e a exportação em massa de conteúdo gerado pelo usuário, além de desativar as contas de usuário identificadas por meio de suas IDs autorizados. No entanto, a exclusão permanente da conta de usuário é realizável por meio da exclusão do nó de usuário no CRXDE Lite, que atende à necessidade de recusa fácil do sistema.

Além disso, a privacidade do AEM Communities oferta por design devido ao seu console Moderação em massa, que permite que membros privilegiados localizem e excluam as contribuições e detalhes dos usuários. O console de gerenciamento de membros permite limitar ao ponto de banir um contribuinte. Além disso, autoriza as pessoas em causa a eliminar as contribuições por elas autorizadas.

## AEM Forms {#aem-forms}

A AEM Forms inclui componentes e workflows que capturam, processam e armazenam dados para orquestrar processos comerciais e concluir transações digitais. Diferentes componentes usam diferentes armazenamentos de dados e também permitem a integração com armazenamentos de dados personalizados. A documentação a seguir explica os procedimentos e as diretrizes para acessar e manipular dados do usuário para dar suporte à proteção de dados e aos workflows de privacidade (por exemplo, RGPD ou CCPA) de um componente.

* [Portal da Forms](/help/forms/using/forms-portal-handling-user-data.md)
* [Gerenciamento de correspondência](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integração com a Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Workflows centrados na Forms no OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Workflows](/help/forms/using/forms-workflow-jee-handling-user-data.md)  Forms JEE (somente AEM Forms JEE)
* [Segurança](/help/forms/using/document-security-handling-user-data.md)  do documento (AEM Forms JEE apenas)
* [Gerenciamento](/help/forms/using/user-management-handling-user-data.md)  de usuários (somente AEM Forms JEE)
