---
title: Integração com o Dynamic Media Classic
description: Saiba como integrar o Adobe Experience Manager com o Dynamic Media Classic.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '5452'
ht-degree: 1%

---


# Integração com o Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}

O Adobe Dynamic Media Classic é uma solução hospedada para gerenciar, aprimorar, publicar e fornecer ativos de mídia avançada para Web, dispositivos móveis, email, impressão e monitores conectados à Internet.

Para usar o Dynamic Media Classic, você precisa configurar a configuração de nuvem para que o Dynamic Media Classic e o AEM Assets possam interagir entre si. Este documento descreve como configurar o AEM e o Dynamic Media Classic.

Para obter informações sobre como usar todos os componentes do Dynamic Media Classic em uma página e trabalhar com vídeo, consulte [Usar o Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* A plataforma do visualizador DHTML do Dynamic Media Classic chegou ao fim da vida útil oficialmente em 31 de janeiro de 2014. Para obter mais informações, consulte as [Perguntas frequentes sobre o fim da vida útil do visualizador DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Antes de configurar o Dynamic Media Classic para trabalhar com o AEM, consulte [Práticas recomendadas](#best-practices-for-integrating-scene-with-aem) para integrar o Dynamic Media Classic ao AEM.
>* Se você estiver usando o Dynamic Media Classic com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do cliente HTTP, pois algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x. A 3.x é configurada com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) e a 4.x é configurada com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).

>



## Integração do AEM/Dynamic Media Classic versus Dynamic Media {#aem-scene-integration-versus-dynamic-media}

AEM usuários têm uma escolha entre duas soluções para trabalhar com o Dynamic Media: Integrando a instância do AEM com o Dynamic Media Classic ou usando a solução da Dynamic Media integrada ao AEM.

Use os seguintes critérios para determinar qual solução escolher:

* Se você for um **cliente existente** do Dynamic Media Classic cujos ativos de mídia avançada residem no Dynamic Media Classic para publicação e entrega, mas quiser integrar esses ativos com a criação do Sites (WCM) e/ou o AEM Assets para gerenciamento, use a [AEM/integração ponto a ponto do Dynamic Media Classic](#aem-scene-point-to-point-integration) descrita neste documento.

* Se você for um **novo** AEM cliente que tenha necessidades de fornecimento de mídia avançada, selecione a [opção Dynamic Media](#aem-dynamic-media). Essa opção faz mais sentido se você não tiver uma conta do S7 e muitos ativos armazenados nesse sistema.

* Em certos casos, você pode usar ambas as soluções. O [cenário de dupla utilização](/help/sites-administering/scene7.md#dual-use-scenario) descreve esse cenário.

### Integração ponto a ponto do AEM/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Ao trabalhar com ativos nessa solução, você executa um dos seguintes procedimentos:

* Faça upload de ativos diretamente no Dynamic Media Classic e acesse por meio do navegador de conteúdo **Dynamic Media Classic** para criação de página ou
* Faça upload para o AEM Assets e ative a publicação automática para o Dynamic Media Classic; você acessa o navegador de conteúdo **Assets** para criação de página

Os componentes usados para essa integração são encontrados na área de componente **Dynamic Media Classic** no [Modo Design.](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEM Dynamic Media {#aem-dynamic-media}

AEM Dynamic Media é a unificação dos recursos do Dynamic Media Classic diretamente da plataforma AEM.

Ao trabalhar com ativos nessa solução, você segue este fluxo de trabalho:

1. Faça upload de ativos de imagem e vídeo únicos diretamente no AEM.
1. Codifique vídeos diretamente no AEM.
1. Crie conjuntos baseados em imagens diretamente no AEM.
1. Se aplicável, adicione interatividade a imagens ou vídeos.

Os componentes usados para o Dynamic Media são encontrados na área de componente **[!UICONTROL Dynamic Media]** em [Modo de design](/help/sites-authoring/author-environment-tools.md#page-modes). Eles incluem:

* **[!UICONTROL Dynamic Media]**  - O  **[!UICONTROL componente]** dinâmico é inteligente. Dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. O componente oferece suporte a predefinições de imagem, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

* **[!UICONTROL Mídia interativa]**  - O  **[!UICONTROL componente]** interativo é para esses ativos, como banners de carrossel, imagens interativas e vídeo interativo, que têm interatividade sobre eles, pontos de acesso ou mapas de imagem. Esse componente é inteligente. Dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

### Cenário de dupla utilização {#dual-use-scenario}

Imediatamente, você pode usar os recursos de integração do Dynamic Media e do Dynamic Media Classic do AEM simultaneamente. A tabela de casos de uso a seguir descreve quando você ativa e desativa determinadas áreas.

Para usar o Dynamic Media e o Dynamic Media Classic simultaneamente:

1. Configure [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) nos serviços em nuvem.
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
    <td>Fazer upload de ativos para AEM e usar AEM componente do Dynamic Media para criar ativos nas páginas do Sites</td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Ligado</a></td>
    <td>Desativado</td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>No varejo e são novos no Sites e no Dynamic Media</td>
    <td>Faça upload de ativos não relacionados ao produto para AEM para gerenciamento e entrega. Faça upload de ativos de produto para o Dynamic Media Classic e use o navegador de conteúdo do Dynamic Media Classic no AEM e componente para criar Páginas de detalhes do produto no Sites.</td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Ligado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Novo no Assets e no Dynamic Media</td>
    <td>Fazer upload de ativos para o AEM Assets e usar o URL/código incorporado publicado do Dynamic Media</td>
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
    <td>Faça upload de ativos para o Dynamic Media Classic e use AEM navegador de conteúdo do Dynamic Media Classic para pesquisar e criar ativos nas páginas do Sites</td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Um cliente Dynamic Media Classic existente e são novos em Sites e Ativos</td>
    <td>Faça upload de ativos no DAM e publique automaticamente no Dynamic Media Classic para entrega. Use AEM navegador de conteúdo do Dynamic Media Classic para pesquisar e criar ativos nas páginas do Sites.</td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Ligado</a></p> <p>(Veja a etapa 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente Dynamic Media Classic existente e novo no Assets</td>
    <td><p>Faça upload de ativos para AEM e usar o Dynamic Media para gerar representações para download/compartilhamento. Publicar automaticamente AEM ativos no Dynamic Media Classic para entrega.</p> <p><strong>Importante:</strong> processar duplicado e as representações geradas no AEM não serão sincronizadas com o Dynamic Media Classic</p> </td>
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
   1. (Opcional) Restrinja o upload do ativo Dynamic Media Classic por tipo MIME em [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). Os tipos MIME de ativos que não estão nessa lista não serão carregados no servidor do Dynamic Media Classic.
   1. (Opcional) Configurar vídeo na configuração do Dynamic Media Classic. Você pode ativar a codificação de vídeo para o Dynamic Media ou para o Dynamic Media Classic simultaneamente. As representações dinâmicas são usadas para visualização e reprodução local em AEM instância, enquanto as representações de vídeo do Dynamic Media Classic são geradas e armazenadas nos servidores do Dynamic Media Classic. Ao configurar serviços de codificação de vídeo para o Dynamic Media e o Dynamic Media Classic, aplique um [perfil de processamento de vídeo](/help/assets/video-profiles.md) à pasta de ativos do Dynamic Media Classic.
   1. (Opcional) [Configurar visualização segura no Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Limitações           {#limitations}

Quando o Dynamic Media Classic e o Dynamic Media estão habilitados, há as seguintes limitações:

* Fazer upload manual no Dynamic Media Classic, selecionando um ativo e arrastando-o para um componente do Dynamic Media Classic em uma página de AEM não funciona.
* Mesmo que os ativos sincronizados AEM-Dynamic Media Classic sejam atualizados para o Dynamic Media Classic automaticamente quando o ativo é editado no Assets, uma ação de reversão não aciona um novo upload, portanto, o Dynamic Media Classic não obteria a versão mais recente imediatamente após uma reversão. A solução alternativa é editar novamente quando a reversão for concluída.
* Se você precisar usar o Dynamic Media para um caso de uso e a integração do Dynamic Media Classic para outro caso de uso, para que os ativos do Dynamic Media não interajam com o sistema do Dynamic Media Classic, não aplique a configuração do Dynamic Media Classic à pasta do Dynamic Media ou a configuração do Dynamic Media (perfil de processamento) para uma pasta do Dynamic Media Classic.

## Práticas recomendadas para integrar o Dynamic Media Classic com AEM {#best-practices-for-integrating-scene-with-aem}

Ao integrar o Dynamic Media Classic com o AEM, há algumas práticas recomendadas importantes que precisam ser observadas nas seguintes áreas:

* Teste da integração
* Upload de ativos diretamente do Dynamic Media Classic recomendado para determinados cenários

Consulte [limitações conhecidas](#known-limitations-and-design-implications).

### Teste sua integração {#test-driving-your-integration}

O Adobe recomenda testar e direcionar a integração fazendo com que a pasta raiz aponte para uma subpasta somente em vez de para uma empresa inteira.

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode demorar muito para ser exibida no AEM. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos (por exemplo, a pasta raiz geralmente terá muitos ativos e poderá travar o sistema).

### Upload de ativos do AEM Assets versus do Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Você pode fazer upload de ativos usando a funcionalidade Ativos (gerenciamento de ativos digitais) ou acessando o Dynamic Media Classic diretamente no AEM por meio do navegador de conteúdo do Dynamic Media Classic. O que você escolher depende dos seguintes fatores:

* Os tipos de ativos do Dynamic Media Classic que o AEM Assets ainda não suporta precisam ser adicionados a um site de AEM do Dynamic Media Classic diretamente, por meio do navegador de conteúdo do Dynamic Media Classic, por exemplo, modelos de imagem.
* Para tipos de ativos compatíveis com o AEM Assets e o Dynamic Media Classic, decidir como fazer upload deles depende do seguinte:

   * Onde os ativos estão hoje E
   * Como é importante gerenciá-los em um repositório comum

Se os ativos já estiverem no Dynamic Media Classic e gerenciá-los em um repositório comum não for tão importante, exportar para o AEM Assets somente para sincronizá-los de volta ao Dynamic Media Classic para entrega seria uma viagem de ida e volta desnecessária. Caso contrário, manter os ativos em um único repositório e sincronizar com o Dynamic Media Classic somente para entrega pode ser preferível.

## Configuração da integração do Dynamic Media Classic {#configuring-scene-integration}

Você pode configurar AEM para fazer upload de ativos no Dynamic Media Classic. Os ativos de uma pasta de destino CQ podem ser carregados (automática ou manualmente) de AEM para uma conta de empresa do Dynamic Media Classic.

>[!NOTE]
>
>O Adobe recomenda usar somente a pasta de destino designada para importar ativos do Dynamic Media Classic. Os ativos digitais que estão fora da pasta de destino só podem ser usados nos componentes do Dynamic Media Classic nas páginas em que a configuração do Dynamic Media Classic foi ativada. Além disso, elas são colocadas em uma pasta ad hoc no Dynamic Media Classic. A pasta adhoc não é sincronizada com o AEM (mas os ativos podem ser descobertos no navegador de conteúdo do Dynamic Media Classic).

Para configurar o Dynamic Media Classic para integrar com o AEM, você precisa concluir as seguintes etapas:

1. [Definir uma configuração de nuvem](#creating-a-cloud-configuration-for-scene)  - Define o mapeamento entre uma pasta do Dynamic Media Classic e uma pasta do Assets. É necessário concluir essa etapa mesmo se quiser apenas a sincronização unidirecional (AEM Assets para Dynamic Media Classic).
1. [Ative o ouvinte de dam do  **Adobe CQ s7dam**](#enabling-the-adobe-cq-scene-dam-listener)  - Feito no   console OSGi.
1. Se quiser que AEM ativos sejam carregados automaticamente no Dynamic Media Classic, ative essa opção e adicione o Dynamic Media Classic ao fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] . Também é possível fazer upload manual de ativos.
1. Adicionar componentes do Dynamic Media Classic ao sidekick. Isso permite que os usuários usem componentes do Dynamic Media Classic em suas páginas de AEM.
1. [Mapear a configuração para a página em AEM](#enabling-scene-for-wcm)  - Essa etapa é necessária para exibir todas as predefinições de vídeo que você criou no Dynamic Media Classic. Também é necessário se você precisar executar uma publicação de ativo de fora da pasta de destino CQ para o Dynamic Media Classic.

Esta seção aborda como executar todas essas etapas e lista limitações importantes.

### Como a sincronização entre o Dynamic Media Classic e o AEM Assets funciona {#how-synchronization-between-scene-and-aem-assets-works}

Ao configurar a sincronização do AEM Assets e do Dynamic Media Classic, é importante entender o seguinte:

#### Upload para o Dynamic Media Classic a partir do AEM Assets {#uploading-to-scene-from-aem-assets}

* Há uma pasta de sincronização designada no AEM para uploads do Dynamic Media Classic.
* Os uploads para o Dynamic Media Classic podem ser automatizados se os ativos digitais forem colocados na pasta de sincronização designada.
* A estrutura de pastas e subpastas no AEM é replicada no Dynamic Media Classic.

>[!NOTE]
>
>AEM incorpora todos os metadados como XMP antes de carregá-los no Dynamic Media Classic, de modo que todas as propriedades no nó de metadados estejam disponíveis no Dynamic Media Classic como XMP.

#### Limitações conhecidas e implicações de design {#known-limitations-and-design-implications}

Com a sincronização entre o AEM Assets e o Dynamic Media Classic, há atualmente as seguintes limitações/implicações de design:

<table>
 <tbody>
  <tr>
   <td><strong>Limitação/implicação de projeto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Uma pasta designada de sincronização (target)</td>
   <td>Você só pode ter uma pasta designada por empresa no AEM para uploads do Dynamic Media Classic. Você pode criar várias configurações se precisar ter acesso a mais de uma conta de empresa no Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Estrutura de pastas</td>
   <td>Se você excluir uma pasta sincronizada com ativos, todos os ativos remotos do Dynamic Media Classic serão excluídos, mas a pasta permanecerá.</td>
  </tr>
  <tr>
   <td>Pasta ad-hoc</td>
   <td>Os ativos que estão fora da pasta de destino carregada manualmente no Dynamic Media Classic no WCM são colocados automaticamente em uma pasta ad hoc separada no Dynamic Media Classic. Isso é configurado na configuração da nuvem no AEM.</td>
  </tr>
  <tr>
   <td>Mídia mista</td>
   <td>Os conjuntos de mídia mista são exibidos no AEM, embora não sejam compatíveis com o AEM.</td>
  </tr>
  <tr>
   <td>PDFs</td>
   <td>Os PDFs gerados a partir de eCatalogs no Dynamic Media Classic são importados para a pasta de destino CQ.</td>
  </tr>
  <tr>
   <td>Atualização da interface do usuário</td>
   <td>Ao sincronizar o AEM com o Dynamic Media Classic, atualize a interface do usuário para exibir as alterações. </td>
  </tr>
  <tr>
   <td>Miniaturas de vídeo</td>
   <td>Se o upload de um vídeo para o AEM Assets for codificado via Dynamic Media Classic, as miniaturas de vídeo e os vídeos codificados poderão levar algum tempo para estarem disponíveis no AEM Assets, dependendo do tempo de processamento do vídeo.</td>
  </tr>
  <tr>
   <td>Subpastas do Target</td>
   <td><p>Se você estiver usando subpastas dentro da pasta de destino, certifique-se de usar nomes exclusivos para cada ativo (independentemente da localização) ou configurar o Dynamic Media Classic (na área Configuração) para não substituir ativos independentemente da localização.</p> <p>Caso contrário, os ativos com o mesmo nome que são carregados em uma subpasta de destino do Dynamic Media Classic serão carregados, mas o ativo com o mesmo nome na pasta de destino será excluído. </p> </td>
  </tr>
 </tbody>
</table>

### Configuração dos servidores Dynamic Media Classic {#configuring-scene-servers}

Se você executar AEM atrás de um proxy ou tiver configurações de firewall especiais, talvez seja necessário ativar explicitamente os hosts das diferentes regiões. Os servidores são gerenciados no conteúdo em `/etc/cloudservices/scene7/endpoints` e podem ser personalizados conforme necessário. Toque em um URL e edite para alterar o URL, se necessário. Em versões anteriores do AEM, esses valores eram codificados.

Se você navegar até `/etc/cloudservices/scene7/endpoints.html`, verá os servidores listados (e poderá editá-los clicando no URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Criação de uma configuração de nuvem para o Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Uma configuração de nuvem define o mapeamento entre uma pasta do Dynamic Media Classic e uma pasta do AEM Assets. Ele precisa ser configurado para sincronizar o AEM Assets com o Dynamic Media Classic. Consulte Como a sincronização funciona para obter mais informações.

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode demorar muito para ser exibida no AEM. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos (por exemplo, a pasta raiz geralmente terá muitos ativos).
>
>Se quiser testar a integração, talvez você queira que a pasta raiz aponte apenas para uma subpasta, em vez da empresa inteira.

>[!NOTE]
>
>É possível ter várias configurações: uma configuração de nuvem representa um usuário em uma empresa do Dynamic Media Classic. Se quiser acessar outras empresas ou usuários do Dynamic Media Classic, é necessário criar várias configurações.

Para configurar o AEM para poder publicar ativos no Dynamic Media Classic:

1. Toque no ícone AEM e navegue até **[!UICONTROL Deployment > Cloud Services]** para acessar o Adobe Dynamic Media Classic.

1. Toque em **[!UICONTROL Configurar agora.]**

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. No campo **[!UICONTROL Title]** e, opcionalmente, no campo **[!UICONTROL Name]**, insira as informações apropriadas. Toque em **[!UICONTROL Criar.]**

   >[!NOTE]
   >
   >Ao criar configurações adicionais, o campo **[!UICONTROL configuração pai]** é exibido.
   >
   >Faça **not** alterar a configuração pai. Alterar a configuração pai pode interromper a integração.

1. Insira o endereço de email, senha e região da sua conta do Dynamic Media Classic e toque em **[!UICONTROL Conectar-se ao Dynamic Media Classic.]** Você está conectado ao servidor Dynamic Media Classic e a caixa de diálogo é expandida com mais opções.

1. Insira o nome **[!UICONTROL Company]** e **[!UICONTROL Root Path]** (esse é o nome do servidor publicado junto com qualquer caminho que você deseja especificar; se você não souber o nome do servidor publicado, no Dynamic Media Classic, vá para **[!UICONTROL Configuração > Configuração do aplicativo.]**)

   >[!NOTE]
   >
   >O caminho raiz do Dynamic Media Classic é a pasta do Dynamic Media Classic AEM se conecta. Ele pode ser limitado a uma pasta específica.

   >[!CAUTION]
   >
   >Dependendo do tamanho da pasta Dynamic Media Classic, a importação de uma pasta raiz pode demorar muito. Além disso, os dados do Dynamic Media Classic podem exceder o armazenamento de AEM. Certifique-se de que está importando a pasta correta. Importar muitos dados pode parar o sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Clique em **[!UICONTROL OK.]** AEM salva sua configuração.

>[!NOTE]
>
>Se estiver reconectando:
>
>* Ao reconectar-se ao Dynamic Media Classic na publicação, talvez seja necessário redefinir a senha ao publicar ou a reconexão não funcionará. Isso não é um problema na instância do autor.
>* Se você modificar valores como sua região, nome da empresa, será necessário reconectar-se ao Dynamic Media Classic. Se as opções de configuração tiverem sido modificadas, mas não tiverem sido salvas, AEM ainda indicar erroneamente que a configuração é válida. Certifique-se de reconectar.

>



### Ativar o ouvinte de Dam do Adobe CQ Dynamic Media Classic {#enabling-the-adobe-cq-scene-dam-listener}

Você deve ativar o Ouvinte de Dam do Adobe CQ Dynamic Media Classic, que é desativado por padrão.

Para habilitá-lo:

1. Toque no ícone [!UICONTROL Ferramentas] e navegue até **[!UICONTROL Operações > Console da Web.]** O console da Web é aberto.
1. Navegue até **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** e selecione a caixa de seleção **[!UICONTROL Enabled]**.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Toque em **[!UICONTROL Salvar.]**

### Adicionar tempo limite configurável ao fluxo de trabalho de Upload do Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Quando uma instância de AEM é configurada para lidar com a codificação de vídeo por meio do Dynamic Media Classic, por padrão, há um tempo limite de 35 minutos em qualquer trabalho de upload. Para acomodar trabalhos de codificação de vídeo potencialmente mais longos, é possível configurar esta configuração:

1. Navegue até **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Altere o número conforme desejado no campo **[!UICONTROL Tempo limite do trabalho ativo]**. Qualquer número não negativo é aceite com a unidade de medida em segundos. Por padrão, é definido como 2100.

   >[!NOTE]
   >
   >Prática recomendada: A maioria dos ativos é assimilada em no máximo minutos (por exemplo, imagens). Mas em determinadas instâncias - vídeos maiores, por exemplo - o valor de tempo limite deve ser aumentado para 7.200 segundos (2 horas) para acomodar o tempo de processamento longo. Caso contrário, esse trabalho de upload do Dynamic Media Classic será marcado como **[!UICONTROL UploadFailed]** nos metadados JCR.

1. Toque em **[!UICONTROL Salvar.]**

### Carregamento automático do AEM Assets {#autouploading-from-aem-assets}

A partir do AEM 6.3.2, o AEM Assets agora é configurado para você, para que todos os ativos digitais carregados no gerenciador de ativos digitais sejam atualizados automaticamente para o Dynamic Media Classic se os ativos estiverem em uma pasta de destino CQ.

Quando um ativo é adicionado ao AEM Assets, ele é carregado e publicado automaticamente no Dynamic Media Classic.

>[!NOTE]
>
>O tamanho máximo de arquivo para o upload automático do AEM Assets para o Dynamic Media Classic é de 500 MB.

Para configurar o upload automático do AEM Assets:

1. Toque no ícone AEM e navegue até **[!UICONTROL Implantação > Cloud Services]** e, no cabeçalho Dynamic Media, em Configurações disponíveis, toque em **[!UICONTROL dms7 (Dynamic Media]**)
1. Toque na guia **[!UICONTROL Avançado]**, marque a caixa de seleção **[!UICONTROL Ativar upload automático]** e toque em **[!UICONTROL OK.]** Agora é necessário configurar o fluxo de trabalho do Ativo DAM para incluir o upload para o Dynamic Media Classic.

   >[!NOTE]
   >
   >Consulte [Configuração do estado (publicado/não publicado) de ativos enviados para o Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) para obter informações sobre como enviar ativos para o Dynamic Media Classic em um estado não publicado.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Navegue de volta à página de boas-vindas AEM e toque em **[!UICONTROL Fluxos de trabalho.]** Clique duas vezes no workflow do  **DAM Update** Assets para abri-lo.
1. No sidekick, navegue até os componentes **[!UICONTROL Fluxo de trabalho]** e selecione **[!UICONTROL Dynamic Media Classic.]** Arraste o  **[!UICONTROL Dynamic Media]** Classic para o workflow e toque em  **[!UICONTROL Salvar.]** Os ativos adicionados ao AEM Assets na pasta de destino serão carregados automaticamente no Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Ao adicionar ativos após a automação, se eles não forem colocados na pasta de destino do CQ, eles não serão carregados no Dynamic Media Classic.
   >* AEM incorpora todos os metadados como XMP antes de carregá-los no Dynamic Media Classic, de modo que todas as propriedades no nó de metadados estejam disponíveis no Dynamic Media Classic como XMP.


### Configurar o estado (publicado/não publicado) dos ativos enviados para o Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Se você estiver enviando ativos do AEM Assets para o Dynamic Media Classic, poderá publicá-los automaticamente (comportamento padrão) ou enviá-los para o Dynamic Media Classic em um estado não publicado.

Talvez você não queira publicar ativos imediatamente no Dynamic Media Classic se quiser testá-los em um ambiente de preparo antes de entrar em funcionamento. Você pode usar o AEM com o ambiente de teste seguro do Dynamic Media Classic para enviar ativos diretamente do Assets para o Dynamic Media Classic em um estado não publicado.

Os ativos do Dynamic Media Classic permanecem disponíveis por meio da visualização segura. Somente quando os ativos são publicados no AEM os ativos do Dynamic Media Classic também entram em produção.

Se você quiser publicar ativos imediatamente ao enviá-los para o Dynamic Media Classic, não precisará configurar nenhuma opção. Esse é o comportamento padrão.

No entanto, se você não quiser que os ativos enviados para o Dynamic Media Classic sejam publicados automaticamente, esta seção descreve como configurar o AEM e o Dynamic Media Classic para fazer isso.

#### Pré-requisitos para enviar ativos para o Dynamic Media Classic não publicados {#prerequisites-to-push-assets-to-scene-unpublished}

Antes de enviar ativos para o Dynamic Media Classic sem publicá-los, você deve configurar o seguinte:

1. [Use o Admin Console para criar um caso de suporte.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) No seu caso de suporte, solicite que a visualização segura seja ativada para sua conta do Dynamic Media Classic.
1. Siga as instruções para [configurar visualização segura para sua conta do Dynamic Media Classic.](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

Essas são as mesmas etapas que você seguiria para criar qualquer configuração de teste seguro no Dynamic Media Classic.

>[!NOTE]
>
>Se o seu ambiente de instalação for um sistema operacional Unix de 64 bits, consulte [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) sobre as opções de configuração adicionais que você precisa definir.

#### Limitações conhecidas para enviar ativos no estado não publicado {#known-limitations-for-pushing-assets-in-unpublished-state}

Se você usar esse recurso, observe as seguintes limitações:

* Não há suporte para controle de versão.
* Se um ativo já estiver publicado no AEM e uma versão subsequente for criada, essa nova versão será publicada imediatamente ao vivo para produção. Publicar na ativação só funciona com a publicação inicial de um ativo.

>[!NOTE]
>
>Se você deseja publicar ativos instantaneamente, a prática recomendada é manter **[!UICONTROL Ativar visualização segura]** definido como **[!UICONTROL Imediatamente]** e usar o recurso **[!UICONTROL Ativar upload automático]**.

### Definir o estado dos ativos enviados para o Dynamic Media Classic como não publicados {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Se um usuário publicar o ativo no AEM, ele automaticamente acionará o ativo S7 para o ativo de produção/ao vivo (o ativo não estará mais em visualização segura/não será publicado).

Para definir o estado dos ativos enviados para o Dynamic Media Classic como não publicados:

1. Toque no ícone AEM e navegue até **[!UICONTROL Deployment > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** e selecione a configuração no Dynamic Media Classic.
1. Toque na guia **[!UICONTROL Avançado]**. No menu suspenso **[!UICONTROL Ativar Exibição segura]**, selecione **[!UICONTROL Na ativação de publicação do AEM]** para enviar ativos para o Dynamic Media Classic sem publicação. (Por padrão, esse valor é definido como **[!UICONTROL Imediatamente]**, onde os ativos do Dynamic Media Classic são publicados imediatamente.)

   Consulte a [documentação do Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) para obter mais informações sobre como testar ativos antes de torná-los públicos.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Toque em **[!UICONTROL OK.]**

Habilitar a Exibição segura significa que seus ativos são encaminhados para o servidor de visualização seguro e não publicados.

Você pode verificar isso navegando até um componente do Dynamic Media Classic em uma página no AEM e tocando em **[!UICONTROL Editar.]** O ativo terá o servidor de visualização seguro listado no URL. Após a publicação no AEM, o domínio do servidor na referência do arquivo é atualizado do URL de visualização para o URL de produção.

### Ativar o Dynamic Media Classic para WCM {#enabling-scene-for-wcm}

A ativação do Dynamic Media Classic para WCM é necessária por dois motivos:

* Para ativar a lista suspensa de perfis de vídeo universais para criação de página. Sem isso, o menu suspenso **[!UICONTROL Universal Video Preset]** fica vazio e não pode ser definido.
* Se um ativo digital não estiver na pasta de destino, você poderá fazer upload do ativo para o Dynamic Media Classic se ativar o Dynamic Media Classic para essa página nas propriedades da página e arrastar e soltar o ativo em um componente Dynamic Media Classic. As regras de herança normais se aplicam (o que significa que as páginas secundárias herdarão a configuração da página principal).

Ao ativar o Dynamic Media Classic para o WCM, observe que, como em outras configurações, as regras de herança se aplicam. Você pode ativar o Dynamic Media Classic para WCM na interface otimizada para toque ou clássica.

#### Ativar o Dynamic Media Classic para WCM na interface otimizada para toque {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

Para ativar o Dynamic Media Classic para WCM na interface otimizada para toque:

1. Toque no ícone de AEM e navegue até **[!UICONTROL Sites]** e, em seguida, na página raiz do site (não específico de idioma).

1. Na barra de ferramentas, selecione o ícone [!UICONTROL settings] e toque em **[!UICONTROL Abrir propriedades.]**

1. Toque em **[!UICONTROL Cloud Services]** e toque em **[!UICONTROL Adicionar configuração]** e selecione **[!UICONTROL Dynamic Media Classic.]**
1. Na lista suspensa **[!UICONTROL Adobe Dynamic Media Classic]**, selecione a configuração desejada e toque em **[!UICONTROL OK.]**

   ![chlimage_1-303](assets/chlimage_1-303.png)

   As predefinições de vídeo dessa configuração do Dynamic Media Classic estão disponíveis para uso no AEM com o componente de vídeo do Dynamic Media Classic nessa página e páginas filhas.

#### Ativar o Dynamic Media Classic para WCM na interface de usuário clássica {#enabling-scene-for-wcm-in-the-classic-user-interface}

Para ativar o Dynamic Media Classic para WCM na interface clássica:

1. Em AEM, toque em **[!UICONTROL Sites]** e navegue até a página raiz do seu site (não específico de idioma).

1. No sidekick, toque no ícone **[!UICONTROL Página]** e toque em **[!UICONTROL Propriedades da página.]**

1. Toque em **[!UICONTROL Cloud Services > Adicionar serviços > Dynamic Media Classic.]**
1. Na lista suspensa **[!UICONTROL Adobe Dynamic Media Classic]**, selecione a configuração desejada e toque em **[!UICONTROL OK.]**

   As predefinições de vídeo dessa configuração do Dynamic Media Classic estão disponíveis para uso no AEM com o componente de vídeo do Dynamic Media Classic nessa página e páginas filhas.

### Configurar uma configuração padrão {#configuring-a-default-configuration}

Se você tiver várias configurações do Dynamic Media Classic, poderá especificar uma delas como padrão para o navegador de conteúdo do Dynamic Media Classic.

Somente uma configuração do Dynamic Media Classic pode ser marcada como padrão em um determinado momento. A configuração padrão são os ativos da empresa exibidos por padrão no Navegador de conteúdo do Dynamic Media Classic.

Para configurar a configuração padrão:

1. Toque no ícone AEM e navegue até **[!UICONTROL Deployment > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** e selecione a configuração no Dynamic Media Classic.
1. Toque em **[!UICONTROL Editar]** para abrir a configuração.

1. Na guia **[!UICONTROL General]**, marque a caixa de seleção **[!UICONTROL Configuração padrão]** para tornar essa a empresa padrão e o caminho raiz que aparecem no navegador de conteúdo do Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Se houver apenas uma configuração, marcar a caixa de seleção **[!UICONTROL Configuração padrão]** não terá efeito.

### Configuração da pasta ad-hoc {#configuring-the-ad-hoc-folder}

Você pode configurar a pasta para a qual os ativos são carregados no Dynamic Media Classic quando o ativo não estiver localizado na pasta de destino CQ. Consulte Publicação de ativos fora da pasta de destino CQ.

Para configurar a pasta adhoc:

1. Toque no ícone AEM e navegue até **[!UICONTROL Deployment > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** e selecione a configuração no Dynamic Media Classic.
1. Toque em **[!UICONTROL Editar]** para abrir a configuração.

1. Toque na guia **[!UICONTROL Avançado]**. No campo **[!UICONTROL Pasta ad-hoc]**, você pode modificar a pasta **Ad-hoc**. Por padrão, é o **name_of_the_company/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configuração de predefinições universais {#configuring-universal-presets}

Para configurar as Predefinições universais para o componente de vídeo, consulte [Vídeo](/help/assets/s7-video.md).

## Ativar o suporte ao parâmetro de trabalho de upload do Assets/Dynamic Media Classic baseado no tipo MIME {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Você pode ativar parâmetros de tarefas de upload configuráveis do Dynamic Media Classic que são acionadas pela sincronização do Digital Asset Manager/Dynamic Media Classic assets.

Especificamente, você configura o formato de arquivo aceito por tipo MIME na área OSGi (iniciativa do Open Service Gateway) do painel Configuração do Console da Web AEM. Em seguida, você pode personalizar os parâmetros de trabalho de upload individuais que são usados para cada tipo MIME no JCR (Java Content Repository).

**Para ativar ativos baseados em tipo MIME:**

1. Toque no ícone AEM e navegue até **[!UICONTROL Ferramentas > Operações > Console da Web.]**
1. No painel Configuração do console da Web do Adobe Experience Manager, no menu **[!UICONTROL OSGi]**, toque em **[!UICONTROL Configuração.]**
1. Na coluna Nome , localize e toque em **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** para editar a configuração.
1. Na área Mapeamento de tipo MIME, toque em qualquer sinal de mais (+) para adicionar um tipo MIME.

   Consulte [Tipos MIME suportados](/help/assets/assets-formats.md#supported-mime-types).

1. No campo de texto, digite o novo nome do tipo MIME.

   Por exemplo, você digitaria um `<file_extension>=<mime_type>` como em `EPS=application/postscript` OU `PSD=image/vnd.adobe.photoshop`.

1. No canto inferior direito da janela de configuração, toque em **[!UICONTROL Save.]**
1. Volte para AEM e, no painel esquerdo, toque em CRXDE Lite.
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
   >`process=MaintainLayers&createTemplate=true`
   >
   >Certifique-se de que o arquivo PSD tenha &quot;camadas&quot;. Se for estritamente uma imagem ou uma imagem com máscara, ela será processada como uma imagem porque não há camadas para processar.

1. No canto superior esquerdo da página CRXDE Lite, toque em **[!UICONTROL Salvar tudo.]**

## Solução de problemas do Dynamic Media Classic e integração de AEM {#troubleshooting-scene-and-aem-integration}

Se tiver problemas para integrar o AEM com o Dynamic Media Classic, consulte os seguintes cenários para soluções.

**Se a publicação de ativos digitais no Dynamic Media Classic falhar:**

* Verifique se o ativo que você está tentando fazer upload está na pasta **[!UICONTROL CQ target]** (você especifica essa pasta na configuração de nuvem do Dynamic Media Classic).
* Caso contrário, você precisará configurar a configuração de nuvem em **[!UICONTROL Propriedades da página]** para essa página para permitir o upload para a pasta **[!UICONTROL CQ adhoc]**.

* Verifique os logs para obter qualquer informação.

**Se as predefinições de vídeo não forem exibidas:**

* Verifique se você configurou a configuração de nuvem dessa página por meio das **[!UICONTROL Propriedades da página.]** As predefinições de vídeo estão disponíveis no componente de vídeo do Dynamic Media Classic.

**Se os ativos de vídeo não forem reproduzidos no AEM:**

* Certifique-se de ter usado o componente de vídeo correto. O componente de vídeo do Dynamic Media Classic é diferente do componente básico de Vídeo. Consulte [Componente de vídeo de base versus Componente de vídeo do Dynamic Media Classic](/help/assets/s7-video.md).

**Se os ativos novos ou modificados no AEM não forem carregados automaticamente no Dynamic Media Classic:**

* Certifique-se de que os ativos estejam na pasta de destino do CQ. Somente os ativos que estão na pasta de destino do CQ são atualizados automaticamente (desde que você tenha configurado o AEM Assets para fazer upload automático dos ativos).
* Certifique-se de ter configurado a configuração do Cloud Services para Ativar o upload automático e que você atualizou e salvou o fluxo de trabalho do Ativo do DAM para incluir o upload do Dynamic Media Classic.
* Ao fazer upload de uma imagem em uma subpasta da pasta de destino do Dynamic Media Classic, siga um destes procedimentos:

   * Certifique-se de que os nomes de todos os ativos, independentemente da localização, sejam exclusivos. Caso contrário, o ativo na pasta de destino principal será excluído e somente o ativo na subpasta permanecerá.
   * Altere como o Dynamic Media Classic substitui ativos na área Configuração da conta do Dynamic Media Classic. Não defina o Dynamic Media Classic para substituir ativos, independentemente do local, se você usar ativos com o mesmo nome em subpastas.

**Se os ativos ou pastas excluídos não forem sincronizados entre o Dynamic Media Classic e o AEM:**

* Os ativos e pastas excluídos no AEM Assets ainda são exibidos na pasta sincronizada no Dynamic Media Classic. Você deve excluí-los manualmente.

**Se o upload de vídeo falhar**

* Se o upload de vídeo falhar e você estiver usando AEM para codificar vídeo por meio da integração com o Dynamic Media Classic, consulte [Adicionar tempo limite configurável ao fluxo de trabalho de upload do Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode demorar muito para ser exibida no AEM. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos (por exemplo, a pasta raiz geralmente terá muitos ativos).
>
>Se quiser testar a integração, talvez você queira que a pasta raiz aponte apenas para uma subpasta, em vez da empresa inteira.

