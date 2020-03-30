---
title: Orientações para solução de problemas para a área de trabalho do AEM Forms
seo-title: Orientações para solução de problemas para a área de trabalho do AEM Forms
description: Ative os logs e use o depurador no navegador para solucionar problemas na área de trabalho do AEM Forms.
seo-description: Ative os logs e use o depurador no navegador para solucionar problemas na área de trabalho do AEM Forms.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Orientações para solução de problemas para a área de trabalho do AEM Forms {#troubleshooting-guidelines-for-aem-forms-workspace}

Este artigo aborda como depurar a área de trabalho do AEM Forms ativando o registro em log e usando o depurador em um navegador. Ele também explica alguns problemas comuns que você pode encontrar ao usar a área de trabalho do AEM Forms e suas soluções alternativas.

## Não é possível instalar o pacote de espaço de trabalho do AEM Forms {#unable-to-install-aem-forms-workspace-package}

Após instalar o patch, abra a área de trabalho do AEM Forms. Se você encontrar o erro Nenhum recurso encontrado, abra o Gerenciador de pacotes CRX e reinstale o `adobe-lc-workspace-pkg-<version>.zip` pacote.

Ao instalar o pacote, se você encontrar um erro `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, execute as seguintes etapas:

1. Efetue logon no CRX DE lite. O url padrão é `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Exclua o seguinte nó:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Vá para o Gerenciador de pacotes. O URL padrão é `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Pesquise e instale o `adobe-lc-workspace-pkg-[version].zip` pacote.
1. Reinicie o servidor de aplicativos.

## Registro em log da área de trabalho do AEM Forms {#aem-forms-workspace-nbsp-logging}

Você pode gerar registros em vários níveis para permitir a solução ideal de erros. Por exemplo, em um aplicativo complexo, o registro em log no nível do componente ajuda na depuração e solução de problemas de componentes específicos.

Na área de trabalho do AEM Forms:

* Para obter as informações de registro sobre um arquivo de componente específico, anexe `/log/<ComponentFile>/<LogLevel>` o URL e pressione `Enter`. Todas as informações de registro do arquivo de componente no nível de registro especificado são impressas no console.

* Para obter informações de registro de todos os arquivos de componente, anexe `/log/all/trace` o URL e pressione `Enter`.

* Formato de registro: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>Por padrão, o nível de log de todos os componentes é definido como INFO.

* O nível de log definido pelo usuário é mantido somente para essa sessão do navegador. Quando o usuário atualiza a página, o nível de log é definido como seu valor inicial para todos os componentes.

### Lista de arquivos de componente na área de trabalho do AEM Forms {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>configuraçõesView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointListModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofficeModel</p> </td>
   <td><p>startpointListView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>offficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>detalhes da tarefaView</p> </td>
   <td><p>wsmessessageView</p> </td>
  </tr>
 </tbody>
</table>

### Níveis de log disponíveis na área de trabalho do AEM Forms {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* ERRO
* AVISO
* INFO
* DEPURAR
* TRAÇO
* DESLIGADO

## Informações de depuração para navegadores {#debugging-information-for-browsers}

Scripts e estilos podem ser depurados em navegadores diferentes.

* **Depuração no IE**: Para depurar a área de trabalho do AEM Forms no IE, consulte: [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx).

* **Depuração no Chrome**: Para abrir o depurador no Chrome, use o atalho: Ctrl+Shift+I. Para obter mais informações, consulte: [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html).

* **Depuração no Firefox**: Vários complementos estão disponíveis para depurar scripts e estilos no Firefox. Por exemplo, o Firebug é um desses utilitários de depuração ([https://getfirebug.com](https://getfirebug.com)).

## Perguntas frequentes {#faqs}

1. O formulário PDF não está sendo renderizado ou enviado no Google Chrome.

   1. Instale o plug-in do Adobe® Reader®.
   1. No Chrome, abra chrome://plugins para visualização dos plug-ins disponíveis.
   1. Desative o plug-in Chrome PDF Viewer e ative o plug-in Adobe Reader.

1. O formulário SWF ou o Guia não é renderizado no Google Chrome.

   1. No Chrome, abra chrome://plugins para visualização dos plug-ins disponíveis.
   1. Consulte os detalhes do plug-in Adobe Flash® Player.
   1. Desative o PepperFlash no plug-in do Adobe Flash Player.

1. Eu personalizei a área de trabalho do AEM Forms, mas não consigo visualizar as alterações.

   Limpe o cache do navegador e acesse a área de trabalho do AEM Forms.

1. O que precisa ser feito pelo usuário para permitir que o formulário seja renderizado em HTML quando aberto na área de trabalho?

   Selecione o botão de opção HTML para o perfil padrão na etapa atribuir tarefa ao usar o Workbench.

1. O anexo não aparece quando clicado.

   Para visualização de anexos, ative pop-ups no navegador.

1. Um usuário está conectado a um aplicativo de formulários. Se o usuário tentar fazer logon na área de trabalho, talvez ele não seja carregado, se o usuário não tiver permissões de área de trabalho.

   Faça logout do outro aplicativo de formulários e, em seguida, faça logon no espaço de trabalho.

1. Formulários HTML, usando Propriedades do processo em seu design, quando renderizados na área de trabalho do AEM Forms, exibem o botão Enviar dentro do formulário.

   Ao projetar formulários, ao usar Propriedades do processo, ele adiciona um botão Enviar dentro do formulário. Quando renderizado como um PDF na área de trabalho do AEM Forms, o botão Enviar não estará visível para o usuário final. Entretanto, ao renderizar como um formulário HTML na área de trabalho do AEM Forms, o botão Enviar fica visível para o usuário final. Clicar nesse botão Enviar dentro do formulário não inicia nenhuma ação. Clicar no botão Enviar na parte inferior da área de trabalho do AEM Forms, fora do formulário, conclui a tarefa.

[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
