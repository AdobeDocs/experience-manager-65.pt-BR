---
title: Ferramentas de desenvolvedor do AEM para Eclipse
description: Ferramentas de desenvolvedor do AEM para Eclipse
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 8336a7257d3c5e75cd37381b0124c227c2d55dca
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 4%

---

# Ferramentas de desenvolvedor do AEM para Eclipse{#aem-developer-tools-for-eclipse}

![Motivo de imagem circular para ferramentas de desenvolvedor de AEM para Eclipse.](do-not-localize/chlimage_1-9.png)

## Visão geral {#overview}

&quot;Ferramentas para desenvolvedores AEM&quot; é um plug-in do Eclipse baseado no [Plug-in Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lançado com a Licença Apache 2.

Ele oferece vários recursos que facilitam o desenvolvimento do AEM:

* Integração perfeita com instâncias de AEM por meio do Eclipse Server Connector.
* Sincronização para conteúdo e pacotes OSGI.
* Suporte à depuração com recurso de troca automática de código.
* Bootstrap simples de projetos AEM por meio de um Assistente de criação de projeto específico.
* Fácil edição das propriedades do JCR.

## Requisitos {#requirements}

Antes de usar as ferramentas de desenvolvedor do AEM, faça o seguinte:

* Baixar e instalar [Desenvolvedores do Eclipse IDE para Java™ EE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). Atualmente, as ferramentas de desenvolvedor do AEM são compatíveis com o Eclipse Kepler ou mais recente

* Pode ser usado com o AEM versão 5.6.1 ou mais recente
* Configure a instalação do eclipse para garantir que você tenha pelo menos 1 GB de memória heap ao editar o `eclipse.ini` arquivo de configuração conforme descrito na seção [Perguntas frequentes sobre o Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>No macOS, clique com o botão direito do mouse em **Eclipse.app** e selecione **Mostrar conteúdo do pacote** para encontrar o seu `eclipse.ini`.

## Como instalar as ferramentas de desenvolvedor do AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Depois de ter cumprido as [requisitos](#requirements) acima, você pode instalar o plug-in da seguinte maneira:

1. Navegue pelo **Ferramentas para desenvolvedores do AEM** site em `https://eclipse.adobe.com/aem/dev-tools/`.

1. Copie o **Link de instalação**.

   Como alternativa, você pode baixar um arquivo em vez de usar o link de instalação. Isso permite a instalação offline, mas você perde as notificações de atualização automática.

1. No Eclipse, abra o **Ajuda** menu.
1. Clique em **Instalar novo software**.
1. Clique em **Adicionar...**.
1. Entrada **Nome** digite Ferramentas para desenvolvedores do AEM.
1. Entrada **Localização** copie o URL de instalação.
1. Clique em **Ok**.
1. Marque ambos **AEM** e **Sling** plugins.
1. Clique em **Avançar**.
1. Clique em **Avançar**.
1. Aceite os contratos lincese e clique em **Concluir**.
1. Clique em **Sim** para reiniciar o Eclipse.

## Como Importar Projetos Existentes {#how-to-import-existing-projects}

>[!NOTE]
>
>Consulte [Como trabalhar com um pacote no Eclipse quando ele foi baixado do AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## A perspectiva do AEM {#the-aem-perspective}

As ferramentas de desenvolvimento do AEM para o Eclipse são fornecidas com uma Perspectiva que oferece controle total sobre seus projetos e instâncias do AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Exemplo de projeto de vários módulos {#sample-multi-module-project}

As &quot;Ferramentas de desenvolvedor de AEM&quot; incluem um projeto de amostra e de vários módulos que ajuda você a se familiarizar rapidamente com uma configuração de projeto no Eclipse. Ele também serve como um guia de práticas recomendadas para vários recursos do AEM. [Saiba mais sobre o Arquétipo de projeto](https://github.com/adobe/aem-project-archetype).

Para criar o projeto de amostra, conclua as seguintes etapas:

1. No **Arquivo** > **Novo** > **Projeto** , navegue até o menu **AEM** e selecione **Projeto de vários módulos de amostra AEM**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Clique em **Avançar**.

   >[!NOTE]
   >
   >Esta etapa pode demorar porque o m2eclipse deve verificar os catálogos de arquétipo.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Escolher **com.adobe.granite.archetypes : arquétipo de projeto de amostra : (número mais alto)** no menu e clique em **Próxima**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Preencher um **Nome**, **ID do grupo**, e uma **ID do artefato** para o projeto de amostra. Você também pode optar por definir algumas propriedades avançadas.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Agora, configure um servidor AEM ao qual o Eclipse possa se conectar.

   Para usar o recurso de depuração, verifique se você iniciou o AEM no modo de depuração, que pode ser obtido adicionando o seguinte à linha de comando:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Clique em **Concluir**. A estrutura do projeto é criada.

   >[!NOTE]
   >
   >Em uma nova instalação (mais especificamente: quando as dependências do Maven nunca foram baixadas), você pode criar o projeto com erros. Nesse caso, siga o procedimento descrito em [Resolvendo Definição de Projeto Inválida](#resolving-invalid-project-definition).

## Resolução de problemas {#troubleshooting}

### Resolvendo Definição de Projeto Inválida {#resolving-invalid-project-definition}

Para resolver dependências inválidas e a definição do projeto, proceda da seguinte maneira:

1. Selecione todos os projetos criados.
1. Clique com o botão direito do mouse em. No menu **Maven**, selecione **Atualizar Projetos**.
1. Marcar **Forçar Atualizações de Instantâneo/Liberações**.
1. Clique em **OK**. O Eclipse tenta fazer download das dependências necessárias.

### Ativação do autopreenchimento da biblioteca de tags em arquivos JSP {#enabling-tag-library-autocompletion-in-jsp-files}

O autopreenchimento da biblioteca de tags funciona imediatamente, já que as dependências apropriadas são adicionadas ao projeto. Há um problema conhecido ao usar o AEM Uber Jar, que não inclui os arquivos tld e TagExtraInfo necessários.

Para contornar isso, verifique se o artefato org.apache.sling.scripting.jsp.taglib está no classpath antes do AEM Uber Jar. Para projetos Maven, coloque a seguinte dependência no pom.xml antes do Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Certifique-se de adicionar a versão adequada para a sua distribuição de AEM.

## Mais informações {#more-information}

A ferramenta oficial do Apache Sling IDE para o site do Eclipse fornece informações úteis:

* A variável [**Ferramentas Apache Sling IDE para Eclipse** Guia do usuário](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentação o orienta pelos conceitos gerais, pela integração de servidores e pelos recursos de implantação compatíveis com as Ferramentas de desenvolvimento do AEM.
* A variável [Seção Solução de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* A variável [Lista de problemas conhecidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

O seguinte funcionário [Eclipse](https://www.eclipse.org/) A documentação do pode ajudar a configurar seu ambiente:

* [Introdução ao Eclipse](https://eclipseide.org/getting-started/)
* [Sistema de ajuda Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integração do Maven (m2eclipse)](https://www.eclipse.org/m2e/)
