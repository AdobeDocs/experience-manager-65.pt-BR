---
title: Retenção de dados no AEM Forms
description: Saiba como o Adobe Experience Manager (AEM) Forms, por padrão, age como um servidor de passagem e não armazena dados do usuário final, oferecendo suporte à privacidade de dados.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%
---
# Retenção de dados no AEM Forms {#data-retention-in-aem-forms}

O AEM Forms armazena dados de formulário? Por padrão, não. O Adobe Experience Manager (AEM) Forms atua como um servidor de passagem para dados capturados pelo Adaptive Forms e não armazena dados do usuário final no Repositório do AEM. Em vez disso, o servidor passa os dados enviados para o destino que você possui e configura. Esse comportamento padrão ajuda a atingir suas metas de privacidade e conformidade de dados, e se aplica ao AEM Forms no OSGi e ao AEM Forms no JEE.

Como o AEM Forms é uma plataforma extensível, você pode personalizar o AEM para alterar esse comportamento padrão. Se a personalização armazenar os dados enviados por meio de um formulário adaptável no repositório do AEM ou gravá-los nos logs do AEM, você deverá garantir que esses dados não sejam retidos nos sistemas de produção e de preparo.

## Comportamento padrão com recursos prontos para uso {#default-behavior}

Quando você usa recursos prontos para uso do Adaptive Forms, a AEM Forms não armazena dados do usuário final. O servidor passa diretamente os dados enviados para o destino que você possui e configura.

Os mecanismos prontos para uso que conectam um formulário a um destino de sua propriedade incluem o Modelo de dados de formulário (FDM), conectores prontos para uso e ações de envio. Cada um desses itens envia dados para um local que você possui e configura, de modo que não sejam retidos no Repositório do AEM. Um formulário também pode invocar um serviço externo ou de terceiros, como uma API REST, de uma regra ou ação de envio e encaminhar dados para esse serviço sem persistir nos dados no AEM.

Se você usar Workflows da AEM com processos de longa duração que envolvam uma etapa de aprovação, a AEM Forms poderá manter os dados na memória e no armazenamento temporário para concluir a operação. Para obter informações sobre como impedir que esses dados sejam salvos no AEM, consulte a seção [Dados em processos de fluxo de trabalho de longa duração](#long-lived-workflow-processes).

A ação Enviar do Forms Portal retém dados capturados ou enviados pelo Adaptive Forms, mas os dados são salvos em um local de armazenamento fornecido e de propriedade sua, não no Repositório ou logs do AEM. Para obter mais informações, consulte [Proteger dados salvos pela ação de envio do portal de formulários](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action).

## Dados em trânsito {#data-in-transit}

Embora o AEM Forms não armazene dados do usuário final por padrão, os dados ainda se movem entre o usuário final, o AEM Forms e o destino configurado. Proteja esse tráfego com o TLS (Transport Layer Security) para que os dados sejam criptografados em trânsito.

Para proteger a conexão entre o navegador e o AEM, habilite o HTTPS na instância do AEM. Para obter as etapas, consulte [SSL/TLS por padrão](/help/sites-administering/ssl-by-default.md).

Além disso, verifique se os endpoints para os quais o AEM Forms envia dados, como configurações de nuvem, URLs de ação de envio e fontes de dados do Modelo de dados de formulário, usam endpoints HTTPS seguros. Como o AEM Forms não armazena os dados transmitidos, a criptografia em repouso não se aplica a esses dados. Para obter mais orientações sobre como proteger a conexão, consulte [Camada de transporte segura](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer).

## Modelo de dados de formulário para armazenamentos de dados externos {#form-data-model}

Para ler e gravar dados em um armazenamento de dados, use um Modelo de Dados de Formulário (FDM). O FDM é o mecanismo recomendado para conectar um formulário a uma fonte de dados que você possui e gerencia, como um banco de dados ou um serviço Web RESTful.

Para obter mais informações, consulte [Introdução à Integração de Dados do AEM Forms](/help/forms/using/data-integration.md). Para obter orientação sobre como proteger os dados tratados por um FDM, consulte [Proteger dados tratados pelo modelo de dados de formulário (FDM)](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm).

## Dados em processos de fluxo de trabalho de longa vida {#long-lived-workflow-processes}

Se você usar processos de fluxo de trabalho de longa duração, o AEM poderá salvar dados temporariamente como parte da carga do fluxo de trabalho. As variáveis de fluxo de trabalho que carregam esse conteúdo são armazenadas nos metadados da instância do fluxo de trabalho no Repositório do AEM e podem conter informações de identificação pessoal (PII) ou dados pessoais confidenciais (SPD) fornecidos pelos usuários finais ao preencher um formulário adaptável.

Para manter esses dados em um repositório que você possui e gerencia, como o armazenamento Azure Blob, em vez do AEM, use o recurso de externalização de dados da AEM. Ao externalizar as variáveis, os dados não são salvos no repositório do AEM; em vez disso, eles são armazenados no seu próprio repositório de dados.

Para obter as etapas para externalizar dados, consulte [Parametrizar dados confidenciais para variáveis de fluxo de trabalho e armazenar em armazenamentos de dados externos](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

## Personalização e registro {#customization-and-logging}

O AEM é uma solução personalizável. Se você personalizar o AEM, certifique-se de que a personalização não armazene dados no Repositório ou logs do AEM.

Quando você usa recursos padrão, o AEM Forms não grava dados do usuário final do formulário nos logs.

O código personalizado pode gravar dados em logs. Se você adicionar rastreamento ou log durante o desenvolvimento, remova os rastreamentos e dados enviados aos logs antes de implantar seu código em ambientes de preparo e produção.

## Perguntas frequentes sobre a retenção de dados do AEM Forms {#faq}

**O AEM Forms armazena dados de formulário?**

Não. Por padrão, o Adobe Experience Manager (AEM) Forms atua como um servidor de passagem para dados capturados pelo Adaptive Forms e não armazena dados do usuário final no Repositório do AEM. O servidor passa dados enviados para o destino que você possui e configura, como uma fonte de dados do Modelo de dados de formulário, um destino de ação de envio ou uma API externa. Esse comportamento padrão se aplica ao AEM Forms no OSGi e ao AEM Forms no JEE.

**Onde os dados do Formulário adaptável são armazenados?**

Os dados do formulário adaptável enviado são armazenados no destino que você possui e configura, não no repositório do Adobe Experience Manager (AEM). Mecanismos prontos para uso, como o Form Data Model (FDM), conectores e ações de envio enviam dados para seu próprio local. Um formulário também pode encaminhar dados para um serviço externo, como uma API REST, sem persistir nele no AEM. A ação de envio do Portal do Forms também salva os dados em um local de armazenamento que você fornece e que é proprietário.

**Os fluxos de trabalho de longa duração armazenam dados de formulário?**

Processos de fluxo de trabalho de longa duração no Adobe Experience Manager (AEM) Forms podem salvar dados temporariamente como parte da carga do fluxo de trabalho, que é armazenada nos metadados da instância do fluxo de trabalho no Repositório do AEM. Para manter esses dados em um repositório que você possui e gerencia, como o armazenamento Azure Blob, em vez do AEM, use o [recurso de externalização de dados do AEM para variáveis de fluxo de trabalho](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

**O AEM Forms grava dados nos logs?**

Não. Com os recursos padrão, o Adobe Experience Manager (AEM) Forms não grava dados do usuário final em logs. Como o AEM é uma plataforma personalizável, o código personalizado pode gravar dados em logs. Se você adicionar rastreamento ou registro durante o desenvolvimento, remova esses rastreamentos e quaisquer dados registrados antes de implantar em ambientes de preparo e produção. Uma personalização não deve armazenar dados no Repositório ou logs do AEM.

**Como os dados são protegidos em trânsito?**

Os dados em trânsito são protegidos com TLS (Transport Layer Security) no Adobe Experience Manager (AEM) Forms. Ative o HTTPS na instância do AEM para proteger a conexão entre o navegador e o AEM. Além disso, verifique se os endpoints para os quais o AEM Forms envia dados, como configurações de nuvem, URLs de ação de envio e fontes de dados do Modelo de dados de formulário, usam endpoints HTTPS seguros. Como o AEM Forms não armazena os dados por onde passa, a criptografia em repouso não se aplica a esses dados.

## Recursos relacionados {#related-resources}

* [Introdução à integração de dados do AEM Forms](/help/forms/using/data-integration.md)
* [Parametrizar dados sigilosos para variáveis de fluxo de trabalho e armazená-los em armazenamentos de dados externos](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [Configuração da ação Enviar](/help/forms/using/configuring-submit-actions.md)
* [Fortalecimento e proteção do AEM Forms no ambiente OSGi](/help/forms/using/hardening-securing-aem-forms-environment.md)
