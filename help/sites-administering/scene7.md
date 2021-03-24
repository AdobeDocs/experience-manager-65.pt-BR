---
title: Integração com o Dynamic Media Classic
description: Saiba como integrar o Adobe Experience Manager com o Dynamic Media Classic.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: ef975961ddcd6910b5fba2dea7e9302921f45055
workflow-type: tm+mt
source-wordcount: '5511'
ht-degree: 1%

---


# Integração com o Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}

O Adobe Dynamic Media Classic é uma solução hospedada para gerenciar, aprimorar, publicar e fornecer ativos de mídia avançada para Web, dispositivos móveis, email, impressão e monitores conectados à Internet.

Para usar o Dynamic Media Classic, você deve configurar a configuração de nuvem para que o Dynamic Media Classic e o Adobe Experience Manager Assets possam interagir uns com os outros. Este documento descreve como configurar o Experience Manager e o Dynamic Media Classic.

Para obter informações sobre como usar todos os componentes do Dynamic Media Classic em uma página e trabalhar com vídeo, consulte [Usar o Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* A plataforma do visualizador DHTML do Dynamic Media Classic chegou ao fim da vida útil oficialmente em 31 de janeiro de 2014. Para obter mais informações, consulte as [Perguntas frequentes sobre o fim da vida útil do visualizador DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Antes de configurar o Dynamic Media Classic para funcionar com o Experience Manager, consulte [Práticas recomendadas](#best-practices-for-integrating-scene-with-aem) para integrar o Dynamic Media Classic com o Experience Manager.
>* Se você usar o Dynamic Media Classic com uma configuração de proxy personalizada, deverá configurar ambas as configurações de proxy do cliente HTTP, pois algumas funcionalidades do Experience Manager usam as APIs 3.x e outras usam as APIs 4.x. A 3.x é configurada com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) e a 4.x é configurada com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).

>



## Integração do Experience Manager/Dynamic Media Classic versus Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Os usuários do Experience Manager têm uma escolha entre duas soluções para trabalhar com o Dynamic Media. Você pode usar um dos seguintes:

* Integre sua instância do Experience Manager com o Dynamic Media Classic.
* Use o Dynamic Media integrado ao Experience Manager.

Use os seguintes critérios para determinar qual solução escolher:

* Se você for um **cliente existente** do Dynamic Media Classic cujos ativos de mídia avançada residem no Dynamic Media Classic para publicação e entrega, mas quiser integrar esses ativos com a criação e/ou o Experience Manager Assets (WCM) para gerenciamento, use a [Experience Manager/Dynamic Media Classic point-to-point integration](#aem-scene-point-to-point-integration) descrita neste documento.

* Se você for um cliente do Experience Manager **new** que tenha necessidades de delivery de mídia avançada, selecione a opção [Dynamic Media](#aem-dynamic-media). Essa opção faz mais sentido se você não tiver uma conta do S7 e muitos ativos armazenados nesse sistema.

* Em certos casos, use ambas as soluções. O [cenário de dupla utilização](/help/sites-administering/scene7.md#dual-use-scenario) descreve esse cenário.

### Integração ponto a ponto do Experience Manager/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Ao trabalhar com ativos nessa solução, você executa um dos seguintes procedimentos:

* Faça upload de ativos diretamente no Dynamic Media Classic e acesse por meio do navegador de conteúdo **Dynamic Media Classic** para criação de página ou
* Faça upload para o Experience Manager Assets e ative a publicação automática para o Dynamic Media Classic; você acessa o navegador de conteúdo **Assets** para criação de página

Os componentes usados para essa integração são encontrados na área de componente **Dynamic Media Classic** no [Modo Design.](/help/sites-authoring/author-environment-tools.md#page-modes)

### Experience Manager Dynamic Media {#aem-dynamic-media}

O Experience Manager Dynamic Media é a unificação dos recursos do Dynamic Media Classic diretamente da plataforma Experience Manager.

Ao trabalhar com ativos nessa solução, você segue este fluxo de trabalho:

1. Faça upload de ativos de imagem e vídeo únicos diretamente no Experience Manager.
1. Codifique vídeos diretamente no Experience Manager.
1. Crie conjuntos baseados em imagens diretamente no Experience Manager.
1. Se aplicável, adicione interatividade a imagens ou vídeos.

Os componentes usados para o Dynamic Media são encontrados na área de componente **[!UICONTROL Dynamic Media]** em [Modo de design](/help/sites-authoring/author-environment-tools.md#page-modes). Eles incluem:

* **[!UICONTROL Dynamic Media]**  - O  **[!UICONTROL componente]** dinâmico é inteligente. Dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. O componente oferece suporte a predefinições de imagem, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

* **[!UICONTROL Mídia interativa]**  - O  **[!UICONTROL componente]** interativo é para ativos como banners de carrossel, imagens interativas e vídeo interativo. Esses ativos têm interatividade em pontos de acesso ou mapas de imagem. Esse componente é inteligente. Ou seja, dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

### Cenário de dupla utilização {#dual-use-scenario}

Imediatamente, você pode usar os recursos de integração do Dynamic Media e do Dynamic Media Classic do Experience Manager simultaneamente. A tabela de casos de uso a seguir descreve quando você ativa e desativa determinadas áreas.

Para usar o Dynamic Media e o Dynamic Media Classic simultaneamente:

1. Configure [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) no Cloud Services.
1. Siga as instruções específicas específicas do seu caso de uso:

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Integração com o Dynamic Media Classic</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>Se você for ...</strong></td>
    <td><strong>Fluxo de trabalho do caso de uso</strong></td>
    <td><strong>Imagem/Vídeo</strong></td>
    <td><strong>Componente de mídia dinâmica</strong></td>
    <td><strong>Navegador e componentes de conteúdo do S7</strong></td>
    <td><strong>Upload automático de ativos para S7</strong></td>
    </tr>
    <tr>
    <td>Novo no Sites e no Dynamic Media</td>
    <td>Faça upload de ativos para o Experience Manager e use o componente Experience Manager Dynamic Media para criar ativos nas páginas do Sites</td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Ligado</a></td>
    <td>Desativado</td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>No varejo e novos em Sites e Dynamic Media</td>
    <td>Faça upload de ativos não relacionados ao produto para o Experience Manager para gerenciamento e entrega. Faça upload de ativos de produto para o Dynamic Media Classic e use o navegador de conteúdo do Dynamic Media Classic no Experience Manager e componente para criar Páginas de detalhes do produto no Sites.</td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Ligado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Novo no Assets e no Dynamic Media</td>
    <td>Fazer upload de ativos para ativos do Experience Manager e usar o código de URL/incorporação publicado do Dynamic Media</td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Novo no Dynamic Media e Modelos</td>
    <td>Use o Dynamic Media para imagens e vídeo. Crie modelos de imagem no Dynamic Media Classic e use o Localizador de conteúdo do Dynamic Media Classic para incluir modelos nas páginas do Sites.</td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Ligado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Um cliente Dynamic Media Classic existente e são novos no Sites</td>
    <td>Faça upload de ativos para o Dynamic Media Classic e use o navegador de conteúdo do Experience Manager Dynamic Media Classic para pesquisar e criar ativos nas páginas do Sites</td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Um cliente Dynamic Media Classic existente e são novos em Sites e Ativos</td>
    <td>Faça upload de ativos no DAM e publique automaticamente no Dynamic Media Classic para entrega. Use o navegador de conteúdo Experience Manager Dynamic Media Classic para pesquisar e criar ativos nas páginas do Sites.</td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Ligado</a></p> <p>(Veja a etapa 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente Dynamic Media Classic existente e novo no Assets</td>
    <td><p>Faça upload de ativos no Experience Manager e use o Dynamic Media para gerar representações para download/compartilhamento. Publique ativos do Experience Manager automaticamente no Dynamic Media Classic para entrega.</p> <p><strong>Importante:</strong> processar e renderizações duplicadas geradas no Experience Manager não são sincronizadas com o Dynamic Media Classic</p> </td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><p><a href="#configuringautouploadingfromaemassets">Ligado</a></p> <p>(Veja a etapa 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Opcional; consulte tabela de casos de uso) - Configure a [configuração de nuvem do Dynamic Media](/help/assets/config-dynamic.md) e [habilite o servidor Dynamic Media](/help/assets/config-dynamic.md).
1. (Opcional; consulte tabela de casos de uso) - Se você optar por ativar o Upload automático de ativos para o Dynamic Media Classic, será necessário adicionar o seguinte:

   1. Configure o upload automático para o Dynamic Media Classic.
   1. Adicione a etapa **Upload do Dynamic Media Classic** depois de todas as etapas do fluxo de trabalho do Dynamic Media *no final do fluxo de trabalho* **Ativo de atualização do Dam** ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Opcional) Restrinja o upload do ativo Dynamic Media Classic por tipo MIME em [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). Os tipos MIME de ativos que não estão nessa lista não são carregados no servidor do Dynamic Media Classic.
   1. (Opcional) Configurar vídeo na configuração do Dynamic Media Classic. Você pode ativar a codificação de vídeo para o Dynamic Media ou para o Dynamic Media Classic simultaneamente. As representações dinâmicas são usadas para visualização e reprodução local na instância do Experience Manager, enquanto as representações de vídeo do Dynamic Media Classic são geradas e armazenadas nos servidores do Dynamic Media Classic. Ao configurar serviços de codificação de vídeo para o Dynamic Media e o Dynamic Media Classic, aplique um [perfil de processamento de vídeo](/help/assets/video-profiles.md) à pasta de ativos do Dynamic Media Classic.
   1. (Opcional) [Configurar visualização segura no Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Limitações           {#limitations}

Quando o Dynamic Media Classic e o Dynamic Media estão habilitados, há as seguintes limitações:

* Fazer upload manual no Dynamic Media Classic, selecionando um ativo e arrastando-o para um componente do Dynamic Media Classic em uma página do Experience Manager, não funciona.
* Mesmo que os ativos sincronizados do Experience Manager-Dynamic Media Classic sejam atualizados para o Dynamic Media Classic automaticamente quando o ativo é editado no Assets, uma ação de reversão não aciona um novo upload. Dessa forma, o Dynamic Media Classic não obtém a versão mais recente imediatamente após uma reversão. A solução alternativa é editar novamente após a conclusão da reversão.
* Se você precisar usar o Dynamic Media para um caso de uso e a integração do Dynamic Media Classic para outro, para que os ativos do Dynamic Media não interajam com o sistema do Dynamic Media Classic, não aplique a configuração do Dynamic Media Classic à pasta do Dynamic Media. E não aplique a configuração do Dynamic Media (perfil de processamento) a uma pasta do Dynamic Media Classic.

## Práticas recomendadas para integrar o Dynamic Media Classic ao Experience Manager {#best-practices-for-integrating-scene-with-aem}

Ao integrar o Dynamic Media Classic com o Experience Manager, há algumas práticas recomendadas importantes que devem ser observadas nas seguintes áreas:

* Teste da integração
* Upload de ativos diretamente do Dynamic Media Classic recomendado para determinados cenários

Consulte [limitações conhecidas](#known-limitations-and-design-implications).

### Teste sua integração {#test-driving-your-integration}

O Adobe recomenda testar e direcionar a integração fazendo com que a pasta raiz aponte para uma subpasta somente em vez de para uma empresa inteira.

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode levar muito tempo para ser exibida no Experience Manager. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos (por exemplo, a pasta raiz geralmente tem muitos ativos e pode travar o sistema).

### Upload de ativos do Experience Manager Assets versus do Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Você pode fazer upload de ativos usando a funcionalidade Ativos (gerenciamento de ativos digitais) ou acessando o Dynamic Media Classic diretamente no Experience Manager por meio do navegador de conteúdo do Dynamic Media Classic. O que você escolher depende dos seguintes fatores:

* Os tipos de ativos do Dynamic Media Classic que o Experience Manager Assets ainda não suporta devem ser adicionados a um site do Experience Manager diretamente do Dynamic Media Classic, por meio do navegador de conteúdo do Dynamic Media Classic. Por exemplo, modelos de imagem.
* Para tipos de ativos compatíveis com o Experience Manager Assets e o Dynamic Media Classic, a decisão de como fazer upload deles depende do seguinte:

   * Onde os ativos estão hoje E
   * Como é importante gerenciá-los em um repositório comum

Se os ativos já estiverem no Dynamic Media Classic e o gerenciamento em um repositório comum não for importante, exportar para o Experience Manager Assets somente para sincronizá-los de volta ao Dynamic Media Classic para entrega é uma viagem de ida e volta desnecessária. Caso contrário, é preferível manter os ativos em um único repositório e sincronizar com o Dynamic Media Classic somente para entrega.

## Configuração da integração do Dynamic Media Classic {#configuring-scene-integration}

Você pode configurar o Experience Manager para fazer upload de ativos no Dynamic Media Classic. Os ativos de uma pasta de destino CQ podem ser carregados (automática ou manualmente) do Experience Manager para uma conta de empresa do Dynamic Media Classic.

>[!NOTE]
>
>O Adobe recomenda usar somente a pasta de destino designada para importar ativos do Dynamic Media Classic. Os ativos digitais que estão fora da pasta de destino só podem ser usados nos componentes do Dynamic Media Classic nas páginas em que a configuração do Dynamic Media Classic foi ativada. Além disso, elas são colocadas em uma pasta ad-hoc no Dynamic Media Classic. A pasta ad-hoc não é sincronizada com o Experience Manager (mas os ativos podem ser descobertos no navegador de conteúdo do Dynamic Media Classic).

Para configurar o Dynamic Media Classic para se integrar ao Experience Manager, você deve concluir as seguintes etapas:

1. [Definir uma configuração de nuvem](#creating-a-cloud-configuration-for-scene)  - Define o mapeamento entre uma pasta do Dynamic Media Classic e uma pasta do Assets. Conclua esta etapa mesmo se desejar apenas a sincronização unidirecional (Experience Manager Assets para o Dynamic Media Classic).
1. [Ative o ouvinte de dam do  **Adobe CQ s7dam**](#enabling-the-adobe-cq-scene-dam-listener)  - Feito no   console OSGi.
1. Se quiser que o Experience Manager Assets faça upload automático para o Dynamic Media Classic, ative essa opção e adicione o Dynamic Media Classic ao fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] . Também é possível fazer upload manual de ativos.
1. Adicionar componentes do Dynamic Media Classic ao sidekick. Essa funcionalidade permite que os usuários usem componentes do Dynamic Media Classic em suas páginas do Experience Manager.
1. [Mapear a configuração para a página no Experience Manager](#enabling-scene-for-wcm)  - Essa etapa é necessária para exibir todas as predefinições de vídeo que você criou no Dynamic Media Classic. Também é necessário se você tiver que executar uma publicação de ativo de fora da pasta de destino CQ para o Dynamic Media Classic.

Esta seção aborda como executar todas essas etapas e lista limitações importantes.

### Como a sincronização entre o Dynamic Media Classic e o Experience Manager Assets funciona {#how-synchronization-between-scene-and-aem-assets-works}

Ao configurar a sincronização do Experience Manager Assets e do Dynamic Media Classic, é importante entender o seguinte:

#### Upload para o Dynamic Media Classic a partir do Experience Manager Assets {#uploading-to-scene-from-aem-assets}

* Há uma pasta de sincronização designada no Experience Manager para uploads do Dynamic Media Classic.
* Os uploads para o Dynamic Media Classic podem ser automatizados se os ativos digitais forem colocados na pasta de sincronização designada.
* A estrutura de pastas e subpastas no Experience Manager é replicada no Dynamic Media Classic.

>[!NOTE]
>
>O Experience Manager incorpora todos os metadados como XMP antes de carregá-los no Dynamic Media Classic, de modo que todas as propriedades no nó de metadados estejam disponíveis no Dynamic Media Classic como XMP.

#### Limitações conhecidas e implicações de design {#known-limitations-and-design-implications}

Com a sincronização entre o Experience Manager Assets e o Dynamic Media Classic, há atualmente as seguintes limitações/implicações de design:

<table>
 <tbody>
  <tr>
   <td><strong>Limitação/implicação de projeto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Uma pasta designada de sincronização (target)</td>
   <td>Você só pode ter uma pasta designada por empresa no Experience Manager para uploads do Dynamic Media Classic. Você pode criar várias configurações se precisar ter acesso a mais de uma conta de empresa no Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Estrutura de pastas</td>
   <td>Se você excluir uma pasta sincronizada com ativos, todos os ativos remotos do Dynamic Media Classic serão excluídos, mas a pasta permanecerá.</td>
  </tr>
  <tr>
   <td>Pasta ad-hoc</td>
   <td>Os ativos que estão fora da pasta de destino carregada manualmente no Dynamic Media Classic no WCM são colocados automaticamente em uma pasta ad hoc separada no Dynamic Media Classic. Você configura essa pasta na configuração da nuvem no Experience Manager.</td>
  </tr>
  <tr>
   <td>Mídia mista</td>
   <td>Os conjuntos de mídia mista são exibidos no Experience Manager, embora não sejam compatíveis com o Experience Manager.</td>
  </tr>
  <tr>
   <td>PDFs</td>
   <td>Os PDFs gerados a partir de eCatalogs no Dynamic Media Classic são importados para a pasta de destino CQ.</td>
  </tr>
  <tr>
   <td>Atualização da interface do usuário</td>
   <td>Ao sincronizar o Experience Manager com o Dynamic Media Classic, atualize a interface do usuário para exibir as alterações. </td>
  </tr>
  <tr>
   <td>Miniaturas de vídeo</td>
   <td>Ao fazer upload de um vídeo para ativos Experience Manager para codificação via Dynamic Media Classic, as miniaturas de vídeo e os vídeos codificados podem levar algum tempo para estarem disponíveis no Experience Manager Assets, dependendo do tempo de processamento do vídeo.</td>
  </tr>
  <tr>
   <td>Subpastas do Target</td>
   <td><p>Se você usa subpastas dentro da pasta de destino, certifique-se de usar nomes exclusivos para cada ativo (independentemente da localização) ou configurar o Dynamic Media Classic (na área Configuração) para não substituir ativos, independentemente da localização.</p> <p>Caso contrário, os ativos com o mesmo nome que são carregados em uma subpasta de destino do Dynamic Media Classic serão carregados, mas o ativo com o mesmo nome na pasta de destino será excluído. </p> </td>
  </tr>
 </tbody>
</table>

### Configuração dos servidores Dynamic Media Classic {#configuring-scene-servers}

Se você executar o Experience Manager atrás de um proxy ou tiver configurações de firewall especiais, deverá habilitar explicitamente os hosts das diferentes regiões. Os servidores são gerenciados no conteúdo em `/etc/cloudservices/scene7/endpoints` e podem ser personalizados conforme necessário. Toque em um URL e edite para alterar o URL, se necessário. Em versões anteriores do Experience Manager, esses valores eram codificados.

Se você navegar até `/etc/cloudservices/scene7/endpoints.html`, verá os servidores listados (e poderá editá-los tocando no URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Criação de uma configuração de nuvem para o Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Uma configuração de nuvem define o mapeamento entre uma pasta Dynamic Media Classic e uma pasta Experience Manager Assets. Ele deve ser configurado para sincronizar o Experience Manager Assets com o Dynamic Media Classic. Consulte Como a sincronização funciona para obter mais informações.

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode levar muito tempo para ser exibida no Experience Manager. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos. Por exemplo, a pasta raiz geralmente tem muitos ativos.
>
>Se você quiser testar a integração, faça com que a pasta raiz aponte apenas para uma subpasta, em vez da empresa inteira.

>[!NOTE]
>
>É possível ter várias configurações: uma configuração de nuvem representa um usuário em uma empresa do Dynamic Media Classic. Para acessar outras empresas ou usuários do Dynamic Media Classic, você deve criar várias configurações.

Para configurar o Experience Manager para poder publicar ativos no Dynamic Media Classic:

1. Toque no ícone Experience Manager e navegue até **[!UICONTROL Deployment > Cloud Services]** para acessar o Adobe Dynamic Media Classic.

1. Toque em **[!UICONTROL Configurar agora]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. No campo **[!UICONTROL Title]** e, opcionalmente, no campo **[!UICONTROL Name]**, insira as informações apropriadas. Toque em **[!UICONTROL Criar]**.

   >[!NOTE]
   >
   >Ao criar mais configurações, o campo **[!UICONTROL configuração pai]** é exibido.
   >
   >Faça **not** alterar a configuração pai. Alterar a configuração pai pode interromper a integração.

1. Insira o endereço de email, senha e região da sua conta do Dynamic Media Classic e toque em **[!UICONTROL Conectar-se ao Dynamic Media Classic]**. Você está conectado ao servidor Dynamic Media Classic e a caixa de diálogo é expandida com mais opções.

1. Insira o nome **[!UICONTROL Company]** e **[!UICONTROL Root Path]**. Essas informações são o nome do servidor publicado junto com qualquer caminho que você deseja especificar. Se você não souber o nome do servidor publicado, no Dynamic Media Classic, vá para **[!UICONTROL Configuração > Configuração do aplicativo]**).

   >[!NOTE]
   >
   >O caminho raiz do Dynamic Media Classic é o Experience Manager de pasta do Dynamic Media Classic. Ele pode ser limitado a uma pasta específica.

   >[!CAUTION]
   >
   >Dependendo do tamanho da pasta Dynamic Media Classic, a importação de uma pasta raiz pode demorar muito. Além disso, os dados do Dynamic Media Classic podem exceder o armazenamento de Experience Manager. Certifique-se de que está importando a pasta correta. Importar muitos dados pode parar o sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Clique em **[!UICONTROL OK]**. O Experience Manager salva sua configuração.

>[!NOTE]
>
>Se estiver reconectando:
>
>* Ao reconectar-se ao Dynamic Media Classic na publicação, redefina a senha ao publicar ou reconectar não funciona (não é um problema na instância do autor).
>* Se você modificar valores como sua região, nome da empresa, será necessário reconectar-se ao Dynamic Media Classic. Se as opções de configuração tiverem sido modificadas, mas não tiverem sido salvas, o Experience Manager ainda indicará erroneamente que a configuração é válida. Certifique-se de reconectar.

>



### Ativar o ouvinte de Dam do Adobe CQ Dynamic Media Classic {#enabling-the-adobe-cq-scene-dam-listener}

Ative o ouvinte de Dam do Adobe CQ Dynamic Media Classic, que é desativado por padrão.

Para habilitá-lo:

1. Toque no ícone [!UICONTROL Ferramentas] e navegue até **[!UICONTROL Operações > Console da Web]**. O console da Web é aberto.
1. Navegue até **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** e selecione a caixa de seleção **[!UICONTROL Enabled]**.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Toque em **[!UICONTROL Salvar]**.

### Adicionar tempo limite configurável ao fluxo de trabalho de Upload do Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Quando uma instância do Experience Manager é configurada para lidar com a codificação de vídeo por meio do Dynamic Media Classic, por padrão, há um tempo limite de 35 minutos em qualquer trabalho de upload. Para acomodar trabalhos de codificação de vídeo potencialmente mais longos, você pode configurar esta configuração:

1. Navegue até **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Altere o número conforme desejado no campo **[!UICONTROL Tempo limite do trabalho ativo]**. Qualquer número não negativo é aceite com a unidade de medida em segundos. Por padrão, esse número é definido como 2100.

   >[!NOTE]
   >
   >Prática recomendada: A maioria dos ativos é assimilada em no máximo minutos (por exemplo, imagens). Mas em certas instâncias - vídeos maiores, por exemplo - aumentam o valor do tempo limite para 7.200 segundos (duas horas) para acomodar o tempo de processamento longo. Caso contrário, esse trabalho de upload do Dynamic Media Classic será marcado como **[!UICONTROL UploadFailed]** nos metadados JCR.

1. Toque em **[!UICONTROL Salvar]**.

### Carregamento automático do Experience Manager Assets {#autouploading-from-aem-assets}

A partir do Experience Manager 6.3.2, o Experience Manager Assets é configurado para que todos os ativos digitais carregados no gerenciador de ativos sejam atualizados para o Dynamic Media Classic se os ativos estiverem em uma pasta de destino CQ.

Quando um ativo é adicionado ao Experience Manager Assets, ele é carregado e publicado automaticamente no Dynamic Media Classic.

>[!NOTE]
>
>O tamanho máximo de arquivo para o upload automático do Experience Manager Assets para o Dynamic Media Classic é de 500 MB.

Para configurar o upload automático do Experience Manager Assets:

1. Toque no ícone Experience Manager e navegue até **[!UICONTROL Implantação > Cloud Services]** e, no cabeçalho Dynamic Media, em Configurações disponíveis, toque em **[!UICONTROL dms7 (Dynamic Media]**)
1. Toque na guia **[!UICONTROL Avançado]**, marque a caixa de seleção **[!UICONTROL Ativar upload automático]** e toque em **[!UICONTROL OK]**. Agora, você deve configurar o fluxo de trabalho do Ativo DAM para incluir o upload para o Dynamic Media Classic.

   >[!NOTE]
   >
   >Consulte [Configuração do estado (publicado/não publicado) de ativos enviados para o Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) para obter informações sobre como enviar ativos para o Dynamic Media Classic em um estado não publicado.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Navegue de volta à página de boas-vindas do Experience Manager e toque em **[!UICONTROL Workflows]**. Clique duas vezes no workflow **DAM Update Asset** para abri-lo.
1. No sidekick, navegue até os componentes **[!UICONTROL Fluxo de trabalho]** e selecione **[!UICONTROL Dynamic Media Classic]**. Arraste **[!UICONTROL Dynamic Media Classic]** para o workflow e toque em **[!UICONTROL Salvar]**. Os ativos adicionados aos Experience Manager Assets na pasta de destino são carregados automaticamente no Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Ao adicionar ativos após a automação, se eles não forem colocados na pasta de destino do CQ, eles não serão carregados no Dynamic Media Classic.
   >* O Experience Manager incorpora todos os metadados como XMP antes de carregá-los no Dynamic Media Classic, de modo que todas as propriedades no nó de metadados estejam disponíveis no Dynamic Media Classic como XMP.


### Configurar o estado (publicado/não publicado) dos ativos enviados para o Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Se estiver enviando ativos do Experience Manager Assets para o Dynamic Media Classic, você pode publicá-los automaticamente (comportamento padrão) ou enviá-los para o Dynamic Media Classic em um estado não publicado.

É possível que você não queira publicar ativos imediatamente no Dynamic Media Classic se quiser testá-los em um ambiente de preparo antes de entrar em funcionamento. Você pode usar o Experience Manager com o ambiente de teste seguro do Dynamic Media Classic para enviar ativos diretamente do Assets para o Dynamic Media Classic em um estado não publicado.

Os ativos do Dynamic Media Classic permanecem disponíveis por meio da visualização segura. Somente quando os ativos são publicados no Experience Manager, os ativos do Dynamic Media Classic também entram em produção.

Se você quiser publicar ativos imediatamente ao enviá-los para o Dynamic Media Classic, não precisará configurar nenhuma opção. Essa funcionalidade é o comportamento padrão.

No entanto, se você não quiser que ativos enviados para o Dynamic Media Classic sejam publicados automaticamente, esta seção descreve como configurar o Experience Manager e o Dynamic Media Classic para realizar essa funcionalidade.

#### Pré-requisitos para enviar ativos para o Dynamic Media Classic não publicados {#prerequisites-to-push-assets-to-scene-unpublished}

Antes de enviar ativos para o Dynamic Media Classic sem publicá-los, você deve configurar o seguinte:

1. [Use o Admin Console para criar um caso de suporte.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) No seu caso de suporte, solicite a ativação de uma pré-visualização segura para sua conta do Dynamic Media Classic.
1. Siga as instruções para [configurar visualização segura para sua conta do Dynamic Media Classic.](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

Essas etapas são as mesmas que você seguiria para criar qualquer configuração de teste seguro no Dynamic Media Classic.

>[!NOTE]
>
>Se o seu ambiente de instalação for um sistema operacional UNIX® de 64 bits, consulte [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) sobre outras opções de configuração que você deve definir.

#### Limitações conhecidas para enviar ativos no estado não publicado {#known-limitations-for-pushing-assets-in-unpublished-state}

Se você usar esse recurso, observe as seguintes limitações:

* Não há suporte para controle de versão.
* Se um ativo já estiver publicado no Experience Manager e uma versão subsequente for criada, essa nova versão será publicada imediatamente ao vivo para produção. Publicar na ativação só funciona com a publicação inicial de um ativo.

>[!NOTE]
>
>Se você deseja publicar ativos instantaneamente, a prática recomendada é manter **[!UICONTROL Ativar visualização segura]** definido como **[!UICONTROL Imediatamente]** e usar o recurso **[!UICONTROL Ativar upload automático]**.

### Definir o estado dos ativos enviados para o Dynamic Media Classic como não publicados {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Se um usuário publicar o ativo no Experience Manager, ele automaticamente acionará o ativo S7 para o ativo de produção/ao vivo (o ativo não está mais em visualização segura/não está mais publicado).

Para definir o estado dos ativos enviados para o Dynamic Media Classic como não publicados:

1. Toque no ícone Experience Manager e navegue até **[!UICONTROL Deployment > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** e selecione a configuração no Dynamic Media Classic.
1. Toque na guia **[!UICONTROL Avançado]**. No menu suspenso **[!UICONTROL Ativar Exibição segura]**, selecione **[!UICONTROL Na ativação de publicação do AEM]** para enviar ativos para o Dynamic Media Classic sem publicação. (Por padrão, esse valor é definido como **[!UICONTROL Imediatamente]**, onde os ativos do Dynamic Media Classic são publicados imediatamente.)

   Consulte a [documentação do Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) para obter mais informações sobre como testar ativos antes de torná-los públicos.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Toque em **[!UICONTROL OK]**.

Ativar a Visualização segura significa que seus ativos são enviados para o servidor de visualização seguro e não publicados.

Para ver se a Visualização segura está ativada, navegue até um componente do Dynamic Media Classic em uma página no Experience Manager. Toque em **[!UICONTROL Editar]**. O ativo tem o servidor de visualização seguro listado no URL. Após a publicação no Experience Manager, o domínio do servidor na referência de arquivo é atualizado do URL de visualização para o URL de produção.

### Ativar o Dynamic Media Classic para WCM {#enabling-scene-for-wcm}

A ativação do Dynamic Media Classic para WCM é necessária por dois motivos:

* Ela ativa a lista suspensa de perfis de vídeo universais para criação de página. Sem essa lista, o menu suspenso **[!UICONTROL Universal Video Preset]** fica vazio e não pode ser definido.
* Se um ativo digital não estiver na pasta de destino, você poderá fazer upload do ativo para o Dynamic Media Classic se ativar o Dynamic Media Classic para essa página nas propriedades da página. Em seguida, arraste e solte o ativo em um componente do Dynamic Media Classic. As regras de herança normais se aplicam (o que significa que as páginas secundárias herdam a configuração da página principal).

Ao ativar o Dynamic Media Classic para o WCM, como em outras configurações, as regras de herança se aplicam. Você pode ativar o Dynamic Media Classic para WCM na interface otimizada para toque ou clássica.

#### Ativar o Dynamic Media Classic para WCM na interface otimizada para toque {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

Para ativar o Dynamic Media Classic para WCM na interface otimizada para toque:

1. Toque no ícone Experience Manager e navegue até **[!UICONTROL Sites]** e, em seguida, a página raiz do seu site (não específico de idioma).

1. Na barra de ferramentas, selecione o ícone [!UICONTROL settings] e toque em **[!UICONTROL Abrir propriedades]**.

1. Toque em **[!UICONTROL Cloud Services]** e toque em **[!UICONTROL Adicionar configuração]** e selecione **[!UICONTROL Dynamic Media Classic]**.
1. Na lista suspensa **[!UICONTROL Adobe Dynamic Media Classic]**, selecione a configuração desejada e toque em **[!UICONTROL OK]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   As predefinições de vídeo dessa configuração do Dynamic Media Classic estão disponíveis para uso no Experience Manager com o componente de vídeo do Dynamic Media Classic nessa página e páginas filhas.

#### Ativar o Dynamic Media Classic para WCM na interface de usuário clássica {#enabling-scene-for-wcm-in-the-classic-user-interface}

Para ativar o Dynamic Media Classic para WCM na interface clássica:

1. No Experience Manager, toque em **[!UICONTROL Sites]** e navegue até a página raiz do seu site (não específico de idioma).

1. No sidekick, toque no ícone **[!UICONTROL Página]** e toque em **[!UICONTROL Propriedades da página]**.

1. Toque em **[!UICONTROL Cloud Services > Adicionar serviços > Dynamic Media Classic]**.
1. Na lista suspensa **[!UICONTROL Adobe Dynamic Media Classic]**, selecione a configuração desejada e toque em **[!UICONTROL OK]**.

   As predefinições de vídeo dessa configuração do Dynamic Media Classic estão disponíveis para uso no Experience Manager com o componente de vídeo do Dynamic Media Classic nessa página e páginas filhas.

### Configurar uma configuração padrão {#configuring-a-default-configuration}

Se você tiver várias configurações do Dynamic Media Classic, poderá especificar uma delas como padrão para o navegador de conteúdo do Dynamic Media Classic.

Somente uma configuração do Dynamic Media Classic pode ser marcada como padrão em um determinado momento. A configuração padrão são os ativos da empresa exibidos por padrão no Navegador de conteúdo do Dynamic Media Classic.

Para configurar a configuração padrão:

1. Toque no ícone Experience Manager e navegue até **[!UICONTROL Deployment > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** e selecione a configuração no Dynamic Media Classic.
1. Para abrir a configuração, toque em **[!UICONTROL Edit]**.

1. Na guia **[!UICONTROL General]**, marque a caixa de seleção **[!UICONTROL Configuração padrão]** para torná-la a empresa padrão e o caminho raiz que aparece no navegador de conteúdo do Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Se houver apenas uma configuração, marcar a caixa de seleção **[!UICONTROL Configuração padrão]** não terá efeito.

### Configuração da pasta ad-hoc {#configuring-the-ad-hoc-folder}

Você pode configurar a pasta para a qual os ativos são carregados no Dynamic Media Classic quando o ativo não estiver na pasta de destino CQ. Consulte Publicação de ativos fora da pasta de destino CQ.

Para configurar a pasta ad hoc:

1. Toque no ícone Experience Manager e navegue até **[!UICONTROL Deployment > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** e selecione a configuração no Dynamic Media Classic.
1. Para abrir a configuração, toque em **[!UICONTROL Edit]**.

1. Toque na guia **[!UICONTROL Avançado]**. No campo **[!UICONTROL Pasta ad-hoc]**, você pode modificar a pasta **Ad-hoc**. Por padrão, é o **name_of_the_company/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configuração de predefinições universais {#configuring-universal-presets}

Para configurar as Predefinições universais para o componente de vídeo, consulte [Vídeo](/help/assets/s7-video.md).

## Ativar o suporte ao parâmetro de trabalho de upload do Assets/Dynamic Media Classic baseado no tipo MIME {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Você pode ativar parâmetros de tarefas de upload configuráveis do Dynamic Media Classic que são acionadas pela sincronização do Digital Asset Manager/Dynamic Media Classic assets.

Especificamente, você configura o formato de arquivo aceito por tipo MIME na área OSGi (iniciativa do Open Service Gateway) do painel Configuração do Console da Web do Experience Manager. Em seguida, você pode personalizar os parâmetros de trabalho de upload individuais que são usados para cada tipo MIME no JCR (Java™ Content Repository).

**Para ativar ativos baseados em tipo MIME:**

1. Toque no ícone Experience Manager e navegue até **[!UICONTROL Ferramentas > Operações > Console da Web]**.
1. No painel Configuração do console da Web do Adobe Experience Manager, no menu **[!UICONTROL OSGi]**, toque em **[!UICONTROL Configuração]**.
1. Na coluna Nome , localize e toque em **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** para editar a configuração.
1. Na área Mapeamento de tipo MIME, toque em qualquer sinal de mais (+) para adicionar um tipo MIME.

   Consulte [Tipos MIME suportados](/help/assets/assets-formats.md#supported-mime-types).

1. No campo de texto, digite o novo nome do tipo MIME.

   Por exemplo, você digitaria um `<file_extension>=<mime_type>` como em `EPS=application/postscript` OU `PSD=image/vnd.adobe.photoshop`.

1. No canto inferior direito da janela de configuração, toque em **[!UICONTROL Save]**.
1. Volte para Experience Manager e, no painel esquerdo, toque em CRXDE Lite.
1. Na página CRXDE Lite, no painel à esquerda, navegue até `/etc/cloudservices/scene7/<environment>` (substitua `<environment>` pelo nome real).
1. Expanda `<environment>` (substitua `<environment>` pelo nome real) para revelar o nó `mimeTypes`.
1. Toque no mimeType que acabou de adicionar.

   Por exemplo, `mimeTypes > application_postscript` OU `mimeTypes > image_vnd.adobe.photoshop`.

1. No lado direito da página CRXDE Lite, toque na guia **[!UICONTROL Properties]**.
1. Especifique um parâmetro de trabalho de upload do Dynamic Media Classic no campo de valor **[!UICONTROL jobParam]** .

   Por exemplo, `psprocess="rasterize"&psresolution=120` .

   Consulte a [Adobe Dynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) para obter mais parâmetros de trabalho de upload que você pode usar.

   >[!NOTE]
   >
   >Se estiver carregando arquivos PSD e quiser processá-los como modelos com extrações de camada, insira o seguinte no campo de valor **[!UICONTROL jobParam]**:
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >Certifique-se de que o arquivo PSD tenha &quot;camadas&quot;. Se for estritamente uma imagem ou uma imagem com máscara, ela será processada como uma imagem porque não há camadas para processar.

1. No canto superior esquerdo da página CRXDE Lite, toque em **[!UICONTROL Salvar tudo]**.

## Solução de problemas na integração do Dynamic Media Classic e do Experience Manager {#troubleshooting-scene-and-aem-integration}

Se tiver problemas para integrar o Experience Manager com o Dynamic Media Classic, consulte os seguintes cenários para soluções.

**Se a publicação de ativos digitais no Dynamic Media Classic falhar:**

* Verifique se o ativo que você está fazendo upload está na pasta **[!UICONTROL CQ target]** (você especifica essa pasta na configuração da nuvem do Dynamic Media Classic).
* Se não estiver, você deve configurar a configuração de nuvem em **[!UICONTROL Propriedades da página]** para essa página para permitir o upload para a pasta **[!UICONTROL CQ ad hoc]**.

* Verifique os logs para obter qualquer informação.

**Se as predefinições de vídeo não forem exibidas:**

* Verifique se você configurou a configuração de nuvem dessa página por meio de **[!UICONTROL Propriedades da página]**. As predefinições de vídeo estão disponíveis no componente de vídeo do Dynamic Media Classic.

**Se os ativos de vídeo não forem reproduzidos no Experience Manager:**

* Certifique-se de ter usado o componente de vídeo correto. O componente de vídeo do Dynamic Media Classic é diferente do componente básico de Vídeo. Consulte [Componente de vídeo de base versus Componente de vídeo do Dynamic Media Classic](/help/assets/s7-video.md).

**Se os ativos novos ou modificados no Experience Manager não forem carregados automaticamente para o Dynamic Media Classic:**

* Certifique-se de que os ativos estejam na pasta de destino do CQ. Somente os ativos que estão na pasta de destino CQ são atualizados automaticamente (desde que você tenha configurado os Ativos do Experience Manager para fazer upload automático dos ativos).
* Certifique-se de ter configurado a configuração do Cloud Services para Ativar o upload automático e que você atualizou e salvou o fluxo de trabalho do Ativo do DAM para incluir o upload do Dynamic Media Classic.
* Ao fazer upload de uma imagem em uma subpasta da pasta de destino do Dynamic Media Classic, siga um destes procedimentos:

   * Certifique-se de que os nomes de todos os ativos, independentemente da localização, sejam exclusivos. Caso contrário, o ativo na pasta de destino principal será excluído e somente o ativo na subpasta permanecerá.
   * Altere como o Dynamic Media Classic substitui ativos na área Configuração da conta do Dynamic Media Classic. Não defina o Dynamic Media Classic para substituir ativos, independentemente do local, se você usar ativos com o mesmo nome em subpastas.

**Se os ativos ou pastas excluídos não forem sincronizados entre o Dynamic Media Classic e o Experience Manager:**

* Os ativos e pastas excluídos no Experience Manager Assets ainda são exibidos na pasta sincronizada no Dynamic Media Classic. Exclua-os manualmente.

**Se o upload de vídeo falhar**

* Se o upload de vídeo falhar e você estiver usando o Experience Manager para codificar vídeo por meio da integração do Dynamic Media Classic, consulte [Adicionar tempo limite configurável ao fluxo de trabalho de upload do Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode levar muito tempo para ser exibida no Experience Manager. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos. Por exemplo, a pasta raiz geralmente tem muitos ativos.
>
>Se você quiser testar a integração, faça com que a pasta raiz aponte apenas para uma subpasta, em vez da empresa inteira.

