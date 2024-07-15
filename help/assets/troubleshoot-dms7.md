---
title: Solução de problemas do modo Dynamic Media - Scene7
description: Saiba como solucionar problemas de instalação, configuração e problemas gerais no Dynamic Media quando ele está em execução no modo Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Troubleshooting
mini-toc-levels: 3
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 0%

---

# Solução de problemas do modo Dynamic Media - Scene7{#troubleshooting-dynamic-media-scene-mode}

O documento a seguir descreve a solução de problemas do Dynamic Media que está executando o **dynamicmedia_scene7** no modo de execução.

## Instalação e configuração {#setup-and-configuration}

Verifique se o Dynamic Media foi configurado corretamente fazendo o seguinte:

* O comando de inicialização contém o argumento de modo de execução `-r dynamicmedia_scene7`.
* Todos os Cumulative Fix Packs (CFPs) do Adobe Experience Manager 6.4 foram instalados primeiro *antes* de qualquer Pacote de Recursos do Dynamic Media disponível.
* O Feature Pack 18912 opcional está instalado.

  Este pacote de recursos opcional é para suporte a FTP ou se você estiver migrando ativos do Dynamic Media Classic para o Dynamic Media.

* Navegue até a interface de usuário do Cloud Service e confirme se a conta provisionada aparece em **[!UICONTROL Configurações disponíveis]**.
* Verifique se o agente de replicação `Dynamic Media Asset Activation (scene7)` está habilitado.

  Esse agente de replicação é encontrado em Agentes no Autor.

## Geral (Todos os Assets) {#general-all-assets}

Veja a seguir algumas dicas e truques gerais para todos os ativos.

### Propriedades do status de sincronização do ativo {#asset-synchronization-status-properties}

As seguintes propriedades do ativo podem ser revisadas no CRXDE Lite para confirmar a sincronização bem-sucedida do ativo do Experience Manager para o Dynamic Media:

| **Propriedade** | **Exemplo** | **Descrição** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | Indicador geral de que o nó está vinculado ao Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** ou texto de erro | Status do upload do ativo para o Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve ser preenchido para gerar URLs para ativo remoto do Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **sucesso** ou **falha:`<error text>`** | Status de sincronização de conjuntos (conjuntos de rotação, conjuntos de imagem e assim por diante), predefinições de imagem, predefinições do visualizador, atualizações de mapa de imagem para um ativo ou imagens que foram editadas. |

### Log de Sincronização {#synchronization-logging}

Erros e problemas de sincronização registrados em `error.log` (diretório do servidor Experience Manager `/crx-quickstart/logs/`). Há logs suficientes disponíveis para determinar a causa raiz da maioria dos problemas. No entanto, você pode aumentar o log para DEBUG no pacote `com.adobe.cq.dam.ips` por meio do Console Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para coletar mais informações.

### Mover, Copiar, Excluir {#move-copy-delete}

Antes de executar uma operação Mover, Copiar ou Deletar, faça o seguinte:

* Para imagens e vídeos, confirme se um valor `<object_node>/jcr:content/metadata/dam:scene7ID` existe antes de executar as operações de movimentação, cópia ou exclusão.
* Para predefinições de imagens e visualizadores, confirme se um valor `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` existe antes de executar operações de movimentação, cópia ou exclusão.
* Se o valor de metadados acima estiver ausente, você deverá fazer upload novamente dos ativos antes das operações de mover, copiar ou excluir.

### Controle da versão {#version-control}

Ao substituir um ativo existente do Dynamic Media (mesmo nome e local), você pode manter ambos os ativos ou substituir/criar uma versão:

* Manter ambos cria um ativo com um nome exclusivo para o URL do ativo publicado. Por exemplo, `image.jpg` é o ativo original e `image1.jpg` é o ativo recém-carregado.

* A criação de uma versão não é compatível com a entrega no modo Dynamic Media - Scene7. A nova versão substitui o ativo existente na entrega.

## Imagens e conjuntos {#images-and-sets}

Se tiver problemas com imagens e conjuntos, consulte a seguinte orientação de solução de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Como depurar</strong></td>
   <td><strong>Solução</strong></td>
  </tr>
  <tr>
   <td>Não é possível acessar o botão copiar URL/Incorporar na exibição detalhada do ativo</td>
   <td>
    <ol>
     <li><p>Vá para CRX/DE:</p>
      <ul>
       <li>Verifique se a predefinição no JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> foi definida. Esse local se aplica se você atualizou do Experience Manager 6.x para o 6.4 e recusou a migração. Caso contrário, o local é <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verifique se o ativo no JCR tem <code>dam:scene7FileStatus</code><strong> </strong>em Metadados exibidos como <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Atualizar página/navegar para outra página e voltar (o JSP do painel lateral deve ser recompilado)</p> <p>Se isso não funcionar:</p>
    <ul>
     <li>Ativo do Publish.</li>
     <li>Recarregue o ativo e publique-o.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>O seletor de ativos no editor de conjuntos ficou preso no carregamento permanente</td>
   <td><p>Problema conhecido a ser corrigido no 6.4</p> </td>
   <td><p>Feche o seletor e abra-o novamente.</p> </td>
  </tr>
  <tr>
   <td>O botão <strong>Selecionar</strong> não fica ativo depois de selecionar um ativo como parte da edição de um conjunto</td>
   <td><p> </p> <p>Problema conhecido a ser corrigido no 6.4</p> <p> </p> </td>
   <td><p>Selecione primeiro em outra pasta no Seletor de ativos e volte para selecionar o ativo.</p> </td>
  </tr>
  <tr>
   <td>O ponto de acesso do carrossel se move após alternar entre os slides</td>
   <td><p>Verifique se todos os slides são do mesmo tamanho.</p> </td>
   <td><p>Use somente imagens com o mesmo tamanho para o carrossel.</p> </td>
  </tr>
  <tr>
   <td>A imagem não é visualizada com o visualizador do Dynamic Media</td>
   <td><p>Verifique se o ativo contém <code>dam:scene7File</code> nas propriedades de Metadados (CRXDE Lite)</p> </td>
   <td><p>Verifique se o processamento de todos os ativos foi concluído.</p> </td>
  </tr>
  <tr>
   <td>O ativo carregado não é exibido no seletor de ativos</td>
   <td><p>Verificar se o ativo tem a propriedade <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verifique se o processamento de todos os ativos foi concluído.</p> </td>
  </tr>
  <tr>
   <td>O banner na exibição de cartão mostra <strong>Novo</strong> quando o ativo não iniciou o processamento</td>
   <td>Verificar ativo <code>jcr:content</code> &gt; <code>dam:assetState</code> = se <code>unprocessed</code> ele não foi selecionado pelo fluxo de trabalho.</td>
   <td>Aguarde até que o ativo seja selecionado pelo fluxo de trabalho.</td>
  </tr>
  <tr>
   <td>As imagens ou conjuntos não exibem o URL do visualizador ou o código de inserção</td>
   <td>Verifique se a predefinição do visualizador foi publicada.</td>
   <td><p>Acesse <strong>Ferramentas</strong> &gt; <strong>Assets</strong> &gt; <strong>Predefinições do Visualizador</strong> e publique a predefinição do visualizador.</p> </td>
  </tr>
 </tbody>
</table>

## Vídeo {#video}

Se tiver problemas com o vídeo, consulte a seguinte orientação para solução de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Como depurar</strong></td>
   <td><strong>Solução</strong></td>
  </tr>
  <tr>
   <td>O vídeo não pode ser visualizado</td>
   <td>
    <ul>
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela (se um formato de arquivo não for compatível). Se não for compatível, somente uma imagem será exibida.</li>
     <li>O perfil de vídeo deve conter mais de uma predefinição de codificação para gerar um conjunto AVS (codificações únicas são tratadas como conteúdo de vídeo para arquivos MP4; para arquivos não compatíveis, são tratadas da mesma forma que não processadas).</li>
     <li>Verifique se o processamento do vídeo foi concluído confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> nos metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribuir um perfil de vídeo à pasta.</li>
     <li>Editar perfil de vídeo para incluir mais de uma predefinição de codificação.</li>
     <li>Aguarde até que o vídeo termine o processamento.</li>
     <li>Ao recarregar o vídeo, verifique se o fluxo de trabalho Codificação de Vídeo do Dynamic Media não está em execução.<br /> </li>
     <li>Recarregue o vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>O vídeo não está codificado</td>
   <td>
    <ul>
     <li>Verifique se o modo de execução é <code>dynamicmedia_scene7</code>.</li>
     <li>Verifique se o serviço em nuvem Dynamic Media está configurado.</li>
     <li>Verifique se um perfil de vídeo está associado à pasta de upload.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Verifique a instância do Experience Manager com <code>-r dynamicmedia_scene7</code></li>
     <li>Verifique se a configuração do Dynamic Media em Cloud Service está definida corretamente.</li>
     <li>Verifique se a pasta tem um perfil de vídeo. Além disso, verifique o perfil do vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>O processamento de vídeo demora muito</td>
   <td><p>Para determinar se a codificação de vídeo ainda está em andamento ou se entrou em um estado de falha:</p>
    <ul>
     <li>Verifique o status do vídeo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Monitore o vídeo a partir das guias do console de fluxo de trabalho <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Instâncias, Arquivamento, Falhas.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Representação de vídeo ausente</td>
   <td><p>Quando o vídeo for carregado, mas não houver representações codificadas:</p>
    <ul>
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela.</li>
     <li>Verifique se o processamento do vídeo foi concluído confirmando <code>dam:scene7FileAvs</code> nos metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribuir um perfil de vídeo à pasta.</li>
     <li>Aguarde a conclusão do processamento do vídeo.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Espectadores {#viewers}

Se tiver problemas com visualizadores, consulte as seguintes orientações para solução de problemas.

### Problema: as predefinições do visualizador não são publicadas {#viewers-not-published}

**Como depurar**

1. Vá para a página de diagnóstico do gerenciador de amostra: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. Observe os valores calculados. Ao operar corretamente, você verá o seguinte: `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >Pode levar cerca de 10 minutos após a definição das configurações de nuvem do Dynamic Media para que os ativos do visualizador sejam sincronizados.

1. Se os ativos desativados permanecerem, selecione um dos botões **Listar todos os Assets** desativados para ver os detalhes.

**Solução**

1. Navegar até a lista de predefinições do visualizador nas ferramentas administrativas: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Selecione todas as predefinições do visualizador e selecione **Publish**.
1. Volte para o gerenciador de amostra e observe que a contagem de ativos desativados agora é zero.

### Problema: o trabalho artístico predefinido do visualizador retorna 404 da Pré-visualização nos detalhes do ativo ou Copiar URL/Código incorporado {#viewer-preset-404}

**Como depurar**

No CRXDE Lite, faça o seguinte:

1. Navegue até a pasta `<sync-folder>/_CSS/_OOTB` dentro da pasta de sincronização do Dynamic Media (por exemplo, `/content/dam/_CSS/_OOTB`).
1. Localize o nó de metadados do ativo problemático (por exemplo, `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Verifique a presença de `dam:scene7*` propriedades. Se o ativo foi sincronizado e publicado com êxito, você vê que o conjunto `dam:scene7FileStatus` é para **PublishComplete**.
1. Tente solicitar o trabalho artístico diretamente da Dynamic Media, concatenando os valores das seguintes propriedades e literais de string:

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Exemplo: `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Solução**

Se o trabalho artístico de ativos de amostra ou predefinição do visualizador não tiver sido sincronizado ou publicado, reinicie todo o processo de cópia/sincronização:

1. Navegue até CRXDE Lite.
1. Excluir `<sync-folder>/_CSS/_OOTB`.
1. Navegue até o CRX Package Manager: `https://localhost:4502/crx/packmgr/`.
1. Procure o pacote do visualizador na lista; ele começa com `cq-dam-scene7-viewers-content`.
1. Selecione **Reinstalar**.
1. Em Cloud Service, navegue até a página Configuração do Dynamic Media e abra a caixa de diálogo de configuração da sua configuração Dynamic Media - S7.
1. Não fazer alterações, selecione **Salvar**.
Essa ação de salvar aciona a lógica novamente para criar e sincronizar os ativos de amostra, o CSS de predefinição do visualizador e o trabalho artístico.

### Problema: a Visualização da imagem não está sendo carregada na criação das predefinições do visualizador {#image-preview-not-loading}

**Solução**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No painel à esquerda, navegue até a pasta de conteúdo de amostra no seguinte local:

   `/content/dam/_DMSAMPLE`

1. Exclua a pasta `_DMSAMPLE`.
1. No painel à esquerda, navegue até a pasta de predefinições no seguinte local:

   `/conf/global/settings/dam/dm/presets/viewer`

1. Exclua a pasta `viewer`.
1. Próximo ao canto superior esquerdo da página de CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.
1. No canto superior esquerdo da página de CRXDE Lite, selecione o ícone **Voltar à página inicial**.
1. Recrie uma Configuração do Dynamic Media [no Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
