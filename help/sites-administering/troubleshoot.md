---
title: Solução de problemas do Adobe Experience Manager
description: Saiba como solucionar alguns problemas que podem surgir com o Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%
---
# Solução de problemas do Adobe Experience Manager {#troubleshooting-aem}

A seção a seguir aborda alguns problemas que você pode encontrar ao usar o AEM (Adobe Experience Manager), juntamente com sugestões sobre como solucioná-los.

>[!NOTE]
>
>Se você estiver solucionando problemas de criação no AEM, consulte [Solução de problemas para autores.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Quando você tiver problemas, também vale a pena verificar a lista de [Problemas conhecidos](/help/release-notes/release-notes.md) para sua instância (versão e service packs).

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
   <td><p>Meu aplicativo em execução no CRX emite erros de memória insuficiente</p> </td>
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

Consulte [Problemas Comuns de Instalação](/help/sites-deploying/troubleshooting.md#common-installation-issues) para obter informações sobre os seguintes cenários de solução de problemas:

* Clicar duas vezes no jar Quickstart não tem efeito ou o arquivo JAR com outro programa (como o gerenciador de arquivos).
* Os aplicativos em execução no CRX apresentam erros de falta de memória.
* A tela de boas-vindas do AEM não é exibida no navegador após clicar duas vezes no AEM Quickstart.

## Métodos de análise de solução de problemas {#methods-for-troubleshooting-analysis}

### Fazendo um despejo de encadeamento {#making-a-thread-dump}

O despejo de thread é uma lista de todas as threads do Java™ que estão ativas no momento. Se o AEM não responder corretamente, o despejo de thread poderá ajudar a identificar bloqueios ou outros problemas.

### Uso do Sling Thread Dumper {#using-sling-thread-dumper}

1. Abra o **AEM Web Console**; por exemplo, em `https://localhost:4502/system/console/`.
1. Selecione a guia **Threads** em **Status**.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Usando jstack (linha de comando) {#using-jstack-command-line}

1. Localize o PID (ID do processo) da instância do AEM Java™.

   Por exemplo, você pode usar `ps -ef` ou `jps`.

1. Executar:

   `jstack <pid>`

1. Mostra o despejo de thread.

>[!NOTE]
>
>Você pode anexar os despejos de thread a um arquivo de log usando o redirecionamento de saída `>>`:
>
>`jstack <pid> >> /path/to/logfile.log`

Consulte a documentação [Como remover despejos de thread de uma JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html) para obter mais informações

### Verificando sessões JCR não fechadas {#checking-for-unclosed-jcr-sessions}

Quando a funcionalidade é desenvolvida para o AEM WCM, as sessões JCR podem ser abertas (comparável à abertura de uma conexão de banco de dados). Se as sessões abertas nunca forem fechadas, o sistema pode apresentar os seguintes sintomas:

* O sistema fica mais lento.
* Você pode ver grande parte das entradas do CacheManager: resizeAll no arquivo de log; o seguinte número (tamanho=&lt;x>) shows the number of caches, each session opens several caches.
* Periodicamente, o sistema fica sem memória (após algumas horas, dias ou semanas - dependendo da gravidade).

Para começar a analisar sessões não fechadas, consulte o artigo da Base de Dados de Conhecimento [Unclosed Resource Resolver](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23761).

### Uso do console da Web do Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

O status dos pacotes OSGi também pode fornecer uma indicação antecipada de possíveis problemas.

1. Abra o **AEM Web Console**; por exemplo, em `https://localhost:4502/system/console/`.
1. Selecione **Pacotes** na guia **OSGI**.
1. Verificar:

   * o Status dos pacotes. Se algum estiver Inativo ou Insatisfeito, tente parar e reiniciar o pacote. Se o problema persistir, investigue mais usando outros métodos.
   * se algum dos pacotes tem dependências ausentes. Esses detalhes podem ser vistos ao clicar no Nome do pacote individual, que é um link (o exemplo a seguir não tem problemas):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
