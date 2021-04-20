---
title: Gerenciar [!DNL Adobe Stock] ativos
description: Pesquise, busque, licencie e gerencie [!DNL Adobe Stock] ativos de dentro de [!DNL Adobe Experience Manager]. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: AG
feature: Search, Adobe Stock
role: Business Practitioner, Administrator
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
translation-type: tm+mt
source-git-commit: a7a9a31364497ab67d805e45ba4fa03c927828ed
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 13%

---

# Use [!DNL Adobe Stock] ativos em [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

As empresas podem integrar o [!DNL Adobe Stock] plano corporativo com [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos criativos e de marketing, com os poderosos recursos de gerenciamento de ativos [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties. [!DNL Experience Manager] os usuários podem localizar, visualizar e licenciar rapidamente  [!DNL Adobe Stock] ativos que são salvos no  [!DNL Experience Manager], sem sair da  [!DNL Experience Manager] interface.

## Pré-requisitos {#prerequisites}

A integração exige um [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).

## Integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Para permitir a comunicação entre [!DNL Experience Manager] e [!DNL Adobe Stock], crie uma configuração IMS e uma configuração [!DNL Adobe Stock] em [!DNL Experience Manager].

>[!NOTE]
>
>Somente administradores [!DNL Experience Manager] e administradores [!DNL Admin Console] de uma organização podem executar a integração, pois ela requer privilégios de administrador.

### Criar uma configuração IMS {#create-an-ims-configuration}

1. Na interface do usuário [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Adobe IMS Configurations]**. Clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Solução da nuvem]** > **[!UICONTROL Adobe Stock]**.
1. Reutilize um certificado existente ou selecione **[!UICONTROL Criar novo certificado]**.
1. Clique em **[!UICONTROL Criar certificado]**. Depois de criada, baixe a chave pública. Clique em **[!UICONTROL Avançar]**. Deixe a tela [!UICONTROL Adobe IMS Technical Account Configuration] aberta para fornecer os valores necessários em breve.
1. Acesse [Console do Desenvolvedor do Adobe](https://console.adobe.io). Certifique-se de que sua conta tenha permissões de administrador para a organização para a qual a integração é necessária.
1. Clique em **[!UICONTROL Criar novo projeto]** e clique em **[!UICONTROL Adicionar API]**. Selecione **[!UICONTROL Adobe Stock]** na lista de APIs disponíveis para você. Selecione [!UICONTROL OAUTH 2.0 Web].
1. Forneça os valores **[!UICONTROL Default redirect URI]** e **[!UICONTROL Redirect URI pattern]**. Clique em **[!UICONTROL Salvar API configurada]**. Copie a ID gerada e o segredo.
1. Na tela [!UICONTROL Adobe IMS Technical Account Configuration], forneça os valores nas caixas intituladas **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]** e **[!UICONTROL Payload&lt;a11/ >.]** Para obter informações detalhadas sobre esses valores, consulte [Início rápido da autenticação JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Criar configuração [!DNL Adobe Stock] em [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. No [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Clique em **[!UICONTROL Criar]** para criar uma configuração e associá-la à sua Configuração IMS existente. Selecione `PROD` como o parâmetro de ambiente.
1. No campo **[!UICONTROL Caminho dos ativos licenciados]**, deixe um local como está. Não altere o local onde deseja armazenar os ativos [!DNL Adobe Stock].
1. Conclua a criação adicionando todas as propriedades necessárias. Clique em **[!UICONTROL Salvar e fechar]**.
1. Adicione [!DNL Experience Manager] usuários ou grupos que podem licenciar os ativos.

>[!NOTE]
>
>Se houver várias configurações [!DNL Adobe Stock], selecione a configuração desejada no painel [!UICONTROL Preferências do usuário]. Para acessar o painel a partir da página inicial [!DNL Experience Manager], clique no ícone do usuário e, em seguida, clique em **[!UICONTROL Preferências do usuário]** > **[!UICONTROL Configuração do Stock]**.

## Use e gerencie [!DNL Adobe Stock] ativos em [!DNL Experience Manager] {#usemanage}

Usando esse recurso, as organizações podem permitir que seus usuários trabalhem usando [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]. Na interface do usuário [!DNL Experience Manager], os usuários podem pesquisar [!DNL Adobe Stock] ativos e licenciar os ativos necessários.

Depois que um ativo [!DNL Adobe Stock] é licenciado em [!DNL Experience Manager], ele pode ser usado e gerenciado como um ativo típico. Em [!DNL Experience Manager], os usuários podem pesquisar e visualizar os ativos; copiar e publicar os ativos; compartilhar os ativos em [!DNL Brand Portal]; acessar e usar os ativos por meio do [!DNL Experience Manager] aplicativo de desktop; e assim por diante.

![Pesquise  [!DNL Adobe Stock] ativos e filtre resultados do seu  [!DNL Adobe Experience Manager] espaço de trabalho](assets/adobe-stock-search-results-workspace.png)

*Figura: Procure por  [!DNL Adobe Stock] ativos e filtre os resultados da sua  [!DNL Experience Manager] interface.*

**A.**[!DNL Adobe Stock] Pesquise ativos semelhantes aos ativos cuja ID do é fornecida. **B.** Pesquise ativos que correspondem à seleção de forma ou orientação. **C.** Procure um dos tipos de ativos mais compatíveis **D.** Abra ou recolha o painel Filtros **E.** Licencie e salve o ativo selecionado no [!DNL Experience Manager]**F.**[!DNL Experience Manager] Salve o ativo no com a marca d&#39;água **G.**[!DNL Adobe Stock] Explore os ativos no site do que são semelhantes ao ativo selecionado **H.**[!DNL Adobe Stock] Exiba os ativos selecionados no site do **I.** Número de ativos selecionados dos resultados de pesquisa **J.** Alterne entre a exibição Cartão e a exibição em Lista

### Localizar ativos {#find-assets}

Seus usuários [!DNL Experience Manager] podem pesquisar ativos em ambos, [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando o local de pesquisa não está limitado a [!DNL Adobe Stock], os resultados da pesquisa de [!DNL Experience Manager] e [!DNL Adobe Stock] são exibidos.

* Para pesquisar ativos [!DNL Adobe Stock], clique em **[!UICONTROL Navegação]** > **[!UICONTROL Ativos]** > **[!UICONTROL Pesquisar Adobe Stock]**.

* Para pesquisar ativos em [!DNL Adobe Stock] e [!DNL Experience Manager Assets], clique em pesquisar ![pesquisar](assets/do-not-localize/search_icon.png).

Como alternativa, comece a digitar `Location: Adobe Stock` na barra de pesquisa para selecionar [!DNL Adobe Stock] ativos. [!DNL Experience Manager] O oferece recursos de filtragem avançados nos ativos pesquisados, permitindo que os usuários entrem rapidamente nos ativos necessários usando filtros, como tipos de ativos compatíveis, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Os ativos pesquisados a partir de [!DNL Adobe Stock] são exibidos apenas em [!DNL Experience Manager]. [!DNL Adobe Stock] os ativos são buscados e armazenados no  [!DNL Experience Manager] repositório somente depois que um usuário  [salva uma ](/help/assets/aem-assets-adobe-stock.md#saveassets) licença do ativo e  [salva um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Os ativos que já estão armazenados em [!DNL Experience Manager] são exibidos e destacados para facilitar a referência e o acesso. Além disso, os ativos [!DNL Stock] são salvos com alguns metadados adicionais para indicar a fonte como [!DNL Stock].

![Pesquisar filtros em  [!DNL Experience Manager] e  [!DNL Adobe Stock] ativos destacados nos resultados de pesquisa](assets/aem-search-filters2.jpg)

*Figura: Pesquise filtros em  [!DNL Experience Manager] e  [!DNL Adobe Stock] ativos destacados nos resultados de pesquisa.*

### Salve e exiba os ativos necessários {#saveassets}

Selecione um ativo que deseja salvar em [!DNL Experience Manager]. Clique em [!UICONTROL Save] na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez que você pesquisar ativos, os ativos salvos serão destacados com um selo, para indicar que tais ativos estão disponíveis em [!DNL Experience Manager Assets].

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um novo selo em vez do selo Licenciado .

### Ativos da licença {#licenseassets}

Os usuários podem licenciar [!DNL Adobe Stock] ativos usando a cota de seu [!DNL Adobe Stock] plano corporativo. Ao licenciar um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso em [!DNL Experience Manager Assets].

![Caixa de diálogo para licenciar e salvar  [!DNL Adobe Stock] ativos em  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*Figura: Caixa de diálogo para licenciar e salvar  [!DNL Adobe Stock] ativos no  [!DNL Experience Manager Assets].*

### Acessar metadados e propriedades de ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e visualizar os metadados, incluindo as propriedades de metadados [!DNL Adobe Stock] dos ativos salvos em [!DNL Experience Manager], e adicionar **[!UICONTROL Referências de licença]** para um ativo. No entanto, as atualizações para a referência de licença não são sincronizadas entre o [!DNL Experience Manager] e o [!DNL Adobe Stock] site.

Os usuários podem ver as propriedades dos ativos licenciados e não licenciados.

![Exibir e acessar metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)

*Figura: Visualize e acesse metadados e referências de licença de ativos salvos.*

## Limitações conhecidas {#known-limitations}

* **O aviso de imagem editorial não é exibido**: Ao licenciar uma imagem, os usuários não podem verificar se uma imagem é Somente para uso editorial. Para evitar um possível uso indevido, os administradores podem desativar o acesso a ativos editoriais no Admin Console.

* **O tipo de licença incorreto é exibido**: É possível que um tipo de licença incorreto seja exibido no  [!DNL Experience Manager] para um ativo. Os usuários podem fazer logon no site [!DNL Adobe Stock] para visualizar o tipo de licença.

* **Os campos e metadados de referência não são sincronizados**: Quando um usuário atualiza um campo de referência de licença, as informações de referência da licença são atualizadas no,  [!DNL Experience Manager] mas não no  [!DNL Adobe Stock] site. Da mesma forma, se o usuário atualizar os campos de referência no site [!DNL Adobe Stock], as atualizações não serão sincronizadas em [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial em vídeo sobre  [!DNL Adobe Stock] o uso de ativos com [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] ajuda do plano empresarial](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Perguntas frequentes](https://helpx.adobe.com/stock/faq.html)

