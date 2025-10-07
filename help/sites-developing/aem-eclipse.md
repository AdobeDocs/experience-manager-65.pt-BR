---
title: Ferramentas de desenvolvedor do AEM para Eclipse
description: Saiba mais sobre as ferramentas de desenvolvedor do Adobe Experience Manager para Eclipse.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 5bd621b14e3bcd21431c1df5629fe4669b14052c
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 2%

---


# Ferramentas de desenvolvedor do AEM para Eclipse {#aem-developer-tools-for-eclipse}

![Ferramentas para desenvolvedores do Experience Manager para o logotipo Eclipse](assets/eclipse-logo.png)

## Visão geral {#overview}

As _Ferramentas para desenvolvedores do Experience Manager para Eclipse_ são um plug-in Eclipse baseado no [plug-in Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lançado com a Licença do Apache 2.

Ele oferece vários recursos que facilitam o desenvolvimento do AEM:

* Integração perfeita com instâncias do AEM por meio do Eclipse Server Connector
* Sincronização para conteúdo e pacotes OSGi
* Suporte à depuração com recurso de troca a quente de código
* Bootstrap simples de projetos do AEM por meio de um assistente de criação de projeto específico
* Fácil edição das propriedades do JCR

## Requisitos {#requirements}

Antes de usar as Ferramentas do desenvolvedor do AEM, é necessário:

* Baixe e instale o [Eclipse IDE para desenvolvedores Enterprise Java e Web.](https://www.eclipse.org/downloads/packages/)
   * A versão 1.4.0 das Ferramentas de desenvolvedor do AEM para Eclipse é compatível com Eclipse 2022-12 (4.26) ou mais recente e requer Java 17 ou mais recente para ser executada.
* Configure a instalação do Eclipse para garantir que você tenha pelo menos 1 GB de memória heap, editando o arquivo de configuração `eclipse.ini` conforme descrito nas [Perguntas frequentes sobre o Eclipse.](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)

>[!NOTE]
>
>No macOS, clique com o botão direito do mouse em **Eclipse.app** e selecione **Mostrar Conteúdo do Pacote** para encontrar seu `eclipse.ini`.

## Como instalar as ferramentas de desenvolvedor do AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Quando tiver atendido aos [requisitos](#requirements) acima, você poderá instalar o plug-in de ferramentas do desenvolvedor da seguinte maneira:

1. Abra o [Site de Ferramentas do Desenvolvedor do AEM.](https://eclipse.adobe.com/)

1. Copie o **Link de Instalação**.

   * Como alternativa, você pode baixar um arquivo em vez de usar o link de instalação.
   * Este método permite a instalação offline, mas você não recebe notificações automáticas de atualização.

1. No Eclipse, abra o menu **Ajuda**.
1. Clique em **Instalar novo software**.
1. Clique em **Adicionar...**.
1. No campo **Nome**, digite `AEM Developer Tools`.
1. No campo **Local**, copie a URL de instalação.
1. Clique em **Adicionar**.
1. Verifique os plug-ins do **AEM** e do **Sling**.
1. Clique em **Avançar**.
1. Na janela **Detalhes da Instalação**, revise os itens a serem instalados e clique novamente em **Avançar**.
1. Aceite os contratos de licença e clique em **Concluir**.
1. Na caixa de diálogo **Autoridades de Confiança** exibida, selecione a autoridade/site `https://eclipse.adobe.com` e clique em **Confiar em Selecionados**.
1. Na caixa de diálogo **Artefatos de Confiança** exibida, selecione os signatários do código e clique em **Confiar em Selecionados**.
1. Clique em **RestartNow** para reiniciar o Eclipse.

## A perspectiva da AEM {#the-aem-perspective}

No Eclipse, uma **Perspectiva** determina as ações e visualizações disponíveis em uma janela e permite a interação orientada a tarefas com recursos no Eclipse. Para obter mais detalhes sobre perspectivas, consulte a [documentação do Eclipse.](https://help.eclipse.org/latest/index.jsp).

As _Ferramentas de desenvolvimento do Experience Manager para Eclipse_ fornecem uma perspectiva do AEM que oferece controle total sobre seus projetos e instâncias do AEM. Para abrir a perspectiva do AEM:

1. Na barra de menus do Eclipse, selecione **Janela** > **Perspectiva** > **Abrir Perspectiva** > **Outras**.
1. Selecione **AEM** no diálogo e clique em **Abrir**.

![A perspectiva do AEM no Eclipse](assets/eclipse-aem-perspective.png)

## Exemplo de projeto de vários módulos {#sample-multi-module-project}

As _Ferramentas de desenvolvedor do Experience Manager para Eclipse_ vêm com uma amostra de projeto de vários módulos que ajuda você a se familiarizar rapidamente com uma configuração de projeto no Eclipse. Ele também serve como um guia de práticas recomendadas para vários recursos do AEM, aproveitando o [Arquétipo de Projetos AEM.](https://github.com/adobe/aem-project-archetype)

Siga estas etapas para criar o projeto de amostra:

1. No menu **Arquivo** > **Novo** > **Projeto**, navegue até a seção **AEM** e selecione **Projeto de vários módulos de exemplo do AEM**.

   ![Projeto de vários módulos de amostra do AEM](assets/aem-sample-project.png)

1. Clique em **Avançar**.

   >[!NOTE]
   >
   >Esta etapa pode demorar porque [m2eclipse](https://eclipse.dev/m2e/) deve verificar os catálogos de arquétipo.

1. `com.adobe.aem : aem-project-archetype : <highest-number>` deve ser selecionado automaticamente no menu suspenso **Arquétipo**. Selecione uma versão anterior, se desejar. Clique em **Avançar**.

   ![Selecionar versão do arquétipo](assets/select-archetype.png)

1. Forneça os seguintes campos para o projeto de amostra:

   * **Nome**
   * **Id Do Grupo**
   * **Id do artefato**
   * **appId** - Talvez seja necessário expandir as opções **Avançado** para definir esse valor.
   * **appTitle** - Talvez seja necessário expandir as opções **Avançado** para definir esse valor.
   * **Pacote** - Talvez seja necessário expandir as opções **Avançado** para definir este valor.

   ![Definir propriedades do arquétipo](assets/archetype-properties.png)

1. Clique em **Avançar**.

1. Configure um servidor AEM ao qual o Eclipse se conecta selecionando **Configurar novo servidor** e fornecendo um nome de servidor e os detalhes de conexão necessários.

   ![Conectar-se ao servidor do AEM](assets/connect-server.png)

   * Para usar o recurso de depuração, você precisa iniciar o AEM no modo de depuração fornecendo o parâmetro `-agentlib`, por exemplo:

   ```text
   $ java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar aem-author-p4502.jar
   ```

   >[!TIP]
   >
   >Para obter mais detalhes sobre como depurar seu projeto em execução em um AEM SDK local, consulte o documento [Depuração remota do AEM SDK.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-sdk/remote-debugging)

1. Clique em **Concluir**.

A estrutura do projeto é criada. Pode levar algum tempo para baixar os artefatos necessários no projeto.

>[!NOTE]
>
>Em uma nova instalação ou quando as dependências do Maven não tiverem sido baixadas anteriormente, o Eclipse poderá relatar que o projeto foi criado com erros. Nesse caso, siga o procedimento descrito na seção [Resolvendo Definição de Projeto Inválida.](#resolving-invalid-project-definition)

## Como Importar Projetos Existentes {#how-to-import-existing-projects}

Use o recurso **Novo Projeto** para criar a estrutura básica do projeto.

1. Siga as instruções para criar um [Projeto de Vários Módulos de Amostra,](#sample-multi-module-project) que cria uma estrutura básica de projeto com uma separação íntegra de preocupações:

   * `PROJECT.ui.apps` para conteúdo de `/apps` e `/etc`
   * `PROJECT.ui.content` para `/content` criado
   * `PROJECT.core` para pacotes Java
   * `PROJECT.it.launcher` e `PROJECT.it.tests` para testes de integração

1. Substitua o conteúdo do projeto `PROJECT.ui.apps` pelas pastas `apps` e `etc` do pacote:

   1. No painel **Project Explorer**, expanda `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Clique com o botão direito do mouse na pasta `apps` e escolha **Mostrar em** > **System Explorer**.
   1. Exclua as pastas `apps` e `etc` lá.
   1. No mesmo local, coloque as pastas `apps` e `etc` do seu pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no projeto `PROJECT.ui.apps` e escolha **Atualizar**.

1. Em seguida, faça o mesmo para `PROJECT.ui.content` e substitua sua pasta de conteúdo pela de seus pacotes:

   1. No painel **Project Explorer**, expanda `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Clique com o botão direito do mouse na pasta de conteúdo mais profundo e escolha **Mostrar em** > **System Explorer**.
   1. Exclua a pasta de conteúdo lá.
   1. No mesmo local, coloque a pasta de conteúdo do seu pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no projeto `PROJECT.ui.content` e escolha **Atualizar**.

1. Atualize os `filter.xml` arquivos desses dois projetos para corresponder ao conteúdo do seu pacote de conteúdo abrindo o `META-INF/vault/filter.xml` arquivo do seu pacote de conteúdo em um editor de texto/código separado.

   * Este é um exemplo de como o arquivo `filter.xml` pode ser:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. Quanto ao conteúdo do seu pacote que foi dividido em dois projetos, você também deve dividir essas regras de filtro em dois e atualizar os arquivos `filter.xml` dos dois projetos adequadamente.

   1. No Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Substitua o conteúdo do elemento `<workspaceFilter>` pelas regras do seu pacote que começam com `/apps` e `/etc`
      * Por exemplo:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. Em seguida, abra `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Substitua as regras pelas do seu pacote que começam com `/content`.
      * Por exemplo:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. Certifique-se de salvar todas as alterações. Agora você pode sincronizar esse novo conteúdo para sua instância do AEM.

1. No painel **Servidores**, verifique se a conexão foi iniciada e, se for o caso, não a inicie.

1. Clique no ícone **Limpar e publicar**.

Depois de concluído, o pacote deve estar em execução na sua instância. Ao salvar, qualquer alteração é sincronizada automaticamente com a instância.

Se quiser recriar um pacote de seu projeto, clique com o botão direito do mouse em `PROJECT.ui.apps` ou `PROJECT.ui.content` e escolha **Executar como** > **Instalação do Maven**.

Agora você tem uma pasta de destino criada com seu pacote (chamada, por exemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Resolução de problemas {#troubleshooting}

### Resolvendo Definição de Projeto Inválida {#resolving-invalid-project-definition}

Para resolver dependências inválidas e a definição do projeto, proceda da seguinte maneira:

1. Selecione todos os projetos criados.
1. Clique com o botão direito do mouse em.
1. No menu de contexto, selecione **Maven** > **Atualizar projetos**.
1. Verificar **Forçar Atualizações de Instantâneos/Versões**.
1. Clique em **OK**.

O Eclipse baixa as dependências necessárias. Isso pode demorar um pouco.

## Mais informações {#more-information}

A ferramenta oficial do Apache Sling IDE para o site do Eclipse fornece informações adicionais úteis:

* O [**Guia do Usuário do Apache Sling IDE para Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html) orienta você pelos conceitos gerais, pela integração do servidor e pelos recursos de implantação compatíveis com as Ferramentas de Desenvolvimento do AEM.
* [Solução de problemas da ferramenta Apache Sling IDE](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [Lista de problemas conhecidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

A documentação oficial [Eclipse](https://www.eclipse.org/) a seguir pode ajudar a configurar seu ambiente:

* [Introdução ao Eclipse](https://eclipseide.org/getting-started/)
* [Sistema de Ajuda do Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integração do Maven (m2eclipse)](https://www.eclipse.org/m2e/)
