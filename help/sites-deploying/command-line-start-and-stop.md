---
title: Início e interrupção da linha de comando
seo-title: Início e interrupção da linha de comando
description: Saiba como iniciar e parar o AEM na linha de comando.
seo-description: Saiba como iniciar e parar o AEM na linha de comando.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Início e interrupção da linha de comando{#command-line-start-and-stop}

## Iniciar o Adobe Experience Manager na linha de comando {#starting-adobe-experience-manager-from-the-command-line}

O `start` script está disponível no diretório &lt;cq-installation>/bin ** . As versões Unix e Windows são fornecidas. O script inicia a instância instalada no diretório *&lt;cq-installation>* .

Essas duas versões suportam uma lista de variáveis de ambiente que podem ser usadas para iniciar e ajustar a instância do AEM.

<table>
 <tbody>
  <tr>
   <td><strong>Variável de ambiente </strong></td>
   <td><strong>Descrição </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Porta TCP usada para scripts de parada e status<br /> </td>
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
   <td>Modo(s) de execução separados por vírgula<br /> </td>
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
   <td>Caminho da configuração do JAAS<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>Opções JVM padrão<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Observe que alguns modos de execução, entre eles autor e publicação, precisam ser definidos antes de iniciar o AEM pela primeira vez e não podem ser alterados posteriormente. Antes de configurar uma instância do AEM que deve ser usada na produção, consulte a documentação [dos modos de](/help/sites-deploying/configure-runmodes.md) execução para obter detalhes.

### Exemplo de script start.bat da plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Exemplo de script de início de plataforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>O script start inicia o Quickstart do AEM instalado na pasta &lt;cq-installation>/app ** .

## Stopping Adobe Experience Manager {#stopping-adobe-experience-manager}

Para interromper o AEM, siga um destes procedimentos:

* Dependendo da plataforma usada:

   * Se você iniciou o AEM a partir de um script ou da linha de comando, pressione **Ctrl+C** para encerrar o servidor.
   * Se você tiver usado o script de inicialização no UNIX, deverá usar o script stop para interromper o AEM.

* Se você começou o AEM clicando duas vezes no arquivo jar, clique no botão **Ligado** na janela de inicialização (o botão em seguida muda para **Desligado**) para desligar o servidor.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Parar o Adobe Experience Manager da linha de comando {#stopping-adobe-experience-manager-from-the-command-line}

O `stop` script está disponível no diretório &lt;cq-installation>/bin ** . As versões Unix e Windows são fornecidas. O script para a instância em execução instalada no diretório *&lt;cq-installation>* .

### Exemplo de script de parada de plataforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Exemplo de script stop.bat da plataforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Caso deseje pré-configurar o repositório (sem relocá-lo), você só terá que:

* extract `repository.xml` to the required location

* atualizar `repository.xml` conforme necessário

* criar `bootstrap.properties` e definir `repository.config`

Novamente, antes de iniciar a instalação real.

