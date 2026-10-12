---
title: Criação de formulários acessíveis do HTML5
description: Os formulários HTML5 usam o padrão de acessibilidade ARIA HTML5. Esses formulários são compatíveis com a navegação com guias e são certificados para serem compatíveis com leitores de tela comuns.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%
---
# Criação de formulários acessíveis do HTML5 {#designing-accessible-html-forms}

Os formulários HTML5 usam o padrão de acessibilidade ARIA HTML5 para gerar formulários HTML acessíveis. Esses formulários são compatíveis com a navegação com guias (exceto o Mozilla FireFox) e são certificados para serem compatíveis com leitores de tela comuns. Para gerar um formulário HTML5 com bons recursos de acessibilidade, crie o modelo de formulário XFA com base em algumas diretrizes básicas de design. As diretrizes de design incluem a configuração da ordem de tabulação correta e o fornecimento do conteúdo de Fale Texto para cada controle de formulário. O AEM Forms Designer é compatível com a configuração desses atributos de controle de formulário para gerar um formulário do PDF e do HTML5 acessível.

A navegação de *Observação:Tabbed não abrange campos protegidos, como campos de cálculo que exibem a soma de valores. Para que o leitor de tela leia o valor de um campo protegido, coloque um campo somente leitura vazio na parte superior ou ao lado do campo protegido. Atribua o valor do campo protegido ao novo campo Somente leitura. O leitor de tela ou a navegação com guias pode escolher esse campo somente leitura e falar como o valor do campo protegido.*

O AEM Forms Designer inclui várias opções de Falar texto que podem ser passadas para leitores de tela. Para cada objeto em um formulário, o usuário pode especificar uma das várias configurações para o texto do leitor de tela:

* Texto do leitor de tela personalizado, que pode ser definido usando a paleta Acessibilidade. Os autores podem anotar os nomes de botões e campos e sua finalidade.
* Dicas de ferramentas, que podem ser definidas na paleta Acessibilidade.
* Legendas para campos no formulário.
* Nomes de objetos, conforme especificado na opção Nome da guia Vinculação.

![acessibilidade](assets/accessibility.png)

Quando várias opções, como dica de ferramenta, Texto da tela de Reader e Legenda estão disponíveis em um controle de Formulário, o Screen Reader usa apenas uma dessas propriedades. A ordem padrão é Texto Reader de tela personalizada, dica de ferramenta, Legenda e Nome. Você pode substituir a ordem padrão usando a opção **Precedência** do Screen Reader na paleta Acessibilidade.
