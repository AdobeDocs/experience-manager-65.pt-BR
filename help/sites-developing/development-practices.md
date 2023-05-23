---
title: Práticas de desenvolvimento
seo-title: Development Practices
description: Práticas recomendadas para o desenvolvimento no AEM
seo-description: Best practices for developing on AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# Práticas de desenvolvimento{#development-practices}

## Trabalhar de acordo com uma definição de concluído {#work-according-to-a-definition-of-done}

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

À medida que a implementação de um projeto cresce em tamanho, também aumentará o tempo necessário para testá-la. Sem uma boa cobertura de testes, a equipe de testes não poderá ser dimensionada e os desenvolvedores acabarão sendo enterrados em erros.

Os desenvolvedores devem praticar o TDD, escrevendo testes de unidade com falha antes do código de produção que atenderá a seus requisitos. O controle de qualidade deve criar um conjunto automatizado de testes de aceitação para garantir que o sistema funcione conforme o esperado de um alto nível.

Há estruturas personalizadas disponíveis, como Jackalope e Prosper, para tornar o zombamento de APIs JCR mais simples para garantir a produtividade dos desenvolvedores ao escrever testes de unidade.

### Prepare-se para a demonstração {#stay-demo-ready}

O sistema deve estar disponível para demonstração aos negócios no final de cada iteração. Ao manter o sistema em um estado pronto para demonstração, a equipe sempre estará dentro de uma iteração de estar pronta para produção e a dívida técnica pode ser mantida em um nível sustentável.

### Implementar um ambiente de integração contínua e usá-lo {#implement-a-continuous-integration-environment-and-use-it}

A implementação de um ambiente de integração contínua permitirá que você execute testes de unidade e de integração de maneira fácil e repetitiva. Ele também dissociará as implantações da equipe de desenvolvimento, permitindo que as outras partes da equipe sejam mais eficientes e possibilitando implantações mais estáveis e previsíveis.

### Manter o ciclo de desenvolvimento rápido, mantendo os tempos de criação baixos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Se os testes de unidade demorarem muito para serem executados, os desenvolvedores evitarão executá-los e perderão o valor. Se levar muito tempo para criar o código e implantá-lo, as pessoas o farão com menos frequência. Tornar os tempos de compilação curtos uma prioridade garante que o tempo investido em nossa cobertura de teste e infraestrutura de CI continue a tornar a equipe mais produtiva.

### Ajuste o Sonar e outras ferramentas de análise de código estático e atue em seus relatórios {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

As ferramentas de análise de código podem ser valiosas, mas somente se seus relatórios levarem à ação por parte da equipe de desenvolvimento. Sem o ajuste da análise fornecida por essas ferramentas, as recomendações geradas não serão relevantes e perderão seu valor.

### Siga a regra do Scout Boy {#follow-the-boy-scout-rule}

O Menino Scout tem uma regra: &quot;Deixe-o melhor do que você encontrou.&quot; Enquanto todos os membros da equipe de desenvolvimento aderirem a essa regra e limparem algo ao se deparar com uma bagunça, o código melhorará constantemente.

### Evitar a implementação de recursos YAGNI {#avoid-implementing-yagni-features}

Os recursos do YAGNI (ou Você não vai precisar) são itens que são implementados quando esperamos que precisemos de algo no futuro, mesmo que não precisemos disso agora. Idealmente, devemos implementar a coisa mais simples que funcionará hoje e usar a refatoração contínua para garantir que a arquitetura do sistema evolua com os requisitos ao longo do tempo. Isso nos permitirá focar no que é importante e evitar o aumento do código e a deformação de recursos.
