---
title: Desenvolvimento com CRXDE Lite
seo-title: Desenvolvimento com CRXDE Lite
description: O CRXDE Lite está incorporado ao AEM e permite que você execute tarefas de desenvolvimento padrão no navegador
seo-description: O CRXDE Lite está incorporado ao AEM e permite que você execute tarefas de desenvolvimento padrão no navegador
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: cb141914428f42a9755b5479ab1652c8ca51f640
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 5%

---


# Desenvolver com CRXDE Lite{#developing-with-crxde-lite}

Esta seção descreve como desenvolver seu aplicativo AEM usando o CRXDE Lite.

Consulte a documentação de visão geral para obter mais informações sobre os diferentes ambientes de desenvolvimento disponíveis.

O CRXDE Lite está incorporado ao AEM e permite que você execute tarefas de desenvolvimento padrão no navegador. Com o CRXDE Lite, você pode criar um projeto, criar e editar arquivos (como .jsp e .java), pastas, modelos, componentes, caixas de diálogo, nós, propriedades e pacotes durante o registro.
É recomendado o CRXDE Lite quando você não tem acesso direto ao servidor AEM, quando você desenvolve um aplicativo, estendendo ou modificando os componentes predefinidos e os pacotes Java ou quando não precisa de um depurador dedicado, finalização de código e realce de sintaxe.

>[!NOTE]
>
>A partir AEM 6.5.5.0, o acesso anônimo ao CRXDE Lite não é mais possível.
>Os usuários são redirecionados para a tela de logon.


>[!NOTE]
>
>É recomendável usar as [AEM Ferramentas do desenvolvedor para Eclipse](/help/sites-developing/aem-eclipse.md) e as [AEM HTML Brackets Extension](/help/sites-developing/aem-brackets.md) durante o desenvolvimento do projeto.

## Introdução ao CRXDE Lite {#getting-started-with-crxde-lite}

Para começar a usar o CRXDE Lite, proceda da seguinte forma:

1. Instale o AEM.
1. Em seu navegador, digite `https://<host>:<port>/crx/de`. Por padrão, é `https://localhost:4502/crx/de`.
1. Digite seu **nome de usuário** e **senha**. Por padrão, é `admin` e `admin`.

1. Clique em **OK**.

A interface do usuário do CRXDE Lite é exibida da seguinte maneira no seu navegador:

![chlimage_1-18](assets/crx-interface.jpg)

Agora você pode usar o CRXDE Lite para desenvolver seu aplicativo.

## Visão geral da interface do usuário {#overview-of-the-user-interface}

CRXDE Lite oferta a seguinte funcionalidade:

<table>
 <tbody>
  <tr>
   <td>Barra do comutador superior</td>
   <td>Permite alternar rapidamente entre o CRXDE Lite, o Gerenciador de pacotes e o Compartilhamento de pacotes.</td>
  </tr>
  <tr>
   <td>Widget de caminho de nó</td>
   <td><p>Exibe o caminho para o nó selecionado no momento.</p> <p>Você também pode usá-lo para pular para um nó, inserindo o caminho manualmente ou colando-o de outro lugar e pressionando Enter.</p> <p>Também oferece suporte para procurar nós com nome de nó específico. Digite o nome do nó que você deseja localizar e aguarde (ou pressione o símbolo de pesquisa no lado direito). Você pode tentar inserir, por exemplo, a string <em>oak</em> no widget para ver como ele funciona. Se um determinado nó ou nós forem carregados no painel explorador, a lista será exibida e você poderá selecionar o caminho e pressionar Enter para navegar até ele. Observe que ele só funciona para os nós carregados no momento no aplicativo cliente CRXDE no navegador. Se quiser pesquisar o repositório inteiro, use Ferramentas e, em seguida, Query.</p> </td>
  </tr>
  <tr>
   <td>Painel do Explorer</td>
   <td><p>Exibe uma árvore de todos os nós no repositório.</p> <p>Clique em um nó para exibir suas propriedades na guia <strong>Propriedades</strong>. Depois de clicar em um nó, você pode selecionar uma ação na barra de ferramentas. Clique no nó novamente para renomeá-lo.</p> <p>Filtro de navegação da árvore (ícone binocular): permite que você filtre os nós no repositório para os quais o nome contém o texto de entrada. Ela se aplica somente aos nós que foram carregados localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Painel Editar</td>
   <td><p><strong></strong> Hometab: permite que você pesquise conteúdo e/ou documentação e acesse recursos do desenvolvedor (documentação, blog do desenvolvedor, base de conhecimento) e suporte (Adobe homepage e centro de suporte).<br /> </p> <p>Duplo clique em um arquivo no painel <strong>Explorer</strong> para exibir seu conteúdo; como, por exemplo, um arquivo .jsp ou .java. Em seguida, você pode modificá-la e salvar as alterações.</p> <p>Depois que um arquivo é editado no painel <strong>Editar</strong>, as seguintes ferramentas ficam disponíveis na barra de ferramentas:<br /> </p> - <strong>Mostrar na árvore: </strong>mostra o arquivo na árvore do repositório.<br /> -  <strong>Pesquisar/Substituir ...</strong>: faça pesquisa ou substitua.<br /> <br /> Clique com o duplo na linha de status do  <strong></strong> painel de edição para abrir a caixa de diálogo  <strong>Ir para </strong> linedialogia, para que você possa inserir um número de linha específico.<br /> </td>
  </tr>
  <tr>
   <td>Guia Propriedades<br /> </td>
   <td>Exibe as propriedades do nó selecionado. Você pode adicionar novas propriedades ou excluir as existentes.<br /> </td>
  </tr>
  <tr>
   <td>guia controle de acesso</td>
   <td><p>Exibir permissões com base no caminho atual, no nível do repositório ou no principal.</p> <p>As permissões são divididas em</p> <p>- <strong>Política de Controle de acesso aplicável</strong>: As políticas que podem ser aplicadas à seleção atual.</p> <p>- <strong>Políticas de Controle de acesso local</strong>: As políticas atuais aplicadas localmente à seleção atual.</p> <p>- <strong>Políticas de Controle de acesso eficazes</strong>: As políticas atuais aplicadas à seleção atual podem ser definidas localmente ou herdadas dos nós pais.</p> <p>Nota. Para poder ver as informações do Controle de acesso, o usuário conectado ao CRXDE Lite deve ter direitos de leitura das entradas ACL. O usuário anônimo não pode ver essas informações por padrão - faça logon como, por exemplo, administrador para ver as informações.</p> </td>
  </tr>
  <tr>
   <td>Guia Replicação</td>
   <td><p>Exibir o status de replicação do nó atual. É possível replicar e excluir o nó atual.</p> </td>
  </tr>
  <tr>
   <td>Guia Console<br /> </td>
   <td><p><strong>Logs do servidor</strong>:</p> <p>Exibe mensagens de registro. Você pode configurar o nível de log, limpar o console, fixar na posição de rolagem selecionada e ativar/desativar a exibição de mensagens.<br /> </p> <p><strong>Controle da versão</strong>:</p> <p>Exibe mensagens de controle de versão.<br /> </p> </td>
  </tr>
  <tr>
   <td>Guia Informações da compilação<br /> </td>
   <td>Exibe informações quando um pacote está sendo criado.<br /> </td>
  </tr>
  <tr>
   <td>Atualizar<br /> </td>
   <td>Atualiza a seleção atual. As alterações de outros usuários são atualizadas na visualização do repositório. As alterações efetuadas não são afetadas.<br /> </td>
  </tr>
  <tr>
   <td>Salvar Tudo</td>
   <td><p><strong>Salvar Tudo</strong>:<br /> </p> <p>Salva todas as alterações feitas. Até que você clique em salvar, as alterações serão temporárias e serão perdidas quando você sair do console.</p> <p><strong>Reverter</strong>:</p> <p>Descarta todas as alterações feitas no nó selecionado desde a última ação de salvamento e, em seguida, recarrega o estado atual do repositório para o nó selecionado.</p> <p><strong>Reverter tudo</strong>:</p> <p>Descarta todas as alterações feitas em todo o repositório desde a última ação de salvar e, em seguida, carrega o estado atual do repositório.</p> </td>
  </tr>
  <tr>
   <td>Criar ...<br /> </td>
   <td><p>Menu suspenso para criar o seguinte sob o nó selecionado:<br /> </p> <p>- <strong>Nó</strong>: um nó com um tipo de nó arbitrário<br /> </p> <p>- <strong>Ficheiro</strong>: nt:nó de arquivo e seu subnó nt:resource</p> <p>- <strong>Pasta</strong>: nt:nó de pasta</p> <p>- <strong>Modelo</strong>: Modelo AEM</p> <p>- <strong>Componente</strong>: componente AEM</p> <p>- <strong>Diálogo</strong>: Caixa de diálogo AEM</p> </td>
  </tr>
  <tr>
   <td>Exclua<br /> </td>
   <td>Exclui o nó selecionado.<br /> </td>
  </tr>
  <tr>
   <td>Copiar</td>
   <td>Copia o nó selecionado.<br /> </td>
  </tr>
  <tr>
   <td>Colar<br /> </td>
   <td>Cola o nó copiado sob o nó selecionado.<br /> </td>
  </tr>
  <tr>
   <td>Mover ...<br /> </td>
   <td>Move o nó selecionado para o nó definido pela caixa de diálogo.</td>
  </tr>
  <tr>
   <td>Renomeie ...<br /> </td>
   <td>Renomeia o nó selecionado.<br /> </td>
  </tr>
  <tr>
   <td>Misturas ...<br /> </td>
   <td>Permite adicionar tipos de mixagem ao tipo de nó. Os tipos de mixin são usados para adicionar recursos avançados, como controle de versão, controle de acesso, referência e bloqueio ao nó.</td>
  </tr>
  <tr>
   <td>Ferramentas<br /> </td>
   <td><p>Menu suspenso com as seguintes ferramentas:</p> <p>- <strong>Configuração do servidor ...</strong>: para acessar o Console do Felix.</p> <p>- <strong>Query ...</strong>: para query do repositório.</p> <p>- <strong>Privilégios ...</strong>: para abrir o gerenciamento de privilégios, onde você pode visualização e adicionar privilégios.</p> <p>- <strong>Controle de acesso de ensaio ...</strong>: um local onde você pode testar a permissão para determinado caminho e/ou principal.</p> <p>- <strong>Exportar Tipo de Nó</strong>: para exportar os tipos de nó no sistema como notação cnd.</p> <p>- <strong>Importar Tipo de Nó ...</strong>: para importar tipos de nó usando a notação cnd.</p> <p>- <strong>Instale o Depurador de SiteCatalysts ...</strong>: instruções sobre como instalar o Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget de logon<br /> </td>
   <td><p>Exibe os usuários conectados no momento e o espaço de trabalho em que eles estão conectados, por exemplo, admin@crx.default.</p> <p>Clique nele para fazer logon ou login novamente como um usuário específico. Se você não especificar um espaço de trabalho para fazer logon, você estará conectado ao espaço de trabalho padrão, crx.default.</p> <p>Se você quiser navegar no repositório como usuário Anônimo, use <strong>anônimo</strong> como nome de logon e qualquer senha (por exemplo, um espaço ou um ponto).<br /> </p> <p>Se sua autorização não for mais válida (por exemplo, ela expirou), o widget de logon exibirá "<strong>Não autorizado - Logon...</strong>". Clique nele para fazer logon novamente.</p> </td>
  </tr>
 </tbody>
</table>

## Criação de uma pasta {#creating-a-folder}

Para criar uma pasta com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel de Navegação, clique com o botão direito do mouse na pasta sob a qual deseja criar a nova pasta, selecione **Criar ...**, em seguida **Criar pasta ...**.

1. Digite a pasta **Nome** e clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criando um Modelo {#creating-a-template}

Para criar um modelo com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel de Navegação, clique com o botão direito do mouse na pasta em que deseja criar o modelo, selecione **Criar ...**, em seguida **Criar modelo ...**.

1. Insira **Label**, **Title**, **Descrição**, **Tipo de Recurso** e **Classificação** do modelo. Clique em **Avançar**.

1. Esta etapa é opcional: defina **Caminhos permitidos**. Clique em **Avançar**

1. Esta etapa é opcional: defina **Pais permitidos**. Clique em **Avançar**.

1. Esta etapa é opcional: defina **Filhos permitidos**. Clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

Cria:

* Um nó do tipo `cq:Template` com propriedades de Modelo

* Um nó filho do tipo `cq:PageContent` com propriedades de Conteúdo da Página

É possível adicionar propriedades ao modelo: consulte a seção [Criação de uma propriedade](#creating-a-property).

## Criação de um componente {#creating-a-component}

O recurso descrito aqui só estará disponível se o CQ5 estiver instalado, isto é, se o tipo de nó `cq:Component` estiver disponível no repositório.

Para criar um componente com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel de Navegação, clique com o botão direito do mouse na pasta em que deseja criar o componente, selecione **Criar ...**, em seguida **Criar componente ...**.

1. Insira **Label**, **Title**, **Descrição**, **Super Resource Type** e **Group** do componente. Clique em **Avançar**.

1. Esta etapa é opcional: defina as propriedades do componente **É Container,** **Sem decoração**, **Nome da célula** e **Caminho da caixa de diálogo**. Clique em **Avançar**.

1. Esta etapa é opcional: defina a propriedade do componente **Pais permitidos**. Clique em **Avançar**.

1. Esta etapa é opcional: defina a propriedade do componente **Filhos permitidos**. Clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

Cria:

* Um nó do tipo `cq:Component`
* Propriedades do componente
* Um script .jsp componente

## Criando uma caixa de diálogo {#creating-a-dialog}

Para criar uma caixa de diálogo com o CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel de Navegação, clique com o botão direito do mouse no componente no qual deseja criar a caixa de diálogo, selecione **Criar ...**, em seguida **Criar caixa de diálogo ...**.

1. Insira **Label** e **Title**. Clique em **OK**.

1. Clique em **Salvar Al** l para salvar as alterações no servidor.

Cria um diálogo com a seguinte estrutura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Agora você pode adaptar a caixa de diálogo às suas necessidades modificando as propriedades ou criando novos nós.

Você também pode usar o Editor de diálogo para editar uma caixa de diálogo. O duplo que clicar no nó de diálogo no CRXDE Lite exibirá o editor. Mais informações sobre o Editor de diálogo podem ser encontradas [aqui](/help/sites-developing/dialog-editor.md).

## Criação de um nó {#creating-a-node}

Para criar um nó com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel Navegação, clique com o botão direito do mouse no nó onde deseja criar o novo nó, selecione **Criar ...**, em seguida **Criar nó ...**.
1. Digite **Name** e **Type**. Clique em **OK**.
1. Clique em **Salvar tudo** para salvar as alterações no servidor.

Agora você pode adaptar o nó às suas necessidades modificando as propriedades ou criando novos nós.

>[!NOTE]
>
>A maioria das operações de edição, incluindo Criar nó, mantém todas as alterações na memória e só as armazena no repositório ao salvar (por meio do botão &quot;Salvar tudo&quot;). No entanto, algumas operações, como mover, são automaticamente persistentes.
>
>A validação para determinar se o nó recém-criado é permitido pelo tipo de nó do nó pai também é realizada pelo repositório JCR primeiro ao salvar alterações. Se você receber uma mensagem de erro ao salvar um nó, verifique se a estrutura de conteúdo é válida (por exemplo, não é possível criar um nó `nt:unstructured` como filho do nó `nt:folder`).

## Criação de uma propriedade {#creating-a-property}

Para criar uma propriedade com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel Navegação, selecione o nó no qual deseja adicionar a nova propriedade.
1. Na guia **Propriedades** no painel inferior, digite **Nome**, **Tipo** e **Valor**. Clique em **Adicionar**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criação de um script {#creating-a-script}

Para criar um novo script:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel de Navegação, clique com o botão direito do mouse no componente no qual deseja criar o script, selecione **Criar ...**, em seguida **Criar arquivo ...**.

1. Insira o Arquivo **Nome**, incluindo sua extensão. Clique em **OK**.

1. O novo arquivo é aberto como uma guia no painel Editar.
1. Edite o arquivo.
1. Clique em **Salvar tudo** para salvar as alterações.

## Exportando e importando tipos de nó {#exporting-and-importing-node-types}

Com o CRXDE Lite, é possível importar e/ou exportar definições de tipo de nó na notação [CND (Namespace compacta e Definição de tipo de nó)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar uma definição de tipo de nó:

1. Abra o CRXDE Lite no seu navegador da 
1. Selecione o nó desejado.
1. Selecione **Ferramentas** em seguida **Exportar tipo de nó**.

1. A definição, em notação cnd, será exibida no seu navegador. Salve as informações, se necessário.

Para importar uma definição de tipo de nó:

1. Abra o CRXDE Lite no seu navegador da 
1. Selecione **Ferramentas** e **Importar Tipo de Nó...**.

1. Insira a notação CND para a definição na caixa de texto.
1. Marque **Permitir atualização** se estiver atualizando uma definição existente.
1. Clique em **Importar**.

## Logs {#logging}

Com o CRXDE Lite, você pode exibir o arquivo `error.log` localizado no sistema de arquivos em `<crx-install-dir>/crx-quickstart/server/logs` e filtrá-lo com o nível de log apropriado. Proceda do seguinte modo:

1. Abra o CRXDE Lite no seu navegador da 
1. Na guia **Console** na parte inferior da janela, no menu suspenso à direita, selecione **Logs de servidor**.

1. Clique no ícone **Parar** para exibir as mensagens.

É possível:

* Ajuste os parâmetros de log no Console do Felix clicando no ícone **Configurações de registro**.
* Limpe as mensagens clicando no ícone **Pincel**.
* Fixar a mensagem na seleção atual clicando no ícone **Pino**.
* Ative ou desative a exibição de mensagens clicando no ícone **Parar**.

## Controle de acesso {#access-control}

>[!NOTE]
>
>Consulte [Administração de usuários, grupos e direitos de acesso](/help/sites-administering/user-group-ac-admin.md) para obter mais informações.
