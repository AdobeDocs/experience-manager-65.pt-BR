---
title: Como desenvolver projetos AEM usando o IntelliJ IDEA
description: Saiba como usar o IntelliJ IDEA para desenvolver projetos do Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Como desenvolver projetos AEM usando o IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Visão geral {#overview}

Para começar a usar o desenvolvimento do AEM no IntelliJ, as seguintes etapas são necessárias.

Cada etapa é explicada com mais detalhes no restante deste tópico.

* Instalar IntelliJ
* Configurar o projeto do AEM com base no Maven
* Preparar suporte JSP para IntelliJ no POM Maven
* Importar o projeto Maven para o IntelliJ

>[!NOTE]
>
>Este guia é baseado no IntelliJ IDEA Ultimate Edition 12.1.4 e AEM 5.6.1.

### Instalar IntelliJ IDEA {#install-intellij-idea}

Baixe o IntelliJ IDEA da [página Downloads na JetBrains](https://www.jetbrains.com/idea/download/).

Em seguida, siga as instruções de instalação nessa página.

### Configurar o projeto do AEM com base no Maven {#set-up-your-aem-project-based-on-maven}

Em seguida, configure seu projeto usando o Maven conforme descrito em [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

Para começar a trabalhar com Projetos AEM no IntelliJ IDEA, a configuração básica no [Introdução em 5 Minutos](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) é suficiente.

### Preparar suporte JSP para IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

O IntelliJ IDEA também pode fornecer suporte ao trabalhar com JSP, por exemplo:

* preenchimento automático de bibliotecas de tags
* reconhecimento de objetos definidos por `<cq:defineObjects />` e `<sling:defineObjects />`

Para que isso funcione, siga as instruções em [Como trabalhar com JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) em [Como criar projetos de AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importar o projeto Maven {#import-the-maven-project}

1. Abra a caixa de diálogo **Importar** no IntelliJ IDEA por

   * selecionando **Importar projeto** na tela de boas-vindas se ainda não houver um projeto aberto
   * selecionando **Arquivo > Importar projeto** no menu principal

1. Na caixa de diálogo Importar, selecione o arquivo POM do projeto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continue com as configurações padrão, conforme mostrado na caixa de diálogo abaixo.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Continue nas caixas de diálogo a seguir clicando em **Avançar** e **Concluir**.
1. Agora você está configurado para Desenvolvimento AEM usando IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Depurando JSPs com IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

As etapas a seguir são necessárias para depurar JSPs com o IntelliJ IDEA

* Configurar uma faceta da Web no projeto
* Instalar o plug-in de suporte a JSR45
* Configurar um perfil de depuração
* Configurar o AEM para o modo de depuração

#### Configurar uma faceta da Web no projeto {#set-up-a-web-facet-in-the-project}

O IntelliJ IDEA deve entender onde encontrar os JSPs para depuração. Como o IDEA não pode interpretar as configurações de `content-package-maven-plugin`, ele deve ser configurado manualmente.

1. Ir para **Arquivo > Estrutura de Projeto**
1. Selecione o módulo **Conteúdo**
1. Clique em **+** acima da lista de módulos e selecione **Web**
1. Como o Diretório de Recursos da Web, selecione o `content/src/main/content/jcr_root subdirectory` do seu projeto, conforme mostrado na captura de tela abaixo.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Instalar o plug-in de suporte a JSR45 {#install-the-jsr-support-plugin}

1. Vá para o painel **Plug-ins** nas configurações do IntelliJ IDEA
1. Navegue até o Plug-in **Integração JSR45** e marque a caixa de seleção ao lado dele
1. Clique em **Aplicar**
1. Reiniciar o IntelliJ IDEA quando solicitado a

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configurar um perfil de depuração {#configure-a-debug-profile}

1. Ir para **Executar > Editar configurações**
1. Clique em **+** e selecione **Remoto de JSR45**
1. Na caixa de diálogo de configuração, selecione **Configurar** ao lado de **Servidor de Aplicativos** e configure um servidor Genérico
1. Defina a página inicial com um URL apropriado se desejar abrir um navegador ao iniciar a depuração
1. Remova todas as tarefas **Antes da inicialização** se você usar a sincronização automática de vlt ou configurar as tarefas apropriadas do Maven se não usar
1. No painel **Inicialização/Conexão**, ajuste a porta, se necessário
1. Copiar os argumentos de linha de comando propostos pelo IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configurar o AEM para o modo de depuração {#configure-aem-for-debug-mode}

A última etapa necessária é iniciar o AEM com as opções JVM propostas pelo IntelliJ IDEA.

Inicie o arquivo jar AEM diretamente e adicione essas opções, por exemplo, com a seguinte linha de comando:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

Você também pode adicionar essas opções ao seu script de inicialização em `crx-quickstart/bin/start`, conforme mostrado abaixo.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Iniciar Depuração {#start-debugging}

Agora você está configurado para depurar os JSPs no AEM.

1. Selecione **Executar > Depurar > Seu Perfil De Depuração**
1. Definir pontos de interrupção no código do componente
1. Acessar uma página no seu navegador

![chlimage_1-52](assets/chlimage_1-52a.png)

### Depurando pacotes com IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

O código em pacotes pode ser depurado usando uma conexão de depuração remota genérica padrão. Você pode seguir a [documentação do Jetbrain sobre depuração remota](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
