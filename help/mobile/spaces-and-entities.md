---
title: Espaços e entidades
description: Esta página serve como página de aterrissagem para desenvolver os Serviços de conteúdo da AEM Mobile.
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 44591900-b01b-4a33-9910-839564477e7d
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---

# Espaços e entidades{#spaces-and-entities}

{{ue-over-mobile}}

Um espaço é um local conveniente para armazenar entidades que são expostas por meio da API REST do Content Services. Isso é especialmente útil porque um aplicativo (ou qualquer canal) pode ser associado a muitas entidades. Forçar entidades a estarem em um espaço força a prática recomendada de agrupar os requisitos de um aplicativo. Como opção, você pode associar um aplicativo no AEM a um pequeno número de Spaces.

>[!NOTE]
>
>Para disponibilizar algo para qualquer canal do Content Services, ele precisa estar em um espaço.

## Criação de um espaço {#creating-a-space}

Se o usuário quiser expor um monte de conteúdo e ativos a um aplicativo móvel, ele cria o espaço usando o painel do AEM Mobile.

Para o primeiro usuário, que não configurou os serviços de conteúdo para funcionar com espaços, o painel do AEM Mobile exibe somente Aplicativos após selecionar **Serviços de Conteúdo**.

>[!CAUTION]
>
>**Pré-requisitos para adicionar um espaço**
>
>Marque a opção **Habilitar Serviços de Conteúdo AEM** para trabalhar com o Spaces e habilite-a no painel de aplicativos do AEM Mobile.
>
>Consulte [Administrando o Content Services](/help/mobile/developing-content-services.md) para obter mais detalhes.

Depois de configurar o Spaces no painel, siga estas etapas para criar o Spaces:

1. Escolha **Espaços** nos Serviços de Conteúdo.

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. Escolha **Criar** para criar um espaço. Insira **Título**, **Nome** e **Descrição** para o espaço.

   Clique em **Criar**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

## Gerenciar um espaço {#managing-a-space}

Depois de criar um espaço, clique em à esquerda para gerenciar o espaço na lista.

Você pode visualizar propriedades do espaço, excluir o espaço ou publicar o espaço e seu conteúdo em uma instância de publicação AEM.

![chlimage_1-85](assets/chlimage_1-85.png)

**Exibindo e Editando Propriedades de um Espaço**

1. Selecione o espaço na lista
1. Escolha **Propriedades** na barra de ferramentas
1. Clique em **Fechar** quando terminar

**Publicando um espaço** Quando um espaço é publicado, todas as pastas e entidades desse espaço também são publicadas.

1. Selecione o espaço clicando em seu ícone na lista Console do espaço
1. Escolher **árvore do Publish**

>[!NOTE]
>
>Você pode **Desfazer a publicação** de um Espaço, o que remove o espaço da instância de publicação.
>
>A imagem a seguir ilustra as ações que podem ser executadas após a publicação do espaço.

![chlimage_1-86](assets/chlimage_1-86.png)

## Trabalhar com pastas em um espaço {#working-with-folders-in-a-space}

Os espaços podem incluir pastas para ajudar a organizar ainda mais o conteúdo e os ativos do espaço. Os usuários podem criar sua própria hierarquia em um espaço.

### Criação de pastas {#creating-a-folder}

1. Clique no espaço na lista no console de espaço e clique em **Criar pasta**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Insira o **Título**, **Nome** e **Descrição** da pasta

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Clique em **Criar** para criar a pasta em um espaço

## Cópia de idioma {#language-copy}

>[!CAUTION]
>
>A Cópia de idioma não está totalmente funcional para esta versão. Ele só configura a estrutura.

O recurso **Cópia de idioma** permite que os autores copiem sua Cópia de idioma principal e, em seguida, criem um Projeto e Fluxo de trabalho para traduzir automaticamente o conteúdo. A Cópia de idioma cria a estrutura correta. Depois de adicionar uma pasta em um espaço, você pode adicionar uma Cópia de idioma ao espaço.

>[!NOTE]
>
>Recomenda-se que qualquer conteúdo que possa ser traduzido, deve ser colocado no nó Cópia de idioma.

### Adicionar cópia de idioma {#adding-language-copy}

1. Após criar o espaço, clique nele para criar uma cópia de idioma.

   Clique em **Criar** e escolha **Cópia de idioma**.

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >Os nós de Cópia de idioma só podem existir como um filho direto do Espaço.

1. Escolha **Idioma do Pacote de Conteúdo&ast;** e insira o **Título&ast;** na caixa de diálogo **Criar Cópia de Idioma**.

   Clique em **Criar**.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Depois de criar uma Cópia de idioma, ela aparecerá no seu espaço em **Idiomas principais**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >Selecione **Idiomas principais** para exibir as pastas de cópia de idioma.

### Removendo uma pasta do espaço {#removing-a-folder-from-the-space}

1. Selecione a pasta na lista do conteúdo do espaço
1. Clique em **Excluir** na barra de ferramentas

   >[!NOTE]
   >
   >Para navegar em uma pasta e ver seu conteúdo ou adicionar uma subpasta ou entidade, clique no título da pasta na lista de conteúdo do espaço.

## Trabalhar com entidades em um espaço {#working-with-entities-in-a-space}

As entidades representam o conteúdo que é exposto por meio do endpoint do serviço Web. As entidades são armazenadas em espaços para que possam ser facilmente encontradas e sejam mantidas independentes da estrutura do repositório do AEM que contém seu conteúdo relacionado.

Talvez você queira agrupar entidades em algum agrupamento lógico. Para fazer isso, é possível criar qualquer número de pastas.

Se os filhos da entidade, que são outras entidades, forem coletados para modelagem de dados, o usuário desenvolvedor poderá criar &quot;Modelos de grupo&quot; específicos a partir do tipo de modelo &quot;Grupo de entidades&quot;, fornecidos prontos para uso.

>[!NOTE]
>
>As entidades são sempre associadas a um espaço, portanto, a maior parte da interface do usuário da entidade é acessada por meio do console de espaço.

### Criação de uma entidade {#creating-an-entity}

1. Abra o console Espaço e clique no título do espaço.

   Como opção, navegue até a pasta clicando no título da pasta na lista.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Escolha o modelo da entidade. Esse é o tipo de entidade que você deseja criar. Clique em Avançar.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >Você tem a opção de escolher o **Modelo do Assets**, o **Modelo de Páginas** ou um modelo do tipo de entidade criado anteriormente.
   >
   >Consulte [Criando um Modelo](/help/mobile/administer-mobile-apps.md), para criar sua entidade personalizada.

1. Insira um **Título**, **Nome**, **Descrição** e **Marcas** para a entidade. Clique em **Criar**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Quando terminar, a entidade aparecerá nos descendentes do seu espaço.

### Editar uma entidade {#editing-an-entity}

1. Depois de criar uma entidade, vá para a pasta ou espaço e escolha sua entidade no console Espaço para editar.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Selecione uma entidade para edição e clique em **Editar**.

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >Dependendo do modelo escolhido para criar sua entidade, a interface será diferente para editar e exibir as propriedades da entidade. Consulte as etapas abaixo para obter mais detalhes.

   ***Se você escolher o modelo para criar a entidade como Modelos do Assets***, clicar em **Editar** permitirá adicionar ativos, como mostrado na figura abaixo:

   ![chlimage_1-97](assets/chlimage_1-97.png)

   Como alternativa, você pode clicar em **Visualizar** para exibir o link json.

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***Se você escolher o modelo para criar a entidade como Modelos de páginas***, clicar em **Editar** permitirá adicionar ativos, como mostrado na figura abaixo:

   ![chlimage_1-99](assets/chlimage_1-99.png)

   Clique no ícone no **Caminho** para adicionar um ativo

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >Depois de adicionar uma entidade, ela deve ser salva para que o link de Pré-visualização funcione. Para exibir a visualização, clique em **Salvar**. Clicar na **Visualização** mostra o json do ativo adicionado, como mostrado na figura abaixo:

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >Quando terminar de adicionar ativos à sua entidade, você poderá escolher **Salvar** para salvar as alterações ou escolher **Salvar e Fechar** para salvar e redirecionar para a lista do console Espaço onde as entidades estão definidas.

   Além disso, selecione uma entidade na lista do console de espaço e clique em **Propriedades** para exibir e editar as propriedades de uma entidade definida.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   É possível editar o título, a descrição, as tags e adicionar os ativos à entidade.

   ![chlimage_1-103](assets/chlimage_1-103.png)

### Remover uma entidade {#removing-an-entity}

1. Selecione a entidade na lista do conteúdo do espaço

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Clique em **Excluir** na barra de ferramentas para remover a entidade específica do espaço

### Publicar uma entidade {#publishing-an-entity}

Você tem a opção de escolher a **Árvore do Publish** ou o **Publish rápido** para publicar sua entidade.

1. Selecione uma entidade na lista do console de espaço e clique em **Árvore do Publish** para publicar essa entidade e seus filhos.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **Ou**,

   Clique em **Quick Publish** para publicar essa entidade específica.
