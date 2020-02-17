---
title: Resolução de Problemas
seo-title: Resolução de Problemas
description: Este artigo aborda alguns dos problemas de instalação que você pode encontrar com o AEM.
seo-description: Este artigo aborda alguns dos problemas de instalação que você pode encontrar com o AEM.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Resolução de Problemas{#troubleshooting}

Esta seção inclui informações detalhadas sobre registros disponíveis para ajudá-lo a solucionar problemas e também informações sobre alguns dos problemas que você pode encontrar com o AEM.

## Solucionar problemas de desempenho do autor {#troubleshoot-author-performance}

Analisar o desempenho lento na instância de criação pode se tornar bastante complexo. Como primeira etapa, é necessário descobrir em qual nível da pilha de tecnologia o desempenho está diminuindo.

A seguinte árvore decisória fornece uma orientação para restringir o gargalo.

![chlimage_1-75](assets/chlimage_1-75.png)

## Otimização básica {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configurar arquivos de registro e registros de auditoria {#configuring-log-files-and-audit-logs}

O AEM registra registros detalhados que talvez você queira configurar para solucionar problemas de instalação. Para obter informações, consulte a seção [Trabalhando com registros de auditoria e arquivos](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) de registro.

## Uso da opção detalhada {#using-the-verbose-option}

Ao iniciar o AEM WCM, você pode adicionar a opção -v (verbose) à linha de comando como em: java -jar cq-wcm-quickstart-&lt;versão>.jar -v.

A opção detalhada exibe parte da saída de log do Quickstart no console, para que possa ser usada para solucionar problemas.

## Problemas comuns de instalação {#common-installation-issues}

A seção a seguir descreve alguns problemas de instalação e suas soluções.

### **Clicar duas vezes no jar do Quickstart não tem nenhum efeito ou abre o arquivo jar com outro programa (por exemplo, gerenciador de arquivos){#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}**

Isso normalmente indica um problema com a forma como o ambiente de desktop do seu sistema operacional está configurado para abrir arquivos com a extensão .jar. Isso também pode indicar que você não tem o Java instalado ou que está usando uma versão não suportada do Java.

Como os arquivos jar usam o formato ZIP onipresente, alguns dos programas de arquivamento podem configurar automaticamente a área de trabalho para abrir arquivos jar como arquivos de arquivamento.

Para solucionar problemas, faça o seguinte:

* Verifique se você tem pelo menos a versão 1.6 do Java instalada.
* Tente usar um menu de contexto (normalmente, clique com o botão direito do mouse) no Início rápido do AEM WCM e selecione &quot;Abrir com....&quot;
* Verifique se Java ou Sun Java está listado e tente executar o AEM WCM com ele. Se você tiver várias versões de Java instaladas, selecione a suportada.

   Se você tiver êxito com essa etapa e seus sistemas operacionais oferecerem uma opção para sempre usar o programa selecionado para executar os arquivos .jar, selecione-o. Clicar duas vezes deve funcionar a partir de agora.

* Às vezes, reinstalar a versão do Java compatível ajuda a restaurar a associação correta.
* Você sempre pode executar o CRX usando a linha de comando ou scripts de início/parada conforme descrito anteriormente neste documento.

### **Meu aplicativo em execução no CRX emite erros de falta de memória{#my-application-running-on-crx-throws-out-of-memory-errors}**

>[!NOTE]
>
>Consulte também [Analisar problemas](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)de memória.


O próprio CRX tem uma memória muito baixa. Se o aplicativo em execução no CRX tiver requisitos de memória maiores ou solicitar operações com muita memória (por exemplo, transações grandes), a instância JVM onde o CRX é executado precisa ser iniciada com as configurações de memória apropriadas.

Use as opções de comando Java para definir as configurações de memória do JVM (por exemplo, java -Xmx512m -jar crx&amp;ast;.jar para definir heapsize como 512MB).

Especifique a opção de configuração de memória ao iniciar o AEM WCM na linha de comando. Os scripts de inicialização/pausa do AEM WCM ou scripts personalizados para gerenciar a inicialização do AEM WCM também podem ser modificados para definir as configurações de memória necessárias.

Se você já tiver definido o tamanho do seu heapsize para 512 MB, talvez você queira analisar o problema de memória ainda mais criando um despejo de heap:

Para criar automaticamente um despejo de heap quando estiver sem memória, use o seguinte comando:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

Isso gera um arquivo de despejo heap (**java_...hprof**) sempre que o processo ficar sem memória. O processo pode continuar sendo executado depois que o despejo de heap for gerado. Normalmente, um arquivo de despejo heap é suficiente para analisar o problema.

### **A tela de boas-vindas do AEM não exibe no navegador depois de clicar duas vezes no Início rápido do AEM{#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}**

Em determinadas situações, as telas de boas-vindas do AEM WCM não são exibidas automaticamente, mesmo que o repositório esteja sendo executado com êxito. Isso pode depender da configuração do sistema operacional, da configuração do navegador ou de fatores similares.

O sintoma comum é que a janela Início rápido do WCM do AEM exibe &quot;Inicialização do WCM do AEM, aguardando a inicialização do servidor....&quot; Se essa mensagem for exibida por um tempo relativamente longo, insira o URL WCM AEM na janela do navegador manualmente, usando a porta padrão 4502 ou a porta na qual a instância está sendo executada: http://localhost:4502/.

Além disso, os registros podem revelar o motivo para o navegador não iniciar.

Às vezes, a janela Início rápido do WCM AEM tem a mensagem &quot;WCM AEM em execução em http://localhost:port/&quot; e o navegador não é iniciado automaticamente. Nesse caso, clique no URL na janela Início rápido do AEM WCM (é um hiperlink) ou insira manualmente o URL no navegador.

Se tudo o mais falhar, verifique os registros para descobrir o que aconteceu.

## Solução de problemas de instalações com um servidor de aplicativos {#troubleshooting-installations-with-an-application-server}

### **Página não encontrada retornada ao solicitar uma página geometrixx-outdoor{#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}**

**Aplica-se ao WebLogic 10.3.5 e JBoss 5.1**

Quando uma solicitação para a página geometrixx-outdoors/en retorna uma página 404 (Página não encontrada), você pode verificar novamente se definiu a propriedade sling adicional no arquivo sling.properties necessário para esses servidores de aplicativos específicos.

Consulte as etapas do aplicativo *da Web* Implantar AEM para obter detalhes.

### **O tamanho do cabeçalho de resposta pode ser maior que 4Kb{#response-header-size-can-be-greater-than-kb}**

Os erros 502 podem indicar que o servidor da Web não pode lidar com o tamanho do cabeçalho de resposta HTTP AEM. O AEM pode gerar cabeçalhos de resposta HTTP que incluem cookies de tamanho superior a 4 Kb. Certifique-se de que seu contêiner de servlet esteja configurado para que o tamanho máximo do cabeçalho de resposta possa exceder 4 kb.

Por exemplo, para Tomcat 7.0, o atributo maxHttpHeaderSize do Conector [](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) HTTP controla as limitações no tamanho do cabeçalho.

## Uninstalling Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Como o AEM é instalado em um único diretório, não há necessidade de um utilitário de desinstalação. A desinstalação pode ser tão simples quanto excluir o diretório de instalação inteiro, embora a maneira como você desinstala o AEM dependa do que você deseja obter e do armazenamento persistente que você usa.

Se o armazenamento persistente estiver incorporado no diretório de instalação, por exemplo, na instalação padrão do TarPM, a exclusão de pastas também remove dados.

>[!NOTE]
>
>A Adobe recomenda que você faça backup do repositório antes de excluir o AEM. Se você excluir todo o &lt;cq-installation-diretory>, excluirá o repositório. Para manter os dados do repositório antes de excluir, mova ou copie a pasta &lt;cq-installation-diretory>/crx-quickstart/repository em outro lugar antes de excluir as outras pastas.

Se a instalação do AEM usar armazenamento externo, por exemplo, um servidor de banco de dados, a remoção da pasta não removerá os dados automaticamente, mas removerá a configuração de armazenamento, o que dificulta a restauração do conteúdo do JCR.

### **Arquivos JSP não são compilados em JBoss{#jsp-files-are-not-compiled-on-jboss}**

Se você instalar ou atualizar arquivos JSP para o Experience Manager em JBoss e os servlets correspondentes não forem compilados, verifique se o compilador JSP JBoss está configurado corretamente. Para obter informações, consulte o artigo Problemas de compilação[JSP no JBoss](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) .
