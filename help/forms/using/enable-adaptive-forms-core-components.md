---
title: Como ativar os Componentes principais do Forms adaptável no AEM 6.5 Forms?
description: Guia passo a passo para ajudá-lo a ativar os Componentes principais do Forms adaptável em um ambiente de Forms AEM 6.5.
keywords: Ativar componentes principais, componentes principais Forms adaptável, componentes principais no 6.5, componentes principais Forms adaptáveis no AEM 6.5, componentes principais AF no AEM AEM 6.5, 6.5, componentes principais Forms do 6.5
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms, Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
source-git-commit: 6cec9874bff54dea63562f7a880429d54e83ba79
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 3%

---

# Ativar os componentes principais adaptáveis do Forms no AEM 6.5 Forms {#enable-adaptive-forms-core-components}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

Habilitar os Componentes principais adaptáveis do Forms permite que você comece a criar, publicar e fornecer [Forms adaptável baseado em componentes principais](create-an-adaptive-form-core-components.md) e [Forms adaptável headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR) do seu ambiente AEM 6.5 Forms.

Para ativar os Componentes principais do Adaptive Forms no ambiente AEM 6.5 Forms, configure e implante um [Arquétipo AEM 41 ou posterior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) projeto baseado em (com as opções de formulários ativadas) em todas as instâncias do Autor e de Publicação.

Este artigo fornece instruções detalhadas para configurar e implantar o Arquétipo AEM 41 ou posterior com base em seu ambiente AEM 6.5 Forms para ativar os Componentes principais adaptáveis do Forms. Consulte a lista abaixo para obter **AEM 6.5** versões compatíveis para ativar os Componentes principais do Forms:

## Pré-requisitos {#prerequisites}

Antes de ativar os Componentes principais do Adaptive Forms em um ambiente AEM 6.5 Forms:

* [Atualizar para AEM 6.5 Forms Service Pack 16 (6.5.16.0) ou posterior](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* Instale a versão mais recente do [Apache Maven](https://maven.apache.org/download.cgi).

* Instale um editor de texto simples. Por exemplo, Microsoft Visual Studio Code.

## Criar e implantar o projeto mais recente baseado no Arquétipo AEM

Para criar um Arquétipo AEM 41 ou [posteriormente](https://github.com/adobe/aem-project-archetype) projeto baseado em e implantá-lo em todas as suas instâncias de Autor e Publicação:

1. Faça logon no computador, hospedando e executando a instância do Forms AEM 6.5, como administrador.
1. Abra o prompt de comando ou terminal e execute o seguinte comando para criar um projeto do Arquétipo AEM (com as opções de formulários ativadas):

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux ou Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   Ao executar o comando acima, considere os seguintes pontos:

   * Não altere o valor de `aemVersion` propriedade de `6.5.15.0` a qualquer outra coisa.

   * Defina o `archetypeVersion` propriedade para `41` ou posteriormente. Para obter a versão mais recente, consulte a seção requisitos de sistema em [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype) documentação.

   * Atualize o comando para refletir os valores específicos do seu ambiente, incluindo o `appTitle`, `appId`, e `groupId`. Além disso, defina o valor do  `includeFormsenrollment` propriedade para `y`. Se você usa o Forms Portal, defina a variável `includeExamples=y` opção para incluir os Componentes principais do Forms Portal no projeto.


1. (Somente para projetos baseados no Arquétipo versão 41) Depois que o projeto Arquétipo AEM for criado, ative temas para o Forms adaptável baseado em Componentes principais. Para ativar temas:

   1. Abra o [Pasta de projeto do arquétipo AEM]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html para edição:

   1. Adicione o seguinte código na linha 21:

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Adicionar o código mencionado acima na linha 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Salvar e fechar o arquivo.

1. Atualize o projeto para incluir a versão mais recente dos Componentes principais do Forms:

   1. Abra o [Pasta de projeto do arquétipo AEM]/pom.xml para edição.
   1. Definir versão de `core.forms.components.version` e `core.forms.components.af.version` para o [Componentes principais mais recentes do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history) e garantir que ambas tenham a mesma versão que **Componentes principais do Forms** mencionado na tabela e defina a versão de `core.wcm.components.version` conforme indicado na [Componentes principais do WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html).

      >[!WARNING]
      >
      >* Ao criar um projeto do Arquétipo com a versão 45, a variável `[AEM Archetype Project Folder]/pom.xml` define inicialmente a versão dos componentes principais de formulários como 1.1.28. Antes de criar ou implantar o projeto Arquétipo, atualize a versão dos componentes principais de formulários para 1.1.26. Você pode encontrar a versão mais recente no [Histórico de versão do AEM 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history).

      >[!NOTE]
      >
      >* Se você configurar qualquer outra topologia, adicione o envio, o preenchimento prévio e outros URLs ao arquivo de inclui na lista de permissões na camada do Dispatcher.

   1. Salvar e fechar o arquivo.


1. Depois que o projeto do Arquétipo AEM for criado com êxito, crie o pacote de implantação para o seu ambiente. Para criar o pacote:

   1. Navegue até o diretório raiz do projeto do Arquétipo AEM.

   1. Execute o seguinte comando para criar o projeto do Arquétipo AEM para o seu ambiente:

      ```Shell
      mvn clean install
      ```

      ![arquétipo de construção-sucesso](/help/forms/using/assets/corecomponent-build-successful.png)


   Depois que o projeto do Arquétipo AEM é criado com êxito, um pacote AEM é gerado. Você pode encontrar o pacote em [Pasta de projeto do arquétipo AEM]\all\target\[appid].all-[version].zip

1. Use o [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) para implantar o [Pasta de projeto do arquétipo AEM]\all\target\[appid].all-[version]pacote .zip em todas as instâncias Autor e Publicar.

>[!NOTE]
>
>
>
> * Caso encontre dificuldades ao acessar a caixa de diálogo de logon em uma instância de publicação, para instalar o pacote por meio do Gerenciador de pacotes, tente usar o URL: `http://[Publish Server URL]:[PORT]/system/console` para fazer logon. Isso permite que você acesse a página de logon em uma instância do Publish, permitindo que continue com o processo de instalação.
> * Não exclua ou descarte o projeto do Arquétipo depois de implantá-lo em seu ambiente. O projeto Arquétipo é necessário para adicionar temas personalizados e novos Componentes principais adaptáveis do Forms ao seu ambiente.

Os Componentes principais são ativados para o seu ambiente. Um modelo de Formulário adaptável e um tema da Tela 3.0 em branco dos Componentes principais são implantados em seu ambiente, permitindo [criar Componentes principais com base no Forms adaptável](create-an-adaptive-form-core-components.md).

## Perguntas frequentes

### Quais são os componentes principais?

A variável [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) são um conjunto de componentes padronizados de Gerenciamento de Conteúdo na Web (WCM, na sigla em inglês) para o AEM a fim de acelerar o tempo de desenvolvimento e reduzir o custo de manutenção de seus sites.

### Quais são os recursos adicionados à habilitação dos componentes principais?


Quando os Componentes principais do Forms adaptável estiverem ativados para seu ambiente, um modelo de Formulário adaptável baseado em Componentes principais em branco e o tema do Canvas 3.0 serão adicionados ao seu ambiente. Depois de ativar os Componentes principais adaptáveis do Forms no seu ambiente, você pode:

* Crie Componentes principais com base no Forms adaptável.
* Crie Componentes principais com base em modelos de formulário adaptável.
* Crie temas personalizados para os Componentes principais com base em modelos de Formulário adaptável.
* Servir representações JSON do Formulário adaptável com base no Componente principal para canais como dispositivos móveis, Web, aplicativos nativos e serviços que exigem a representação headless de um formulário.

## O que vem a seguir

* [Criar um formulário adaptável baseado nos Componentes principais](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Criar ou adicionar um formulário adaptável a uma página do AEM Sites ou a um fragmento de experiência](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Criar temas para Forms adaptável com base em Componentes principais](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Criar um modelo para os Componentes principais com base no Forms adaptável](template-editor.md)
