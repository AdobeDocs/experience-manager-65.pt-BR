---
title: Iniciando e interrompendo o WebLogic Server
description: Vários procedimentos exigem que você inicie ou interrompa a instância do WebLogic Server em que deseja implantar módulos de formulários AEM. Este documento descreve como iniciar e parar o WebLogic Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# Iniciando e interrompendo o WebLogic Server {#starting-and-stopping-weblogic-server}

Vários procedimentos exigem que você inicie ou interrompa a instância do WebLogic Server em que deseja implantar módulos de formulários AEM. Certifique-se de que o WebLogic Server esteja parado ou em execução, dependendo da tarefa que você está executando.

<table>
 <thead>
  <tr>
   <th><p>Atividade</p></th>
   <th><p>Estado do WebLogic obrigatório</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Criação de um domínio do WebLogic</p></td>
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
   <td><p>Implantação de produtos de formulários AEM</p></td>
   <td><p>Em execução</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se você estiver executando o WebLogic Server no Red Hat® Enterprise Linux Advanced Server 4.0, defina a variável de ambiente `LD_ASSUME_KERNEL` como 2.4.19 usando o comando `export LD_ASSUME_KERNEL=2.4.19`. Em seguida, execute o WebLogic Server no mesmo shell em que você define essa variável de ambiente.

## Iniciar WebLogic Server {#start-weblogic-server}

1. Em um prompt de comando, vá para *[appserver root]*/user_projects/domains/*[appserverdomain]*.
1. Digite o seguinte comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Parar WebLogic Server {#stop-weblogic-server}

1. Inicie o console de administração do WebLogic Server digitando `https://[host name]:7001/console` na linha de URL de um navegador da Web.
1. Efetue logon digitando o nome de usuário e a senha que foram usados ao criar essa configuração do WebLogic e, em seguida, clique em Efetuar Logon.
1. Em Centro de alterações, clique em Bloquear e editar.
1. Em Estrutura do domínio, clique em Ambiente > Servidores.
1. Clique em AdminServer e, no painel Configurações para o AdminServer, clique na guia Controle.
1. Verifique se AdminServer está selecionado na tabela Status do servidor e clique em Desligar.
1. Selecione Quando o Trabalho For Concluído para desligar o servidor normalmente ou selecione Forçar Desligamento Agora para interromper o servidor imediatamente sem concluir as tarefas em andamento.
1. No painel Assistente de Ciclo de Vida do Servidor, clique em Sim para concluir o desligamento.

O console de administração do WebLogic Server não está mais disponível e o prompt de comando a partir do qual você executou o comando de início está disponível.

## Iniciar console de administração do WebLogic {#start-weblogic-administration-console}

1. Se o WebLogic Admin Server ainda não estiver em execução, em um prompt de comando, vá para o diretório *[appserver root]\user_projects\domains\[domainname]* e digite o seguinte comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Acesse o console de administração do WebLogic Server digitando `https://[host name]:[port]/console` na linha de URL de um navegador da Web, em que *[porta]* é a porta de escuta não segura. Por padrão, esse valor de porta é 7001.
1. Na tela de login, digite seu nome de usuário e senha de administrador e clique em Login.

## Iniciar gerenciador de nós {#start-node-manager}

1. Verifique se o WebLogic Server está em execução.
1. Em um novo prompt de comando, vá para *[raiz do appserver]*/server/bin.
1. Digite o seguinte comando:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Parar gerenciador de nós {#stop-node-manager}

Após desativar o WebLogic Server, você pode fechar o prompt de comando a partir do qual chamou o Gerenciador de Nós.

## Iniciar um servidor gerenciado WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Esta tarefa só pode ser executada após a criação de um domínio WebLogic e um servidor gerenciado.

1. Verifique se o WebLogic Server e o Gerenciador de Nós estão em execução.
1. Inicie o console de administração do WebLogic Server digitando `https://host name]:[port]/console` na linha de URL de um navegador da Web.
1. Em Estrutura do domínio, clique em Ambiente > Servidores.
1. No painel direito, clique na guia Controle.
1. Selecione o servidor gerenciado que deseja iniciar.
1. Clique no botão Iniciar abaixo do servidor gerenciado que deseja iniciar.

## Interromper um servidor gerenciado WebLogic {#stop-a-weblogic-managed-server}

1. Inicie o console de administração do WebLogic Server digitando `https://`*[nome do host]:[porta ]*`/console` na linha de URL de um navegador da Web.
1. Em Estrutura do domínio, clique em Ambiente > Servidores.
1. No painel direito, clique na guia Controle.
1. Selecione o servidor gerenciado que deseja parar.
1. Clique no botão Desligar abaixo do servidor gerenciado que você deseja parar.
1. Selecione Quando o Trabalho For Concluído para desligar o servidor normalmente ou selecione Forçar Desligamento Agora para interromper o servidor imediatamente sem concluir as tarefas em andamento.
1. No painel Assistente de Ciclo de Vida do Servidor, clique em Sim para concluir o desligamento.

