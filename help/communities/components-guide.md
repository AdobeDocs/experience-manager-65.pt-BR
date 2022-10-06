---
title: Guia de componentes da comunidade
seo-title: Community Components Guide
description: Uma ferramenta de desenvolvimento interativo para começar a usar a estrutura de componentes sociais (SCF)
seo-description: An interactive development tool to get started with the social component framework (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 2%

---

# Guia de componentes da comunidade  {#community-components-guide}

O guia Componentes da comunidade é uma ferramenta de desenvolvimento interativo para o [quadro de componentes sociais (SCF)](scf.md). Ele fornece uma lista de componentes disponíveis do AEM Communities ou os recursos mais complexos criados de vários componentes.

Juntamente com as informações básicas de cada componente, o guia permite a experimentação sobre como os componentes/recursos do SCF funcionam e como eles podem ser configurados ou personalizados.

Para obter informações sobre essências de desenvolvimento relacionadas a cada componente, consulte [Fundamentos de recursos e componentes](essentials.md).

## Introdução {#getting-started}

O guia deve ser usado em instalações de desenvolvimento de instâncias do autor (localhost:4502) e de publicação (localhost:4503).

O site Componentes da comunidade é acessado navegando até

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

As interações com os componentes das Comunidades variam de acordo com:

* O servidor (autor ou publicação).
* Se o visitante do site está ou não conectado.
* Se estiver conectado, os privilégios atribuídos ao membro.
* se o SRP padrão é ou não, [JSRP](jsrp.md), está em uso.

Ao criar, para entrar no modo de edição, insira `editor.html` ou `cf#` como o primeiro segmento de caminho após o nome do servidor:

* Interface do usuário padrão:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* Interface clássica:

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>No modo Editar, os links em uma página não estão ativos.
>
>Para navegar até uma página de componente, primeiro selecione o Modo de visualização para ativar os links.
>
>Com a página do componente exibida no navegador, volte para o modo Editar para abrir a caixa de diálogo de edição do componente.
>
>Para obter informações gerais sobre criação, visualize o [guia rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>Se não estiver familiarizado com AEM, visualize a documentação em [tratamento básico](../../help/sites-authoring/basic-handling.md).

### Página Inicial {#home-page}

O guia fornece uma lista de componentes SCF disponíveis para pré-visualização e protótipo no lado esquerdo da página.

O Guia de componentes é exibido em uma instância do autor no modo de Edição:

![componente da comunidade1](assets/community-component1.png)

## Páginas de componentes {#component-pages}

Selecione um componente na lista no lado esquerdo da página.

![páginas componentes da comunidade](assets/community-component2.png)

O corpo principal da guia é exibido:

1. Título: O nome do componente selecionado
1. [Bibliotecas do lado do cliente](#client-side-libraries): Uma lista de uma ou mais categorias obrigatórias
1. [Inclusive](scf.md#add-or-include-a-communities-component): Se o componente puder ser incluído dinamicamente, o estado poderá ser alternado no modo de edição do autor:

   * Se adicionado, o texto exibido é: &quot;Esse componente é incluído por meio de seu nó par.&quot;
   * Se incluído, o texto exibido é: &quot;Esse componente é incluído dinamicamente.&quot;
   * Se não for incluível, nenhum texto será exibido

1. Componente ou recurso de exemplo: uma instância ativa do componente ou recurso. Se um componente, ele pode ser alterado com alterações feitas nos modelos, CSS e dados fornecidos na seção da guia .

>[!NOTE]
>
>Depois de fazer uma seleção no lado esquerdo, o componente aparecerá abaixo, em vez de ao lado, da listagem de componentes quando a janela do navegador for muito estreita.

### Interações do autor {#author-interactions}

Ao usar o guia em uma instância de autor, é possível experimentar a configuração de um componente abrindo sua caixa de diálogo. As informações para desenvolvedores são fornecidas na seção [Componentes e recursos básicos](essentials.md) da documentação, enquanto as configurações da caixa de diálogo estão descritas em [Componentes das comunidades](author-communities.md) para autores.

Para o guia Componentes da comunidade , algumas configurações de diálogo de componentes são sobrepostas com o [Inclusive](scf.md#add-or-include-a-communities-component) alternar estado. Para alternar entre o uso do recurso existente ou de um recurso incluído dinamicamente, no modo de edição, selecione o componente e o texto incluível e clique duas vezes para abrir a caixa de diálogo de edição:

![componente da comunidade3](assets/community-component3.png)

Em **Modelos** guia :

![componente da comunidade4](assets/community-component4.png)

* **Incluir o componente-filho com sling:include**

   Se estiver desmarcado, o Guia de componentes usará o recurso existente no repositório (um nó jcr que é filho de um nó par).

   * o texto exibido é: &quot;Esse componente é incluído por meio de seu nó par.&quot;

   Se marcada, o Guia de componentes usará o sling para incluir dinamicamente um componente do resourceType do nó filho (recurso não existente).

   * o texto exibido é: &quot;Esse componente é incluído dinamicamente.&quot;

   O padrão está desmarcado.

### Publicar interações {#publish-interactions}

Ao usar o guia em uma instância de publicação, é possível experimentar os componentes e recursos como um visitante do site (não conectado) e como membros com vários privilégios quando conectado.

>[!NOTE]
>
>Esteja ciente de que, se a SRP for deixada como padrão [JSRP](jsrp.md), o UGC inserido na instância de publicação estará visível somente na publicação e será *not* seja visível do [moderação](moderate-ugc.md) na instância do autor.

## Bibliotecas do lado do cliente {#client-side-libraries}

As bibliotecas do lado do cliente (clientlibs) listadas para cada componente são *obrigatório* a ser referenciado quando o componente for colocado em uma página. As clientlibs fornecem um meio de gerenciar e otimizar o download do Javascript e do CSS usado para renderizar o componente no navegador.

Para obter mais informações, visite [Clientlibs para componentes do Communities](clientlibs.md).

## Representação {#impersonation}

Na instância do autor, onde um deles geralmente está conectado como administrador ou desenvolvedor, para experimentar o componente conectado como outro usuário, use a caixa de texto à esquerda do **[!UICONTROL Representar]** para digitar o nome de usuário ou selecione na lista suspensa e clique no botão . Clique em Reverter para sair e encerrar a representação.

A instância de publicação não precisa representar. Basta usar o link Logon/Logout para representar vários usuários, como o [usuários de demonstração](tutorials.md#demo-users).

## Personalização {#customization}

Quando ativado, cada componente do SCF está disponível para protótipo de possíveis personalizações, modificando temporariamente o modelo do componente, o CSS e os dados.

### Ativação da personalização {#enabling-customization}

>[!NOTE]
>
>**Esta ferramenta é somente leitura**. Nenhuma das edições feitas nos modelos, CSS ou dados é salva no repositório.

Para experimentar rapidamente personalizações, a `scg:showIde`deve ser adicionada ao nó do JCR de conteúdo da página de componente e definida como true.

Usando o componente comments como exemplo, na instância de autor ou publicação, conectado com privilégios de administrador:

1. Navegue até [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Por exemplo, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Selecione o `jcr:content` nó

   Por exemplo, `/content/community-components/en/comments/jcr:content`

1. Adicionar uma propriedade

   * **Nome** `scg:showIde`
   * **Tipo** `String`
   * **Valor** `true`

1. Selecionar **[!UICONTROL Salvar tudo]**
1. Recarregue a página Comentários no guia

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Observe que agora há 3 guias para Modelos, CSS e Dados.

![componente da comunidade5](assets/community-component5.png)

![componente da comunidade6](assets/community-component6.png)

### Guia Modelos {#templates-tab}

Selecione a guia modelos para ver os modelos associados ao componente.

O Editor de modelo permite que edições locais sejam compiladas e aplicadas à instância do componente de amostra na parte superior da página, sem afetar o componente no repositório.

Executar a compilação em edições locais destacará quaisquer erros ao colocar um ponto na sarjeta e marcar o texto em vermelho.

### Guia CSS {#css-tab}

Selecione a guia CSS para ver o CSS associado ao componente.

Se um componente for composto de vários componentes, alguns CSS poderão ser listados em um dos outros componentes.

O Editor de CSS permite que o CSS seja modificado e aplicado à instância do componente de amostra na parte superior da página.

Uma regra pode ser selecionada para realçar as partes do DOM usando essa regra, clicando em ao lado da regra na guia .

### Guia Dados {#data-tab}

Selecione a guia Data para mostrar os dados do endpoint .social.json . Esses dados são editáveis e aplicados à instância do componente de amostra.

Erros de sintaxe podem ser marcados na guia , bem como destacados no editor.
