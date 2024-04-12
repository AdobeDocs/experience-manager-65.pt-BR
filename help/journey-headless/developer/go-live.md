---
title: Como executar o aplicativo headless
description: Nesta parte da Jornada de desenvolvedores sem periféricos do AEM, saiba como implantar um aplicativo sem periféricos em tempo real.
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 51%

---

# Como executar o aplicativo headless {#go-live}

Nesta parte do [Jornada do desenvolvedor sem periféricos do AEM](overview.md), saiba como implantar um aplicativo headless ao vivo.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como atualizar seu conteúdo por meio das APIs do AEM Assets](update-your-content.md) você aprendeu a atualizar o conteúdo headless existente no AEM por meio da API e agora deve:

* Entender a API HTTP do AEM Assets.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto headless do AEM.

## Objetivo {#objective}

Este documento ajuda você a entender o pipeline de publicação headless do AEM e as considerações de desempenho que você deve conhecer antes de executar seu aplicativo.

* Saiba mais sobre o SDK do AEM e as ferramentas de desenvolvimento necessárias
* Configure um tempo de execução de desenvolvimento local para simular seu conteúdo antes de ele entrar em funcionamento
* Noções básicas sobre replicação e armazenamento em cache de conteúdo do AEM
* Proteger e dimensionar o aplicativo antes do lançamento
* Monitorar o desempenho e depurar problemas

## O SDK do AEM {#the-aem-sdk}

O SDK do AEM é usado para criar e implantar código personalizado. É a ferramenta principal que você deve desenvolver e testar seu aplicativo headless antes de entrar em funcionamento. Ele contém os seguintes artefatos:

* O Quickstart jar: um arquivo jar executável que pode ser usado para configurar um autor e uma instância de publicação
* Ferramentas do Dispatcher - o módulo Dispatcher e suas dependências para sistemas baseados no Windows e no UNIX
* Java™ API Jar: a dependência Java™ Jar/Maven que expõe todas as APIs Java™ permitidas que podem ser usadas para desenvolvimento no AEM
* Javadoc jar: o javadocs para o jar da API Java™

## Ferramentas de desenvolvimento adicionais {#additional-development-tools}

Além do SDK do AEM, você precisa de ferramentas adicionais que facilitam o desenvolvimento e o teste de seu código e conteúdo localmente:

* Java™
* Git
* Apache Maven
* A biblioteca Node.js
* O IDE de sua escolha

Como AEM é um aplicativo Java™, você deve instalar o Java™ e o SDK Java™ para oferecer suporte ao desenvolvimento do AEM as a Cloud Service.

O Git é o que você usa para gerenciar o controle de origem e verificar as alterações no Cloud Manager e, em seguida, implantá-las em uma instância de produção.

O AEM usa o Apache Maven para criar projetos gerados a partir do arquétipo de projeto Maven do AEM. Todos os principais IDEs fornecem suporte de integração para Maven.

Node.js é um ambiente de tempo de execução JavaScript usado para trabalhar com os ativos de front-end de um projeto AEM `ui.frontend` subprojeto. O Node.js é distribuído com o npm, que é o gerenciador de pacotes Node.js de fato, usado para gerenciar dependências do JavaScript.

## Principais características de componentes de um sistema do AEM {#components-of-an-aem-system-at-a-glance}

Em seguida, vamos analisar as partes constituintes de um ambiente do AEM.

Um ambiente do AEM completo é composto de um Autor, Publicação e Dispatcher. Esses mesmos componentes são disponibilizados no tempo de execução de desenvolvimento local para facilitar a pré-visualização do código e do conteúdo antes de entrar em funcionamento.

* **O serviço do Autor** é onde os usuários internos criam, gerenciam e visualizam conteúdo.

* **O serviço de Publicação** O é considerado o ambiente &quot;ativo&quot; e é, normalmente, com o que os usuários finais interagem. O conteúdo, após ser editado e aprovado no serviço do Autor, é distribuído (replicado) para o serviço de Publicação. O padrão de implantação mais comum com aplicativos headless do AEM é ter uma versão de produção do aplicativo conectada a um serviço de publicação do AEM.

* **O Dispatcher** é um servidor Web estático aumentado com o módulo AEM Dispatcher. Ele armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

## O fluxo de trabalho de desenvolvimento local {#the-local-development-workflow}

O projeto de desenvolvimento local é construído no Apache Maven e usa o Git para controle de origem. Para atualizar o projeto, a equipe de desenvolvimento pode usar seu ambiente integrado preferido, como Eclipse, Visual Studio Code, IntelliJ, entre outros.

Para testar atualizações de código ou conteúdo assimiladas pelo aplicativo headless, implante as atualizações no tempo de execução do AEM local. Isso inclui instâncias locais dos serviços de autoria e publicação do AEM.

Anote as distinções entre cada componente no tempo de execução do AEM local, pois é importante testar as atualizações onde elas são mais importantes. Por exemplo, teste as atualizações de conteúdo no autor ou teste o novo código na instância de publicação.

Em um sistema de produção, um Dispatcher e um servidor http Apache sempre estarão na frente de uma instância de publicação do AEM. Eles fornecem serviços de armazenamento em cache e de segurança para o sistema do AEM, portanto, é fundamental testar atualizações de código e conteúdo em relação ao Dispatcher também.

## Visualização do código e conteúdo localmente com o ambiente de desenvolvimento local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar seu projeto AEM headless para o lançamento, verifique se todas as partes constituintes do projeto estão funcionando bem.

Para fazer isso, você deve reunir tudo: código, conteúdo e configuração e testá-los em um ambiente de desenvolvimento local para preparação para ativação.

O ambiente de desenvolvimento local é composto por três áreas principais:

1. O Projeto AEM - contém todo o código personalizado, configuração e conteúdo em que os desenvolvedores do AEM vão trabalhar
1. O tempo de execução do AEM local: versões locais dos serviços de criação e publicação do AEM usados para implantar o código do projeto do AEM
1. O tempo de execução do Dispatcher local: uma versão local do servidor Web Apache httpd que inclui o módulo Dispatcher

Depois que o ambiente de desenvolvimento local for configurado, você poderá simular o fornecimento de conteúdo para o aplicativo React implantando um servidor de nó estático localmente.

Para obter uma visão mais detalhada da configuração de um ambiente de desenvolvimento local e todas as dependências necessárias para a pré-visualização de conteúdo, consulte [Documentação de implantação de produção](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html).

## Preparar seu aplicativo AEM Headless para ativação {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Agora, é hora de preparar seu aplicativo AEM headless para o lançamento, seguindo as práticas recomendadas descritas abaixo.

### Proteja seu aplicativo headless antes do lançamento {#secure-and-scale-before-launch}

1. Preparar [Autenticação](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) para suas solicitações do GraphQL

### Estrutura do modelo vs Saída da GraphQL {#structure-vs-output}

* Evite criar consultas que produzam mais de 15 KB de JSON (compactado com gzip). Arquivos JSON longos consomem muitos recursos para análise do aplicativo cliente.
* Evite mais de cinco níveis aninhados de hierarquias de fragmentos. Níveis adicionais tornam difícil para os autores de conteúdo considerar o impacto de suas alterações.
* Use consultas de vários objetos em vez de modelar consultas com hierarquias de dependência nos modelos. Isso permite uma flexibilidade de mais longo prazo para reestruturar a saída JSON sem precisar fazer muitas alterações de conteúdo.

### Maximizar a taxa de ocorrências do cache CDN {#maximize-cdn}

* Não use consultas diretas da GraphQL, a menos que esteja solicitando conteúdo ao vivo a partir da superfície.
   * Use consultas persistentes sempre que possível.
   * Forneça um TTL de CDN acima de 600 segundos para que o CDN possa armazená-los em cache.
   * O AEM pode calcular o impacto de uma alteração de modelo em consultas existentes.
* Divida arquivos JSON/consultas GraphQL entre taxa de alteração de conteúdo baixa e alta para reduzir o tráfego do cliente para CDN e atribuir um TTL mais alto. Isso minimiza a revalidação da CDN do JSON com o servidor de origem.
* Para invalidar ativamente o conteúdo da CDN, use a Limpeza suave. Isso permite que a CDN baixe novamente o conteúdo sem causar perda de cache.

>[!NOTE]
>
>Consulte [Recursos adicionais](#additional-resources) para obter mais informações sobre CDN e cache.

### Melhore o tempo de download de conteúdo headless {#improve-download-time}

* Verifique se os clientes HTTP usam HTTP/2.
* Verifique se os clientes HTTP aceitam a solicitação de cabeçalhos para gzip.
* Minimize o número de domínios usados para hospedar JSON e artefatos referenciados.
* Uso `Last-modified-since` para atualizar recursos.
* Use a saída `_reference` no arquivo JSON para iniciar o download de ativos sem precisar analisar os arquivos JSON completos.

<!-- End of CDN Review -->

## Implantar para produção {#deploy-to-production}

Implantar para produção pode depender se você tem um *tradicional* Instância de AEM que é implantada usando Maven ou que está no Adobe Managed Services (AMS) e, portanto, usando o Cloud Manager.

## Implantar para produção usando Maven {#deploy-to-production-maven}

Para um *tradicional* (não AMS) usando Maven, consulte a seção [Tutorial do WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html#build) para obter uma visão geral.

## Implantar para produção usando o Cloud Manager {#deploy-to-production-cloud-manager}

Se você for um cliente do AMS usando o Cloud Manager, depois de verificar se tudo foi testado e está funcionando corretamente, poderá enviar as atualizações de código para um [repositório Git centralizado no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html).

Depois que as atualizações forem carregadas no Cloud Manager, implante-as no AEM usando [Pipeline de CI/CD do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html).

<!-- Cannot find a parallel link -->
<!--
You can start deploying your code by using the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## Monitoramento de desempenho {#performance-monitoring}

Para que os usuários tenham a melhor experiência possível ao usar o aplicativo headless do AEM, é importante monitorar as principais métricas de desempenho, conforme detalhado abaixo:

* Validar versões de visualização e produção do aplicativo
* Verificar as páginas de status do AEM para obter o status atual de disponibilidade do serviço
* Acessar relatórios de desempenho
   * Desempenho da entrega
      * Servidores de origem: número de chamadas, taxas de erro, cargas da CPU, tráfego de conteúdo
   * Desempenho do autor
      * Verificar número de usuários, solicitações e carga
* Relatórios de desempenho específicos do Access App e Space
   * Quando o servidor estiver ativo, verifique se as métricas gerais estão verdes/laranjas/vermelhas, então identifique problemas específicos do aplicativo
   * Abra os mesmos relatórios acima filtrados para o aplicativo ou espaço (por exemplo, desktop Photoshop, paywall)
   * Use APIs de log do Splunk para acessar o desempenho do serviço e do aplicativo
   * Entre em contato com o Suporte ao cliente em caso de outros problemas.

## Resolução de problemas {#troubleshooting}

### Depuração {#debugging}

Siga essas práticas recomendadas como uma abordagem geral para depurar:

* Valide a funcionalidade e o desempenho com a versão de visualização do aplicativo
* Valide a funcionalidade e o desempenho com a versão de produção do aplicativo
* Valide com a visualização JSON do Editor de fragmento de conteúdo
* Para verificar a presença de problemas do aplicativo cliente ou do delivery, inspecione o JSON no aplicativo cliente
* Para verificar a presença de problemas relacionados ao conteúdo em cache ou ao AEM, inspecione o JSON usando o GraphQL

### Registro de um erro com o suporte {#logging-a-bug-with-support}

Para registrar um erro com o Suporte da, caso precise de mais ajuda, conclua as seguintes etapas:

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
* O que fazer depois que a ativação for concluída.

Ou você já lançou seu primeiro projeto AEM Headless ou agora tem todo o conhecimento para fazê-lo. Excelente trabalho!

### Explore os Aplicativos de página única {#explore-spa}

Não há necessidade de parar as lojas headless no AEM. No [Introdução como parte da jornada](getting-started.md#integration-levels)Em seguida, discutiu como o AEM não apenas suporta a entrega headless e os modelos tradicionais de pilha completa, mas também suporta modelos híbridos que combinam as vantagens de ambos.

Se esse tipo de flexibilidade for algo que você precisa para seu projeto, continue com a parte adicional opcional da jornada, [Como criar aplicativos de página única (SPA) com AEM.](create-spa.md)

## Recursos adicionais {#additional-resources}

* [Guia de desenvolvimento do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html)

* [Tutorial do WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR)

* [Cloud Manager para AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR)

* Cache da CDN

   * [Controle de um cache CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * Configuração do [Reescrita CDN](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*pesquisar Reescritor CDN*)

* [Introdução ao AEM as a Headless CMS](/help/sites-developing/headless/introduction.md)
* [Portal do desenvolvedor de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* [Tutorials para headless no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR)
