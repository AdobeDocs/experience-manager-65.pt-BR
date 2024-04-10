---
title: Início e Interrupção da Linha de Comando
description: Saiba como iniciar e parar o Adobe Experience Manager na linha de comando.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Início e Interrupção da Linha de Comando{#command-line-start-and-stop}

## Iniciar o Adobe Experience Manager a partir da linha de comando {#starting-adobe-experience-manager-from-the-command-line}

A variável `start` script está disponível em *o &lt;cq-installation>/bin* diretório. São fornecidas as versões para UNIX® e Windows. O script inicia a instância instalada no *&lt;cq-installation>* diretório.

Essas duas versões oferecem suporte a uma lista de variáveis de ambiente que podem ser usadas para iniciar e ajustar a instância do Adobe Experience Manager (AEM).

<table>
 <tbody>
  <tr>
   <td><strong>Variável de ambiente </strong></td>
   <td><strong>Descrição </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Porta TCP usada para scripts de interrupção e status<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>Nome do host<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Interface que este servidor deve escutar<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>Modos de execução separados por vírgula<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nome do jarfile<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>Uso do JAAS (se verdadeiro)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>Caminho da configuração JAAS<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>Opções de JVM padrão<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Alguns modos de execução, entre eles autor e publicação, devem ser definidos antes de o AEM ser iniciado primeiro e não podem ser alterados posteriormente. Antes de configurar uma instância do AEM usada na produção, consulte [documentação de modos de execução](/help/sites-deploying/configure-runmodes.md) para obter detalhes.

### Exemplo de script start.bat para plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Exemplo de script de início de plataforma UNIX® {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>O script de inicialização inicia o AEM Quickstart instalado em *o &lt;cq-installation>/app* pasta.

## Interrupção do Adobe Experience Manager {#stopping-adobe-experience-manager}

Para interromper o AEM, siga um destes procedimentos:

* Dependendo da plataforma usada:

   * Se você iniciou o AEM a partir de um script ou da linha de comando, pressione **Ctrl+C** para desligar o servidor.
   * Se você tiver usado o script de inicialização no UNIX®, deverá usar o script de interrupção para interromper o AEM.

* Se você iniciou o AEM clicando duas vezes no arquivo jar, clique no ícone **Ligado** na janela de inicialização (o botão muda então para **Desligado**) para desligar o servidor.

  ![chlimage_1-63](assets/chlimage_1-63.png)

## Interrupção do Adobe Experience Manager a partir da linha de comando {#stopping-adobe-experience-manager-from-the-command-line}

A variável `stop` script está disponível em *o &lt;cq-installation>/bin* diretório. São fornecidas as versões para UNIX® e Windows. O script interrompe a instância em execução instalada no *&lt;cq-installation>* diretório.

### Exemplo de script de interrupção da plataforma UNIX® {#unix-platform-stop-script-example}

```shell
./stop
```

### Exemplo de script stop.bat para plataforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Se você quiser apenas pré-configurar o repositório (sem realocá-lo), basta:

* Extract `repository.xml` para o local necessário

* atualizar `repository.xml` conforme necessário

* criar `bootstrap.properties` e definir `repository.config`

Novamente, antes de iniciar a instalação real.
