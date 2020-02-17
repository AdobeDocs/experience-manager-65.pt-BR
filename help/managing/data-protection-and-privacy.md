---
title: Proteção de dados e regulamentos de privacidade de dados - disponibilidade do Adobe Experience Manager
seo-title: Prontidão do Adobe Experience Manager para proteção de dados e regulamentos de privacidade de dados; como RGPD, CCPA etc
description: 'Saiba mais sobre o suporte do Adobe Experience Manager para os vários Regulamentos de proteção de dados e privacidade de dados; incluindo o Regulamento geral da UE sobre proteção de dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e como cumprir ao implementar um novo projeto do AEM. '
seo-description: 'Saiba mais sobre o suporte do Adobe Experience Manager para os vários Regulamentos de proteção de dados e privacidade de dados; incluindo o Regulamento geral da UE sobre proteção de dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e como cumprir ao implementar um novo projeto do AEM. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: grdp
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: 9b16c8ae2ee28c60f35f9e0f990d79173463c33b

---


# Prontidão do Adobe Experience Manager para proteção de dados e regulamentos de privacidade de dados {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não substitui o aconselhamento jurídico.
>
>Consulte o departamento jurídico da sua empresa para obter conselhos sobre as regulamentações de Proteção de Dados e Privacidade de Dados.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a problemas de privacidade e o que isso significa para você como cliente da Adobe, consulte o Centro [de privacidade da](https://www.adobe.com/privacy.html)Adobe.

A Adobe está fornecendo documentação e procedimentos (com APIs quando disponíveis), para que o administrador de privacidade do cliente ou o administrador do AEM atenda às solicitações de proteção de dados e privacidade e ajude nossos clientes a cumprir essas regulamentações. Os procedimentos documentados permitirão que os clientes executem as solicitações normativas manualmente ou chamando as APIs, quando disponíveis, de um portal ou serviço externo.

>[!CAUTION]
>
>Os detalhes documentados aqui estão restritos ao Adobe Experience Manager.
>
>Os dados de outro serviço sob demanda da Adobe, juntamente com quaisquer solicitações de privacidade relacionadas, exigirão ações nesse serviço.
>
>Para obter mais informações, consulte o Centro [de privacidade da](https://www.adobe.com/privacy.html)Adobe.

## Introdução {#introduction}

As instâncias do Adobe Experience Manager e os aplicativos executados nelas são de propriedade e operados por nossos clientes.

Como consequência, regulamentos de proteção de dados, como o RGPD, o CCPA e outros, são em grande parte da responsabilidade dos clientes.

Como introdução muito breve, os regulamentos relativos à privacidade e proteção de dados incluem novas regras que devem ser seguidas pelas funções de:

* Entidades de Negócios (CCPA) e/ou Controladores de Dados (RGPD)

* Fornecedores de serviços (CCPA) e/ou Processadores de dados (RGPD)

As principais disposições desses regulamentos são:

1. Definição ampliada de dados pessoais para incluir todas as IDs exclusivas; como nos dados direta e indiretamente identificáveis.

2. Requisitos de consentimento reforçados.

3. Aumento do foco nos direitos de exclusão (eliminação de dados).

4. Recusar a venda de dados.

Para o Adobe Experience Manager:

* As instâncias e os aplicativos que são executados nelas são de propriedade e operados pelo cliente.

   * Isso significa que o cliente gerencia efetivamente as funções normativas, incluindo Entidades de negócios e Provedor de serviços, Controlador de dados e Processador de dados, entre outros.

   * O Adobe Experience Platform Privacy Service não fará parte do fluxo de trabalho do AEM, como ilustrado no diagrama abaixo.

* O AEM inclui documentação e procedimentos para o administrador de privacidade do cliente e/ou o administrador do AEM executar as solicitações de regulamento de privacidade; manualmente ou por meio de APIs, quando disponível.

* Nenhum novo serviço ou interface de usuário foi adicionado.

   * Em vez disso, os procedimentos e as APIs são documentados para uso pelas interfaces de usuário/portais do cliente que lidam com solicitações de regulamentação de privacidade.

* O AEM não incluirá nenhuma ferramenta pronta para uso para suportar o fluxo de trabalho de solicitações de privacidade.

   * A Adobe fornecerá documentação e procedimentos para o administrador de privacidade do cliente e/ou o administrador de AEM, permitindo que ele execute manualmente solicitações relacionadas às regras de privacidade.

A Adobe está fornecendo procedimentos para lidar com solicitações de privacidade relacionadas ao Access, Delete e Opt-Out para o Adobe Experience Manager. Em alguns casos, há APIs disponíveis que podem ser chamadas de um portal desenvolvido pelo cliente ou scripts para ajudar na automação.

O diagrama a seguir ilustra a aparência de um fluxo de trabalho de solicitação de privacidade (ilustrado com o Adobe Experience Manager 6.5):

![Proteção de dados e privacidade](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager e disponibilidade normativa {#aem-and-regulatory-readiness}

Consulte as seções abaixo para obter a documentação normativa das áreas de produto do AEM.

## AEM Foundation {#aem-foundation}

Consulte [Manuseio de proteção de dados e solicitações de privacidade para a AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM Optando pela coleta de estatísticas de uso agregado {#aem-opting-into-aggregate-usage-statistics-collection}

Consulte Coleta [de Estatísticas de Uso](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)Agregado.

## AEM Sites {#aem-sites}

Consulte [AEM Sites - Proteção de dados e prontidão para privacidade.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Consulte Comércio [AEM - Proteção de dados e prontidão](/help/sites-administering/gdpr-compliance-commerce.md)para privacidade.

## AEM Mobile {#aem-mobile}

Consulte [AEM Mobile - Proteção de dados e prontidão](/help/mobile/aem-mobile-gdpr-compliance.md)para privacidade.

## Integração do AEM com o Adobe Target e o Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Essas integrações do Adobe Experience Manager têm proteção de dados e serviços de privacidade (por exemplo, RGPD ou CCPA) prontos. Nenhum dado pessoal do Adobe Target ou Adobe Analytics é armazenado no AEM em relação às integrações.
Para obter mais informações, consulte:

* [Adobe Target - Visão geral de privacidade](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Fluxo de trabalho de privacidade de dados do Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

O AEM Communities concede às pessoas de dados o direito à portabilidade dos dados, o direito de acesso e o direito de serem esquecidos por meio de APIs [](/help/communities/user-ugc-management-service.md)prontas para uso. Essas APIs permitem a exclusão em massa e a exportação em massa de conteúdo gerado pelo usuário, além de desativar as contas de usuário identificadas por meio de suas IDs autorizados. No entanto, a exclusão permanente da conta de usuário é realizável por meio da exclusão do nó de usuário no CRXDE Lite, que atende à necessidade de recusa fácil do sistema.

Além disso, o AEM Communities oferece privacidade por design devido ao seu console de Moderação em massa, que permite que membros privilegiados localizem e excluam as contribuições e os detalhes dos usuários. O console de gerenciamento de membros permite limitar ao ponto de banir um contribuinte. Além disso, autoriza as pessoas em causa a eliminar as contribuições por elas autorizadas.

## Formulários AEM {#aem-forms}

O AEM Forms inclui componentes e fluxos de trabalho que capturam, processam e armazenam dados para orquestrar processos de negócios e concluir transações digitais. Diferentes componentes usam diferentes armazenamentos de dados e também permitem a integração com armazenamentos de dados personalizados. A documentação a seguir explica os procedimentos e diretrizes para acessar e manipular dados do usuário para suportar os fluxos de trabalho de proteção de dados e privacidade (por exemplo, RGPD ou CCPA) de um componente.

* [Portal de formulários](/help/forms/using/forms-portal-handling-user-data.md)
* [Gerenciamento de correspondência](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integração com o Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Fluxos de trabalho centrados em formulários no OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Fluxos de trabalho](/help/forms/using/forms-workflow-jee-handling-user-data.md) JEE do Forms (somente JEE do AEM Forms)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (somente AEM Forms JEE)
* [Gerenciamento](/help/forms/using/user-management-handling-user-data.md) de usuários (somente AEM Forms JEE)
