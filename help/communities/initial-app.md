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

* O **[modelo](#createthepagetemplate)** que é usado para criar páginas de conteúdo no site de exemplo.
* O **[componente e o script](#create-the-template-s-rendering-component)** usados para renderizar as páginas do site.

## Criar o modelo de conteúdo {#create-the-content-template}

Um modelo define o conteúdo padrão de uma nova página. Sites complexos podem usar vários modelos para criar os diferentes tipos de páginas no site. Além disso, o conjunto de modelos pode se tornar um blueprint usado para implantar alterações em um cluster de servidores.

Neste exercício, todas as páginas se baseiam em um modelo simples.

1. No painel do explorador do CRXDE Lite:

   * Selecionar `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Criar]** > **[!UICONTROL Criar Modelo]**

1. Na caixa de diálogo Criar Modelo, digite os seguintes valores e clique em **[!UICONTROL Avançar]**:

   * Rótulo: `playpage`
   * Título: `An SCF Sandbox Play Template`
   * Descrição: `An SCF Sandbox template for play pages`
   * Tipo de recurso: `an-scf-sandbox/components/playpage`
   * Classificação: &lt;deixar como padrão>

   O Label é usado para o nome do nó.

   O Tipo de Recurso aparece no nó `jcr:content` de `playpage` como a propriedade `sling:resourceType`. Ele identifica o componente (recurso) que renderiza o conteúdo quando solicitado por um navegador.

   Nesse caso, todas as páginas criadas usando o modelo `playpage` são renderizadas pelo componente `an-scf-sandbox/components/playpage`. Por convenção, o caminho para o componente é relativo, permitindo que o Sling pesquise o recurso primeiro na pasta `/apps` e, se não for encontrado, na pasta `/libs`.

   ![criar-modelo-conteúdo](assets/create-content-template-1.png)

1. Se estiver usando copiar/colar, verifique se o valor Tipo de recurso não tem espaços à esquerda ou à direita.

   Clique em **[!UICONTROL Avançar]**.

1. &quot;Caminhos permitidos&quot; refere-se aos caminhos das páginas que usam este modelo, de forma que o modelo seja listado para a caixa de diálogo **[!UICONTROL Nova página]**.

   Para adicionar um caminho, clique no botão de adição `+` e digite `/content(/.&ast;)?` na caixa de texto exibida. Se estiver usando copiar/colar, verifique se não há espaços à esquerda ou à direita.

   Observação: o valor da propriedade de caminho permitida é uma *expressão regular*. As páginas de conteúdo que têm um caminho que corresponde à expressão podem usar o modelo. Nesse caso, a expressão regular corresponde ao caminho da pasta **/content** e de todas as suas subpáginas.

   Quando um autor cria uma página abaixo de `/content`, o modelo `playpage` intitulado &quot;Um Modelo de Página de Sandbox do SCF&quot; aparece em uma lista de modelos disponíveis para uso.

   Depois que a página raiz é criada a partir do modelo, o acesso ao modelo pode ser restrito a este site editando a propriedade para incluir o caminho raiz na expressão regular.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![caminho-configuração-modelo](assets/configure-template-path.png)

1. Clique em **[!UICONTROL Avançar]**.

   Clique em **[!UICONTROL Avançar]** no painel **[!UICONTROL Pais permitidos]**.

   Clique em **[!UICONTROL Avançar]** no painel **[!UICONTROL Filhos permitidos]**.

   Clique em **[!UICONTROL OK]**.

1. Depois de clicar em OK e concluir a criação do modelo, observe os triângulos vermelhos que são exibidos nos cantos dos valores da guia Propriedades do novo modelo `playpage`. Esses triângulos vermelhos indicam edições que não foram salvas.

   Clique em **[!UICONTROL Salvar tudo]** para salvar o novo modelo no repositório.

   ![verificar-modelo-conteúdo](assets/verify-content-template.png)

### Criar o componente de renderização do modelo {#create-the-template-s-rendering-component}

Crie o *componente* que define o conteúdo e renderiza todas as páginas criadas com base no [modelo de página de reprodução](#createthepagetemplate).

1. No CRXDE Lite, clique com o botão direito do mouse em **`/apps/an-scf-sandbox/components`** e clique em **[!UICONTROL Criar > Componente]**.
1. Ao configurar o nome do nó (Rótulo) como *playpage*, o caminho para o componente será

   `/apps/an-scf-sandbox/components/playpage`

   que corresponde ao Tipo de recurso do modelo de página de reprodução (opcionalmente menos a parte **`/apps/`** inicial do caminho).

   Na caixa de diálogo **[!UICONTROL Criar Componente]**, digite os seguintes valores de propriedade:

   * Rótulo: **playpage**
   * Título: **Um Componente de Reprodução de Sandbox do SCF**
   * Descrição: **Este é o componente que renderiza conteúdo para uma página de Sandbox SCF.**
   * Supertipo: *&lt;deixe em branco>*
   * Grupo: *&lt;deixe em branco>*

   ![criar-componente-modelo](assets/create-template-component.png)

1. Clique em **[!UICONTROL Avançar]** até que o painel **[!UICONTROL Filhos permitidos]** da caixa de diálogo seja exibido:

   * Clique em **[!UICONTROL OK]**.
   * Clique em **[!UICONTROL Salvar tudo]**.

1. Verifique se o caminho para o componente e o resourceType do modelo correspondem.

   >[!CAUTION]
   >
   >A correspondência entre o caminho para o componente de página de reprodução e a propriedade `sling:resourceType` do modelo de página de reprodução é crucial para o funcionamento correto do site.

   ![verificar-modelo-componente](assets/verify-template-component.png)
