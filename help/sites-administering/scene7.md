---
title: Integrar o Adobe Experience Manager ao Dynamic Media Classic
description: Saiba como integrar o Adobe Experience Manager com o Dynamic Media Classic.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '5484'
ht-degree: 1%

---

# Integrar o Adobe Experience Manager ao Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}

O Adobe Dynamic Media Classic é uma solução hospedada para gerenciar, aprimorar, publicar e fornecer ativos de mídia avançada para Web, dispositivos móveis, email, impressão e monitores conectados à Internet.

Para usar o Dynamic Media Classic, você deve configurar a configuração de nuvem para que o Dynamic Media Classic e o Adobe Experience Manager Assets possam interagir entre si. Este documento descreve como configurar o Experience Manager e o Dynamic Media Classic.

Para obter informações sobre como usar todos os componentes do Dynamic Media Classic em uma página e trabalhar com vídeo, consulte [Usar o Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* A plataforma do visualizador DHTML da Dynamic Media Classic chegou ao fim da vida útil oficialmente em 31 de janeiro de 2014. Para obter mais informações, consulte o [Perguntas frequentes sobre o fim da vida útil do visualizador DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Antes de configurar o Dynamic Media Classic para funcionar com o Experience Manager, consulte [Práticas recomendadas](#best-practices-for-integrating-scene-with-aem) para integrar o Dynamic Media Classic com o Experience Manager.
>* Se você usar o Dynamic Media Classic com uma configuração de proxy personalizada, deverá configurar ambas as configurações de proxy do cliente HTTP, pois algumas funcionalidades do Experience Manager usam as APIs 3.x e outras usam as APIs 4.x. 3.x está configurado com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) e 4.x está configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).
>


## Integração do Experience Manager/Dynamic Media Classic com o Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Os usuários do Experience Manager têm uma escolha entre duas soluções para trabalhar com o Dynamic Media. Você pode usar um dos seguintes:

* Integre sua instância do Experience Manager ao Dynamic Media Classic.
* Use o Dynamic Media integrado ao Experience Manager.

Use os seguintes critérios para determinar qual solução escolher:

* Você é um **existente** Cliente do Dynamic Media Classic cujos ativos residem no Dynamic Media Classic para publicação e entrega, mas você deseja integrar esses ativos com a criação do Sites (WCM), ou Experience Manager Assets, ou ambos? Em caso afirmativo, use a variável [Integração ponto a ponto do Experience Manager/Dynamic Media Classic](#aem-scene-point-to-point-integration) descrito neste documento.

* Se você for um **novo** Experience Manager cliente que tenha necessidades de fornecimento de mídia avançada, selecione o [Opção Dynamic Media](#aem-dynamic-media). Essa opção faz mais sentido se você não tiver uma conta do S7 e muitos ativos armazenados nesse sistema.

* Em certos casos, use ambas as soluções. O [cenário de dupla utilização](/help/sites-administering/scene7.md#dual-use-scenario) descreve esse cenário.

### Integração ponto a ponto do Experience Manager/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Ao trabalhar com ativos nessa solução, você executa um dos seguintes procedimentos:

* Faça upload de ativos diretamente no Dynamic Media Classic e acesse por meio do **Dynamic Media Classic** navegador de conteúdo para criação de página ou
* Faça upload para o Experience Manager Assets e ative a publicação automática no Dynamic Media Classic; você acessa via **Ativos** navegador de conteúdo para criação de página

Os componentes usados para essa integração são encontrados no **Dynamic Media Classic** área do componente em [Modo de design](/help/sites-authoring/author-environment-tools.md#page-modes).

### Experience Manager Dynamic Media {#aem-dynamic-media}

O Experience Manager Dynamic Media é a unificação dos recursos do Dynamic Media Classic diretamente na plataforma Experience Manager.

Ao trabalhar com ativos nessa solução, você segue este fluxo de trabalho:

1. Faça upload de ativos de imagem e vídeo únicos diretamente no Experience Manager.
1. Codifique vídeos diretamente no Experience Manager.
1. Crie conjuntos baseados em imagens diretamente no Experience Manager.
1. Se aplicável, adicione interatividade a imagens ou vídeos.

Os componentes que você usa para o Dynamic Media são encontrados no **[!UICONTROL Dynamic Media]** área do componente em [Modo de design](/help/sites-authoring/author-environment-tools.md#page-modes). Eles incluem:

* **[!UICONTROL Dynamic Media]** - O **[!UICONTROL Dynamic Media]** componente é inteligente - dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. O componente oferece suporte a predefinições de imagem, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

* **[!UICONTROL Mídia interativa]** - O **[!UICONTROL Mídia interativa]** O componente é para ativos como banners de carrossel, imagens interativas e vídeo interativo. Esses ativos têm interatividade em pontos de acesso ou mapas de imagem. Esse componente é inteligente. Ou seja, dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

### Cenário de dupla utilização {#dual-use-scenario}

Imediatamente, você pode usar os recursos de integração do Dynamic Media e do Dynamic Media Classic do Experience Manager simultaneamente. A tabela de casos de uso a seguir descreve quando você ativa e desativa determinadas áreas.

Para usar o Dynamic Media e o Dynamic Media Classic simultaneamente:

1. Configurar [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) no Cloud Services.
1. Siga as instruções específicas específicas do seu caso de uso:

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Integração do Dynamic Media Classic</strong></td>
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
    <td>Faça upload de ativos não relacionados ao produto para o Experience Manager para gerenciamento e entrega. Faça upload de ativos de PRODUTO para o Dynamic Media Classic e use o navegador de conteúdo Dynamic Media Classic no Experience Manager e componente para criar Páginas de detalhes do produto no Sites.</td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Ligado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Novo no Assets e no Dynamic Media</td>
    <td>Fazer upload de ativos para o Experience Manager Assets e usar o URL/código incorporado publicado do Dynamic Media</td>
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
    <td>Um cliente existente do Dynamic Media Classic e são novos em Sites</td>
    <td>Faça upload de ativos para o Dynamic Media Classic e use o navegador de conteúdo do Experience Manager Dynamic Media Classic para pesquisar e criar ativos nas páginas do Sites</td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td>Desativado</td>
    </tr>
    <tr>
    <td>Um cliente existente do Dynamic Media Classic e são novos em Sites e Ativos</td>
    <td>Faça upload de ativos no DAM e publique automaticamente no Dynamic Media Classic para entrega. Use o navegador de conteúdo Experience Manager Dynamic Media Classic para pesquisar e criar ativos nas páginas do Sites.</td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Ligado</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Ligado</a></p> <p>(Veja a etapa 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente Dynamic Media Classic existente e novo no Assets</td>
    <td><p>Faça upload de ativos no Experience Manager e use o Dynamic Media para gerar representações para download/compartilhamento. Publicar automaticamente ativos do Experience Manager no Dynamic Media Classic para entrega.</p> <p><strong>Importante:</strong> Processamento duplicado interno e representações geradas no Experience Manager não são sincronizadas com o Dynamic Media Classic</p> </td>
    <td><p>Ligado</p> <p>(Veja a etapa 3)</p> </td>
    <td>Desativado</td>
    <td>Desativado</td>
    <td><p><a href="#configuringautouploadingfromaemassets">Ligado</a></p> <p>(Veja a etapa 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Opcional; consulte tabela de casos de uso) - Configure o [Configuração da nuvem do Dynamic Media](/help/assets/config-dynamic.md) e [habilitar o servidor do Dynamic Media](/help/assets/config-dynamic.md).
1. (Opcional; consulte tabela de casos de uso) - Se você optar por ativar o Upload automático de ativos no Dynamic Media Classic, será necessário adicionar o seguinte:

   1. Configure o upload automático para o Dynamic Media Classic.
   1. Adicione o **Upload do Dynamic Media Classic** etapa depois de todas as etapas do fluxo de trabalho do Dynamic Media *no final de* **Ativo de atualização Dam** workflow ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Opcional) Restrinja o upload de ativos do Dynamic Media Classic por tipo MIME em [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). Os tipos MIME de ativos que não estão nessa lista não são carregados no servidor do Dynamic Media Classic.
   1. (Opcional) Configurar vídeo na configuração do Dynamic Media Classic. Você pode ativar a codificação de vídeo para Dynamic Media e Dynamic Media Classic simultaneamente. As representações dinâmicas são usadas para visualização e reprodução local na instância do Experience Manager, enquanto as representações de vídeo do Dynamic Media Classic são geradas e armazenadas nos servidores do Dynamic Media Classic. Ao configurar serviços de codificação de vídeo para Dynamic Media e Dynamic Media Classic, aplique uma [perfil de processamento de vídeo](/help/assets/video-profiles.md) para a pasta de ativos do Dynamic Media Classic.
   1. (Opcional) [Configurar visualização segura no Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Limitações {#limitations}

Quando o Dynamic Media Classic e o Dynamic Media estão habilitados, há as seguintes limitações:

* Fazer upload manual no Dynamic Media Classic selecionando um ativo e arrastando-o para um componente do Dynamic Media Classic em uma página do Experience Manager não funciona.
* Mesmo que os ativos sincronizados Experience Manager-Dynamic Media Classic sejam atualizados automaticamente para o Dynamic Media Classic quando o ativo é editado no Assets, uma ação de reversão não aciona um novo upload. Dessa forma, a Dynamic Media Classic não obtém a versão mais recente imediatamente após uma reversão. A solução alternativa é editar novamente após a conclusão da reversão.
* É necessário usar o Dynamic Media para um caso de uso e a integração do Dynamic Media Classic para outro, para que os ativos da Dynamic Media não interajam com o sistema do Dynamic Media Classic? Em caso positivo, não aplique a configuração do Dynamic Media Classic à pasta do Dynamic Media. E não aplique a configuração do Dynamic Media (perfil de processamento) a uma pasta do Dynamic Media Classic.

## Práticas recomendadas para integrar o Dynamic Media Classic com o Experience Manager {#best-practices-for-integrating-scene-with-aem}

Ao integrar o Dynamic Media Classic com o Experience Manager, há algumas práticas recomendadas importantes que devem ser observadas nas seguintes áreas:

* Teste da integração
* Upload de ativos diretamente do Dynamic Media Classic recomendado para determinados cenários

Consulte [limitações conhecidas](#known-limitations-and-design-implications).

### Teste sua integração {#test-driving-your-integration}

O Adobe recomenda testar e direcionar a integração fazendo com que a pasta raiz aponte para uma subpasta somente em vez de para uma empresa inteira.

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode levar muito tempo para ser exibida no Experience Manager. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos (por exemplo, a pasta raiz geralmente tem muitos ativos e pode travar o sistema).

### Fazer upload de ativos do Experience Manager Assets versus do Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Você pode fazer upload de ativos usando a funcionalidade Ativos (gerenciamento de ativos digitais) ou acessando o Dynamic Media Classic diretamente no Experience Manager por meio do navegador de conteúdo do Dynamic Media Classic. O que você escolher depende dos seguintes fatores:

* Os tipos de ativos do Dynamic Media Classic que o Experience Manager Assets ainda não suporta devem ser adicionados a um site do Experience Manager diretamente do Dynamic Media Classic, por meio do navegador de conteúdo do Dynamic Media Classic. Por exemplo, modelos de imagem.
* Para tipos de ativos compatíveis com o Experience Manager Assets e a Dynamic Media Classic, decidir como fazer upload deles depende do seguinte:

   * Onde os ativos estão hoje E
   * Como é importante gerenciá-los em um repositório comum

Suponha que os ativos já estejam no Dynamic Media Classic e gerenciá-los em um repositório comum não é importante. Se esse for o caso, exportar os ativos para o Experience Manager Assets somente para sincronizá-los de volta ao Dynamic Media Classic para entrega é uma viagem de ida e volta desnecessária. O Adobe recomenda manter os ativos em um único repositório e sincronizar com o Dynamic Media Classic somente para entrega.

## Configurar integração do Dynamic Media Classic {#configuring-scene-integration}

Você pode configurar o Experience Manager para fazer upload de ativos no Dynamic Media Classic. Os ativos de uma pasta de destino CQ podem ser carregados (automática ou manualmente) do Experience Manager para uma conta de empresa da Dynamic Media Classic.

>[!NOTE]
>
>O Adobe recomenda usar somente a pasta de destino designada para importar ativos do Dynamic Media Classic. Os ativos digitais que estão fora da pasta de destino só podem ser usados nos componentes do Dynamic Media Classic nas páginas em que a configuração do Dynamic Media Classic foi ativada. Além disso, elas são colocadas em uma pasta sob demanda no Dynamic Media Classic. A pasta sob demanda não é sincronizada com o Experience Manager (mas os ativos podem ser descobertos no navegador de conteúdo Dynamic Media Classic).

**Para configurar o Dynamic Media Classic para integrar com o Experience Manager:**

1. [Definir uma configuração de nuvem](#creating-a-cloud-configuration-for-scene) - Define o mapeamento entre uma pasta Dynamic Media Classic e uma pasta Ativos. Conclua esta etapa mesmo se desejar apenas sincronização unidirecional (Experience Manager Assets para Dynamic Media Classic).
1. [Ative o **Ouvinte de Dam do Adobe CQ s7dam**](#enabling-the-adobe-cq-scene-dam-listener) - Feito no [!UICONTROL OSGi] console.
1. Se você deseja que o Experience Manager Assets faça upload automático para o Dynamic Media Classic, ative essa opção e adicione o Dynamic Media Classic ao [!UICONTROL Ativo de atualização DAM] fluxo de trabalho. Também é possível fazer upload manual de ativos.
1. Adicionar componentes do Dynamic Media Classic ao sidekick. Essa funcionalidade permite que os usuários usem componentes do Dynamic Media Classic em suas páginas do Experience Manager.
1. [Mapeie a configuração para a página no Experience Manager](#enabling-scene-for-wcm) - Esta etapa é necessária para exibir todas as predefinições de vídeo criadas no Dynamic Media Classic. Também é necessário se você tiver que executar uma publicação de ativo de fora da pasta de destino CQ para o Dynamic Media Classic.

Esta seção aborda como executar todas essas etapas e lista limitações importantes.

### Como a sincronização entre o Dynamic Media Classic e o Experience Manager Assets funciona {#how-synchronization-between-scene-and-aem-assets-works}

Ao configurar a sincronização do Experience Manager Assets e do Dynamic Media Classic, é importante entender o seguinte:

#### Fazer upload para o Dynamic Media Classic a partir do Experience Manager Assets {#uploading-to-scene-from-aem-assets}

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
   <td>Você só pode ter uma pasta designada por empresa no Experience Manager para uploads do Dynamic Media Classic. É possível criar várias configurações se você precisar ter acesso a mais de uma conta de empresa no Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Estrutura de pastas</td>
   <td>Se você excluir uma pasta sincronizada com ativos, todos os ativos remotos do Dynamic Media Classic serão excluídos, mas a pasta permanecerá.</td>
  </tr>
  <tr>
   <td>Pasta sob demanda</td>
   <td>Os ativos que ficam fora da pasta de destino carregada manualmente no Dynamic Media Classic no WCM são colocados automaticamente em uma pasta sob demanda separada no Dynamic Media Classic. Você configura essa pasta na configuração da nuvem no Experience Manager.</td>
  </tr>
  <tr>
   <td>Mídia mista</td>
   <td>Os conjuntos de mídia mista são exibidos no Experience Manager, embora não sejam compatíveis com o Experience Manager.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>As PDF geradas dos eCatalogs no Dynamic Media Classic são importadas para a pasta de destino CQ.</td>
  </tr>
  <tr>
   <td>Atualização da interface do usuário</td>
   <td>Ao sincronizar o Experience Manager e o Dynamic Media Classic, atualize a interface do usuário para exibir as alterações. </td>
  </tr>
  <tr>
   <td>Miniaturas de vídeo</td>
   <td>Ao fazer upload de um vídeo para o Experience Manager Assets para codificação via Dynamic Media Classic, as miniaturas de vídeo e os vídeos codificados podem levar algum tempo para serem disponibilizados no Experience Manager Assets, dependendo do tempo de processamento do vídeo.</td>
  </tr>
  <tr>
   <td>Subpastas do Target</td>
   <td><p>Se você usar subpastas dentro da pasta de destino, certifique-se de usar nomes exclusivos para cada ativo (independentemente da localização). Além disso, certifique-se de configurar o Dynamic Media Classic (na área Configuração ) para não substituir ativos, independentemente do local.</p> <p>Caso contrário, os ativos com o mesmo nome que são carregados em uma subpasta de destino do Dynamic Media Classic serão carregados, mas o ativo com o mesmo nome na pasta de destino será excluído. </p> </td>
  </tr>
 </tbody>
</table>

### Configurar servidores da Dynamic Media Classic {#configuring-scene-servers}

Se você executar o Experience Manager atrás de um proxy ou tiver configurações de firewall especiais, deverá habilitar explicitamente os hosts das diferentes regiões. Os servidores são gerenciados no conteúdo em `/etc/cloudservices/scene7/endpoints` e podem ser personalizadas, conforme necessário. Selecione um URL e edite para alterar o URL, se necessário. Em versões anteriores do Experience Manager, esses valores eram codificados.

Se você navegar para `/etc/cloudservices/scene7/endpoints.html`, você verá os servidores listados (e poderá editá-los tocando no URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Criar uma configuração de nuvem para o Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Uma configuração de nuvem define o mapeamento entre uma pasta do Dynamic Media Classic e uma pasta do Experience Manager Assets. Ele deve ser configurado para sincronizar o Experience Manager Assets com o Dynamic Media Classic. Consulte Como a sincronização funciona para obter mais informações.

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode levar muito tempo para ser exibida no Experience Manager. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos. Por exemplo, a pasta raiz geralmente tem muitos ativos.
>
>Se quiser testar e direcionar a integração, faça com que a pasta raiz aponte apenas para uma subpasta, em vez da empresa inteira.

>[!NOTE]
>
>É possível ter várias configurações: uma configuração de nuvem representa um usuário em uma empresa do Dynamic Media Classic. Se quiser acessar outras empresas ou usuários da Dynamic Media Classic, crie várias configurações.

**Para criar uma configuração de nuvem para o Dynamic Media Classic:**

1. Selecione o ícone Experience Manager e navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]** para que você possa acessar o Adobe Dynamic Media Classic.

1. Selecionar **[!UICONTROL Configurar agora]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. No **[!UICONTROL Título]** e, opcionalmente, no campo **[!UICONTROL Nome]** , insira as informações apropriadas. Selecione **[!UICONTROL Criar]**.

   >[!NOTE]
   >
   >Ao criar mais configurações, a variável **[!UICONTROL configuração principal]** é exibido.
   >
   >Do **not** altere a configuração pai. Alterar a configuração pai pode interromper a integração.

1. Digite o endereço de email, senha e região da sua conta do Dynamic Media Classic e selecione **[!UICONTROL Conectar-se ao Dynamic Media Classic]**. Você está conectado ao servidor do Dynamic Media Classic e a caixa de diálogo é expandida com mais opções.

1. Insira o **[!UICONTROL Empresa]** nome e **[!UICONTROL Caminho raiz]**. Essas informações são o nome do servidor publicado junto com qualquer caminho que você deseja especificar. Caso não saiba o nome do servidor publicado, no Dynamic Media Classic, acesse **[!UICONTROL Configuração > Configuração do aplicativo]**).

   >[!NOTE]
   >
   >O caminho raiz do Dynamic Media Classic é o Experience Manager de pasta do Dynamic Media Classic. Ele pode ser limitado a uma pasta específica.

   >[!CAUTION]
   >
   >Dependendo do tamanho da pasta Dynamic Media Classic, a importação de uma pasta raiz pode demorar muito. Além disso, os dados do Dynamic Media Classic podem exceder o armazenamento de Experience Manager. Certifique-se de que está importando a pasta correta. Importar muitos dados pode parar o sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Selecionar **[!UICONTROL OK]**. O Experience Manager salva sua configuração.

>[!NOTE]
>
>Se estiver reconectando:
>
>* Ao reconectar-se ao Dynamic Media Classic ao publicar, redefina a senha ao publicar ou reconectar não funciona (não é um problema na instância do autor).
>* Se você modificar valores como sua região, nome da empresa, será necessário reconectar-se ao Dynamic Media Classic. Se as opções de configuração tiverem sido modificadas, mas não tiverem sido salvas, o Experience Manager ainda indicará erroneamente que a configuração é válida. Certifique-se de reconectar.
>


### Ativar o ouvinte do Adobe CQ Dynamic Media Classic Dam {#enabling-the-adobe-cq-scene-dam-listener}

Ative o ouvinte do Adobe CQ Dynamic Media Classic Dam, que é desativado por padrão.

**Para ativar o ouvinte do Adobe CQ Dynamic Media Classic Dam:**

1. Selecione o [!UICONTROL Ferramentas] e navegue até **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No console da Web, navegue até **[!UICONTROL Ouvinte do Adobe CQ Dynamic Media Classic Dam]** e selecione o **[!UICONTROL Ativado]** caixa de seleção.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Selecione **[!UICONTROL Salvar]**.

### Adicionar tempo limite configurável ao fluxo de trabalho de upload do Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Quando uma instância do Experience Manager é configurada para lidar com a codificação de vídeo pelo Dynamic Media Classic, por padrão, há um tempo limite de 35 minutos em qualquer trabalho de upload. Para acomodar trabalhos de codificação de vídeo potencialmente mais longos, é possível definir essa configuração.

1. Navegar para **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Altere o número conforme desejado na **[!UICONTROL Tempo limite do trabalho ativo]** campo. Qualquer número não negativo é aceite com a unidade de medida em segundos. Por padrão, esse número é definido como 2100.

   >[!NOTE]
   >
   >Prática recomendada: A maioria dos ativos é assimilada em no máximo minutos (por exemplo, imagens). Mas em certas instâncias - vídeos maiores, por exemplo - aumentam o valor do tempo limite para 7.200 segundos (duas horas) para acomodar o tempo de processamento longo. Caso contrário, esse trabalho de upload do Dynamic Media Classic será marcado como **[!UICONTROL UploadFailed]** nos metadados JCR (Java™ Content Repository).

1. Selecione **[!UICONTROL Salvar]**.

### Fazer upload automático da Experience Manager Assets {#autouploading-from-aem-assets}

A partir do Experience Manager 6.3.2, o Experience Manager Assets é configurado para que todos os ativos digitais carregados sejam atualizados para o Dynamic Media Classic, se os ativos estiverem em uma pasta de destino CQ.

Quando um ativo é adicionado ao Experience Manager Assets, ele é carregado e publicado automaticamente no Dynamic Media Classic.

>[!NOTE]
>
>O tamanho máximo de arquivo para o upload automático do Experience Manager Assets para o Dynamic Media Classic é de 500 MB.

**Para fazer upload automático do Experience Manager Assets:**

1. Selecione o ícone Experience Manager e navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**.
1. No cabeçalho Dynamic Media , em Configurações disponíveis, selecione **[!UICONTROL dms7 (Dynamic Media)]**).
1. Selecione o **[!UICONTROL Avançado]** selecione a guia **[!UICONTROL Ativar upload automático]** caixa de seleção, em seguida, selecione **[!UICONTROL OK]**. Agora, você deve configurar o fluxo de trabalho do Ativo DAM para incluir o upload no Dynamic Media Classic.

   >[!NOTE]
   >
   >Consulte [Configuração do estado (publicado/não publicado) de ativos enviados para o Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) para obter informações sobre como enviar ativos para o Dynamic Media Classic em um estado não publicado.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Volte para a página de boas-vindas do Experience Manager e selecione **[!UICONTROL Fluxos de trabalho]**. Clique duas vezes no botão **Ativo de atualização DAM** para que seja aberto.
1. No sidekick, navegue até o **[!UICONTROL Fluxo de trabalho]** componentes e selecione **[!UICONTROL Dynamic Media Classic]**. Arrastar **[!UICONTROL Dynamic Media Classic]** para o fluxo de trabalho e selecione **[!UICONTROL Salvar]**. Os ativos adicionados ao Experience Manager Assets na pasta de destino são carregados automaticamente no Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Ao adicionar ativos após a automação, se eles não forem colocados na pasta de destino CQ, eles não serão carregados no Dynamic Media Classic.
   >* O Experience Manager incorpora todos os metadados como XMP antes de carregá-los no Dynamic Media Classic, de modo que todas as propriedades no nó de metadados estejam disponíveis no Dynamic Media Classic como XMP.


### Configurar o estado (publicado/não publicado) dos ativos enviados para o Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Se você estiver enviando ativos do Experience Manager Assets para o Dynamic Media Classic, é possível publicá-los automaticamente (comportamento padrão) ou enviá-los para o Dynamic Media Classic em um estado não publicado.

É possível que você não queira publicar ativos imediatamente no Dynamic Media Classic se quiser testá-los em um ambiente de preparo antes de entrar no ar. Você pode usar o Experience Manager com o ambiente de Teste Seguro da Dynamic Media Classic para enviar ativos diretamente do Assets para o Dynamic Media Classic em um estado não publicado.

Os ativos do Dynamic Media Classic permanecem disponíveis por meio de uma visualização segura. Somente quando os ativos são publicados no Experience Manager, os ativos da Dynamic Media Classic também entram em produção.

Se quiser publicar ativos imediatamente ao enviá-los para o Dynamic Media Classic, não será necessário configurar nenhuma opção. Essa funcionalidade é o comportamento padrão.

No entanto, se você não quiser que ativos enviados para o Dynamic Media Classic sejam publicados automaticamente, esta seção descreve como configurar o Experience Manager e o Dynamic Media Classic para executar essa funcionalidade.

#### Pré-requisitos para enviar ativos para o Dynamic Media Classic não publicados {#prerequisites-to-push-assets-to-scene-unpublished}

Antes de enviar ativos para o Dynamic Media Classic sem publicá-los, você deve configurar o seguinte:

1. [Use o Admin Console para criar um caso de suporte](https://helpx.adobe.com/br/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html). No caso de suporte, solicite a ativação de uma pré-visualização segura para sua conta do Dynamic Media Classic.
1. [Configurar pré-visualização segura para sua conta do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en).

Essas etapas são as mesmas que você seguiria para criar qualquer configuração de teste seguro no Dynamic Media Classic.

>[!NOTE]
>
>Se o seu ambiente de instalação for um sistema operacional UNIX® de 64 bits, consulte [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) em relação a outras opções de configuração, você deve definir.

#### Limitações conhecidas para enviar ativos no estado não publicado  {#known-limitations-for-pushing-assets-in-unpublished-state}

Se você usar esse recurso, observe as seguintes limitações:

* Não há suporte para controle de versão.
* Se um ativo já estiver publicado no Experience Manager e uma versão subsequente for criada, essa nova versão será publicada imediatamente ao vivo para produção. Publicar na ativação só funciona com a publicação inicial de um ativo.

>[!NOTE]
>
>Se você deseja publicar ativos instantaneamente, a prática recomendada é manter **[!UICONTROL Ativar visualização segura]** defina como **[!UICONTROL Imediatamente]** e use o **[!UICONTROL Ativar upload automático]** recurso.

### Definir o estado dos ativos enviados para o Dynamic Media Classic como não publicados {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Se um usuário publicar o ativo no Experience Manager, ele automaticamente acionará o ativo S7 para o ativo de produção/ao vivo (o ativo não está mais em visualização segura/não está mais publicado).

**Para definir o estado dos ativos enviados para o Dynamic Media Classic como não publicados:**

1. Selecione o ícone Experience Manager e navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**.
1. Selecionar **[!UICONTROL Dynamic Media Classic]**.
1. Selecione sua configuração no Dynamic Media Classic.
1. Selecione o **[!UICONTROL Avançado]** guia .
1. No **[!UICONTROL Habilitar Exibição Segura]** , selecione **[!UICONTROL Após a ativação de publicação do AEM]** para enviar ativos para o Dynamic Media Classic sem publicá-los. (Por padrão, esse valor é definido como **[!UICONTROL Imediatamente]**, onde os ativos do Dynamic Media Classic são publicados imediatamente.)

   Consulte [Documentação do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html) para obter mais informações sobre como testar ativos antes de torná-los públicos.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Selecionar **[!UICONTROL OK]**.

Ativar a Visualização segura significa que seus ativos são enviados para o servidor de visualização seguro e não publicados.

Para ver se **[!UICONTROL Visualização segura]** estiver habilitado, navegue até um componente Dynamic Media Classic em uma página no Experience Manager. Selecione **[!UICONTROL Editar]**. O ativo tem o servidor de visualização seguro listado no URL. Após a publicação no Experience Manager, o domínio do servidor na referência de arquivo é atualizado do URL de visualização para o URL de produção.

### Habilitar o Dynamic Media Classic para WCM {#enabling-scene-for-wcm}

A ativação do Dynamic Media Classic para WCM é necessária por dois motivos:

* Ela ativa a lista suspensa de perfis de vídeo universais para criação de página. Sem essa lista, a variável **[!UICONTROL Predefinição de vídeo universal]** O menu suspenso está vazio e não pode ser definido.
* Se um ativo digital não estiver na pasta de destino, você poderá fazer upload do ativo para o Dynamic Media Classic se ativar o Dynamic Media Classic para essa página nas propriedades da página. Em seguida, arraste e solte o ativo em um componente do Dynamic Media Classic. As regras de herança normais se aplicam (o que significa que as páginas secundárias herdam a configuração da página principal).

Ao ativar o Dynamic Media Classic para o WCM, como em outras configurações, as regras de herança se aplicam. Você pode ativar o Dynamic Media Classic para WCM na interface otimizada para toque ou clássica.

#### Ativar o Dynamic Media Classic para WCM na interface otimizada para toque {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. Selecione o ícone Experience Manager e navegue até **[!UICONTROL Sites]**, em seguida, a página raiz do site (não específica do idioma).

1. Na barra de ferramentas, selecione o [!UICONTROL configurações] e selecione **[!UICONTROL Abrir propriedades]**.

1. Selecionar **[!UICONTROL Cloud Services]** e selecione **[!UICONTROL Adicionar configuração]** e selecione **[!UICONTROL Dynamic Media Classic]**.
1. No **[!UICONTROL Adobe Dynamic Media Classic]** , selecione a configuração desejada e selecione **[!UICONTROL OK]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   As predefinições de vídeo dessa configuração do Dynamic Media Classic estão disponíveis para uso no Experience Manager com o componente de vídeo do Dynamic Media Classic nessa página e nas páginas filhas.

#### Ativar o Dynamic Media Classic para WCM na interface do usuário clássica {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. No Experience Manager, selecione **[!UICONTROL Sites]** e navegue até a página raiz do seu site (não específico de idioma).

1. No sidekick, selecione o **[!UICONTROL Página]** e selecione **[!UICONTROL Propriedades da página]**.

1. Selecionar **[!UICONTROL Cloud Services]** > **[!UICONTROL Adicionar serviços]** > **[!UICONTROL Dynamic Media Classic]**.
1. No **[!UICONTROL Adobe Dynamic Media Classic]** , selecione a configuração desejada e selecione **[!UICONTROL OK]**.

   As predefinições de vídeo dessa configuração do Dynamic Media Classic estão disponíveis para uso no Experience Manager com o componente de vídeo do Dynamic Media Classic nessa página e nas páginas filhas.

### Configurar uma configuração padrão {#configuring-a-default-configuration}

Se você tiver várias configurações do Dynamic Media Classic, é possível especificar uma delas como padrão para o navegador de conteúdo do Dynamic Media Classic.

Somente uma configuração Dynamic Media Classic pode ser marcada como padrão em um determinado momento. A configuração padrão são os ativos da empresa exibidos por padrão no Navegador de conteúdo do Dynamic Media Classic.

**Para configurar uma configuração padrão:**

1. Selecione o ícone Experience Manager e navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**.
1. Selecionar **[!UICONTROL Dynamic Media Classic]**.
1. Selecione sua configuração no Dynamic Media Classic.
1. Para abrir a configuração, selecione **[!UICONTROL Editar]**.

1. No **[!UICONTROL Geral]** selecione a guia **[!UICONTROL Configuração padrão]** caixa de seleção para torná-lo a empresa padrão e o caminho raiz que aparece no navegador de conteúdo do Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Se houver apenas uma configuração, selecione a variável **[!UICONTROL Configuração padrão]** a caixa de seleção não tem efeito.

### Configurar a pasta ad-hoc {#configuring-the-ad-hoc-folder}

Você pode configurar a pasta sob demanda para a qual os ativos são carregados no Dynamic Media Classic quando o ativo não está na pasta de destino CQ. Consulte Publicação de ativos fora da pasta de destino CQ.

**Para configurar a pasta Ad-hoc:**

1. Selecione o ícone Experience Manager e navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**.
1. Selecionar **[!UICONTROL Dynamic Media Classic]**.
1. Selecione sua configuração no Dynamic Media Classic.
1. Para abrir a configuração, selecione **[!UICONTROL Editar]**.

1. Selecione o **[!UICONTROL Avançado]** guia . No **[!UICONTROL Pasta ad-hoc]** , é possível modificar o **Ad-hoc** pasta. Por padrão, é a variável **name_of_the_company/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configurar predefinições de vídeo universal {#configuring-universal-presets}

Para configurar predefinições de vídeo universal para o componente de vídeo, consulte [Vídeo](/help/assets/s7-video.md).

## Habilitar o suporte ao parâmetro de trabalho de upload de ativos/Dynamic Media Classic baseado em tipo MIME {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Você pode ativar parâmetros de tarefas de upload configuráveis do Dynamic Media Classic que são acionadas pela sincronização dos ativos do Digital Asset Manager/Dynamic Media Classic.

Especificamente, você configura o formato de arquivo aceito por tipo MIME na área OSGi (iniciativa do Open Service Gateway) do painel Configuração do Console da Web do Experience Manager. Em seguida, você pode personalizar os parâmetros de trabalho de upload individuais que são usados para cada tipo MIME no JCR (Java™ Content Repository).

**Para ativar ativos baseados em tipo MIME:**

1. Selecione o ícone Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No painel Configuração do console da Web do Adobe Experience Manager, no **[!UICONTROL OSGi]** selecione **[!UICONTROL Configuração]**.
1. Na coluna Nome , localize e selecione **[!UICONTROL Serviço do tipo MIME do Adobe CQ Dynamic Media Classic Asset]** para editar a configuração.
1. Na área Mapeamento de tipo MIME, selecione qualquer sinal de mais (+) para adicionar um tipo MIME.

   Consulte [Tipos MIME suportados](/help/assets/assets-formats.md#supported-mime-types).

1. No campo de texto, digite o novo nome do tipo MIME.

   Por exemplo, você digitaria um `<file_extension>=<mime_type>` como em `EPS=application/postscript` OU `PSD=image/vnd.adobe.photoshop`.

1. No canto inferior direito da janela de configuração, selecione **[!UICONTROL Salvar]**.
1. Volte para Experience Manager e, no painel esquerdo, selecione **[!UICONTROL CRXDE Lite]**.
1. Na página CRXDE Lite, no painel esquerdo, navegue até `/etc/cloudservices/scene7/<environment>` (substituto `<environment>` para o nome real).
1. Expandir `<environment>` (substituto `<environment>` para o nome real) para revelar o `mimeTypes` nó .
1. Selecione o mimeType que acabou de adicionar.

   Por exemplo, `mimeTypes > application_postscript` OU `mimeTypes > image_vnd.adobe.photoshop`.

1. No lado direito da página CRXDE Lite, selecione o **[!UICONTROL Propriedades]** guia .
1. Especifique um parâmetro de trabalho de upload do Dynamic Media Classic no **[!UICONTROL jobParam]** campo de valor.

   Por exemplo, `psprocess="rasterize"&psresolution=120` .

   Consulte a [API do sistema de produção de imagens Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) para obter mais parâmetros de trabalho de upload, você pode usar.

   >[!NOTE]
   >
   >Se estiver carregando arquivos PSD e quiser processá-los como modelos com extrações de camada, insira o seguinte na **[!UICONTROL jobParam]** campo de valor:
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >Certifique-se de que o arquivo PSD tenha &quot;camadas&quot;. Se for estritamente uma imagem ou uma imagem com máscara, ela será processada como uma imagem porque não há camadas para processar.

1. No canto superior esquerdo da página do CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

## Solução de problemas de integração do Dynamic Media Classic e do Experience Manager {#troubleshooting-scene-and-aem-integration}

Se tiver problemas para integrar o Experience Manager com o Dynamic Media Classic, consulte os seguintes cenários para soluções.

**Se a publicação de ativos digitais no Dynamic Media Classic falhar:**

* Verifique se o ativo que você está fazendo upload está no **[!UICONTROL Direcionamento CQ]** pasta (especifique essa pasta na configuração da nuvem do Dynamic Media Classic).
* Se não estiver, você deve configurar a configuração de nuvem no **[!UICONTROL Propriedades da página]** para que essa página permita o upload para o **[!UICONTROL Ad hoc do CQ]** pasta.

* Verifique os logs para obter qualquer informação.

**Se as predefinições de vídeo não forem exibidas:**

* Verifique se você configurou a configuração de nuvem dessa página **[!UICONTROL Propriedades da página]**. As predefinições de vídeo estão disponíveis no componente de vídeo do Dynamic Media Classic.

**Se os ativos de vídeo não forem reproduzidos no Experience Manager:**

* Certifique-se de ter usado o componente de vídeo correto. O componente de vídeo do Dynamic Media Classic é diferente do componente básico de Vídeo. Consulte [Componente de vídeo básico versus Componente de vídeo do Dynamic Media Classic](/help/assets/s7-video.md).

**Se os ativos novos ou modificados no Experience Manager não forem carregados automaticamente para o Dynamic Media Classic:**

* Certifique-se de que os ativos estejam na pasta de destino do CQ. Somente os ativos que estão na pasta de destino do CQ são atualizados automaticamente (desde que você tenha configurado o Experience Manager Assets para fazer upload automático dos ativos).
* Certifique-se de ter configurado a configuração do Cloud Services para Ativar o upload automático e que você atualizou e salvou o fluxo de trabalho do Ativo do DAM para incluir o upload do Dynamic Media Classic.
* Ao fazer upload de uma imagem em uma subpasta da pasta de destino do Dynamic Media Classic, certifique-se de fazer o seguinte:

   * Certifique-se de que os nomes de todos os ativos, independentemente da localização, sejam exclusivos. Caso contrário, o ativo na pasta de destino principal será excluído e somente o ativo na subpasta permanecerá.
   * Altere como o Dynamic Media Classic substitui ativos na área Configuração da conta do Dynamic Media Classic. Não defina o Dynamic Media Classic para substituir ativos, independentemente do local, se você usar ativos com o mesmo nome em subpastas.

**Se os ativos ou pastas excluídos não forem sincronizados entre o Dynamic Media Classic e o Experience Manager:**

* Os ativos e pastas excluídos no Experience Manager Assets ainda são exibidos na pasta sincronizada no Dynamic Media Classic. Exclua-os manualmente.

**Se o upload do vídeo falhar:**

* Se o upload de vídeo falhar e você estiver usando o Experience Manager para codificar vídeo por meio da integração com o Dynamic Media Classic, consulte [Adicionar tempo limite configurável ao fluxo de trabalho de upload do Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>A importação de ativos de uma conta de empresa existente do Dynamic Media Classic pode levar muito tempo para ser exibida no Experience Manager. Certifique-se de designar uma pasta no Dynamic Media Classic que não tenha muitos ativos. Por exemplo, a pasta raiz geralmente tem muitos ativos.
>
>Se quiser testar a integração, faça com que a pasta raiz aponte apenas para uma subpasta, em vez da empresa inteira.
