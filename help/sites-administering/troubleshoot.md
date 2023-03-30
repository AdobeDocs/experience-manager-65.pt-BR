---
title: Solução de problemas de AEM
seo-title: Troubleshooting AEM
description: Saiba mais sobre como solucionar problemas com o AEM.
seo-description: Learn about troubleshooting issues with AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: e147605ff4d5c3d2403632285956559db235c084
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Solução de problemas de AEM {#troubleshooting-aem}

A seção a seguir aborda alguns problemas que você pode encontrar ao usar o AEM, juntamente com sugestões sobre como resolvê-los.

>[!NOTE]
>
>Se você estiver solucionando problemas de criação no AEM, consulte [Solução de problemas para autores.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Ao enfrentar problemas, também vale a pena verificar a lista de [Problemas conhecidos](/help/release-notes/release-notes.md) para sua instância (pacotes de versões e serviços).

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
   <td><p>Clicar duas vezes no Quickstart jar não tem efeito ou abre o arquivo jar com outro programa (por exemplo, gerenciador de arquivos)</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> </td>
   <td><p>Meu aplicativo em execução no CRX gera erros de falta de memória</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> </td>
   <td><p>A tela de boas-vindas AEM não é exibida no navegador após clicar duas vezes AEM CM Quickstart</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> <p>usuário administrador</p> </td>
   <td><p>Fazer um despejo de encadeamento</p> </td>
  </tr>
  <tr>
   <td><p>Administrador do sistema</p> <p>usuário administrador</p> </td>
   <td><p>Verificando se há sessões JCR não fechadas</p> </td>
  </tr>
 </tbody>
</table>

## Problemas de instalação {#installation-issues}

Consulte [Problemas de instalação comuns](/help/sites-deploying/troubleshooting.md#common-installation-issues) para obter informações sobre os seguintes cenários de solução de problemas:

* Clicar duas vezes no jar do Quickstart não terá efeito ou o arquivo JAR com outro programa (como o gerenciador de arquivos).
* Os aplicativos em execução em CRX lançam erros de falta de memória.
* A tela AEM Welcome não é exibida no navegador após clicar duas vezes AEM Quickstart.

## Métodos para análise de solução de problemas {#methods-for-troubleshooting-analysis}

### Fazer um despejo de encadeamento {#making-a-thread-dump}

O despejo de threads é uma lista de todos os threads Java™ que estão ativos no momento. Se AEM não responder corretamente, o despejo de thread poderá ajudar a identificar bloqueios ou outros problemas.

### Uso do despejo de encadeamento Sling {#using-sling-thread-dumper}

1. Abra o **Console da Web AEM**; por exemplo, em `https://localhost:4502/system/console/`.
1. Selecione o **Threads** under **Status** guia .

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Uso de jstack (linha de comando) {#using-jstack-command-line}

1. Encontre o PID (id do processo) da instância AEM do Java™.

   Por exemplo, você pode usar `ps -ef` ou `jps`.

1. Executar:

   `jstack <pid>`

1. Mostra o despejo de encadeamento.

>[!NOTE]
>
>Você pode anexar os dumps de encadeamento a um arquivo de log usando o `>>` redirecionamento de saída:
>
>`jstack <pid> >> /path/to/logfile.log`

Consulte a [Como tirar os despejos de encadeamento de uma JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=en) documentação para obter mais informações

### Verificando se há sessões JCR não fechadas {#checking-for-unclosed-jcr-sessions}

Quando a funcionalidade é desenvolvida para AEM WCM, as Sessões JCR podem ser abertas (comparável à abertura de uma conexão de banco de dados). Se as sessões abertas nunca estiverem fechadas, o sistema poderá apresentar os seguintes sintomas:

* O sistema fica mais lento.
* Você pode ver muito do CacheManager: resizeAll entradas no arquivo de log; o seguinte número (tamanho=&lt;x>) mostra o número de caches, cada sessão abre vários caches.
* De tempos em tempos, o sistema fica sem memória (após algumas horas, dias ou semanas - dependendo da gravidade).

Para analisar sessões não fechadas e descobrir qual código não está fechando uma sessão, consulte o artigo da Base de conhecimento [Analisar Sessões Não Fechadas](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Uso do Console da Web do Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

O status dos pacotes OSGi também pode fornecer uma indicação prévia de possíveis problemas.

1. Abra o **Console da Web AEM**; por exemplo, em `https://localhost:4502/system/console/`.
1. Selecionar **Pacotes** under **OSGI** guia .
1. Verificar:

   * o Status dos pacotes. Se algum estiver Inativo ou insatisfeito, tente parar e reiniciar o pacote. Se o problema persistir, investigue mais sobre como usar outros métodos.
   * se qualquer um dos pacotes tem dependências ausentes. Esses detalhes podem ser visualizados clicando no Nome do pacote individual, que é um link (o exemplo a seguir não tem problemas):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
