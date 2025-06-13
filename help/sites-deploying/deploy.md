---
title: Implantação e manutenção
description: Saiba como começar a instalação do AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 3%

---

# Implantação e manutenção{#deploying-and-maintaining}

Nesta página, você encontrará:

* [Conceitos básicos](#basic-concepts)

   * [O que é o AEM?](#what-is-aem)
   * [Implantações típicas](#typical-deployment-scenarios)

      * [No local](#on-premise)
      * [Managed Services usando o Cloud Manager](#managed-services-using-cloud-manager)

* [Introdução](#getting-started)

   * [Pré-requisitos](#prerequisites)
   * [Obtendo o software](#getting-the-software)
   * [Instalação local padrão](#default-local-install)
   * [Instalações do Author e Publish](#author-and-publish-installs)
   * [Diretório de Instalação Desempacotado](#unpacked-install-directory)
   * [Iniciando e Interrompendo](#starting-and-stopping)

Depois de se familiarizar com essas noções básicas, você pode encontrar informações mais avançadas e detalhadas nas seguintes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalação Personalizada Independente](/help/sites-deploying/custom-standalone-install.md)
* [Instalação do Servidor de Aplicativos](/help/sites-deploying/application-server-install.md)
* [Resolução de problemas](/help/sites-deploying/troubleshooting.md)
* [Início e Interrupção da Linha de Comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuração](/help/sites-deploying/configuring.md)
* [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artigos de instruções sobre configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Práticas recomendadas](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [O que é o AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=pt-BR)

## Conceitos básicos {#basic-concepts}

### O que é o AEM? {#what-is-aem}

O Adobe Experience Manager é um sistema cliente-servidor baseado na Web para criar, gerenciar e implantar sites comerciais e serviços relacionados. Ele combina várias funções de nível de infraestrutura e nível de aplicativo em um único pacote integrado.

No nível da infraestrutura, a AEM oferece o seguinte:

* **Servidor de Aplicativos Web**: o AEM pode ser implantado no modo autônomo (inclui um servidor Web Jetty integrado) ou como um aplicativo Web em um servidor de aplicativos de terceiros.
* **Estrutura de Aplicativo Web**: o AEM incorpora a estrutura de Aplicativo Web Sling que simplifica a gravação de aplicativos Web RESTful orientados a conteúdo.
* **Repositório de Conteúdo**: o AEM inclui um Java™ Content Repository (JCR), um tipo de banco de dados hierárquico projetado especificamente para dados não estruturados e semiestruturados. O repositório armazena não apenas o conteúdo voltado para o usuário, mas também todos os códigos, modelos e dados internos usados pelo aplicativo.

Com base nessa base, a AEM também oferece vários recursos no nível de aplicativos para o gerenciamento de:

* **Sites**
* **Aplicativos móveis**
* **Publicações digitais**
* **Forms e documentos**
* **Assets digital**
* **Comunidades**
* **Commerce Online**

Por fim, os clientes podem usar esses componentes básicos de infraestrutura e nível de aplicativo para criar soluções personalizadas, criando aplicativos próprios.

O servidor AEM é **baseado em Java** e é executado na maioria dos sistemas operacionais que oferecem suporte a essa plataforma. Toda interação do cliente com o AEM é feita através de um **navegador da Web**.

>[!NOTE]
>
>O recurso Adaptive Forms, disponível no AEM 6.5 QuickStart, foi projetado apenas para fins de exploração e avaliação. Para usá-lo na produção, é essencial obter uma licença válida para o AEM Forms, pois a funcionalidade de formulários adaptáveis requer uma licença adequada.

### Cenários de implantação típicos {#typical-deployment-scenarios}

Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor. As instalações do AEM geralmente envolvem pelo menos duas instâncias, normalmente executadas em computadores separados:

* **Autor**: uma instância do AEM usada para criar, carregar, editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
* **Publicar**: uma instância do AEM que serve o conteúdo publicado para o público.

Essas instâncias são idênticas em termos de software instalado. Eles são diferenciados somente pela configuração. Além disso, a maioria das instalações usa um Dispatcher:

* **Dispatcher**: um servidor Web estático (Apache httpd, Microsoft® IIS e assim por diante) aumentado com o módulo AEM Dispatcher. Ele armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

Há muitas opções e elaborações avançadas dessa configuração, mas o padrão básico do autor, publicação e Dispatcher está no centro da maioria das implantações. Vamos começar focando em uma configuração simples. As discussões sobre opções avançadas de implantação serão realizadas a seguir.

As seções a seguir descrevem ambos os cenários:

* **No local**: o AEM foi implantado e gerenciado em seu ambiente corporativo.

* **Managed Services - Cloud Manager para Adobe Experience Manager**: AEM implantado e gerenciado pelo Adobe Managed Services.

### No local {#on-premise}

Você pode instalar o AEM em servidores em seu ambiente corporativo. As instâncias de instalação típicas incluem: Ambientes de desenvolvimento, teste e publicação. Consulte [Introdução](/help/sites-deploying/deploy.md#getting%20started) para obter detalhes básicos sobre como obter o software AEM para instalá-lo localmente.

Para saber mais sobre as implantações locais típicas, consulte [Implantações Recomendadas](/help/sites-deploying/recommended-deploys.md).

### Managed Services usando o Cloud Manager {#managed-services-using-cloud-manager}

O AEM Managed Services é uma solução completa para o gerenciamento da experiência digital. Ele oferece os benefícios da solução de entrega de experiência na nuvem, além de manter todos os benefícios de controle, segurança e personalização de uma implantação local. O AEM Managed Services permite que os clientes iniciem mais rapidamente, implantando na nuvem e também aproveitando as práticas recomendadas e o suporte da Adobe. As organizações e os usuários empresariais podem envolver os clientes em pouco tempo, impulsionar participação no mercado e se concentrar na criação de campanhas de marketing inovadoras enquanto reduzem a carga sobre a TI.

Com o AEM Managed Services, os clientes podem obter os seguintes benefícios:

**Lançamento mais rápido**: com a infraestrutura de nuvem flexível do Adobe Managed Services, as organizações podem planejar, lançar e otimizar rapidamente experiências digitais bem-sucedidas. A Adobe gerencia a arquitetura de nuvem sem necessidade de capital adicional, hardware ou software e os engenheiros de soluções para o cliente da Adobe ajudam com a arquitetura, o provisionamento e a personalização da AEM para conexão com aplicativos de back-end e práticas recomendadas de ativação.

**Desempenho superior:** fornece experiências digitais confiáveis para sua empresa com quatro opções de disponibilidade de serviço: 99,5%, 99,9%, 99,95% e 99,99%. Além disso, permite o backup automático e modelos de recuperação de desastres multimodo para ajudar a garantir a confiabilidade e o gerenciamento de contingências.

**Custos de TI otimizados:** orientação proativa e conhecimento ajudam as organizações a se manterem atualizadas sobre a versão mais recente do AEM. O Suporte e manutenção Adobe Platinum está incluído automaticamente em novas implantações do AMS Enterprise/Basic, oferecendo experiência técnica e operacional para ajudar as organizações a manter seus aplicativos de missão crítica. Recursos básicos gratuitos do Analytics ou do Target oferecem valor adicional especialmente para organizações de médio porte com necessidades limitadas de análise e personalização.

**Segurança Máxima:** Garante a segurança física, de rede e de dados de nível empresarial ao hospedar aplicativos do cliente em um recurso de acesso restrito, atrás de sistemas de firewall ou dentro de uma nuvem privada virtual. Ele inclui máquinas virtuais de locatário único com criptografia de armazenamento de dados robusta, antivirais e isolamento de dados.

**Cloud Manager**: o Cloud Manager, parte da oferta do Adobe Experience Manager Managed Services, é um portal de autoatendimento que permite ainda mais que as organizações gerenciem o Adobe Experience Manager na nuvem. Ele inclui um pipeline de integração e entrega contínua (CI/CD) de última geração que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações sem comprometer o desempenho ou a segurança. O Cloud Manager só está disponível para clientes do Adobe Managed Service.

Para saber mais sobre o Cloud Manager e seus recursos, consulte [**Guia do Usuário do Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR).

## Introdução {#getting-started}

### Pré-requisitos {#prerequisites}

Enquanto as instâncias de produção são executadas em máquinas dedicadas que executam um sistema operacional com suporte oficial (consulte [Requisitos Técnicos](/help/sites-deploying/technical-requirements.md)), o servidor do Experience Manager será executado em qualquer sistema que ofereça suporte ao [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8).

Para fins de familiarização e para desenvolver no AEM, é comum usar uma instância instalada em seu computador local que executa o Apple OS X ou versões de desktop do Microsoft® Windows ou Linux®.

No lado do cliente, o AEM funciona com todos os navegadores modernos (**Microsoft® Edge**, **Internet Explorer** 11, **Chrome &#x200B;** 51+**&#x200B; **, **Firefox &#x200B;** 47+, **Safari** 8+) nos sistemas operacionais desktop e tablet. Consulte [Plataformas de Clientes com Suporte](/help/sites-deploying/technical-requirements.md#supported-client-platforms) para obter detalhes.

### Obtendo o software {#getting-the-software}

Os clientes com um contrato de manutenção e suporte válido devem ter recebido uma notificação por email com um código e poder baixar o AEM do [**Site de Licenciamento da Adobe**](https://licensing.adobe.com/). Parceiros comerciais podem solicitar acesso para download de [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

O pacote de software do AEM está disponível de duas formas:

* **cq-quickstart-6.5.0.jar:** Um arquivo executável autônomo *jar* que inclui tudo o que você precisa para começar a executar.

* **cq-quickstart-6.5.0.war:** Um arquivo *war* para implantação em um servidor de aplicativos de terceiros.

Na seção a seguir, descrevemos a **instalação independente**. Para obter detalhes sobre como instalar o AEM em um servidor de aplicativos, consulte [Instalação do Servidor de Aplicativos](/help/sites-deploying/application-server-install.md).

### Instalação local padrão {#default-local-install}

1. Crie um diretório de instalação no computador local. Por exemplo:

   Local de instalação do UNIX®: **/opt/aem**

   Local de instalação do Windows: **`C:\Program Files\aem`**

   Da mesma forma, é comum instalar instâncias de amostra em uma pasta logo na área de trabalho. Em qualquer caso, a Adobe se refere a esse local genericamente como:

   `<aem-install>`

   *O caminho do diretório de arquivos deve consistir somente em caracteres ASCII dos EUA.*

1. Coloque os arquivos **jar** e **de licença** neste diretório:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Se você não fornecer um arquivo `license.properties`, a AEM redirecionará seu navegador para uma tela de **Boas-vindas** na inicialização, onde você poderá inserir uma chave de licença. Você precisa solicitar uma chave de licença válida do Adobe se ainda não tiver uma.

1. Para iniciar a instância em um ambiente GUI, clique duas vezes no arquivo **`cq-quickstart-6.5.0.jar`**.

   Como alternativa, inicie o AEM na linha de comando:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

O AEM leva alguns minutos para descompactar o arquivo jar, instalar-se e iniciar. O procedimento acima resulta em:

* uma instância de **autor do AEM**
* executando em **localhost**
* na porta **4502**

Para acessar a instância, aponte seu navegador para:

**`https://localhost:4502`**

O resultado na instância do autor será configurado automaticamente para se conectar a uma **instância de publicação** em **`localhost:4503`**.

### Instalações do Author e Publish {#author-and-publish-installs}

A instalação padrão (uma instância de **autor** em **`localhost:4502`**) pode ser alterada simplesmente renomeando o arquivo `jar` antes de iniciá-lo pela primeira vez. O padrão de nomenclatura é:

**`cq-<instance-type>-p<port-number>.jar`**

Por exemplo, renomear o arquivo para

**`cq-author-p4502.jar`**

E iniciá-lo, resultará em uma instância de autor em execução em **`localhost:4502`**.

Da mesma forma, renomear e iniciar o arquivo

**`cq-publish-p4503.jar`**

Resulta em uma instância de publicação em execução em **`localhost:4503`**.

Você instalaria essas duas instâncias no, por exemplo

`<aem-install>/author`e

**`<aem-install>/publish`**

Para obter mais detalhes sobre como personalizar a instalação, consulte o seguinte:

* [Instalação Personalizada Independente](/help/sites-deploying/custom-standalone-install.md)
* [Modos de execução](/help/sites-deploying/configure-runmodes.md)

### Diretório de Instalação Desempacotado {#unpacked-install-directory}

Quando o jar de início rápido é iniciado pela primeira vez, ele é descompactado no mesmo diretório em um novo subdiretório chamado `crx-quickstart`. Você deve ter o seguinte:

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

Se a instância tiver sido instalada da interface do usuário, uma janela do navegador será aberta automaticamente e uma janela do aplicativo de desktop também será aberta, exibindo o host e a porta da instância e uma chave liga/desliga:

![tela de inicialização](assets/screen_shot_.png)

### Iniciando e Interrompendo {#starting-and-stopping}

Depois que o AEM tiver desempacotado a si mesmo e inicializado pela primeira vez, clicando duas vezes no arquivo jar no diretório de instalação simplesmente iniciará a instância, ela não a reinstalará.

Para parar a instância da GUI, clique no botão **ligar/desligar** na janela do aplicativo de desktop.

Você também pode interromper e iniciar o AEM a partir da linha de comando. Supondo que você já tenha instalado a instância pela primeira vez, os **scripts de linha de comando** estão aqui:

**`<aem-install>/crx-quickstart/bin/`**

Esta pasta contém os seguintes scripts de shell bash UNIX®:

* **`start`**: inicia a instância
* `stop`: Para a instância
* **`status`**: relata o status da instância
* **`quickstart`**: usado para configurar informações de início, se necessário.

Também há arquivos **`bat`** equivalentes para o Windows. Para obter informações mais detalhadas, consulte:

* [Início e Interrupção da Linha de Comando](/help/sites-deploying/command-line-start-and-stop.md)

O AEM inicia e redireciona automaticamente o navegador da Web para a página apropriada, geralmente a página de logon. Por exemplo:

`https://localhost:4502/`

![entrar na tela](assets/screen_shot_2019-04-08at83533am.png)

Depois de fazer logon, você terá acesso ao AEM. Para obter mais informações, dependendo da sua função, consulte o seguinte:

* [Criação  ](/help/sites-authoring/first-steps.md)
* [Administração](/help/sites-administering/home.md)
* [Desenvolver](/help/sites-developing/getting-started.md)
* [Gerenciamento](/help/managing/best-practices.md)

## Implantação avançada {#advanced-deployment}

A seção acima deve fornecer uma boa compreensão das noções básicas de instalação do AEM. No entanto, a instalação de um sistema de produção completo do AEM pode envolver consideravelmente mais complexidade. Para obter uma cobertura completa da instalação avançada, consulte as seguintes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalação Personalizada Independente](/help/sites-deploying/custom-standalone-install.md)
* [Instalação do Servidor de Aplicativos](/help/sites-deploying/application-server-install.md)
* [Resolução de problemas](/help/sites-deploying/troubleshooting.md)
* [Início e Interrupção da Linha de Comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuração](/help/sites-deploying/configuring.md)
* [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artigos de instruções sobre configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Práticas recomendadas](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [O que é o AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=pt-BR)
