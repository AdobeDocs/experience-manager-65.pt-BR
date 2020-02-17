---
title: Ferramentas de desenvolvedor do AEM para Eclipse
seo-title: Ferramentas de desenvolvedor do AEM para Eclipse
description: 'null'
seo-description: 'null'
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# Ferramentas de desenvolvedor do AEM para Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Visão geral {#overview}

As ferramentas de desenvolvedor do AEM para Eclipse são um plug-in do Eclipse baseado no plug-in do [Eclipse para o Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lançado sob a licença do Apache 2.

Ele oferece vários recursos que facilitam o desenvolvimento do AEM:

* Integração perfeita com instâncias do AEM por meio do Eclipse Server Connector.
* Sincronização de pacotes de conteúdo e OSGI.
* Suporte de depuração com capacidade de troca automática de código.
* Inicialização simples de projetos AEM por meio de um Assistente de criação de projeto específico.
* Edição fácil das propriedades do JCR.

## Requisitos {#requirements}

Antes de usar as ferramentas do desenvolvedor do AEM, é necessário:

* Baixe e instale o [Eclipse IDE para desenvolvedores](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)Java EE. Atualmente, as ferramentas de desenvolvedor do AEM são compatíveis com o Eclipse Kepler ou mais recente

* Pode ser usado com o AEM versão 5.6.1 ou mais recente
* Configure a instalação do eclipse para garantir que você tenha pelo menos 1 gigabyte de memória heap editando o arquivo de `eclipse.ini` configuração conforme descrito nas Perguntas frequentes do [Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>No macOS, você precisa clicar com o botão direito do mouse em **Eclipse.app** e selecionar **Mostrar conteúdo** do pacote para encontrar seu `eclipse.ini`**.**

## Como instalar as ferramentas do desenvolvedor do AEM para o Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Depois de cumprir os [requisitos](#requirements) acima, você pode instalar o plug-in da seguinte maneira:

1. Navegue no site [**Ferramentas do desenvolvedor do **AEM](https://eclipse.adobe.com/aem/dev-tools/).

1. Copie o link **de instalação**.

   Observe que, como alternativa, você pode baixar um arquivo em vez de usar o link de instalação. Isso permite a instalação offline, mas você perderá notificações automáticas de atualização dessa forma.

1. No Eclipse, abra o menu **Ajuda** .
1. Clique em **Instalar novo software**.
1. Clique em **Adicionar...**.
1. Em **Nome** , digite Ferramentas do desenvolvedor do AEM.
1. Em **Local** , copie o URL de instalação.
1. Click **Ok**.
1. Verifique os plug-ins **AEM** e **Sling** .
1. Clique em **Avançar**.
1. Clique em **Avançar**.
1. Aceite os contratos de lixeira e clique em **Concluir**.
1. Clique em **Sim** para reiniciar o Eclipse.

## Como importar projetos existentes {#how-to-import-existing-projects}

>[!NOTE]
>
>Consulte [Como trabalhar com um pacote no Eclipse quando ele foi baixado do AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## A perspectiva do AEM {#the-aem-perspective}

As Ferramentas de desenvolvimento do AEM para Eclipse são enviadas com uma Perspectiva que oferece controle total sobre seus projetos e instâncias do AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Exemplo de projeto de vários módulos {#sample-multi-module-project}

As Ferramentas de desenvolvedor do AEM para Eclipse vêm com uma amostra de projeto de vários módulos que ajuda você a se familiarizar rapidamente com a configuração de um projeto no Eclipse, além de servir como um guia de práticas recomendadas para vários recursos do AEM. [Saiba mais sobre o Tipo de Arquivo](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)do Projeto.

Siga estas etapas para criar o projeto de amostra:

1. No menu **Arquivo** > **Novo** > **Projeto** , navegue até a seção **AEM** e selecione **AEM Sample Multi-Module Project**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Clique em **Avançar**.

   >[!NOTE]
   >
   >Essa etapa pode levar algum tempo, pois m2eclipse precisa verificar os catálogos de arquétipos.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Escolha **com.adobe.granite.archetypes : sample-project-archetype : (número mais alto)** no menu e clique em **Avançar**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Preencha um **Nome**, uma ID **de** grupo e uma ID **de** artefato para o projeto de amostra. Você também pode optar por definir algumas propriedades avançadas.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Em seguida, configure um servidor AEM ao qual o Eclipse se conectará.

   Para usar o recurso do depurador, é necessário ter iniciado o AEM no modo de depuração - o que pode ser obtido, por exemplo, adicionando o seguinte à linha de comando:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Click **Finish**. A estrutura do projeto é criada.

   >[!NOTE]
   >
   >Numa instalação nova (mais especificamente: quando as dependências maven nunca foram baixadas), você pode criar o projeto com erros. Nesse caso, siga o procedimento descrito em [Resolução de definição](#resolving-invalid-project-definition)de projeto inválida.

## Resolução de Problemas{#troubleshooting}

### Resolvendo Definição de Projeto Inválida {#resolving-invalid-project-definition}

Para resolver dependências inválidas e definição de projeto, siga estas instruções:

1. Selecione todos os projetos criados.
1. Clique com o botão direito do mouse. No menu **Maven** , selecione **Atualizar projetos**.
1. Verifique **Forçar Atualizações de Instantâneos/Versões**.
1. Clique em **OK**. O Eclipse tenta baixar as dependências necessárias.

### Habilitar a autocompletar da biblioteca de tags em arquivos JSP {#enabling-tag-library-autocompletion-in-jsp-files}

A autoconclusão da biblioteca de tags funciona fora da caixa, visto que as dependências adequadas são adicionadas ao projeto. Há um problema conhecido ao usar o AEM Uber Jar, que não inclui os arquivos tld e TagExtraInfo necessários.

Para contornar isso, verifique se o artefato org.apache.sling.scripting.jsp.taglib está localizado no classpath antes do AEM Uber Jar. Para projetos Maven, coloque a seguinte dependência no pom.xml antes do Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Certifique-se de adicionar a versão correta para sua implantação do AEM.

## More information {#more-information}

A ferramenta oficial Apache Sling IDE para o site Eclipse fornece informações úteis:

* A ferramenta [**Apache Sling IDE para o Guia **do Usuário do Eclipse](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentação o guiará pelos conceitos gerais, integração de servidor e recursos de implantação suportados pelas Ferramentas de Desenvolvimento do AEM.
* A seção [Solução de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* A lista [Problemas](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)conhecidos.

A seguinte documentação oficial do [Eclipse](https://eclipse.org/) pode ajudar a configurar seu ambiente:

* [Introdução ao Eclipse](https://eclipse.org/users/)
* [Sistema de ajuda do Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integração Maven (m2eclipse)](https://www.eclipse.org/m2e/)

