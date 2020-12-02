---
title: Aplicativo Sandbox Inicial
seo-title: Aplicativo Sandbox Inicial
description: Criar modelo, componente e script
seo-description: Criar modelo, componente e script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---


# Aplicativo Sandbox Inicial {#initial-sandbox-application}

Nesta seção, você criará o seguinte:

* O **[modelo](#createthepagetemplate)** que será usado para criar páginas de conteúdo no site de exemplo.
* O componente **[e o script](#create-the-template-s-rendering-component)** que serão usados para renderizar as páginas do site.

## Criar o modelo de conteúdo {#create-the-content-template}

Um modelo define o conteúdo padrão de uma nova página. Sites complexos podem usar vários modelos para criar os diferentes tipos de páginas no site. Além disso, o conjunto de modelos pode se tornar um modelo usado para implantar alterações em um cluster de servidores.

Neste exercício, todas as páginas são baseadas em um modelo simples.

1. No painel explorador de CRXDE Lite:

   * Selecionar `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Criar]** >  **[!UICONTROL Criar modelo]**

1. Na caixa de diálogo Criar modelo, digite os seguintes valores e clique em **[!UICONTROL Próximo]**:

   * Etiqueta: `playpage`
   * Título: `An SCF Sandbox Play Template`
   * Descrição: `An SCF Sandbox template for play pages`
   * Tipo de recurso: `an-scf-sandbox/components/playpage`
   * Classificação: &lt;deixar como padrão>

   O Rótulo é usado para o nome do nó.

   O Tipo de recurso aparece no nó jcr:content de `playpage` como a propriedade `sling:resourceType`. Ela identifica o componente (recurso) que renderiza o conteúdo quando solicitado por um navegador.

   Nesse caso, todas as páginas criadas usando o modelo `playpage` são renderizadas pelo componente `an-scf-sandbox/components/playpage`. Por convenção, o caminho para o componente é relativo, permitindo que Sling procure o recurso primeiro na pasta `/apps` e, se não for encontrado, na pasta `/libs`.

   ![create-content-template](assets/create-content-template-1.png)

1. Se estiver usando copiar/colar, verifique se o valor Tipo de recurso não tem espaços à esquerda ou à direita.

   Clique em **[!UICONTROL Avançar]**.

1. &quot;Caminhos permitidos&quot; refere-se aos caminhos das páginas que usam esse modelo, de modo que o modelo está listado para a caixa de diálogo **[!UICONTROL Nova página]**.

   Para adicionar um caminho, clique no botão de mais `+` e digite `/content(/.&ast;)?` na caixa de texto que é exibida. Se estiver usando copiar/colar, verifique se não há espaços à esquerda ou à direita.

   Observação: O valor da propriedade de caminho permitida é uma *expressão regular*. As páginas de conteúdo com um caminho que corresponda à expressão podem usar o modelo. Nesse caso, a expressão regular corresponde ao caminho da pasta **/content** e de todas as suas subpáginas.

   Quando um autor cria uma página abaixo de `/content`, o modelo `playpage` intitulado &quot;An SCF Sandbox Page Template&quot; aparece em uma lista de modelos disponíveis para uso.

   Depois que a página raiz é criada a partir do modelo, o acesso ao modelo pode ser restrito a este site modificando a propriedade para incluir o caminho raiz na expressão normal, isto é,

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Clique em **[!UICONTROL Avançar]**.

   Clique em **[!UICONTROL Próximo]** no painel **[!UICONTROL Pais permitidos]**.

   Clique em **[!UICONTROL Próximo]** nos painéis **[!UICONTROL Filhos permitidos]**.

   Clique em **[!UICONTROL OK]**.

1. Depois de clicar em OK e terminar de criar o modelo, você observará triângulos vermelhos mostrando nos cantos dos valores da guia Propriedades do novo modelo `playpage`. Esses triângulos vermelhos indicam edições que não foram salvas.

   Clique em **[!UICONTROL Salvar tudo]** para salvar o novo modelo no repositório.

   ![verify-content-template](assets/verify-content-template.png)

### Criar o componente de renderização do modelo {#create-the-template-s-rendering-component}

Crie o *componente* que define o conteúdo e renderiza quaisquer páginas criadas com base no [modelo de página de reprodução](#createthepagetemplate).

1. No CRXDE Lite, clique com o botão direito do mouse em **`/apps/an-scf-sandbox/components`** e clique em **[!UICONTROL Criar > Componente]**.
1. Ao definir o nome do nó (Rótulo) como *playpage*, o caminho para o componente é

   `/apps/an-scf-sandbox/components/playpage`

   que corresponde ao Tipo de recurso do modelo de página de reprodução (como opção, menos a parte inicial **`/apps/`** do caminho).

   Na caixa de diálogo **[!UICONTROL Criar componente]**, digite os seguintes valores de propriedade:

   * Rótulo: **playpage**
   * Título: **Um Componente de Reprodução de Caixa de Segurança SCF**
   * Descrição: **Este é o componente que renderiza conteúdo para uma página de Caixa de Proteção SCF.**
   * Supertipo: *&lt;deixar em branco>*
   * Grupo: *&lt;deixar em branco>*

   ![create-template-component](assets/create-template-component.png)

1. Clique em **[!UICONTROL Próximo]** até que o painel **[!UICONTROL Filhos permitidos]** da caixa de diálogo seja exibido:

   * Clique em **[!UICONTROL OK]**.
   * Clique em **[!UICONTROL Salvar tudo]**.

1. Verifique se o caminho para o componente e o resourceType para o modelo correspondem.

   >[!CAUTION]
   >
   >A correspondência entre o caminho para o componente de página de reprodução e a propriedade sling:resourceType do modelo de página de reprodução é crucial para o funcionamento correto do site.

   ![verify-template-component](assets/verify-template-component.png)