---
title: Diretrizes para solução de problemas do AEM Forms Workspace
description: Habilite logs e use o depurador no navegador para solucionar problemas do espaço de trabalho do AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# Diretrizes para solução de problemas do AEM Forms Workspace {#troubleshooting-guidelines-for-aem-forms-workspace}

Este artigo discute como depurar o espaço de trabalho do AEM Forms ativando o registro e usando o depurador em um navegador. Ele também explica alguns problemas comuns que você pode encontrar ao usar o espaço de trabalho do AEM Forms e suas soluções alternativas.

## Não é possível instalar o pacote do espaço de trabalho do AEM Forms {#unable-to-install-aem-forms-workspace-package}

Após instalar o patch, abra o espaço de trabalho do AEM Forms. Se você encontrar o erro Nenhum recurso encontrado, abra o Gerenciador de pacotes do CRX e reinstale o `adobe-lc-workspace-pkg-<version>.zip` pacote.

Ao instalar o pacote, se você encontrar um erro `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, execute as seguintes etapas:

1. Efetue logon no CRXDE Lite. O URL padrão é `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Exclua o seguinte nó:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Acesse o Gerenciador de pacotes. O URL padrão é `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Pesquise e instale o `adobe-lc-workspace-pkg-[version].zip` pacote.
1. Reinicie o servidor de aplicativos.

>[!NOTE]
>
> É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Registro de espaço de trabalho do AEM Forms {#aem-forms-workspace-nbsp-logging}

Você pode gerar logs em vários níveis para permitir a solução ideal de problemas de erros. Por exemplo, em um aplicativo complexo, registrar no nível do componente ajuda na depuração e na solução de problemas de componentes específicos.

No espaço de trabalho do AEM Forms:

* Para obter as informações de registro sobre um arquivo de componente específico, anexe `/log/<ComponentFile>/<LogLevel>` no URL e pressione `Enter`. Todas as informações de registro do arquivo componente no nível de registro especificado são impressas no console.

* Para obter informações de registro de todos os arquivos de componentes, anexe `/log/all/trace` no URL e pressione `Enter`.

* Formato do log: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>Por padrão, o nível de log de todos os componentes é definido como INFO.

* O nível de log definido pelo usuário é mantido somente para essa sessão do navegador. Quando o usuário atualiza a página, o nível de log é definido como seu valor inicial para todos os componentes.

### Lista de arquivos de componentes no espaço de trabalho do AEM Forms {#list-of-component-files-in-nbsp-aem-forms-workspace}

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
   <td><p>exibiçãoListaTarefas</p> </td>
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
   <td><p>exibiçãodefilasEquipe</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>procnameView</p> </td>
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
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outoofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outoofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>visualizaçãoPreferências</p> </td>
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
   <td><p>exibiçãodedetalhesdaTarefa</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### Níveis de log disponíveis no espaço de trabalho do AEM Forms {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* ERRO
* AVISO
* INFO
* DEPURAR
* TRACE
* DESLIGADO

## Informações de depuração para navegadores {#debugging-information-for-browsers}

Scripts e estilos podem ser depurados em navegadores diferentes.

* **Depuração no IE**: para depurar o espaço de trabalho do AEM Forms no IE, consulte: [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **Depuração no Chrome**: para abrir o depurador no Chrome, use o atalho: Ctrl+Shift+I. Para obter mais informações, consulte: [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **Depuração no Firefox**: vários complementos estão disponíveis para depurar scripts e estilos no Firefox. Por exemplo, o Firebug é um desses utilitários de depuração ([https://getfirebug.com](https://getfirebug.com)).

## Perguntas frequentes {#faqs}

1. O formulário PDF não está sendo renderizado ou enviado no Google Chrome.

   1. Instale o plug-in Adobe® Reader®.
   1. No Chrome, abra chrome://plugins para visualizar os plug-ins disponíveis.
   1. Desative o plug-in do Visualizador de PDF do Chrome e ative o plug-in do Adobe Reader.

1. O formulário ou o Guia do SWF não é renderizado no Google Chrome.

   1. No Chrome, abra chrome://plugins para visualizar os plug-ins disponíveis.
   1. Consulte os detalhes do plug-in Adobe Flash® Player.
   1. Desative o PepperFlash no plug-in Adobe Flash Player.

1. Personalizei o espaço de trabalho do AEM Forms, mas não consegui ver as alterações.

   Limpe o cache do navegador e acesse o espaço de trabalho do AEM Forms.

1. O que precisa ser feito pelo usuário para habilitar o formulário a ser renderizado em HTML quando aberto no desktop?

   Selecione o botão de opção HTML para o perfil padrão na etapa Atribuir tarefa ao usar o Workbench.

1. O anexo não é exibido quando clicado.

   Para exibir anexos, ative pop-ups no navegador.

1. Um usuário está conectado a um aplicativo de formulários. Se o usuário tentar fazer logon no espaço de trabalho, talvez ele não seja carregado se não tiver permissões do espaço de trabalho.

   Faça logoff do outro aplicativo de formulários e, em seguida, faça logon no espaço de trabalho.

1. Os formulários HTML, usando Propriedades do processo no design, quando renderizados no espaço de trabalho do AEM Forms, exibem o botão Enviar dentro do formulário.

   Ao criar formulários, ao usar Propriedades do processo, ele adiciona um botão Enviar dentro do formulário. Quando renderizado como um PDF no espaço de trabalho do AEM Forms, o botão Enviar não fica visível para o usuário final. No entanto, ao renderizar como um formulário HTML no espaço de trabalho do AEM Forms, o botão Enviar fica visível para o usuário final. Clicar nesse botão Enviar dentro do formulário não inicia nenhuma ação. Clicar no botão Enviar na parte inferior do espaço de trabalho do AEM Forms, fora do formulário, conclui a tarefa.
