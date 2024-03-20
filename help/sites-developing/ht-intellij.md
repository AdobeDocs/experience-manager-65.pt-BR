---
title: Como desenvolver projetos AEM usando o IntelliJ IDEA
description: Saiba como usar o IntelliJ IDEA para desenvolver projetos do Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
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

Baixar IntelliJ IDEA de [a página de downloads na JetBrains](https://www.jetbrains.com/idea/download/).

Em seguida, siga as instruções de instalação nessa página.

### Configurar o projeto do AEM com base no Maven {#set-up-your-aem-project-based-on-maven}

Em seguida, configure seu projeto usando o Maven, conforme descrito em [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

Para começar a trabalhar com Projetos AEM no IntelliJ IDEA, a configuração básica no [Introdução em 5 minutos](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) é suficiente.

### Preparar suporte JSP para IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

O IntelliJ IDEA também pode fornecer suporte ao trabalhar com JSP, por exemplo:

* preenchimento automático de bibliotecas de tags
* reconhecimento de objetos definidos por `<cq:defineObjects />` e `<sling:defineObjects />`

Para isso, siga as instruções em [Como trabalhar com JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importar o projeto Maven {#import-the-maven-project}

1. Abra o **Importar** caixa de diálogo no IntelliJ IDEA por

   * seleção **Importar projeto** na tela de boas-vindas, se você ainda não tiver um projeto aberto
   * seleção **Arquivo > Importar projeto** no menu principal

1. Na caixa de diálogo Importar, selecione o arquivo POM do projeto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continue com as configurações padrão, conforme mostrado na caixa de diálogo abaixo.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Prossiga pelas caixas de diálogo a seguir clicando em **Próxima** e **Concluir**.
1. Agora você está configurado para Desenvolvimento AEM usando IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Depurando JSPs com IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

As etapas a seguir são necessárias para depurar JSPs com o IntelliJ IDEA

* Configurar uma faceta da Web no projeto
* Instalar o plug-in de suporte a JSR45
* Configurar um perfil de depuração
* Configurar o AEM para o modo de depuração

#### Configurar uma faceta da Web no projeto {#set-up-a-web-facet-in-the-project}

O IntelliJ IDEA deve entender onde encontrar os JSPs para depuração. Porque IDEA não pode interpretar o `content-package-maven-plugin` configurações, ele deve ser configurado manualmente.

1. Ir para **Arquivo > Estrutura de projeto**
1. Selecione o **Conteúdo** módulo
1. Clique em **+** acima da lista de módulos e selecione **Web**
1. Como o Diretório de Recursos da Web, selecione o `content/src/main/content/jcr_root subdirectory` do seu projeto, conforme mostrado na captura de tela abaixo.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Instalar o plug-in de suporte a JSR45 {#install-the-jsr-support-plugin}

1. Vá para a **Plug-ins** painel nas configurações do IntelliJ IDEA
1. Navegue até a **Integração JSR45** Plug-in e marque a caixa de seleção ao lado dele
1. Clique em **Aplicar**
1. Reiniciar o IntelliJ IDEA quando solicitado a

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configurar um perfil de depuração {#configure-a-debug-profile}

1. Ir para **Executar > Editar configurações**
1. Clique em **+** e selecione **Remoto JSR45**
1. Na caixa de diálogo de configuração, selecione **Configurar** ao lado de **Servidor de aplicativos** e configurar um servidor genérico
1. Defina a página inicial com um URL apropriado se desejar abrir um navegador ao iniciar a depuração
1. Remover tudo **Antes do lançamento** tarefas se você usar a sincronização automática de vlt ou configurar tarefas apropriadas do Maven se não
1. No **Inicialização/Conexão** ajuste a porta, se necessário
1. Copiar os argumentos de linha de comando propostos pelo IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configurar o AEM para o modo de depuração {#configure-aem-for-debug-mode}

A última etapa necessária é iniciar o AEM com as opções JVM propostas pelo IntelliJ IDEA.

Inicie o arquivo jar AEM diretamente e adicione essas opções, por exemplo, com a seguinte linha de comando:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

Você também pode adicionar essas opções ao script de inicialização em `crx-quickstart/bin/start` conforme mostrado abaixo.

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

1. Selecionar **Executar > Depurar > Seu Perfil De Depuração**
1. Definir pontos de interrupção no código do componente
1. Acessar uma página no seu navegador

![chlimage_1-52](assets/chlimage_1-52a.png)

### Depurando pacotes com IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

O código em pacotes pode ser depurado usando uma conexão de depuração remota genérica padrão. Você pode seguir o [Documentação do Jetbrain sobre depuração remota](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
