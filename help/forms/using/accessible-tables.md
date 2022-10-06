---
title: Criar tabelas complexas acessíveis em formulários HTML5
seo-title: Create accessible complex tables in HTML5 forms
description: Saiba como criar tabelas acessíveis em formulários HTML5.
seo-description: Learn how to create accessible tables in HTML5 forms.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Criar tabelas complexas acessíveis em formulários HTML5 {#create-accessible-complex-tables-in-html-forms}

A implementação padrão de tabelas no HTML5 Forms usa elementos HTML DIV para renderizar uma tabela. A renderização envolve o uso de funções ARIA para atender aos requisitos de acessibilidade.

Para evitar problemas de acessibilidade com leitores de tela que não suportam totalmente as funções ARIA usadas com tabelas de dados, o HTML5 Forms fornece uma representação alternativa para as tabelas. Essas tabelas são baseadas no novo formato de tabela introduzido no Designer, que também suporta:

* Cabeçalhos de linha
* Intervalo de linha

Para usar o novo formato no HTML5 Forms, marque a tabela como complexa. Para marcar a tabela como complexa, adicione `extras` na origem XML do subformulário de tabela da seguinte maneira:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

As tabelas marcadas como *complexTable* siga a representação de HTML nativo e forneça melhor suporte de acessibilidade para determinados leitores de tela.  Para criar uma extensão de linha, selecione células consecutivas de uma tabela na mesma coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Mesclar células]**.

>[!NOTE]
>
>A criação de um span de linha funciona somente para as células mais à esquerda.

Para marcar uma linha como cabeçalho da linha, selecione todas as células na linha, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar Cabeçalho]**.

Para marcar uma célula como cabeçalho da coluna, selecione qualquer célula na coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar Cabeçalho]**.

Limitações em novas *TabelaAcessível* formato:

* Falta de suporte para campos que podem ser expandidos se a extensão da linha for usada na tabela
* Nenhum suporte para tabelas aninhadas (tabelas dentro de células da tabela)
* O suporte para expansão de linha é limitado às linhas de cabeçalho e células de cabeçalho
* O suporte é limitado a tabelas regulares
* Nenhum suporte para preenchimento prévio de dados em tabelas com duração > 1
