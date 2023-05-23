---
title: Iniciando processos
seo-title: Starting processes
description: Como usar o espaço de trabalho do LiveCycle AEM Forms — selecione processos, adicione notas e anexos, salve cópias de rascunho e adicione a favoritos.
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

o espaço de trabalho do AEM Forms organiza os processos pelas categorias que o administrador ou designer de processo configura. Você também pode colocar processos que usa com frequência na categoria Favoritos, para que possa encontrá-los rapidamente.

Ao iniciar um processo, talvez seja necessário preencher um formulário para iniciar um processo de negócios controlado pelo fluxo de trabalho do AEM Forms. Se um formulário usar Preparar processo de dados, algumas informações poderão ser preenchidas previamente em um formulário em branco, quando um novo processo for iniciado.

Por exemplo, você deseja comprar um novo monitor de computador e, portanto, iniciar um processo chamado *Ordem de Compra*. Quando você inicia o processo, um formulário é aberto e solicita detalhes sobre o item a ser solicitado. Seu nome, número de funcionário e nome de gerente já podem estar preenchidos no formulário. Quando você submete a solicitação, um processo de negócios é iniciado. Com base na definição do processo, o servidor roteia automaticamente a solicitação para o seu gerente. A tarefa começa a aparecer na lista de tarefas pendentes do seu gerente. Quando seu gerente aprova a solicitação, o workflow do forms encaminha a solicitação ao departamento de compras e envia uma notificação por email.

## Selecionar processos para iniciar {#selecting-processes-to-start}

Você pode selecionar um processo para iniciá-lo ou para exibir mais informações sobre ele.

Ao selecionar um processo para iniciar, talvez seja necessário preencher um formulário associado a esse processo. O envio do formulário inicia o processo.

O Forms em vários tipos de formatos de arquivo é compatível, incluindo Adobe PDF, HTML e SWF file. Um formulário pode se parecer com um formulário tradicional imprimível ou baseado na Web, ou pode orientá-lo por uma série de painéis no estilo de assistente para coletar informações.

Se o formulário e o processo permitirem, também será possível salvar o formulário offline, preenchê-lo e enviá-lo para concluir a tarefa. Quando o formulário for enviado, seu cliente de email será iniciado com o endereço de email do servidor apropriado, se o ponto de acesso de email estiver configurado. Em seguida, você pode enviar o formulário preenchido para o servidor por email.

Quando você seleciona um processo, a guia Formulário e a guia Detalhes são exibidas. Se o processo permitir que você adicione avisos ou anexos, a guia Anexos e a guia Avisos também serão exibidas. Se você também tiver configurado o url de resumo com o processo, a guia Resumo também será exibida. A guia Forms exibe o formulário associado e a guia Detalhes exibe informações sobre a tarefa atual e o processo do qual ela faz parte.

### Iniciar um processo de negócios {#start-a-business-process}

1. Na página Iniciar processo, na lista à esquerda, selecione uma categoria. Todos os processos aos quais você tem acesso na categoria aparecem à direita.

   >[!NOTE]
   >
   >Se o painel Categorias estiver recolhido, clique em &quot;Abrir categorias&quot;, na área superior esquerda do espaço de trabalho do AEM Forms, para abrir o painel.

1. Selecione um processo clicando em uma tarefa. O formulário associado ao processo é aberto na guia Formulário.

   Cada formulário em um processo tem um URL exclusivo. Você pode usar o URL exclusivo para iniciar diretamente o espaço de trabalho do HTML com o processo e formulário específicos. O formato do URL é https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;applicationname>%2F&lt;processname>. A variável &lt;applicationname>%2F&lt;processname> a string sempre é codificada por URL. Um exemplo de URL é http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. A cadeia de caracteres ApplicationName%2FProcessName no exemplo é codificada por URL.

1. Preencha o formulário de acordo com as instruções fornecidas. Se necessário, clique em **Maximizar** para aumentar a área visível do formulário.
1. Se a guia Anexos estiver disponível, adicione os anexos conforme necessário.
1. Se a guia Notas estiver disponível, forneça as notas conforme necessário.
1. Execute uma destas etapas:

   * Clique no botão Enviar no formulário, caso ele tenha um botão Enviar.
   * Clique em Concluído abaixo do formulário, caso ele não tenha um botão Enviar.

   O Process Management inicia o processo e direciona o formulário para as listas de tarefas pendentes das pessoas apropriadas que precisam concluir a próxima tarefa no processo.

   Se você precisar fechar um formulário antes de enviá-lo e sem perder os dados inseridos, salve um rascunho e preencha-o posteriormente, se o processo permitir. Se o formulário e o processo permitirem, você também poderá clicar em **Offline** e mais tarde, envie-o do Adobe® Reader® ou Adobe® Acrobat® Professional ou Acrobat Standard.

   >[!NOTE]
   >
   >A opção off-line está disponível somente para PDF forms.

## Adicionando avisos e anexos {#adding-notes-and-attachments}

É possível adicionar notas e anexos de arquivo a um processo se o processo permitir. É possível fornecer permissões para outros usuários que participam do processo para exibir, atualizar e excluir as notas ou os anexos.

### Adicionar uma observação {#add-a-note}

É possível adicionar várias notas, editar as notas escritas e excluí-las. Cada nota tem um título, uma descrição e uma permissão de acesso associada a ela. Você pode definir uma das seguintes permissões de acesso em uma observação:

* Somente leitura (a permissão padrão)
* Ler/Editar/Excluir
* Ler/Editar
* Ler/Excluir
* Sem acesso

1. Abra uma tarefa e clique no link **Notas** se o processo permitir.
1. Digite um título para a nota na caixa **Título** e digite o texto da nota na caixa **Nota** caixa.
1. Selecione o **Permissões** nível da nota para outros usuários que participam do processo.
1. Clique em **OK**. Um arquivo de texto que contém sua nota é anexado ao formulário. Você pode atualizar uma nota clicando nela e modificando diretamente o texto. É possível excluir uma nota clicando no ícone **Excluir** botão ![Imagem de uma lata de lixo](assets/icondelete.png) ao lado da nota.

### Adicionar um anexo {#add-an-attachment}

Você também pode adicionar comentários sobre o anexo. Você pode definir uma das seguintes permissões de acesso em um anexo:

* Somente leitura (a permissão padrão)
* Ler/Editar/Excluir
* Ler/Editar
* Ler/Excluir
* Sem acesso

1. Clique em **Anexos** e selecione **Anexo**.
1. Clique em **Procurar** para selecionar o arquivo a ser anexado.
1. Selecione o **Permissões** nível do anexo para outros usuários que participam do processo. Se você selecionar **Ler**, outros usuários poderão salvar o arquivo localmente. Se você selecionar uma das permissões de edição, outros usuários também poderão fazer upload de um novo arquivo para substituir seu anexo.
1. Clique em **OK**. O arquivo é anexado ao formulário. É possível excluir um arquivo clicando no ícone **Excluir** botão ![Imagem de uma lata de lixo](assets/icondelete.png) ao lado do anexo.

## Salvamento de cópias de rascunho de formulários {#saving-draft-copies-of-forms}

Se precisar preencher e enviar um formulário posteriormente, você poderá salvar uma cópia de rascunho de um formulário para não perder o trabalho existente. As cópias de rascunho são adicionadas à categoria Rascunhos na página Tarefas Pendentes.

Depois de reabrir e enviar um formulário de rascunho, o rascunho é removido da categoria Rascunhos.

Além disso, você pode configurar o espaço de trabalho para salvar automaticamente as informações inseridas por um usuário como rascunho. Para obter mais informações, consulte [Gerenciamento de preferências](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>O botão Salvar não está disponível para alguns formulários, dependendo do processo ao qual está associado.

### Salvar uma cópia de rascunho {#save-a-draft-copy}

1. Clique em **Salvar** no canto inferior esquerdo de qualquer guia. O formulário é adicionado à categoria Rascunhos na página Tarefas Pendentes. Todas as alterações feitas no formulário são salvas.

### Reabrir uma cópia de rascunho {#reopen-a-draft-copy}

1. Na página Tarefas, selecione a variável **Rascunhos** e clique na cópia de rascunho do formulário.

   Se o formulário contiver uma série de painéis, talvez seja necessário ir até o painel em que você encerrou sua última sessão.

## Adicionar processos à categoria Favoritos {#adding-processes-to-the-favorites-category}

Você pode adicionar qualquer processo à sua categoria Favoritos. Ao definir favoritos, você pode agrupar todos os processos que frequentemente começam em uma única categoria para que possa encontrá-los rapidamente.

>[!NOTE]
>
>Se você geralmente inicia processos ao usar o espaço de trabalho do AEM Forms, pode definir a preferência Iniciar local para exibir automaticamente a categoria Favoritos ao iniciar o espaço de trabalho do AEM Forms. Para obter mais detalhes, consulte Gerenciamento de preferências em [Introdução ao AEM Forms Workspace](/help/forms/using/getting-started-livecycle-html-workspace.md).

Para marcar um processo como favorito, selecione a tarefa em sua categoria e clique na estrela vazia. A estrela fica dourada. Para desmarcar um processo como favorito, clique novamente na estrela dourada.
