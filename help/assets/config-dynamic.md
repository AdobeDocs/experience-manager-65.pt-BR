---
title: Configurar o Dynamic Media - Modo híbrido
description: Saiba como configurar o Dynamic Media - Modo híbrido.
mini-toc-levels: 3
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '7792'
ht-degree: 2%

---

# Configurar o Dynamic Media - Modo híbrido {#configuring-dynamic-media-hybrid-mode}

O Dynamic Media-Hybrid deve ser ativado e configurado para uso. Dependendo do seu caso de uso, a Dynamic Media tem vários [configurações suportadas](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Se você pretende configurar e executar o Dynamic Media no modo de execução Scene7, consulte [Configurar o Dynamic Media - Modo Scene7](/help/assets/config-dms7.md).
>
>Se você pretende configurar e executar o Dynamic Media no modo de execução híbrido, siga as instruções nesta página.

Saiba mais sobre como trabalhar com a [vídeo](/help/assets/video.md) no Dynamic Media.

>[!NOTE]
>
>Se você usar o Adobe Experience Manager configurado para ambientes diferentes, como um para desenvolvimento, armazenamento temporário e produção ao vivo, configure os Dynamic Media Cloud Services para cada ambiente.

>[!NOTE]
>
>Se tiver problemas com a configuração do Dynamic Media, procure os arquivos de log específicos do Dynamic Media. Esses arquivos são instalados automaticamente quando você ativa o Dynamic Media:
>
>* `s7access.log`
>* `ImageServing.log`
>
>Eles estão documentados em [Monitore e mantenha sua instância de Experience Manager](/help/sites-deploying/monitoring-and-maintaining.md).

A publicação e o delivery híbridos são um recurso principal da adição do Dynamic Media ao Adobe Experience Manager. A publicação híbrida permite fornecer ativos do Dynamic Media, como imagens, conjuntos e vídeo, a partir da nuvem, em vez dos nós de publicação do Experience Manager.

Outros conteúdos, como visualizadores do Dynamic Media, páginas do Site e conteúdo estático, continuam a ser veiculados a partir dos nós de publicação do Experience Manager.

Se você for um cliente do Dynamic Media, será necessário usar o delivery híbrido como o mecanismo de delivery para todo o conteúdo do Dynamic Media.

## Arquitetura de publicação híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## Arquitetura de publicação híbrida para imagens {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## Configurações compatíveis do Dynamic Media {#supported-dynamic-media-configurations}

As tarefas de configuração que seguem fazem referência aos seguintes termos:

| **Termo** | **Dynamic Media ativado** | **Descrição** |
|---|---|---|
| Nó Autor do Experience Manager | Marca de seleção branca em um círculo verde | O nó de criação que você implantou no local ou pelo Managed Services. |
| Nó de publicação do Experience Manager | &quot;X&quot; branco em um quadrado vermelho. | O nó de publicação implantado no local ou pelo Managed Services. |
| Nó de publicação do serviço de imagem | Marca de seleção branca em um círculo verde. | O nó de publicação executado nos data centers gerenciados pelo Adobe. Refere-se ao URL do serviço de imagem. |

Você pode optar por implementar o Dynamic Media somente para geração de imagens, somente para vídeo ou para geração de imagens e vídeo. Para determinar as etapas para configurar o Dynamic Media para seu cenário específico, consulte a tabela a seguir.

<table>
 <tbody>
  <tr>
   <td><strong>Cenário</strong></td>
   <td ><strong>Como funciona</strong></td>
   <td><strong>Etapas de configuração</strong></td>
  </tr>
  <tr>
   <td>Fornecer SOMENTE imagens na produção</td>
   <td>As imagens são fornecidas por meio de servidores em data centers globais da Adobe e, em seguida, armazenadas em cache por uma CDN para proporcionar desempenho escalável e alcance global.</td>
   <td>
    <ol>
     <li>No Experience Manager <strong>autor</strong> nó, <a href="#enabling-dynamic-media">habilitar o Dynamic Media</a>.</li>
     <li>Configurar a geração de imagens no <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services</a>.</li>
     <li><a href="#configuring-image-replication">Configurar replicação de imagem</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configurações do catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Usar filtros de ativos padrão para replicação</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Definir configurações do servidor de imagem do Dynamic Media</a>.</li>
     <li><a href="#delivering-assets">Entregar ativos</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Fornecer SOMENTE imagens em pré-produção (Dev, QE, Stage e assim por diante).</td>
   <td>As imagens são entregues por meio do nó Experience Manager publish . Nesse cenário, como o tráfego é mínimo, não há necessidade de fornecer imagens ao data center do Adobe. E permite uma pré-visualização segura do conteúdo antes do lançamento da produção.</td>
   <td>
    <ol>
     <li>No Experience Manager <strong>autor</strong> nó, <a href="#enabling-dynamic-media">habilitar o Dynamic Media</a>.</li>
     <li>No Experience Manager <strong>publicar</strong> nó, <a href="#enabling-dynamic-media">habilitar o Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li>Configurar <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">filtro de ativos para imagens que não são de produção</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Defina as configurações do Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Entregar ativos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Fornecer SOMENTE vídeo em qualquer ambiente (Produção, Desenvolvimento, QE, Preparo e assim por diante)</td>
   <td>Os vídeos são fornecidos e armazenados em cache por uma CDN para proporcionar desempenho escalável e alcance global. A imagem do pôster de vídeo (miniatura do vídeo que aparece antes do início da reprodução) é entregue pela instância de publicação do Experience Manager.</td>
   <td>
    <ol>
     <li>No Experience Manager <strong>autor</strong> nó, <a href="#enabling-dynamic-media">habilitar o Dynamic Media</a>.</li>
     <li>No Experience Manager <strong>publicar</strong> nó, <a href="#enabling-dynamic-media">habilitar o Dynamic Media</a> (a instância de publicação fornece a imagem de pôster de vídeo e fornece metadados para a reprodução de vídeo).</li>
     <li>Configurar vídeo em <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services.</a></li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li>Configurar <a href="#setting-up-asset-filters-for-video-only-deployments">filtro de ativos somente para vídeo</a>.</li>
     <li><a href="#delivering-assets">Entregar ativos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Fornecer imagens e vídeo em produção</td>
   <td><p>Os vídeos são fornecidos e armazenados em cache por uma CDN para proporcionar desempenho escalável e alcance global. Imagens e imagens de pôster de vídeo são entregues por meio de servidores em data centers mundiais da Adobe e armazenadas em cache por um CDN para proporcionar desempenho escalável e alcance global.</p> <p>Consulte as seções anteriores para configurar a imagem ou o vídeo na pré-produção. </p> </td>
   <td>
    <ol>
     <li>No Experience Manager <strong>autor</strong> nó, <a href="#enabling-dynamic-media">habilitar o Dynamic Media</a>.</li>
     <li>Configurar vídeo em <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services.</a></li>
     <li>Configurar a geração de imagens no <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services.</a></li>
     <li><a href="#configuring-image-replication">Configurar replicação de imagem</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configurações do catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Use filtros de ativos padrão para replicação.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Defina as configurações do Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Entregar ativos.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Ativar o Dynamic Media {#enabling-dynamic-media}

[As mídias dinâmicas são desativadas por padrão. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Para aproveitar os recursos do Dynamic Media, você deve ativar o Dynamic Media usando o `dynamicmedia` modo de execução como você faria, por exemplo, `publish` modo de execução. Antes de habilitar, verifique se [requisitos técnicos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>Habilitar o Dynamic Media por meio do modo de execução substitui a funcionalidade no Experience Manager 6.1 e Experience Manager 6.0, onde você habilitou o Dynamic Media ao definir a variável `dynamicMediaEnabled` sinalizador para **[!UICONTROL true]**. Esse sinalizador não tem funcionalidade no Experience Manager 6.2 e posterior. Além disso, não é necessário reiniciar o início rápido para ativar o Dynamic Media.

Ao ativar o Dynamic Media, os recursos do Dynamic Media estão disponíveis na interface do usuário e cada ativo de imagem carregado recebe uma *cqdam.pyramid.tiff* representação usada para entrega rápida de representações dinâmicas de imagens. Esses PTIFF apresentam vantagens significativas, como as seguintes:

* A capacidade de gerenciar apenas uma única imagem de fonte primária e gerar representações infinitas de forma instantânea sem qualquer armazenamento adicional.
* A capacidade de usar a visualização interativa, como zoom, panorâmica e rotação.

Se quiser usar o Dynamic Media Classic no Experience Manager, não ative o Dynamic Media, a menos que esteja usando um [cenário específico](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). O Dynamic Media é desativado a menos que você ative o Dynamic Media por meio do modo de execução.

Para habilitar o Dynamic Media, você deve habilitar o modo de execução do Dynamic Media a partir da linha de comando ou do nome do arquivo de início rápido.

**Para ativar o Dynamic Media:**

1. Na linha de comando, ao iniciar o início rápido, faça o seguinte:

   * Adicionar `-r dynamicmedia` ao final da linha de comando ao iniciar o arquivo jar.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   Se você estiver publicando no s7delivery, também deverá incluir os seguintes argumentos trustStore:

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. Solicitação `https://localhost:4502/is/image` e verifique se o Servidor de imagem está em execução.

   >[!NOTE]
   >
   >Para solucionar problemas com o Dynamic Media, consulte os seguintes logs na `crx-quickstart/logs/` diretório:
   >
   >* ImageServer-&lt;portid>-&lt;yyyy>&lt;mm>&lt;dd>.log - O log ImageServer fornece estatísticas e informações analíticas usadas para analisar o comportamento do processo interno do ImageServer.

   Exemplo de um nome de arquivo de log do Servidor de Imagens: `ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - O log s7access registra cada solicitação feita ao Dynamic Media por meio de `/is/image` e `/is/content`.

   Esses logs são usados somente quando o Dynamic Media está ativado. Eles não estão incluídos na variável **Download completo** pacote gerado pelo `system/console/status-Bundlelist` página; ao chamar o Suporte ao cliente em caso de problema com a Dynamic Media, anexe esses dois logs ao problema.

### Se você instalou o Experience Manager para uma porta ou caminho de contexto diferente... {#if-you-installed-aem-to-a-different-port-or-context-path}

Se você estiver implantando o [Experience Manager para um servidor de aplicativos](/help/sites-deploying/application-server-install.md) e tiver o Dynamic Media ativado, você deve configurar a variável **autodomínio** no Externalizador. Caso contrário, a geração de miniaturas de ativos não funcionará corretamente para os ativos da Dynamic Media.

Além disso, se você executar o início rápido em uma porta ou um caminho de contexto diferente, também precisará alterar a variável **autodomínio**.

Quando o Dynamic Media é ativado, as representações de miniatura estáticas para ativos de imagem são geradas usando o Dynamic Media. Para que a geração de miniaturas funcione corretamente para o Dynamic Media, o Experience Manager deve executar uma solicitação de URL para si mesmo e deve saber o número da porta e o caminho do contexto.

No Experience Manager:

* O **autodomínio** no [Externalizador](/help/sites-developing/externalizer.md) é usada para recuperar o número da porta e o caminho do contexto.
* Se não **autodomínio** estiver configurado, o número da porta e o caminho do contexto serão recuperados do serviço HTTP Jetty.

Em uma implantação WAR do QuickStart do Experience Manager, o número da porta e o caminho do contexto não podem ser derivados, portanto, você deve configurar um **autodomínio**. Consulte [Documentação do Externalizador](/help/sites-developing/externalizer.md) sobre como configurar o **autodomínio**.

>[!NOTE]
Em um [Implantação independente do Experience Manager Quickstart](/help/sites-deploying/deploy.md), a **autodomínio** geralmente não precisa ser configurado, pois o número da porta e o caminho do contexto podem ser configurados automaticamente. No entanto, se todas as interfaces de rede estiverem desativadas, você deverá configurar a variável **autodomínio**.

## Desativar o Dynamic Media  {#disabling-dynamic-media}

O Dynamic Media não está habilitado por padrão. No entanto, se você ativou o Dynamic Media anteriormente, é possível desativá-lo posteriormente.

Para desativar o Dynamic Media depois de ativá-lo, remova a variável `-r dynamicmedia` sinalizador de modo de execução.

**Para desativar o Dynamic Media:**

1. Na linha de comando, ao iniciar o início rápido, você pode fazer o seguinte:

   * Não adicionar `-r dynamicmedia` para a linha de comando ao iniciar o arquivo jar.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Solicitação `https://localhost:4502/is/image`. Você receberá uma mensagem informando que o Dynamic Media está desativado.

   >[!NOTE]
   Depois que o modo de execução Dynamic Media é desativado, a etapa do fluxo de trabalho que gera a variável `cqdam.pyramid.tiff` a representação é ignorada automaticamente. Também desativa o suporte de representação dinâmica e outros recursos do Dynamic Media.
   Observe também que, quando o modo de execução Dynamic Media é desativado após a configuração do servidor Experience Manager, todos os ativos que foram carregados nesse modo de execução agora são inválidos.

## (Opcional) Migrar predefinições e configurações do Dynamic Media de 6.3 para 6.5 Zero Down time {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Se você estiver atualizando o Experience Manager - Dynamic Media de 6.3 para 6.5 (que agora inclui a capacidade de implantações de tempo de inatividade zero), deverá executar o seguinte comando curl. O comando migra todas as suas predefinições e configurações do de `/etc` para `/conf` em CRXDE Lite.

>[!NOTE]
Se você executar a instância do Experience Manager no modo de compatibilidade, ou seja, você tem o pacote de compatibilidade instalado, não é necessário executar esses comandos.

Para todas as atualizações, com ou sem o pacote de compatibilidade, você pode copiar as predefinições padrão e prontas para uso do visualizador que vieram originalmente com o Dynamic Media executando o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar qualquer predefinição e configuração do visualizador personalizado do `/etc` para `/conf`, execute o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Configurar replicação de imagem {#configuring-image-replication}

A entrega de imagens da Dynamic Media funciona através da publicação de ativos de imagem, incluindo miniaturas de vídeo, desde a criação do Experience Manager até o serviço de replicação Adobe on Demand (o URL do serviço de replicação). Os ativos são então entregues por meio do serviço de entrega de imagem sob demanda (o URL do Serviço de Imagem).

Faça o seguinte:

1. [Configurar autenticação](#setting-up-authentication).
1. [Configurar o agente de replicação](#configuring-the-replication-agent).

O Agente de replicação publica ativos do Dynamic Media, como imagens, metadados de vídeo e configurações para o Serviço de imagem hospedado no Adobe. O Agente de Replicação não está habilitado por padrão.

Após configurar o agente de replicação, você deve [validar e testar se foi configurado com êxito](#validating-the-replication-agent-for-dynamic-media). Esta seção descreve esses procedimentos.

>[!NOTE]
O limite de memória padrão para a criação de PTIFF é de 3 GB em todos os workflows. Por exemplo, você pode processar uma imagem que requer 3 GB de memória enquanto outros fluxos de trabalho são pausados, ou pode processar 10 imagens em paralelo que exigem 300 MB de memória cada.
O limite de memória é configurável e se encaixa na disponibilidade de recursos do sistema e no tipo de conteúdo de imagem que está sendo processado. Se você tiver muitos ativos grandes e tiver memória suficiente no sistema, é possível aumentar esse limite para garantir que as imagens sejam processadas em paralelo.
Uma imagem que requer mais do que o limite máximo de memória é rejeitada.
Para alterar o limite de memória para a criação de PTIFF, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** > **[!UICONTROL Adobe CQ Scene7 PTiffManager]** e altere a **[!UICONTROL maxMemory]** valor.

### Configurar autenticação {#setting-up-authentication}

Configure a autenticação de replicação no autor para que você possa replicar imagens para o serviço de entrega de imagens da Dynamic Media. Primeiro, obtenha um KeyStore e depois salve-o no **[!UICONTROL dynamic-media-replication]** e configure-a. O administrador da empresa recebeu um email de boas-vindas com o arquivo KeyStore e as credenciais necessárias durante o processo de provisionamento. Caso não tenha recebido essas informações, entre em contato com o Suporte ao cliente do Adobe.

**Para configurar a autenticação:**

1. Entre em contato com o Suporte ao cliente do Adobe para obter o arquivo KeyStore e a senha, caso ainda não tenha o arquivo e a senha. Essas informações são uma parte necessária do provisionamento. Ele associa as chaves à sua conta.

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Na página Gerenciamento de usuários , navegue até o **[!UICONTROL dynamic-media-replication]** e selecione para abrir.

   ![dm-replication](assets/dm-replication.png)

1. Na página Editar configurações do usuário para replicação de mídia dinâmica , selecione o **[!UICONTROL Armazenamento de chaves]** e selecione **[!UICONTROL Criar KeyStore]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. Digite uma senha e confirme a senha no **[!UICONTROL Definir senha de acesso do KeyStore]** caixa de diálogo.

   >[!NOTE]
   Lembre-se da senha porque você deve inseri-la novamente quando configurar o Agente de Replicação mais tarde.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. No **[!UICONTROL Editar configurações do usuário para replicação de mídia dinâmica]** expanda a página **Adicionar chave privada do arquivo KeyStore** e adicione o seguinte (veja as imagens a seguir):

   * No **[!UICONTROL Novo Alias]** , insira o nome de um alias que deseja usar posteriormente na configuração de replicação. Por exemplo, você pode usar `replication` como alias.
   * Selecionar **[!UICONTROL Arquivo KeyStore]**. Navegue até o arquivo KeyStore fornecido para você por Adobe, selecione-o e, em seguida, selecione **[!UICONTROL Abrir]**.
   * No **[!UICONTROL Senha do arquivo KeyStore]** digite a senha do arquivo KeyStore. Esta senha é **not** a senha do KeyStore criada na Etapa 5, mas é o Adobe de senha do arquivo KeyStore fornece no email de boas-vindas enviado a você durante o provisionamento. Entre em contato com o Suporte ao cliente do Adobe se você não tiver recebido uma senha do arquivo KeyStore.
   * No **[!UICONTROL Senha da chave privada]** , digite a senha da chave privada (pode ser a mesma senha da chave privada fornecida na etapa anterior). O Adobe fornece a senha da chave privada no email de boas-vindas enviado a você durante o provisionamento. Entre em contato com o Suporte ao cliente do Adobe se não tiver recebido uma senha de chave privada.
   * No **[!UICONTROL Alias da chave privada]** , insira o alias da chave privada. Por exemplo, `*companyname*-alias`. O Adobe fornece o alias da chave privada no email de boas-vindas enviado a você durante o provisionamento. Entre em contato com o Suporte ao cliente do Adobe se não tiver recebido um alias de chave privada.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. Selecionar **[!UICONTROL Salvar e fechar]** para salvar as alterações neste usuário.

   Em seguida, você deve [configurar o agente de replicação](#configuring-the-replication-agent).

### Configurar o agente de replicação {#configuring-the-replication-agent}

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes do autor]**.
1. Na página Agentes no autor, selecione **[!UICONTROL Replicação de imagem híbrida do Dynamic Media (s7delivery)]**.
1. Selecione **[!UICONTROL Editar]**.
1. Selecione o **[!UICONTROL Configurações]** e insira o seguinte:

   * **[!UICONTROL Ativado]** - Marque essa caixa de seleção para ativar o agente de replicação.
   * **[!UICONTROL Região]** - Definido para a região apropriada: América do Norte, Europa ou Ásia
   * **[!UICONTROL ID do locatário]** - Esse valor é o nome da sua empresa/locatário que está publicando no Serviço de replicação. Esse valor é a ID do locatário que o Adobe fornece no email de boas-vindas enviado a você durante o provisionamento. Caso não tenha recebido essas informações, entre em contato com o Suporte ao cliente do Adobe.
   * **[!UICONTROL Alias do Armazenamento de Chaves]** - Esse valor é igual ao valor **Novo Alias** valor definido ao gerar a chave em [Configuração da autenticação](#setting-up-authentication); por exemplo, `replication`. (Consulte a etapa 7 em [Configuração da autenticação](#setting-up-authentication).)
   * **[!UICONTROL Senha do Armazenamento de Chaves]** - A senha do KeyStore criada quando você tocou **[!UICONTROL Criar KeyStore]**. O Adobe não fornece essa senha. Veja a etapa 5 de [Configurar autenticação](#setting-up-authentication).

   A imagem a seguir mostra o agente de replicação com dados de amostra:

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. Selecionar **[!UICONTROL OK]**.

### Validar o agente de replicação do Dynamic Media {#validating-the-replication-agent-for-dynamic-media}

Para validar o agente de replicação do Dynamic Media, faça o seguinte:

Selecionar **[!UICONTROL Testar conexão]**. O exemplo de saída é o seguinte:

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
Você também pode verificar seguindo um destes procedimentos:
* Verifique os logs de replicação para garantir que o ativo seja replicado.
* Publique uma imagem. Selecione a imagem e selecione **[!UICONTROL Visualizadores]** no menu suspenso, selecione uma predefinição do visualizador. Selecionar **[!UICONTROL URL]**. Para verificar se você pode ver a imagem, copie e cole o caminho do URL no navegador.
>


### Solução de problemas de autenticação {#troubleshooting-authentication}

Ao configurar a autenticação, você pode encontrar alguns problemas com as soluções disponíveis. Antes de verificar esses problemas, verifique se você configurou a replicação.

#### Problema: Código de status HTTP 401 com mensagem - Autorização necessária {#problem-http-status-code-with-message-authorization-required}

Esse problema pode ser causado por uma falha na configuração do KeyStore para `dynamic-media-replication` usuário.

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**Solução:**
Verifique se a variável `KeyStore` é salvo em **dynamic-media-replication** e recebe a senha correta.

#### Problema: Não foi possível descriptografar a chave - Não foi possível descriptografar dados {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**Solução:**
Verifique a senha. A senha salva no agente de replicação não é a mesma senha usada para criar keystore.

#### Problema: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

Esse problema é causado por um erro de configuração na instância do autor do Experience Manager. O processo do Java™ no Autor não está recebendo a configuração correta `javax.net.ssl.trustStore`. Você vê este erro no log de replicação:

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

Ou o log de erros:

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**Solução:**
Certifique-se de que o processo Java™ no autor do Experience Manager tenha a propriedade do sistema `-Djavax.net.ssl.trustStore=` definido como um truststore válido.

#### Problema: O KeyStore não está configurado ou não está inicializado {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

Esse problema provavelmente é causado por um hotfix ou por um pacote de recursos que substitui o nó dynamic-media-user ou keystore.

Exemplo de log de replicação:

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**Solução:**

1. Navegue até a página Gerenciamento de usuários :
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. Na página Gerenciamento de usuários , navegue até o `dynamic-media-replication` e selecione para abrir.
1. Selecione o **[!UICONTROL KeyStore]** guia . Se a variável **[!UICONTROL Criar KeyStore]** for exibido, você deverá refazer as etapas em [Configurar autenticação](#setting-up-authentication) anteriormente.
1. Se tiver que refazer a configuração do KeyStore, é necessário [Configurando o Agente de Replicação](/help/assets/config-dynamic.md#configuring-the-replication-agent) novamente, também.

   Reconfigure o s7delivery Replication Agent.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. Selecionar **[!UICONTROL Testar conexão]** para que você possa verificar se a configuração é válida.

#### Problema: O Agente de Publicação está usando SSL em vez de OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

Esse problema provavelmente é causado por um hotfix ou pacote de recursos que não instalou corretamente ou sobrescreveu as configurações.

Exemplo de log de replicação:

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**Solução:**

1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.

   `localhost:4502/crx/de/index.jsp`

1. Navegue até o nó s7delivery Replication Agent.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. Adicione essa configuração ao agente de replicação (booleano com valor definido como **[!UICONTROL Verdadeiro]**):

   `enableOauth=true`

1. Ao lado do canto superior esquerdo da página, selecione **[!UICONTROL Salvar tudo]**.

### Testar sua configuração {#testing-your-configuration}

O Adobe recomenda que você execute um teste completo da configuração.

Certifique-se de que você já fez o seguinte antes de iniciar este teste:

* Predefinições de imagem adicionadas.
* Configurar **[!UICONTROL Configuração do Dynamic Media (Pré 6.3)]** em Cloud Services. O URL do Serviço de Imagem é necessário para este teste

**Para testar sua configuração:**

1. Faça upload de um ativo de imagem. (No Assets, navegue até **[!UICONTROL Criar]** > **[!UICONTROL Arquivos]** e selecione o arquivo.)
1. Aguarde a conclusão do fluxo de trabalho.
1. Publique o ativo da imagem. (Selecione o ativo e selecione **[!UICONTROL Publicação rápida]**.)
1. Navegue até as representações dessa imagem, abrindo a imagem e tocando **[!UICONTROL Representações]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. Selecione qualquer representação dinâmica.
1. Para obter o URL para esse ativo, selecione **[!UICONTROL URL]**.
1. Navegue até o URL selecionado e verifique se a imagem se comporta como esperado.

Outra maneira de testar se seus ativos foram entregues é anexar req=exists ao seu URL.

## Configurar Dynamic Media Cloud Services {#configuring-dynamic-media-cloud-services}

O Dynamic Media Cloud Service suporta publicação híbrida e entrega de imagens e vídeo, análise de vídeo e codificação de vídeo, entre outras coisas.

Como parte da configuração, você deve inserir uma ID de registro, o URL do serviço de vídeo, o URL do serviço de imagem, o URL do serviço de replicação e configurar a autenticação. Essas informações foram enviadas por email para você como parte do processo de provisionamento da conta. Caso não tenha recebido essas informações, entre em contato com o administrador da Adobe Experience Manager ou com o Suporte ao cliente do Adobe para obter as informações.

>[!NOTE]
Antes de configurar o Dynamic Media Cloud Services, certifique-se de configurar sua instância de publicação. Você também deve ter a replicação configurada antes de configurar o Dynamic Media Cloud Services.

**Para configurar o Dynamic Media Cloud Services:**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração do Dynamic Media (Pré-6.3)]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]**, em seguida selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração do Dynamic Media]** no campo Título, digite um título.
1. Se você estiver configurando o Dynamic Media para vídeo,

   * No **[!UICONTROL ID de registro]** digite sua ID de registro.
   * No **[!UICONTROL URL do serviço de vídeo]** , insira o URL do serviço de vídeo do Dynamic Media Gateway.

1. Se você estiver configurando o Dynamic Media para geração de imagens, na variável **[!UICONTROL URL do Serviço de imagem]** , insira o URL do serviço de imagem do gateway do Dynamic Media.
1. Selecionar **[!UICONTROL Salvar]** para retornar à página Navegador de configuração do Dynamic Media.
1. Para acessar o console de navegação global, selecione o logotipo Experience Manager.

## Configurar relatórios de vídeo {#configuring-video-reporting}

Você pode configurar relatórios de vídeo em várias instalações do Experience Manager usando o Dynamic Media Hybrid.

**Quando usar:** No momento em que você configura a configuração do Dynamic Media (pré 6.3), vários recursos são iniciados, incluindo relatórios de vídeo. A configuração cria um conjunto de relatórios em uma empresa regional do Analytics. Se você configurar vários nós de Autor, criará um conjunto de relatórios separado para cada um. Como resultado, os dados de relatório são inconsistentes entre as instalações. Além disso, se cada nó do Autor fizer referência ao mesmo servidor de Publicação híbrido, a última instalação do Autor alterará o conjunto de relatórios de destino para todos os relatórios de vídeo. Esse problema sobrecarrega o sistema do Analytics com muitos conjuntos de relatórios.

**Introdução:** Configure o relatório de vídeo concluindo as três tarefas a seguir.

1. Crie um pacote de predefinição do Video Analytics após configurar a Configuração do Dynamic Media (Pré 6.3) no primeiro nó do autor. Essa tarefa inicial é importante porque permite que uma nova configuração continue usando o mesmo conjunto de relatórios.
1. Instale o pacote de predefinição do Video Analytics em qualquer ***novo*** Nó Autor ***before*** Você configura a Configuração do Dynamic Media (Pré 6.3).
1. Verifique e depure a instalação do pacote.

### Crie um pacote predefinido do Video Analytics após configurar o primeiro nó Autor {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

Quando terminar esta tarefa, você terá um arquivo de pacote que contém as predefinições do Video Analytics. Essas predefinições contêm um conjunto de relatórios, o servidor de rastreamento, o namespace de rastreamento e a ID da organização do Experience Cloud, se disponível.

1. Se ainda não tiver feito isso, configure a Configuração do Dynamic Media (Pré 6.3).
1. (Opcional) Exiba e copie a ID do conjunto de relatórios (você deve ter acesso ao JCR). Embora não seja necessário ter a ID do conjunto de relatórios, facilita a validação.
1. Crie um pacote usando o Gerenciador de pacotes.
1. Edite o pacote para incluir um filtro.

   No Experience Manager: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. Crie o pacote.
1. Baixe ou compartilhe o pacote predefinido do Video Analytics para que ele possa ser compartilhado com os novos nós subsequentes do Autor.

### Instale o pacote de predefinição do Video Analytics antes de configurar mais nós do Author {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Certifique-se de concluir esta tarefa ***before*** Você configura a Configuração do Dynamic Media (Pré 6.3). Se isso não for feito, haverá a criação de outro conjunto de relatórios não utilizado. Além disso, mesmo que os relatórios de vídeo continuem a funcionar corretamente, a coleta de dados não é otimizada.

Verifique se o pacote de predefinição do Video Analytics do primeiro nó Autor está acessível no novo nó Autor .

1. Faça upload do pacote predefinido do Video Analytics criado anteriormente para o Gerenciador de pacotes.
1. Instale o pacote de predefinição do Video Analytics.
1. Configuração do Dynamic Media (Pré 6.3).

### Verificar e depurar a instalação do pacote {#verifying-and-debugging-the-package-installation}

1. Siga qualquer um destes procedimentos para verificar e, se necessário, depurar a instalação do pacote:

   * **Verifique a predefinição do Video Analytics por meio do JCR**
Para verificar a predefinição do Video Analytics por meio do JCR, você deve ter acesso ao CRXDE Lite.

      Experience Manager - No CRXDE Lite, navegue até `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

      Em `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      Se você não tiver acesso ao CRXDE Lite no nó Autor , poderá verificar a predefinição por meio do servidor Publicar .

   * **Verifique a predefinição do Video Analytics por meio do servidor de imagens**

      É possível validar a predefinição do Video Analytics diretamente, fazendo uma solicitação de dados req=userdata do servidor de imagens.
Por exemplo, para ver a predefinição do Analytics no nó Autor , você pode fazer a seguinte solicitação:

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      Para validar a predefinição nos servidores de Publicação, você pode fazer uma solicitação direta semelhante ao servidor de Publicação. As respostas são as mesmas nos nós Autor e Publicação . A resposta é semelhante ao seguinte:

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **Verifique a predefinição do Video Analytics por meio da ferramenta Relatório de vídeo no Experience Manager**
Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatório de vídeo]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      Caso veja a seguinte mensagem de erro, o conjunto de relatórios está disponível, mas não está preenchido. Esse erro está correto — e é desejado — em uma nova instalação antes que o sistema colete quaisquer dados.
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   Para gerar dados de relatório, faça upload e publique um vídeo. Use **[!UICONTROL Copiar URL]** e executar o vídeo pelo menos uma vez.

   Pode levar até 12 horas até que os dados de relatório sejam preenchidos a partir do uso do Visualizador de vídeo.

   Se houver um erro e o conjunto de relatórios não estiver definido corretamente, o alerta a seguir será exibido.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   Esse erro também será exibido se o Relatório de vídeo for executado antes que você configure os serviços de Configuração do Dynamic Media (Pré 6.3).

### Solução de problemas de configuração de relatório de vídeo {#troubleshooting-the-video-reporting-configuration}

* Durante a instalação, às vezes, as conexões com o servidor da API do Analytics expiram. A instalação repete a conexão 20 vezes, mas ainda falha. Quando essa situação ocorre, o arquivo de log registra vários erros. Pesquisar `SiteCatalystReportService`.
* Não instalar primeiro o pacote de predefinição do Analytics pode causar a criação de um novo conjunto de relatórios.
* Ao atualizar do Experience Manager 6.3 para o Experience Manager 6.4 ou Experience Manager 6.4.1 e, em seguida, configurar a configuração do Dynamic Media (Pré 6.3), o ainda cria um conjunto de relatórios. Esse problema é conhecido e está marcado para ser corrigido no Experience Manager 6.4.2.

### Sobre a predefinição do Video Analytics {#about-the-video-analytics-preset}

A predefinição do Video Analytics, às vezes conhecida simplesmente como predefinição do Analytics, é armazenada ao lado das predefinições do Visualizador no Dynamic Media. Basicamente, é o mesmo que uma predefinição do Visualizador, mas com informações usadas para configurar os relatórios do AppMeasurement e do Video Heartbeat.

As propriedades da predefinição são as seguintes:

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (não está presente nas versões anteriores do Experience Manager)

Experience Manager 6.4 e versões mais recentes salvam essa predefinição em `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## Replicar configurações do catálogo {#replicating-catalog-settings}

Publique suas próprias configurações de catálogo padrão como parte do processo de configuração por meio do JCR. Para replicar configurações de catálogo:

1. Em uma janela Terminal, execute o seguinte:

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. No Experience Manager, navegue até o seguinte local no CRXDE Lite (requer privilégios de administrador):

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Selecione o **[!UICONTROL Replicação]** guia .
1. Selecionar **[!UICONTROL Replicar]**.

## Replicar predefinições do visualizador {#replicating-viewer-presets}

Para entregar *um ativo com uma predefinição do visualizador, você deve replicar/publicar* a predefinição do visualizador. (Todas as predefinições do visualizador devem ser ativadas *e* replicado para obter o URL ou código incorporado de um ativo.
Consulte [Publicar predefinições do visualizador](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) para obter mais informações.

>[!NOTE]
Por padrão, o sistema mostra várias representações ao selecionar **[!UICONTROL Representações]** e várias predefinições do visualizador ao selecionar **[!UICONTROL Visualizadores]** na exibição detalhada do ativo. Você pode aumentar ou diminuir o número visto. Consulte [Aumente o número de predefinições de imagens exibidas](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Aumentar o número de predefinições do visualizador exibidas](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## Filtrar ativos para replicação {#filtering-assets-for-replication}

Em implantações que não são da Dynamic Media, você replica *all* ativos (imagens e vídeo) do ambiente de criação do Experience Manager para o nó de publicação do Experience Manager. Esse workflow é necessário porque os servidores de Publicação do Experience Manager também entregam os ativos.

No entanto, em implantações do Dynamic Media, como os ativos são fornecidos por meio da nuvem, não há necessidade de replicar esses mesmos ativos para nós de publicação do Experience Manager. Esse workflow de &quot;publicação híbrida&quot; evita custos de armazenamento extras e tempos de processamento mais longos para replicar ativos. Outros conteúdos, como visualizadores do Dynamic Media, páginas do Site e conteúdo estático, continuam a ser veiculados a partir dos nós de publicação do Experience Manager.

Além de replicar os ativos, os seguintes não ativos também são replicados:

* Configuração do Dynamic Media Delivery: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* Predefinições de imagem: `/conf/global/settings/dam/dm/presets/macros`
* Predefinições do visualizador: `/conf/global/settings/dam/dm/presets/viewer`

Os filtros fornecem uma maneira de *exclude* ativos de serem replicados para o nó de publicação do Experience Manager.

### Usar filtros de ativos padrão para replicação {#using-default-asset-filters-for-replication}

Se você usa o Dynamic Media para (1) geração de imagens na produção *ou* (2) imagem e vídeo, então você pode usar os filtros padrão que o Adobe fornece como estão. Os seguintes filtros estão ativos por padrão:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filtro</strong></td>
   <td><strong>Tipo Mime</strong></td>
   <td><strong>Representações</strong></td>
  </tr>
  <tr>
   <td>Entrega de imagem do Dynamic Media</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p> </p> </td>
   <td><p>Começa com <strong>image/</strong></p> <p>Contém <strong>application/</strong> e termina com <strong>set</strong>.</p> </td>
   <td>As "imagens-filtro" prontas para uso (aplica-se a ativos de imagens individuais, incluindo imagens interativas) e "conjuntos de filtros" (aplica-se a Conjuntos de rotação, Conjuntos de imagens, Conjuntos de mídia mista e Conjuntos de carrossel):
    <ul>
     <li>Incluir imagens PTIFF e metadados para replicação (Qualquer representação que comece com <strong>cqdam</strong>).</li>
     <li>Excluir da replicação a imagem original e as representações de imagem estática.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Entrega de vídeo do Dynamic Media</td>
   <td>filter-video</td>
   <td>Começa com <strong>video/</strong></td>
   <td>O "filter-video" pronto para uso:
    <ul>
     <li>Incluir representações de vídeo proxy, miniatura de vídeo/imagem de pôster, metadados (tanto em representações de vídeo pai quanto de vídeo) para replicação (Qualquer representação que comece com <strong>cqdam</strong>).</li>
     <li>Exclua da replicação do vídeo original e das representações estáticas de miniatura.<br /> <br /> <strong>Observação:</strong> As representações de vídeo proxy não contêm binários, mas são apenas propriedades de nós. Portanto, não há impacto no tamanho do repositório do editor.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Integração do Dynamic Media Classic (Scene7)</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p>filter-video</p> </td>
   <td><p>Começa com <strong>image/</strong></p> <p>Contém <strong>application/</strong> e termina com <strong>set</strong>.</p> <p>Começa com <strong>video/</strong></p> </td>
   <td><p>Você configura o URI de transporte para apontar para o servidor de publicação do Experience Manager em vez do URL do Adobe Dynamic Media Cloud Replication Service. Configurar esse filtro permite que o Dynamic Media Classic forneça ativos em vez da instância de publicação do Experience Manager.</p> <p>Os "filter-images" prontos para uso, "filter-sets" e "filter-video" irão:</p>
    <ul>
     <li>Inclua imagem PTIFF, representações de vídeo proxy e metadados para replicação. No entanto, como eles não existem no JCR-para aqueles que executam o Experience Manager - a integração do Dynamic Media Classic não faz nada.</li>
     <li>Exclua da replicação a imagem original, as representações de imagem estática, o vídeo original e as representações de miniatura estáticas. Em vez disso, a Dynamic Media Classic fornece ativos de imagem e vídeo.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Os filtros se aplicam aos tipos MIME e não podem ser específicos de caminho.

### Configurar filtros de ativos para implantações somente de vídeo {#setting-up-asset-filters-for-video-only-deployments}

Se estiver usando o Dynamic Media somente para vídeo, siga estas etapas para configurar filtros de ativos para replicação:

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes do autor]**.
1. Na página Agentes no autor, selecione **[!UICONTROL Agente padrão (publicar)]**.
1. Selecione **[!UICONTROL Editar]**.
1. No **[!UICONTROL Configurações do agente]** na caixa de diálogo , na **[!UICONTROL Configurações]** guia , verifique **[!UICONTROL Ativado]** para ligar o agente.
1. Selecionar **[!UICONTROL OK]**.
1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore da pasta esquerda, navegue até `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. Localizar **[!UICONTROL filter-video]**, clique com o botão direito do mouse e selecione **[!UICONTROL Copiar]**.
1. Na árvore da pasta esquerda, navegue até `/etc/replication/agents.author/publish`
1. Localizar `jcr:content`, clique com o botão direito do mouse e selecione **[!UICONTROL Colar]**.

Essas etapas configuram a instância de publicação do Experience Manager para fornecer a imagem de pôster de vídeo e os metadados de vídeo necessários para a reprodução, enquanto o próprio vídeo é entregue pelo Cloud Service Dynamic Media. O filtro também exclui da replicação o vídeo original e as representações de miniatura estáticas, que não são necessárias na instância de publicação.

### Configurar filtros de ativos para geração de imagens em implantações não relacionadas à produção {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

Se você estiver usando o Dynamic Media para geração de imagens em implantações que não são de produção, siga estas etapas para configurar filtros de ativos para replicação:

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes do autor]**.
1. Na página Agentes no autor, selecione **[!UICONTROL Agente padrão (publicar)]**.
1. Selecione **[!UICONTROL Editar]**.
1. No **[!UICONTROL Configurações do agente]** na caixa de diálogo , na **[!UICONTROL Configurações]** guia , verifique **[!UICONTROL Ativado]** para ligar o agente.
1. Selecionar **[!UICONTROL OK]**.
1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore da pasta esquerda, navegue até `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. Localizar **[!UICONTROL filter-images]**, clique com o botão direito do mouse e selecione **[!UICONTROL Copiar]**.
1. Na árvore da pasta esquerda, navegue até `/etc/replication/agents.author/publish`
1. Localizar `jcr:content`, clique com o botão direito do mouse e acesse **[!UICONTROL Criar]** > **[!UICONTROL Criar nó]**. Insira o nome `damRenditionFilters` de tipo `nt:unstructured`.
1. Localizar `damRenditionFilters`, clique com o botão direito do mouse e selecione **[!UICONTROL Colar]**.

Essas etapas configuram a instância de publicação do Experience Manager para fornecer as imagens ao ambiente de não produção. O filtro também exclui da replicação a imagem original e as representações estáticas, que não são necessárias na instância de publicação.

>[!NOTE]
Se houver muitos filtros diferentes em um autor, cada agente precisará de um usuário diferente atribuído a ele. O código granite impõe o modelo de um filtro por usuário. Sempre tenha um usuário diferente para cada configuração de filtro.
Você está usando mais de um filtro em um servidor? Por exemplo, um filtro para replicação publicar e um segundo filtro para s7delivery. Nesse caso, você deve garantir que esses dois filtros tenham um diferente **userId** atribuído a eles no `jcr:content` nó . Veja a imagem a seguir:

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### Personalizar filtros de ativos para replicação (opcional) {#customizing-asset-filters-for-replication}

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore da pasta esquerda, navegue até `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` para analisar os filtros.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. Para definir o Tipo MIME para o filtro, você pode localizar o Tipo MIME da seguinte maneira:

   No painel esquerdo, expanda `content > dam > <locate_your_asset> >  jcr:content > metadata` e, em seguida, na tabela, localize `dc:format`.

   O gráfico a seguir é um exemplo do caminho de um ativo para `dc:format`.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   Observe que a variável `dc:format` para o ativo `Fiji Red.jpg` é `image/jpeg`.

   Para que esse filtro se aplique a todas as imagens, independentemente do formato, defina o valor como `image/*` em que `*` é uma expressão regular aplicada a todas as imagens de qualquer formato.

   Para que o filtro seja aplicado somente às imagens do JPEG de tipo , insira um valor de `image/jpeg`.

1. Defina quais representações deseja incluir ou excluir da replicação.

   Os caracteres que você pode usar para filtrar para replicação incluem:

   | Caractere a ser usado | Como ele filtra ativos para replicação |
   | --- | --- |
   | `*` | Caracteres curingas |
   | `+` | Inclui ativos para replicação |
   | `-` | Exclui ativos da replicação |

   Vá até `content/dam/<locate your asset>/jcr:content/renditions`.

   O gráfico a seguir é um exemplo das representações de um ativo.

   ![chlimage_1-513](assets/chlimage_1-4.png)

   Usando o exemplo acima, se você quiser apenas replicar o PTIFF (TIFF da Pirâmide), digite `+cqdam,*` que inclui todas as representações que começam com `cqdam`. No exemplo, essa representação é `cqdam.pyramid.tiff`.

   Se você quiser apenas replicar o original, insira `+original`.

## Definição das configurações do Dynamic Media Image Server {#configuring-dynamic-media-image-server-settings}

A configuração do Dynamic Media Image Server envolve a edição do pacote Adobe CQ Scene7 ImageServer e do pacote Adobe CQ Scene7 PlatformServer.

>[!NOTE]
O Dynamic Media funciona imediatamente [depois de habilitado](#enabling-dynamic-media). No entanto, opcionalmente, você pode optar por ajustar a instalação configurando o Dynamic Media Image Server para atender a determinadas especificações ou requisitos.

**Pré-requisito** - *Antes* Se você configurar o Dynamic Media Image Server, certifique-se de que sua VM do Windows® inclui uma instalação das Bibliotecas do Microsoft® Visual C++. As bibliotecas são necessárias para executar o Dynamic Media Image Server. Você pode [faça o download do Microsoft® Visual C++ 2010 Redistributable Package (x64) aqui](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

Para definir as configurações do Dynamic Media Image Server:

1. No canto superior esquerdo do Experience Manager, selecione **[!UICONTROL Adobe Experience Manager]** para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Na página Configuração do console da Web do Adobe Experience Manager, acesse **[!UICONTROL OSGi]** > **[!UICONTROL Configuração]** para listar todos os pacotes que estão sendo executados no Experience Manager.

   Os Servidores de entrega da Dynamic Media podem ser encontrados com os seguintes nomes na lista:

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. Na lista de pacotes, à direita de Adobe CQ Scene7 ImageServer, selecione o **[!UICONTROL Editar]** ícone .
1. Na caixa de diálogo Adobe CQ Scene7 ImageServer, defina os seguintes valores de configuração:

   >[!NOTE]
   Geralmente, não há necessidade de alterar os valores padrão. No entanto, se você alterar os valores padrão, deverá reiniciar o pacote para que as alterações tenham efeito.

   | Propriedade | Valor padrão | Descrição |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | Número da porta a ser usado para comunicação com o processo ImageServer. Por padrão, a porta livre é detectada automaticamente. |
   | `AllowRemoteAccess.name` | *`empty`* | Permitir ou não permitir acesso remoto ao processo do ImageServer. Se falso, o servidor de imagem escuta apenas no host local.<br> As configurações padrão do Externalizador que apontam para o host local devem especificar o domínio ou endereço IP real da instância específica da VM. O motivo é porque o host local aponta para o sistema principal da VM.<br>Os domínios ou endereços IP da VM devem ter uma entrada de arquivo de host para que ela possa se resolver. |
   | `MaxRenderRgnPixels` | 16 MP | Tamanho máximo em megapixels renderizados. |
   | `MaxMessageSize` | 16 MB | Tamanho máximo da mensagem em megabytes que é entregue. |
   | `RandomAccessUrlTimeout` | 20 | Valor de tempo limite por quanto tempo, em segundos, o Servidor de Imagens aguarda o JCR para responder a uma solicitação de bloco variada. |
   | `WorkerThreads` | 10 | Número de threads de trabalho. |

1. Selecione **[!UICONTROL Salvar]**.
1. Na lista de pacotes, à direita de Adobe CQ Scene7 PlatformServer, selecione o **[!UICONTROL Editar]** ícone .
1. Na caixa de diálogo Adobe CQ Scene7 Platform Server, defina as seguintes opções de valor padrão:

   >[!NOTE]
   O Dynamic Media Image Server usa seu próprio cache de disco para armazenar em cache as respostas. O cache HTTP do Experience Manager e o Dispatcher não podem ser usados para armazenar em cache as respostas do Dynamic Media Image Server.

   | Propriedade | Valor padrão | Descrição |
   |---|---|---|
   | Cache ativado | Marcado | Se o cache de resposta está ativado |
   | Raízes de cache | cache | Um ou mais caminhos para as pastas do cache de resposta. Os caminhos relativos são resolvidos em relação à pasta interna do pacote s7imaging. |
   | Tamanho máx. do cache | 20000000 | Tamanho máximo do cache de resposta em bytes. |
   | Máximo de inscrições em cache | 100000 | Número máximo de entradas permitidas no cache. |

### Configurações de Manifesto padrão {#default-manifest-settings}

O manifesto padrão permite configurar os padrões usados para gerar as respostas de Delivery do Dynamic Media. Você pode ajustar a qualidade (qualidade do JPEG, resolução, modo de reamostragem), armazenar em cache (expiração) e impedir a renderização de imagens muito grandes (defaultpix, defaultthumbpix, maxpix).

O local da configuração de manifesto padrão é retirado do **[!UICONTROL Raiz do catálogo]** valor padrão do **[!UICONTROL Adobe CQ Scene7 PlatformServer]** pacote. Por padrão, esse valor está no seguinte caminho dentro de **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**

`/conf/global/settings/dam/dm/imageserver/`

![Configurar o servidor de imagem no CRXDE Lite](assets/configimageservercrxdelite.png)

Você pode alterar os valores das propriedades, conforme descrito na tabela abaixo, inserindo novos valores.

Quando terminar de alterar o manifesto padrão, no canto superior esquerdo da página, selecione **[!UICONTROL Salvar tudo]**.

Certifique-se de selecionar a variável **[!UICONTROL Controle de acesso]** (à direita da guia Properties ), em seguida, defina os privilégios de controle de acesso como `jcr:read` para todos e usuários de replicação de mídia dinâmica.

![Configure o servidor de imagem no CRXDE Lite e defina a guia Controle de acesso](assets/configimageservercrxdeliteaccesscontroltab.png)

Tabela de configurações de Manifesto e seus valores padrão:

| Propriedade | Valor padrão | Descrição |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | Cor de fundo padrão. Valor RGB usado para preencher qualquer área de uma imagem de resposta que não contenha dados de imagem reais. Consulte também [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api) na API de disponibilização de imagens. |
| `defaultpix` | `300,300` | Tamanho de exibição padrão. O servidor restringe as imagens de resposta a não serem maiores que essa largura e altura, se a solicitação não especificar o tamanho da exibição explicitamente usando wid=, hei= ou scl=.<br>Especificado como dois números inteiros, 0 ou maior, separados por vírgula. Largura e altura em pixels. Qualquer um dos valores pode ser definido como 0 para mantê-los sem restrições. Não se aplica a solicitações aninhadas/incorporadas.<br>Consulte também [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api) na API de disponibilização de imagens.<br>No entanto, normalmente, você está usando uma predefinição do visualizador ou uma predefinição de imagem para entregar o ativo. O padrão pix se aplica somente a um ativo que não está usando uma predefinição do visualizador ou uma predefinição de imagem. |
| `defaultthumbpix` | `100,100` | Tamanho padrão da miniatura. Usado em vez do atributo::DefaultPix para solicitações de miniatura (`req=tmb`).<br>O servidor restringe as imagens de resposta a não serem maiores que essa largura e altura. Essa ação é verdadeira se uma solicitação de miniatura (`req=tmb`) não especifica o tamanho explicitamente e não especifica o tamanho da exibição explicitamente usando `wid=`, `hei=`ou `scl=`.<br>Especificado como dois números inteiros, 0 ou maior, separados por vírgula. Largura e altura em pixels. Qualquer um dos valores pode ser definido como 0 para mantê-los sem restrições.<br>Não se aplica a solicitações aninhadas/incorporadas.<br>Consulte também [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api) na API de disponibilização de imagens. |
| `expiration` | `36000000` | Tempo de vida padrão do cache do cliente. Fornece um intervalo de expiração padrão no caso de um registro de catálogo específico não conter um valor de catálogo válido::Expiration .<br>Número real, 0 ou superior. Número de milissegundos até a expiração desde que os dados de resposta foram gerados. Defina como 0 para sempre expirar a imagem de resposta imediatamente, o que efetivamente desativa o armazenamento em cache do cliente. Por padrão, esse valor é definido como 10 horas, o que significa que, se uma nova imagem for publicada, levará 10 horas para a imagem antiga deixar o cache do usuário. Entre em contato com o Suporte ao cliente se precisar limpar o cache mais cedo.<br>Consulte também [Expiração](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) na API de disponibilização de imagens. |
| `jpegquality` | `80` | Atributos padrão de codificação de JPEG. Especifica os atributos padrão para imagens JPEG reply.<br>Número inteiro e sinalizador, separados por vírgula. O primeiro valor está no intervalo 1.100 e define a qualidade. O segundo valor pode ser 0 para comportamento normal ou 1 para desativar a amostragem regressiva de cromaticidade de RGB usada por codificadores de JPEG.<br>Consulte também [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api) na API de disponibilização de imagens. |
| `maxpix` | `2000,2000` | Limite de tamanho da imagem de resposta. Largura e altura máximas da imagem de resposta que são retornadas ao cliente.<br>O servidor retornará um erro se uma solicitação causar uma imagem de resposta cuja largura ou altura é maior que o atributo::MaxPix.<br>Consulte também [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html#image-serving-api) na API de disponibilização de imagens. |
| `resmode` | `SHARP2` | Modo de reamostragem padrão. Especifica a reamostragem e os atributos de interpolação padrão a serem usados para dimensionar dados de imagem.<br>Usado quando `resMode=` não é especificado em uma solicitação.<br>Os valores permitidos incluem `BILIN`, `BICUB`ou `SHARP2`.<br>Enum. Defina como 2 para `bilin`, 3 para `bicub`ou 4 para `sharp2` modo de interpolação. Use `sharp2` para obter melhores resultados.<br>Consulte também [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api) na API de disponibilização de imagens. |
| `resolution` | `72` | Resolução de objeto padrão. Fornece uma resolução de objeto padrão no caso de um registro de catálogo específico não conter um valor de catálogo válido::Resolution .<br>Número real, maior que 0. Normalmente expresso como pixels por polegada, mas também pode estar em outras unidades, como pixels por metro.<br>Consulte também [Resolução](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api) na API de disponibilização de imagens. |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | Esses valores representam um instantâneo do tempo de reprodução do vídeo e são passados para [encoding.com](https://www.encoding.com/). Consulte [Sobre a miniatura de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) para obter mais informações. |

## Configuração do gerenciamento de cores Dynamic Media {#configuring-dynamic-media-color-management}

O gerenciamento de cores do Dynamic Media permite que você corrija os ativos para visualização.

Com a correção de cores, os ativos assimilados retêm seu espaço de cores (RGB, CMYK, cinza) e o perfil de cores incorporado na representação de TIFF de pirâmide gerada. Quando você solicita uma representação dinâmica, a cor da imagem é corrigida no espaço de cores de destino. Você configura o perfil de cor de saída nas configurações de publicação do Dynamic Media no JCR.

O Adobe Color Consmanagement usa perfis ICC (International Ortium).

Você pode configurar o gerenciamento de cores do Dynamic Media e configurar predefinições de imagens usando saída CMYK, RGB ou Cinza. Consulte [Configuração de predefinições de imagens](/help/assets/managing-image-presets.md).

Casos de uso avançados podem usar uma configuração manual `icc=` modificador para selecionar explicitamente um perfil de cor de saída:

* `icc` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
O conjunto padrão de perfis de cores do Adobe só estará disponível se você tiver [Feature Pack 12445 da Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) instalado. Todos os pacotes de recursos e service packs estão disponíveis em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). O Feature Pack 12445 fornece perfis coloridos Adobe.


### Instalação do Feature Pack 12445 {#installing-feature-pack}

Para usar os recursos de gerenciamento de cores do Dynamic Media, instale o feature pack 12445.

**Para instalar o feature pack 12445:**

1. Navegar para [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) e faça o download de `cq-6.3.0-featurepack-12445`.

   Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre o uso de pacotes em [!DNL Adobe Experience Manager].

1. Instale o pacote de recursos.

### Configuração dos perfis de cores padrão {#configuring-the-default-color-profiles}

Depois de instalar o feature pack, configure os perfis de cores padrão apropriados para ativar a correção de cores ao solicitar dados de imagem do RGB ou CMYK.

**Para configurar os perfis de cores padrão:**

1. Em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**, navegue até `/conf/global/settings/dam/dm/imageserver/jcr:content` que contém os perfis padrão do Adobe Color.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. Adicione uma propriedade de correção de cor rolando até a parte inferior do **[!UICONTROL Propriedades]** guia . Insira manualmente o nome, o tipo e o valor da propriedade, descritos nas tabelas a seguir. Depois de inserir os valores, selecione **[!UICONTROL Adicionar]** e depois **[!UICONTROL Salvar tudo]** para salvar seus valores.

   As propriedades de correção de cores são descritas na seção **Propriedades de correções de cores** tabela. Os valores que você pode atribuir às propriedades de correção de cores estão na **Perfil de cores** tabela.

   Por exemplo, em **[!UICONTROL Nome]**, adicionar `iccprofilecmyk`, selecione **[!UICONTROL Tipo]** `String`e adicionar `WebCoated` como **[!UICONTROL Valor]**. Em seguida, selecione **[!UICONTROL Adicionar]** e depois **[!UICONTROL Salvar tudo]** para salvar seus valores.

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **Tabela de propriedades da correção de cores**

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Padrão</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">iccprofilergb</a></td>
   <td>Sequência de caracteres</td>
   <td>&lt;empty&gt;</td>
   <td>Nome do perfil de cor do RGB padrão.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">iccprofilecmyk</a></td>
   <td>Sequência de caracteres</td>
   <td>&lt;empty&gt;</td>
   <td>Nome do perfil de cores CMYK padrão.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">iccprofilegray</a></td>
   <td>Sequência de caracteres</td>
   <td>&lt;empty&gt;</td>
   <td>Nome do perfil de cor cinza padrão.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofilesrcrgb</a></td>
   <td>Sequência de caracteres</td>
   <td>&lt;empty&gt;</td>
   <td>Nome do perfil de cor RGB padrão usado para imagens RGB que não têm um perfil de cor incorporado</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrcmyk</a></td>
   <td>Sequência de caracteres</td>
   <td>&lt;empty&gt;</td>
   <td>Nome do perfil de cores CMYK padrão usado para imagens CMYK que não têm um perfil de cores incorporado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>Sequência de caracteres</td>
   <td>&lt;empty&gt;</td>
   <td>Nome do perfil de cor cinza padrão usado para imagens CMYK que não têm um perfil de cor incorporado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">icchblackpoint</a></td>
   <td>Booleano</td>
   <td>Verdadeiro</td>
   <td>Especifica se a compensação do ponto preto é feita durante a correção de cores. O Adobe recomenda que essa configuração esteja ativada.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">iccdither</a></td>
   <td>Booleano</td>
   <td>Falso</td>
   <td>Especifica se o pontilhamento é feito durante a correção de cores.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrenderintent</a></td>
   <td>Sequência de caracteres</td>
   <td>relativo</td>
   <td><p>Especifica o propósito de renderização. Os valores aceitáveis são: <strong>perceptivo, relativo, saturação, absoluto. </strong><i></i>Adobe recomenda <strong>relation </strong><i></i>como padrão.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Os nomes de propriedades fazem distinção entre maiúsculas e minúsculas e devem estar todos em minúsculas.

**Tabela de perfil de cores**

Os seguintes perfis de cores estão instalados:

<table>
 <tbody>
  <tr>
   <th><p>Nome</p> </th>
   <th><p>Espaço das cores</p> </th>
   <th><p>Descrição</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RGB</td>
   <td>Adobe RGB (1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>RGB Apple</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>RGB CIE</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>Revestido FOGRA27 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>Revestido FOGRA39 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColunaRevestida</td>
   <td>CMYK</td>
   <td>GRACoL 2006 revestido (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>RGB ColorMatch</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>Europa ISO Revestido FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euro scale Coated v2</td>
  </tr>
  <tr>
   <td>EuroescalaNãoRevestido</td>
   <td>CMYK</td>
   <td>Escala Euro não revestida v2</td>
  </tr>
  <tr>
   <td>JapãoColorCoated</td>
   <td>CMYK</td>
   <td>Japão - Cor 2001 Revestida</td>
  </tr>
  <tr>
   <td>JapãoCorJornal</td>
   <td>CMYK</td>
   <td>Jornal japonês Color 2002</td>
  </tr>
  <tr>
   <td>JapãoCorNãoRevestida</td>
   <td>CMYK</td>
   <td>Japão - Cor 2001 não revestida</td>
  </tr>
  <tr>
   <td>JapãoColorWebCoated</td>
   <td>CMYK</td>
   <td>Japão Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapãoWebCoated</td>
   <td>CMYK</td>
   <td>Japão - Revestido da Web (Anúncio)</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMYK</td>
   <td>Jornal dos EUA (SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC (1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>RGB ProPhoto</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>CMYK padrão do Photoshop 4</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>CMYK padrão do Photoshop 5</td>
  </tr>
  <tr>
   <td>CheifadoRevestido</td>
   <td>CMYK</td>
   <td>U.S. Sheetfeed Coated v2</td>
  </tr>
  <tr>
   <td>PlacaSemRevestimento</td>
   <td>CMYK</td>
   <td>U.S.A., Placa Não Revestida v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RGB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRGB</td>
   <td>RGB</td>
   <td>sRGB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>Fogra29 Não Revestido</td>
   <td>CMYK</td>
   <td>FOGRA29 não revestida (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>US Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Web Coated FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Papel SWOP Revestido da Web 2006 Grau 3</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Papel SWOP Revestido da Web 2006 Grau 5</td>
  </tr>
  <tr>
   <td>WebUn-Revelado</td>
   <td>CMYK</td>
   <td>U.S. Web Untrated v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RGB</td>
   <td>RGB de gama larga</td>
  </tr>
 </tbody>
</table>

1. Selecionar **[!UICONTROL Salvar tudo]**.

Por exemplo, é possível definir a variável **[!UICONTROL iccprofilergb]** para `sRGB`e **[!UICONTROL iccprofilecmyk]** para **[!UICONTROL WebCoated]**.

Isso faria o seguinte:

* Habilita a correção de cores para imagens RGB e CMYK.
* Pressupõe-se que as imagens RGB que não têm um perfil de cor estejam na *sRGB* espaço de cores.
* Pressupõe-se que as imagens CMYK que não têm um perfil de cor estejam em *WebCoated* espaço de cores.
* As representações dinâmicas que retornam a saída do RGB, retornam no espaço de cores *sRGB *.
* As renderizações dinâmicas que retornam a saída CMYK, retornam-na no *WebCoated* espaço de cores.

## Fornecer ativos {#delivering-assets}

Após concluir todas as tarefas acima, os ativos ativados do Dynamic Media são veiculados pelo Serviço de imagem ou vídeo. No Experience Manager, essa habilidade aparece em um **[!UICONTROL Copiar URL da imagem]**, **[!UICONTROL Copiar URL do visualizador]**, **[!UICONTROL Incorporar código do visualizador]** e no WCM.

Consulte [Entrega de ativos da Dynamic Media](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>Quando você...</strong></td>
   <td><strong>Resultado</strong></td>
  </tr>
  <tr>
   <td>Copiar um URL de imagem</td>
   <td><p>A caixa de diálogo Copiar URL exibe um URL semelhante ao seguinte (o URL é somente para fins de demonstração):</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>Onde <code>IMAGESERVICEPUBLISHNODE</code> refere-se ao URL do Serviço de imagem.</p> <p>Consulte também <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de ativos da Dynamic Media</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar um URL do visualizador</td>
   <td><p>A caixa de diálogo Copiar URL exibe um URL semelhante ao seguinte (o URL é somente para fins de demonstração):</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>Onde <code>PUBLISHNODE</code> refere-se ao nó de publicação do Experience Manager regular e <code>IMAGESERVICEPUBLISHNODE</code> refere-se ao URL do Serviço de imagem.</p> <p>Consulte também <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de ativos da Dynamic Media</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar o código incorporado de um visualizador</td>
   <td><p>A caixa de diálogo Copiar código incorporado exibe um trecho de código semelhante ao seguinte (a amostra de código é somente para fins de demonstração):</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p>Onde <code>PUBLISHNODE</code> refere-se ao nó de publicação do Experience Manager regular e <code>IMAGESERVICEPUBLISHNODE</code> refere-se ao URL do Serviço de imagem.</p> <p>Consulte também <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de ativos da Dynamic Media</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media WCM e componentes de mídia interativa {#wcm-dynamic-media-and-interactive-media-components}

As páginas WCM que fazem referência aos componentes do Dynamic Media e do Interative Media fazem referência ao serviço de entrega.
