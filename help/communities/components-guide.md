---
title: Guia de componentes da comunidade
description: Uma ferramenta de desenvolvimento interativa para começar a usar a estrutura de componente social (SCF)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 0%

---

# Guia de componentes da comunidade  {#community-components-guide}

O guia Componentes da Comunidade é uma ferramenta de desenvolvimento interativa para a [estrutura do componente social (SCF)](scf.md). Ele fornece uma lista de componentes disponíveis das Comunidades Adobe Experience Manager (AEM) ou os recursos mais complexos criados com vários componentes.

Juntamente com as informações básicas de cada componente, o guia permite a experimentação de como os componentes/recursos do SCF funcionam e como eles podem ser configurados ou personalizados.

Para obter informações sobre os fundamentos de desenvolvimento relacionados a cada componente, consulte [Recursos e Componentes Essenciais](essentials.md).

## Introdução {#getting-started}

O guia deve ser usado em instalações de desenvolvimento de instâncias de autor (localhost:4502) e instâncias de publicação (localhost:4503).

O site Componentes da comunidade é acessado navegando até

* [https://&lt;servidor>:&lt;porta>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

As interações com os componentes das Comunidades variam de acordo com:

* O servidor (autor ou publicação).
* Se o visitante do site está conectado ou não.
* Se estiver conectado, os privilégios atribuídos ao membro.
* Se o SRP padrão, [JSRP](jsrp.md), está em uso.

No autor, para entrar no modo de edição, insira `editor.html` ou `cf#` como o primeiro segmento de caminho após o nome do servidor:

* Interface do usuário padrão:

  [https://&lt;servidor>:&lt;porta>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* Interface clássica:

  [https://&lt;servidor>:&lt;porta>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>Quando o autor está no modo de Edição, os links em uma página não estão ativos.
>
>Para navegar até uma página de componente, primeiro selecione o modo Visualização para ativar os links.
>
>Com a página do componente exibida no navegador, volte para o modo Editar para abrir a caixa de diálogo de edição do componente.
>
>Para obter informações gerais sobre criação, exiba o [guia rápido das páginas de criação](../../help/sites-authoring/qg-page-authoring.md).
>
>Se não estiver familiarizado com o AEM, exiba a documentação sobre [manipulação básica](../../help/sites-authoring/basic-handling.md).

### Página inicial {#home-page}

O guia fornece uma lista de componentes SCF disponíveis para visualização e protótipo no lado esquerdo da página.

O Guia de componentes conforme visualizado em uma instância do autor no modo Editar:

![componente1](assets/community-component1.png) da comunidade

## Páginas de componentes {#component-pages}

Selecione um componente na lista do lado esquerdo da página.

![páginas-componente-comunidade](assets/community-component2.png)

O corpo principal do guia é exibido:

1. Título: o nome do componente selecionado
1. [Bibliotecas do lado do cliente](#client-side-libraries): uma lista de uma ou mais categorias necessárias
1. [Incluível](scf.md#add-or-include-a-communities-component): se o componente puder ser incluído dinamicamente, o estado poderá ser alternado no modo de edição do autor:

   * Se adicionado, o texto exibido é: &quot;Este componente é incluído por meio de seu nó par&quot;.
   * Se incluído, o texto exibido é: &quot;Este componente é incluído dinamicamente&quot;.
   * Se não puder ser incluído, o texto não será exibido

1. Componente ou recurso de amostra: uma instância ativa do componente ou recurso. Se for um componente, ele poderá ser alterado com as alterações feitas nos modelos, CSS e dados fornecidos na seção da guia.

>[!NOTE]
>
>Depois de fazer uma seleção no lado esquerdo, o componente aparecerá abaixo, em vez de ao lado, da lista de componentes quando a janela do navegador for muito estreita.

### Interações do autor {#author-interactions}

Ao usar o guia em uma instância do autor, é possível executar a configuração de um componente abrindo a caixa de diálogo. As informações para desenvolvedores são fornecidas na seção [Component and Feature Essentials](essentials.md) da documentação, enquanto as configurações da caixa de diálogo são descritas na seção [Componentes de Comunidades](author-communities.md) para autores.

Para o guia Componentes da Comunidade, algumas configurações da caixa de diálogo de componentes são sobrepostas ao estado de alternância [Incluível](scf.md#add-or-include-a-communities-component). Para alternar entre o uso do recurso existente ou de um recurso incluído dinamicamente, no modo de edição, selecione o componente e o texto incluível e clique duas vezes para abrir a caixa de diálogo de edição:

![componente da comunidade3](assets/community-component3.png)

Na guia **Modelos**:

![componente-comunidade4](assets/community-component4.png)

* **Incluir o componente filho com sling:include**

  Se desmarcado, o Guia de componentes usará o recurso existente no repositório (um nó jcr que é filho de um nó par).

   * o texto exibido é: &quot;Este componente é incluído por meio de seu nó par&quot;.

  Se marcado, o Guia do componente usará o sling para incluir dinamicamente um componente do resourceType do nó secundário (recurso não existente).

   * o texto exibido é: &quot;Este componente é incluído dinamicamente.&quot;

  O padrão está desmarcado.

### Interações do Publish {#publish-interactions}

Ao usar o guia em uma instância de publicação, é possível experimentar os componentes e recursos como um visitante do site (não conectado) e como membros com vários privilégios quando conectados.

>[!NOTE]
>
>Observe que, se o SRP for deixado com o padrão [JSRP](jsrp.md), o UGC inserido na instância de publicação só estará visível na publicação e *não* ficará visível no console [moderação](moderate-ugc.md) na instância de autor.

## Bibliotecas do lado do cliente {#client-side-libraries}

As bibliotecas do lado do cliente (clientlibs) listadas para cada componente são aquelas *necessárias* para serem referenciadas quando o componente for colocado em uma página. As clientlibs fornecem um meio de gerenciar e otimizar o download do JavaScript e do CSS usados para renderizar o componente no navegador.

Para obter mais informações, visite [Clientlibs para Componentes de Comunidades](clientlibs.md).

## Representação {#impersonation}

Na instância do autor, onde geralmente há um usuário conectado como administrador ou desenvolvedor, para experimentar o componente conectado como outro usuário, use a caixa de texto à esquerda do botão **[!UICONTROL Representar]** para digitar o nome de usuário ou selecione na lista suspensa e clique no botão. Clique em Reverter para sair e encerrar a representação.

A instância de publicação não precisa representar. Basta usar o link Logon/Logout para representar vários usuários, como os [usuários de demonstração](tutorials.md#demo-users).

## Personalização {#customization}

Quando ativado, cada componente do SCF está disponível para prototipar de possíveis personalizações, modificando temporariamente o modelo, o CSS e os dados do componente.

### Habilitando a personalização {#enabling-customization}

>[!NOTE]
>
>**Esta ferramenta é somente leitura**. Nenhuma das edições feitas em modelos, CSS ou dados é salva no repositório.

Para experimentar rapidamente as personalizações, a propriedade `scg:showIde` deve ser adicionada ao nó JCR de conteúdo da página de componentes e definida como true.

Usando o componente de comentários como exemplo, na instância do autor ou de publicação, conectada com privilégios de administrador:

1. Navegar até [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Por exemplo, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Selecione o nó `jcr:content` do componente

   Por exemplo, `/content/community-components/en/comments/jcr:content`

1. Adicionar uma propriedade do

   * **Nome** `scg:showIde`
   * **Tipo** `String`
   * **Valor** `true`

1. Selecione **[!UICONTROL Salvar tudo]**
1. Recarregar a página Comentários no guia

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Observe que agora há três guias para Modelos, CSS e Dados.

![componente da comunidade5](assets/community-component5.png)

![componente da comunidade6](assets/community-component6.png)

### Guia Modelos {#templates-tab}

Selecione a guia templates para ver os templates associados ao componente.

O Editor de modelo permite que edições locais sejam compiladas e aplicadas à instância do componente de amostra na parte superior da página, sem afetar o componente no repositório.

Executar a compilação em edições locais destacará os erros ao colocar um ponto na medianiz e marcar o texto como vermelho.

### Guia CSS {#css-tab}

Selecione a guia CSS para ver o CSS associado ao componente.

Se um componente for composto por vários componentes, alguns CSS podem ser listados em um dos outros componentes.

O Editor de CSS permite que o CSS seja modificado e aplicado à instância do componente de amostra na parte superior da página.

Uma regra pode ser selecionada para realçar as partes do DOM que usam essa regra clicando ao lado da regra na medianiz.

### Guia Dados {#data-tab}

Selecione a guia Dados para mostrar os dados do ponto de extremidade .social.json. Esses dados são editáveis e são aplicados à instância do componente de amostra.

Os erros de sintaxe podem ser marcados na medianiz e destacados no editor.
