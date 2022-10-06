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

Os agentes de replicação são fundamentais para o Adobe Experience Manager (AEM), pois o mecanismo é usado para:

* [Publicar (ativar)](/help/sites-authoring/publishing-pages.md#activatingcontent) conteúdo de um autor em um ambiente de publicação.
* Liberar explicitamente o conteúdo do cache do Dispatcher.
* Retorne a entrada do usuário (por exemplo, a entrada de formulário) do ambiente de publicação para o ambiente do autor (sob controle do ambiente do autor).

As solicitações são [em fila](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) ao agente de transformação adequado.

>[!NOTE]
>
>Os dados do usuário (usuários, grupos de usuários e perfis de usuário) não são replicados entre as instâncias de autor e publicação.
>
>Para várias instâncias de publicação, os dados do usuário são distribuídos pelo Sling quando [Sincronização de usuários](/help/sites-administering/sync.md) estiver ativado.

## Replicação do autor para publicação {#replicating-from-author-to-publish}

A replicação para uma instância de publicação ou dispatcher ocorre em várias etapas:

* o autor solicita que certos conteúdos sejam publicados (ativados); isso pode ser iniciado por uma solicitação manual ou por acionadores automáticos que foram pré-configurados.
* a solicitação é passada para o agente de replicação padrão apropriado; um ambiente pode ter vários agentes padrão que sempre serão selecionados para tais ações.
* o agente de replicação &quot;compacta&quot; o conteúdo e o coloca na fila de replicação.
* na guia Sites , o [indicador de status colorido](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) é definido para páginas individuais.
* o conteúdo é removido da fila e transportado para o ambiente de publicação usando o protocolo configurado; geralmente, isso é HTTP.
* um servlet no ambiente de publicação recebe a solicitação e publica o conteúdo recebido; o servlet padrão é `https://localhost:4503/bin/receive`.

* vários ambientes de criação e publicação podem ser configurados.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replicação de Publicar para Autor {#replicating-from-publish-to-author}

Alguns recursos permitem que os usuários insiram dados em uma instância de publicação.

Em alguns casos, um tipo de replicação conhecido como replicação inversa é necessário para retornar esses dados ao ambiente do autor, de onde são redistribuídos para outros ambientes de publicação. Devido a considerações de segurança, qualquer tráfego do ambiente de publicação para o autor deve ser rigorosamente controlado.

A replicação inversa usa um agente no ambiente de publicação que faz referência ao ambiente do autor. Esse agente coloca os dados em uma caixa de saída. Essa caixa de saída corresponde aos ouvintes de replicação no ambiente do autor. Os listeners pesquisam as caixas de saída para coletar os dados inseridos e depois distribuí-los conforme necessário. Isso garante que o ambiente do autor controle todo o tráfego.

Em outros casos, como para recursos do Communities (por exemplo, fóruns, blogs, comentários e revisões), a quantidade de conteúdo gerado pelo usuário (UGC) que está sendo inserida no ambiente de publicação é difícil de sincronizar com eficiência entre instâncias AEM usando replicação.

AEM [Comunidades](/help/communities/overview.md) O nunca usa replicação para UGC. Em vez disso, a implantação do Communities requer um armazenamento comum para UGC (consulte [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md)).

### Replicação - pronta para uso {#replication-out-of-the-box}

O site we-retail incluído em uma instalação padrão de AEM pode ser usado para ilustrar a replicação.

Para seguir este exemplo e usar os agentes de replicação padrão, é necessário [Instalar AEM](/help/sites-deploying/deploy.md) com:

* o ambiente do autor no porto `4502`
* o ambiente de publicação no porto `4503`

>[!NOTE]
>
>Ativado por padrão :
>
>* Agentes do autor : Agente padrão (publicar)
>
>Eficazmente desativado por padrão (a partir do AEM 6.1) :
>
>* Agentes do autor : Agente de replicação inversa (publish_reverse)
>* Agentes na publicação : Replicação reversa (caixa de saída)
>
>Para verificar o status do agente ou da fila, use a função **Ferramentas** console.
>Consulte [Monitorar os agentes de replicação](#monitoring-your-replication-agents).

#### Replicação (Autor para publicar) {#replication-author-to-publish}

1. Navegue até a página de suporte no ambiente de criação.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Edite a página para adicionar novo texto.
1. **Ativar página** para publicar as alterações.
1. Abra a página de suporte no ambiente de publicação:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Agora é possível ver as alterações inseridas no autor.

Essa replicação é acionada do ambiente de criação pelo:

* **Agente padrão (publicar)**
Esse agente replica conteúdo na instância de publicação padrão.
Os detalhes disso (configuração e logs) podem ser acessados no console Ferramentas do ambiente do autor; ou:

   `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agentes de replicação - prontos para uso {#replication-agents-out-of-the-box}

Os seguintes agentes estão disponíveis em uma instalação padrão de AEM:

* [Agente padrão](#replication-author-to-publish)
Usado para replicar do autor para publicar.

* Liberação do Dispatcher É usada para gerenciar o cache do Dispatcher. Consulte [Invalidar o cache do Dispatcher no ambiente de criação](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) e [Invalidar o cache do Dispatcher de uma Instância de Publicação](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) para obter mais informações.

* [Replicação inversa](#reverse-replication-publish-to-author)
Usado para replicar da publicação para o autor. A replicação inversa não é usada para recursos do Communities, como fóruns, blogs e comentários. Ela é efetivamente desativada, pois a caixa de saída não está ativada. O uso da replicação inversa exigiria configuração personalizada.

* Agente estático É um &quot;Agente que armazena uma representação estática de um nó no sistema de arquivos&quot;.
Por exemplo, com as configurações padrão, as páginas de conteúdo e os ativos dam são armazenados em `/tmp`, como HTML ou o formato de ativo apropriado. Consulte a `Settings` e `Rules` para a configuração.
Isso foi solicitado para que, quando a página for solicitada diretamente do servidor de aplicativos, o conteúdo possa ser visualizado. Este é um agente especializado e (provavelmente) não será necessário para a maioria das instâncias.

## Agentes de Replicação - Parâmetros de Configuração {#replication-agents-configuration-parameters}

Ao configurar um agente de replicação no console Ferramentas , quatro guias estão disponíveis na caixa de diálogo:

### Configurações {#settings}

* **Nome**

   Um nome exclusivo para o agente de replicação.

* **Descrição**

   Uma descrição da finalidade que esse agente de replicação servirá.

* **Ativado**

   Indica se o agente de replicação está ativado no momento.

   Quando o agente é **ativado** a fila será exibida como:

   * **Ativo** quando os itens estão sendo processados.
   * **Inativo** quando a fila estiver vazia.
   * **Bloqueio** quando os itens estão na fila, mas não podem ser processados; por exemplo, quando a fila de recebimento está desativada.

* **Tipo de serialização**

   O tipo de serialização:

   * **Padrão**: Defina se o agente deve ser selecionado automaticamente.
   * **Liberação do Dispatcher**: Selecione essa opção se o agente for usado para liberar o cache do dispatcher.

* **Tentar novamente o atraso**

   O atraso (tempo de espera em milissegundos) entre duas tentativas, caso um problema seja encontrado.

   Padrão: `60000`

* **ID de usuário agente**

   Dependendo do ambiente, o agente usará essa conta de usuário para:

   * coletar e empacotar o conteúdo do ambiente de criação
   * criar e gravar o conteúdo no ambiente de publicação

   Deixe este campo vazio para usar a conta de usuário do sistema (a conta definida no sling como o usuário administrador; por padrão, isso é `admin`).

   >[!CAUTION]
   >
   >Para um agente no ambiente de criação, esta conta *must* tenha acesso de leitura a todos os caminhos que deseja replicar.

   >[!CAUTION]
   >
   >Para um agente no ambiente de publicação, essa conta *must* ter o acesso de criação/gravação necessário para replicar o conteúdo.

   >[!NOTE]
   >
   >Isso pode ser usado como um mecanismo para selecionar conteúdo específico para replicação.

* **Nível de registro**

   Especifica o nível de detalhes a serem usados para mensagens de log.

   * `Error`: somente erros serão registrados
   * `Info`: erros, avisos e outras mensagens informativas serão registrados
   * `Debug`: um alto nível de detalhes será usado nas mensagens, principalmente para fins de depuração

   Padrão: `Info`

* **Use para replicação reversa**

   Indica se esse agente será usado para replicação inversa; retorna a entrada do usuário do ambiente de publicação para autor.

* **Atualização do alias**

   Selecionar essa opção ativa solicitações de invalidação de alias ou caminho personalizado para o Dispatcher. Além disso, consulte [Configurar um agente de limpeza do Dispatcher](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transporte {#transport}

* **URI**

   Especifica o servlet de recebimento no local de destino. Em particular, você pode especificar o nome do host (ou alias) e o caminho do contexto para a instância do público alvo aqui.

   Por exemplo:

   * Um Agente Padrão pode replicar para `https://localhost:4503/bin/receive`
   * Um agente Dispatcher Flush pode replicar para `https://localhost:8000/dispatcher/invalidate.cache`

   O protocolo especificado aqui (HTTP ou HTTPS) determinará o método de transporte.

   Para agentes de Liberação do Dispatcher, a propriedade URI será usada somente se você usar entradas virtualhost baseadas em caminho para diferenciar entre farms, use esse campo para direcionar o farm para invalidar. Por exemplo, o farm nº 1 tem um host virtual de `www.mysite.com/path1/*`, e o farm nº 2 tem um host virtual de `www.mysite.com/path2/*`. Você pode usar um URL de `/path1/invalidate.cache` para direcionar o primeiro farm, e `/path2/invalidate.cache` para direcionar o segundo farm.

* **Usuário**

   Nome de usuário da conta a ser usada para acessar o target.

* **Senha**

   Senha da conta a ser usada para acessar o target.

* **Domínio NTLM**

   Domínio para autenticação NTML.

* **Host NTLM**

   Host para autenticação NTML.

* **Ativar SSL relaxado**

   Ative se desejar que certificados SSL autocertificados sejam aceitos.

* **Permitir certificados expirados**

   Ative se desejar que certificados SSL expirados sejam aceitos.

#### Proxy {#proxy}

As configurações a seguir são necessárias somente se um proxy for necessário:

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

   Aqui você pode definir a interface do soquete para a qual vincular.

   Isso define o endereço local a ser usado ao criar conexões. Se isso não for definido, o endereço padrão será usado. Isso é útil para especificar a interface a ser usada em sistemas com vários pontos ou em cluster.

* **Método HTTP**

   O método HTTP a ser usado.

   Para um agente de Liberação do Dispatcher, isso é quase sempre GET e não deve ser alterado (POST seria outro valor possível).

* **Cabeçalhos de HTTP**

   Eles são usados para agentes de Liberação do Dispatcher e especificam elementos que devem ser liberados.

   Para um agente de Liberação do Dispatcher, as três entradas padrão não devem precisar ser alteradas:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   Elas são usadas, conforme apropriado, para indicar a ação a ser usada ao limpar o manípulo ou o caminho. Os subparâmetros são dinâmicos:

   * `{action}` indica uma ação de replicação

   * `{path}` indica um caminho

   Eles são substituídos pelo caminho/ação relevante para a solicitação e, portanto, não precisam ser &quot;codificados&quot;:

   >[!NOTE]
   >
   >Se tiver instalado o AEM em um contexto diferente do contexto padrão recomendado, será necessário registrar o contexto nos Cabeçalhos HTTP. Por exemplo:
   >`CQ-Handle:/<*yourContext*>{path}`

* **Fechar conexão**

   Ative para fechar a conexão após cada solicitação.

* **Tempo limite de conexão**

   Tempo limite (em milissegundos) a ser aplicado ao tentar estabelecer uma conexão.

* **Tempo limite do soquete**

   Tempo limite (em milissegundos) a ser aplicado ao aguardar tráfego após estabelecer uma conexão.

* **Versão do protocolo**

   Versão do protocolo; por exemplo `1.0` para HTTP/1.0.

#### Acionadores {#triggers}

Essas configurações são usadas para definir acionadores para replicação automatizada:

* **Ignorar padrão**

   Se marcada, o agente é excluído da replicação padrão; isso significa que ele não será usado se um autor de conteúdo emitir uma ação de replicação.

* **Em modificação**

   Aqui, uma replicação por esse agente será acionada automaticamente quando uma página for modificada. Isso é usado principalmente para agentes de liberação do Dispatcher, mas também para replicação reversa.

* **Durante roll-out**

   Se marcada, o agente replicará automaticamente qualquer conteúdo marcado para distribuição quando for modificado.

* **Tempo de Ativação/Desativação atingido**

   Isso acionará a replicação automática (para ativar ou desativar uma página, conforme apropriado) quando ocorrerem as vezes ou horas de inatividade definidas para uma página. Isso é usado principalmente para agentes de liberação do Dispatcher.

* **No recebimento**

   Se marcada, o agente fará a replicação em cadeia sempre que receber eventos de replicação.

* **Sem atualização de status**

   Quando marcado, o agente não forçará uma atualização de status de replicação.

* **Sem controle de versão**

   Quando marcado, o agente não forçará o controle de versão de páginas ativadas.

## Configurar seus agentes de replicação {#configuring-your-replication-agents}

Para obter informações sobre como conectar agentes de replicação à instância de publicação usando MSSL, consulte [Replicação usando SSL mútuo](/help/sites-deploying/mssl-replication.md).

### Configurar os agentes de replicação no ambiente de criação {#configuring-your-replication-agents-from-the-author-environment}

Na guia Ferramentas no ambiente de criação, é possível configurar agentes de replicação que residam no ambiente de criação (**Agentes do autor**) ou o ambiente de publicação (**Agentes na publicação**). Os procedimentos a seguir ilustram a configuração de um agente para o ambiente do autor, mas podem ser usados para ambos.

>[!NOTE]
>
>Quando um dispatcher lida com solicitações HTTP para instâncias de autor ou publicação, a solicitação HTTP do agente de replicação deve incluir o cabeçalho PATH. Além do procedimento a seguir, você deve adicionar o cabeçalho PATH à lista de dispatchers dos cabeçalhos do cliente. (Consulte [/clientheaders (Cabeçalhos do Cliente)](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

1. Acesse o **Ferramentas** em AEM.
1. Clique em **Replicação** (painel esquerdo para abrir a pasta).
1. Clique duas vezes **Agentes do autor** (painel esquerdo ou direito).
1. Clique no nome do agente apropriado (que é um link) para mostrar informações detalhadas sobre esse agente.
1. Clique em **Editar** para abrir a caixa de diálogo de configuração:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Os valores fornecidos devem ser suficientes para uma instalação padrão. Se você fizer alterações, clique em **OK** para salvá-los (consulte [Agentes de Replicação - Parâmetros de Configuração](#replication-agents-configuration-parameters) para obter mais detalhes sobre os parâmetros individuais).

>[!NOTE]
>
>Uma instalação padrão de AEM especifica `admin` como usuário para credenciais de transporte nos agentes de replicação padrão.
>
>Isso deve ser alterado para uma conta de usuário de replicação específica do site com os privilégios para replicar os caminhos necessários.

### Configurando Replicação Inversa {#configuring-reverse-replication}

A replicação inversa é usada para gerar o conteúdo do usuário em uma instância de publicação de volta a uma instância do autor. Isso é comumente usado para recursos como pesquisas e formulários de registro.

Por motivos de segurança, a maioria das topologias de rede não permite conexões *from* a &quot;Zona desmilitarizada&quot; (uma subrede que expõe os serviços externos a uma rede não confiável, como a Internet).

Como o ambiente de publicação geralmente está no DMZ, para obter conteúdo de volta ao ambiente do autor, a conexão deve ser iniciada a partir da instância do autor. Isso é feito com:

* um *caixa de saída* no ambiente de publicação, onde o conteúdo é colocado.
* um agente (publicar) no ambiente de criação que consulta periodicamente a caixa de saída para novo conteúdo.

>[!NOTE]
>
>Para AEM [Comunidades](/help/communities/overview.md), a replicação não é usada para conteúdo gerado pelo usuário em uma instância de publicação. Consulte [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md).

Para fazer isso, você precisa:

**Um agente de replicação inversa no ambiente de criação** Funciona como o componente ativo para coletar informações da caixa de saída no ambiente de publicação:

Se quiser usar a replicação inversa, verifique se esse agente está ativado.

![chlimage_1-23](assets/chlimage_1-23.png)

**Um agente de replicação inversa no ambiente de publicação (uma caixa de saída)** Esse é o elemento passivo, pois atua como uma &quot;caixa de saída&quot;. A entrada do usuário é colocada aqui, de onde é coletada pelo agente no ambiente de criação.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configuração da replicação para várias instâncias de publicação {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Somente o conteúdo é replicado - os dados do usuário não são (usuários, grupos de usuários e perfis de usuário).
>
>Para sincronizar os dados do usuário em várias instâncias de publicação, ative [Sincronização de usuários](/help/sites-administering/sync.md).

Após a instalação, um agente padrão já está configurado para replicação de conteúdo em uma instância de publicação em execução na porta 4503 do host local.

Para configurar a replicação de conteúdo para uma instância de publicação adicional, você precisa criar e configurar um novo agente de replicação:

1. Abra o **Ferramentas** em AEM.
1. Selecionar **Replicação**, em seguida **Agentes do autor** no painel esquerdo.
1. Selecionar **Novo...**.
1. Defina as **Título** e **Nome**, em seguida selecione **Agente de replicação**.
1. Clique em **Criar** para criar o novo agente.
1. Clique duas vezes no novo item de agente para abrir o painel de configuração.
1. Clique em **Editar** - o **Configurações do agente** será aberta - a caixa de diálogo **Tipo de serialização** já estiver definido como Padrão, deve permanecer assim.

   * No **Configurações** guia :

      * Ativar **Ativado**.
      * Insira um **Descrição**.
      * Defina as **Retardo de tentativa** para `60000`.

      * Deixe o **Tipo de serialização** as `Default`.
   * No **Transportes** guia :

      * Insira o URI necessário para a nova instância de publicação; por exemplo,
         `https://localhost:4504/bin/receive`.

      * Insira a conta de usuário específica do site usada para replicação.
      * Você pode configurar outros parâmetros, conforme necessário.


1. Clique em **OK** para salvar as configurações.

Em seguida, você pode testar a operação atualizando e publicando uma página no ambiente de criação.

As atualizações serão exibidas em todas as instâncias de publicação configuradas como acima.

Se encontrar algum problema, você pode verificar os logs na instância do autor. Dependendo do nível de detalhes necessário, também é possível definir a variável **Nível de log** para `Debug` usando o **Configurações do agente** como acima.

>[!NOTE]
>
>Isso pode ser combinado com o uso da variável [ID de usuário do agente](#agentuserid) para selecionar conteúdo diferente para replicar nos ambientes de publicação individuais. Para cada ambiente de publicação:
>
>1. Configure um agente de replicação para replicar para esse ambiente de publicação.
>1. Configurar uma conta de usuário; com os direitos de acesso necessários para ler o conteúdo que será replicado para esse ambiente de publicação específico.
>1. Atribua a conta de usuário como a **ID de usuário do agente** para o agente de replicação.

>


### Configurar um agente de limpeza do Dispatcher {#configuring-a-dispatcher-flush-agent}

Os agentes padrão são incluídos na instalação. No entanto, determinada configuração ainda é necessária e o mesmo se aplica se você estiver definindo um novo agente:

1. Abra o **Ferramentas** em AEM.
1. Clique em **Implantação**.
1. Selecionar **Replicação** e depois **Agentes na publicação**.
1. Clique duas vezes no **Liberação do Dispatcher** para abrir a visão geral.
1. Clique em **Editar** - o **Configurações do agente** será aberta:

   * No **Configurações** guia :

      * Ativar **Ativado**.
      * Insira um **Descrição**.
      * Deixe o **Tipo de serialização** as `Dispatcher Flush`ou defina como tal se estiver criando um novo agente.

      * (opcional) Selecione **Atualização de alias** para habilitar solicitações de invalidação de alias ou caminho personalizado para o Dispatcher.
   * No **Transportes** guia :

      * Insira o URI necessário para a nova instância de publicação; por exemplo,
         `https://localhost:80/dispatcher/invalidate.cache`.

      * Insira a conta de usuário específica do site usada para replicação.
      * Você pode configurar outros parâmetros, conforme necessário.

   Para agentes de Liberação do Dispatcher, a propriedade URI será usada somente se você usar entradas virtualhost baseadas em caminho para diferenciar entre farms, use esse campo para direcionar o farm para invalidar. Por exemplo, o farm nº 1 tem um host virtual de `www.mysite.com/path1/*`, e o farm nº 2 tem um host virtual de `www.mysite.com/path2/*`. Você pode usar um URL de `/path1/invalidate.cache` para direcionar o primeiro farm, e `/path2/invalidate.cache` para direcionar o segundo farm.

   >[!NOTE]
   >
   >Se tiver instalado o AEM em um contexto diferente do contexto padrão recomendado, será necessário configurar o [Cabeçalhos HTTP](#extended) no **Estendido** guia .

1. Clique em **OK** para salvar as alterações.
1. Retorne ao **Ferramentas** guia , daqui você pode **Ativar** o **Liberação do Dispatcher** agente (**Agentes na publicação**).

O **Liberação do Dispatcher** o agente de replicação não está ativo no autor. Você pode acessar a mesma página no ambiente de publicação usando o URI equivalente; por exemplo, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Controlando o acesso aos agentes de replicação {#controlling-access-to-replication-agents}

O acesso às páginas usadas para configurar os agentes de replicação pode ser controlado usando permissões de página de usuário e/ou grupo na `etc/replication` nó .

>[!NOTE]
>
>A configuração dessas permissões não afetará os usuários que replicam o conteúdo (por exemplo, do console Sites ou da opção de sidekick). A estrutura de replicação não usa a &quot;sessão de usuário&quot; do usuário atual para acessar agentes de replicação ao replicar páginas.

### Configurar seus agentes de replicação do CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>A criação de agentes de replicação só é compatível com o `/etc/replication` local do repositório. Isso é necessário para que as ACLs associadas sejam manipuladas adequadamente. A criação de um agente de replicação em outro local da árvore pode levar ao acesso não autorizado.

Vários parâmetros dos agentes de replicação podem ser configurados usando o CRXDE Lite.

Se você navegar para `/etc/replication` você pode ver os três nós a seguir:

* `agents.author`
* `agents.publish`
* `treeactivation`

Os dois `agents` mantenha as informações de configuração sobre o ambiente apropriado e elas só estarão ativas quando esse ambiente estiver em execução. Por exemplo, `agents.publish` serão usadas somente no ambiente de publicação. A captura de tela a seguir mostra o agente de publicação no ambiente do autor, conforme incluído AEM WCM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Monitorar os agentes de replicação {#monitoring-your-replication-agents}

Para monitorar um agente de replicação:

1. Acesse o **Ferramentas** em AEM.
1. Clique em **Replicação**.
1. Clique duas vezes no link para agentes do ambiente apropriado (no painel esquerdo ou direito); por exemplo **Agentes do autor**.

   A janela resultante mostra uma visão geral de todos os agentes de replicação para o ambiente do autor, incluindo o target e o status.

1. Clique no nome do agente apropriado (que é um link) para mostrar informações detalhadas sobre esse agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Aqui você pode:

   * Veja se o agente está ativado.
   * Consulte o target de qualquer replicação.
   * Veja se a fila de replicação está ativa no momento (habilitada).
   * Veja se há algum item na fila.
   * **Atualizar** ou **Limpar** para atualizar a exibição de entradas da fila; isso ajuda você a ver os itens entrando e deixando a fila.

   * **Exibir registro** para acessar o log de quaisquer ações pelo agente de replicação.
   * **Testar conexão** para a instância do target.
   * **Forçar nova tentativa** em qualquer item da fila, se necessário.

   >[!CAUTION]
   >
   >Não use o link &quot;Testar conexão&quot; para a Caixa de saída de replicação inversa em uma instância de publicação.
   >
   >
   >Se um teste de replicação for executado para uma fila da Caixa de saída, todos os itens mais antigos que a replicação de teste serão reprocessados com cada replicação inversa.
   >
   >
   >Se esses itens já existirem em uma fila, eles poderão ser encontrados com a seguinte consulta XPath JCR e deverão ser removidos.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replicação em lote {#batch-replication}

A replicação em lote não replica páginas ou ativos individuais, mas aguarda o primeiro limite dos dois, com base no tempo ou no tamanho, para ser acionado.

Em seguida, ele compacta todos os itens de replicação em um pacote, que é replicado como um único arquivo para o editor.

O editor descompactará todos os itens, salvá-los e relatará ao autor.

### Configuração da Replicação em Lote {#configuring-batch-replication}

1. Ir para `http://serveraddress:serverport/siteadmin`
1. Pressione a tecla **[!UICONTROL Ferramentas]** ícone no lado superior do ecrã
1. No painel de navegação esquerdo, vá para **[!UICONTROL Replicação - Agentes no Autor]** e clique duas vezes **[!UICONTROL Agente padrão]**.
   * Você também pode acessar o agente de replicação de publicação padrão indo diretamente para `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Pressione a tecla **[!UICONTROL Editar]** acima da fila de replicação.
1. Na janela a seguir, acesse o **[!UICONTROL Em lote]** guia :
   ![batchreplication](assets/batchreplication.png)
1. Configure o agente.

### Parâmetros {#parameters}

* `[!UICONTROL Enable Batch Mode]` - ativa ou desativa o modo de replicação em lote
* `[!UICONTROL Max Wait Time]` - Tempo máximo de espera até que uma solicitação em lote seja iniciada, em segundos. O padrão é 2 segundos.
* `[!UICONTROL Trigger Size]` - Inicia a replicação em lote quando esse limite de tamanho

## Recursos adicionais {#additional-resources}

Para obter detalhes sobre a solução de problemas, leia a seção [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md) página.
