---
title: Como executar o aplicativo headless
description: Nesta parte da Jornada de desenvolvedores headless do AEM, saiba como implantar um aplicativo headless ao vivo.
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 54%

---

# Como executar o aplicativo headless {#go-live}

Nesta parte do [jornada do desenvolvedor sem periféricos do AEM](overview.md), saiba como implantar um aplicativo sem periféricos ao vivo.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como atualizar seu conteúdo por meio das APIs do AEM Assets](update-your-content.md) você aprendeu a atualizar o conteúdo headless existente no AEM por meio da API e agora deve:

* Entender a API HTTP do AEM Assets.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto headless do AEM.

## Objetivo {#objective}

Este documento ajuda você a entender o pipeline de publicação sem periféricos AEM e as considerações de desempenho que você precisa ter em mente antes de entrar em contato com seu aplicativo.

* Saiba mais sobre o SDK do AEM e a ferramenta de desenvolvimento necessária
* Configure um tempo de execução de desenvolvimento local para simular seu conteúdo antes de entrar no ar
* Noções básicas sobre replicação e cache de conteúdo AEM
* Proteger e dimensionar o aplicativo antes do lançamento
* Monitorar o desempenho e depurar problemas

## O SDK do AEM {#the-aem-sdk}

O SDK do AEM é usado para criar e implantar código personalizado. É a principal ferramenta necessária para desenvolver e testar seu aplicativo sem periféricos antes de entrar online. Ele contém os seguintes artefatos:

* O Quickstart jar: um arquivo jar executável que pode ser usado para configurar um autor e uma instância de publicação
* Ferramentas do Dispatcher - o módulo Dispatcher e suas dependências para sistemas baseados em Windows e UNIX
* Java API Jar - A dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolvimento em relação a AEM
* Javadoc jar - o javadocs para o jar da API Java

## Ferramentas de desenvolvimento adicionais {#additional-development-tools}

Além do SDK AEM, você precisará de ferramentas adicionais que facilitem o desenvolvimento e o teste do código e conteúdo localmente:

* Java
* Git
* Apache Maven
* A biblioteca Node.js
* O IDE de sua escolha

Como AEM é um aplicativo Java, é necessário instalar o Java e o SDK do Java para dar suporte ao desenvolvimento AEM as a Cloud Service.

O Git é o que você usará para gerenciar o controle do código-fonte, bem como para verificar as alterações no Cloud Manager e, em seguida, implantá-las em uma instância de produção.

AEM usa o Apache Maven para criar projetos gerados a partir do arquétipo de projeto AEM Maven. Todos os principais IDEs fornecem suporte de integração para Maven.

Node.js é um ambiente de tempo de execução JavaScript usado para trabalhar com os ativos de front-end de um subprojeto de `ui.frontend` do projeto do AEM. O Node.js é distribuído com o npm, que é o gerenciador de pacotes Node.js de fato, usado para gerenciar dependências do JavaScript.

## Principais características de componentes de um sistema do AEM {#components-of-an-aem-system-at-a-glance}

Em seguida, vamos dar uma olhada nas partes constituintes de um ambiente AEM.

Um ambiente do AEM completo é composto de um Autor, Publicação e Dispatcher. Esses mesmos componentes serão disponibilizados no tempo de execução de desenvolvimento local para facilitar a visualização do código e conteúdo antes de entrar no ar.

* **O serviço do Autor** é onde os usuários internos criam, gerenciam e visualizam conteúdo.

* **O serviço de Publicação** é considerado o ambiente “ativo” e é, normalmente, com o que os usuários finais interagem. O conteúdo, após ser editado e aprovado no serviço Autor, é distribuído (replicado) ao serviço de Publicação. O padrão de implantação mais comum com aplicativos headless do AEM é ter uma versão de produção do aplicativo conectada a um serviço de publicação do AEM.

* **O Dispatcher** é um servidor Web estático aumentado com o módulo dispatcher do AEM. Ele armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

## O fluxo de trabalho de desenvolvimento local {#the-local-development-workflow}

O projeto de desenvolvimento local é construído no Apache Maven e usa o Git para controle de origem. Para atualizar o projeto, os desenvolvedores podem usar seu ambiente de desenvolvimento integrado preferido, como Eclipse, Visual Studio Code ou IntelliJ, entre outros.

Para testar atualizações de código ou conteúdo que serão assimiladas pelo aplicativo sem periféricos, é necessário implantar as atualizações no tempo de execução do AEM local, que inclui instâncias locais dos serviços de criação e publicação do AEM.

Anote as distinções entre cada componente no tempo de execução do AEM local, pois é importante testar as atualizações onde elas são mais importantes. Por exemplo, teste as atualizações de conteúdo no autor ou teste o novo código na instância de publicação.

Em um sistema de produção, um dispatcher e um servidor http Apache sempre se sentarão na frente de uma instância de publicação de AEM. Eles fornecem serviços de armazenamento em cache e de segurança para o sistema de AEM, portanto, é fundamental testar atualizações de código e conteúdo no dispatcher também.

## Visualização do código e conteúdo localmente com o ambiente de desenvolvimento local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar o seu projeto sem periféricos AEM para lançamento, você precisa garantir que todas as partes constituintes do seu projeto estejam funcionando bem.

Para fazer isso, você precisa juntar tudo: código, conteúdo e configuração e teste-os em um ambiente de desenvolvimento local para estar em prontidão.

O ambiente de desenvolvimento local compreende três áreas principais:

1. O AEM Project - isso conterá todos os códigos personalizados, configurações e conteúdo em que os desenvolvedores AEM trabalharão
1. O Local AEM Runtime - versões locais dos serviços de criação e publicação do AEM que serão usados para implantar o código do AEM projeto
1. O tempo de execução do Dispatcher local: uma versão local do servidor Web Apache httpd que inclui o módulo Dispatcher

Depois que o ambiente do desenvolvimento local estiver configurado, você pode simular a exibição de conteúdo para o aplicativo React implantando um servidor Node estático localmente.

Para obter uma análise mais detalhada da configuração de um ambiente de desenvolvimento local e todas as dependências necessárias para a visualização de conteúdo, consulte [Documentação de implantação de produção](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## Prepare seu aplicativo AEM headless para ativação {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Agora, é hora de preparar seu aplicativo sem periféricos AEM para o lançamento, seguindo as práticas recomendadas descritas abaixo.

### Proteja seu aplicativo sem cabeçalho antes do lançamento {#secure-and-scale-before-launch}

1. Preparar [Autenticação](/help/assets/content-fragments/graphql-authentication-content-fragments.md) para suas solicitações do GraphQL

### Estrutura do modelo vs Saída da GraphQL {#structure-vs-output}

* Evite criar consultas que produzem mais de 15 kb de JSON (gzip compactado). Arquivos JSON longos consomem muitos recursos para análise do aplicativo cliente.
* Evite mais de cinco níveis aninhados de hierarquias de fragmentos. Níveis adicionais tornam difícil para os autores de conteúdo considerar o impacto de suas alterações.
* Use consultas de vários objetos em vez de modelar consultas com hierarquias de dependência nos modelos. Isso permite maior flexibilidade a longo prazo para reestruturar a saída JSON sem precisar fazer muitas alterações de conteúdo.

### Maximizar a taxa de ocorrências do cache CDN {#maximize-cdn}

* Não use consultas diretas da GraphQL, a menos que esteja solicitando conteúdo ao vivo a partir da superfície.
   * Use consultas persistentes sempre que possível.
   * Forneça TTL CDN acima de 600 segundos para que a CDN armazene em cache.
   * O AEM pode calcular o impacto de uma alteração de modelo em consultas existentes.
* Divida arquivos JSON/consultas GraphQL entre taxas de alteração de conteúdo baixas e altas para reduzir o tráfego de clientes para CDN e atribuir TTL maior. Isso minimiza a revalidação do CDN no JSON com o servidor de origem.
* Para invalidar ativamente o conteúdo da CDN, use a limpeza suave. Isso permite que a CDN baixe novamente o conteúdo sem causar a perda de um cache.

>[!NOTE]
>
>Consulte [Recursos adicionais](#additional-resources) para obter mais informações sobre CDN e armazenamento em cache.

### Melhore o tempo de download de conteúdo headless {#improve-download-time}

* Verifique se os clientes HTTP usam HTTP/2.
* Verifique se os clientes HTTP aceitam a solicitação de cabeçalhos para gzip.
* Minimize o número de domínios usados para hospedar JSON e artefatos referenciados.
* Aproveite o `Last-modified-since` para atualizar recursos.
* Use a saída `_reference` no arquivo JSON para iniciar o download de ativos sem precisar analisar os arquivos JSON completos.

<!-- End of CDN Review -->

## Implantar para produção {#deploy-to-production}

A implantação na produção pode depender do fato de você ter uma *tradicional* AEM instância que é implantada usando o Maven ou que está no Adobe Managed Services (AMS) e, portanto, usa o Cloud Manager.

## Implantar na produção usando o Maven {#deploy-to-production-maven}

Para um *tradicional* implantação (não AMS) usando o Maven, você pode ver a variável [Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) para obter uma visão geral.

## Implantar na produção usando o Cloud Manager {#deploy-to-production-cloud-manager}

Se você for um cliente do AMS usando o Cloud Manager, depois de verificar se tudo foi testado e está funcionando corretamente, estará pronto para enviar as atualizações de código para um [repositório Git centralizado no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=pt-BR).

Depois que as atualizações forem carregadas no Cloud Manager, elas poderão ser implantadas no AEM usando o [pipeline de CI/CD do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## Monitoramento de desempenho {#performance-monitoring}

Para que os usuários tenham a melhor experiência possível ao usar o aplicativo sem periféricos AEM, é importante monitorar as principais métricas de desempenho, conforme detalhado abaixo:

* Validar versões de visualização e produção do aplicativo
* Verificar as páginas de status do AEM para obter o status atual de disponibilidade do serviço
* Acessar relatórios de desempenho
   * Desempenho da entrega
      * Servidores de origem: número de chamadas, taxas de erro, cargas da CPU, tráfego de conteúdo
   * Desempenho do autor
      * Verificar o número de usuários, solicitações e carga
* Acessar relatórios de desempenho específicos do aplicativo e do espaço
   * Quando o servidor estiver ativo, verifique se as métricas gerais estão verdes/laranjas/vermelhas, então identifique problemas específicos do aplicativo
   * Abra os mesmos relatórios acima filtrados para o aplicativo ou espaço (por exemplo, desktop do Photoshop, paywall)
   * Use APIs de log do Splunk para acessar o desempenho do serviço e do aplicativo
   * Entre em contato com o Suporte ao cliente em caso de outros problemas.

## Resolução de problemas {#troubleshooting}

### Depuração {#debugging}

Siga essas práticas recomendadas como uma abordagem geral para depurar:

* Valide a funcionalidade e o desempenho com a versão de visualização do aplicativo
* Valide a funcionalidade e o desempenho com a versão de produção do aplicativo
* Valide com a visualização JSON do Editor de fragmento de conteúdo
* Inspecione o JSON no aplicativo cliente para verificar a presença de problemas nele ou na entrega
* Inspecione o JSON usando o GraphQL para verificar a presença de problemas relacionados ao conteúdo em cache ou ao AEM 

### Registro de um erro com o suporte {#logging-a-bug-with-support}

Para registrar um erro com o Suporte mais eficientemente, siga as etapas abaixo:

* Tire capturas de tela do problema, se necessário
* Documente uma maneira de reproduzir o problema
* Documente o conteúdo com o qual o é possível reproduz o problema
* Registre o problema por meio do portal de suporte do AEM com a prioridade apropriada

## A jornada termina - Será? {#journey-ends}

Parabéns! Você concluiu a Jornada do desenvolvedor headless do AEM! Agora você deve ter uma compreensão básica sobre:

* A diferença entre a entrega de conteúdo headless e headful.
* Recursos headless do AEM.
* Como organizar um projeto do AEM Headless.
* Como criar conteúdo headless no AEM.
* Como recuperar e atualizar conteúdo headless no AEM.
* Como ativar um projeto do AEM Headless.
* O que fazer depois do lançamento?

Ou você já lançou seu primeiro projeto Headless do AEM ou agora tem todo o conhecimento necessário para tal. Excelente trabalho!

### Explore os Aplicativos de página única {#explore-spa}

Armazenamento headless no AEM não precisa parar aqui. Você deve se lembrar do [Parte Introdução da jornada](getting-started.md#integration-levels) discutimos brevemente como o AEM não só suporta o delivery sem interface e os modelos de pilha completa tradicionais, como também pode suportar modelos híbridos que combinam as vantagens de ambos.

Se esse tipo de flexibilidade é algo que você precisa para o seu projeto, continue para a parte adicional opcional da jornada, [Como criar Aplicativos de página única (SPAs) com o AEM.](create-spa.md)

## Recursos adicionais {#additional-resources}

* [Guia de desenvolvimento de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [Cloud Manager para AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=en)

* Cache CDN

   * [Controlando um Cache CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * Configurar a [Gravador CDN](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*pesquisar por regravador CDN*)
