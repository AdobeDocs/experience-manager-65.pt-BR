---
title: Criar tabelas complexas acessíveis em formulários HTML5
description: Saiba como criar tabelas acessíveis em formulários HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Criar tabelas complexas acessíveis em formulários HTML5 {#create-accessible-complex-tables-in-html-forms}

A implementação padrão de tabelas no HTML5 Forms usa elementos HTML DIV para renderizar uma tabela. A renderização envolve o uso de funções ARIA para atender aos requisitos de acessibilidade.

Para evitar problemas de acessibilidade com leitores de tela que não suportam totalmente as funções ARIA usadas com tabelas de dados, o HTML5 Forms fornece uma representação alternativa para as tabelas. Essas tabelas são baseadas no novo formato de tabela introduzido no Designer, que também é compatível com:

* Cabeçalhos de linha
* Extensão de linha

Para usar o novo formato no HTML5 Forms, marque a tabela como complexa. Para marcar a tabela como complexa, adicione `extras` na fonte XML do subformulário da tabela da seguinte maneira:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

As tabelas marcadas como *complexTable* siga a representação de HTML nativa e forneça um melhor suporte de acessibilidade para determinados leitores de tela.  Para criar uma extensão de linha, selecione células consecutivas de uma tabela na mesma coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Mesclar Células]**.

>[!NOTE]
>
>A criação de uma extensão de linha funciona somente para as células mais à esquerda.

Para marcar uma linha como cabeçalho da linha, selecione todas as células na linha, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar Cabeçalho]**.

Para marcar uma célula como cabeçalho da coluna, selecione qualquer célula na coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar Cabeçalho]**.

Limitações em novos *AccessibleTable* formato:

* Falta de suporte para campos que podem ser expandidos se rowspan for usado na tabela
* Não há suporte para tabelas aninhadas (tabelas dentro de células de tabela)
* A compatibilidade com rowspan é limitada às linhas e células do cabeçalho
* Suporte limitado a tabelas regulares
* Não há suporte para preenchimentos prévios de dados em tabelas com rowspan > 1
