---
title: Ferramentas de desenvolvedor do AEM para Eclipse
seo-title: AEM Developer Tools for Eclipse
description: Ferramentas de desenvolvedor do AEM para Eclipse
seo-description: null
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 3%

---

# Ferramentas de desenvolvedor do AEM para Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Visão geral {#overview}

O AEM Developer Tools for Eclipse é um plug-in Eclipse com base no [Plug-in do Eclipse para o Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lançado sob a licença do Apache 2.

Ela oferece vários recursos que facilitam AEM desenvolvimento:

* Integração perfeita com instâncias AEM por meio do Eclipse Server Connector.
* Sincronização para pacotes de conteúdo e OSGI.
* Suporte à depuração com capacidade de troca automática de código.
* Inicialização simples de projetos de AEM por meio de um Assistente de criação de projeto específico.
* Edição fácil das propriedades do JCR.

## Requisitos {#requirements}

Antes de usar as Ferramentas do desenvolvedor do AEM, é necessário:

* Baixe e instale [Eclipse IDE para desenvolvedores Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). AEM Ferramentas de desenvolvedor atualmente oferecem suporte ao Eclipse Kepler ou mais recente

* Pode ser usado com AEM versão 5.6.1 ou mais recente
* Configure sua instalação do eclipse para garantir que você tenha pelo menos 1 gigabyte de memória heap editando seu `eclipse.ini` arquivo de configuração, conforme descrito na [Perguntas frequentes sobre o Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>No macOS, é necessário clicar com o botão direito do mouse em **Eclipse.app** e depois selecione **Mostrar conteúdo do pacote** para encontrar seu `eclipse.ini`**.**

## Como instalar as Ferramentas de Desenvolvedor do AEM para o Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Uma vez que tenha cumprido o [requisitos](#requirements) acima, você pode instalar o plug-in da seguinte maneira:

1. Navegue pelo [**AEM** Site das Ferramentas do Desenvolvedor](https://eclipse.adobe.com/aem/dev-tools/).

1. Copie o **Link de instalação**.

   Observe que, como alternativa, você pode baixar um arquivo em vez de usar o link de instalação. Isso permite a instalação offline, mas você perderá as notificações de atualização automáticas dessa maneira.

1. No Eclipse, abra o **Ajuda** menu.
1. Clique em **Instalar novo software**.
1. Clique em **Adicionar...**.
1. Em **Nome** digite AEM Ferramentas do desenvolvedor.
1. Em **Localização** copie o URL de instalação.
1. Clique em **Ok**.
1. Verifique ambos **AEM** e **Sling** plug-ins.
1. Clique em **Avançar**.
1. Clique em **Avançar**.
1. Aceite os contratos do lixão e clique em **Concluir**.
1. Clique em **Sim** para reiniciar o Eclipse.

## Como Importar Projetos Existentes {#how-to-import-existing-projects}

>[!NOTE]
>
>Consulte [Como trabalhar com um pacote no Eclipse quando ele foi baixado do AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## A perspectiva AEM {#the-aem-perspective}

As Ferramentas de Desenvolvimento de AEM para o Eclipse são fornecidas com uma Perspectiva que oferece controle total sobre seus projetos e instâncias de AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Exemplo de projeto de vários módulos {#sample-multi-module-project}

O AEM Developer Tools for Eclipse vem com uma amostra de projeto de vários módulos que ajuda você a se familiarizar rapidamente com a configuração do projeto no Eclipse, além de servir como um guia de práticas recomendadas para vários recursos AEM. [Saiba mais sobre o Arquétipo de projeto](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Siga estas etapas para criar o projeto de amostra:

1. No **Arquivo** > **Novo** > **Projeto** navegue até o menu **AEM** e selecione **AEM exemplo de projeto de vários módulos**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Clique em **Avançar**.

   >[!NOTE]
   >
   >Essa etapa pode demorar um pouco, pois m2eclipse precisa verificar os catálogos de arquétipo.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Choose **com.adobe.granite.archetypes : sample-project-archetype : (número mais alto)** no menu e, em seguida, clique em **Próximo**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Preencha um **Nome**, **ID do grupo** e um **ID do artefato** para o projeto de amostra. Também é possível optar por definir algumas propriedades avançadas.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Em seguida, você deve configurar um servidor AEM ao qual o Eclipse se conectará.

   Para usar o recurso do depurador, é necessário ter iniciado o AEM no modo de depuração - o que pode ser feito, por exemplo, adicionando o seguinte à linha de comando:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Clique em **Concluir**. A estrutura do projeto é criada.

   >[!NOTE]
   >
   >Numa nova instalação (mais especificamente: quando as dependências maven nunca tiverem sido baixadas), você poderá criar o projeto com erros. Neste caso, siga o procedimento descrito em [Resolvendo Definição de Projeto Inválida](#resolving-invalid-project-definition).

## Resolução de problemas {#troubleshooting}

### Resolvendo Definição de Projeto Inválida {#resolving-invalid-project-definition}

Para resolver dependências inválidas e definição de projeto, proceda da seguinte maneira:

1. Selecione todos os projetos criados.
1. Clique com o botão direito do mouse. No menu **Maven** select **Atualizar projetos**.
1. Verificar **Forçar atualizações de instantâneos/versões**.
1. Clique em **OK**. O Eclipse tenta baixar as dependências necessárias.

### Ativação do autopreenchimento da biblioteca de tags em arquivos JSP {#enabling-tag-library-autocompletion-in-jsp-files}

O autopreenchimento da biblioteca de tags funciona imediatamente, visto que as dependências adequadas são adicionadas ao projeto. Há um problema conhecido ao usar o AEM Uber Jar, que não inclui os arquivos tld e TagExtraInfo necessários.

Para contornar isso, verifique se o artefato org.apache.sling.scripting.jsp.taglib está localizado no classpath antes do AEM Uber Jar. Para projetos Maven, coloque a seguinte dependência no pom.xml antes do Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Certifique-se de adicionar a versão adequada para a implantação do AEM.

## Mais informações {#more-information}

O site oficial Apache Sling IDE tooling for Eclipse fornece informações úteis:

* O [**Ferramentas do Apache Sling IDE para Eclipse** Guia do usuário](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentação guiará você pelos conceitos gerais, pela integração do servidor e pelos recursos de implantação suportados pelas Ferramentas de desenvolvimento de AEM.
* O [Seção Solução de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* O [Lista de problemas conhecidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

O seguinte funcionário [Eclipse](https://eclipse.org/) a documentação pode ajudar a configurar seu ambiente:

* [Introdução ao Eclipse](https://eclipse.org/users/)
* [Sistema de ajuda do Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integração Maven (m2eclipse)](https://www.eclipse.org/m2e/)
