---
title: Início e interrupção da linha de comando
seo-title: Início e interrupção da linha de comando
description: Saiba como start e parar AEM na linha de comando.
seo-description: Saiba como start e parar AEM na linha de comando.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---


# Início e interrupção da linha de comando{#command-line-start-and-stop}

## Iniciar o Adobe Experience Manager a partir da Linha de Comando {#starting-adobe-experience-manager-from-the-command-line}

O script `start` está disponível em *no diretório &lt;cq-installation>/bin*. As versões Unix e Windows são fornecidas. O script start a instância instalada no diretório *&lt;cq-installation>*.

Essas duas versões suportam uma lista de variáveis de ambiente que podem ser usadas para start e ajuste da instância AEM.

<table>
 <tbody>
  <tr>
   <td><strong>variável ambiente </strong></td>
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
   <td>Uso de JAAS (se verdadeiro)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>Caminho da configuração do JAAS<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>Opções de JVM padrão<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Observe que alguns modos de execução, entre eles autor e publicação, precisam ser definidos antes da primeira inicialização do AEM e não podem ser alterados posteriormente. Antes de configurar uma instância AEM que deve ser usada na produção, consulte a [documentação dos modos de execução](/help/sites-deploying/configure-runmodes.md) para obter detalhes.

### Exemplo de script start.bat da plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Exemplo de script de start da plataforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>O script do start inicia o AEM Quickstart instalado na pasta *cq-installation>/app*.

## Parando o Adobe Experience Manager {#stopping-adobe-experience-manager}

Para interromper o AEM, execute um dos procedimentos a seguir:

* Dependendo da plataforma usada:

   * Se você começou a AEM de um script ou da linha de comando, pressione **Ctrl+C** para encerrar o servidor.
   * Se você tiver usado o script de start no UNIX, deverá usar o script stop para interromper o AEM.

* Se você começou a AEM ao clicar no arquivo jar com o duplo, clique no botão **On** na janela de inicialização (o botão muda para **Off**) para desligar o servidor.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Parando o Adobe Experience Manager da Linha de Comando {#stopping-adobe-experience-manager-from-the-command-line}

O script `stop` está disponível em *no diretório &lt;cq-installation>/bin*. As versões Unix e Windows são fornecidas. O script para a instância em execução instalada no diretório *&lt;cq-installation>*.

### Exemplo de script de parada de plataforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Exemplo de script stop.bat da plataforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Caso deseje pré-configurar o repositório (sem relocá-lo), você só terá que:

* extrair `repository.xml` para o local desejado

* atualizar `repository.xml` conforme necessário

* crie `bootstrap.properties` e defina `repository.config`

Novamente, antes de iniciar a instalação real.

