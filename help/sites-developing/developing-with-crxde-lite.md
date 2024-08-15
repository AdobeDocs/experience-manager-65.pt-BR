---
title: Desenvolvimento com o CRXDE Lite
description: O CRXDE Lite está incorporado ao Adobe Experience Manager (AEM) e permite executar tarefas de desenvolvimento padrão no navegador
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 1%

---

# Desenvolvimento com o CRXDE Lite{#developing-with-crxde-lite}

Esta seção descreve como desenvolver o aplicativo Adobe Experience Manager (AEM) usando o CRXDE Lite.

Consulte a documentação de visão geral para obter mais informações sobre os diferentes ambientes de desenvolvimento disponíveis.

o CRXDE Lite é incorporado ao AEM e permite executar tarefas de desenvolvimento padrão no navegador. Com o CRXDE Lite, você pode criar um projeto, criar e editar arquivos (como .jsp e .java), pastas, modelos, componentes, caixas de diálogo, nós, propriedades e pacotes ao fazer logon.
O CRXDE Lite é recomendado quando você não tem acesso direto ao servidor AEM. Ou, quando você desenvolve uma aplicação estendendo ou modificando os componentes prontos para uso e pacotes Java™, ou quando não precisa de um depurador dedicado, autocompletar de código e realce de sintaxe.

>[!NOTE]
>
>A partir do AEM 6.5.5.0, o acesso anônimo ao CRXDE Lite não é mais possível.
>Os usuários são redirecionados para a tela de logon.


>[!NOTE]
>
>A Adobe AEM recomenda que você use as [Ferramentas do desenvolvedor para Eclipse](/help/sites-developing/aem-eclipse.md) e a [Extensão de Colchetes HTL do AEM](/help/sites-developing/aem-brackets.md) durante o desenvolvimento do projeto.

## Introdução ao CRXDE Lite {#getting-started-with-crxde-lite}

Para começar a usar o CRXDE Lite, proceda da seguinte maneira:

1. Instale o AEM.
1. Em seu navegador, digite `https://<host>:<port>/crx/de`. Por padrão, é `https://localhost:4502/crx/de`.
1. Digite seu **nome de usuário** e sua **senha**. Por padrão, é `admin` e `admin`.

1. Clique em **OK**.

No seu navegador, a interface de usuário do CRXDE Lite é semelhante a:

![chlimage_1-18](assets/crx-interface.jpg)

Agora você pode usar o CRXDE Lite para desenvolver seu aplicativo.

## Visão geral da interface do usuário {#overview-of-the-user-interface}

O CRXDE Lite oferece a seguinte funcionalidade:

<table>
 <tbody>
  <tr>
   <td>Barra do seletor superior</td>
   <td>Alterne rapidamente entre o CRXDE Lite, o Gerenciador de pacotes e o Compartilhamento de pacotes.</td>
  </tr>
  <tr>
   <td>Widget de caminho de nó</td>
   <td><p>Exibe o caminho para o nó selecionado.</p> <p>Você também pode usá-lo para pular para um nó, inserindo o caminho manualmente ou colando-o de outro lugar e pressionando Enter.</p> <p>Também oferece suporte à procura de nós com um nome de nó específico. Insira o nome do nó que deseja localizar e aguarde (ou pressione o símbolo de pesquisa no lado direito). Você pode tentar inserir, por exemplo, a sequência <em>oak</em> no widget para ver como ele funciona. Se um determinado nó ou nós forem carregados no painel do explorador, a lista será exibida, e você poderá selecionar o caminho e pressionar Enter para navegar até ele. Ele só funciona para os nós carregados no aplicativo cliente CRXDE no navegador. Se quiser pesquisar todo o repositório, use Ferramentas e, em seguida, Consulta.</p> </td>
  </tr>
  <tr>
   <td>Painel do Explorer</td>
   <td><p>Exibe uma árvore de todos os nós no repositório.</p> <p>Clique em um nó para exibir suas propriedades na guia <strong>Propriedades</strong>. Depois de clicar em um nó, você pode selecionar uma ação na barra de ferramentas. Clique no nó novamente para renomeá-lo.</p> <p>Filtro de navegação em árvore (ícone binocular): permite filtrar os nós no repositório cujo nome contém o texto de entrada. Aplica-se somente a nós que foram carregados localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Editar painel</td>
   <td><p>Guia <strong>Página inicial</strong>: permite pesquisar conteúdo e/ou documentação e acessar recursos do desenvolvedor (documentação, blog do desenvolvedor, base de dados de conhecimento) e suporte (página inicial e centro de suporte do Adobe).<br /> </p> <p>Clique duas vezes em um arquivo no painel do <strong>Explorer</strong> para que você possa exibir seu conteúdo. Por exemplo, um arquivo .jsp ou .java. Em seguida, você pode modificá-lo e salvar as alterações.</p> <p>Depois que um arquivo é editado no painel <strong>Editar</strong>, as seguintes ferramentas ficam disponíveis na barra de ferramentas:<br /> </p> - <strong>Mostrar na árvore: </strong>mostra o arquivo na árvore do repositório.<br /> - <strong>Pesquisar/Substituir...</strong>: pesquisar ou substituir.<br /> <br /> Clique duas vezes na linha de status do painel <strong>Editar</strong> para abrir a caixa de diálogo <strong>Ir para a linha</strong>, para que você possa inserir um número de linha específico para ir para.<br /> </td>
  </tr>
  <tr>
   <td>Guia Propriedades<br /> </td>
   <td>Exibe as propriedades do nó selecionado. Você pode adicionar novas propriedades ou excluir propriedades existentes.<br /> </td>
  </tr>
  <tr>
   <td>Guia Controle de acesso</td>
   <td><p>Exibir permissões com base no caminho, nível de repositório ou principal.</p> <p>As permissões são divididas em</p> <p>- <strong>Política de Controle de Acesso Aplicável</strong>: as políticas que podem ser aplicadas à seleção.</p> <p>- <strong>Políticas de Controle de Acesso Local</strong>: as políticas aplicadas localmente à seleção.</p> <p>- <strong>Políticas de Controle de Acesso Efetivas</strong>: as políticas aplicadas à seleção podem ser definidas localmente ou herdadas dos nós pai.</p> <p>Observação. Para conseguir ver as informações do Controle de acesso, o usuário conectado ao CRXDE Lite deve ter direitos de leitura para entradas de ACL. O usuário anônimo não pode ver essas informações por padrão: faça logon como administrador para ver as informações, por exemplo.</p> </td>
  </tr>
  <tr>
   <td>Guia Replicação</td>
   <td><p>Exiba o status de replicação do nó. É possível replicar e replicar e excluir o nó.</p> </td>
  </tr>
  <tr>
   <td>Guia Console<br /> </td>
   <td><p><strong>Logs do Servidor</strong>:</p> <p>Exibe mensagens de logs. Você pode configurar o nível de log, limpar o console, fixar na posição de rolagem selecionada e habilitar ou desabilitar a exibição de mensagens.<br /> </p> <p><strong>Controle de Versão</strong>:</p> <p>Exibe mensagens de controle de versão.<br /> </p> </td>
  </tr>
  <tr>
   <td>Guia Informações de Compilação<br /> </td>
   <td>Exibe informações quando um pacote está sendo compilado.<br /> </td>
  </tr>
  <tr>
   <td>Atualizar<br /> </td>
   <td>Atualiza a seleção. As alterações de outros usuários são atualizadas na sua visualização do repositório. As alterações que você fez não foram afetadas.<br /> </td>
  </tr>
  <tr>
   <td>Salvar Tudo</td>
   <td><p><strong>Salvar tudo</strong>:<br /> </p> <p>Salva todas as alterações feitas. Até que você clique em Salvar, as alterações serão temporárias e serão perdidas quando você sair do console.</p> <p><strong>Reverter</strong>:</p> <p>Descarta todas as alterações feitas no nó selecionado desde a última ação de salvamento e, em seguida, recarrega o estado do repositório para o nó selecionado.</p> <p><strong>Reverter tudo</strong>:</p> <p>Descarta todas as alterações feitas em todo o repositório desde a última ação de salvamento, e recarrega o estado do repositório.</p> </td>
  </tr>
  <tr>
   <td>Criar...<br /> </td>
   <td><p>Menu suspenso para criar o seguinte no nó selecionado:<br /> </p> <p>- <strong>Nó</strong>: um nó com um tipo de nó arbitrário<br /> </p> <p>- <strong>Arquivo</strong>: nó nt:file e seu subnó nt:resource</p> <p>- <strong>Pasta</strong>: nó nt:folder</p> <p>- <strong>Modelo</strong>: modelo AEM</p> <p>- <strong>Componente</strong>: componente AEM</p> <p>- <strong>Caixa de diálogo</strong>: caixa de diálogo AEM</p> </td>
  </tr>
  <tr>
   <td>Excluir<br /> </td>
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
   <td>Mover...<br /> </td>
   <td>Move o nó selecionado para o nó definido na caixa de diálogo.</td>
  </tr>
  <tr>
   <td>Renomear...<br /> </td>
   <td>Renomeia o nó selecionado.<br /> </td>
  </tr>
  <tr>
   <td>Combinações...<br /> </td>
   <td>Permite adicionar tipos de mixin ao tipo de nó. Os tipos de mixin são usados principalmente para adicionar recursos avançados, como controle de versão, controle de acesso, referência e bloqueio ao nó.</td>
  </tr>
  <tr>
   <td>Ferramentas<br /> </td>
   <td><p>Menu suspenso com as seguintes ferramentas:</p> <p>- <strong>Configuração do servidor...</strong>: para acessar o Felix Console.</p> <p>- <strong>Consulta...</strong>: para consultar o repositório.</p> <p>- <strong>Privilégios...</strong>: para abrir o gerenciamento de privilégios, onde você pode exibir e adicionar privilégios.</p> <p>- <strong>Testar Controle de Acesso...</strong>: um local onde você pode testar a permissão para um determinado caminho e/ou entidade de segurança.</p> <p>- <strong>Exportar Tipo de Nó</strong>: para exportar tipos de nó no sistema como notação cnd.</p> <p>- <strong>Importar Tipo de Nó...</strong>: para importar tipos de nó usando a notação cnd.</p> <p>- <strong>Instalar o SiteCatalyst Debugger...</strong>: instruções sobre como instalar o Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget de login<br /> </td>
   <td><p>Exibe os usuários conectados e o espaço de trabalho no qual eles estão conectados, por exemplo, admin@crx.default.</p> <p>Clique nele para fazer logon ou refazer logon como um usuário específico. Se você não especificar um espaço de trabalho para fazer logon, estará conectado ao espaço de trabalho padrão, crx.default.</p> <p>Se você deseja navegar no repositório como um usuário Anônimo, use <strong>anônimo</strong> como o nome de logon e qualquer senha (por exemplo, um espaço ou um ponto).<br /> </p> <p>Se sua autorização não for mais válida (por exemplo, ela expirou), o widget de logon exibirá "<strong>Não autorizado - Logon...</strong>". Clique para fazer logon novamente.</p> </td>
  </tr>
 </tbody>
</table>

## Criação de pastas {#creating-a-folder}

Para criar uma pasta com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse na pasta em que deseja criar a pasta, selecione **Criar...** e **Criar Pasta...**.

1. Insira a pasta **Name** e clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criação de um modelo {#creating-a-template}

Para criar um template com CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse na pasta onde deseja criar o modelo, selecione **Criar...** e **Criar Modelo...**.

1. Insira o **Rótulo**, **Título**, **Descrição**, **Tipo de Recurso** e **Classificação** do modelo. Clique em **Avançar**.

1. Esta etapa é opcional: defina os **Caminhos permitidos**. Clique em **Avançar**

1. Esta etapa é opcional: defina os **Pais permitidos**. Clique em **Avançar**.

1. Esta etapa é opcional: defina os **Filhos permitidos**. Clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

Ele cria:

* Um nó do tipo `cq:Template` com propriedades de Modelo

* Um nó filho do tipo `cq:PageContent` com propriedades de Conteúdo de Página

Você pode adicionar propriedades ao modelo: consulte a seção [Criação de uma Propriedade](#creating-a-property).

## Criação de um componente {#creating-a-component}

O recurso descrito aqui só estará disponível se o CQ5 estiver instalado, ou seja, se o tipo de nó `cq:Component` estiver disponível no repositório.

Para criar um componente com CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse na pasta onde deseja criar o componente, selecione **Criar...** e **Criar Componente...**.

1. Insira o **Rótulo**, **Título**, **Descrição**, **SuperTipo de Recurso** e **Grupo** do componente. Clique em **Avançar**.

1. Esta etapa é opcional: defina as propriedades do componente **É Contêiner,** **Sem Decoração**, **Nome da Célula** e **Caminho da Caixa de Diálogo**. Clique em **Avançar**.

1. Esta etapa é opcional: defina a propriedade do componente **Pais Permitidos**. Clique em **Avançar**.

1. Esta etapa é opcional: defina a propriedade do componente **Filhos Permitidos**. Clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

Ele cria:

* Um nó do tipo `cq:Component`
* Propriedades do componente
* Um componente script .jsp

## Criando uma caixa de diálogo {#creating-a-dialog}

Para criar uma caixa de diálogo com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse no componente em que deseja criar a caixa de diálogo, selecione **Criar ...**, depois **Criar Caixa de Diálogo ...**.

1. Insira o **Rótulo** e o **Título**. Clique em **OK**.

1. Clique em **Salvar tudo** l para salvar as alterações no servidor.

Ele cria uma caixa de diálogo com a seguinte estrutura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Agora você pode adaptar a caixa de diálogo às suas necessidades modificando propriedades ou criando nós.

Você também pode usar o Editor de diálogo para editar um diálogo. Clicar duas vezes no nó da caixa de diálogo no CRXDE Lite exibe o editor. Consulte [Editor da caixa de diálogo](/help/sites-developing/dialog-editor.md) para obter mais detalhes.

## Criando um nó {#creating-a-node}

Para criar um nó com CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse no nó em que deseja criar o nó, selecione **Criar ...**, depois **Criar Nó ...**.
1. Insira o **Nome** e o **Tipo**. Clique em **OK**.
1. Clique em **Salvar tudo** para salvar as alterações no servidor.

Agora você pode adaptar o nó às suas necessidades modificando propriedades ou criando nós.

>[!NOTE]
>
>A maioria das operações de edição, incluindo Criar nó, mantém todas as alterações na memória e só as armazena no repositório após salvar (por meio do botão &quot;Salvar tudo&quot;). No entanto, algumas operações, como mover, são automaticamente mantidas.
>
>A validação sobre se o nó recém-criado é permitido pelo tipo de nó do nó principal também é realizada pelo repositório JCR primeiro ao salvar as alterações. Se você receber uma mensagem de erro ao salvar um nó, verifique se a estrutura de conteúdo é válida (por exemplo, não é possível criar um nó `nt:unstructured` como filho do nó `nt:folder`).

## Criação de uma propriedade {#creating-a-property}

Para criar uma propriedade com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, selecione o nó ao qual deseja adicionar a nova propriedade.
1. Na guia **Propriedades** do painel inferior, digite o **Nome**, o **Tipo** e o **Valor**. Clique em **Adicionar**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criação de um script {#creating-a-script}

Para criar um script:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse no componente em que deseja criar o script, selecione **Criar ...**, depois **Criar arquivo ...**.

1. Insira o Arquivo **Nome**, incluindo sua extensão. Clique em **OK**.

1. O novo arquivo é aberto como uma guia no painel Editar.
1. Edite o arquivo.
1. Clique em **Salvar tudo** para salvar as alterações.

## Exportando e importando tipos de nós {#exporting-and-importing-node-types}

Com o CRXDE Lite, você pode importar e/ou exportar definições de tipo de nó na [notação CND (Compact Namespace and Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar uma definição de tipo de nó:

1. Abra o CRXDE Lite no navegador.
1. Selecione o nó desejado.
1. Selecione **Ferramentas** e **Exportar Tipo de Nó**.

1. A definição, em notação de contagem, é exibida no navegador. Salve as informações, se necessário.

Para importar uma definição de tipo de nó:

1. Abra o CRXDE Lite no navegador.
1. Selecione **Ferramentas** e **Importar Tipo de Nó...**.

1. Insira a notação CND para a definição na caixa de texto.
1. Marque **Permitir atualização** se estiver atualizando uma definição existente.
1. Clique em **Importar**.

## Logs {#logging}

Com o CRXDE Lite, você pode exibir o arquivo `error.log` que está no sistema de arquivos em `<crx-install-dir>/crx-quickstart/server/logs` e filtrá-lo com o nível de log apropriado. Proceda da seguinte forma:

1. Abra o CRXDE Lite no navegador.
1. Na guia **Console**, na parte inferior da janela, no menu suspenso à direita, selecione **Logs do Servidor**.

1. Clique no ícone **Parar** para exibir as mensagens.

É possível:

* Ajuste os parâmetros de log no Felix Console clicando no ícone **Configurações de Log**.
* Limpe as mensagens clicando no ícone **Pincel**.
* Fixar a mensagem na seleção clicando no ícone **Fixar**.
* Habilite ou desabilite a exibição de mensagens clicando no ícone **Parar**.

## Controle de acesso {#access-control}

>[!NOTE]
>
>Consulte [Administração de Usuários, Grupos e Direitos de Acesso](/help/sites-administering/user-group-ac-admin.md) para obter mais informações.
