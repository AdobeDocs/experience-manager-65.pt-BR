---
title: Replicação
seo-title: Replication
description: Saiba como configurar e monitorar agentes de replicação no AEM.
seo-description: Learn how to configure and monitor replication agents in AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '3425'
ht-degree: 4%

---

# Replicação{#replication}

Os agentes de replicação são fundamentais para o Adobe Experience Manager (AEM), pois o mecanismo usado para:

* [Publicar (ativar)](/help/sites-authoring/publishing-pages.md#activatingcontent) conteúdo de um autor para um ambiente de publicação.
* Limpar explicitamente o conteúdo do cache do Dispatcher.
* Retorne a entrada do usuário (por exemplo, entrada de formulário) do ambiente de publicação para o ambiente do autor (sob controle do ambiente do autor).

As solicitações são [na fila](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) ao agente apropriado para processamento.

>[!NOTE]
>
>Os dados do usuário (usuários, grupos de usuários e perfis de usuários) não são replicados entre instâncias de autor e de publicação.
>
>Para várias instâncias de publicação, os dados do usuário são distribuídos pelo Sling quando [Sincronização de usuário](/help/sites-administering/sync.md) está ativado.

## Replicação do autor para a publicação {#replicating-from-author-to-publish}

A replicação para uma instância de publicação ou dispatcher ocorre em várias etapas:

* o autor solicita que determinado conteúdo seja publicado (ativado); isso pode ser iniciado por uma solicitação manual ou por acionadores automáticos que foram pré-configurados.
* a solicitação é passada para o agente de replicação padrão apropriado; um ambiente pode ter vários agentes padrão que sempre serão selecionados para essas ações.
* o agente de replicação &quot;empacota&quot; o conteúdo e o coloca na fila de replicação.
* na guia Sites, a variável [indicador de status colorido](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) é definido para páginas individuais.
* o conteúdo é retirado da fila e transportado para o ambiente de publicação usando o protocolo configurado; geralmente, é HTTP.
* um servlet no ambiente de publicação recebe a solicitação e publica o conteúdo recebido; o servlet padrão é `https://localhost:4503/bin/receive`.

* vários ambientes de autor e publicação podem ser configurados.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replicação de publicação para autor {#replicating-from-publish-to-author}

Alguns recursos permitem que os usuários insiram dados em uma instância de publicação.

Em alguns casos, um tipo de replicação conhecido como replicação reversa é necessário para retornar esses dados ao ambiente de criação de onde são redistribuídos para outros ambientes de publicação. Devido a considerações de segurança, qualquer tráfego da publicação para o ambiente de criação deve ser estritamente controlado.

A replicação reversa usa um agente no ambiente de publicação que faz referência ao ambiente de autor. Esse agente coloca os dados em uma caixa de saída. Essa caixa de saída corresponde aos ouvintes de replicação no ambiente do autor. Os ouvintes sondam as caixas de saída para coletar todos os dados inseridos e distribuí-los conforme necessário. Isso garante que o ambiente de criação controle todo o tráfego.

Em outros casos, como os recursos do Communities (por exemplo, fóruns, blogs, comentários e revisões), a quantidade de conteúdo gerado pelo usuário (UGC) inserida no ambiente de publicação é difícil de sincronizar com eficiência entre instâncias AEM usando replicação.

AEM [Communities](/help/communities/overview.md) nunca usa replicação para UGC. Em vez disso, a implantação do Communities requer um armazenamento comum para UGC (consulte [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md)).

### Replicação - pronta para uso {#replication-out-of-the-box}

O site de varejo na Web incluído em uma instalação padrão do AEM pode ser usado para ilustrar a replicação.

Para seguir este exemplo e usar os agentes de replicação default necessários [Instalar AEM](/help/sites-deploying/deploy.md) com:

* o ambiente do autor na porta `4502`
* o ambiente de publicação na porta `4503`

>[!NOTE]
>
>Ativado por padrão :
>
>* Agentes sobre o autor : Agente padrão (publicação)
>
>Efetivamente desabilitado por padrão (a partir do AEM 6.1):
>
>* Agentes no autor : Agente de replicação reversa (publish_reverse)
>* Agentes na publicação : Replicação reversa (caixa de saída)
>
>Para verificar o status do agente ou da fila, use o **Ferramentas** console.
>Consulte [Monitoramento dos agentes de replicação](#monitoring-your-replication-agents).

#### Replicação (Autor para publicar) {#replication-author-to-publish}

1. Acesse a página de suporte no ambiente do autor.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Edite a página para adicionar algum texto novo.
1. **Ativar página** para publicar as alterações.
1. Abra a página de suporte no ambiente de publicação:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Agora você pode ver as alterações inseridas no autor.

Essa replicação é ativada do ambiente do autor pelo:

* **Agente padrão (publicação)**
Esse agente replica o conteúdo na instância de publicação padrão.
É possível acessar os detalhes disso (configuração e registros) no console Ferramentas do ambiente do autor; ou:

   `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agentes de replicação - prontos para uso {#replication-agents-out-of-the-box}

Os seguintes agentes estão disponíveis em uma instalação padrão do AEM:

* [Agente padrão](#replication-author-to-publish)
Usado para replicar do autor para publicação.

* Limpeza do Dispatcher Usada para gerenciar o cache do Dispatcher. Consulte [Invalidação do cache do Dispatcher no ambiente de criação](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) e [Invalidação do cache do Dispatcher de uma instância de publicação](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) para obter mais informações.

* [Replicação reversa](#reverse-replication-publish-to-author)
Usado para replicação de publicação para autor. A replicação reversa não é usada para recursos das Comunidades, como fóruns, blogs e comentários. Ela é efetivamente desativada, pois a caixa de saída não está ativada. O uso da replicação reversa exigiria uma configuração personalizada.

* Agente estático: é um &quot;agente que armazena uma representação estática de um nó no sistema de arquivos&quot;.
Por exemplo, com as configurações padrão, as páginas de conteúdo e os ativos do DAM são armazenados em `/tmp`, como HTML ou o formato de ativo apropriado. Consulte a `Settings` e `Rules` para a configuração.
Isso foi solicitado para que, quando a página for solicitada diretamente do servidor de aplicativos, o conteúdo possa ser visto. Esse é um agente especializado e (provavelmente) não será necessário para a maioria das instâncias.

## Agentes de replicação - Parâmetros de configuração {#replication-agents-configuration-parameters}

Ao configurar um agente de replicação no console Ferramentas, quatro guias estarão disponíveis na caixa de diálogo:

### Configurações {#settings}

* **Nome**

   Nome exclusivo do agente de replicação.

* **Descrição**

   Uma descrição da finalidade deste agente de replicação.

* **Ativado**

   Indica se o agente de replicação está ativado no momento.

   Quando o agente estiver **habilitado** a fila será exibida como:

   * **Ativo** quando os itens estão sendo processados.
   * **Ocioso** quando a fila estiver vazia.
   * **Bloqueado** quando itens estão na fila, mas não podem ser processados; por exemplo, quando a fila de recebimento está desativada.

* **Tipo de serialização**

   O tipo de serialização:

   * **Padrão**: Defina se o agente deve ser selecionado automaticamente.
   * **Limpeza do Dispatcher**: selecione esta opção se o agente for usado para liberar o cache do dispatcher.

* **Tentar novamente o atraso**

   O atraso (tempo de espera em milissegundos) entre duas tentativas, caso seja encontrado um problema.

   Padrão: `60000`

* **ID de usuário agente**

   Dependendo do ambiente, o agente usará essa conta de usuário para:

   * coletar e empacotar o conteúdo do ambiente do autor
   * criar e gravar o conteúdo no ambiente de publicação

   Deixe este campo vazio para usar a conta de usuário do sistema (a conta definida no sling como o usuário administrador); por padrão, é `admin`).

   >[!CAUTION]
   >
   >Para um agente no ambiente de criação, esta conta *deve* ter acesso de leitura a todos os caminhos que deseja replicar.

   >[!CAUTION]
   >
   >Para um agente no ambiente de publicação, essa conta *deve* ter o acesso de criação/gravação necessário para replicar o conteúdo.

   >[!NOTE]
   >
   >Isso pode ser usado como um mecanismo para selecionar conteúdo específico para replicação.

* **Nível de registro**

   Especifica o nível de detalhes a ser usado para mensagens de log.

   * `Error`: somente erros serão registrados em log
   * `Info`: erros, avisos e outras mensagens informativas serão registrados
   * `Debug`: um alto nível de detalhes será usado nas mensagens, principalmente para fins de depuração

   Padrão: `Info`

* **Use para replicação reversa**

   Indica se esse agente será usado para replicação reversa; retorna a entrada do usuário da publicação para o ambiente do autor.

* **Atualização do alias**

   Selecionar essa opção permite solicitações de invalidação de alias ou caminho personalizado para o Dispatcher. Consulte também [Configuração de um agente de limpeza do Dispatcher](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transporte {#transport}

* **URI**

   Especifica o servlet de recebimento no local de destino. Especificamente, você pode especificar o nome do host (ou alias) e o caminho do contexto para a instância de destino aqui.

   Por exemplo:

   * Um agente padrão pode ser replicado para `https://localhost:4503/bin/receive`
   * Um agente de limpeza do Dispatcher pode replicar em `https://localhost:8000/dispatcher/invalidate.cache`

   O protocolo especificado aqui (HTTP ou HTTPS) determinará o método de transporte.

   Para agentes de limpeza do Dispatcher, a propriedade do URI é usada somente se você usar entradas de hosts virtuais baseadas em caminho para diferenciar entre farms. Use esse campo para direcionar o farm a ser invalidado. Por exemplo, o farm nº 1 tem um host virtual de `www.mysite.com/path1/*`, e o farm nº 2 tem um host virtual de `www.mysite.com/path2/*`. Você pode usar um URL de `/path1/invalidate.cache` para direcionar o primeiro farm, e `/path2/invalidate.cache` para direcionar o segundo farm.

* **Usuário**

   Nome de usuário da conta a ser usada para acessar o público alvo.

* **Senha**

   Senha da conta a ser usada para acessar o público alvo.

* **Domínio NTLM**

   Domínio para autenticação NTML.

* **Host NTLM**

   Host para autenticação NTML.

* **Ativar SSL relaxado**

   Ative se quiser que certificados SSL autocertificados sejam aceitos.

* **Permitir certificados expirados**

   Ative se quiser que certificados SSL expirados sejam aceitos.

#### Proxy {#proxy}

As seguintes configurações só serão necessárias se um proxy for necessário:

* **Host do proxy**

   Nome do host do proxy usado para transporte.

* **Porta de proxy**

   Porta do proxy.

* **Usuário de proxy**

   Nome de usuário da conta a ser usada.

* **Senha do proxy**

   Senha da conta a ser usada.

* **Domínio do proxy NTLM**

   O domínio do proxy NTLM.

* **Host do proxy NTLM**

   O domínio do proxy NTLM.

#### Estendido {#extended}

* **Interface**

   Aqui você pode definir a interface de soquete à qual se vincular.

   Isso define o endereço local a ser usado ao criar conexões. Se isso não for definido, o endereço padrão será usado. Isso é útil para especificar a interface a ser usada em sistemas com vários locais ou em cluster.

* **Método HTTP**

   O método HTTP a ser usado.

   Para um agente de limpeza do Dispatcher, isso é quase sempre GET e não deve ser alterado (POST seria outro valor possível).

* **Cabeçalhos de HTTP**

   Eles são usados para agentes de limpeza do Dispatcher e especificam elementos que devem ser removidos.

   Para um agente de limpeza do Dispatcher, as três entradas padrão não devem precisar ser alteradas:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   Eles são usados, conforme apropriado, para indicar a ação a ser usada ao limpar a alça ou o caminho. Os subparâmetros são dinâmicos:

   * `{action}` indica uma ação de replicação

   * `{path}` indica um caminho

   Eles são substituídos pelo caminho/ação relevante para a solicitação e, portanto, não precisam ser &quot;codificados&quot;:

   >[!NOTE]
   >
   >Se você instalou o AEM em um contexto diferente do contexto padrão recomendado, será necessário registrar o contexto nos Cabeçalhos HTTP. Por exemplo:
   >`CQ-Handle:/<*yourContext*>{path}`

* **Fechar conexão**

   Ativar para fechar a conexão após cada solicitação.

* **Tempo limite da conexão**

   Tempo limite (em milissegundos) a ser aplicado ao tentar estabelecer uma conexão.

* **Tempo limite do soquete**

   Tempo limite (em milissegundos) a ser aplicado ao aguardar pelo tráfego após uma conexão ser estabelecida.

* **Versão do protocolo**

   Versão do protocolo; por exemplo `1.0` para HTTP/1.0.

#### Acionadores {#triggers}

Essas configurações são usadas para definir acionadores para replicação automatizada:

* **Ignorar padrão**

   Se marcado, o agente será excluído da replicação padrão; isso significa que ele não será usado se um autor de conteúdo emitir uma ação de replicação.

* **Em modificação**

   Aqui, uma replicação por esse agente será acionada automaticamente quando uma página for modificada. Isso é usado principalmente para agentes de limpeza do Dispatcher, mas também para replicação reversa.

* **Durante roll-out**

   Se marcado, o agente replicará automaticamente qualquer conteúdo marcado para distribuição quando for modificado.

* **Horário Ligado/Desligado atingido**

   Isso acionará a replicação automática (para ativar ou desativar uma página, conforme apropriado) quando ocorrerem os tempos online ou offline definidos para uma página. Isso é usado principalmente para agentes de limpeza do Dispatcher.

* **No recebimento**

   Se marcado, o agente encadeará a replicação sempre que receber eventos de replicação.

* **Sem atualização de status**

   Quando marcado, o agente não forçará uma atualização do status de replicação.

* **Sem controle de versão**

   Quando marcado, o agente não forçará o controle da versão das páginas ativadas.

## Configurar os agentes de replicação {#configuring-your-replication-agents}

Para obter informações sobre como conectar agentes de replicação à instância de publicação usando MSSL, consulte [Replicação usando SSL mútuo](/help/sites-deploying/mssl-replication.md).

### Configurar os agentes de replicação no ambiente do autor {#configuring-your-replication-agents-from-the-author-environment}

Na guia Ferramentas do ambiente de autor, é possível configurar agentes de replicação que residem no ambiente do autor (**Agentes sobre o autor**) ou o ambiente de publicação (**Agentes sobre publicação**). Os procedimentos a seguir ilustram a configuração de um agente para o ambiente de criação, mas podem ser usados para ambos.

>[!NOTE]
>
>Quando um dispatcher lida com solicitações HTTP para instâncias de autor ou publicação, a solicitação HTTP do agente de replicação deve incluir o cabeçalho PATH. Além do procedimento a seguir, você deve adicionar o cabeçalho PATH à lista de cabeçalhos de clientes do dispatcher. (Consulte [/clientheaders (Cabeçalhos do cliente)](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

1. Acesse o **Ferramentas** no AEM.
1. Clique em **Replicação** (painel esquerdo para abrir a pasta).
1. Clique duas vezes **Agentes sobre o autor** (painel esquerdo ou direito).
1. Clique no nome do agente apropriado (que é um link) para mostrar informações detalhadas sobre esse agente.
1. Clique em **Editar** para abrir a caixa de diálogo de configuração:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Os valores fornecidos devem ser suficientes para uma instalação padrão. Se você fizer alterações, clique em **OK** para salvá-los (consulte [Agentes de replicação - Parâmetros de configuração](#replication-agents-configuration-parameters) para obter mais detalhes sobre os parâmetros individuais).

>[!NOTE]
>
>Uma instalação padrão de AEM especifica `admin` como o usuário para credenciais de transporte nos agentes de replicação padrão.
>
>Isso deve ser alterado para uma conta de usuário de replicação específica do site com os privilégios para replicar os caminhos necessários.

### Configuração da replicação reversa {#configuring-reverse-replication}

A replicação reversa é usada para obter o conteúdo do usuário gerado em uma instância de publicação de volta para uma instância do autor. Isso é comumente usado para recursos como pesquisas e formulários de registro.

Por motivos de segurança, a maioria das topologias de rede não permite conexões *de* a &quot;Zona desmilitarizada&quot; (uma sub-rede que expõe os serviços externos a uma rede não confiável, como a Internet).

Como o ambiente de publicação geralmente está no DMZ, para retornar o conteúdo ao ambiente de criação, a conexão deve ser iniciada a partir da instância de criação. Isso é feito com:

* um *caixa de saída* no ambiente de publicação onde o conteúdo é colocado.
* um agente (publicação) no ambiente de criação que pesquisa periodicamente a caixa de saída em busca de novo conteúdo.

>[!NOTE]
>
>Para AEM [Communities](/help/communities/overview.md), a replicação não é usada para conteúdo gerado pelo usuário em uma instância de publicação. Consulte [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md).

Para fazer isso, é necessário:

**Um agente de replicação reversa no ambiente de autor** Ele atua como o componente ativo para coletar informações da caixa de saída no ambiente de publicação:

Se quiser usar replicação reversa, verifique se esse agente está ativado.

![chlimage_1-23](assets/chlimage_1-23.png)

**Um agente de replicação reversa no ambiente de publicação (uma caixa de saída)** Esse é o elemento passivo, pois atua como uma &quot;caixa de saída&quot;. A entrada do usuário é colocada aqui, de onde é coletada pelo agente no ambiente do autor.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configuração da replicação para várias instâncias de publicação {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Somente o conteúdo é replicado — os dados do usuário não são (usuários, grupos de usuários e perfis de usuários).
>
>Para sincronizar dados do usuário em várias instâncias de publicação, habilite [Sincronização de usuário](/help/sites-administering/sync.md).

Após a instalação, um agente padrão já está configurado para replicação de conteúdo em uma instância de publicação em execução na porta 4503 do host local.

Para configurar a replicação de conteúdo para uma instância de publicação adicional, você precisa criar e configurar um novo agente de replicação:

1. Abra o **Ferramentas** no AEM.
1. Selecionar **Replicação**, depois **Agentes sobre o autor** no painel esquerdo.
1. Selecionar **Novo...**.
1. Defina o **Título** e **Nome** e selecione **Agente de replicação**.
1. Clique em **Criar** para criar o novo agente.
1. Clique duas vezes no novo item de agente para abrir o painel de configuração.
1. Clique em **Editar** - o **Configurações do agente** será aberta - a caixa de diálogo **Tipo de serialização** já estiver definido como Padrão, assim deverá permanecer.

   * No **Configurações** guia:

      * Ativar **Ativado**.
      * Insira um **Descrição**.
      * Defina o **Tentar novamente o atraso** para `60000`.

      * Deixe a **Tipo de serialização** as `Default`.
   * No **Transporte** guia:

      * Insira o URI necessário para a nova instância de publicação; por exemplo,
         `https://localhost:4504/bin/receive`.

      * Insira a conta de usuário específica do site usada para replicação.
      * Você pode configurar outros parâmetros conforme necessário.


1. Clique em **OK** para salvar as configurações.

Em seguida, você pode testar a operação atualizando e publicando uma página no ambiente de criação.

As atualizações serão exibidas em todas as instâncias de publicação que foram configuradas como acima.

Se encontrar problemas, verifique os logs na instância do autor. Dependendo do nível de detalhes necessário, você também pode definir a variável **Nível de registro** para `Debug` usando o **Configurações do agente** como acima.

>[!NOTE]
>
>Esta possibilidade pode ser combinada com a [ID de usuário agente](#agentuserid) para selecionar conteúdo diferente para replicação nos ambientes de publicação individuais. Para cada ambiente de publicação:
>
>1. Configure um agente de replicação para replicar nesse ambiente de publicação.
>1. Configurar uma conta de usuário; com os direitos de acesso necessários para ler o conteúdo que será replicado para esse ambiente de publicação específico.
>1. Atribua a conta de usuário como o **ID de usuário agente** para o agente de replicação.

>


### Configuração de um agente de limpeza do Dispatcher {#configuring-a-dispatcher-flush-agent}

Os agentes padrão estão incluídos na instalação. No entanto, determinadas configurações ainda são necessárias e o mesmo se aplica se você estiver definindo um novo agente:

1. Abra o **Ferramentas** no AEM.
1. Clique em **Implantação**.
1. Selecionar **Replicação** e depois **Agentes sobre publicação**.
1. Clique duas vezes na guia **Limpeza do Dispatcher** item para abrir a visão geral.
1. Clique em **Editar** - o **Configurações do agente** será aberta:

   * No **Configurações** guia:

      * Ativar **Ativado**.
      * Insira um **Descrição**.
      * Deixe a **Tipo de serialização** as `Dispatcher Flush`ou defina-o como tal se estiver criando um novo agente.

      * (opcional) Selecione **Atualização de alias** para ativar solicitações de invalidação de alias ou caminho personalizado para o Dispatcher.
   * No **Transporte** guia:

      * Insira o URI necessário para a nova instância de publicação; por exemplo,
         `https://localhost:80/dispatcher/invalidate.cache`.

      * Insira a conta de usuário específica do site usada para replicação.
      * Você pode configurar outros parâmetros conforme necessário.

   Para agentes de limpeza do Dispatcher, a propriedade do URI é usada somente se você usar entradas de hosts virtuais baseadas em caminho para diferenciar entre farms. Use esse campo para direcionar o farm a ser invalidado. Por exemplo, o farm nº 1 tem um host virtual de `www.mysite.com/path1/*`, e o farm nº 2 tem um host virtual de `www.mysite.com/path2/*`. Você pode usar um URL de `/path1/invalidate.cache` para direcionar o primeiro farm, e `/path2/invalidate.cache` para direcionar o segundo farm.

   >[!NOTE]
   >
   >Se você instalou o AEM em um contexto diferente do contexto padrão recomendado, será necessário configurar o [Cabeçalhos HTTP](#extended) no **Estendido** guia.

1. Clique em **OK** para salvar as alterações.
1. Retorne para a **Ferramentas** , daqui é possível **Ativar** o **Limpeza do Dispatcher** agente (**Agentes sobre publicação**).

A variável **Limpeza do Dispatcher** o agente de replicação não está ativo no autor. É possível acessar a mesma página no ambiente de publicação usando o URI equivalente; por exemplo, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Controle de acesso aos agentes de replicação {#controlling-access-to-replication-agents}

O acesso às páginas usadas para configurar os agentes de replicação pode ser controlado usando permissões de página de usuário e/ou grupo no `etc/replication` nó.

>[!NOTE]
>
>A definição dessas permissões não afetará os usuários que replicam conteúdo (por exemplo, a partir do console Sites ou da opção sidekick). A estrutura de replicação não usa a &quot;sessão de usuário&quot; do usuário atual para acessar agentes de replicação ao replicar páginas.

### Configurar os agentes de replicação do CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>A criação de agentes de replicação só é compatível com o `/etc/replication` local do repositório. Isso é necessário para que as ACLs associadas sejam manipuladas adequadamente. A criação de um agente de replicação em outro local da árvore pode levar a acesso não autorizado.

Vários parâmetros dos agentes de replicação podem ser configurados usando o CRXDE Lite.

Se você navegar até `/etc/replication` você pode ver os três nós a seguir:

* `agents.author`
* `agents.publish`
* `treeactivation`

Os dois `agents` mantém informações de configuração sobre o ambiente apropriado e só estão ativas quando esse ambiente está em execução. Por exemplo, `agents.publish` serão usados somente no ambiente de publicação. A captura de tela a seguir mostra o agente de publicação no ambiente de criação, conforme incluído no WCM do AEM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Monitoramento dos agentes de replicação {#monitoring-your-replication-agents}

Para monitorar um agente de replicação:

1. Acesse o **Ferramentas** no AEM.
1. Clique em **Replicação**.
1. Clique duas vezes no link para agentes do ambiente apropriado (no painel esquerdo ou direito); por exemplo **Agentes sobre o autor**.

   A janela resultante mostra uma visão geral de todos os agentes de replicação para o ambiente de criação, incluindo o destino e o status.

1. Clique no nome do agente apropriado (que é um link) para mostrar informações detalhadas sobre esse agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Aqui você pode:

   * Veja se o agente está ativado.
   * Visualizar o destino de qualquer replicação.
   * Verifique se a fila de replicação está ativa no momento (ativada).
   * Verificar se há itens na fila.
   * **Atualizar** ou **Limpar** para atualizar a exibição de entradas na fila; isso ajuda a ver os itens que entram e saem da fila.

   * **Exibir registro** para acessar o registro de qualquer ação pelo agente de replicação.
   * **Testar conexão** para a instância de destino.
   * **Forçar nova tentativa** em qualquer item da fila, se necessário.

   >[!CAUTION]
   >
   >Não use o link &quot;Testar conexão&quot; para a Caixa de saída de replicação reversa em uma instância de publicação.
   >
   >
   >Se um teste de replicação for executado para uma fila da Caixa de saída, quaisquer itens mais antigos que a replicação de teste serão reprocessados com cada replicação reversa.
   >
   >
   >Se esses itens já existirem em uma fila, eles poderão ser encontrados com a seguinte consulta XPath JCR e deverão ser removidos.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replicação em lote {#batch-replication}

A replicação em lote não replica páginas ou ativos individuais, mas aguarda que o primeiro limite dos dois, com base no tempo ou tamanho, seja acionado.

Em seguida, compacta todos os itens de replicação em um pacote, que é replicado como um único arquivo para o publicador.

O editor desembalará todos os itens, os salvará e relatará ao autor.

### Configuração da replicação em lote {#configuring-batch-replication}

1. Ir para `http://serveraddress:serverport/siteadmin`
1. Pressione a **[!UICONTROL Ferramentas]** ícone no lado superior da tela
1. No painel de navegação esquerdo, vá para **[!UICONTROL Replicação - Agentes no autor]** e clique duas vezes **[!UICONTROL Agente padrão]**.
   * Você também pode acessar o agente de replicação de publicação padrão acessando diretamente `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Pressione a **[!UICONTROL Editar]** acima da fila de replicação.
1. Na janela a seguir, vá para a **[!UICONTROL Lote]** guia:
   ![replicação em lote](assets/batchreplication.png)
1. Configure o agente.

### Parâmetros {#parameters}

* `[!UICONTROL Enable Batch Mode]` - ativa ou desativa o modo de replicação de lote
* `[!UICONTROL Max Wait Time]` - Tempo máximo de espera até que uma solicitação de lote seja iniciada, em segundos. O padrão é 2 segundos.
* `[!UICONTROL Trigger Size]` - Inicia a replicação de lote quando este limite de tamanho

## Recursos adicionais {#additional-resources}

Para obter detalhes sobre a solução de problemas, leia o [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md) página.
