---
title: Solução de problemas do Adobe Experience Manager
description: Saiba como solucionar alguns problemas que podem surgir com o Adobe Experience Manager.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 3%

---

# Solução de problemas do Adobe Experience Manager {#troubleshooting-aem}

A seção a seguir aborda alguns problemas que você pode encontrar ao usar o AEM (Adobe Experience Manager), juntamente com sugestões sobre como solucioná-los.

>[!NOTE]
>
>Se estiver solucionando problemas de criação no AEM, consulte [Solução de problemas para autores.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Em caso de problemas, vale a pena também verificar a lista de [Problemas conhecidos](/help/release-notes/release-notes.md) para sua instância (versão e service packs).

## Cenários de solução de problemas para administradores {#troubleshooting-scenarios-for-administrators}

A tabela a seguir fornece uma visão geral dos problemas que os administradores podem solucionar:

<table>
 <tbody>
  <tr>
   <td><strong>Função</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Administrador do sistema</td>
   <td><p>Clicar duas vezes no jar Quickstart não tem efeito ou abre o arquivo jar com outro programa (por exemplo, gerenciador de arquivos)</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> </td>
   <td><p>Meu aplicativo em execução no CRX emite erros de falta de memória</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> </td>
   <td><p>A tela de boas-vindas do AEM não é exibida no navegador após clicar duas vezes no AEM CM Quickstart</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> <p>usuário administrador</p> </td>
   <td><p>Fazendo um despejo de encadeamento</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> <p>usuário administrador</p> </td>
   <td><p>Verificando sessões JCR não fechadas</p> </td>
  </tr>
 </tbody>
</table>

## Problemas de instalação {#installation-issues}

Consulte [Problemas comuns de instalação](/help/sites-deploying/troubleshooting.md#common-installation-issues) para obter informações sobre os seguintes cenários de solução de problemas:

* Clicar duas vezes no jar Quickstart não tem efeito ou o arquivo JAR com outro programa (como o gerenciador de arquivos).
* Os aplicativos em execução no CRX lançam erros de falta de memória.
* A tela de boas-vindas do AEM não é exibida no navegador após clicar duas vezes no AEM Quickstart.

## Métodos de análise de solução de problemas {#methods-for-troubleshooting-analysis}

### Fazendo um despejo de encadeamento {#making-a-thread-dump}

O despejo de thread é uma lista de todas as threads do Java™ que estão ativas no momento. Se o AEM não responder corretamente, o despejo de encadeamento pode ajudar a identificar bloqueios ou outros problemas.

### Uso do Sling Thread Dumper {#using-sling-thread-dumper}

1. Abra o **Console da Web AEM**; por exemplo, em `https://localhost:4502/system/console/`.
1. Selecione o **Threads** em **Status** guia.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Usando jstack (linha de comando) {#using-jstack-command-line}

1. Localize o PID (ID do processo) da instância do Java™ AEM.

   Por exemplo, você pode usar `ps -ef` ou `jps`.

1. Executar:

   `jstack <pid>`

1. Mostra o despejo de thread.

>[!NOTE]
>
>Você pode anexar os despejos de thread a um arquivo de log usando o `>>` redirecionamento de saída:
>
>`jstack <pid> >> /path/to/logfile.log`

Consulte a [Como fazer despejos de thread de uma JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=pt-BR) documentação para obter mais informações

### Verificando sessões JCR não fechadas {#checking-for-unclosed-jcr-sessions}

Quando a funcionalidade é desenvolvida para o WCM do AEM, as sessões JCR podem ser abertas (comparável à abertura de uma conexão de banco de dados). Se as sessões abertas nunca forem fechadas, o sistema pode apresentar os seguintes sintomas:

* O sistema fica mais lento.
* Você pode ver grande parte das entradas do CacheManager: resizeAll no arquivo de log; o seguinte número (size=&lt;x>) mostra o número de caches, cada sessão abre vários caches.
* Periodicamente, o sistema fica sem memória (após algumas horas, dias ou semanas - dependendo da gravidade).

Para analisar sessões não fechadas e descobrir qual código não está fechando uma sessão, consulte o artigo da Base de conhecimento [Analisar Sessões Não Fechadas](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Uso do console da Web do Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

O status dos pacotes OSGi também pode fornecer uma indicação antecipada de possíveis problemas.

1. Abra o **Console da Web AEM**; por exemplo, em `https://localhost:4502/system/console/`.
1. Selecionar **Pacotes** em **OSGI** guia.
1. Verificar:

   * o Status dos pacotes. Se algum estiver Inativo ou Insatisfeito, tente parar e reiniciar o pacote. Se o problema persistir, investigue mais usando outros métodos.
   * se algum dos pacotes tem dependências ausentes. Esses detalhes podem ser vistos ao clicar no Nome do pacote individual, que é um link (o exemplo a seguir não tem problemas):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
