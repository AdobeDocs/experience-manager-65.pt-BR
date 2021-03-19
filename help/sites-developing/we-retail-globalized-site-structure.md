---
title: Tentar a estrutura do site globalizado no We.Retail
seo-title: Tentar a estrutura do site globalizado no We.Retail
description: Tentar a estrutura do site globalizado no We.Retail
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Tentar a estrutura do site globalizado em We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

O We.Retail foi criado com uma estrutura de site globalizada que oferece mestres de idioma que podem ser copiados em tempo real para sites específicos do país. Tudo está pronto para uso para permitir que você experimente essa estrutura e os recursos incorporados de tradução.

## Tentando sair {#trying-it-out}

1. Abra o console Sites de **Navegação global -> Sites**.
1. Alterne para a exibição de coluna (se ainda não estiver ativa) e selecione We.Retail. Observe a estrutura de país de exemplo com a Suíça, os Estados Unidos, a França, etc., ao lado dos Mestrados em Idioma.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Selecione a Suíça e veja as raízes de idioma para os idiomas desse país. Observe que ainda não há conteúdo abaixo dessas raízes.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Alterne para a exibição de lista e veja que as cópias de idioma dos países são todas cópias em tempo real.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Retorne à exibição de coluna e clique no Idioma Principal e veja o idioma principal raiz com conteúdo. Observe que somente o inglês tem conteúdo.

   We.Retail não vem com nenhum conteúdo traduzido, mas a estrutura e a configuração estão em vigor para permitir que você demonstre os serviços de tradução.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Com o idioma inglês Principal selecionado, abra o painel **Referências** no console de sites e selecione **Cópias de idioma**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Marque a caixa de seleção ao lado do rótulo **Cópias de idioma** para selecionar todas as cópias de idioma. Na seção **Update language copies** do painel, selecione a opção **Create a new translation project**. Forneça um nome para o projeto e clique em **Atualizar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Um projeto é criado para cada tradução de idioma. Exiba-os em **Navegação -> Projetos**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Clique em alemão para ver os detalhes do projeto de tradução. Observe que o status está em **Rascunho**. Para iniciar a tradução com o serviço de tradução da Microsoft, clique na divisa ao lado do cabeçalho **Tarefa de Tradução** e selecione **Iniciar**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. O projeto de tradução é iniciado. Clique nas reticências na parte inferior do cartão denominado Tarefa de tradução para ver os detalhes. As páginas com o estado **Pronto para revisão** já foram traduzidas pelo serviço de tradução.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Selecionar uma das páginas na lista e, em seguida, **Visualizar nos sites** na barra de ferramentas abre a página traduzida no editor de páginas.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Este procedimento demonstrou a integração interna com a tradução automática da Microsoft. Usando a [AEM Estrutura de integração de tradução](/help/sites-administering/translation.md), você pode se integrar a muitos serviços de tradução padrão para orquestrar a tradução de AEM.

## Informações adicionais {#further-information}

Para obter mais informações, consulte o documento de criação [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md) para obter detalhes técnicos completos.
