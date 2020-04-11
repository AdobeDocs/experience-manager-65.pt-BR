---
title: Iniciando processos
seo-title: Iniciando processos
description: 'Como usar a área de trabalho do LiveCycle AEM Forms: selecionar processos, adicionar notas e anexos, salvar cópias de rascunho e adicionar aos favoritos.'
seo-description: 'Como usar a área de trabalho do LiveCycle AEM Forms: selecionar processos, adicionar notas e anexos, salvar cópias de rascunho e adicionar aos favoritos.'
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Iniciando processos {#starting-processes}

A área de trabalho do AEM Forms organiza processos pelas categorias que o administrador ou o designer de processos configura. Também é possível colocar processos que você usa com frequência em sua categoria Favoritos para localizá-los rapidamente.

Ao start de um processo, talvez seja necessário preencher um formulário para start de um processo de negócios que o fluxo de trabalho do AEM Forms controla. Se um formulário usar o Processo de preparação de dados, algumas informações poderão ser preenchidas previamente em um formulário em branco, quando um novo processo for iniciado.

Por exemplo, você deseja comprar um novo monitor de computador e, portanto, start um processo chamado Pedido *de compra*. Quando você start o processo, um formulário é aberto e solicita detalhes sobre o item a ser solicitado. Seu nome, o número do funcionário e o nome do gerente já podem ser pré-preenchidos no formulário. Quando você submete a solicitação, um processo de negócios é iniciado. Com base na definição do processo, o servidor automaticamente encaminha a solicitação para o seu gerente. Os start de tarefa que aparecem na lista de tarefas do seu gerente. Quando o gerente aprova a solicitação, o fluxo de trabalho dos formulários encaminha a solicitação para o departamento de compras e envia uma notificação por email.

## Selecionar processos para start {#selecting-processes-to-start}

Você pode selecionar um processo para start ou para visualização de mais informações sobre ele.

Ao selecionar um processo a ser start, talvez seja necessário preencher um formulário associado a esse processo. Enviar o formulário start o processo.

Os formulários em vários tipos de formatos de arquivo são suportados, incluindo Adobe PDF, HTML e arquivo SWF. Um formulário pode se parecer com um formulário tradicional impresso ou baseado na Web ou pode orientá-lo por uma série de painéis no estilo assistente para coletar informações.

Se o formulário e o processo permitirem, você também poderá salvar o formulário off-line, preenchê-lo e enviá-lo para completar a tarefa. Quando o formulário for enviado, seu cliente de e-mail será iniciado com o endereço de e-mail do servidor apropriado, se o ponto final do e-mail estiver configurado. Em seguida, é possível enviar o formulário preenchido para o servidor por email.

Quando um processo é selecionado, as guias Formulário e Detalhes são exibidas. Se o processo permitir que você adicione notas ou anexos, a guia Anexos e a guia Notas também serão exibidas. Se você também tiver configurado o url de resumo com o processo, a guia Resumo também será exibida. A guia Formulários exibe o formulário associado e a guia Detalhes exibe informações sobre a tarefa atual e o processo do qual ela faz parte.

### Start de um processo de negócios {#start-a-business-process}

1. Na página Processo de Start, na lista à esquerda, selecione uma categoria. Todos os processos aos quais você tem acesso na categoria são exibidos à direita.

   >[!NOTE]
   >
   >Se o painel Categoria for recolhido, clique em &#39;Abrir Categoria&#39;, na área superior esquerda da área de trabalho do AEM Forms, para abrir o painel.

1. Selecione um processo clicando em uma tarefa. O formulário associado ao processo é aberto na guia Formulário.

   Cada formulário em um processo tem um URL exclusivo. Você pode usar o URL exclusivo para iniciar diretamente o espaço de trabalho HTML com o processo e o formulário específicos. O formato do URL é https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;ApplicationName>%2F&lt;ProcessName>. A cadeia de caracteres &lt;ApplicationName>%2F&lt;ProcessName> sempre tem codificação de URL. Um URL de exemplo é http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. A cadeia ApplicationName%2FProcessName no exemplo é codificada por URL.

1. Preencha o formulário de acordo com as instruções fornecidas com ele. Se necessário, clique em **Maximizar** para aumentar a área visível do formulário.
1. Se a guia Anexos estiver disponível, adicione anexos conforme necessário.
1. Se a guia Notas estiver disponível, forneça as notas conforme necessário.
1. Execute uma destas etapas:

   * Clique no botão Enviar no formulário, se o formulário tiver um botão Enviar.
   * Clique em Concluir abaixo do formulário se o formulário não tiver um botão Enviar.
   O Process Management start o processo e encaminha o formulário para as listas de tarefas das pessoas apropriadas que precisam concluir a próxima tarefa no processo.

   Se você precisar fechar um formulário antes de enviá-lo e sem perder os dados inseridos, salve um rascunho e preencha-o posteriormente, se o processo permitir. Se o formulário e o processo permitirem, você também pode clicar em **Off-line** e enviá-lo posteriormente do Adobe® Reader® ou Adobe® Acrobat® Professional ou Acrobat Standard.

   >[!NOTE]
   >
   >A opção offline está disponível somente para formulários PDF.

## Adicionar notas e anexos {#adding-notes-and-attachments}

É possível adicionar notas e anexos de arquivo a um processo se o processo permitir. Você pode fornecer permissões para outros usuários que participam do processo para visualização, atualização e exclusão das notas ou anexos.

### Adicionar uma nota {#add-a-note}

É possível adicionar várias notas, editá-las e excluí-las. Cada nota tem um título, uma descrição e uma permissão de acesso associada. Você pode definir uma das seguintes permissões de acesso em uma observação:

* Somente leitura (a permissão padrão)
* Ler/editar/excluir
* Ler/editar
* Leitura/exclusão
* Sem acesso

1. Abra uma tarefa e clique na guia **Notas** , se o processo permitir.
1. Digite um título para a nota na caixa **Título** e digite o texto da nota na caixa **Nota** .
1. Selecione o nível de **Permissões** para a observação para outros usuários que participam do processo.
1. Clique em **OK**. Um arquivo de texto que contém sua nota é anexado ao formulário. Você pode atualizar uma nota clicando nela e modificando diretamente o texto. Você pode excluir uma nota clicando no botão **Excluir** ![Imagem de uma lixeira ao lado da nota](assets/icondelete.png) .

### Adicionar um anexo {#add-an-attachment}

Você também pode adicionar seus comentários sobre o anexo. Você pode definir uma das seguintes permissões de acesso em um anexo:

* Somente leitura (a permissão padrão)
* Ler/editar/excluir
* Ler/editar
* Leitura/exclusão
* Sem acesso

1. Clique na guia **Anexos** e selecione **Anexo**.
1. Clique em **Procurar** para selecionar o arquivo a ser anexado.
1. Selecione o nível de **Permissões** para o anexo para outros usuários que participam do processo. Se você selecionar **Ler**, outros usuários poderão salvar o arquivo localmente. Se você selecionar uma das permissões de edição, outros usuários também poderão carregar um novo arquivo para substituir seu anexo.
1. Clique em **OK**. O arquivo é anexado ao formulário. Você pode excluir um arquivo clicando no botão **Excluir** ![Imagem de uma lixeira ao lado do anexo](assets/icondelete.png) .

## Salvar cópias de rascunho de formulários {#saving-draft-copies-of-forms}

Se for necessário preencher e enviar um formulário posteriormente, é possível salvar uma cópia de rascunho de um formulário para não perder o trabalho existente. As cópias de rascunho são adicionadas à categoria Rascunhos na página de Tarefas.

Após reabrir e enviar um formulário de rascunho, ele será removido da categoria Rascunhos.

Além disso, você pode configurar o espaço de trabalho para salvar automaticamente as informações inseridas por um usuário como rascunho. Para obter mais informações, consulte [Gerenciamento de preferências](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>O botão Salvar não está disponível para alguns formulários, dependendo do processo ao qual está associado.

### Salvar uma cópia de rascunho {#save-a-draft-copy}

1. Clique em **Salvar** no canto inferior esquerdo de qualquer guia. O formulário é adicionado à categoria Rascunhos na página de Tarefas Pendentes. Todas as alterações feitas no formulário são salvas.

### Reabrir uma cópia de rascunho {#reopen-a-draft-copy}

1. Na página A fazer, selecione a fila **Rascunhos** e clique na cópia de rascunho do formulário.

   Se o formulário contiver uma série de painéis, talvez seja necessário ir para o painel onde terminou a última sessão.

## Adicionando processos à categoria Favoritos {#adding-processes-to-the-favorites-category}

Você pode adicionar qualquer processo à sua categoria Favoritos. Ao configurar os favoritos, você pode agrupar todos os processos que você start com frequência em uma única categoria para encontrá-los rapidamente.

>[!NOTE]
>
>Se você costuma processar o start ao usar a área de trabalho do AEM Forms, é possível definir a preferência Local do Start para exibir automaticamente a categoria Favoritos ao start da área de trabalho do AEM Forms. Para obter mais detalhes, consulte Gerenciar preferências em [Introdução à área de trabalho](/help/forms/using/getting-started-livecycle-html-workspace.md)do AEM Forms.

Para marcar um processo como favorito, selecione a tarefa na categoria e clique na estrela vazia. A estrela fica dourada. Para desmarcar um processo como favorito, clique na estrela dourada novamente.
