---
title: Adicionar comentário à página de exemplo
description: Saiba como uma instância do sistema de comentários de um site deve definir seu resourceType como o sistema de comentários personalizado e incluir todas as bibliotecas de clientes necessárias.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Adicionar comentário à página de exemplo  {#add-comment-to-sample-page}

Agora que os componentes do sistema de comentários personalizados estão no diretório do aplicativo (/apps), é possível usar o componente estendido. A instância do sistema de comentários em um site a ser afetado deve definir seu resourceType como o sistema de comentários personalizado e incluir todas as bibliotecas de clientes necessárias.

## Identificar Clientlibs Necessárias {#identify-required-clientlibs}

As bibliotecas de clientes necessárias para o estilo e funcionamento dos Comentários padrão também são necessárias para Comentários estendidos.

O [Guia de Componentes da Comunidade](/help/communities/components-guide.md) identifica as bibliotecas de clientes necessárias. Navegue até o Guia Componentes e exiba o componente Comentários, por exemplo:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Observe as três bibliotecas de clientes necessárias para que os Comentários sejam renderizados e funcionem corretamente. Eles devem ser incluídos onde os Comentários estendidos são referenciados e a [biblioteca do cliente de Comentários estendidos](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comentários-componente1](assets/comments-component1.png)

### Adicionar comentários personalizados a uma página {#add-custom-comments-to-a-page}

Como só pode haver um sistema de Comentários por página, é mais simples criar uma página de exemplo conforme descrito no breve tutorial [criar uma página de exemplo](/help/communities/create-sample-page.md).

Depois de criado, entre no modo Design e disponibilize o grupo de componentes Personalizado para permitir que o componente `Alt Comments` seja adicionado à página.

Para que o Comentário apareça e funcione corretamente, as bibliotecas de clientes para Comentários devem ser adicionadas à clientlibslist da página (consulte [Clientlibs para Componentes de Comunidades](/help/communities/clientlibs.md)).

#### Clientlibs de comentários na página de exemplo {#comments-clientlibs-on-sample-page}

![comentários-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Autor: Comentário alternativo na página de exemplo {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Autor: Exemplo do nó Comentários da página {#author-sample-page-comments-node}

Você pode verificar o resourceType no CRXDE visualizando as propriedades do nó comentários para a página de exemplo em `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verificar-comentário-crxde](assets/verify-comment-crxde.png)

#### Página de exemplo do Publish {#publish-sample-page}

Depois que o componente personalizado for adicionado à página, também será necessário (re) [publicar a página](/help/communities/sites-console.md#publishing-the-site).

#### Publish: Comentário alternativo na página de exemplo {#publish-alt-comment-on-sample-page}

Depois de publicar o aplicativo personalizado e a página de exemplo, é possível inserir um comentário. Quando você entrar, com um [usuário de demonstração](/help/communities/tutorials.md#demo-users) ou administrador, é possível postar um comentário.

Aqui está aaron.mcdonald@mailinator.com postando um comentário:

![publicar-alt-comment](assets/publish-alt-comment.png)

![publicar-alt-comment1](assets/publish-alt-comment1.png)

Agora que parece que o componente estendido está funcionando corretamente com a aparência padrão, é hora de modificar a aparência.
