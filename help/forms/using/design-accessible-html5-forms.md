---
title: Criar formulários HTML5 acessíveis
seo-title: Criar formulários HTML5 acessíveis
description: Os formulários HTML5 usam o padrão de acessibilidade ARIA HTML5. Esses formulários oferecem suporte à navegação por guias e são certificados para serem compatíveis com leitores de tela comuns.
seo-description: Os formulários HTML5 usam o padrão de acessibilidade ARIA HTML5. Esses formulários oferecem suporte à navegação por guias e são certificados para serem compatíveis com leitores de tela comuns.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Criar formulários HTML5 acessíveis {#designing-accessible-html-forms}

Os formulários HTML5 usam o padrão de acessibilidade ARIA HTML5 para gerar formulários HTML acessíveis. Esses formulários oferecem suporte à navegação por guias (exceto o Mozilla FireFox) e são certificados para serem compatíveis com leitores de tela comuns. Para gerar um formulário HTML5 com bons recursos de acessibilidade, crie o modelo de formulário XFA com base em algumas diretrizes básicas de design. As diretrizes de design incluem configurar a ordem de tabulação correta e fornecer o conteúdo de Texto falado para cada controle de formulário. O AEM Forms Designer oferece suporte à configuração desses atributos de controle de formulário para gerar um formulário PDF e HTML5 acessíveis.

*Observação: a navegação com guias não cobre campos protegidos, como campos de cálculo que exibem a soma dos valores. Para que o leitor de tela leia o valor de um campo protegido, coloque um campo vazio somente leitura na parte superior ou ao lado do campo protegido. Atribua o valor do campo protegido ao novo campo Somente leitura. O leitor de tela ou a navegação com guias pode selecionar esse campo somente leitura e falar como o valor do campo protegido.*

O AEM Forms Designer inclui várias opções de Texto falado que podem ser passadas para leitores de tela. Para cada objeto em um formulário, o usuário pode especificar uma das várias configurações para o texto do leitor de tela:

* Texto personalizado do leitor de tela, que pode ser definido usando a paleta Acessibilidade. Os autores podem anotar os nomes de botões e campos, bem como sua finalidade.
* Dicas de ferramentas, que podem ser definidas na paleta Acessibilidade.
* Legendas para campos no formulário.
* Nomes de objetos, conforme especificado na opção Nome da guia Vínculo.

![acessibilidade](assets/accessibility.png)

Quando várias opções, como dica de ferramenta, Texto do leitor de tela e Legenda, estiverem disponíveis em um controle de Formulário, o Leitor de tela usará apenas uma dessas propriedades. A ordem padrão é Texto personalizado do leitor de tela, dica de ferramenta, Legenda e Nome. You can override the default order using the Screen Reader **Precedence** option in the Accessibility palette.
