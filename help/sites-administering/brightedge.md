---
title: Integração com o BrightEdge Content Otimizer
seo-title: Integrating with BrightEdge Content Optimizer
description: Saiba mais sobre como integrar AEM com o BrightEdge Content Otimizer.
seo-description: Learn about integrating AEM with BrightEdge Content Optimizer.
uuid: 7075dd3c-2fd6-4050-af1c-9b16ad4366ec
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: cf25c9a8-0555-4c67-8aa5-55984fd8d301
exl-id: f14cc5fd-aeab-4619-b926-b6f1df7e50e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# Integração com o BrightEdge Content Otimizer{#integrating-with-brightedge-content-optimizer}

Crie uma configuração de nuvem BrightEdge para que AEM possa se conectar usando as credenciais da conta BrightEdge. É possível criar várias configurações se você usar várias contas.

Ao criar a configuração, especifique um título. O título deve ser descritivo para que as pessoas possam correlacionar a configuração com a conta do BrightEdge. Quando um autor ou administrador de página associa uma página da Web à conta do BrightEdge , esse título é apresentado em uma lista suspensa.

1. No trilho, clique em Ferramentas > Operações > Nuvem > Cloud Services.
1. Clique no link exibido na seção BrightEdge Content Otimizer . Se uma configuração do BrightEdge foi criada, determina o texto do link:

   * Configurar agora: Esse link aparece quando nenhuma configuração foi criada.
   * Mostrar configurações: Esse link aparece quando uma ou mais configurações foram criadas.

   ![chlimage_1-4](assets/chlimage_1-4a.png)

1. Se você clicou em Mostrar configurações, clique no link + ao lado de Configurações disponíveis.
1. Digite um título para a configuração. Opcionalmente, digite um nome para o nó usado para armazenar a configuração no repositório. Clique em Criar.
1. Na caixa de diálogo Configuração do BrightEdge Content Otimizer, digite o nome de usuário e a senha da conta BrightEdge e clique em OK.

## Editar uma configuração do BrightEdge {#editing-a-brightedge-configuration}

Modifique o nome de usuário e a senha de uma configuração do BrightEdge, quando necessário. As modificações afetam todas as páginas que usam a configuração.

1. No trilho, clique em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na seção BrightEdge Content Otimizer , clique em Mostrar configurações.

   ![chlimage_1-5](assets/chlimage_1-5a.png)

1. Clique no nome da configuração que deseja editar.
1. Clique em Editar, modifique os valores da propriedade e clique em OK.

## Associar páginas a uma configuração do BrightEdge {#associating-pages-with-a-brightedge-configuration}

Associe páginas com uma configuração do BrightEdge para enviar dados de página ao serviço BrightEdge para análise. Quando você associa uma página a uma configuração, as páginas filhas herdam a associação. Normalmente, você associa a página inicial do site para que os dados de todas as páginas sejam enviados para o BrightEdge.

1. Abra o console Sites clássicos. ([http://localhost:4502/siteadmin#/content](http://localhost:4502/siteadmin#/content))
1. Na árvore Sites, selecione a pasta ou página que contém a página que você deseja associar à configuração do BrightEdge.
1. Na lista de páginas, clique com o botão direito do mouse na página que deseja configurar e clique em Propriedades.
1. Na guia Cloud Services, clique no botão Adicionar serviço e, na caixa de diálogo Cloud Services, selecione BrightEdge Content Otimizer e clique em OK.
1. Na lista Otimizador de conteúdo do BrightEdge , selecione a configuração do BrightEdge a ser associada à página e clique em OK.

   ![chlimage_1-6](assets/chlimage_1-6a.png)

## Ativando uma configuração do BrightEdge {#activating-a-brightedge-configuration}

Ative uma configuração do BrightEdge para replicá-la na instância de publicação e ativar as páginas publicadas para interagir com o serviço BrightEdge.

1. No painel, clique em Sites e procure e selecione a página associada à configuração do BrightEdge.
1. Clique ou toque no ícone Publicar e, em seguida, clique ou toque em Publicar .

   ![chlimage_1-7](assets/chlimage_1-7a.png)

1. Na lista de configurações exibidas, verifique se a configuração do BrightEdge está selecionada e clique em Publicar.

   ![chlimage_1-8](assets/chlimage_1-8a.png)
