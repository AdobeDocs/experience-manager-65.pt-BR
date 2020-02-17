---
title: Implantação e manutenção
seo-title: Implantação e manutenção
description: Saiba como começar a usar a instalação do AEM.
seo-description: Saiba como começar a usar a instalação do AEM.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
translation-type: tm+mt
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# Implantação e manutenção{#deploying-and-maintaining}

Nesta página, você encontrará:

* [Conceitos básicos](#basic-concepts)

   * [O que é o AEM?](#what-is-aem)
   * [Implantações típicas](#typical-deployment-scenarios)

      * [Local](#on-premise)
      * [Serviços gerenciados usando o Cloud Manager](#managed-services-using-cloud-manager)

* [Introdução](#getting-started)

   * [Pré-requisitos](#prerequisites)
   * [Obtendo o software](#getting-the-software)
   * [Instalação local padrão](#default-local-install)
   * [Instalações de autor e publicação](#author-and-publish-installs)
   * [Diretório de instalação descompactado](#unpacked-install-directory)
   * [Início e interrupção](#starting-and-stopping)

Depois de se familiarizar com essas noções básicas, você encontrará informações mais avançadas e detalhadas nas seguintes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalação do servidor de aplicativos](/help/sites-deploying/application-server-install.md)
* [Resolução de Problemas](/help/sites-deploying/troubleshooting.md)
* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuração](/help/sites-deploying/configuring.md)
* [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/sites-deploying/ecommerce.md)
* [Artigos sobre procedimentos de configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Melhores práticas](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Atualizar Definições do Veículo de Liberação](/help/sites-deploying/update-release-vehicle-definitions.md)
* [O que é o AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

## Conceitos básicos {#basic-concepts}

### O que é o AEM? {#what-is-aem}

O Adobe Experience Manager é um sistema cliente-servidor baseado na web para compilar, gerenciar e implantar sites comerciais e serviços relacionados. Corresponde a um número de funções do nível de infraestrutura e do aplicativo em um único pacote integrado.

No nível da infraestrutura, o AEM fornece o seguinte:

* **Servidor** de Aplicações Web: O AEM pode ser implantado no modo independente (inclui um servidor Web Jetty integrado) ou como um aplicativo da Web em um servidor de aplicativos de terceiros.
* **Estrutura** da Aplicação Web: O AEM incorpora o Sling Web Application Framework que simplifica a criação de aplicativos Web RESTful voltados para conteúdo.
* **Repositório** de conteúdo: O AEM inclui um Java Content Repository (JCR), um tipo de banco de dados hierárquico criado especificamente para dados não estruturados e semiestruturados. O repositório armazena não apenas o conteúdo voltado para o usuário, mas também todos os códigos, modelos e dados internos usados pelo aplicativo.

Com base nessa base, o AEM também oferece vários recursos no nível do aplicativo para o gerenciamento de:

* **Sites**
* **Aplicativos móveis**
* **Publicações digitais**
* **Forms**
* **Ativos digitais**
* **Comunidades**
* **Comércio online**

Por fim, os clientes podem usar esses blocos componentes de infraestrutura e de nível de aplicativo para criar soluções personalizadas ao criar aplicativos próprios.

O servidor AEM é baseado **em** Java e é executado na maioria dos sistemas operacionais compatíveis com essa plataforma. Toda interação do cliente com o AEM é feita por meio de um navegador **da** Web.

### Cenários de implantação típicos {#typical-deployment-scenarios}

Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor. Geralmente, as instalações do AEM envolvem pelo menos duas instâncias, normalmente executadas em máquinas separadas:

* **Autor**: Uma instância do AEM usada para criar, carregar e editar conteúdo e administrar o site. Depois que o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
* **Publicar**: Uma instância do AEM que fornece o conteúdo publicado ao público.

Essas instâncias são idênticas em termos de software instalado. Eles são diferenciados somente por configuração. Além disso, a maioria das instalações usa um dispatcher:

* **Dispatcher**: Um servidor Web estático (Apache httpd, Microsoft IIS etc.) aumentado com o módulo do dispatcher do AEM. Ele armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

Há muitas opções e elaborações avançadas dessa configuração, mas o padrão básico de autor, publicação e despachante está no centro da maioria das implantações. Começaremos por focar uma configuração relativamente simples. Seguir-se-á a discussão das opções de implantação avançadas.

As seções a seguir descrevem ambos os cenários:

* **Local**: AEM implantado e gerenciado em seu ambiente corporativo.

* **Serviços gerenciados - Gerenciador de nuvem para o Adobe Experience Manager**: AEM implantado e gerenciado pelos serviços gerenciados da Adobe.

### On-premise {#on-premise}

Você pode instalar o AEM em servidores em seu ambiente corporativo. As instâncias de instalação típicas incluem: Ambientes de desenvolvimento, teste e publicação. Consulte a seção [Introdução](/help/sites-deploying/deploy.md#getting%20started) para obter detalhes básicos sobre como fazer com que o software AEM seja instalado localmente.

Para saber mais sobre as implantações locais típicas, consulte [Implantações](/help/sites-deploying/recommended-deploys.md)recomendadas.

### Serviços gerenciados usando o Cloud Manager {#managed-services-using-cloud-manager}

O AEM Managed Services é uma solução completa para o gerenciamento da Experiência digital. Ele oferece benefícios da solução de entrega de experiência na nuvem, além de manter todos os benefícios de controle, segurança e personalização de uma implantação local. Os serviços gerenciados do AEM permitem que os clientes iniciem mais rapidamente ao implantar na nuvem e também ao aproveitar as práticas recomendadas e o suporte da Adobe. As organizações e os usuários empresariais podem envolver os clientes no mínimo de tempo, aumentar a participação no mercado e se concentrar na criação de campanhas de marketing inovadoras e, ao mesmo tempo, reduzir a carga sobre a TI.

Com os serviços gerenciados do AEM, os clientes podem obter os seguintes benefícios:

**** Mais rápido no mercado: Com a infraestrutura flexível de nuvem dos Serviços gerenciados da Adobe, as organizações podem planejar, lançar e otimizar rapidamente experiências digitais bem-sucedidas. A Adobe gerencia a arquitetura da nuvem sem necessidade de capital, hardware ou software adicionais e os engenheiros de sucesso do cliente da Adobe, ajuda com a arquitetura do AEM, provisionamento, personalização para conexão com aplicativos de back-end e práticas recomendadas.

**** Maior desempenho: Fornece experiências digitais confiáveis para sua empresa com quatro opções de disponibilidade de serviço, 99,5%, 99,9%, 99,95% e 99,99%. Além disso, permite o backup automático e modelos de recuperação de desastres multimodo para ajudar a garantir a confiabilidade e o gerenciamento de contingências.

**** Custos otimizados de TI: A orientação e o conhecimento proativos ajudam as organizações a permanecerem atualizadas na versão mais recente do AEM. A Manutenção e suporte do Adobe Platinum é incluída automaticamente em novas implantações do AMS Enterprise/Basic, oferecendo experiência técnica e operacional para ajudar as organizações a manter seus aplicativos essenciais. Os recursos básicos gratuitos do Analytics ou Target oferecem valor adicional, especialmente para organizações de médio mercado com necessidades limitadas de análise e personalização.

**** Maior segurança: Garante segurança física, de rede e de dados de nível empresarial, hospedando aplicativos de clientes em uma instalação de acesso restrito, atrás de sistemas de firewall ou dentro de uma nuvem privada virtual. Inclui máquinas virtuais de locatário único com criptografia de armazenamento de dados robusta, antivirais e isolamento de dados.

**Gerenciador** de nuvem: O Cloud Manager, parte da oferta de serviços gerenciados do Adobe Experience Manager, é um portal de autoatendimento que permite que as organizações gerenciem ainda mais o Adobe Experience Manager na nuvem. Ele inclui um pipeline avançado de integração contínua e entrega contínua (CI/CD) que permite que equipes de TI e parceiros de implementação acelerem a entrega de personalizações ou atualizações sem comprometer o desempenho ou a segurança. O Cloud Manager só está disponível para clientes do Adobe Managed Service.

Para saber mais sobre o Cloud Manager e seus recursos, consulte o Guia [**do usuário do **](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)Cloud Manager.

## Introdução {#getting-started}

### Pré-requisitos {#prerequisites}

Embora as instâncias de produção sejam normalmente executadas em máquinas dedicadas que executam um SO oficialmente compatível (consulte Requisitos [](/help/sites-deploying/technical-requirements.md)técnicos), o servidor Experience Manager será executado em qualquer sistema que suporte o [**Java Standard Edition 8 **](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Para fins de familiarização e desenvolvimento no AEM, é muito comum usar uma instância instalada em sua máquina local executando versões do Apple OS X ou de desktop do Microsoft Windows ou Linux.

No lado do cliente, o AEM funciona com todos os navegadores modernos (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) nos sistemas operacionais para desktop e tablet. Consulte Plataformas [de clientes](/help/sites-deploying/technical-requirements.md#supported-client-platforms) suportadas para obter detalhes.

### Obtendo o software {#getting-the-software}

Customers with a valid maintenance and support contract should have received a mail notification with a code and be able to download AEM from the [**Adobe Licensing Website **](https://licensing.adobe.com/). Business partners can request download access from[**spphelp@adobe.com**](mailto:spphelp@adobe.com).

O pacote de software AEM está disponível em duas versões:

* **** cq-quickstart-6.5.0.jar: Um arquivo *jar* executável independente que inclui tudo o que é necessário para iniciar e executar.

* **** cq-quickstart-6.5.0.war: Um arquivo de *guerra* para implantação em um servidor de aplicativos de terceiros.

Na seção a seguir descrevemos a instalação **** independente. Para obter detalhes sobre como instalar o AEM em um servidor de aplicativos, consulte Instalação [do servidor de](/help/sites-deploying/application-server-install.md)aplicativos.

### Instalação local padrão {#default-local-install}

1. Crie um diretório de instalação no computador local. Por exemplo:

   Local de instalação do UNIX: **/opt/aem**

   Local de instalação do Windows: **`C:\Program Files\aem`**

   Da mesma forma, é comum instalar instâncias de amostra em uma pasta diretamente na área de trabalho. Em qualquer caso, referimo-nos genericamente a esta localização como:

   `<aem-install>`

   *Observe que o caminho do diretório de arquivos deve consistir apenas em caracteres ASCII dos EUA.*

1. Coloque os arquivos **jar** e **license **neste diretório:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Se você não fornecer um `license.properties` arquivo, o AEM redirecionará seu navegador para uma tela de **boas-vindas** na inicialização, onde você pode inserir uma chave de licença. Você precisará solicitar uma chave de licença válida da Adobe se ainda não tiver uma.

1. Para iniciar a instância em um ambiente GUI, basta clicar duas vezes no **`cq-quickstart-6.5.0.jar`** arquivo.

   Como alternativa, você pode iniciar o AEM na linha de comando. Para uma VM Java de 32 bits, insira o seguinte:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   Para uma VM de 64 bits, insira:

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

O AEM levará alguns minutos para desempacotar o arquivo jar, instalar-se e iniciar. O procedimento acima resulta em:

* uma instância do autor **do** AEM
* em execução no **localhost**
* no porto **4502**

Para acessar a instância, aponte o navegador para:

**`https://localhost:4502`**

O resultado na instância do autor será configurado automaticamente para se conectar a uma instância **de** publicação em **`localhost:4503`**.

### Instalações de autor e publicação {#author-and-publish-installs}

A instalação padrão (uma instância do **autor** ativada **`localhost:4502`**) pode ser alterada simplesmente renomeando o `jar` arquivo antes de iniciá-lo pela primeira vez. O padrão de nomenclatura é:

**`cq-<instance-type>-p<port-number>.jar`**

Por exemplo, renomear o arquivo para

**`cq-author-p4502.jar`**

e iniciá-la resultará em uma instância do autor em execução **`localhost:4502`**.

Da mesma forma, renomear e iniciar o arquivo

**`cq-publish-p4503.jar`**

resultará em uma instância de publicação em execução **`localhost:4503`**.

Você instalaria essas duas instâncias em, por exemplo,

`<aem-install>/author`e

**`<aem-install>/publish`**

Para obter mais detalhes sobre como personalizar sua instalação, consulte o seguinte:

* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Modos de execução](/help/sites-deploying/configure-runmodes.md)

### Diretório de instalação descompactado {#unpacked-install-directory}

Quando o jar de início rápido for iniciado pela primeira vez, ele se descompactará no mesmo diretório sob um novo subdiretório chamado `crx-quickstart`. Você deve terminar com o seguinte:

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

Se a instância foi instalada da interface do usuário, então uma janela do navegador será aberta automaticamente e uma janela do aplicativo desktop também abrirá exibindo o host e a porta da instância e um switch de ativação/desativação:

![tela de inicialização](assets/screen_shot_.png)

>[!NOTE]
>
>Se você estiver usando links simbólicos, analise [os problemas com ele](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Início e interrupção {#starting-and-stopping}

Depois que o AEM se desempacotar e inicializar pela primeira vez, clicar duas vezes no arquivo jar no diretório de instalação simplesmente iniciará a instância, ela não a reinstalará.

Para interromper a instância da GUI, basta clicar no botão **ligar/desligar** na janela do aplicativo para desktop.

Você também pode parar e iniciar o AEM na linha de comando. Supondo que você já tenha instalado a instância pela primeira vez, os scripts **de linha de** comando estão localizados aqui:

**`<aem-install>/crx-quickstart/bin/`**

Esta pasta contém os seguintes scripts de shell básicos do Unix:

* **`start`**: Inicia a instância
* `stop`: Interrompe a instância
* **`status`**: Relata o Status da instância
* **`quickstart`**: Usado para configurar as informações de início, se necessário.

Também há **`bat`** arquivos equivalentes para o Windows. Para obter informações mais detalhadas, consulte:

* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)

O AEM inicia e redireciona automaticamente seu navegador da Web para a página apropriada, geralmente a página de logon; por exemplo:

`https://localhost:4502/`

![tela de logon](assets/screen_shot_2019-04-08at83533am.png)

Depois de conectado, você tem acesso ao AEM. Para obter mais informações, dependendo da sua função, consulte o seguinte:

* [Criação](/help/sites-authoring/home.md)
* [Administração](/help/sites-administering/home.md)
* [Desenvolvimento](/help/sites-developing/home.md)
* [Gerenciamento](/help/managing/best-practices.md)

## Implantação avançada {#advanced-deployment}

A seção acima deve fornecer uma boa compreensão das noções básicas da instalação do AEM. No entanto, a instalação de um sistema de produção completo do AEM pode envolver consideravelmente mais complexidade. Para obter a cobertura completa da instalação avançada, consulte as seguintes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalação do servidor de aplicativos](/help/sites-deploying/application-server-install.md)
* [Resolução de Problemas](/help/sites-deploying/troubleshooting.md)
* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuração](/help/sites-deploying/configuring.md)
* [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/sites-deploying/ecommerce.md)
* [Artigos sobre procedimentos de configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Melhores práticas](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Atualizar Definições do Veículo de Liberação](/help/sites-deploying/update-release-vehicle-definitions.md)
* [O que é o AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

