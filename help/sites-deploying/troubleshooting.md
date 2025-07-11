---
title: Solução de problemas de instalação com o AEM
description: Este artigo aborda alguns dos problemas de instalação que você pode encontrar no AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 0%

---

# Solução de problemas de instalação com o AEM{#troubleshooting}

Esta seção inclui informações detalhadas sobre os logs disponíveis para ajudá-lo a solucionar problemas e também inclui informações sobre alguns dos problemas que você pode encontrar com o AEM.

## Solução de problemas de desempenho do autor {#troubleshoot-author-performance}

A análise de desempenho lento na instância de criação pode se tornar complexa. Como primeiro passo, é necessário descobrir em qual nível da pilha de tecnologia o desempenho está diminuindo.

A árvore decisória a seguir fornece orientação para restringir o gargalo.

![chlimage_1-75](assets/chlimage_1-75.png)

## Otimização básica {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configuração de arquivos de log e logs de auditoria {#configuring-log-files-and-audit-logs}

O AEM registra logs detalhados que você pode querer configurar para solucionar problemas de instalação. Para obter informações, consulte a seção [Trabalhando com registros de auditoria e arquivos de log](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Uso da Opção Detalhada {#using-the-verbose-option}

Ao iniciar o AEM WCM, você pode adicionar a opção -v (verboso) à linha de comando como em: java -jar cq-wcm-quickstart-&lt;version>.jar -v.

A opção detalhada exibe parte da saída de log do Quickstart no console, para que possa ser usada para a solução de problemas.

## Problemas comuns de instalação {#common-installation-issues}

A seção a seguir descreve alguns problemas de instalação e suas soluções.

### Clicar duas vezes no jar Quickstart não tem efeito ou abre o arquivo jar com outro programa (por exemplo, gerenciador de arquivos) {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

Esse problema geralmente indica um problema com a forma como o ambiente de desktop do sistema operacional está configurado para abrir arquivos com extensão .jar. Ela também pode indicar que você não tem o Java™ instalado ou que você está usando uma versão não compatível do Java™.

Como os arquivos jar usam o formato ZIP onipresente, alguns dos programas de arquivamento podem configurar automaticamente a área de trabalho para abrir arquivos jar como arquivos mortos.

Para solucionar problemas, faça o seguinte:

* Verifique se você tem pelo menos a versão 1.6 do Java™ instalada.
* Experimente um menu de contexto (normalmente, clique com o botão direito do mouse) no Quickstart do AEM WCM e selecione &quot;Abrir com...&quot;
* Verifique se Java™ ou Sun Java™ está listado e tente executar o AEM WCM com ele. Se você tiver várias versões do Java™ instaladas, selecione a compatível.

  Se você tiver êxito nesta etapa e seu sistema operacional oferecer uma opção para sempre usar o programa selecionado para executar os arquivos .jar, selecione-o. Clicar duas vezes deve funcionar a partir de agora.

* Às vezes, reinstalar a versão compatível do Java™ ajuda a restaurar a associação correta.
* Você sempre pode executar o CRX usando a linha de comando ou scripts de iniciar/parar, conforme descrito anteriormente neste documento.

### Meu aplicativo em execução no CRX emite erros de memória insuficiente {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Consulte também [Analisar problemas de memória](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=pt-BR).


O próprio CRX tem pouco espaço de memória. Se a aplicação em execução no CRX tiver requisitos de memória maiores ou solicitar operações com muita memória (por exemplo, transações grandes), a instância da JVM em que o CRX é executado deverá ser iniciada com configurações de memória apropriadas.

Use as opções de comando do Java™ para definir as configurações de memória da JVM (por exemplo, java -Xmx512m -jar crx&ast;.jar para definir heapsize como 512 MB).

Especifique a opção de configuração de memória ao iniciar o AEM WCM a partir da linha de comando. Os scripts de inicialização/interrupção do AEM WCM ou os scripts personalizados para gerenciar a inicialização do AEM WCM também podem ser modificados para definir as configurações de memória necessárias.

Se você já tiver definido o tamanho do heap como 512 MB, convém analisar mais detalhadamente o problema de memória criando um despejo de heap.

Para criar automaticamente um despejo de heap ao ficar sem memória, use o seguinte comando:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &ast;.jar

Este método gera um arquivo de despejo de heap (**java_...hprof**) sempre que o processo fica sem memória. O processo pode continuar a ser executado após a geração do despejo de heap.

Geralmente, três arquivos de despejo de heap, coletados durante um período, são necessários para analisar o problema:

* Antes que ocorra uma falha
* Durante a falha 1
* Durante a falha 2
* *Idealmente, também seria bom coletar informações após o evento ser resolvido*

Eles podem ser comparados para ver as alterações e como os objetos estão usando a memória.

>[!NOTE]
>
>Se você coletar regularmente essas informações ou se tiver experiência na leitura de despejos de heap, um arquivo de despejo de heap pode ser suficiente para analisar o problema.

### A tela de boas-vindas do AEM não é exibida no navegador após clicar duas vezes no AEM Quickstart {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

Em determinadas situações, as telas de boas-vindas do AEM WCM não são exibidas automaticamente, mesmo que o repositório em si esteja sendo executado com êxito. Esse problema pode depender da configuração do sistema operacional, da configuração do navegador ou de fatores semelhantes.

O sintoma comum é que a janela AEM WCM Quickstart exibe &quot;AEM WCM inicializando, aguardando a inicialização do servidor...&quot; Se essa mensagem for exibida por um tempo relativamente longo, insira manualmente o URL do AEM WCM na janela do navegador, usando a porta 4502 padrão ou a porta em que a instância está sendo executada: http://localhost:4502/.

Além disso, os registros podem revelar o motivo pelo qual o navegador não está sendo iniciado.

Às vezes, a janela de início rápido do AEM WCM exibe a mensagem &quot;AEM WCM em execução em http://localhost:port/&quot; e o navegador não é iniciado automaticamente. Nesse caso, clique no URL na janela Quickstart do AEM WCM (é um hiperlink) ou insira manualmente o URL no navegador.

Se tudo falhar, verifique os logs para descobrir o que aconteceu.

### O site não carrega ou falha intermitentemente com o Java™ 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}

Há um problema conhecido com o AEM 6.5 em execução no Java™ 11, no qual o site pode não ser carregado ou falhar intermitentemente.

Se esse problema ocorrer, faça o seguinte:

1. Abra o arquivo `sling.properties` na pasta `crx-quickstart/conf/`
1. Localize a seguinte linha:

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. Substitua-o pelo seguinte:

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. Reinicie a instância.

## Solução de problemas de instalações com um servidor de aplicativos {#troubleshooting-installations-with-an-application-server}

### Página não encontrada retornada ao solicitar uma página geometrixx-outdoor {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**Aplicável ao WebLogic 10.3.5 e JBoss® 5.1**

Quando uma solicitação para a página geometrixx-outdoors/en retorna um erro 404 (Página não encontrada), é possível verificar novamente se você definiu a propriedade sling adicional no arquivo sling.properties necessário para esses Servidores de aplicativos específicos.

Consulte as etapas *Implantar aplicativo Web do AEM* para obter detalhes.

### O tamanho do cabeçalho de resposta pode ser maior que 4 KB {#response-header-size-can-be-greater-than-kb}

Os erros 502 podem indicar que o servidor Web não pode lidar com o tamanho do cabeçalho de resposta HTTP do AEM. O AEM pode gerar cabeçalhos de resposta HTTP que incluem cookies com tamanho superior a 4 KB. Certifique-se de que o container de servlet esteja configurado para que o tamanho máximo do cabeçalho de resposta possa exceder 4 KB.

Por exemplo, para Tomcat 7.0, o atributo maxHttpHeaderSize do [Conector HTTP](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) controla as limitações no tamanho do cabeçalho.

## Desinstalação do Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Como o AEM é instalado em um único diretório, não há necessidade de um utilitário de desinstalação. A desinstalação pode ser tão simples quanto excluir todo o diretório de instalação, embora a forma como você desinstala o AEM dependa do que você deseja obter e do armazenamento persistente que usa.

Se o armazenamento persistente estiver incorporado no diretório de instalação, por exemplo, na instalação padrão do TarPM, a exclusão de pastas também removerá os dados.

>[!NOTE]
>
>A Adobe recomenda fazer backup do repositório antes de excluir o AEM. Se você excluir todo o &lt;cq-installation-diretory>, também excluirá o repositório. Para manter os dados do repositório antes de excluir, mova ou copie a pasta &lt;cq-installation-diretory>/crx-quickstart/repository em outro lugar antes de excluir as outras pastas.

Se sua instalação do AEM usar armazenamento externo, por exemplo, um servidor de banco de dados, a remoção da pasta não removerá os dados automaticamente, mas removerá a configuração de armazenamento, o que dificultará a restauração do conteúdo JCR.
