---
title: Iniciar e parar o WebLogic Server
seo-title: Iniciar e parar o WebLogic Server
description: Vários procedimentos exigem que você inicie ou pare a instância do WebLogic Server, onde deseja implantar módulos de formulários AEM. Este documento descreve como iniciar e parar o WebLogic Server.
seo-description: Vários procedimentos exigem que você inicie ou pare a instância do WebLogic Server, onde deseja implantar módulos de formulários AEM. Este documento descreve como iniciar e parar o WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---


# Iniciando e parando o WebLogic Server {#starting-and-stopping-weblogic-server}

Vários procedimentos exigem que você inicie ou pare a instância do WebLogic Server, onde deseja implantar módulos de formulários AEM. Verifique se o WebLogic Server está interrompido ou em execução, dependendo da tarefa que você está executando.

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
   <td><p>Criação de um servidor gerenciado do WebLogic</p></td>
   <td><p>Em execução</p></td>
  </tr>
  <tr>
   <td><p>Aumentando a contagem de threads do servidor</p></td>
   <td><p>Em execução</p></td>
  </tr>
  <tr>
   <td><p>Implantação de produtos AEM formulários</p></td>
   <td><p>Em execução</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se você estiver executando o WebLogic Server no Red Hat® Enterprise Linux Advanced Server 4.0, defina a variável de ambiente `LD_ASSUME_KERNEL` como 2.4.19 usando o comando `export LD_ASSUME_KERNEL=2.4.19`. Em seguida, execute o WebLogic Server a partir do mesmo shell no qual você definiu essa variável de ambiente.

## Iniciar o WebLogic Server {#start-weblogic-server}

1. Em um prompt de comando, vá para *[appserver root]*/user_projects/domains/*[appserverdomain]*.
1. Digite o seguinte comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Parar o WebLogic Server {#stop-weblogic-server}

1. Inicie o console de administração do WebLogic Server digitando `https://[host name]:7001/console` na linha de URL de um navegador da Web.
1. Faça logon digitando o nome de usuário e a senha usados ao criar essa configuração do WebLogic e clique em Fazer logon.
1. Em Centro de alterações, clique em Bloquear e editar.
1. Em Estrutura de domínio, clique em Ambiente > Servidores.
1. Clique em AdminServer e, no painel Configurações do AdminServer , clique na guia Controle .
1. Verifique se AdminServer está selecionado na tabela Status do Servidor e clique em Desligar.
1. Selecione Quando o trabalho for concluído para encerrar o servidor com cuidado ou selecione Forçar desligamento agora para interromper o servidor imediatamente sem concluir as tarefas em andamento.
1. No painel do Server Life Cycle Assistant, clique em Sim para concluir o desligamento.

O console de administração do WebLogic Server não está mais disponível e o prompt de comando do qual você executou o comando de início está disponível.

## Iniciar o console de administração do WebLogic {#start-weblogic-administration-console}

1. Se o WebLogic Admin Server ainda não estiver em execução, a partir de um prompt de comando, vá para o diretório *[appserver root]\user_projects\domains\[domainname]* e insira o seguinte comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Acesse o console de administração do WebLogic Server digitando `https://[host name]:[port]/console` na linha de URL de um navegador da Web, onde *[port]* é a porta de escuta não segura. Por padrão, esse valor de porta é 7001.
1. Na tela de logon, digite o nome de usuário e a senha do administrador e clique em Fazer logon.

## Inicie o Gerenciador de Nó {#start-node-manager}

1. Certifique-se de que o WebLogic Server esteja em execução.
1. Em um novo prompt de comando, vá para *[appserver root]*/server/bin.
1. Digite o seguinte comando:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Parar o Gerenciador de Nó {#stop-node-manager}

Após encerrar o WebLogic Server, você pode fechar o prompt de comando do qual chamou o Gerenciador de nós.

## Iniciar um servidor gerenciado do WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Esta tarefa só pode ser executada depois de criar um domínio WebLogic e um servidor gerenciado.

1. Verifique se o WebLogic Server e o Gerenciador de nós estão em execução.
1. Inicie o console de administração do WebLogic Server digitando `https://host name]:[port]/console` na linha de URL de um navegador da Web.
1. Em Estrutura de domínio, clique em Ambiente > Servidores.
1. No painel direito, clique na guia Controle .
1. Selecione o servidor gerenciado que deseja iniciar.
1. Clique no botão Start abaixo do servidor gerenciado que deseja iniciar.

## Pare um servidor gerenciado do WebLogic {#stop-a-weblogic-managed-server}

1. Inicie o console de administração do WebLogic Server digitando `https://`*[host name]:[port ]*`/console` na linha de URL de um navegador da Web.
1. Em Estrutura de domínio, clique em Ambiente > Servidores.
1. No painel direito, clique na guia Controle .
1. Selecione o servidor gerenciado que deseja interromper.
1. Clique no botão Shutdown abaixo do servidor gerenciado que deseja parar.
1. Selecione Quando o trabalho for concluído para encerrar o servidor com cuidado ou selecione Forçar desligamento agora para interromper o servidor imediatamente sem concluir as tarefas em andamento.
1. No painel do Server Life Cycle Assistant, clique em Sim para concluir o desligamento.

