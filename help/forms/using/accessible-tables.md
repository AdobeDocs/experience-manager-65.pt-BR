---
title: Criar tabelas complexas acessíveis em formulários HTML5
seo-title: Criar tabelas complexas acessíveis em formulários HTML5
description: Saiba como criar tabelas acessíveis em formulários HTML5.
seo-description: Saiba como criar tabelas acessíveis em formulários HTML5.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Criar tabelas complexas acessíveis em formulários HTML5 {#create-accessible-complex-tables-in-html-forms}

A implementação padrão de tabelas no HTML5 Forms usa elementos DIV HTML para renderizar uma tabela. A renderização envolve o uso de funções ARIA para atender aos requisitos de acessibilidade.

Para evitar problemas de acessibilidade com leitores de tela que não suportam totalmente as funções ARIA usadas com tabelas de dados, o HTML5 Forms fornece uma execução alternativa para as tabelas. Essas tabelas são baseadas no novo formato de tabela introduzido no Designer, que também oferece suporte a:

* Cabeçalhos de Linha
* Intervalo de linha

Para usar o novo formato no HTML5 Forms, marque a tabela como complexa. Para marcar a tabela como complexa, adicione `extras` tag à fonte XML do subformulário de tabela da seguinte maneira:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

As tabelas marcadas como *complexasTable* seguem a execução HTML nativa e fornecem melhor suporte de acessibilidade para determinados leitores de tela.  Para criar uma extensão de linha, selecione células consecutivas de uma tabela na mesma coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Unir células]**.

>[!NOTE]
>
>A criação de uma extensão de linha funciona somente para células na extremidade esquerda.

Para marcar uma linha como cabeçalho de linha, selecione todas as células na linha, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar cabeçalho]**.

Para marcar uma célula como cabeçalho da coluna, selecione qualquer célula na coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar cabeçalho]**.

Limitações no novo formato *AccessibleTable* :

* Falta de suporte para campos com capacidade de expansão se a extensão de linha for usada na tabela
* Não há suporte para tabelas aninhadas (tabelas dentro de células de tabela)
* O suporte para a extensão de linha está limitado às linhas de cabeçalho e células de cabeçalho
* O suporte é limitado a tabelas regulares
* Não há suporte para preenchimento prévio de dados em tabelas com expansão de linhas > 1

