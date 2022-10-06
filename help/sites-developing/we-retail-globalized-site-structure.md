---
title: Tentar a estrutura do site globalizado no We.Retail
seo-title: Trying out the Globalized Site Structure in We.Retail
description: Tentar a estrutura do site globalizado no We.Retail
seo-description: null
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Tentar a estrutura do site globalizado no We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

O We.Retail foi criado com uma estrutura de site globalizada que oferece mestres de idioma que podem ser copiados em tempo real para sites específicos do país. Tudo está pronto para uso para permitir que você experimente essa estrutura e os recursos incorporados de tradução.

## Tentando {#trying-it-out}

1. Abra o console de sites de **Navegação global -> Sites**.
1. Alterne para a exibição de coluna (se ainda não estiver ativa) e selecione We.Retail. Observe a estrutura de país de exemplo com a Suíça, os Estados Unidos, a França, etc., ao lado dos Mestrados em Idioma.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Selecione a Suíça e veja as raízes de idioma para os idiomas desse país. Observe que ainda não há conteúdo abaixo dessas raízes.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Alterne para a exibição de lista e veja que as cópias de idioma dos países são todas cópias em tempo real.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Retorne à exibição de coluna e clique no Idioma Principal e veja o idioma principal raiz com conteúdo. Observe que somente o inglês tem conteúdo.

   We.Retail não vem com nenhum conteúdo traduzido, mas a estrutura e a configuração estão em vigor para permitir que você demonstre os serviços de tradução.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Com o idioma inglês Principal selecionado, abra o **Referências** no console sites e selecione **Cópias de idioma**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Marque a caixa de seleção ao lado do **Cópias de idioma** para selecionar todas as cópias de idioma. No **Atualizar cópias de idioma** do painel, selecione a opção para **Criar um novo projeto de tradução**. Forneça um nome para o projeto e clique em **Atualizar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Um projeto é criado para cada tradução de idioma. Exiba-os em **Navegação -> Projetos**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Clique em alemão para ver os detalhes do projeto de tradução. Observe que o status está em **Rascunho**. Para iniciar a tradução com o serviço de tradução Microsoft, clique na divisa ao lado do **Tarefa de tradução** e selecione **Iniciar**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. O projeto de tradução é iniciado. Clique nas reticências na parte inferior do cartão denominado Tarefa de tradução para ver os detalhes. Páginas com o estado **Pronto para revisão** já foram traduzidas pelo serviço de tradução.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Selecionar uma das páginas na lista e **Visualizar em sites** na barra de ferramentas, a página traduzida é aberta no editor de páginas.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Esse procedimento demonstrou a integração integrada com a tradução automática do Microsoft. Usar o [Estrutura de integração de tradução AEM](/help/sites-administering/translation.md), é possível integrar com muitos serviços de tradução padrão para orquestrar a tradução de AEM.

## Informações adicionais {#further-information}

Para obter mais informações, consulte o documento de criação [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md) para obter detalhes técnicos completos.
