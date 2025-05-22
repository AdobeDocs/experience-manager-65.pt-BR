---
title: Configurar o Dynamic Media - modo híbrido
description: Saiba como configurar o Dynamic Media - Modo híbrido.
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
solution: Experience Manager, Experience Manager Assets
source-git-commit: 952b4d675d2f0291d1761cf2e7d9e459362ac404
workflow-type: tm+mt
source-wordcount: '7982'
ht-degree: 1%

---

# Configurar o Dynamic Media - modo híbrido {#configuring-dynamic-media-hybrid-mode}

## Dynamic Media - Pacote complementar híbrido (AEM 6.5.23 e posterior)

A partir do AEM 6.5 Service Pack 23, um novo pacote complementar está disponível para Dynamic Media - Modo híbrido. Este pacote inclui o pacote `cq-scene7-imaging` especificamente compatível com o modo de execução Dynamic Media - Híbrido.

**Correção de chave incluída**

Correção de um problema no Dynamic Media - Implantações híbridas em que as atualizações do parâmetro `catalog.expiration` em `/conf/global/settings/dam/dm/imageserver` não eram refletidas nas URLs do servidor ou do autor, apesar da replicação ser bem-sucedida sem erros. A atualização garante valores de expiração consistentes entre o CRX/DE, a resposta do servidor e os URLs de entrega pública. Por sua vez, melhora o comportamento do cache e a confiabilidade das transformações de imagem. (ASSETS-44837)

**Considerações importantes**

* O conjunto `cq-scene7-imaging` na instalação base do AEM 6.5.23 (e posterior) é *não compatível* com o Dynamic Media - modo de execução híbrido.
* A instalação do Service Pack 23 (e posterior) sozinha *não atualiza automaticamente* o pacote `cq-scene7-imaging` existente nas instâncias do AEM configuradas para Dynamic Media - Híbrido (modo de execução `-r dynamicmedia`).

**Quando instalar o pacote complementar Híbrido**

* Ao atualizar diretamente para o AEM 6.5.23 (e posterior) do AEM 6.5.19 ou anterior.
* Quando precisar de correções específicas para o Dynamic Media - funcionalidade híbrida.
* Ao implantar uma nova instância do Dynamic Media - Hybrid diretamente do AEM 6.5 GA (Disponibilidade geral) para o Service Pack 23 (e posterior).

**Baixar pacote complementar híbrido**

O pacote complementar do Hybrid está disponível na Distribuição de software e estará acessível ao público na versão oficial do AEM 6.5.23, em 22 de maio de 2025.

[Baixar Dynamic Media - Pacote complementar híbrido](https://author-p11553-e21065.adobeaemcloud.com/ui#/aem/assetdetails.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-dam-delivery-65-hybrid-addon-1.0.zip).


## Fim do suporte para SSL 2.0 e 3.0 e TLS 1.0 e 1.1.

Fim do suporte para Secure Socket Layer 2.0 e 3.0 e Transport Layer Security 1.0 e 1.1.

A partir de 30 de abril de 2024, o Adobe Dynamic Media encerrou o suporte para o seguinte:

* SSL (Secure Socket Layer) 2.0
* SSL 3.0
* TLS (Transport Layer Security) 1.0 e 1.1
* As seguintes cifras fracas no TLS 1.2:
  `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  `TLS_RSA_WITH_AES_256_GCM_SHA384`
  `TLS_RSA_WITH_AES_256_CBC_SHA256`
  `TLS_RSA_WITH_AES_256_CBC_SHA`
  `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  `TLS_RSA_WITH_AES_128_GCM_SHA256`
  `TLS_RSA_WITH_AES_128_CBC_SHA256`
  `TLS_RSA_WITH_AES_128_CBC_SHA`
  `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

Consulte também [Limitações do Dynamic Media](/help/assets/limitations.md).

<!-- FOR ABOVE - CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->


O Dynamic Media-Hybrid deve ser ativado e configurado para uso. Dependendo do caso de uso, o Dynamic Media tem várias [configurações com suporte](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Se você pretende configurar e executar o Dynamic Media no modo de execução do Scene7, consulte [Configurar o Dynamic Media - Modo Scene7](/help/assets/config-dms7.md).
>
>Se você pretende configurar e executar o Dynamic Media no modo de execução híbrido, siga as instruções nesta página.

Saiba mais sobre como trabalhar com [vídeo](/help/assets/video.md) no Dynamic Media.

>[!NOTE]
>
>Se você usar o Adobe Experience Manager configurado para ambientes diferentes, como um para desenvolvimento, armazenamento temporário e produção em tempo real, configure os Serviços de nuvem do Dynamic Media para cada ambiente.

>[!NOTE]
>
>Se tiver problemas com a configuração do Dynamic Media, verifique os arquivos de log específicos do Dynamic Media. Esses arquivos são instalados automaticamente quando você ativa o Dynamic Media:
>
>* `s7access.log`
>* `ImageServing.log`
>
>Eles estão documentados em [Monitorar e manter sua instância do Experience Manager](/help/sites-deploying/monitoring-and-maintaining.md).

A publicação e a entrega híbridas são um recurso principal da adição do Dynamic Media ao Adobe Experience Manager. A publicação híbrida permite que você forneça ativos do Dynamic Media, como imagens, conjuntos e vídeos, a partir da nuvem em vez de partir dos nós de publicação do Experience Manager.

Outros conteúdos, como visualizadores do Dynamic Media, páginas do site e conteúdo estático continuam a ser veiculados a partir dos nós de publicação do Experience Manager.

Se você for um cliente do Dynamic Media, precisará usar a entrega híbrida como mecanismo de entrega para todo o conteúdo do Dynamic Media.

## Arquitetura de publicação híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## Arquitetura de publicação híbrida para imagens {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## Configurações compatíveis do Dynamic Media {#supported-dynamic-media-configurations}

As tarefas de configuração a seguir fazem referência aos seguintes termos:

| **Termo** | **Dynamic Media Habilitada** | **Descrição** |
|---|---|---|
| Nó Autor do Experience Manager | Marca de seleção branca em um círculo verde | O nó do autor que você implanta no local ou por meio do Managed Services. |
| Nó Publicar do Experience Manager | &quot;X&quot; branco em um quadrado vermelho. | O nó de publicação que você implanta no local ou por meio do Managed Services. |
| Nó de publicação do serviço de imagem | Marca de seleção branca em um círculo verde. | O nó de publicação executado nos data centers gerenciados pelo Adobe. Refere-se ao URL do serviço de imagem. |

Você pode optar por implementar o Dynamic Media apenas para criação de imagens, apenas para vídeo ou para criação de imagens e vídeo. Para determinar as etapas para configurar o Dynamic Media para o seu cenário específico, consulte a tabela a seguir.

<table>
 <tbody>
  <tr>
   <td><strong>Cenário</strong></td>
   <td ><strong>Como funciona</strong></td>
   <td><strong>Etapas de configuração</strong></td>
  </tr>
  <tr>
   <td>Entregar SOMENTE imagens em produção</td>
   <td>As imagens são entregues por meio de servidores nos data centers mundiais da Adobe e, em seguida, armazenadas em cache por um CDN para desempenho escalável e alcance global.</td>
   <td>
    <ol>
     <li>No nó <strong>author</strong> do Experience Manager, <a href="#enabling-dynamic-media">habilite o Dynamic Media</a>.</li>
     <li>Configure a geração de imagens no <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services</a>.</li>
     <li><a href="#configuring-image-replication">Configurar replicação de imagem</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configurações do catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Usar filtros de ativos padrão para replicação</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Definir configurações do Servidor de Imagens do Dynamic Media</a>.</li>
     <li><a href="#delivering-assets">Enviar ativos</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Fornecer SOMENTE imagens na pré-produção (desenvolvimento, controle de qualidade, preparo e assim por diante).</td>
   <td>As imagens são entregues por meio do nó de publicação do Experience Manager. Nesse cenário, como o tráfego é mínimo, não há necessidade de fornecer imagens ao data center da Adobe. E permite uma visualização segura do conteúdo antes do lançamento da produção.</td>
   <td>
    <ol>
     <li>No nó <strong>author</strong> do Experience Manager, <a href="#enabling-dynamic-media">habilite o Dynamic Media</a>.</li>
     <li>No nó <strong>publish</strong> do Experience Manager, <a href="#enabling-dynamic-media">habilite o Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li>Configure o <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">filtro de ativos para imagens não relacionadas à produção</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Defina as configurações do Servidor de imagens do Dynamic Media.</a></li>
     <li><a href="#delivering-assets">Entregar ativos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Fornecer SOMENTE vídeo em qualquer ambiente (produção, desenvolvimento, controle de qualidade, preparo e assim por diante)</td>
   <td>Os vídeos são entregues e armazenados em cache por um CDN para desempenho escalável e alcance global. A imagem do pôster do vídeo (miniatura do vídeo que é exibida antes do início da reprodução) é entregue pela instância de publicação do Experience Manager.</td>
   <td>
    <ol>
     <li>No nó <strong>author</strong> do Experience Manager, <a href="#enabling-dynamic-media">habilite o Dynamic Media</a>.</li>
     <li>No nó <strong>publicar</strong> do Experience Manager, <a href="#enabling-dynamic-media">habilite o Dynamic Media</a> (a instância de publicação fornece a imagem do pôster do vídeo e os metadados para reprodução do vídeo).</li>
     <li>Configurar vídeo no <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services.</a></li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li>Configure o <a href="#setting-up-asset-filters-for-video-only-deployments">filtro de ativos para somente vídeo</a>.</li>
     <li><a href="#delivering-assets">Entregar ativos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Entregar imagens e vídeo na produção</td>
   <td><p>Os vídeos são entregues e armazenados em cache por um CDN para desempenho escalável e alcance global. Imagens e imagens de pôster de vídeo são entregues por servidores em data centers mundiais da Adobe e, em seguida, armazenadas em cache por um CDN para desempenho escalável e alcance global.</p> <p>Consulte as seções anteriores para configurar imagem ou vídeo na pré-produção. </p> </td>
   <td>
    <ol>
     <li>No nó <strong>author</strong> do Experience Manager, <a href="#enabling-dynamic-media">habilite o Dynamic Media</a>.</li>
     <li>Configurar vídeo no <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services.</a></li>
     <li>Configurar imagens no <a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services.</a></li>
     <li><a href="#configuring-image-replication">Configurar replicação de imagem</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configurações do catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar predefinições do visualizador</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Use filtros de ativos padrão para replicação.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Defina as configurações do Servidor de imagens do Dynamic Media.</a></li>
     <li><a href="#delivering-assets">Entregar ativos.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Ativar Dynamic Media {#enabling-dynamic-media}

A [Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) está desabilitada por padrão. Para aproveitar os recursos do Dynamic Media, habilite o Dynamic Media usando o modo de execução `dynamicmedia` da mesma maneira que você faria, por exemplo, com o modo de execução `publish`. Antes de habilitar, verifique os [requisitos técnicos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>Habilitar o Dynamic Media pelo modo de execução substitui a funcionalidade no Experience Manager 6.1 e no Experience Manager 6.0, onde você habilita o Dynamic Media definindo o sinalizador `dynamicMediaEnabled` como **[!UICONTROL true]**. Esse sinalizador não tem funcionalidade no Experience Manager 6.2 e posteriores. Além disso, não é necessário reiniciar o quickstart para ativar o Dynamic Media.

Ao habilitar o Dynamic Media, os recursos do Dynamic Media estão disponíveis na interface e cada ativo de imagem carregado recebe uma representação *cqdam.pyramid.tiff* usada para a entrega rápida de representações de imagem dinâmicas. Esses PTIFFs têm vantagens significativas, como as seguintes:

* A capacidade de gerenciar apenas uma única imagem de origem principal e gerar representações infinitas a qualquer momento, sem armazenamento adicional.
* A capacidade de usar visualização interativa, como zoom, panorâmica e rotação.

Se quiser usar o Dynamic Media Classic no Experience Manager, não habilite o Dynamic Media, a menos que esteja usando um [cenário específico](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). O Dynamic Media está desativado, a menos que você o ative no modo de execução.

Para ativar o Dynamic Media, você deve ativar o modo de execução do Dynamic Media na linha de comando ou no nome do arquivo de início rápido.

**Para habilitar o Dynamic Media:**

1. Na linha de comando, ao iniciar o início rápido, faça o seguinte:

   * Adicione `-r dynamicmedia` ao final da linha de comando ao iniciar o arquivo jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   Se você estiver publicando no s7delivery, também deverá incluir os seguintes argumentos do trustStore:

   ```shellsession {.line-numbers}
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. Solicite `https://localhost:4502/is/image` e verifique se o Servidor de imagens está em execução agora.

   >[!NOTE]
   >
   >Para solucionar problemas com o Dynamic Media, consulte os seguintes logs no diretório `crx-quickstart/logs/`:
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - O log do ImageServer fornece estatísticas e informações analíticas usadas para analisar o comportamento do processo interno do ImageServer.
   >
   Exemplo de um nome de arquivo de log do Servidor de Imagens: `ImageServer-57346-2020-07-25.log`
   >
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - O log de acesso do s7registra cada solicitação feita ao Dynamic Media pelo `/is/image` e `/is/content`.
   >
   Esses logs são usados somente quando o Dynamic Media está habilitado. Eles não estão incluídos no pacote **Download Completo** gerado pela página `system/console/status-Bundlelist`; ao ligar para o Suporte ao Cliente se você tiver um problema com o Dynamic Media, anexe ambos os logs ao problema.

### Se você instalou o Experience Manager em uma porta ou caminho de contexto diferente ... {#if-you-installed-aem-to-a-different-port-or-context-path}

Se estiver implantando o [Experience Manager em um servidor de aplicativos](/help/sites-deploying/application-server-install.md) e tiver o Dynamic Media habilitado, você deverá configurar o **autodomínio** no Externalizador. Caso contrário, a geração de miniaturas para ativos não funcionará corretamente para ativos do Dynamic Media.

Além disso, se você executar o início rápido em uma porta ou caminho de contexto diferente, também será necessário alterar o **autodomínio**.

Quando o Dynamic Media está ativado, as representações de miniatura estáticas para ativos de imagem são geradas usando o Dynamic Media. Para que a geração de miniaturas funcione corretamente para o Dynamic Media, o Experience Manager deve executar uma solicitação de URL para si mesmo e deve saber o número da porta e o caminho do contexto.

No Experience Manager:

* O **autodomínio** no [Externalizador](/help/sites-developing/externalizer.md) é usado para recuperar o número da porta e o caminho do contexto.
* Se nenhum **autodomínio** estiver configurado, o número da porta e o caminho do contexto serão recuperados do serviço HTTP Jetty.

Em uma implantação do Experience Manager QuickStart WAR, o número da porta e o caminho do contexto não podem ser derivados, portanto, você deve configurar um **autodomínio**. Consulte a [Documentação do Externalizador](/help/sites-developing/externalizer.md) sobre como configurar o **autodomínio**.

>[!NOTE]
>
Em uma [implantação autônoma do Experience Manager Quickstart](/help/sites-deploying/deploy.md), um **autodomínio** geralmente não precisa ser configurado, pois o número da porta e o caminho de contexto podem ser configurados automaticamente. No entanto, se todas as interfaces de rede estiverem desativadas, você deverá configurar o **autodomínio**.

## Desativar Dynamic Media  {#disabling-dynamic-media}

O Dynamic Media não está habilitado por padrão. No entanto, se você tiver ativado o Dynamic Media anteriormente, poderá desativá-lo mais tarde.

Para desabilitar o Dynamic Media depois de habilitá-lo, remova o sinalizador de modo de execução `-r dynamicmedia`.

**Para desabilitar o Dynamic Media:**

1. Na linha de comando, ao iniciar o início rápido, você pode executar um dos seguintes procedimentos:

   * Não adicione `-r dynamicmedia` à linha de comando ao iniciar o arquivo jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Solicitação `https://localhost:4502/is/image`. Você receberá uma mensagem informando que o Dynamic Media está desativado.

   >[!NOTE]
   >
   Depois que o modo de execução do Dynamic Media é desativado, a etapa do fluxo de trabalho que gera a representação `cqdam.pyramid.tiff` é ignorada automaticamente. Também desativa o suporte à representação dinâmica e outros recursos do Dynamic Media.
   >
   Observe também que quando o modo de execução do Dynamic Media é desativado após a configuração do servidor do Experience Manager, todos os ativos que foram carregados nesse modo de execução agora são inválidos.

## (Opcional) Migração de predefinições e configurações do Dynamic Media da versão 6.3 para a 6.5, sem tempo de inatividade {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Se estiver atualizando o Experience Manager - Dynamic Media da versão 6.3 para a 6.5 (que agora inclui a capacidade de implantações com tempo de inatividade zero), você deverá executar o seguinte comando curl. O comando migra todas as suas predefinições e configurações do `/etc` para o `/conf` no CRXDE Lite.

>[!NOTE]
>
Se você executar a instância do Experience Manager no modo de compatibilidade (ou seja, se tiver o pacote de compatibilidade instalado), não será necessário executar esses comandos.

Para todas as atualizações, com ou sem o pacote de compatibilidade, você pode copiar as predefinições do visualizador padrão prontas para uso que originalmente acompanhavam o Dynamic Media executando o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar qualquer predefinição e configuração personalizada do visualizador criada de `/etc` para `/conf`, execute o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Configurar replicação de imagem {#configuring-image-replication}

A entrega de imagens do Dynamic Media funciona publicando ativos de imagem, incluindo miniaturas de vídeo, do Experience Manager Author e replicando-os para o serviço de replicação sob demanda da Adobe (o URL do Serviço de replicação). O Assets é então fornecido por meio do serviço de entrega de imagens sob demanda (o URL do serviço de imagem).

Faça o seguinte:

1. [Configurar autenticação](#setting-up-authentication).
1. [Configurar o agente de replicação](#configuring-the-replication-agent).

O Agente de replicação publica ativos do Dynamic Media, como imagens, metadados de vídeo e conjuntos, no Serviço de imagens hospedado pela Adobe. O Agente de replicação não está habilitado por padrão.

Após configurar o agente de replicação, você deve [validar e testar se ele foi configurado com êxito](#validating-the-replication-agent-for-dynamic-media). Esta seção descreve esses procedimentos.

>[!NOTE]
>
O limite de memória padrão para a criação de PTIFF é de 3 GB em todos os fluxos de trabalho. Por exemplo, você pode processar uma imagem que requer 3 GB de memória enquanto outros fluxos de trabalho estão pausados ou processar 10 imagens em paralelo que exigem 300 MB de memória cada.
>
O limite de memória é configurável e se ajusta à disponibilidade de recursos do sistema e ao tipo de conteúdo de imagem que está sendo processado. Se você tiver muitos ativos grandes e memória suficiente no sistema, poderá aumentar esse limite para garantir que as imagens sejam processadas em paralelo.
>
Uma imagem que requer mais do que o limite máximo de memória é rejeitada.
>
Para alterar o limite de memória para criação de PTIFF, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** > **[!UICONTROL Adobe CQ Scene7 PTiffManager]** e altere o valor **[!UICONTROL maxMemory]**.

### Configurar autenticação {#setting-up-authentication}

Configure a autenticação de replicação no autor para replicar imagens para o serviço de entrega de imagens do Dynamic Media. Primeiro, você obtém um KeyStore e depois o salva com o usuário **[!UICONTROL dynamic-media-replication]** e o configura. O administrador da sua empresa recebeu um email de boas-vindas com o arquivo KeyStore e as credenciais necessárias durante o processo de provisionamento. Se você não recebeu essas informações, entre em contato com o Suporte ao cliente da Adobe.

**Para configurar a autenticação:**

1. Entre em contato com o Suporte ao cliente da Adobe para obter seu arquivo e senha do KeyStore se você ainda não tiver o arquivo e a senha. Essas informações são uma parte necessária do provisionamento. Ele associa as chaves à sua conta.

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Na página Gerenciamento de usuários, navegue até o usuário **[!UICONTROL dynamic-media-replication]** e selecione para abrir.

   ![dm-replication](assets/dm-replication.png)

1. Na página Editar configurações de usuário para replicação de mídia dinâmica, selecione a guia **[!UICONTROL Armazenamento de chaves]** e selecione **[!UICONTROL Criar armazenamento de chaves]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. Digite uma senha e confirme-a na caixa de diálogo **[!UICONTROL Definir senha de acesso do KeyStore]**.

   >[!NOTE]
   >
   Lembre-se da senha porque você deve digitá-la novamente quando configurar o Agente de Replicação posteriormente.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. Na página **[!UICONTROL Editar Configurações de Usuário para replicação de mídia dinâmica]**, expanda a área **Adicionar Chave Privada do arquivo KeyStore** e adicione o seguinte (veja as imagens a seguir):

   * No campo **[!UICONTROL Novo Alias]**, digite o nome de um alias que você deseja usar posteriormente na configuração de replicação. Por exemplo, você poderia usar `replication` como um alias.
   * Selecione **[!UICONTROL Arquivo do KeyStore]**. Navegue até o arquivo do KeyStore fornecido pelo Adobe, selecione-o e, em seguida, **[!UICONTROL Abrir]**.
   * No campo **[!UICONTROL Senha do arquivo do KeyStore]**, digite a senha do arquivo do KeyStore. Esta senha é **não** a senha do KeyStore que você criou na Etapa 5, mas é a senha do Arquivo do KeyStore que a Adobe fornece no email de boas-vindas enviado a você durante o provisionamento. Entre em contato com o Suporte ao cliente da Adobe se você não recebeu uma senha do arquivo do KeyStore.
   * No campo **[!UICONTROL Senha da Chave Privada]**, digite a senha da chave privada (pode ser a mesma senha da chave privada fornecida na etapa anterior). O Adobe fornece a senha da chave privada no email de boas-vindas enviado a você durante o provisionamento. Entre em contato com o Suporte ao cliente da Adobe se você não recebeu uma senha de chave privada.
   * No campo **[!UICONTROL Alias da Chave Privada]**, insira o alias da chave privada. Por exemplo, `*companyname*-alias`. O Adobe fornece o alias da chave privada no email de boas-vindas enviado a você durante o provisionamento. Entre em contato com o Suporte ao cliente da Adobe se você não recebeu um alias de chave privada.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. Selecione **[!UICONTROL Salvar e fechar]** para salvar suas alterações neste usuário.

   Em seguida, você deve [configurar o agente de replicação](#configuring-the-replication-agent).

### Configurar o agente de replicação {#configuring-the-replication-agent}

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes no autor]**.
1. Na página Agentes no autor, selecione **[!UICONTROL Replicação de imagem híbrida do Dynamic Media (s7delivery)]**.
1. Selecione **[!UICONTROL Editar]**.
1. Selecione a guia **[!UICONTROL Configurações]** e digite o seguinte:

   * **[!UICONTROL Habilitado]** - marque esta caixa de seleção para habilitar o agente de replicação.
   * **[!UICONTROL Região]** - Defina para a região apropriada: América do Norte, Europa ou Ásia
   * **[!UICONTROL ID do Locatário]** - Este valor é o nome da sua empresa/locatário que está publicando no Serviço de Replicação. Esse valor é a ID do locatário fornecida pela Adobe no email de boas-vindas enviado a você durante o provisionamento. Se você não recebeu essas informações, entre em contato com o Suporte ao cliente da Adobe.
   * **[!UICONTROL Alias do Repositório de Chaves]** - Este valor é igual ao valor **Novo Alias** definido ao gerar a chave em [Configurando a Autenticação](#setting-up-authentication); por exemplo, `replication`. (Consulte a etapa 7 em [Configurando a Autenticação](#setting-up-authentication).)
   * **[!UICONTROL Senha do Key Store]** - A senha do KeyStore que foi criada quando você tocou em **[!UICONTROL Criar KeyStore]**. A Adobe não fornece essa senha. Consulte a etapa 5 de [Configurando a autenticação](#setting-up-authentication).

   A imagem a seguir mostra o agente de replicação com dados de amostra:

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. Selecione **[!UICONTROL OK]**.

### Validar o agente de replicação para Dynamic Media {#validating-the-replication-agent-for-dynamic-media}

Para validar o agente de replicação do Dynamic Media, faça o seguinte:

Selecione **[!UICONTROL Testar Conexão]**. O exemplo de saída é o seguinte:

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
>
Você também pode verificar executando um dos procedimentos a seguir:
>
* Verifique os logs de replicação para garantir que o ativo seja replicado.
* Publique uma imagem. Selecione a imagem e **[!UICONTROL Visualizadores]** no menu suspenso, em seguida, selecione uma predefinição do visualizador. Selecione **[!UICONTROL URL]**. Para verificar se você pode ver a imagem, copie e cole o caminho do URL no navegador.
>

### Solução de problemas de autenticação {#troubleshooting-authentication}

Ao configurar a autenticação, veja a seguir alguns problemas que você pode encontrar com as soluções da. Antes de verificar esses problemas, verifique se você configurou a replicação.

#### Problema: Código de Status HTTP 401 com Mensagem - Autorização Necessária {#problem-http-status-code-with-message-authorization-required}

Esse problema pode ser causado por uma falha ao configurar o KeyStore para o usuário `dynamic-media-replication`.

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
Verifique se `KeyStore` foi salvo no usuário **dynamic-media-replication** e se foi fornecida a senha correta.

#### Problema: Não Foi Possível Descriptografar A Chave - Não Foi Possível Descriptografar Os Dados {#problem-could-not-decrypt-key-could-not-decrypt-data}

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
Verifique a senha. A senha salva no agente de replicação não é a mesma senha usada para criar o keystore.

#### Problema: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

Esse problema é causado por um erro de configuração na instância do autor do Experience Manager. O processo Java™ no Autor não está obtendo o `javax.net.ssl.trustStore` correto. Você vê este erro no log de replicação:

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
Verifique se o processo Java™ no Autor do Experience Manager tem a propriedade do sistema `-Djavax.net.ssl.trustStore=` definida como um truststore válido.

#### Problema: KeyStore não está configurado ou não foi inicializado {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

Esse problema provavelmente é causado por um hot fix ou um pacote de recursos que substitui o nó do usuário de mídia dinâmica ou do armazenamento de chaves.

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

1. Navegue até a página Gerenciamento de usuários:
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. Na página Gerenciamento de usuários, navegue até o usuário `dynamic-media-replication` e selecione para abrir.
1. Selecione a guia **[!UICONTROL KeyStore]**. Se o botão **[!UICONTROL Criar KeyStore]** for exibido, você deverá refazer as etapas em [Configurando a Autenticação](#setting-up-authentication) anteriormente.
1. Se você tiver que refazer a configuração do KeyStore, também deverá [Configurar o Agente de Replicação](/help/assets/config-dynamic.md#configuring-the-replication-agent) novamente.

   Reconfigure o Agente de replicação s7delivery.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. Selecione **[!UICONTROL Testar Conexão]** para verificar se a configuração é válida.

#### Problema: o Agente de Publicação está usando SSL em vez de OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

Esse problema provavelmente é causado por um hot fix ou um pacote de recursos que não foi instalado corretamente ou substituiu as configurações.

Exemplo de log replicado:

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

1. Adicionar esta configuração ao agente de replicação (Booleano com valor definido como **[!UICONTROL True]**):

   `enableOauth=true`

1. Próximo ao canto superior esquerdo da página, selecione **[!UICONTROL Salvar tudo]**.

### Testar sua configuração {#testing-your-configuration}

A Adobe recomenda executar um teste completo da configuração.

Certifique-se de já ter feito o seguinte antes de iniciar este teste:

* Predefinições de imagem adicionadas.
* Configure **[!UICONTROL Configuração do Dynamic Media (Pré 6.3)]** no Cloud Services. A URL do Serviço de Imagem é necessária para este teste

**Para testar sua configuração:**

1. Fazer upload de um ativo de imagem. (No Assets, navegue até **[!UICONTROL Criar]** > **[!UICONTROL Arquivos]** e selecione o arquivo.)
1. Aguarde a conclusão do fluxo de trabalho.
1. Publique o ativo de imagem. (Selecione o ativo e selecione **[!UICONTROL Publicação rápida]**.)
1. Navegue até as representações dessa imagem, abrindo a imagem e tocando em **[!UICONTROL Representações]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. Selecione qualquer representação dinâmica.
1. Para obter a URL para este ativo, selecione **[!UICONTROL URL]**.
1. Navegue até o URL selecionado e verifique se a imagem se comporta conforme esperado.

Outra maneira de testar se seus ativos foram entregues é anexar req=exists ao seu URL.

## Configurar os serviços em nuvem do Dynamic Media {#configuring-dynamic-media-cloud-services}

O Dynamic Media Cloud Service é compatível com publicação e entrega híbridas de imagens e vídeo, análise de vídeo e codificação de vídeo, entre outras coisas.

Como parte da configuração, você deve inserir uma ID de registro, um URL de serviço de vídeo, um URL de serviço de imagem, um URL de serviço de replicação e configurar a autenticação. Essas informações foram enviadas por email para você como parte do processo de provisionamento de conta. Se você não recebeu essas informações, entre em contato com o administrador da Adobe Experience Manager ou com o Suporte ao cliente da Adobe para obter as informações.

>[!NOTE]
>
Antes de configurar o Dynamic Media Cloud Services, certifique-se de configurar a instância de publicação. Você também deve ter a replicação configurada antes de configurar o Dynamic Media Cloud Services.

**Para configurar os Serviços de Nuvem do Dynamic Media:**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Configuração do Dynamic Media (Pré-6.3)]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]** e, em seguida, **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar configuração do Dynamic Media]**, no campo Título, digite um título.
1. Se estiver configurando o Dynamic Media para vídeo,

   * No campo **[!UICONTROL ID de Registro]**, digite sua ID de registro.
   * No campo **[!UICONTROL URL do Serviço de Vídeo]**, digite a URL do serviço de vídeo para o Gateway do Dynamic Media.

1. Se você estiver configurando o Dynamic Media para geração de imagens, no campo **[!UICONTROL URL do Serviço de Imagem]**, digite a URL do serviço de imagem para o Gateway do Dynamic Media.
1. Selecione **[!UICONTROL Salvar]** para retornar à página Navegador de Configuração do Dynamic Media.
1. Para acessar o console de navegação global, selecione o logotipo do Experience Manager.

## Configurar relatórios de vídeo {#configuring-video-reporting}

Você pode configurar relatórios de vídeo em várias instalações do Experience Manager usando o Dynamic Media Hybrid.

**Quando usar:** No momento em que você define a Configuração do Dynamic Media (Pré 6.3), vários recursos são iniciados, incluindo relatórios de vídeo. A configuração cria um conjunto de relatórios em uma empresa regional do Analytics. Se você configurar vários nós de Autor, criará um conjunto de relatórios separado para cada um. Como resultado, os dados de relatórios são inconsistentes entre as instalações. Além disso, se cada nó Autor se referir ao mesmo servidor de publicação híbrido, a última instalação do Autor alterará o conjunto de relatórios de destino para todos os relatórios de vídeo. Esse problema sobrecarrega o sistema Analytics com muitos conjuntos de relatórios.

**Introdução:** configure relatórios de vídeo concluindo as três tarefas a seguir.

1. Crie um pacote de predefinição do Video Analytics após definir a Configuração do Dynamic Media (Pré 6.3) no primeiro nó Autor. Essa tarefa inicial é importante porque permite que uma nova configuração continue usando o mesmo conjunto de relatórios.
1. Instale o pacote predefinido do Video Analytics em qualquer nó ***novo*** de autor ***antes*** de configurar o Dynamic Media Configuration (Pré 6.3).
1. Verifique e depure a instalação do pacote.

### Criar um pacote de predefinição do Video Analytics após configurar o primeiro nó Autor {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

Ao concluir essa tarefa, você terá um arquivo de pacote que contém as predefinições do Video Analytics. Essas predefinições contêm um conjunto de relatórios, o servidor de rastreamento, o namespace de rastreamento e a ID da organização da Experience Cloud, se disponível.

1. Se ainda não tiver feito isso, defina a Configuração do Dynamic Media (Pré 6.3).
1. (Opcional) Visualize e copie a ID do conjunto de relatórios (você deve ter acesso ao JCR). Embora não seja necessário ter a ID do conjunto de relatórios, a validação facilita.
1. Criar um pacote usando o Gerenciador de pacotes.
1. Edite o pacote para incluir um filtro.

   No Experience Manager: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. Crie o pacote.
1. Baixe ou compartilhe o pacote de predefinição do Video Analytics para que ele possa ser compartilhado com os novos nós de autor subsequentes.

### Instale o pacote de predefinição do Video Analytics antes de configurar mais nós de autor {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Conclua esta tarefa ***antes*** de configurar o Dynamic Media Configuration (Pré 6.3). Se isso não for feito, haverá a criação de outro conjunto de relatórios não utilizado. Além disso, mesmo que os relatórios de vídeo continuem a funcionar corretamente, a coleta de dados não é otimizada.

Verifique se o pacote de predefinição do Video Analytics do primeiro nó Autor está acessível no novo nó Autor.

1. Carregue o pacote de predefinição do Video Analytics criado anteriormente no Gerenciador de pacotes.
1. Instale o pacote de predefinição do Video Analytics.
1. Configurar O Dynamic Media (Pré 6.3).

### Verificar e depurar a instalação do pacote {#verifying-and-debugging-the-package-installation}

1. Siga qualquer um destes procedimentos para verificar e, se necessário, depurar a instalação do pacote:

   * **Verifique a predefinição do Video Analytics por meio do JCR**
Para verificar a predefinição do Video Analytics por meio do JCR, é necessário ter acesso ao CRXDE Lite.

     Experience Manager - No CRXDE Lite, navegue até `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

     Como em `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

     Se você não tiver acesso ao CRXDE Lite no nó Autor, poderá verificar a predefinição por meio do Servidor de publicação.

   * **Verifique a predefinição do Video Analytics por meio do Servidor de imagens**

     É possível validar a predefinição do Video Analytics diretamente fazendo uma solicitação req=userdata do servidor de imagens.
Por exemplo, para ver a predefinição do Analytics no nó Autor, é possível fazer a seguinte solicitação:

     `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

     Para validar a predefinição nos servidores de publicação, é possível fazer uma solicitação direta semelhante ao servidor de publicação. As respostas são as mesmas nos nós Autor e Publicar. A resposta é semelhante ao seguinte:

     ```
     marketingCloudOrgId=0FC4E86B573F99CC7F000101
      reportSuite=aemaem6397618-2018-05-23
      trackingNamespace=aemvideodal
      trackingServer=aemvideodal.d2.sc.omtrdc.net
     ```

   * **Verifique a predefinição do Video Analytics por meio da ferramenta Relatório de Vídeo no Experience Manager**
Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios de Vídeo]**

     `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

     Caso veja a seguinte mensagem de erro, o conjunto de relatórios está disponível, mas não preenchido. Esse erro está correto e é desejado em uma nova instalação antes que o sistema colete dados.

   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   Para gerar dados de relatório, carregue e publique um vídeo. Use **[!UICONTROL Copiar URL]** e execute o vídeo pelo menos uma vez.

   Pode levar até 12 horas para que os dados de relatório sejam preenchidos a partir do uso do Visualizador de vídeo.

   Se houver um erro e o conjunto de relatórios não estiver definido corretamente, o alerta a seguir será exibido.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   Esse erro também será exibido se o Relatório de vídeo for executado antes da configuração dos serviços de Dynamic Media Configuration (Pré 6.3).

### Solucionar problemas de configuração de relatórios de vídeo {#troubleshooting-the-video-reporting-configuration}

* Durante a instalação, às vezes, as conexões com o servidor de API do Analytics atingem o tempo limite. A instalação repete a conexão 20 vezes, mas ainda falha. Quando essa situação ocorre, o arquivo de log registra vários erros. Pesquisar por `SiteCatalystReportService`.
* Não instalar o pacote de predefinição do Analytics primeiro pode causar a criação de um novo conjunto de relatórios.
* A atualização do Experience Manager 6.3 para o Experience Manager 6.4 ou Experience Manager 6.4.1 e, em seguida, a configuração do Dynamic Media (Pré 6.3) ainda criam um conjunto de relatórios. Este problema é conhecido e programado para ser corrigido para o Experience Manager 6.4.2.

### Sobre a predefinição do Video Analytics {#about-the-video-analytics-preset}

A predefinição do Video Analytics, às vezes conhecida simplesmente como predefinição do Analytics, é armazenada ao lado das predefinições do Visualizador no Dynamic Media. É basicamente o mesmo que uma predefinição do visualizador, mas com informações usadas para configurar os relatórios do AppMeasurement e do Video Heartbeat.

As propriedades da predefinição são as seguintes:

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (não presente nas versões mais antigas do Experience Manager)

O Experience Manager 6.4 e versões mais recentes salvam esta predefinição em `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## Replicar configurações do catálogo {#replicating-catalog-settings}

Publique suas próprias configurações padrão do catálogo como parte do processo de configuração por meio do JCR. Para replicar configurações do catálogo:

1. Em uma janela Terminal, execute o seguinte:

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. No Experience Manager, navegue até o seguinte local no CRXDE Lite (requer privilégios de administrador):

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Selecione a guia **[!UICONTROL Replicação]**.
1. Selecione **[!UICONTROL Replicar]**.

## Replicar predefinições do visualizador {#replicating-viewer-presets}

Para entregar *um ativo com uma predefinição do visualizador, você deve replicar/publicar* a predefinição do visualizador. (Todas as predefinições do visualizador devem ser ativadas *e* replicadas para obter a URL ou o código de inserção de um ativo.
Consulte [Publicar predefinições do visualizador](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) para obter mais informações.

>[!NOTE]
>
Por padrão, o sistema mostra várias representações ao selecionar **[!UICONTROL Representações]** e várias predefinições do visualizador ao selecionar **[!UICONTROL Visualizadores]** na exibição detalhada do ativo. Você pode aumentar ou diminuir o número visto. Consulte [Aumentar o número de predefinições de imagens exibidas](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Aumentar o número de predefinições do visualizador exibidas](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## Filtrar ativos para replicação {#filtering-assets-for-replication}

Em implantações de mídia não dinâmica, você replica *todos* ativos (tanto imagens quanto vídeos) do ambiente de criação do Experience Manager para o nó de publicação do Experience Manager. Esse fluxo de trabalho é necessário porque os servidores de publicação do Experience Manager também fornecem os ativos.

No entanto, nas implantações do Dynamic Media, como os ativos são entregues por meio da nuvem, não há necessidade de replicar esses mesmos ativos para os nós de publicação do Experience Manager. Esse fluxo de trabalho de &quot;publicação híbrida&quot; evita custos adicionais de armazenamento e tempos de processamento mais longos para replicar ativos. Outros conteúdos, como visualizadores do Dynamic Media, páginas do site e conteúdo estático continuam a ser veiculados a partir dos nós de publicação do Experience Manager.

Além de replicar os ativos, os seguintes não ativos também são replicados:

* Configuração de entrega do Dynamic Media: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* Predefinições de imagem: `/conf/global/settings/dam/dm/presets/macros`
* Predefinições do Visualizador: `/conf/global/settings/dam/dm/presets/viewer`

Os filtros fornecem uma maneira de *excluir* ativos da replicação para o nó de publicação do Experience Manager.

### Usar filtros de ativos padrão para replicação {#using-default-asset-filters-for-replication}

Se você usar o Dynamic Media para (1) imagens em produção *ou* (2) imagens e vídeos, poderá usar os filtros padrão fornecidos pelo Adobe como estão. Os seguintes filtros estão ativos por padrão:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filtro</strong></td>
   <td><strong>Tipo MIME</strong></td>
   <td><strong>Representações</strong></td>
  </tr>
  <tr>
   <td>Entrega de imagem do Dynamic Media</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p> </p> </td>
   <td><p>Começa com <strong>image/</strong></p> <p>Contém <strong>application/</strong> e termina com <strong>set</strong>.</p> </td>
   <td>As "imagens de filtro" prontas para uso (aplica-se a ativos de imagens únicas, incluindo imagens interativas) e "conjuntos de filtros" (aplica-se a Conjuntos de rotação, Conjuntos de imagem, Conjuntos de mídia mista e Conjuntos de carrossel) irão:
    <ul>
     <li>Incluir imagens PTIFF e Metadados para replicação (Qualquer representação que comece com <strong>cqdam</strong>).</li>
     <li>Exclua da replicação a imagem original e as representações de imagem estática.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Entrega de vídeo do Dynamic Media</td>
   <td>filter-video</td>
   <td>Começa com <strong>vídeo/</strong></td>
   <td>O "vídeo de filtro" pronto para uso irá:
    <ul>
     <li>Inclua representações de vídeo proxy, miniatura/imagem de pôster do vídeo, metadados (tanto em representações de vídeo pai quanto em representações de vídeo) para replicação (Qualquer representação que comece com <strong>cqdam</strong>).</li>
     <li>Exclua da replicação o vídeo original e as representações em miniatura estáticas.<br /> <br /> <strong>Observação:</strong> as representações de vídeo de proxy não contêm binários, mas são apenas propriedades de nó. Portanto, não há impacto no tamanho do repositório do editor.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Integração do Dynamic Media Classic (Scene7)</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p>filter-video</p> </td>
   <td><p>Começa com <strong>image/</strong></p> <p>Contém <strong>application/</strong> e termina com <strong>set</strong>.</p> <p>Começa com <strong>vídeo/</strong></p> </td>
   <td><p>Você configura o URI de transporte para apontar para o servidor de publicação do Experience Manager em vez do URL do serviço de replicação da Adobe Dynamic Media Cloud. A configuração desse filtro permite que o Dynamic Media Classic entregue ativos em vez da instância de publicação do Experience Manager.</p> <p>As "imagens de filtro", "conjuntos de filtros" e "vídeo de filtro" prontas para uso irão:</p>
    <ul>
     <li>Inclua imagem PTIFF, representações de vídeo proxy e metadados para replicação. No entanto, como eles não existem no JCR-para aqueles que executam a integração Experience Manager - Dynamic Media Classic, eles não fazem nada de fato.</li>
     <li>Exclua da replicação a imagem original, as representações de imagem estática, o vídeo original e as representações de miniatura estáticas. Em vez disso, a Dynamic Media Classic fornece ativos de imagem e vídeo.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Os filtros se aplicam aos tipos MIME e não podem ser específicos de caminho.

### Configurar filtros de ativos para implantações somente de vídeo {#setting-up-asset-filters-for-video-only-deployments}

Se você estiver usando o Dynamic Media somente para vídeo, siga estas etapas para configurar filtros de ativos para replicação:

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes no autor]**.
1. Na página Agentes na criação, selecione **[!UICONTROL Agente padrão (publicação)]**.
1. Selecione **[!UICONTROL Editar]**.
1. Na caixa de diálogo **[!UICONTROL Configurações do Agente]**, na guia **[!UICONTROL Configurações]**, marque **[!UICONTROL Habilitado]** para ativar o agente.
1. Selecione **[!UICONTROL OK]**.
1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore de pastas à esquerda, navegue até `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. Localize o **[!UICONTROL filtro-vídeo]**, clique com o botão direito nele e selecione **[!UICONTROL Copiar]**.
1. Na árvore de pastas à esquerda, navegue até `/etc/replication/agents.author/publish`
1. Localize `jcr:content`, clique com o botão direito do mouse e selecione **[!UICONTROL Colar]**.

Essas etapas configuram a instância de publicação do Experience Manager para fornecer a imagem de pôster do vídeo e os metadados de vídeo necessários para a reprodução, enquanto o próprio vídeo é entregue pelo Dynamic Media Cloud Service. O filtro também exclui da replicação as representações originais de vídeo e miniatura estática, que não são necessárias na instância de publicação.

### Configurar filtros de ativos para imagens em implantações de não produção {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

Se você estiver usando o Dynamic Media para criação de imagens em implantações de não produção, siga estas etapas para configurar filtros de ativos para replicação:

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes no autor]**.
1. Na página Agentes na criação, selecione **[!UICONTROL Agente padrão (publicação)]**.
1. Selecione **[!UICONTROL Editar]**.
1. Na caixa de diálogo **[!UICONTROL Configurações do Agente]**, na guia **[!UICONTROL Configurações]**, marque **[!UICONTROL Habilitado]** para ativar o agente.
1. Selecione **[!UICONTROL OK]**.
1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore de pastas à esquerda, navegue até `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. Localize **[!UICONTROL imagens-filtro]**, clique com o botão direito do mouse e selecione **[!UICONTROL Copiar]**.
1. Na árvore de pastas à esquerda, navegue até `/etc/replication/agents.author/publish`
1. Localize `jcr:content`, clique com o botão direito do mouse nele e vá para **[!UICONTROL Criar]** > **[!UICONTROL Criar Nó]**. Insira o nome `damRenditionFilters` do tipo `nt:unstructured`.
1. Localize `damRenditionFilters`, clique com o botão direito do mouse e selecione **[!UICONTROL Colar]**.

Essas etapas configuram a instância de publicação do Experience Manager para fornecer as imagens para seu ambiente de não produção. O filtro também exclui da replicação a imagem original e as representações estáticas, que não são necessárias na instância de publicação.

>[!NOTE]
>
Se houver vários filtros diferentes em um autor, cada agente precisará de um usuário diferente atribuído a ele. O código granite impõe o modelo de um filtro por usuário. Sempre tenha um usuário diferente para cada configuração de filtro.
>
Você está usando mais de um filtro em um servidor? Por exemplo, um filtro para publicação da replicação e um segundo filtro para s7delivery. Em caso afirmativo, você deve garantir que esses dois filtros tenham um **userId** diferente atribuído a eles no nó `jcr:content`. Veja a imagem a seguir:

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### Personalizar filtros de ativos para replicação (opcional) {#customizing-asset-filters-for-replication}

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore de pastas à esquerda, navegue até `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` para examinar os filtros.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. Para definir o Tipo MIME para o filtro, você pode localizar o Tipo MIME da seguinte maneira:

   No painel à esquerda, expanda `content > dam > <locate_your_asset> >  jcr:content > metadata` e, na tabela, localize `dc:format`.

   O gráfico a seguir é um exemplo do caminho de um ativo para `dc:format`.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   Observe que `dc:format` para o ativo `Fiji Red.jpg` é `image/jpeg`.

   Para que esse filtro seja aplicado a todas as imagens, independentemente do formato, defina o valor como `image/*`, onde `*` é uma expressão regular aplicada a todas as imagens de qualquer formato.

   Para que o filtro seja aplicado apenas a imagens do tipo JPEG, digite um valor de `image/jpeg`.

1. Defina quais representações você deseja incluir ou excluir da replicação.

   Os caracteres que podem ser usados para filtrar para replicação incluem:

   | Caractere a ser usado | Como ele filtra ativos para replicação |
   | --- | --- |
   | `*` | Caracteres curingas |
   | `+` | Inclui ativos para replicação |
   | `-` | Exclui ativos da replicação |

   Vá até `content/dam/<locate your asset>/jcr:content/renditions`.

   O gráfico a seguir é um exemplo das representações de um ativo.

   ![chlimage_1-513](assets/chlimage_1-4.png)

   Usando o exemplo acima, se você deseja apenas replicar o PTIFF (Pyramid TIFF), digite `+cqdam,*`, que inclui todas as representações que começam com `cqdam`. No exemplo, essa representação é `cqdam.pyramid.tiff`.

   Se você quiser replicar apenas o original, digite `+original`.

## Definição das configurações do Servidor de imagens do Dynamic Media {#configuring-dynamic-media-image-server-settings}

A configuração do Dynamic Media Image Server envolve a edição do pacote Adobe CQ Scene7 ImageServer e do pacote Adobe CQ Scene7 PlatformServer.

>[!NOTE]
>
O Dynamic Media funciona imediatamente [depois de ser habilitado](#enabling-dynamic-media). No entanto, você pode optar por ajustar a instalação configurando o Servidor de imagens do Dynamic Media para atender a determinadas especificações ou requisitos.

**Pré-requisito** - *Antes* de configurar o Servidor de Imagens do Dynamic Media, certifique-se de que sua VM do Windows® inclua uma instalação das Bibliotecas do Microsoft® Visual C++. As bibliotecas são necessárias para executar o Servidor de imagens do Dynamic Media. Você pode [baixar o Pacote Redistribuível do Microsoft® Visual C++ 2010 (x64) aqui](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

Para definir as configurações do Servidor de imagens do Dynamic Media:

1. No canto superior esquerdo do Experience Manager, selecione **[!UICONTROL Adobe Experience Manager]** para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Na página Configuração do Console da Web do Adobe Experience Manager, vá para **[!UICONTROL OSGi]** > **[!UICONTROL Configuração]** para listar todos os pacotes que estão sendo executados no Experience Manager.

   Os servidores de entrega do Dynamic Media são encontrados com os seguintes nomes na lista:

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. Na lista de pacotes, à direita de Adobe CQ Scene7 ImageServer, selecione o ícone **[!UICONTROL Editar]**.
1. Na caixa de diálogo Adobe CQ Scene7 ImageServer, defina os seguintes valores de configuração:

   >[!NOTE]
   >
   Normalmente, não há necessidade de alterar os valores padrão. No entanto, se você alterar os valores padrão, deverá reiniciar o pacote para que as alterações entrem em vigor.

   | Propriedade | Valor padrão | Descrição |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | Número da porta a ser usada para comunicação com o processo ImageServer. Por padrão, a porta livre é detectada automaticamente. |
   | `AllowRemoteAccess.name` | *`empty`* | Permitir ou não o acesso remoto ao processo ImageServer. Se false, o servidor de imagem ouvirá somente no localhost.<br> As configurações de Externalizador Padrão que apontam para o host local devem especificar o domínio ou endereço IP real da instância da VM específica. O motivo é porque o host local aponta para o sistema pai da VM.<br>Os domínios ou endereços IP da VM devem ter uma entrada de arquivo de host para que ela possa se resolver. |
   | `MaxRenderRgnPixels` | 16 MP | Tamanho máximo em megapixels renderizado. |
   | `MaxMessageSize` | 16 MB | Tamanho máximo da mensagem em megabytes que é entregue. |
   | `RandomAccessUrlTimeout` | 20 | Valor de tempo limite para o tempo em segundos que o Servidor de imagens aguarda para que o JCR responda a uma solicitação de bloco de intervalo. |
   | `WorkerThreads` | 10 | Número de threads de trabalho. |

1. Selecione **[!UICONTROL Salvar]**.
1. Na lista de pacotes, à direita de Adobe CQ Scene7 PlatformServer, selecione o ícone **[!UICONTROL Editar]**.
1. Na caixa de diálogo Adobe CQ Scene7 PlatformServer, defina as seguintes opções de valor padrão:

   >[!NOTE]
   >
   O Dynamic Media Image Server usa seu próprio cache de disco para armazenar em cache as respostas. O cache HTTP do Experience Manager e o Dispatcher não podem ser usados para armazenar em cache respostas do Servidor de imagens do Dynamic Media.

   | Propriedade | Valor padrão | Descrição |
   |---|---|---|
   | Cache habilitado | Marcado | Se o cache de resposta está habilitado |
   | Raízes de cache | cache | Um ou mais caminhos para as pastas do cache de resposta. Os caminhos relativos são resolvidos em relação à pasta interna do pacote s7imaging. |
   | Tamanho máximo do cache | 200000000 | Tamanho máximo do cache de resposta em bytes. |
   | Máximo de Entradas do Cache | 100000 | Número máximo de entradas permitidas no cache. |

### Configurações padrão do manifesto {#default-manifest-settings}

O manifesto padrão permite configurar os padrões usados para gerar as respostas do Dynamic Media Delivery. Você pode ajustar a qualidade (qualidade, resolução, modo de reamostragem do JPEG), armazenar em cache (expiração) e impedir a renderização de imagens muito grandes (defaultpix, defaultthumbpix, maxpix).

O local da configuração de manifesto padrão é obtido do valor padrão **[!UICONTROL Raiz de catálogo]** do pacote **[!UICONTROL Adobe CQ Scene7 PlatformServer]**. Por padrão, este valor está no seguinte caminho em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**

`/conf/global/settings/dam/dm/imageserver/`

![Configurar o Servidor de Imagens no CRXDE Lite](assets/configimageservercrxdelite.png)

É possível alterar os valores das propriedades, conforme descrito na tabela abaixo, inserindo novos valores.

Quando terminar de alterar o manifesto padrão, no canto superior esquerdo da página, selecione **[!UICONTROL Salvar tudo]**.

Certifique-se de selecionar a guia **[!UICONTROL Controle de Acesso]** (à direita da guia Propriedades) e definir os privilégios de controle de acesso como `jcr:read` para todos os usuários e usuários de replicação de mídia dinâmica.

![Configurar o Servidor de Imagens no CRXDE Lite e definir a guia Controle de Acesso](assets/configimageservercrxdeliteaccesscontroltab.png)

Configurações da Tabela de manifestos e seus valores padrão:

| Propriedade | Valor padrão | Descrição |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | Cor de fundo padrão. O valor de RGB usado para preencher qualquer área de uma imagem de resposta que não contenha dados reais da imagem. Consulte também [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api) na API de disponibilização de imagens. |
| `defaultpix` | `300,300` | Tamanho de exibição padrão. As restrições do servidor respondem que as imagens não são maiores que essa largura e altura se a solicitação não especificar explicitamente o tamanho da exibição usando wid=, hei= ou scl=.<br>Especificado como dois números inteiros, 0 ou maiores, separados por vírgula. Largura e altura em pixels. Um ou ambos os valores podem ser definidos como 0 para mantê-los sem restrições. Não se aplica a solicitações aninhadas/incorporadas.<br>Consulte também [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api) na API do Servidor de imagens.<br>No entanto, geralmente você usa uma predefinição do visualizador ou uma predefinição de imagem para entregar o ativo. O Defaultpix se aplica somente a um ativo que não está usando uma predefinição do visualizador ou de imagem. |
| `defaultthumbpix` | `100,100` | Tamanho padrão da miniatura. Usado em vez de attribute::DefaultPix para solicitações de miniatura (`req=tmb`).<br>As restrições do servidor respondem que as imagens não são maiores que essa largura e altura. Esta ação será verdadeira se uma solicitação de miniatura (`req=tmb`) não especificar explicitamente o tamanho e não especificar explicitamente o tamanho da exibição usando `wid=`, `hei=` ou `scl=`.<br>Especificado como dois números inteiros, 0 ou maiores, separados por vírgula. Largura e altura em pixels. Um ou ambos os valores podem ser definidos como 0 para mantê-los sem restrições.<br>Não se aplica a solicitações aninhadas/inseridas.<br>Consulte também [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api) na API do Servidor de Imagens. |
| `expiration` | `36000000` | Tempo de vida padrão do cache do cliente. Fornece um intervalo de expiração padrão caso um determinado registro de catálogo não contenha um valor catalog::Expiration válido.<br>Número real, 0 ou maior. Número de milissegundos até a expiração desde que os dados de resposta foram gerados. Defina como 0 para sempre expirar a imagem de resposta imediatamente, o que desativa efetivamente o cache do cliente. Por padrão, esse valor é definido como 10 horas, o que significa que, se uma nova imagem for publicada, levará 10 horas para que a imagem antiga saia do cache do usuário. Entre em contato com o Suporte ao cliente se precisar que o cache seja limpo antes.<br>Consulte também [Expiração](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) na API do Servidor de imagens. |
| `jpegquality` | `80` | Atributos de codificação padrão do JPEG. Especifica os atributos padrão para imagens de resposta do JPEG.<br>Número inteiro e sinalizador, separados por vírgula. O primeiro valor está no intervalo 1-100 e define a qualidade. O segundo valor pode ser 0 para comportamento normal ou 1 para desativar a redução de resolução de cromaticidade de RGB empregada pelos codificadores de JPEG.<br>Consulte também [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api) na API de disponibilização de imagens. |
| `maxpix` | `2000,2000` | Limite de tamanho da imagem de resposta. Largura e altura máximas da imagem de resposta retornadas ao cliente.<br>O servidor retornará um erro se uma solicitação causar uma imagem de resposta cuja largura ou altura for maior que attribute::MaxPix.<br>Consulte também [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html#image-serving-api) na API do Servidor de imagens. |
| `resmode` | `SHARP2` | Modo de reamostragem padrão. Especifica os atributos padrão de reamostragem e interpolação a serem usados para dimensionar dados de imagem.<br>Usado quando `resMode=` não é especificado em uma solicitação.<br>Os valores permitidos incluem `BILIN`, `BICUB` ou `SHARP2`.<br>Enumeração. Defina como 2 para `bilin`, 3 para `bicub` ou 4 para o modo de interpolação `sharp2`. Use `sharp2` para obter melhores resultados.<br>Consulte também [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api) na API do Servidor de imagens. |
| `resolution` | `72` | Resolução de objeto padrão. Fornece uma resolução de objeto padrão caso um determinado registro de catálogo não contenha um valor catalog::Resolution válido.<br>Número real, maior que 0. Normalmente expresso em pixels por polegada, mas também pode estar em outras unidades, como pixels por metro.<br>Consulte também [Resolução](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api) na API de disponibilização de imagens. |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | Esses valores representam um instantâneo do tempo de reprodução de vídeo e são passados para [encoding.com](https://www.encoding.com/). Consulte [Sobre a miniatura do vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) para obter mais informações. |

## Configuração do gerenciamento de cores do Dynamic Media {#configuring-dynamic-media-color-management}

O gerenciamento de cores do Dynamic Media permite corrigir as cores dos ativos para visualização.

Com a correção de cores, os ativos assimilados mantêm o espaço de cores (RGB, CMYK, Cinza) e o perfil de cores incorporado na representação TIFF da pirâmide gerada. Quando você solicita uma representação dinâmica, a cor da imagem é corrigida no espaço de cores de destino. Você define o perfil de cor de saída nas configurações de publicação do Dynamic Media no JCR.

O gerenciamento de cores do Adobe usa perfis ICC (International Color Consortium), um formato definido pelo ICC.

É possível configurar o gerenciamento de cores do Dynamic Media e configurar as predefinições de imagem usando a saída CMYK, RGB ou cinza. Consulte [Configurando Predefinições De Imagem](/help/assets/managing-image-presets.md).

Casos de uso avançados podem usar um modificador de configuração manual `icc=` para selecionar explicitamente um perfil de cor de saída:

* `icc` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
>
O conjunto padrão de perfis de cores do Adobe só estará disponível se você tiver o [Feature Pack 12445 da Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) instalado. Todos os pacotes de recursos e service packs estão disponíveis em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). O Pacote de recursos 12445 fornece perfis de cores do Adobe.


### Instalação do Feature Pack 12445 {#installing-feature-pack}

Para usar os recursos de gerenciamento de cores do Dynamic Media, instale o pacote de recursos 12445.

**Para instalar o pacote de recursos 12445:**

1. Navegue até [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html) e baixe `cq-6.3.0-featurepack-12445`.

   Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre como usar pacotes em [!DNL Adobe Experience Manager].

1. Instale o pacote de recursos.

### Configuração dos perfis de cores padrão {#configuring-the-default-color-profiles}

Após instalar o pacote de recursos, configure os perfis de cor padrão apropriados para ativar a correção de cores ao solicitar dados de imagem RGB ou CMYK.

**Para configurar os perfis de cores padrão:**

1. Em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**, navegue até `/conf/global/settings/dam/dm/imageserver/jcr:content`, que contém os Perfis Adobe Color padrão.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. Adicione uma propriedade de correção de cor rolando até a parte inferior da guia **[!UICONTROL Propriedades]**. Insira manualmente o nome, o tipo e o valor da propriedade, que são descritos nas tabelas a seguir. Depois de inserir os valores, selecione **[!UICONTROL Adicionar]** e depois **[!UICONTROL Salvar tudo]** para salvar seus valores.

   As propriedades de correção de cores são descritas na tabela **Propriedades de Correções de Cor**. Os valores que você pode atribuir às propriedades de correção de cores estão na tabela **Perfil de Cores**.

   Por exemplo, em **[!UICONTROL Nome]**, adicione `iccprofilecmyk`, selecione **[!UICONTROL Tipo]** `String` e adicione `WebCoated` como um **[!UICONTROL Valor]**. Em seguida, selecione **[!UICONTROL Adicionar]** e **[!UICONTROL Salvar tudo]** para salvar seus valores.

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **Tabela de Propriedades de Correção de Cor**

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
   <td>String</td>
   <td>&lt;vazio&gt;</td>
   <td>Nome do perfil de cores padrão do RGB.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">iccprofilecmyk</a></td>
   <td>String</td>
   <td>&lt;vazio&gt;</td>
   <td>Nome do perfil de cores CMYK padrão.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">iccprofilegray</a></td>
   <td>String</td>
   <td>&lt;vazio&gt;</td>
   <td>Nome do perfil de cor cinza padrão.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofilesrcrgb</a></td>
   <td>String</td>
   <td>&lt;vazio&gt;</td>
   <td>Nome do perfil de cores padrão do RGB usado para imagens RGB que não têm um perfil de cores incorporado</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrcmyk</a></td>
   <td>String</td>
   <td>&lt;vazio&gt;</td>
   <td>Nome do perfil de cores CMYK padrão usado para imagens CMYK que não têm um perfil de cores incorporado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>String</td>
   <td>&lt;vazio&gt;</td>
   <td>Nome do perfil de cores Cinza padrão usado para imagens CMYK que não têm um perfil de cores incorporado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompression</a></td>
   <td>Booleano</td>
   <td>Verdadeiro</td>
   <td>Especifica se a compensação do ponto preto é feita durante a correção de cores. A Adobe recomenda que essa configuração esteja ativada.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">iccdither</a></td>
   <td>Booleano</td>
   <td>Falso</td>
   <td>Especifica se o pontilhamento é feito durante a correção de cores.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrederintent</a></td>
   <td>String</td>
   <td>relativo</td>
   <td><p>Especifica a intenção de renderização. Os valores aceitáveis são: <strong>perceptivo, relativo, saturação, absoluto. </strong><i></i>A Adobe recomenda <strong>o </strong><i></i>relativo como padrão.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Os nomes de propriedades fazem distinção entre maiúsculas e minúsculas e devem ser todos em minúsculas.

**Tabela de Perfil de Cores**

Os seguintes perfis de cores estão instalados:

<table>
 <tbody>
  <tr>
   <th><p>Nome</p> </th>
   <th><p>Espaço de cores</p> </th>
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
   <td>Apple RGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>RGB CIE</td>
  </tr>
  <tr>
   <td>FograRevestida27</td>
   <td>CMYK</td>
   <td>FOGRA27 revestida (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>FograRevestida39</td>
   <td>CMYK</td>
   <td>FOGRA39 revestida (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>GraCol revestido</td>
   <td>CMYK</td>
   <td>GRACoL 2006 revestido (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatch RGB</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>Europa ISO Revestido FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Revestimento na escala do euro v2</td>
  </tr>
  <tr>
   <td>EuroscaleNão revestido</td>
   <td>CMYK</td>
   <td>Escala do euro não revestida v2</td>
  </tr>
  <tr>
   <td>JapãoRevestidoPorCor</td>
   <td>CMYK</td>
   <td>Japão Colorido 2001 Revestido</td>
  </tr>
  <tr>
   <td>JapãoColorNewspaper</td>
   <td>CMYK</td>
   <td>Jornal Japan Color 2002</td>
  </tr>
  <tr>
   <td>JapãoCorNãoRevestida</td>
   <td>CMYK</td>
   <td>Japão Colorido 2001 Sem Revestimento</td>
  </tr>
  <tr>
   <td>JapãoCorRevestidoWeb</td>
   <td>CMYK</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapãoRevestidoWeb</td>
   <td>CMYK</td>
   <td>Revestimento Para Web No Japão (Anúncio)</td>
  </tr>
  <tr>
   <td>Papel de jornalSNAP2007</td>
   <td>CMYK</td>
   <td>Papel de jornal dos EUA (SNAP 2007)</td>
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
   <td>ProPhoto RGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>Photoshop 4 Padrão CMYK</td>
  </tr>
  <tr>
   <td>PS5Padrão</td>
   <td>CMYK</td>
   <td>CMYK padrão do Photoshop 5</td>
  </tr>
  <tr>
   <td>RevestidoFolheado</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>Não revestidaFolha</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed sem revestimento v2</td>
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
   <td>Fogra29 não revestida</td>
   <td>CMYK</td>
   <td>FOGRA29 não revestida (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>Revestido pela Web</td>
   <td>CMYK</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>FOGRA28 revestida com revestimento web (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Papel revestido para web SWOP 2006 Grade 3</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Papel revestido para web SWOP 2006 Grade 5</td>
  </tr>
  <tr>
   <td>WebNão revestida</td>
   <td>CMYK</td>
   <td>Web sem revestimento dos EUA v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RGB</td>
   <td>RGB de gamut amplo</td>
  </tr>
 </tbody>
</table>

1. Selecione **[!UICONTROL Salvar tudo]**.

Por exemplo, você pode definir o **[!UICONTROL iccprofilergb]** como `sRGB` e o **[!UICONTROL iccprofilecmyk]** como **[!UICONTROL WebCoated]**.

Isso faria o seguinte:

* Ativa a correção de cores para imagens RGB e CMYK.
* Pressupõe-se que as imagens do RGB que não têm um perfil de cores estejam no espaço de cores *sRGB*.
* Supõe-se que as imagens CMYK que não têm um perfil de cores estejam no espaço de cores *WebCoated*.
* Representações dinâmicas que retornam a saída do RGB, retornam no espaço de cores *sRGB *.
* Representações dinâmicas que retornam saída CMYK, retornam no espaço de cores *WebCoated*.

## Entrega do Assets {#delivering-assets}

Após concluir todas as tarefas acima, os ativos do Dynamic Media ativados são fornecidos pelo Serviço de imagem ou vídeo. No Experience Manager, esse recurso é exibido em uma **[!UICONTROL Copiar URL da Imagem]**, **[!UICONTROL Copiar URL do Visualizador]**, **[!UICONTROL Incorporar Código do Visualizador]** e no WCM.

Consulte [Delivery de Dynamic Media Assets](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>Quando você...</strong></td>
   <td><strong>Resultado</strong></td>
  </tr>
  <tr>
   <td>Copiar um URL de imagem</td>
   <td><p>A caixa de diálogo Copiar URL exibe um URL semelhante ao seguinte (o URL é somente para fins de demonstração):</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>Onde <code>IMAGESERVICEPUBLISHNODE</code> refere-se à URL do Serviço de Imagem.</p> <p>Consulte também <a href="/help/assets/delivering-dynamic-media-assets.md">Delivery de Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar um URL do visualizador</td>
   <td><p>A caixa de diálogo Copiar URL exibe um URL semelhante ao seguinte (o URL é somente para fins de demonstração):</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>Onde <code>PUBLISHNODE</code> refere-se ao nó de publicação normal do Experience Manager e <code>IMAGESERVICEPUBLISHNODE</code> refere-se à URL do Serviço de Imagem.</p> <p>Consulte também <a href="/help/assets/delivering-dynamic-media-assets.md">Delivery de Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar um código incorporado do visualizador</td>
   <td><p>A caixa de diálogo Copiar código incorporado exibe um trecho de código semelhante ao seguinte (o exemplo de código é somente para fins de demonstração):</p> <p><code class="code">&lt;style type="text/css"&gt;
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
       &lt;/script&gt;</code></p> <p>Onde <code>PUBLISHNODE</code> refere-se ao nó de publicação normal do Experience Manager e <code>IMAGESERVICEPUBLISHNODE</code> refere-se à URL do Serviço de Imagem.</p> <p>Consulte também <a href="/help/assets/delivering-dynamic-media-assets.md">Delivery de Dynamic Media Assets</a>.</p> </td>
  </tr>
 </tbody>
</table>

### WCM Dynamic Media e componentes de mídia interativa {#wcm-dynamic-media-and-interactive-media-components}

As páginas WCM que fazem referência aos componentes do Dynamic Media e do Interative Media fazem referência ao serviço de entrega.
