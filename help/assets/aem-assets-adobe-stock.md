---
title: Gerenciar [!DNL Adobe Stock] ativos
description: Pesquise, busque, licencie e gerencie [!DNL Adobe Stock] ativos de dentro de [!DNL Adobe Experience Manager]. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 13%

---


# Usar [!DNL Adobe Stock] ativos em [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

As organizações podem integrar seu [!DNL Adobe Stock] plano corporativo com [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos de criação e marketing, com os poderosos recursos de gerenciamento de ativos de [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties. [!DNL Experience Manager] os usuários podem encontrar, pré-visualização e licenciar rapidamente  [!DNL Adobe Stock] ativos salvos em  [!DNL Experience Manager], sem sair da  [!DNL Experience Manager] interface.

## Pré-requisitos {#prerequisites}

A integração requer um [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).

## Integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Para permitir a comunicação entre [!DNL Experience Manager] e [!DNL Adobe Stock], crie uma configuração IMS e uma configuração [!DNL Adobe Stock] em [!DNL Experience Manager].

>[!NOTE]
>
>Somente os administradores [!DNL Experience Manager] e [!DNL Admin Console] administradores de uma organização podem executar a integração, pois ela requer privilégios de administrador.

### Criar uma configuração IMS {#create-an-ims-configuration}

1. Na interface do usuário [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações IMS de Adobe]**. Clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Solução da nuvem]** > **[!UICONTROL Adobe Stock]**.
1. Reutilize um certificado existente ou selecione **[!UICONTROL Criar novo certificado]**.
1. Clique em **[!UICONTROL Criar certificado]**. Depois de criada, baixe a chave pública. Clique em **[!UICONTROL Avançar]**.
1. Adicione a chave pública baixada à sua conta de serviço [!DNL Adobe Developer Console]. Clique em **[!UICONTROL Avançar]**. Deixe a tela [!UICONTROL Configuração técnica de conta do Adobe IMS] aberta para fornecer os valores em breve.
1. Acesse [Console do desenvolvedor do Adobe](https://console.adobe.io). Certifique-se de que sua conta tenha permissões de administrador para a organização para a qual a integração é necessária.
1. Clique em **[!UICONTROL Criar novo projeto]** e clique em **[!UICONTROL Adicionar API]**. Selecione **[!UICONTROL Adobe Stock]** na lista de APIs disponíveis para você. Selecione [!UICONTROL OAUTH 2.0 Web]. Configure e copie os vários valores apresentados.
1. Em [!DNL Experience Manager] forneça os valores nos campos intitulados **[!UICONTROL Title]**, **[!UICONTROL Servidor de Autorização]**, **[!UICONTROL Chave de API]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL Carga]**. Consulte [start rápido de autenticação JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md) para obter informações detalhadas sobre esses valores.

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Criar configuração [!DNL Adobe Stock] em [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Clique em **[!UICONTROL Criar]** para criar uma configuração e associá-la à Configuração IMS existente. Selecione `PROD` como parâmetro de ambiente.
1. No campo **[!UICONTROL Caminho dos ativos licenciados]**, deixe um local como está. Não altere o local onde deseja armazenar os ativos [!DNL Adobe Stock].
1. Conclua a criação adicionando todas as propriedades necessárias. Clique em **[!UICONTROL Salvar e fechar]**.
1. Adicione [!DNL Experience Manager] usuários ou grupos que podem licenciar os ativos.

>[!NOTE]
>
>Se houver várias [!DNL Adobe Stock] configurações, selecione a configuração desejada no painel [!UICONTROL Preferências do usuário]. Para acessar o painel do home page [!DNL Experience Manager], clique no ícone do usuário e, em seguida, clique em **[!UICONTROL Preferências do usuário]** > **[!UICONTROL Configuração do Stock]**.

## Usar e gerenciar ativos [!DNL Adobe Stock] em [!DNL Experience Manager] {#usemanage}

Usando esse recurso, as organizações podem permitir que seus usuários trabalhem usando [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]. Na interface do usuário [!DNL Experience Manager], os usuários podem pesquisar [!DNL Adobe Stock] ativos e licenciar os ativos necessários.

Depois que um ativo [!DNL Adobe Stock] é licenciado em [!DNL Experience Manager], ele pode ser usado e gerenciado como um ativo comum. Em [!DNL Experience Manager], os usuários podem pesquisar e pré-visualização os ativos; copiar e publicar os ativos; compartilhar os ativos em [!DNL Brand Portal]; acessar e usar os ativos por meio do [!DNL Experience Manager] aplicativo de desktop; e assim por diante.

![Procure  [!DNL Adobe Stock] ativos e filtre os resultados de seu  [!DNL Adobe Experience Manager] espaço de trabalho](assets/adobe-stock-search-results-workspace.png)

*Figura: Procure  [!DNL Adobe Stock] ativos e filtre os resultados de sua  [!DNL Experience Manager] interface.*

**A.**[!DNL Adobe Stock] Pesquise ativos semelhantes aos ativos cuja ID do é fornecida. **B.** Pesquise ativos que correspondem à seleção de forma ou orientação. **C.** Procure um dos tipos de ativos mais compatíveis **D.** Abra ou recolha o painel Filtros **E.** Licencie e salve o ativo selecionado no [!DNL Experience Manager]**F.**[!DNL Experience Manager] Salve o ativo no com a marca d&#39;água **G.**[!DNL Adobe Stock] Explore os ativos no site do que são semelhantes ao ativo selecionado **H.**[!DNL Adobe Stock] Exiba os ativos selecionados no site do **I.** Número de ativos selecionados dos resultados de pesquisa **J.** Alterne entre a exibição Cartão e a exibição em Lista

### Localizar ativos {#find-assets}

Seus usuários do [!DNL Experience Manager] podem pesquisar ativos em ambos, [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando o local de pesquisa não estiver limitado a [!DNL Adobe Stock], os resultados da pesquisa de [!DNL Experience Manager] e [!DNL Adobe Stock] serão exibidos.

* Para pesquisar ativos [!DNL Adobe Stock], clique em **[!UICONTROL Navegação]** > **[!UICONTROL Ativos]** > **[!UICONTROL Pesquisar Adobe Stock]**.

* Para pesquisar ativos em [!DNL Adobe Stock] e [!DNL Experience Manager Assets], clique em pesquisar ![pesquisar](assets/do-not-localize/search_icon.png).

Como alternativa, digite `Location: Adobe Stock` na barra de pesquisa para selecionar [!DNL Adobe Stock] ativos. [!DNL Experience Manager] oferta os recursos de filtragem avançada nos ativos pesquisados, permitindo que os usuários façam rapidamente o logon zero nos ativos necessários usando filtros, como tipos de ativos suportados, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Os ativos pesquisados de [!DNL Adobe Stock] são exibidos em [!DNL Experience Manager]. [!DNL Adobe Stock] os ativos são buscados e armazenados no  [!DNL Experience Manager] repositório somente depois que um usuário  [salva uma ](/help/assets/aem-assets-adobe-stock.md#saveassets) licença de  [ativo e salva um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Os ativos que já estão armazenados em [!DNL Experience Manager] são exibidos e destacados para facilitar a referência e o acesso. Além disso, os ativos [!DNL Stock] são salvos com alguns metadados adicionais para indicar a fonte como [!DNL Stock].

![Pesquisar filtros em  [!DNL Experience Manager] e  [!DNL Adobe Stock] ativos destacados nos resultados da pesquisa](assets/aem-search-filters2.jpg)

*Figura: Pesquise filtros em  [!DNL Experience Manager] e  [!DNL Adobe Stock] ativos destacados nos resultados da pesquisa.*

### Salve e visualização os ativos necessários {#saveassets}

Selecione um ativo que deseja salvar em [!DNL Experience Manager]. Clique em [!UICONTROL Salvar] na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez que você pesquisar ativos, os ativos salvos serão destacados com um selo, para indicar que tais ativos estão disponíveis em [!DNL Experience Manager Assets].

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um novo selo em vez de um selo licenciado.

### Ativos da licença {#licenseassets}

Os usuários podem licenciar ativos [!DNL Adobe Stock] usando a cota de seus [!DNL Adobe Stock] planos corporativos. Ao licenciar um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso em [!DNL Experience Manager Assets].

![Diálogo para licenciar e salvar  [!DNL Adobe Stock] ativos em  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*Figura: Caixa de diálogo para licenciar e salvar  [!DNL Adobe Stock] ativos em  [!DNL Experience Manager Assets].*

### Acessar metadados e propriedades de ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e pré-visualização os metadados, incluindo as propriedades de metadados [!DNL Adobe Stock] dos ativos salvos em [!DNL Experience Manager], e adicionar **[!UICONTROL Referências de licença]** para um ativo. No entanto, as atualizações para referência de licença não são sincronizadas entre os sites [!DNL Experience Manager] e [!DNL Adobe Stock].

Os usuários podem ver as propriedades dos ativos licenciados e não licenciados.

![Visualização e acesso a metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)

*Figura: Visualização e acesso metadados e referências de licença de ativos salvos.*

## Limitações conhecidas {#known-limitations}

* **O aviso de imagem editorial não é exibido**: Ao licenciar uma imagem, os usuários não poderão verificar se uma imagem é Somente para uso editorial. Para evitar um possível uso indevido, os administradores podem desativar o acesso a ativos editoriais do Admin Console.

* **O tipo de licença incorreto é exibido**: É possível que um tipo de licença incorreto seja exibido  [!DNL Experience Manager] para um ativo. Os usuários podem fazer logon no site [!DNL Adobe Stock] para ver o tipo de licença.

* **Campos de referência e metadados não são sincronizados**: Quando um usuário atualiza um campo de referência de licença, as informações de referência de licença são atualizadas no  [!DNL Experience Manager] site, mas não no  [!DNL Adobe Stock] site. Da mesma forma, se o usuário atualizar os campos de referência no site [!DNL Adobe Stock], as atualizações não serão sincronizadas em [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial em vídeo sobre como  [!DNL Adobe Stock] usar ativos com [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] ajuda do plano corporativo](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Perguntas frequentes](https://helpx.adobe.com/stock/faq.html)

