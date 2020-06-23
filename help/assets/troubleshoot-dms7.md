---
title: Solução de problemas do Dynamic Media - modo Scene7
description: Solução de problemas do Dynamic Media no modo de execução Scene7.
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 1%

---


# Solução de problemas do Dynamic Media - modo Scene7{#troubleshooting-dynamic-media-scene-mode}

O documento a seguir descreve a solução de problemas para o Dynamic Media que está executando o modo de execução **dynamicmedia_sceno7** .

## Configuração e configuração {#setup-and-configuration}

Certifique-se de que a Dynamic Media tenha sido configurada corretamente, fazendo o seguinte:

* O comando Start up contém o argumento `-r dynamicmedia_scene7` runmode.
* Todos os CFPs (Pacotes de correção cumulativos) AEM 6.4 foram instalados primeiro *antes* de qualquer Pacote de recursos Dynamic Media disponível.
* O Feature Pack 18912 opcional está instalado.

   Este pacote de recursos opcional é para suporte a FTP ou se você estiver migrando ativos do Dynamic Media Classic (Scene7) para o Dynamic Media.

* Navegue até a interface do usuário do Cloud Service e confirme se a conta provisionada aparece em Configurações **[!UICONTROL disponíveis.]**
* Certifique-se de que o agente de `Dynamic Media Asset Activation (scene7)` replicação esteja ativado.

   Esse agente de replicação é encontrado em Agentes no Autor.

## Geral (Todos os ativos) {#general-all-assets}

Veja a seguir algumas dicas gerais e truques para todos os ativos.

### Propriedades do status da sincronização de ativos {#asset-synchronization-status-properties}

As seguintes propriedades de ativos podem ser revisadas no CRXDE Lite para confirmar a sincronização bem-sucedida do ativo do AEM para a Dynamic Media:

| **Propriedade** | **Exemplo** | **Descrição** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicador geral de que o nó está vinculado ao Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublicarConcluído** ou texto de erro | Status do upload do ativo para a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve ser preenchido para gerar URLs para um ativo remoto do Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **sucesso** ou **falha:`<error text>`** | Status de sincronização de conjuntos (conjuntos de rotação, conjuntos de imagens etc.), predefinições de imagens, predefinições do visualizador, atualizações do mapa de imagens para um ativo ou imagens que foram editadas. |

### Registro de sincronização {#synchronization-logging}

Erros e problemas de sincronização são registrados no logon `error.log` (diretório do servidor AEM `/crx-quickstart/logs/`). O registro em log é suficiente para determinar a causa raiz da maioria dos problemas, no entanto, você pode aumentar o registro em log para DEBUG no `com.adobe.cq.dam.ips` pacote por meio do Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para coletar mais informações.

### Mover, Copiar, Excluir {#move-copy-delete}

Antes de executar uma operação Mover, Copiar ou Excluir, faça o seguinte:

* Para imagens e vídeos, confirme se existe um `<object_node>/jcr:content/metadata/dam:scene7ID` valor antes de executar operações de mover, copiar ou excluir.
* Para predefinições de imagem e visualizador, confirme se existe um `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` valor antes de executar operações de movimentação, cópia ou exclusão.
* Se o valor dos metadados acima estiver ausente, será necessário fazer upload dos ativos novamente antes de mover, copiar ou excluir operações.

### Controle da versão {#version-control}

Ao substituir um ativo Dynamic Media existente (mesmo nome e local), você tem a opção de manter ambos os ativos ou substituir/criar uma versão:

* Manter ambos criará um novo ativo com um nome exclusivo para o URL do ativo publicado. Por exemplo, `image.jpg` é o ativo original e `image1.jpg` é o ativo carregado recentemente.

* Não há suporte para a criação de uma versão no Dynamic Media - delivery de modo Scene7. A nova versão substituirá o ativo existente no delivery.

## Imagens e conjuntos {#images-and-sets}

Se tiver problemas com imagens e conjuntos, consulte as seguintes orientações para solução de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Como depurar</strong></td>
   <td><strong>Solução</strong></td>
  </tr>
  <tr>
   <td>Não é possível acessar o URL de cópia/botão Incorporar na visualização de detalhes do ativo</td>
   <td>
    <ol>
     <li><p>Ir para CRX/DE:</p>
      <ul>
       <li>Verifique se a predefinição no JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> está definida. Observe que esse local se aplica se você tiver atualizado do AEM 6.x para o 6.4 e opt out da migração. Caso contrário, a localização é <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verifique se o ativo no JCR tem <code>dam:scene7FileStatus</code><strong> em Metadados </strong>exibido como <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Atualizar página/navegar para outra página e voltar (o JSP do painel lateral precisa ser recompilado)</p> <p>Se isso não funcionar:</p>
    <ul>
     <li>Publicar ativo.</li>
     <li>Carregue novamente o ativo e publique-o.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Seletor de ativos no editor definido travado no carregamento perpétuo</td>
   <td><p>Problema conhecido a ser corrigido na seção 6.4</p> </td>
   <td><p>Feche o seletor e abra-o novamente.</p> </td>
  </tr>
  <tr>
   <td><strong>O botão Selecionar</strong> não está ativo depois de selecionar um ativo como parte da edição de um conjunto</td>
   <td><p> </p> <p>Problema conhecido a ser corrigido na seção 6.4</p> <p> </p> </td>
   <td><p>Clique em outra pasta no Seletor de ativos primeiro e volte para selecionar o ativo.</p> </td>
  </tr>
  <tr>
   <td>O ponto de conexão do carrossel se move após alternar entre os slides</td>
   <td><p>Verifique se todos os slides têm o mesmo tamanho.</p> </td>
   <td><p>Use apenas imagens com o mesmo tamanho para o carrossel.</p> </td>
  </tr>
  <tr>
   <td>A imagem não é pré-visualização com o visualizador do Dynamic Media</td>
   <td><p>Verifique se o ativo contém <code>dam:scene7File</code> as propriedades de Metadados (CRXDE Lite)</p> </td>
   <td><p>Verifique se todos os ativos concluíram o processamento.</p> </td>
  </tr>
  <tr>
   <td>O ativo carregado não aparece no seletor de ativos</td>
   <td><p>Verificar ativo tem propriedade <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verifique se todos os ativos concluíram o processamento.</p> </td>
  </tr>
  <tr>
   <td>Banner na visualização do cartão mostra <strong>Novo</strong> quando o ativo não começou a processar</td>
   <td>Marque o ativo <code>jcr:content</code> &gt; <code>dam:assetState</code> = se <code>unprocessed</code> ele não foi selecionado pelo fluxo de trabalho.</td>
   <td>Aguarde até que o ativo seja selecionado pelo fluxo de trabalho.</td>
  </tr>
  <tr>
   <td>As imagens ou conjuntos não exibem o URL do visualizador ou o código incorporado</td>
   <td>Verifique se a predefinição do visualizador foi publicada.</td>
   <td><p>Acesse <strong>Ferramentas</strong> &gt; <strong>Ativos</strong> &gt; Predefinições <strong>do</strong> visualizador e publique a predefinição do visualizador.</p> </td>
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
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela (se não houver suporte para o formato de arquivo). Se não houver suporte, somente uma imagem será exibida.</li>
     <li>O perfil de vídeo deve conter mais de uma predefinição de codificação para gerar um conjunto AVS (as codificações únicas são tratadas como conteúdo de vídeo para arquivos MP4; para arquivos não suportados, tratados da mesma forma que os não processados).</li>
     <li>Verifique se o processamento do vídeo foi concluído, confirmando <code>dam:scene7FileAvs</code> a presença <code>dam:scene7File</code> nos metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribua um perfil de vídeo à pasta.</li>
     <li>Edite o perfil de vídeo para incluir mais de uma predefinição de codificação.</li>
     <li>Aguarde o vídeo terminar de processar.</li>
     <li>Se você recarregar o vídeo, verifique se o fluxo de trabalho Codificar vídeo da Dynamic Media não está em execução.<br /> </li>
     <li>Carregue novamente o vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>O vídeo não é codificado</td>
   <td>
    <ul>
     <li>Verifique se o modo de execução está <code>dynamicmedia_scene7</code>.</li>
     <li>Verifique se o serviço de nuvem da Dynamic Media está configurado.</li>
     <li>Verifique se um perfil de vídeo está associado à pasta de upload.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Verifique sua instância do AEM com <code>-r dynamicmedia_scene7</code></li>
     <li>Verifique se a Configuração Dynamic Media em Cloud Service está configurada corretamente.</li>
     <li>Verifique se a pasta tem um perfil de vídeo. Verifique também o perfil de vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>O processamento de vídeo leva muito tempo</td>
   <td><p>Para determinar se a codificação de vídeo ainda está em andamento ou se entrou em um estado de falha:</p>
    <ul>
     <li>Verifique o status do vídeo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Monitore o vídeo no console de fluxo de trabalho <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; guias Instâncias, Arquivo, Falhas.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Execução de vídeo ausente</td>
   <td><p>Quando o vídeo é carregado, mas não há renderizações codificadas:</p>
    <ul>
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela.</li>
     <li>Verifique se o processamento do vídeo foi concluído ao confirmar <code>dam:scene7FileAvs</code> nos metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribua um perfil de vídeo à pasta.</li>
     <li>Aguarde o vídeo terminar de processar.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Espectadores {#viewers}

Se tiver problemas com os visualizadores, consulte as seguintes orientações para solução de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Como depurar</strong></td>
   <td><strong>Solução</strong></td>
  </tr>
  <tr>
   <td>As predefinições do visualizador não são publicadas</td>
   <td><p>Vá para a página de diagnóstico do gerenciador de amostras: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Observe os valores calculados. Ao operar corretamente, você deve ver:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Observação</strong>: Pode levar cerca de 10 minutos após a configuração das configurações de nuvem do Dynamic Media para que os ativos do visualizador sejam sincronizados.</p> <p>Se os ativos não ativados permanecerem, clique em um dos botões <strong>Lista de todos os ativos</strong> não ativados para ver os detalhes.</p> </td>
   <td>
    <ol>
     <li>Navegue até a lista predefinida do visualizador nas ferramentas administrativas: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Selecione todas as predefinições do visualizador e clique em <strong>Publicar</strong>.</li>
     <li>Navegue de volta para o gerenciador de amostras e observe que a contagem de ativos não ativados agora é zero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>A arte-final predefinida do visualizador retorna 404 da pré-visualização nos detalhes do ativo ou copia o URL/código incorporado</td>
   <td><p>No CRXDE Lite, faça o seguinte:</p>
    <ol>
     <li>Navegue até a <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> pasta dentro da pasta de sincronização do Dynamic Media (por exemplo, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Encontre o nó de metadados do ativo problemático (por exemplo, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Verifique a presença das <code>dam:scene7*</code> propriedades. Se o ativo foi sincronizado e publicado com êxito, você verá que o <code>dam:scene7FileStatus</code> conjunto é <strong>PublicarConcluído</strong>.</li>
     <li>Tente solicitar a arte-final diretamente da Dynamic Media concatenando os valores das seguintes propriedades e literais de string
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Exemplo: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Se os ativos de amostra ou a arte-final predefinida do visualizador não foram sincronizados ou publicados, reinicie todo o processo de cópia/sincronização:</p>
    <ol>
     <li>Navegue até CRXDE Lite.
      <ul>
       <li>Exclua <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>Navegue até o gerenciador de pacote CRX: <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>Pesquisar o pacote do visualizador na lista (ele start com <code>cq-dam-scene7-viewers-content</code>)</li>
       <li>Clique em <strong>Reinstalar</strong>.</li>
      </ol> </li>
     <li>Em Cloud Service, navegue até a página Configuração do Dynamic Media e abra a caixa de diálogo de configuração para sua configuração Dynamic Media - S7.
      <ul>
       <li>Não faça alterações, clique em <strong>Salvar</strong>. Isso aciona a lógica novamente para criar e sincronizar os ativos de amostra, o CSS predefinido do visualizador e a arte-final.<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

