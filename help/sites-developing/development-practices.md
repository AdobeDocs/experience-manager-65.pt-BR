---
title: Práticas de desenvolvimento
seo-title: Development Practices
description: Práticas recomendadas para desenvolvimento em AEM
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

Cada equipe tem uma definição diferente do que significa &quot;feito&quot;, mas é importante ter um e garantir que uma história atenda aos critérios definidos antes de ser aceita.

Alguns critérios normalmente especificados por equipes incluem:

* Código revisado para formatação
* Comentários/Javadoc adicionados
* Atende aos níveis de cobertura de teste necessários
* Passa por testes de unidade e integração
* Validado no ambiente de controle de qualidade
* Localização implementada

Sem um DDO bem definido, é fácil chegar a uma situação em que muitas coisas estão a meio caminho e nada é verdadeiramente completo.

### Definir e aderir às convenções de codificação e formatação {#define-and-adhere-to-coding-and-formatting-conventions}

Coisas como níveis de recuo e espaço em branco podem não parecer importantes, mas ter um código corretamente formatado vai muito longe da legibilidade e da mantenibilidade. As convenções devem ser discutidas e acordadas como uma equipe e, em seguida, seguidas no código.

### Objetivo para cobertura de teste elevado  {#aim-for-high-test-coverage}

À medida que a implementação do projeto aumenta em tamanho, também aumenta a quantidade de tempo necessária para testá-la. Sem uma boa cobertura de teste, a equipe de testes não poderá ser dimensionada e os desenvolvedores acabarão se enterrando em insetos.

Os desenvolvedores devem praticar TDD, escrevendo testes de unidade com falha antes do código de produção que atenderá aos requisitos. O controle de qualidade deve criar um conjunto automatizado de testes de aceitação para garantir que o sistema funcione como esperado de um alto nível.

Há estruturas personalizadas disponíveis, como Jackalope e Prosper, para tornar a zombaria das APIs de JCR mais simples para garantir a produtividade dos desenvolvedores ao escrever testes de unidade.

### Fique pronto para demonstração {#stay-demo-ready}

O sistema deve estar disponível para demonstração à empresa no final de cada iteração. Ao manter o sistema em um estado pronto para demonstração, a equipe estará sempre dentro de uma iteração de estar pronta para produção e a dívida técnica poderá ser mantida em um nível sustentável.

### Implementar um ambiente de integração contínua e usá-lo {#implement-a-continuous-integration-environment-and-use-it}

A implementação de um ambiente de integração contínua permitirá que você execute testes de unidade e testes de integração de forma fácil e repetida. Também dissociará as implantações da equipe de desenvolvimento, permitindo que as outras partes da equipe sejam mais eficientes e permitindo implantações mais estáveis e previsíveis.

### Mantenha o ciclo de desenvolvimento rápido mantendo os tempos de compilação baixos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Se os testes de unidade levarem muito tempo para serem executados, os desenvolvedores evitarão executá-los e perderão seu valor. Se levar muito tempo para criar o código e implantá-lo, as pessoas farão isso com menos frequência. Tornar os tempos de compilação curtos uma prioridade garante que o tempo que investimos em nossa cobertura de teste e na infraestrutura de CI continuará a tornar a equipe mais produtiva.

### Ajustar o Sonar e outras ferramentas de análise de código estático e agir em seus relatórios {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

As ferramentas de análise de código podem ser valiosas, mas somente se seus relatórios levarem à ação da equipe de desenvolvimento. Sem ajustar a análise que essas ferramentas fornecem, as recomendações geradas não serão relevantes e perderão seu valor.

### Siga a regra Scout Boy {#follow-the-boy-scout-rule}

Os Scout têm uma regra: &quot;Deixe-o melhor do que você encontrou.&quot; Enquanto todos os membros da equipe de desenvolvimento aderirem a essa regra e limparem algo quando encontrarem uma bagunça, o código melhorará constantemente.

### Evite implementar recursos YAGNI {#avoid-implementing-yagni-features}

Os recursos de YAGNI (ou Você não vai precisar dele) são coisas que são implementadas quando esperamos que precisaremos de algo no futuro, mesmo que não precisemos disso agora. Idealmente, devemos implementar a coisa mais simples que funcionará hoje e usar a refatoração contínua para garantir que a arquitetura do sistema evolua com os requisitos ao longo do tempo. Isso nos permitirá focar no que importa e evitar o aumento do código e o aumento dos recursos.
