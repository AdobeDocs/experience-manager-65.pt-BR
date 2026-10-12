---
title: Ferramentas de teste e rastreamento
description: O AEM fornece uma estrutura para testar a interface do usuário do componente e um mecanismo para testar e depurar componentes
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 2%
---
# Ferramentas de teste e rastreamento{#testing-and-tracking-tools}

## Testes {#testing}

O AEM fornece:

* [uma estrutura para testar a interface do usuário do componente](/help/sites-developing/hobbes.md).
* [um mecanismo para componentes de teste e depuração](/help/sites-developing/developer-mode.md).

Veja a seguir duas ferramentas de teste do Open Source:

**Selenium**

O Selenium é usado para testes de função em um navegador com um usuário por atividade. Ele registra as etapas de teste (cliques) como tabelas do HTML ou classes Java™.

Para obter mais informações, consulte [https://www.selenium.dev/](https://www.selenium.dev/).

**JMeter**

O JMeter é usado para rastrear solicitações e pode ser usado para testes funcionais, de desempenho e de stress.

Para obter mais informações, consulte [https://jmeter.apache.org/](https://jmeter.apache.org/).

Há também muitas ferramentas proprietárias para automatizar testes e gerenciar planos de teste.

### Rastreamento {#tracking}

As ferramentas a seguir estão facilmente disponíveis. No entanto, um problema importante em todos os casos é a disponibilidade dos dados para todos os membros da equipe do projeto: parceiro e cliente.

**Bugzilla**

Um sistema de acompanhamento de erros que pode ser configurado de acordo com os seus próprios requisitos.

**Planilhas**

Embora não seja uma ferramenta de rastreamento de erros específica, as planilhas são frequentemente *mis* usadas para essa finalidade, pois são fáceis de entender e a maioria dos usuários tem experiência em sua funcionalidade.

Se essas planilhas forem usadas para rastreamento, então:

* devem ser mantidas simples.
* o número de planilhas individuais deve ser reduzido ao mínimo.
* eles devem ser atualizados regularmente.
* somente uma cópia principal deve ser mantida e todos devem saber onde está a cópia principal.
* eles devem estar acessíveis a todos os membros do projeto.
* se a segurança for um problema (geralmente ocorre em grandes empresas) e o acesso comum não for possível, as cópias poderão ser distribuídas desde que todos entendam que essas planilhas são cópias e não podem ser atualizadas.

Novamente, há muitas ferramentas proprietárias para rastrear bugs e requisitos de recursos.
