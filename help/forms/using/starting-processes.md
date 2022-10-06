---
title: Iniciando processos
seo-title: Starting processes
description: Como usar a área de trabalho do LiveCycle AEM Forms — selecione processos, adicione notas e anexos, salve cópias de rascunho e adicione aos favoritos.
seo-description: How to use LiveCycle AEM Forms workspace--select processes, add notes and attachments, save draft copies, and add to favorites.
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
exl-id: b2a6ba3a-0f4c-44b1-8f9a-c15c6fb8c305
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# Iniciando processos {#starting-processes}

O espaço de trabalho do AEM Forms organiza processos pelas categorias configuradas pelo administrador ou pelo designer de processos. Você também pode colocar processos que utiliza com frequência na categoria Favoritos para encontrá-los rapidamente.

Ao iniciar um processo, pode ser necessário preencher um formulário para iniciar um processo de negócios que o fluxo de trabalho do AEM Forms controla. Se um formulário usar o Processo de preparação de dados, algumas informações poderão ser preenchidas previamente em um formulário em branco, quando um novo processo for iniciado.

Por exemplo, você deseja comprar um novo monitor de computador e, portanto, iniciar um processo chamado *Pedido de compra*. Quando você inicia o processo, um formulário é aberto e solicita detalhes sobre o item a ser solicitado. Seu nome, número de funcionário e nome do gerente podem já estar pré-preenchidos no formulário. Ao enviar a solicitação, um processo de negócios é iniciado. Com base na definição do processo, o servidor encaminha automaticamente a solicitação para o gerente. A tarefa começa a aparecer na lista de Tarefas do gerente. Quando o gerente aprova a solicitação, o workflow do forms encaminha a solicitação ao departamento de compras e envia uma notificação por email.

## Selecionar processos para iniciar {#selecting-processes-to-start}

Você pode selecionar um processo para iniciá-lo ou exibir mais informações sobre ele.

Ao selecionar um processo para iniciar, talvez seja necessário preencher um formulário associado a esse processo. O envio do formulário inicia o processo.

O Forms em vários tipos de formatos de arquivo são suportados, incluindo Adobe PDF, HTML e SWF file. Um formulário pode ter a aparência de um formulário tradicional, impresso ou baseado na Web, ou pode guiá-lo por uma série de painéis no estilo de assistente para coletar informações.

Se o formulário e o processo permitirem, também é possível salvar o formulário offline, preenchê-lo e enviá-lo para concluir a tarefa. Quando o formulário for enviado, seu cliente de email será iniciado com o endereço de email do servidor apropriado, se o ponto final do email estiver configurado. Em seguida, é possível enviar o formulário preenchido para o servidor por email.

Ao selecionar um processo, a guia Formulário e a guia Detalhes são exibidas. Se o processo permitir que você adicione notas ou anexos, a guia Anexos e a guia Notas também serão exibidas. Se você também tiver configurado o url de resumo com o processo, a guia Resumo também será exibida. A guia Forms exibe o formulário associado e a guia Details exibe informações sobre a tarefa atual e o processo do qual faz parte.

### Iniciar um processo de negócios {#start-a-business-process}

1. Na página Iniciar processo , na lista à esquerda, selecione uma categoria. Todos os processos aos quais você tem acesso na categoria aparecem à direita.

   >[!NOTE]
   >
   >Se o painel Categorias for recolhido, clique em &quot;Abrir Categorias&quot;, na área superior esquerda do espaço de trabalho do AEM Forms, para abrir o painel.

1. Selecione um processo clicando em uma tarefa. O formulário associado ao processo é aberto na guia Formulário .

   Cada formulário em um processo tem um URL exclusivo. Você pode usar o URL único para iniciar diretamente o HTML Workspace com o processo e o formulário específicos. O formato do URL é https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;applicationname>%2F&lt;processname>. O &lt;applicationname>%2F&lt;processname> string é sempre codificada por URL. Um exemplo de URL é http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. A cadeia de caracteres ApplicationName%2FProcessName no exemplo é codificada por URL.

1. Preencha o formulário de acordo com as instruções fornecidas. Se necessário, clique em **Maximizar** para aumentar a área visível do formulário.
1. Se a guia Attachments estiver disponível, adicione anexos conforme necessário.
1. Se a guia Notas estiver disponível, forneça as notas necessárias.
1. Execute uma destas etapas:

   * Clique no botão Enviar no formulário, se ele tiver um botão Enviar.
   * Clique em Concluído abaixo do formulário, se ele não tiver um botão Enviar.

   O Process Management inicia o processo e encaminha o formulário para as listas de tarefas das pessoas apropriadas que precisam concluir a próxima tarefa no processo.

   Se for necessário fechar um formulário antes de enviá-lo e sem perder os dados inseridos, salve um rascunho e complete-o posteriormente, se o processo permitir. Se o formulário e o processo permitirem, também é possível clicar em **Offline** e depois envie-o do Adobe® Reader® ou Adobe® Acrobat® Professional ou Acrobat Standard.

   >[!NOTE]
   >
   >A opção offline está disponível somente para PDF forms.

## Adição de notas e anexos {#adding-notes-and-attachments}

É possível adicionar notas e anexos de arquivo a um processo, se o processo permitir. Você pode fornecer permissões para outros usuários que participam do processo para visualizar, atualizar e excluir as notas ou anexos.

### Adicionar uma nota {#add-a-note}

É possível adicionar várias notas, editar as notas escritas e excluí-las. Cada nota tem um título, uma descrição e uma permissão de acesso associada a ela. É possível definir uma das seguintes permissões de acesso em uma observação:

* Somente leitura (a permissão padrão)
* Ler/Editar/Excluir
* Ler/Editar
* Ler/Excluir
* Sem acesso

1. Abra uma tarefa e clique no botão **Notas** , se o processo permitir.
1. Digite um título para a nota no **Título** e digite o texto da nota no **Observação** caixa.
1. Selecione o **Permissões** nível da nota para outros usuários que participam do processo.
1. Clique em **OK**. Um arquivo de texto que contém sua nota é anexado ao formulário. Você pode atualizar uma nota clicando nela e modificando diretamente o texto. É possível excluir uma nota clicando no botão **Excluir** botão ![Imagem da lata de lixo](assets/icondelete.png) ao lado da nota.

### Adicionar um anexo {#add-an-attachment}

Você também pode adicionar seus comentários sobre o anexo. Você pode definir uma das seguintes permissões de acesso em um anexo:

* Somente leitura (a permissão padrão)
* Ler/Editar/Excluir
* Ler/Editar
* Ler/Excluir
* Sem acesso

1. Clique no botão **Anexos** e selecione **Anexo**.
1. Clique em **Procurar** para selecionar o arquivo a ser anexado.
1. Selecione o **Permissões** nível do anexo para outros usuários que participam do processo. Se você selecionar **Ler**, outros usuários podem salvar o arquivo localmente. Se você selecionar uma das permissões de edição, outros usuários também poderão fazer upload de um novo arquivo para substituir seu anexo.
1. Clique em **OK**. O arquivo é anexado ao formulário. Você pode excluir um arquivo clicando no botão **Excluir** botão ![Imagem da lata de lixo](assets/icondelete.png) ao lado do anexo.

## Salvar cópias de rascunho de formulários {#saving-draft-copies-of-forms}

Se for necessário preencher e enviar um formulário posteriormente, é possível salvar uma cópia de rascunho de um formulário para não perder o trabalho existente. As cópias de rascunho são adicionadas à categoria Rascunhos na página Tarefas.

Após reabrir e enviar um formulário de rascunho, o rascunho é removido da categoria Rascunhos .

Além disso, é possível configurar o espaço de trabalho para salvar automaticamente as informações inseridas por um usuário como rascunho. Para obter mais informações, consulte [Gerenciamento de preferências](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>O botão Salvar não está disponível para alguns formulários, dependendo do processo ao qual ele está associado.

### Salvar uma cópia de rascunho {#save-a-draft-copy}

1. Clique em **Salvar** no canto inferior esquerdo de qualquer guia. O formulário é adicionado à categoria Rascunhos na página A fazer. Todas as alterações feitas no formulário são salvas.

### Reabrir uma cópia de rascunho {#reopen-a-draft-copy}

1. Na página Para fazer , selecione o **Rascunhos** e clique na cópia de rascunho do formulário.

   Se o formulário contiver uma série de painéis, talvez seja necessário ir para o painel em que você terminou a última sessão.

## Adicionar processos à categoria Favoritos {#adding-processes-to-the-favorites-category}

É possível adicionar qualquer processo à categoria Favoritos . Ao configurar os favoritos, é possível agrupar todos os processos que você começa frequentemente em uma única categoria para encontrá-los rapidamente.

>[!NOTE]
>
>Se você normalmente inicia processos ao usar o AEM Forms workspace, é possível definir a preferência de Local inicial para exibir automaticamente a categoria Favoritos ao iniciar o AEM Forms workspace. Para obter mais detalhes, consulte Gerenciamento de preferências em [Introdução ao AEM Forms workspace](/help/forms/using/getting-started-livecycle-html-workspace.md).

Para marcar um processo como favorito, selecione a tarefa em sua categoria e clique na estrela vazia. A estrela fica de ouro. Para desmarcar um processo como favorito, clique novamente na estrela dourada.
