---
title: Criação de formulários HTML5 acessíveis
seo-title: Designing accessible HTML5 forms
description: Os formulários HTML5 usam o padrão de acessibilidade ARIA HTML5. Esses formulários são compatíveis com a navegação com guias e são certificados para serem compatíveis com leitores de tela comuns.
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Criação de formulários HTML5 acessíveis {#designing-accessible-html-forms}

Os formulários HTML5 usam o padrão de acessibilidade ARIA HTML5 para gerar formulários HTML acessíveis. Esses formulários são compatíveis com a navegação com guias (exceto o Mozilla FireFox) e são certificados para serem compatíveis com leitores de tela comuns. Para gerar um formulário HTML5 com bons recursos de acessibilidade, crie o modelo de formulário XFA com base em algumas diretrizes básicas de design. As diretrizes de design incluem a configuração da ordem de tabulação correta e o fornecimento do conteúdo de Fale Texto para cada controle de formulário. O AEM Forms Designer é compatível com a configuração desses atributos de controle de formulário para gerar um formulário PDF e HTML acessíveis.

*Nota:A navegação com guias não abrange campos protegidos, como campos de cálculo que exibem a soma dos valores. Para que o leitor de tela leia o valor de um campo protegido, coloque um campo somente leitura vazio na parte superior ou ao lado do campo protegido. Atribua o valor do campo protegido ao novo campo Somente leitura. O leitor de tela ou a navegação com guias pode escolher esse campo somente leitura e falar como o valor do campo protegido.*

O AEM Forms Designer inclui várias opções de Falar texto que podem ser passadas para leitores de tela. Para cada objeto em um formulário, o usuário pode especificar uma das várias configurações para o texto do leitor de tela:

* Texto do leitor de tela personalizado, que pode ser definido usando a paleta Acessibilidade. Os autores podem anotar os nomes de botões e campos, bem como sua finalidade.
* Dicas de ferramentas, que podem ser definidas na paleta Acessibilidade.
* Legendas para campos no formulário.
* Nomes de objetos, conforme especificado na opção Nome da guia Vinculação.

![acessibilidade](assets/accessibility.png)

Quando várias opções como dica de ferramenta, Texto de Reader da tela e Legenda estão disponíveis em um controle de Formulário, o Reader da tela usa apenas uma dessas propriedades. A ordem padrão é Texto de Reader de tela personalizada, dica de ferramenta, Legenda e Nome. Você pode substituir a ordem padrão usando o Reader de tela **Precedência** na paleta Acessibilidade.
