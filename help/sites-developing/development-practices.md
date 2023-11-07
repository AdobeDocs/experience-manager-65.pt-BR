---
title: Práticas de desenvolvimento
description: Práticas recomendadas para desenvolvimento no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Práticas de desenvolvimento{#development-practices}

## Trabalhar de acordo com uma definição de concluído (DoD) {#work-according-to-a-definition-of-done}

Cada equipe tem uma definição diferente do que &quot;feito&quot; significa, mas é importante ter uma e garantir que uma história atenda aos critérios definidos antes de ser aceita.

Alguns critérios normalmente especificados por equipes incluem:

* Código revisado para formatação
* Comentários/Javadoc adicionado
* Atende aos níveis de cobertura de teste necessários
* Aprovado em testes de unidade e integração
* Validado no ambiente de controle de qualidade
* Localização implementada

Sem uma DoD bem definida, é fácil acabar numa situação em que muitas coisas estão no meio do caminho e nada está realmente completo.

### Definir e aderir às convenções de codificação e formatação {#define-and-adhere-to-coding-and-formatting-conventions}

Coisas como níveis de recuo e espaço em branco podem não parecer importantes, mas ter um código formatado corretamente leva um longo caminho em direção à legibilidade e manutenção. As convenções devem ser discutidas e acordadas como uma equipe e seguidas no código.

### Objetivo para cobertura de teste elevado  {#aim-for-high-test-coverage}

À medida que a implementação de um projeto cresce em tamanho, o mesmo acontece com a quantidade de tempo necessária para testá-la. Sem uma boa cobertura de testes, a equipe de testes não consegue escalar e os desenvolvedores eventualmente ficam enterrados em bugs.

Os desenvolvedores devem praticar o TDD (Test Driven Development), gravando testes de unidade com falha antes do código de produção que atende aos requisitos. O controle de qualidade deve criar um conjunto automatizado de testes de aceitação para garantir que o sistema funcione conforme o esperado de um alto nível.

Há estruturas personalizadas disponíveis, como Jackalope e Prosper, para tornar o zombamento de APIs JCR mais simples para garantir a produtividade dos desenvolvedores ao escrever testes de unidade.

### Prepare-se para a demonstração {#stay-demo-ready}

O sistema deve estar disponível para demonstração aos negócios no final de cada iteração. Ao manter o sistema em um estado pronto para demonstração, a equipe sempre estará dentro de uma iteração de estar pronta para produção e a dívida técnica pode ser mantida em um nível sustentável.

### Implementar um ambiente de integração contínua e usá-lo {#implement-a-continuous-integration-environment-and-use-it}

A implementação de um ambiente de integração contínua permite que você execute testes de unidade e de integração de forma fácil e repetitiva. Ele também desvincula as implantações da equipe de desenvolvimento, permitindo que as outras partes da equipe sejam mais eficientes e possibilitando implantações mais estáveis e previsíveis.

### Manter o ciclo de desenvolvimento rápido, mantendo os tempos de criação baixos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Se os testes de unidade demorarem muito para serem executados, os desenvolvedores evitarão executá-los e perderão o valor. Se levar muito tempo para criar o código e implantá-lo, as pessoas o farão com menos frequência. Tornar os tempos de criação curtos uma prioridade garante que o tempo investido na cobertura de testes e na infraestrutura de CI continue a tornar a equipe mais produtiva.

### Ajuste o Sonar e outras ferramentas de análise de código estático e atue em seus relatórios {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

As ferramentas de análise de código podem ser valiosas, mas somente se seus relatórios levarem à ação por parte da equipe de desenvolvimento. Sem o ajuste da análise que essas ferramentas oferecem, as recomendações que geram tornam-se irrelevantes e perdem seu valor.

### Siga a regra do Scout Boy {#follow-the-boy-scout-rule}

O Menino Scout tem uma regra: &quot;Deixe-o melhor do que você encontrou.&quot; Enquanto todos os membros da equipe de desenvolvimento aderirem a essa regra e limparem algo ao se deparar com uma bagunça, o código melhorará constantemente.

### Evitar a implementação de recursos YAGNI {#avoid-implementing-yagni-features}

Os recursos do YAGNI (You Are&#39;t Gonna Need It) são itens que são implementados quando esperamos que precisemos de algo no futuro, mesmo que não precisemos disso agora. Idealmente, devemos implementar a coisa mais simples que funcionará hoje e usar a refatoração contínua para garantir que a arquitetura do sistema evolua com os requisitos ao longo do tempo. Isso nos permite focar no que é importante e evitar o aumento excessivo de código e a deformação de recursos.
