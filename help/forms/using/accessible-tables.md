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
source-wordcount: '280'
ht-degree: 0%
---
# Criar tabelas complexas acessíveis em formulários HTML5 {#create-accessible-complex-tables-in-html-forms}

A implementação padrão de tabelas no HTML5 Forms usa elementos HTML DIV para renderizar uma tabela. A renderização envolve o uso de funções ARIA para atender aos requisitos de acessibilidade.

Para evitar problemas de acessibilidade com leitores de tela que não suportam totalmente as funções ARIA usadas com tabelas de dados, o HTML5 Forms fornece uma representação alternativa para as tabelas. Essas tabelas são baseadas no novo formato de tabela introduzido no Designer, que também é compatível com:

* Cabeçalhos de linha
* Extensão de linha

Para usar o novo formato no HTML5 Forms, marque a tabela como complexa. Para marcar a tabela como complexa, adicione a marca `extras` na fonte XML do subformulário de tabela da seguinte maneira:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

As tabelas marcadas como *complexTable* seguem a representação nativa do HTML e oferecem melhor suporte à acessibilidade para determinados leitores de tela.  Para criar uma extensão de linha, selecione células consecutivas de uma tabela na mesma coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Mesclar Células]**.

>[!NOTE]
>
>A criação de uma extensão de linha funciona somente para as células mais à esquerda.

Para marcar uma linha como cabeçalho de linha, selecione todas as células na linha, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar Cabeçalho]**.

Para marcar uma célula como cabeçalho da coluna, selecione qualquer célula na coluna, clique com o botão direito do mouse na seleção e clique em **[!UICONTROL Marcar Cabeçalho]**.

Limitações no novo formato *AccessibleTable*:

* Falta de suporte para campos que podem ser expandidos se rowspan for usado na tabela
* Não há suporte para tabelas aninhadas (tabelas dentro de células de tabela)
* A compatibilidade com rowspan é limitada às linhas e células do cabeçalho
* Suporte limitado a tabelas regulares
* Não há suporte para preenchimentos prévios de dados em tabelas com rowspan > 1
