---
title: Tentando a estrutura do site globalizado no We.Retail
seo-title: Tentando a estrutura do site globalizado no We.Retail
description: 'null'
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Tentando a estrutura do site globalizado no We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail foi construído com uma estrutura de site globalizada que oferece mestres de idioma que podem ser copiados ao vivo para sites específicos de cada país. Tudo está pronto para o teste para permitir que você experimente esta estrutura e os recursos de tradução integrados.

## Tentando sair {#trying-it-out}

1. Abra o console Sites de Navegação **global -> Sites**.
1. Alterne para a exibição de coluna (se ainda não estiver ativa) e selecione We.Retail. Observe o exemplo da estrutura do país com a Suíça, os Estados Unidos, a França, etc., ao lado dos Mestres em Linguagem.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Selecione a Suíça e veja as raízes de idioma para os idiomas daquele país. Observe que ainda não há nenhum conteúdo abaixo dessas raízes.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Alterne para a exibição de lista e veja se as cópias de idioma dos países são todas cópias online.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Retorne à exibição de coluna e clique em Idioma mestre e veja as raízes do idioma mestre com conteúdo. Observe que somente o inglês tem conteúdo.

   We.Retail não vem com nenhum conteúdo traduzido, mas a estrutura e configuração estão em vigor para permitir que você demonstre os serviços de tradução.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Com o Idioma mestre selecionado, abra o painel **Referências** no console de sites e selecione Cópias **de** idioma.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Marque a caixa de seleção ao lado do rótulo Cópias **de** idioma para selecionar todas as cópias de idioma. Na seção **Atualizar cópias** de idioma do painel, selecione a opção para **Criar um novo projeto** de tradução. Forneça um nome para o projeto e clique em **Atualizar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Um projeto é criado para cada tradução de idioma. Exiba-os em **Navegação -> Projetos**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Clique em alemão para ver os detalhes do projeto de tradução. Observe que o status está em **Rascunho**. Para iniciar a tradução com o serviço de tradução da Microsoft, clique na divisa ao lado do cabeçalho Trabalho **de** tradução e selecione **Iniciar**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. O projeto de tradução começa. Clique nas reticências na parte inferior do cartão rotulado Trabalho de tradução para ver os detalhes. As páginas com o estado **Pronto para revisão** já foram traduzidas pelo serviço de tradução.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Selecionar uma das páginas na lista e, em seguida, **Visualizar nos sites** na barra de ferramentas abrirá a página traduzida no editor de páginas.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Este procedimento demonstrou a integração integrada com a tradução automática da Microsoft. Usando a estrutura [de integração de tradução do](/help/sites-administering/translation.md)AEM, você pode se integrar a muitos serviços de tradução padrão para orquestrar a tradução do AEM.

## Informações adicionais {#further-information}

Para obter mais informações, consulte o documento de criação [Traduzindo conteúdo para sites](/help/sites-administering/translation.md) multilíngues para obter detalhes técnicos completos.
