---
title: Guia de componentes da comunidade
seo-title: Guia de componentes da comunidade
description: Uma ferramenta de desenvolvimento interativo para começar a usar a estrutura de componentes sociais (SCF)
seo-description: Uma ferramenta de desenvolvimento interativo para começar a usar a estrutura de componentes sociais (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
translation-type: tm+mt
source-git-commit: 3da113e88784def54e0a94e280bf1a965de015ed
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 2%

---


# Guia de componentes da comunidade  {#community-components-guide}

O guia Community Components é uma ferramenta de desenvolvimento interativo para o quadro de componentes [sociais (SCF)](scf.md). Ele fornece uma lista de componentes AEM Communities disponíveis ou os recursos mais complexos criados com vários componentes.

Juntamente com as informações básicas de cada componente, o guia permite experimentar como os componentes/recursos do SCF funcionam e como eles podem ser configurados ou personalizados.

Para obter informações sobre o desenvolvimento essencial relacionado a cada componente, consulte [Recurso e Componentes essenciais](essentials.md).

## Introdução {#getting-started}

O guia é destinado ao uso em instalações de desenvolvimento de instâncias do autor (localhost:4502) e de publicação (localhost:4503).

O site Componentes da comunidade é acessado navegando até

* [https://&lt;servidor>:&lt;porta>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

As interações com os componentes das Comunidades variam, dependendo de:

* O servidor (autor ou publicação).
* Se o visitante do site está conectado ou não.
* Se conectado, os privilégios atribuídos ao membro.
* Se o SRP padrão, [JSRP](jsrp.md), está ou não em uso.

No autor, para entrar no modo de edição, insira `editor.html` ou `cf#` como o primeiro segmento de caminho após o nome do servidor:

* Interface do usuário padrão:

   [https://&lt;servidor>:&lt;porta>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* Interface clássica:

   [https://&lt;servidor>:&lt;porta>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>No modo Editar, os links em uma página não estão ativos.
>
>Para navegar até uma página de componente, primeiro selecione o modo de Pré-visualização para ativar os links.
>
>Com a página do componente exibida no navegador, volte ao modo de Edição para abrir a caixa de diálogo de edição do componente.
>
>Para obter informações gerais sobre criação, visualização no guia [rápido para criar páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>Se não estiver familiarizado com AEM, visualização a documentação sobre manuseio [](../../help/sites-authoring/basic-handling.md)básico.


### Página Inicial {#home-page}

O guia fornece uma lista de componentes SCF disponíveis para pré-visualização e prototipagem no lado esquerdo da página.

Guia de componentes conforme exibido em uma instância do autor no modo Editar:

![community-component1](assets/community-component1.png)

## Páginas de componentes {#component-pages}

Selecione um componente da lista no lado esquerdo da página.

![páginas de componentes da comunidade](assets/community-component2.png)

O corpo principal da guia exibe:

1. Título: O nome do componente selecionado
1. [Bibliotecas](#client-side-libraries)do lado do cliente: Uma lista de uma ou mais categorias necessárias
1. [Incluível](scf.md#add-or-include-a-communities-component): Se o componente puder ser incluído dinamicamente, o estado pode ser alternado no modo de edição do autor:

   * Se adicionado, o texto exibido é: &quot;Esse componente é incluído por meio de seu nó par.&quot;
   * Se incluído, o texto exibido é: &quot;Esse componente é incluído dinamicamente.&quot;
   * Se não for incluível, nenhum texto será exibido

1. Componente de amostra ou recurso: uma instância ativa do componente ou recurso. Se um componente, ele pode ser alterado com alterações feitas nos modelos, CSS e dados fornecidos na seção da guia.

>[!NOTE]
>
>Depois de fazer uma seleção no lado esquerdo, o componente aparecerá abaixo, em vez de ao lado, da lista de componentes quando a janela do navegador for muito estreita.

### Interações do autor {#author-interactions}

Ao usar o guia em uma instância do autor, é possível experimentar a configuração de um componente abrindo sua caixa de diálogo. As informações para desenvolvedores são fornecidas na seção [Component and Feature Essentials](essentials.md) da documentação, enquanto as configurações da caixa de diálogo são descritas na seção [Communities Components](author-communities.md) (Componentes de comunidades) para autores.

Para o guia Componentes da comunidade, algumas configurações de diálogo do componente são sobrepostas com o estado de alternância [Incluível](scf.md#add-or-include-a-communities-component) . Para alternar entre o uso do recurso existente ou de um recurso incluído dinamicamente, no modo de edição, selecione o componente e o texto e clique em duplo para abrir a caixa de diálogo de edição:

![community-component3](assets/community-component3.png)

Na guia **Modelos** :

![community-component4](assets/community-component4.png)

* **Incluir o componente-filho com sling:include**

   Se desmarcada, o Guia de componentes usará o recurso existente no repositório (um nó jcr que é filho de um nó par).

   * o texto exibido é: &quot;Esse componente é incluído por meio de seu nó par.&quot;

   Se marcada, o Guia de componentes usará sling para incluir dinamicamente um componente do resourceType do nó filho (recurso não existente).

   * o texto exibido é: &quot;Esse componente é incluído dinamicamente.&quot;

   O padrão está desmarcado.

### Publicar interações {#publish-interactions}

Ao usar o guia em uma instância de publicação, é possível experimentar os componentes e os recursos como um visitante do site (não conectado) e como membros com vários privilégios ao fazer logon.

>[!NOTE]
>
>Observe que, se o SRP for deixado como padrão para [JSRP](jsrp.md), o UGC inserido na instância de publicação estará visível somente na publicação e *não* estará visível do console de [moderação](moderate-ugc.md) na instância do autor.

## Bibliotecas do lado do cliente {#client-side-libraries}

As bibliotecas do lado do cliente (clientlibs) listadas para cada componente são aquelas *necessárias* para serem referenciadas quando o componente é colocado em uma página. Os clientlibs fornecem um meio de gerenciar e otimizar o download do Javascript e do CSS usados para renderizar o componente no navegador.

Para obter mais informações, visite [Clientlibs for Communities Components (Clientlibs para componentes](clientlibs.md)de comunidades).

## Representação {#impersonation}

Na instância do autor, em que um deles é frequentemente conectado como administrador ou desenvolvedor, para experimentar o componente conectado como outro usuário, use a caixa de texto à esquerda do botão **[!UICONTROL Representar]** para digitar no nome de usuário ou selecionar na lista suspensa e clique no botão. Clique em Reverter para sair e encerrar a representação.

A instância de publicação não precisa representar. Basta usar o link Logon/Logout para representar vários usuários, como os usuários [da](tutorials.md#demo-users)demonstração.

## Personalização {#customization}

Quando ativado, cada componente SCF está disponível para prototipagem de possíveis personalizações modificando temporariamente o modelo do componente, o CSS e os dados.

### Ativação da personalização {#enabling-customization}

>[!NOTE]
>
>**Esta ferramenta é somente** leitura. Nenhuma das edições feitas nos modelos, CSS ou dados são salvas no repositório.

Para experimentar rapidamente personalizações, a `scg:showIde`propriedade deve ser adicionada ao nó do JCR de conteúdo da página do componente e definida como true.

Usando o componente comments como um exemplo, na instância autor ou de publicação, conectado com privilégios de administrador:

1. Navegue até [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Por exemplo, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Selecionar o `jcr:content` nó do componente

   Por exemplo, `/content/community-components/en/comments/jcr:content`

1. Adicionar uma propriedade

   * **Nome** `scg:showIde`
   * **Tipo** `String`
   * **Valor** `true`

1. Selecione **[!UICONTROL Salvar tudo]**
1. Recarregar a página Comentários no guia

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Observe que agora há 3 guias para Modelos, CSS e Dados.

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### Guia Modelos {#templates-tab}

Selecione a guia modelos para ver os modelos associados ao componente.

O Editor de modelos permite que as edições locais sejam compiladas e aplicadas à instância do componente de amostra na parte superior da página, sem afetar o componente no repositório.

Executar a compilação em edições locais destacará quaisquer erros ao colocar um ponto na medianiz e marcar o texto em vermelho.

### Guia CSS {#css-tab}

Selecione a guia CSS para ver o CSS associado ao componente.

Se um componente for um composto de vários componentes, alguns CSS podem ser listados em um dos outros componentes.

O Editor de CSS permite que o CSS seja modificado e aplicado à instância do componente de amostra na parte superior da página.

Uma regra pode ser selecionada para realçar as partes do DOM usando essa regra clicando em ao lado da regra na medianiz.

### Guia Dados {#data-tab}

Selecione a guia Dados para mostrar os dados do ponto de extremidade .social.json. Esses dados são editáveis e são aplicados à instância do componente de amostra.

Os erros de sintaxe podem ser marcados na medianiz, bem como destacados no editor.
