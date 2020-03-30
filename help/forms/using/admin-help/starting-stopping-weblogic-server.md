---
title: Iniciando e parando o WebLogic Server
seo-title: Iniciando e parando o WebLogic Server
description: Vários procedimentos exigem que você start ou pare a instância do WebLogic Server onde deseja implantar módulos de formulários AEM. Este documento descreve como start e parar o WebLogic Server.
seo-description: Vários procedimentos exigem que você start ou pare a instância do WebLogic Server onde deseja implantar módulos de formulários AEM. Este documento descreve como start e parar o WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Iniciando e parando o WebLogic Server {#starting-and-stopping-weblogic-server}

Vários procedimentos exigem que você start ou pare a instância do WebLogic Server onde deseja implantar módulos de formulários AEM. Verifique se o WebLogic Server está parado ou em execução, dependendo da tarefa que você está executando.

<table>
 <thead>
  <tr>
   <th><p>Atividade</p></th>
   <th><p>Estado WebLogic necessário</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Criação de um domínio WebLogic</p></td>
   <td><p>Parado</p></td>
  </tr>
  <tr>
   <td><p>Criação de um servidor gerenciado WebLogic</p></td>
   <td><p>Em execução</p></td>
  </tr>
  <tr>
   <td><p>Aumentando a contagem de threads do servidor</p></td>
   <td><p>Em execução</p></td>
  </tr>
  <tr>
   <td><p>Implantação de produtos de formulários do AEM</p></td>
   <td><p>Em execução</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se você estiver executando o WebLogic Server no Red Hat® Enterprise Linux Advanced Server 4.0, defina a variável `LD_ASSUME_KERNEL` ambiente como 2.4.19 usando o `export LD_ASSUME_KERNEL=2.4.19` comando. Em seguida, execute o WebLogic Server a partir do mesmo shell no qual você definiu essa variável de ambiente.

## Start WebLogic Server {#start-weblogic-server}

1. Em um prompt de comando, vá para *[appserver root]*/user_projects/domain/*[appserverdomain]*.
1. Digite o seguinte comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Parar o WebLogic Server {#stop-weblogic-server}

1. Start do console de administração do WebLogic Server digitando `https://[host name]:7001/console` na linha de URL de um navegador da Web.
1. Faça logon digitando o nome de usuário e a senha usados ao criar esta configuração WebLogic e clique em Fazer logon.
1. Em Centro de alterações, clique em Bloquear e editar.
1. Em Estrutura do domínio, clique em Ambiente > Servidores.
1. Clique em AdminServer e, no painel Configurações do AdminServer, clique na guia Controle.
1. Verifique se AdminServer está selecionado na tabela Status do servidor e clique em Desligar.
1. Selecione Quando o trabalho terminar para encerrar o servidor com cuidado ou selecione Forçar o encerramento agora para interromper o servidor imediatamente sem concluir as tarefas em andamento.
1. No painel Server Life Cycle Assistant (Assistente do ciclo de vida do servidor), clique em Yes (Sim) para concluir o encerramento.

O console de administração do WebLogic Server não está mais disponível e o prompt de comando do qual você executou o comando do start está disponível.

## Console de administração do Start WebLogic {#start-weblogic-administration-console}

1. Se o WebLogic Admin Server ainda não estiver em execução, a partir de um prompt de comando, vá para o diretório raiz *[\user_projects\domains\[nome_do_domínio]]do *appserver e digite o seguinte comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Acesse o console de administração do WebLogic Server digitando `https://[host name]:[port]/console` na linha de URL de um navegador da Web, onde a *[porta]* é a porta de escuta não segura. Por padrão, esse valor de porta é 7001.
1. Na tela de logon, digite o nome de usuário e a senha do administrador e clique em Login.

## Gerenciador de nó de Start {#start-node-manager}

1. Verifique se o WebLogic Server está em execução.
1. Em um novo prompt de comando, vá para *[appserver root]*/server/bin.
1. Digite o seguinte comando:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Parar Gerenciador de Nó {#stop-node-manager}

Depois de encerrar o WebLogic Server, você pode fechar o prompt de comando do qual chamou o Node Manager.

## Start de um servidor gerenciado WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Essa tarefa só pode ser executada depois que você criar um domínio WebLogic e um servidor gerenciado.

1. Verifique se o WebLogic Server e o Gerenciador de nós estão em execução.
1. Start do console de administração do WebLogic Server digitando `https://host name]:[port]`/console&quot; na linha de URL de um navegador da Web.
1. Em Estrutura do domínio, clique em Ambiente > Servidores.
1. No painel direito, clique na guia Controle.
1. Selecione o servidor gerenciado que deseja start.
1. Clique no botão Start abaixo do servidor gerenciado que deseja start.

## Parar um servidor gerenciado WebLogic {#stop-a-weblogic-managed-server}

1. Start do console de administração do WebLogic Server digitando nome `https://`*[do]host:[porta ]*`/console`na linha de URL de um navegador da Web.
1. Em Estrutura do domínio, clique em Ambiente > Servidores.
1. No painel direito, clique na guia Controle.
1. Selecione o servidor gerenciado que deseja interromper.
1. Clique no botão Desligar abaixo do servidor gerenciado que deseja interromper.
1. Selecione Quando o trabalho terminar para encerrar o servidor com cuidado ou selecione Forçar o encerramento agora para interromper o servidor imediatamente sem concluir as tarefas em andamento.
1. No painel Server Life Cycle Assistant (Assistente do ciclo de vida do servidor), clique em Yes (Sim) para concluir o encerramento.

