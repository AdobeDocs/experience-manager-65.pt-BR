---
title: Gerenciar ativos do Adobe Stock nos ativos AEM
description: Pesquise, busque, licencie e gerencie ativos do Adobe Stock no AEM. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 62e82b6da2a5f961acf8cbc30ad29b3c25b1ecef

---


# Use Adobe Stock assets in AEM Assets {#use-adobe-stock-assets-in-aem-assets}

As organizações podem integrar o plano empresarial do Adobe Stock aos ativos AEM para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos de criação e marketing, com os poderosos recursos de gerenciamento de ativos do AEM.

O serviço do Adobe Stock fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties. Os usuários do AEM podem encontrar, visualizar e licenciar rapidamente ativos do Adobe Stock que são salvos no AEM, sem sair da área de trabalho do AEM.

## Pré-requisitos {#prerequisites}

A integração exige um plano [](https://stockenterprise.adobe.com/) corporativo do Adobe Stock e AEM 6.5 ou posterior. Para obter detalhes sobre o service pack do AEM 6.5, consulte estas notas [de](/help/release-notes/sp-release-notes.md)versão.

## Integrar o AEM e o Adobe Stock {#integrate-aem-and-adobe-stock}

Para permitir a comunicação entre o AEM e o Adobe Stock, crie uma configuração IMS e uma configuração do Adobe Stock no AEM.

>[!NOTE]
>
>Somente administradores do AEM e administradores do Admin Console para uma organização podem executar a integração, pois ela requer privilégios de administrador.

### Criar uma configuração IMS {#create-an-ims-configuration}

1. Clique no logotipo do AEM. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**. Clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Solução da nuvem]** > **[!UICONTROL Adobe Stock]**.
1. Reutilize um certificado existente ou selecione **[!UICONTROL Criar novo certificado]**.
1. Clique em **[!UICONTROL Criar certificado]**. Depois de criada, baixe a chave pública. Clique em **[!UICONTROL Avançar]**.
1. Forneça os valores adequados nos campos **[!UICONTROL Título]**, **[!UICONTROL Servidor de autorização]**, **[!UICONTROL Chave da API]**, **[!UICONTROL Segredo do cliente]** e **[!UICONTROL Carga]**. Consulte [Início rápido da autenticação JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md) para obter informações detalhadas sobre esses valores da Adobe I/O.
1. Adicione a chave pública baixada à sua conta de serviço de E/S da Adobe.

### Criar configuração do Adobe Stock no AEM {#create-adobe-stock-configuration-in-aem}

1. Na interface do usuário do AEM, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Adobe Stock]**.
1. Clique em **[!UICONTROL Criar]** para criar uma configuração e associá-la à sua Configuração IMS existente. Selecione `PROD` como parâmetro de ambiente.
1. No campo Caminho **[!UICONTROL dos ativos]** licenciados, deixe um local como está. Não altere o local onde deseja armazenar os ativos do Adobe Stock.
1. Conclua a criação adicionando todas as propriedades necessárias. Clique em **[!UICONTROL Salvar e fechar]**.
1. Adicione usuários ou grupos do AEM, que podem licenciar os ativos.

>[!NOTE]
>
>Se houver várias Configurações do Adobe Stock, selecione a configuração desejada no painel Preferências [!UICONTROL do] usuário clicando no logotipo do AEM na interface do usuário do AEM.

## Usar e gerenciar ativos do Adobe Stock no AEM {#usemanage}

Usando esse recurso, as organizações podem permitir que seus usuários trabalhem usando os ativos do Adobe Stock nos ativos AEM. Na interface do usuário do AEM, os usuários podem pesquisar ativos do Adobe Stock e licenciar os ativos necessários.

Depois que um ativo do Adobe Stock é licenciado no AEM, ele pode ser usado e gerenciado como um ativo comum. No AEM, os usuários podem pesquisar e visualizar os ativos; copiar e publicar os ativos; compartilhar os ativos no Brand Portal; acessar e usar os ativos por meio do aplicativo de desktop do AEM; e assim por diante.

![Procure ativos do Adobe Stock e filtre os resultados de sua área de trabalho do AEM](assets/adobe-stock-search-results-workspace.png)

*Figura: Procure ativos do Adobe Stock e filtre os resultados de sua área de trabalho do AEM*

**A.** Pesquise ativos semelhantes aos ativos cuja ID do Adobe Stock é fornecida. **B.** Pesquise ativos que correspondem à seleção de forma ou orientação. **C.** Procure um dos tipos de ativos mais compatíveis **D.** Abra ou recolha o painel Filtros **E.** Licencie e salve o ativo selecionado no AEM **F.** Salve o ativo no AEM com a marca d&#39;água **G.** Explore os ativos no site do Adobe Stock que são semelhantes ao ativo selecionado **H.** Exiba os ativos selecionados no site do Adobe Stock **I.** Número de ativos selecionados dos resultados de pesquisa **J.** Alterne entre a exibição Cartão e a exibição em Lista

### Localizar ativos {#find-assets}

Seus usuários do AEM podem procurar ativos no AEM e no Adobe Stock. Quando o local de pesquisa não estiver limitado ao Adobe Stock, os resultados da pesquisa do AEM e do Adobe Stock serão exibidos.

* Para pesquisar ativos do Adobe Stock, clique em **[!UICONTROL Navegação]** > **[!UICONTROL Ativos]** > **[!UICONTROL Pesquisar no Adobe Stock]**.

* Para pesquisar ativos no Adobe Stock e nos ativos AEM, clique no ícone de pesquisa ![search_icon](assets/search_icon.png).

Como alternativa, comece a digitar `Location: Adobe Stock` na barra de pesquisa para selecionar ativos do Adobe Stock.  O AEM oferece recursos avançados de filtragem nos ativos pesquisados, permitindo que os usuários façam rapidamente o logon nos ativos necessários usando filtros, como tipos de ativos suportados, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Os ativos pesquisados a partir do Adobe Stock são exibidos apenas no AEM. Os ativos do Adobe Stock são obtidos e armazenados no repositório do AEM somente depois que um usuário [salva um ativo](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [licencia um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Os ativos já armazenados no AEM são exibidos e destacados para facilitar a referência e o acesso. Além disso, esses ativos são salvos com alguns metadados adicionais para indicar a fonte como o Adobe Stock.

![Pesquisar filtros no AEM e destacar ativos do Adobe Stock nos resultados da pesquisa](assets/aem-search-filters2.jpg)

*Figura: Pesquisar filtros no AEM e destacar ativos do Adobe Stock nos resultados da pesquisa*

### Salvar e exibir os ativos necessários {#saveassets}

Selecione um ativo que deseja salvar no AEM. Clique em Salvar na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez que você pesquisar ativos, os ativos salvos serão destacados com um selo para indicar que tais ativos estão disponíveis nos ativos AEM.

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um novo selo em vez de um selo licenciado.

### Ativos da licença {#licenseassets}

Os usuários podem licenciar ativos do Adobe Stock usando a cota de seu plano Adobe Stock Enterprise. Ao licenciar um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso nos ativos AEM.

![Diálogo para licenciar e salvar ativos do Adobe Stock nos ativos AEM](assets/aem-stock_licenseandsave.jpg)

*Figura: Diálogo para licenciar e salvar ativos do Adobe Stock nos ativos AEM*

### Acessar metadados e propriedades de ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e visualizar os metadados, incluindo as propriedades de metadados do Adobe Stock para os ativos salvos no AEM, e adicionar Referências **[!UICONTROL de]** licença para um ativo. No entanto, as atualizações para referência de licença não são sincronizadas entre o site do AEM e o site do Adobe Stock.

Os usuários podem ver as propriedades dos ativos licenciados e não licenciados.

![Exibir e acessar metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)

*Figura: Exibir e acessar metadados e referências de licença de ativos salvos*

## Limitações conhecidas {#known-limitations}

### O aviso de imagem editorial não é exibido

Ao licenciar uma imagem, os usuários não poderão verificar se uma imagem é Somente para uso editorial. Para evitar um possível uso indevido, os administradores podem desativar o acesso a ativos editoriais no Admin Console.

### Tipo de licença incorreto exibido

É possível que um tipo de licença incorreto seja exibido no AEM para um ativo. Os usuários podem fazer logon no site do Adobe Stock para ver o tipo de licença.

### Campos de referência e metadados não são sincronizados

Quando um usuário atualiza um campo de referência de licença, as informações de referência de licença são atualizadas no AEM, mas não no site do Adobe Stock. Da mesma forma, se o usuário atualizar os campos de referência no site do Adobe Stock, as atualizações não serão sincronizadas no AEM.

## Related resources {#related-resources}

[Tutorial em vídeo sobre como usar ativos do Adobe Stock com ativos AEM](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)

[Ajuda do plano corporativo do Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)

[Perguntas frequentes sobre o Adobe Stock](https://helpx.adobe.com/stock/faq.html)
