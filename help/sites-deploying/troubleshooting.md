---
title: Resolução de problemas
seo-title: Troubleshooting
description: Este artigo aborda alguns dos problemas de instalação que você pode encontrar com o AEM.
seo-description: This article covers some of the installation issues you might encounter with AEM.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 1%

---

# Resolução de problemas{#troubleshooting}

Esta seção inclui informações detalhadas sobre logs disponíveis para ajudar você a solucionar problemas e também inclui informações sobre alguns dos problemas que você pode encontrar com o AEM.

## Solucionar problemas de desempenho do autor {#troubleshoot-author-performance}

A análise do desempenho lento na instância de criação pode se tornar bastante complexa. Como primeiro passo, é necessário descobrir em qual nível da tecnologia empilhada o desempenho está diminuindo.

A árvore de decisão a seguir fornece orientação para reduzir o gargalo.

![chlimage_1-75](assets/chlimage_1-75.png)

## Otimização básica {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configuração de arquivos de log e logs de auditoria {#configuring-log-files-and-audit-logs}

AEM registra registros detalhados que você pode querer configurar para solucionar problemas de instalação. Para obter informações, consulte o [Trabalhar com registros de auditoria e arquivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) seção.

## Uso da opção detalhada {#using-the-verbose-option}

Ao iniciar AEM WCM, é possível adicionar a opção -v (verboso) à linha de comando como em: java -jar cq-wcm-quickstart-&lt;version>.jar -v.

A opção detalhada exibe parte da saída de log do Quickstart no console para que possa ser usada para a solução de problemas.

## Problemas de instalação comuns {#common-installation-issues}

A seção a seguir descreve alguns problemas de instalação e suas soluções.

### Clicar duas vezes no jar do Quickstart não terá efeito ou abrirá o arquivo jar com outro programa (por exemplo, gerenciador de arquivos) {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

Isso geralmente indica um problema com a maneira como o ambiente de desktop do seu sistema operacional é configurado para abrir arquivos com a extensão .jar. Também pode indicar que você não tem o Java instalado ou que está usando uma versão não suportada do Java.

Como os arquivos jar usam o formato ZIP onipresente, alguns programas de arquivamento podem configurar automaticamente o desktop para abrir arquivos jar como arquivos de arquivamento.

Para solucionar problemas, faça o seguinte:

* Verifique se você tem pelo menos o Java versão 1.6 instalado.
* Tente um menu de contexto (normalmente clique com o botão direito do mouse) no Início rápido do WCM AEM e selecione &quot;Abrir com....&quot;
* Verifique se Java ou Sun Java está listado e tente executar AEM WCM com ele. Se você tiver várias versões do Java instaladas, selecione a suportada.

   Se você tiver êxito nessa etapa e seus sistemas operacionais oferecerem uma opção para sempre usar o programa selecionado para executar os arquivos .jar, selecione-o. Clicar duas vezes deve funcionar a partir de agora.

* Às vezes, reinstalar a versão do Java compatível ajuda a restaurar a associação correta.
* Você sempre pode executar o CRX usando a linha de comando ou iniciar/parar scripts conforme descrito anteriormente neste documento.

### Meu aplicativo em execução no CRX gera erros de falta de memória {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Consulte também [Analise problemas de memória](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html).


O próprio CRX tem um espaço de memória muito baixo. Se o aplicativo em execução no CRX tiver requisitos de memória maiores ou solicitar operações com muita memória (por exemplo, transações grandes), a instância da JVM em que o CRX é executado precisa ser iniciada com as configurações de memória apropriadas.

Use as opções de comando do Java para definir as configurações de memória da JVM (por exemplo, java -Xmx512m -jar crx&amp;ast;.jar para definir o heapsize como 512MB).

Especifique a opção de configuração de memória ao iniciar AEM WCM a partir da linha de comando. Os scripts AEM de início/parada do WCM ou os scripts personalizados para gerenciar AEM inicialização do WCM também podem ser modificados para definir as configurações de memória necessárias.

Se você já tiver definido seu tamanho de heap para 512 MB, talvez queira analisar o problema de memória ainda mais criando um despejo de heap:

Para criar automaticamente um despejo de heap ao ficar sem memória, use o seguinte comando:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

Isso gera um arquivo de despejo de heap (**java_...hprof**) sempre que o processo ficar sem memória. O processo pode continuar a ser executado depois que o despejo de heap foi gerado. Geralmente, um arquivo de despejo de heap é suficiente para analisar o problema.

### A tela de boas-vindas do AEM não exibe no navegador depois de clicar duas vezes no Início rápido do AEM {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

Em determinadas situações, as telas de boas-vindas do WCM AEM não são exibidas automaticamente, mesmo que o repositório em si esteja em execução com êxito. Isso pode depender da configuração do sistema operacional, da configuração do navegador ou de fatores similares.

O sintoma habitual é que a janela AEM WCM Quickstart exibe &quot;AEM WCM iniciando, aguardando a inicialização do servidor....&quot; Se essa mensagem for exibida por um tempo relativamente longo, insira o URL WCM AEM na janela do navegador manualmente, usando a porta 4502 padrão ou a porta em que a instância está sendo executada: http://localhost:4502/.

Além disso, os logs podem revelar o motivo para o navegador não iniciar.

Às vezes, a janela AEM WCM Quickstart tem a mensagem &quot;AEM WCM em execução em http://localhost:port/&quot; e o navegador não inicia automaticamente. Nesse caso, clique no URL na janela AEM WCM Quickstart (é um hiperlink) ou insira manualmente o URL no navegador.

Se tudo o resto falhar, verifique os logs para descobrir o que aconteceu.

### O site não é carregado ou falha intermitentemente com o Java 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}

Há um problema conhecido com a AEM 6.5 em execução no Java 11, em que o site pode não carregar ou falhar intermitentemente.

Se isso acontecer, siga a solução alternativa abaixo:

1. Abra o `sling.properties` sob o `crx-quickstart/conf/` pasta
1. Localize a seguinte linha:

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. Substitua por:

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. Reinicie a instância.

## Solução de problemas de instalações com um servidor de aplicativos {#troubleshooting-installations-with-an-application-server}

### Página não encontrada retornada ao solicitar uma página geometrixx-outdoor {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**Aplica-se ao WebLogic 10.3.5 e JBoss 5.1**

Quando uma solicitação para a página geometrixx-outdoors/en retorna uma página 404 (Página não encontrada), você pode verificar novamente se definiu a propriedade sling adicional no arquivo sling.properties necessária para esses Servidores de Aplicativo específicos.

Consulte no *Implantar AEM aplicação web* etapas para obter os detalhes.

### O tamanho do cabeçalho de resposta pode ser maior que 4 Kb {#response-header-size-can-be-greater-than-kb}

Os erros 502 podem indicar que o servidor da Web não pode lidar com o tamanho do cabeçalho de resposta HTTP AEM. AEM pode gerar cabeçalhos de resposta HTTP que incluem cookies de tamanho superior a 4 Kb. Certifique-se de que o contêiner de servlet esteja configurado de modo que o tamanho máximo do cabeçalho de resposta possa exceder 4 kb.

Por exemplo, para Tomcat 7.0, o atributo maxHttpHeaderSize da variável [Conector HTTP](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) controla as limitações do tamanho do cabeçalho.

## Desinstalação do Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Como o AEM é instalado em um único diretório, não há necessidade de um utilitário de desinstalação. A desinstalação pode ser tão simples quanto excluir todo o diretório de instalação, embora a forma como você desinstala o AEM dependa do que você deseja alcançar e do armazenamento persistente que você usa.

Se o armazenamento persistente estiver incorporado no diretório de instalação, por exemplo, na instalação padrão do TarPM, a exclusão de pastas também removerá os dados.

>[!NOTE]
>
>O Adobe recomenda fazer backup do repositório antes de excluir o AEM. Se você excluir o todo &lt;cq-installation-directory>, você excluirá o repositório. Para manter os dados do repositório antes de excluir, mover ou copiar o &lt;cq-installation-directory>/crx-quickstart/repository folder em outro lugar antes de excluir as outras pastas.

Se a sua instalação do AEM usar armazenamento externo, por exemplo, um servidor de banco de dados, a remoção de uma pasta não removerá os dados automaticamente, mas removerá a configuração de armazenamento, o que dificulta a restauração do conteúdo JCR.

### Arquivos JSP não são compilados no JBoss {#jsp-files-are-not-compiled-on-jboss}

Se você instalar ou atualizar arquivos JSP para o Experience Manager no JBoss e os servlets correspondentes não forem compilados, verifique se o compilador JSP do JBoss está configurado corretamente. Para obter informações, consulte o
[Problemas de compilação JSP no JBoss](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) artigo 10. o
