---
title: Início e interrupção da linha de comando
seo-title: Command Line Start and Stop
description: Saiba como iniciar e parar AEM a partir da linha de comando.
seo-description: Learn how to start and stop AEM from the command line.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# Início e interrupção da linha de comando{#command-line-start-and-stop}

## Iniciando o Adobe Experience Manager a partir da linha de comando {#starting-adobe-experience-manager-from-the-command-line}

O `start` script está disponível em *o &lt;cq-installation>/bin* diretório. As versões Unix e Windows são fornecidas. O script inicia a instância instalada em *&lt;cq-installation>* diretório.

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
   <td>Modo(s) de execução separado(s) por vírgula<br /> </td>
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
   <td>Opções padrão da JVM<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Observe que alguns modos de execução, entre eles autor e publicação, precisam ser definidos antes da primeira inicialização AEM e não podem ser alterados posteriormente. Antes de configurar uma instância de AEM que deve ser usada na produção, consulte o [documentação dos modos de execução](/help/sites-deploying/configure-runmodes.md) para obter detalhes.

### Exemplo de script start.bat da plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Exemplo de script de início da plataforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>O script de início inicia o AEM Quickstart instalado em *o &lt;cq-installation>/app* pasta.

## Parando o Adobe Experience Manager {#stopping-adobe-experience-manager}

Para interromper o AEM, siga um destes procedimentos:

* Dependendo da plataforma que você estiver usando:

   * Se você começou a AEM a partir de um script ou da linha de comando, pressione **Ctrl+C** para encerrar o servidor.
   * Se você tiver usado o script de início no UNIX, deverá usar o script de parada para parar o AEM.

* Se você começou a AEM clicando duas vezes no arquivo jar, clique no link **Ligado** na janela de inicialização (o botão então muda para **Desligado**) para encerrar o servidor.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Parando o Adobe Experience Manager da Linha de Comando {#stopping-adobe-experience-manager-from-the-command-line}

O `stop` script está disponível em *o &lt;cq-installation>/bin* diretório. As versões Unix e Windows são fornecidas. O script interrompe a instância em execução instalada em *&lt;cq-installation>* diretório.

### Exemplo de script de parada da plataforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Exemplo de script stop.bat da plataforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Se você quiser apenas pré-configurar o repositório (sem relocá-lo), basta:

* extrair `repository.xml` para o local necessário

* atualizar `repository.xml` conforme necessário

* criar `bootstrap.properties` e defina `repository.config`

Novamente, antes de iniciar a instalação real.
