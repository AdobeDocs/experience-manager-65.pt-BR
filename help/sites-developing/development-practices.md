---
title: Práticas de desenvolvimento
seo-title: Práticas de desenvolvimento
description: Práticas recomendadas para o desenvolvimento em AEM
seo-description: Práticas recomendadas para o desenvolvimento em AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Práticas de desenvolvimento{#development-practices}

## Trabalhar de acordo com uma Definição de Concluído {#work-according-to-a-definition-of-done}

Cada equipe tem uma definição diferente do que significa &quot;feito&quot;, mas é importante ter um e garantir que uma história atenda aos critérios definidos antes de ser aceita.

Alguns critérios normalmente especificados pelas equipes incluem:

* Código revisado para formatação
* Comentários/Javadoc adicionados
* Atende aos níveis de cobertura de teste necessários
* Passa os testes de unidade e integração
* Validado no ambiente de controle de qualidade
* Localização implementada

Sem um Dd bem definido, é fácil acabar numa situação em que muitas coisas estão a meio caminho e nada é verdadeiramente completo.

### Definir e aderir às convenções de codificação e formatação {#define-and-adhere-to-coding-and-formatting-conventions}

Coisas como níveis de recuo e espaço em branco podem não parecer importantes, mas ter um código devidamente formatado vai muito longe para a legibilidade e a manutenibilidade. As convenções devem ser discutidas e acordadas como uma equipe e então seguidas no código.

### Objetivo para a cobertura de teste elevado {#aim-for-high-test-coverage}

À medida que a implementação de um projeto cresce em tamanho, o mesmo acontecerá com o tempo necessário para testá-la. Sem uma boa cobertura de teste, a equipe de teste não poderá ser dimensionada e os desenvolvedores acabarão enterrados em insetos.

Os desenvolvedores devem praticar o TDD, gravando testes de unidade com falha antes do código de produção que atenderá aos seus requisitos. O controle de qualidade deve criar um conjunto automatizado de testes de aceitação para garantir que o sistema funcione como esperado a partir de um nível alto.

Há estruturas personalizadas disponíveis, como Jackalope e Prosper, para tornar o zombaria das APIs em JCR mais simples para garantir a produtividade dos desenvolvedores enquanto escrevem testes de unidade.

### Mantenha a demonstração pronta {#stay-demo-ready}

O sistema deve estar disponível para demonstração à empresa no final de cada iteração. Ao manter o sistema em um estado pronto para demonstração, a equipe estará sempre em uma iteração de prontidão para a produção e a dívida técnica pode ser mantida em um nível sustentável.

### Implemente um ambiente de integração contínua e use-o {#implement-a-continuous-integration-environment-and-use-it}

A implementação de um ambiente de integração contínua permitirá a execução fácil e repetida de testes de unidade e testes de integração. Também dissociará as implantações da equipe de desenvolvimento, permitindo que as outras partes da equipe sejam mais eficientes e permitindo implantações mais estáveis e previsíveis.

### Mantenha o ciclo de desenvolvimento rápido mantendo os tempos de compilação baixos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Se os testes de unidade levarem muito tempo para serem executados, os desenvolvedores evitarão executá-los e perderão seu valor. Se levar muito tempo para criar o código e implantá-lo, as pessoas farão isso com menos frequência. Tornar os tempos de construção curtos uma prioridade garante que o tempo que investimos na nossa cobertura de testes e na infraestrutura de IC continuarão a tornar a equipe mais produtiva.

### Ajuste o Sonar e outras ferramentas de análise de código estático e aja em seus relatórios {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

As ferramentas de análise de código podem ser valiosas, mas somente se seus relatórios levarem à ação da equipe de desenvolvimento. Sem ajustar a análise que essas ferramentas oferecem, as recomendações que geram não serão relevantes e perderão seu valor.

### Siga a Regra de Scout de Menino {#follow-the-boy-scout-rule}

Os Scout Boy têm uma regra: &quot;Deixe melhor do que você encontrou.&quot; Desde que todos os membros da equipe de desenvolvimento adiram a esta regra e limpam algo quando eles se deparam com uma bagunça, o código vai melhorar constantemente.

### Evite implementar recursos YAGNI {#avoid-implementing-yagni-features}

Os recursos do YAGNI (ou Você não vai precisar dele) são coisas que são implementadas quando esperamos que precisemos de algo no futuro, mesmo que não precisemos disso agora. Idealmente, devemos implementar a coisa mais simples que vai funcionar hoje e usar a refatoração contínua para garantir que a arquitetura do sistema evolua com os requisitos ao longo do tempo. Isso nos permitirá focar no que importa e evitar o borrão do código e o deslizamento de recursos.
