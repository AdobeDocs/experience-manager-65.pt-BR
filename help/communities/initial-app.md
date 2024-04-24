---
title: Aplicativo de sandbox inicial
description: Saiba como usar o modelo de conteúdo usado para criar páginas de conteúdo e um componente e script usado para renderizar páginas do site.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# Aplicativo de sandbox inicial {#initial-sandbox-application}

Nesta seção, você cria o seguinte:

* A variável **[modelo](#createthepagetemplate)** que é usado para criar páginas de conteúdo no site de exemplo.
* A variável **[componente e script](#create-the-template-s-rendering-component)** que é usado para renderizar as páginas do site.

## Criar o modelo de conteúdo {#create-the-content-template}

Um modelo define o conteúdo padrão de uma nova página. Sites complexos podem usar vários modelos para criar os diferentes tipos de páginas no site. Além disso, o conjunto de modelos pode se tornar um blueprint usado para implantar alterações em um cluster de servidores.

Neste exercício, todas as páginas se baseiam em um modelo simples.

1. No painel do explorador do CRXDE Lite:

   * Selecionar `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Criar]** > **[!UICONTROL Criar modelo]**

1. Na caixa de diálogo Criar modelo, digite os seguintes valores e clique em **[!UICONTROL Próxima]**:

   * Etiqueta: `playpage`
   * Título: `An SCF Sandbox Play Template`
   * Descrição: `An SCF Sandbox template for play pages`
   * Tipo de recurso: `an-scf-sandbox/components/playpage`
   * Classificação: &lt;leave as=&quot;&quot; default=&quot;&quot;>

   O Label é usado para o nome do nó.

   O Tipo de recurso é exibido na `playpage`do `jcr:content` como a propriedade `sling:resourceType`. Ele identifica o componente (recurso) que renderiza o conteúdo quando solicitado por um navegador.

   Nesse caso, todas as páginas criadas usando o `playpage` modelo são renderizados pelo `an-scf-sandbox/components/playpage` componente. Por convenção, o caminho para o componente é relativo, permitindo que o Sling pesquise o recurso primeiro na variável `/apps` pasta e, se não for encontrada, no `/libs` pasta.

   ![create-content-template](assets/create-content-template-1.png)

1. Se estiver usando copiar/colar, verifique se o valor Tipo de recurso não tem espaços à esquerda ou à direita.

   Clique em **[!UICONTROL Avançar]**.

1. &quot;Caminhos permitidos&quot; refere-se aos caminhos das páginas que usam esse modelo, de modo que o modelo seja listado para o **[!UICONTROL Nova página]** diálogo.

   Para adicionar um caminho, clique no botão de adição `+` e tipo `/content(/.&ast;)?` na caixa de texto exibida. Se estiver usando copiar/colar, verifique se não há espaços à esquerda ou à direita.

   Observação: o valor da propriedade de caminho permitida é um *expressão regular*. As páginas de conteúdo que têm um caminho que corresponde à expressão podem usar o modelo. Nesse caso, a expressão regular corresponde ao caminho do **/content** pasta e todas as suas subpáginas.

   Quando um autor cria uma página abaixo de `/content`, o `playpage` O modelo chamado &quot;Um modelo de página de sandbox SCF&quot; aparece em uma lista de modelos disponíveis para uso.

   Depois que a página raiz é criada a partir do modelo, o acesso ao modelo pode ser restrito a este site editando a propriedade para incluir o caminho raiz na expressão regular.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Clique em **[!UICONTROL Avançar]**.

   Clique em **[!UICONTROL Próxima]** no **[!UICONTROL Pais permitidos]** painel.

   Clique em **[!UICONTROL Próxima]** no **[!UICONTROL Filhos permitidos]** painel.

   Clique em **[!UICONTROL OK]**.

1. Depois de clicar em OK e terminar de criar o modelo, observe os triângulos vermelhos que são exibidos nos cantos dos valores da guia Propriedades para o novo `playpage` modelo. Esses triângulos vermelhos indicam edições que não foram salvas.

   Clique em **[!UICONTROL Salvar tudo]** para salvar o novo modelo no repositório.

   ![verify-content-template](assets/verify-content-template.png)

### Criar o componente de renderização do modelo {#create-the-template-s-rendering-component}

Crie o *componente* que define o conteúdo e renderiza todas as páginas criadas com base na variável [modelo de página de reprodução](#createthepagetemplate).

1. No CRXDE Lite, clique com o botão direito do mouse em **`/apps/an-scf-sandbox/components`** e clique em **[!UICONTROL Criar > Componente]**.
1. Ao configurar o nome do nó (Rótulo) para *playpage*, o caminho para o componente é

   `/apps/an-scf-sandbox/components/playpage`

   que corresponde ao Tipo de recurso do modelo de página de reprodução (opcionalmente menos o valor **`/apps/`** parte do caminho).

   No **[!UICONTROL Criar componente]** digite os seguintes valores de propriedade:

   * Etiqueta: **playpage**
   * Título: **Um componente de reprodução de sandbox SCF**
   * Descrição: **Este é o componente que renderiza o conteúdo para a página Uma sandbox SCF.**
   * Supertipo: *&lt;leave blank=&quot;&quot;>*
   * Grupo: *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. Clique em **[!UICONTROL Próxima]** até que o **[!UICONTROL Filhos permitidos]** painel da caixa de diálogo aparece:

   * Clique em **[!UICONTROL OK]**.
   * Clique em **[!UICONTROL Salvar tudo]**.

1. Verifique se o caminho para o componente e o resourceType do modelo correspondem.

   >[!CAUTION]
   >
   >A correspondência entre o caminho para o componente de página de reprodução e o `sling:resourceType` do modelo de página de reprodução é crucial para o correto funcionamento do site.

   ![verify-template-component](assets/verify-template-component.png)
