---
title: Replicação
seo-title: Replicação
description: Saiba como configurar e monitorar agentes de replicação no AEM.
seo-description: Saiba como configurar e monitorar agentes de replicação no AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
translation-type: tm+mt
source-git-commit: 480e1f62e34783295133d10451ec409cf3a8bb0b
workflow-type: tm+mt
source-wordcount: '3661'
ht-degree: 2%

---


# Replicação{#replication}

Os agentes de replicação são fundamentais para a Adobe Experience Manager (AEM) como mecanismo usado para:

* [Publique (ative)](/help/sites-authoring/publishing-pages.md#activatingcontent) conteúdo de um autor em um ambiente de publicação.
* Limpe explicitamente o conteúdo do cache do Dispatcher.
* Retorna a entrada do usuário (por exemplo, a entrada de formulário) do ambiente publish para o ambiente author (sob controle do ambiente author).

As solicitações são [enfileiradas](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) ao agente apropriado para processamento.

>[!NOTE]
>
>Os dados do usuário (usuários, grupos de usuários e perfis de usuários) não são replicados entre as instâncias de autor e publicação.
>
>Para várias instâncias de publicação, os dados do usuário são distribuídos Sling quando a Sincronização [](/help/sites-administering/sync.md) do usuário está ativada.

## Replicação de autor para publicação {#replicating-from-author-to-publish}

A replicação, para uma instância ou despachante de publicação, ocorre em várias etapas:

* o autor solicita que certos conteúdos sejam publicados (ativados); isso pode ser iniciado por uma solicitação manual ou por acionadores automáticos que foram pré-configurados.
* A solicitação é transmitida ao agente de replicação padrão adequado; um ambiente pode ter vários agentes padrão que sempre serão selecionados para essas ações.
* o agente de replicação &quot;agrupa&quot; o conteúdo e o coloca na fila de replicação.
* na guia Sites, o indicador [de status](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) colorido é definido para as páginas individuais.
* O conteúdo é retirado da fila e transportado para o ambiente de publicação usando o protocolo configurado; normalmente, isso é HTTP.
* um servlet no ambiente de publicação recebe a solicitação e publica o conteúdo recebido; o servlet padrão é `https://localhost:4503/bin/receive`.

* vários ambientes de autor e publicação podem ser configurados.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replicação de Publicar para Autor {#replicating-from-publish-to-author}

Alguns recursos permitem que os usuários digitem dados em uma instância de publicação.

Em alguns casos, um tipo de replicação conhecido como replicação reversa é necessário para retornar esses dados ao ambiente do autor de onde são redistribuídos para outros ambientes de publicação. Devido a considerações de segurança, qualquer tráfego da publicação para o ambiente do autor deve ser rigorosamente controlado.

A replicação reversa usa um agente no ambiente de publicação que faz referência ao ambiente do autor. Esse agente coloca os dados em uma caixa de saída. Essa caixa de saída corresponde aos ouvintes de replicação no ambiente do autor. Os ouvintes pesquisam as caixas de saída para coletar os dados digitados e depois distribuí-los conforme necessário. Isso garante que o ambiente do autor controle todo o tráfego.

Em outros casos, como nos recursos de Comunidades (por exemplo, fóruns, blogs, comentários e revisões), a quantidade de conteúdo gerado pelo usuário (UGC) que está sendo inserida no ambiente de publicação é difícil de sincronizar com eficiência entre instâncias AEM usando replicação.

AEM [Communities](/help/communities/overview.md) nunca usa replicação para UGC. Em vez disso, a implantação para Comunidades requer uma loja comum para o UGC (consulte o Armazenamento [de conteúdo da](/help/communities/working-with-srp.md)comunidade).

### Replicação - pronta para uso {#replication-out-of-the-box}

O site de varejo incluído em uma instalação padrão de AEM pode ser usado para ilustrar a replicação.

Para seguir este exemplo e usar os agentes de replicação padrão, é necessário [instalar AEM](/help/sites-deploying/deploy.md) com:

* o ambiente author on port `4502`
* o ambiente publish na porta `4503`

>[!NOTE]
>
>Ativado por padrão :
>
>* Agentes do autor : Agente padrão (publicar)
>
>
Efetivamente desativado por padrão (a partir do AEM 6.1):
>
>* Agentes do autor : Agente de Replicação Inversa (publish_back)
>* Agentes ao publicar : Replicação reversa (caixa de saída)

>
>
Para verificar o status do agente ou da fila, use o console **Ferramentas** .
>Consulte [Monitoramento dos agentes](#monitoring-your-replication-agents)de replicação.

#### Replicação (Autor para publicar) {#replication-author-to-publish}

1. Navegue até a página de suporte no ambiente do autor.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Edite a página para adicionar um texto novo.
1. **Ativar a Página** para publicar as alterações.
1. Abra a página de suporte no ambiente de publicação:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Agora você pode ver as alterações inseridas no autor.

Essa replicação é acionada a partir do ambiente do autor pelo:

* **Agente padrão (publicar)**Esse agente replica o conteúdo para a instância de publicação padrão.
Os detalhes (configuração e registros) podem ser acessados no console Ferramentas do ambiente do autor; ou:

   `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agentes de Replicação - prontos para uso {#replication-agents-out-of-the-box}

Os seguintes agentes estão disponíveis em uma instalação padrão AEM:

* [Agente](#replication-author-to-publish)padrão usado para replicar do autor para publicar.

* Dispatcher FlashÉ usado para gerenciar o cache do Dispatcher. Consulte [Invalidando o Cache do Dispatcher do Ambiente](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) de criação e [Invalidando o Cache do Dispatcher de uma Instância](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) de publicação para obter mais informações.

* [Replicação](#reverse-replication-publish-to-author)inversa usada para replicação de publicação para autor. A replicação reversa não é usada para recursos das Comunidades, como fóruns, blogs e comentários. Ela é efetivamente desativada, pois a caixa de saída não está ativada. O uso da replicação reversa exigiria configuração personalizada.

* Agente estáticoÉ um &quot;Agente que armazena uma representação estática de um nó no sistema de arquivos.&quot;
Por exemplo, com as configurações padrão, as páginas de conteúdo e os ativos dam são armazenados em `/tmp`, como HTML ou o formato de ativo apropriado. Consulte as guias `Settings` e `Rules` para obter a configuração.
Isso foi solicitado para que, quando a página for solicitada diretamente do servidor de aplicativos, o conteúdo possa ser visualizado. Este é um agente especializado e (provavelmente) não será necessário para a maioria das instâncias.

## Agentes de Replicação - Parâmetros de Configuração {#replication-agents-configuration-parameters}

Ao configurar um agente de replicação a partir do console Ferramentas, quatro guias estão disponíveis na caixa de diálogo:

### Configurações {#settings}

* **Nome**

   Um nome exclusivo para o agente de replicação.

* **Descrição**

   Uma descrição da finalidade que este agente de replicação servirá.

* **Ativado**

   Indica se o agente de replicação está ativado no momento.

   Quando o agente é **ativado** , a fila será mostrada como:

   * **Ativo** quando os itens estão sendo processados.
   * **Ocioso** quando a fila está vazia.
   * **Bloqueado** quando os itens estão na fila, mas não podem ser processados; por exemplo, quando a fila de recebimento está desativada.

* **Tipo de serialização**

   O tipo de serialização:

   * **Padrão**: Defina se o agente deve ser selecionado automaticamente.
   * **Dispatcher Flush**: Selecione essa opção se o agente for usado para liberar o cache do dispatcher.

* **Tentar novamente o atraso**

   O atraso (tempo de espera em milissegundos) entre duas tentativas, caso algum problema seja encontrado.

   Padrão: `60000`

* **ID de usuário agente**

   Dependendo do ambiente, o agente usará essa conta de usuário para:

   * coletar e empacotar o conteúdo do ambiente do autor
   * criar e gravar o conteúdo no ambiente de publicação

   Deixe este campo vazio para usar a conta de usuário do sistema (a conta definida no sling como o usuário administrador; por padrão, isso é `admin`).

   >[!CAUTION]
   >
   >Para um agente no ambiente do autor, esta conta *deve* ter acesso de leitura a todos os caminhos que você deseja que sejam replicados.

   >[!CAUTION]
   >
   >Para um agente no ambiente de publicação, essa conta *deve* ter o acesso de criação/gravação necessário para replicar o conteúdo.

   >[!NOTE]
   >
   >Isso pode ser usado como um mecanismo para selecionar conteúdo específico para replicação.

* **Nível de registro**

   Especifica o nível de detalhes a ser usado para mensagens de log.

   * `Error`: somente os erros serão registrados
   * `Info`: serão registrados erros, avisos e outras mensagens informativas
   * `Debug`: um alto nível de detalhes será usado nas mensagens, principalmente para fins de depuração

   Padrão: `Info`

* **Use para replicação reversa**

   Indica se este agente será usado para replicação reversa; retorna a entrada do usuário do ambiente de publicação para o autor.

* **Atualização do alias**

   A seleção dessa opção ativa solicitações de invalidação de caminho de alias ou vanity para o Dispatcher. Além disso, consulte [Configuração de um Dispatcher Flush Agent](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transporte {#transport}

* **URI**

   Isso especifica o servlet de recebimento no local do público alvo. Em particular, você pode especificar o nome do host (ou alias) e o caminho do contexto para a instância do público alvo aqui.

   Por exemplo:

   * Um Agente Padrão pode replicar para `https://localhost:4503/bin/receive`
   * Um agente do Dispatcher Flush pode replicar para `https://localhost:8000/dispatcher/invalidate.cache`

   O protocolo especificado aqui (HTTP ou HTTPS) determinará o método de transporte.

   Para os agentes do Dispatcher Flush, a propriedade URI será usada somente se você usar entradas de host virtual baseadas em caminho para diferenciar entre farm, você usará esse campo para público alvo do farm para invalidar. Por exemplo, o farm nº 1 tem um host virtual de `www.mysite.com/path1/*` e o farm nº 2 tem um host virtual de `www.mysite.com/path2/*`. Você pode usar um URL de `/path1/invalidate.cache` para público alvo do primeiro farm e `/path2/invalidate.cache` para público alvo do segundo farm.

* **Usuário**

   Nome de usuário da conta a ser usada para acessar o público alvo.

* **Senha**

   Senha da conta a ser usada para acessar o público alvo.

* **Domínio NTLM**

   Domínio para autenticação NTML.

* **Host NTLM**

   Host para autenticação NTML.

* **Ativar SSL relaxado**

   Ative se desejar que certificados SSL autocertificados sejam aceitos.

* **Permitir certificados expirados**

   Ative se desejar que certificados SSL expirados sejam aceitos.

#### Proxy {#proxy}

As seguintes configurações são necessárias somente se um proxy for necessário:

* **Host do proxy**

   Nome do host do proxy usado para transporte.

* **Porta de proxy**

   Porta do proxy.

* **Usuário de proxy**

   Nome de usuário da conta a ser usada.

* **Senha do proxy**

   Senha da conta a ser usada.

* **Domínio do proxy NTLM**

   O domínio NTLM proxy.

* **Host do proxy NTLM**

   O domínio NTLM proxy.

#### Estendido {#extended}

* **Interface**

   Aqui você pode definir a interface de soquete à qual se vincular.

   Isso define o endereço local a ser usado ao criar conexões. Se isso não for definido, o endereço padrão será usado. Isso é útil para especificar a interface a ser usada em sistemas com vários pontos ou em cluster.

* **Método HTTP**

   O método HTTP a ser usado.

   Para um agente do Dispatcher Flush, isso é quase sempre GET e não deve ser alterado (POST seria outro valor possível).

* **Cabeçalhos de HTTP**

   Eles são usados para os agentes do Dispatcher Flush e especificam elementos que devem ser liberados.

   Para um agente do Dispatcher Flush, as três entradas padrão não precisam ser alteradas:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   Estes são utilizados, conforme apropriado, para indicar a ação a ser utilizada ao lavar a pega ou o caminho. Os subparâmetros são dinâmicos:

   * `{action}` indica uma ação de replicação

   * `{path}` indica um caminho

   Eles são substituídos pelo caminho/ação relevante para o pedido e, portanto, não precisam ser &quot;codificados&quot;:

   >[!NOTE]
   >
   >Se você instalou o AEM em um contexto diferente do padrão recomendado, será necessário registrar o contexto nos Cabeçalhos HTTP. Por exemplo:
   >`CQ-Handle:/<*yourContext*>{path}`

* **Fechar conexão**

   Ative para fechar a conexão após cada solicitação.

* **Tempo limite de conexão**

   Tempo limite (em milissegundos) a ser aplicado ao tentar estabelecer uma conexão.

* **Tempo limite do soquete**

   Tempo limite (em milissegundos) a ser aplicado ao aguardar tráfego após uma conexão ter sido estabelecida.

* **Versão do protocolo**

   Versão do protocolo; por exemplo `1.0` para HTTP/1.0.

#### Acionadores {#triggers}

Essas configurações são usadas para definir acionadores para replicação automatizada:

* **Ignorar padrão**

   Se marcado, o agente será excluído da replicação padrão; isso significa que ele não será usado se um autor de conteúdo executar uma ação de replicação.

* **Em modificação**

   Aqui, uma replicação por esse agente será acionada automaticamente quando uma página for modificada. Isso é usado principalmente para agentes do Dispatcher Flush, mas também para replicação reversa.

* **Durante roll-out**

   Se marcada, o agente replicará automaticamente qualquer conteúdo marcado para distribuição quando for modificado.

* **Tempo de ativação/desativação atingido**

   Isso acionará a replicação automática (para ativar ou desativar uma página, conforme o caso) quando ocorrer o tempo de funcionamento ou o tempo de inatividade definidos para uma página. Esta é utilizada principalmente para agentes do Dispatcher Flush.

* **No recebimento**

   Se marcado, o agente fará a replicação em cadeia sempre que receber eventos de replicação.

* **Sem atualização de status**

   Quando marcado, o agente não forçará uma atualização de status de replicação.

* **Sem controle de versão**

   Quando marcado, o agente não forçará o controle de versão de páginas ativadas.

## Configuração dos Agentes de Replicação {#configuring-your-replication-agents}

Para obter informações sobre como conectar agentes de replicação à instância de publicação usando MSSL, consulte [Replicação usando SSL](/help/sites-deploying/mssl-replication.md)Mútuo.

### Configuração dos agentes de replicação a partir do Ambiente Autor {#configuring-your-replication-agents-from-the-author-environment}

Na guia Ferramentas, no ambiente do autor, é possível configurar agentes de replicação que residem no ambiente do autor (**Agentes no autor**) ou no ambiente de publicação (**Agentes na publicação**). Os procedimentos a seguir ilustram a configuração de um agente para o ambiente autor, mas podem ser usados para ambos.

>[!NOTE]
>
>Quando um dispatcher manipula solicitações HTTP para instâncias de autor ou publicação, a solicitação HTTP do agente de replicação deve incluir o cabeçalho PATH. Além do procedimento a seguir, você deve adicionar o cabeçalho PATH à lista de despachantes dos cabeçalhos do cliente. (Consulte [/clientheaders (Cabeçalhos do cliente)](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders). [](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)


1. Acesse a guia **Ferramentas** no AEM.
1. Clique em **Replicação** (painel esquerdo para abrir a pasta).
1. Clique em **Agentes no autor** (no painel esquerdo ou direito).
1. Clique no nome do agente apropriado (que é um link) para mostrar informações detalhadas sobre esse agente.
1. Clique em **Editar** para abrir a caixa de diálogo de configuração:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Os valores fornecidos devem ser suficientes para uma instalação padrão. Se você fizer alterações, clique em **OK** para salvá-las (consulte Agentes [de Replicação - Parâmetros](#replication-agents-configuration-parameters) de Configuração para obter mais detalhes sobre os parâmetros individuais).

>[!NOTE]
>
>Uma instalação padrão de AEM especifica `admin` como usuário para credenciais de transporte dentro dos agentes de replicação padrão.
>
>Isso deve ser alterado para uma conta de usuário de replicação específica do site com os privilégios para replicar os caminhos necessários.

### Configurando Replicação Inversa {#configuring-reverse-replication}

A replicação reversa é usada para gerar o conteúdo do usuário em uma instância de publicação para uma instância do autor. Isso é comumente usado para recursos como pesquisas e formulários de registro.

Por motivos de segurança, a maioria das topologias de rede não permite conexões ** da &quot;Zona Desmilitarizada&quot; (uma subrede que expõe os serviços externos a uma rede não confiável, como a Internet).

Como o ambiente publish costuma estar no DMZ, para obter conteúdo de volta ao ambiente do autor, a conexão deve ser iniciada a partir da instância do autor. Isso é feito com:

* uma *caixa de saída* no ambiente de publicação onde o conteúdo é colocado.
* um agente (publicar) no ambiente do autor que consulta periodicamente a caixa de saída para novo conteúdo.

>[!NOTE]
>
>Para AEM [Communities](/help/communities/overview.md), a replicação não é usada para conteúdo gerado pelo usuário em uma instância de publicação. Consulte Armazenamento [de conteúdo da](/help/communities/working-with-srp.md)comunidade.

Para fazer isso, você precisa:

**Um agente de replicação reversa no ambiente** do autor Funciona como o componente ativo para coletar informações da caixa de saída no ambiente de publicação:

Se quiser usar a replicação reversa, verifique se esse agente está ativado.

![chlimage_1-23](assets/chlimage_1-23.png)

**Um agente de replicação reversa no ambiente de publicação (uma caixa de saída)** Esse é o elemento passivo, pois atua como uma &quot;caixa de saída&quot;. A entrada do usuário é colocada aqui, de onde é coletada pelo agente no ambiente do autor.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configuração da replicação para várias instâncias de publicação {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Somente o conteúdo é replicado - os dados do usuário não são replicados (usuários, grupos de usuários e perfis de usuários).
>
>Para sincronizar os dados do usuário em várias instâncias de publicação, ative a Sincronização [](/help/sites-administering/sync.md)do usuário.

Durante a instalação, um agente padrão já está configurado para replicação de conteúdo para uma instância de publicação executada na porta 4503 do host local.

Para configurar a replicação de conteúdo para uma instância de publicação adicional, é necessário criar e configurar um novo agente de replicação:

1. Abra a guia **Ferramentas** no AEM.
1. Selecione **Replicação** e, em seguida, **Agentes no autor** no painel esquerdo.
1. Selecionar **Novo...**.
1. Defina o **Título** e o **Nome** e selecione Agente **de** Replicação.
1. Clique em **Criar** para criar o novo agente.
1. Clique com o duplo no novo item do agente para abrir o painel de configuração.
1. Clique em **Editar** - a caixa de diálogo Configurações **do** agente será aberta - o Tipo **de** serialização já está definido como Padrão, isso deve continuar.

   * Na guia **Configurações** :

      * Ativar **Ativado**.
      * Informe uma **Descrição**.
      * Defina **Repetir atraso** como `60000`.

      * Deixe o Tipo **de** serialização como `Default`.
   * Na guia **Transporte** :

      * Insira o URI necessário para a nova instância de publicação; por exemplo,
         `https://localhost:4504/bin/receive`.

      * Insira a conta de usuário específica do site usada para replicação.
      * Você pode configurar outros parâmetros, conforme necessário.


1. Click **OK** to save the settings.

Em seguida, você pode testar a operação atualizando e publicando uma página no ambiente do autor.

As atualizações serão exibidas em todas as instâncias de publicação configuradas como acima.

Se encontrar algum problema, você pode verificar os registros na instância do autor. Dependendo do nível de detalhes necessário, também é possível definir o Nível **de** log para `Debug` usar a caixa de diálogo Configurações **do** agente como acima.

>[!NOTE]
>
>Isso pode ser combinado com o uso da ID [de usuário do](#agentuserid) agente para selecionar conteúdo diferente para replicação para os ambientes de publicação individuais. Para cada ambiente de publicação:
>
>1. Configure um agente de replicação para replicar para esse ambiente de publicação.
>1. Configurar uma conta de usuário; com os direitos de acesso necessários para ler o conteúdo que será replicado para esse ambiente de publicação específico.
>1. Atribua a conta de usuário como a ID **de usuário do** agente para o agente de replicação.

>



### Configurar um agente do Dispatcher Flush {#configuring-a-dispatcher-flush-agent}

Os agentes padrão são incluídos na instalação. No entanto, determinadas configurações ainda são necessárias e o mesmo se aplica se você estiver definindo um novo agente:

1. Abra a guia **Ferramentas** no AEM.
1. Clique em **Implantação**.
1. Selecione **Replicação** e, em seguida, **Agentes na publicação**.
1. Clique com o duplo no item **Dispatcher Flush** para abrir a visão geral.
1. Clique em **Editar** - a caixa de diálogo Configurações **do** agente será aberta:

   * Na guia **Configurações** :

      * Ativar **Ativado**.
      * Informe uma **Descrição**.
      * Deixe o Tipo **de** serialização como `Dispatcher Flush`, ou defina-o como tal se estiver criando um novo agente.

      * (opcional) Selecione Atualização **de** alias para ativar solicitações de invalidação de alias ou caminho personalizado para o Dispatcher.
   * Na guia **Transporte** :

      * Insira o URI necessário para a nova instância de publicação; por exemplo,
         `https://localhost:80/dispatcher/invalidate.cache`.

      * Insira a conta de usuário específica do site usada para replicação.
      * Você pode configurar outros parâmetros, conforme necessário.

   Para os agentes do Dispatcher Flush, a propriedade URI será usada somente se você usar entradas de host virtual baseadas em caminho para diferenciar entre farm, você usará esse campo para público alvo do farm para invalidar. Por exemplo, o farm nº 1 tem um host virtual de `www.mysite.com/path1/*` e o farm nº 2 tem um host virtual de `www.mysite.com/path2/*`. Você pode usar um URL de `/path1/invalidate.cache` para público alvo do primeiro farm e `/path2/invalidate.cache` para público alvo do segundo farm.

   >[!NOTE]
   >
   >Se você instalou AEM em um contexto diferente do padrão recomendado, é necessário configurar os Cabeçalhos [](#extended) HTTP na guia **Estendido** .

1. Clique em **OK** para salvar as alterações.
1. Retorne à guia **Ferramentas** , a partir daí você pode **Ativar** o agente **Dispatcher Flush** (**Agentes ao publicar**).

O agente de replicação **Dispatcher Flush** não está ativo no autor. Você pode acessar a mesma página no ambiente de publicação usando o URI equivalente; por exemplo, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Controle do acesso aos agentes de replicação {#controlling-access-to-replication-agents}

O acesso às páginas usadas para configurar os agentes de replicação pode ser controlado usando permissões de página de usuário e/ou grupo no `etc/replication` nó.

>[!NOTE]
>
>A configuração dessas permissões não afetará os usuários que replicam o conteúdo (por exemplo, no console Sites ou na opção de sidekick). A estrutura de replicação não usa a &quot;sessão de usuário&quot; do usuário atual para acessar agentes de replicação ao replicar páginas.

### Configuração dos agentes de replicação a partir do CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>A criação de agentes de replicação só é suportada no local do `/etc/replication` repositório. Isso é necessário para que as ACLs associadas sejam manipuladas corretamente. A criação de um agente de replicação em outro local da árvore pode resultar em acesso não autorizado.

Vários parâmetros dos agentes de replicação podem ser configurados usando o CRXDE Lite.

Se você navegar até `/etc/replication` você poderá ver os três nós a seguir:

* `agents.author`
* `agents.publish`
* `treeactivation`

As duas `agents` guardam informações de configuração sobre o ambiente apropriado e só estão ativas quando o ambiente está em execução. Por exemplo, `agents.publish` será usado somente no ambiente de publicação. A seguinte captura de tela mostra o agente de publicação no ambiente do autor, conforme incluído AEM WCM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Monitorando seus Agentes de Replicação {#monitoring-your-replication-agents}

Para monitorar um agente de replicação:

1. Acesse a guia **Ferramentas** no AEM.
1. Clique em **Replicação**.
1. Clique com o duplo no link para os agentes do ambiente apropriado (no painel esquerdo ou direito); por exemplo, **Agentes no autor**.

   A janela resultante mostra uma visão geral de todos os seus agentes de replicação para o ambiente do autor, incluindo seu público alvo e status.

1. Clique no nome do agente apropriado (que é um link) para mostrar informações detalhadas sobre esse agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Aqui você pode:

   * Veja se o agente está ativado.
   * Veja o público alvo de qualquer replicação.
   * Veja se a fila de replicação está ativa no momento (ativada).
   * Veja se há algum item na fila.
   * **Atualizar** ou **Limpar** para atualizar a exibição de entradas da fila; isso ajuda você a ver os itens entrando e saindo da fila.

   * **Log** de visualizações para acessar o log de quaisquer ações pelo agente de replicação.
   * **Testar conexão** com a instância do público alvo.
   * **Forçar nova tentativa** em qualquer item da fila, se necessário.

   >[!CAUTION]
   >
   >Não use o link &quot;Testar conexão&quot; para a caixa de saída de replicação inversa em uma instância de publicação.
   >
   >
   >Se um teste de replicação for executado para uma fila de caixa de saída, todos os itens mais antigos que a replicação de teste serão processados novamente com cada replicação reversa.
   >
   >
   >Se esses itens já existirem em uma fila, eles podem ser encontrados com o seguinte query XPath JCR e devem ser removidos.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replicação em lote {#batch-replication}

A replicação em lote não replica páginas ou ativos individuais, mas aguarda o primeiro limite dos dois, com base no tempo ou no tamanho, a ser acionado.

Em seguida, ele compacta todos os itens de replicação em um pacote, que é replicado como um único arquivo para o editor.

O editor descompactará todos os itens, salvá-los e retornará ao autor.

### Configuração da Replicação em Lote {#configuring-batch-replication}

1. Ir para `http://serveraddress:serverport/siteadmin`
1. Prima o ícone **[!UICONTROL Ferramentas]** no lado superior do ecrã
1. No painel de navegação do lado esquerdo, vá para **[!UICONTROL Replicação - agentes no autor]** e duplo clique em Agente **** padrão.
   * Você também pode acessar o agente de replicação de publicação padrão indo diretamente para `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Pressione o botão **[!UICONTROL Editar]** acima da fila de replicação.
1. Na seguinte janela, vá para a guia **[!UICONTROL Lote]** :
   ![replicação em lote](assets/batchreplication.png)
1. Configure o agente.

### Parâmetros {#parameters}

* `[!UICONTROL Enable Batch Mode]` - ativa ou desativa o modo de replicação em lote
* `[!UICONTROL Max Wait Time]` - Tempo máximo de espera até que uma solicitação em lote seja iniciada, em segundos. O padrão é 2 segundos.
* `[!UICONTROL Trigger Size]` - Replicação em lote de Start quando este limite de tamanho

## Recursos adicionais {#additional-resources}

Para obter detalhes sobre a solução de problemas, leia a página [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md) .

Para obter informações adicionais, o Adobe tem uma série de artigos da Base de conhecimento relacionados à replicação:

[https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html](https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html)[https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html](https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html)[https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html](https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html)[](https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html)https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html[https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html](https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html)[](https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.html)[](https://helpx.adobe.com/experience-manager/kb/ReplicationListener.html)[](https://helpx.adobe.com/experience-manager/kb/replication-stuck.html)[](https://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.html)[](https://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.html)[](https://helpx.adobe.com/experience-manager/kb/ACLReplication.html)[](https://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.html)[](https://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.html)https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationListener.htmlhttps://helpx.adobe.com/experience-manager/kb/replication-stuck.htmlhttps://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.html333333https://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.html3333333333333333333333333333333333333344333333333333333433333343333334333333300
