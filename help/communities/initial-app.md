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
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# Aplicativo Sandbox Inicial {#initial-sandbox-application}

Nesta seção, você criará o seguinte:

* O **[modelo](#createthepagetemplate)**que será usado para criar páginas de conteúdo no site de exemplo.
* O **[componente e o script](#create-the-template-s-rendering-component)**que serão usados para renderizar as páginas do site.

## Criar o modelo de conteúdo {#create-the-content-template}

Um modelo define o conteúdo padrão de uma nova página. Sites complexos podem usar vários modelos para criar os diferentes tipos de páginas no site. Além disso, o conjunto de modelos pode se tornar um modelo usado para implantar alterações em um cluster de servidores.

Neste exercício, todas as páginas são baseadas em um modelo simples.

1. No painel explorador do CRXDE Lite:

   * Selecionar `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Criar]** > **[!UICONTROL Criar modelo]**

1. Na caixa de diálogo Criar modelo, digite os seguintes valores e clique em **[!UICONTROL Avançar]**:

   * Etiqueta: `playpage`
   * Título: `An SCF Sandbox Play Template`
   * Descrição: `An SCF Sandbox template for play pages`
   * Tipo de recurso: `an-scf-sandbox/components/playpage`
   * Classificação: &lt;deixar como padrão>
   O Rótulo é usado para o nome do nó.

   O Tipo de recurso é exibido no nó jcr:content `playpage`da propriedade `sling:resourceType`. Ela identifica o componente (recurso) que renderiza o conteúdo quando solicitado por um navegador.

   Nesse caso, todas as páginas criadas usando o `playpage` modelo são renderizadas pelo `an-scf-sandbox/components/playpage` componente. Por convenção, o caminho para o componente é relativo, permitindo que Sling procure o recurso primeiro na `/apps` pasta e, se não for encontrado, na `/libs` pasta.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Se estiver usando copiar/colar, verifique se o valor Tipo de recurso não tem espaços à esquerda ou à direita.

   Clique em **[!UICONTROL Avançar]**.

1. &quot;Caminhos permitidos&quot; refere-se aos caminhos das páginas que usam esse modelo, de modo que o modelo é listado para a caixa de diálogo **[!UICONTROL Nova página]** .

   Para adicionar um caminho, clique no botão de adição `+` e digite `/content(/.&ast;)?` na caixa de texto exibida. Se estiver usando copiar/colar, verifique se não há espaços à esquerda ou à direita.

   Observação: O valor da propriedade path permitida é uma expressão *regular.* As páginas de conteúdo com um caminho que corresponda à expressão podem usar o modelo. Nesse caso, a expressão regular corresponde ao caminho da pasta **/conteúdo** e de todas as suas subpáginas.

   Quando um autor cria uma página abaixo `/content`, o `playpage` modelo intitulado &quot;Um modelo de página de caixa de proteção SCF&quot; é exibido em uma lista de modelos disponíveis para uso.

   Depois que a página raiz é criada a partir do modelo, o acesso ao modelo pode ser restrito a este site modificando a propriedade para incluir o caminho raiz na expressão normal, isto é,

   `/content/an-scf-sandbox(/.&ast;)?`

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Clique em **[!UICONTROL Avançar]**.

   Clique em **[!UICONTROL Avançar]** no painel Pais **[!UICONTROL permitidos]** .

   Clique em **[!UICONTROL Avançar]** nos painéis Filhos **** permitidos.

   Clique em **[!UICONTROL OK]**.

1. Depois de clicar em OK e terminar de criar o modelo, você observará triângulos vermelhos mostrando nos cantos dos valores da guia Propriedades do novo `playpage` modelo. Esses triângulos vermelhos indicam edições que não foram salvas.

   Clique em **[!UICONTROL Salvar tudo]** para salvar o novo modelo no repositório.

   ![chlimage_1-77](assets/chlimage_1-77.png)

### Criar o componente de renderização do modelo {#create-the-template-s-rendering-component}

Crie o *componente* que define o conteúdo e renderiza todas as páginas criadas com base no modelo [de](#createthepagetemplate)página de reprodução.

1. No CRXDE Lite, clique com o botão direito do mouse **`/apps/an-scf-sandbox/components`** e clique em **[!UICONTROL Criar > Componente]**.
1. Ao definir o nome do nó (Rótulo) para a *página* de reprodução, o caminho para o componente é

   `/apps/an-scf-sandbox/components/playpage`

   que corresponde ao Tipo de recurso do modelo de página de reprodução (como opção, menos a parte inicial **`/apps/`** do caminho).

   Na caixa de diálogo **[!UICONTROL Criar componente]** , digite os seguintes valores de propriedade:

   * Rótulo: página **de reprodução**
   * Título: Componente **de reprodução de caixa de proteção SCF**
   * Descrição: **Este é o componente que renderiza conteúdo para a página de Caixa de proteção de SCF.**
   * Supertipo: *&lt;deixar em branco>*
   * Grupo:
   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Clique em **[!UICONTROL Avançar]** até que o painel Filhos **** permitidos da caixa de diálogo seja exibido:

   * Clique em **[!UICONTROL OK]**
   * Clique em **[!UICONTROL Salvar tudo]**

1. Verifique se o caminho para o componente e o resourceType para o modelo correspondem.

   >[!CAUTION]
   >
   >A correspondência entre o caminho para o componente de página de reprodução e a propriedade sling:resourceType do modelo de página de reprodução é crucial para o funcionamento correto do site.

   ![chlimage_1-79](assets/chlimage_1-79.png)