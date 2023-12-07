---
title: Ferramentas de teste e rastreamento
description: O AEM fornece uma estrutura para testar a interface do usuário do componente e um mecanismo para testar e depurar componentes
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 1%

---

# Ferramentas de teste e rastreamento{#testing-and-tracking-tools}

## Testes {#testing}

O AEM fornece:

* [uma estrutura para testar a interface do usuário do componente](/help/sites-developing/hobbes.md).
* [um mecanismo para testar e depurar componentes](/help/sites-developing/developer-mode.md).

Veja a seguir duas ferramentas de teste de código aberto:

**Selênio**

O Selenium é usado para testes de função em um navegador com um usuário por atividade. Ele registra etapas de teste (cliques) como tabelas de HTML ou classes Java™.

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

Embora não seja especificamente uma ferramenta de rastreamento de erros, as planilhas são frequentemente *mis* usados para essa finalidade, pois são fáceis de entender e a maioria dos usuários tem experiência de sua funcionalidade.

Se essas planilhas forem usadas para rastreamento, então:

* devem ser mantidas simples.
* o número de planilhas individuais deve ser reduzido ao mínimo.
* eles devem ser atualizados regularmente.
* somente uma cópia principal deve ser mantida e todos devem saber onde está a cópia principal.
* eles devem estar acessíveis a todos os membros do projeto.
* se a segurança for um problema (geralmente ocorre em grandes empresas) e o acesso comum não for possível, as cópias poderão ser distribuídas desde que todos entendam que essas planilhas são cópias e não podem ser atualizadas.

Novamente, há muitas ferramentas proprietárias para rastrear bugs e requisitos de recursos.
