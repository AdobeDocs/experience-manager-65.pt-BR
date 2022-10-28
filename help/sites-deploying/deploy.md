---
title: Implantação e manutenção
seo-title: Deploying and Maintaining
description: Saiba como começar a usar a instalação do AEM.
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: bb8dbb9069c4575af62a4d0b21195cee75944fea
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 8%

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
   * [Obter o software](#getting-the-software)
   * [Instalação local padrão](#default-local-install)
   * [Instalações de criação e publicação](#author-and-publish-installs)
   * [Diretório de instalação descompactado](#unpacked-install-directory)
   * [Início e interrupção](#starting-and-stopping)

Depois de se familiarizar com essas noções básicas, você encontrará informações mais avançadas e detalhadas nas seguintes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalação do servidor de aplicativos](/help/sites-deploying/application-server-install.md)
* [Resolução de problemas](/help/sites-deploying/troubleshooting.md)
* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuração](/help/sites-deploying/configuring.md)
* [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artigos explicativos de configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Práticas recomendadas    ](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma de AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [O que é o AEM Screens?](https://docs.adobe.com/content/help/pt-BR/experience-manager-screens/user-guide/aem-screens-introduction.html)

## Conceitos básicos {#basic-concepts}

### O que é o AEM? {#what-is-aem}

O Adobe Experience Manager é um sistema cliente-servidor baseado na web para compilar, gerenciar e implantar sites comerciais e serviços relacionados. Corresponde a um número de funções do nível de infraestrutura e do aplicativo em um único pacote integrado.

No nível da infraestrutura, o AEM fornece o seguinte:

* **Servidor de Aplicações Web**: AEM pode ser implantado no modo independente (inclui um servidor Web Jetty integrado) ou como um aplicativo Web em um servidor de aplicativos de terceiros.
* **Estrutura de Aplicações Web**: AEM incorpora a Estrutura de Aplicativo Web do Sling que simplifica a escrita de aplicativos Web RESTful orientados ao conteúdo.
* **Repositório de conteúdo**: AEM inclui um Java Content Repository (JCR), um tipo de banco de dados hierárquico criado especificamente para dados não estruturados e semiestruturados. O repositório armazena não apenas o conteúdo voltado para o usuário, mas também todos os códigos, modelos e dados internos usados pelo aplicativo.

Com base nessa base, a AEM também oferece vários recursos no nível do aplicativo para o gerenciamento de:

* **Sites**
* **Aplicativos móveis**
* **Publicações digitais**
* **Forms**
* **Ativos digitais**
* **Communities**
* **Comércio online**

Por fim, os clientes podem usar essa infraestrutura e os blocos componentes do nível do aplicativo para criar soluções personalizadas, criando aplicativos próprios.

O servidor AEM é **Baseado em Java** O e é executado na maioria dos sistemas operacionais que suportam essa plataforma. Toda interação do cliente com o AEM é feita por meio de uma **navegador da web**.

### Cenários típicos de implantação {#typical-deployment-scenarios}

Em AEM terminologia, uma &quot;instância&quot; é uma cópia de AEM em execução em um servidor. As instalações AEM geralmente envolvem pelo menos duas instâncias, normalmente em máquinas separadas:

* **Autor**: Uma instância AEM usada para criar, carregar e editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
* **Publicar**: Uma instância de AEM que serve o conteúdo publicado para o público.

Essas instâncias são idênticas em termos de software instalado. Elas são diferenciadas somente pela configuração. Além disso, a maioria das instalações usa um dispatcher:

* **Dispatcher**: Um servidor Web estático (Apache httpd, Microsoft IIS etc.) aumentado com o módulo dispatcher AEM. Armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

Há muitas opções e elaborações avançadas dessa configuração, mas o padrão básico de autor, publicação e dispatcher está no centro da maioria das implantações. Começaremos por concentrar-nos num sistema relativamente simples. Seguirá-se a discussão sobre opções avançadas de implantação.

As seções a seguir descrevem os dois cenários:

* **No local**: AEM implantado e gerenciado no ambiente corporativo.

* **Managed Services - Cloud Manager para Adobe Experience Manager**: AEM implantado e gerenciado pelo Adobe Managed Services.

### No local {#on-premise}

Você pode instalar o AEM em servidores do seu ambiente corporativo. As instâncias de instalação típicas incluem: Ambientes de desenvolvimento, teste e publicação. Consulte a [Introdução](/help/sites-deploying/deploy.md#getting%20started) para obter detalhes básicos sobre como obter o software AEM para instalá-lo localmente.

Para saber mais sobre as implantações locais típicas, consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md).

### Managed Services usando o Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services é uma solução completa para o gerenciamento de experiência digital. Ela oferece benefícios da solução de entrega de experiência na nuvem, além de manter todos os benefícios de controle, segurança e personalização de uma implantação local. AEM Managed Services permite que os clientes iniciem mais rápido ao implantar na nuvem e também se apoiando nas práticas recomendadas e no suporte do Adobe. As organizações e os usuários empresariais podem envolver os clientes em um período mínimo, aumentar a participação no mercado e se concentrar na criação de campanhas de marketing inovadoras e, ao mesmo tempo, reduzir a carga sobre a TI.

Com AEM Managed Services, os clientes podem obter os seguintes benefícios:

**Acesso mais rápido ao mercado:** Com a infraestrutura em nuvem flexível do Adobe Managed Services, as organizações podem planejar, lançar e otimizar rapidamente experiências digitais bem-sucedidas. O Adobe gerencia a arquitetura de nuvem sem necessidade de capital, hardware ou software adicional e os engenheiros de sucesso do cliente do Adobe, ajuda com AEM arquitetura, provisionamento, personalização para conexão com aplicativos de back-end e práticas recomendadas.

**Maior desempenho:** Fornece experiências digitais confiáveis para sua empresa com quatro opções de disponibilidade de serviço 99,5%, 99,9%, 99,95% e 99,99%. Além disso, permite o backup automático e modelos de recuperação de desastres multimodo para ajudar a garantir a confiabilidade e o gerenciamento de contingências.

**Custos de TI otimizados:** A orientação e o conhecimento proativos ajudam as organizações a manter-se atualizadas com a versão mais recente do AEM. A manutenção e o suporte do Adobe Platinum são incluídos automaticamente em novas implantações do AMS Enterprise/Basic, oferecendo conhecimento técnico e experiência operacional para ajudar as organizações a manter seus aplicativos essenciais. Os recursos básicos gratuitos do Analytics ou do Target oferecem valor adicional, especialmente para organizações intermediárias com necessidades limitadas de análise e personalização.

**Maior segurança:** Garante segurança física, de rede e de dados de nível empresarial, hospedando aplicativos de clientes em um recurso de acesso restrito, por trás de sistemas de firewall ou dentro de uma nuvem privada virtual. Ele inclui máquinas virtuais de único locatário com criptografia de armazenamento de dados robusta, antivirais e isolamento de dados.

**Cloud Manager**: O Cloud Manager, parte da oferta da Adobe Experience Manager Managed Services, é um portal de autoatendimento que permite ainda mais que as organizações autogerenciem o Adobe Experience Manager na nuvem. Ele inclui um pipeline de integração contínua e entrega contínua (CI/CD) de última geração que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações sem comprometer o desempenho ou a segurança. O Cloud Manager só está disponível para clientes do Adobe Managed Service.

Para saber mais sobre o Cloud Manager e seus recursos, consulte [**Guia do usuário do Cloud Manager**](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Introdução {#getting-started}

### Pré-requisitos {#prerequisites}

Embora as instâncias de produção sejam normalmente executadas em máquinas dedicadas que executam um SO oficialmente suportado (consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)), o servidor Experience Manager será executado em qualquer sistema compatível [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Para fins de familiarização e desenvolvimento em AEM é bem comum usar uma instância instalada em sua máquina local que execute as versões do Apple OS X ou desktop do Microsoft Windows ou Linux.

No lado do cliente, o AEM funciona com todos os navegadores modernos (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) nos sistemas operacionais desktop e tablet. Consulte [Plataformas compatíveis de clientes](/help/sites-deploying/technical-requirements.md#supported-client-platforms) para obter detalhes.

### Obter o software {#getting-the-software}

Os clientes com um contrato válido de manutenção e suporte devem ter recebido uma notificação por e-mail com um código e podem baixar AEM do [**Site de licenciamento de Adobe**](https://licensing.adobe.com/). Os parceiros comerciais podem solicitar acesso para download a partir de [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

O pacote de software AEM está disponível em dois formatos:

* **cq-quickstart-6.5.0.jar:** Um executável independente *jarro* arquivo que inclui tudo o que é necessário para ativar e executar.

* **cq-quickstart-6.5.0.war:** A *guerra* para implantação em um servidor de aplicativos de terceiros.

Na seção a seguir, descrevemos a variável **instalação autônoma**. Para obter detalhes sobre a instalação do AEM em um servidor de aplicativos, consulte [Instalação do servidor de aplicativos](/help/sites-deploying/application-server-install.md).

### Instalação local padrão {#default-local-install}

1. Crie um diretório de instalação no computador local. Por exemplo:

   Local de instalação UNIX: **/opt/aem**

   Local de instalação do Windows: **`C:\Program Files\aem`**

   Da mesma forma, é comum instalar instâncias de exemplo em uma pasta diretamente na área de trabalho. Em qualquer caso, referiremos-nos genericamente a esta localização como:

   `<aem-install>`

   *Observe que o caminho do diretório de arquivos deve consistir apenas em caracteres ASCII dos EUA.*

1. Coloque o **jarro** e **licença **arquivos neste diretório:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Se você não fornecer uma `license.properties` AEM redirecionará seu navegador para um **Welcome** na inicialização, onde você pode inserir uma chave de licença. Você precisará solicitar uma chave de licença válida do Adobe se ainda não tiver uma.

1. Para iniciar a instância em um ambiente GUI, clique duas vezes no botão **`cq-quickstart-6.5.0.jar`** arquivo.

   Como alternativa, você pode iniciar o AEM na linha de comando:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM levará alguns minutos para descompactar o arquivo jar, instalar e iniciar. O procedimento acima resulta em:

* um **Autor AEM** instância
* em execução **localhost**
* no porto **4502**

Para acessar a instância, aponte o navegador para:

**`https://localhost:4502`**

O resultado na instância do autor será configurado automaticamente para se conectar a um **instância de publicação** on **`localhost:4503`**.

### Instalações de criação e publicação {#author-and-publish-installs}

A instalação padrão (um **autor** instância em **`localhost:4502`**) pode ser alterada simplesmente renomeando o `jar` antes de iniciá-lo pela primeira vez. O padrão de nomenclatura é:

**`cq-<instance-type>-p<port-number>.jar`**

Por exemplo, renomear o arquivo para

**`cq-author-p4502.jar`**

e iniciá-la resultará em uma instância de autor em execução em **`localhost:4502`**.

Da mesma forma, renomear e iniciar o arquivo

**`cq-publish-p4503.jar`**

resultará em uma instância de publicação em execução em **`localhost:4503`**.

Você instalaria essas duas instâncias no, por exemplo,

`<aem-install>/author`e

**`<aem-install>/publish`**

Para obter mais detalhes sobre como personalizar sua instalação, consulte o seguinte:

* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Modos de execução](/help/sites-deploying/configure-runmodes.md)

### Diretório de instalação descompactado {#unpacked-install-directory}

Quando o jar do início rápido for iniciado pela primeira vez, ele será descompactado no mesmo diretório em um novo subdiretório chamado `crx-quickstart`. Você deve acabar com o seguinte:

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

Se a instância foi instalada da interface do usuário, uma janela do navegador será aberta automaticamente e uma janela do aplicativo de desktop também será aberta exibindo o host e a porta da instância e um switch on/off:

![tela iniciar](assets/screen_shot_.png)

>[!NOTE]
>
>Se você estiver usando links simbólicos, consulte [problemas com link simbólico](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Início e interrupção {#starting-and-stopping}

Depois que o AEM tiver se descompactado e iniciado pela primeira vez, clicar duas vezes no arquivo jar no diretório de instalação simplesmente iniciará a instância, ela não a reinstalará.

Para interromper a instância da GUI, basta clicar no botão **ligado/desligado** na janela do aplicativo de desktop.

Você também pode parar e iniciar o AEM a partir da linha de comando. Supondo que você já tenha instalado a instância pela primeira vez, a variável **scripts de linha de comando** estão localizadas aqui:

**`<aem-install>/crx-quickstart/bin/`**

Esta pasta contém os seguintes scripts de shell de base Unix:

* **`start`**: Inicia a instância
* `stop`: Interrompe a instância
* **`status`**: Relata o Status da instância
* **`quickstart`**: Usado para configurar as informações de início, se necessário.

Também há equivalentes **`bat`** arquivos para Windows. Para obter informações mais detalhadas, consulte:

* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)

AEM inicia e redireciona automaticamente o navegador para a página apropriada, geralmente a página de logon; por exemplo:

`https://localhost:4502/`

![tela de logon](assets/screen_shot_2019-04-08at83533am.png)

Depois de fazer logon, você tem acesso ao AEM. Para obter mais informações, dependendo da sua função, consulte o seguinte:

* [Criação  ](/help/sites-authoring/home.md)
* [Administração](/help/sites-administering/home.md)
* [Desenvolvimento](/help/sites-developing/home.md)
* [Gerenciar](/help/managing/best-practices.md)

## Implantação avançada {#advanced-deployment}

A seção acima deve fornecer uma boa compreensão das noções básicas AEM instalação. No entanto, a instalação de um sistema de produção completo de AEM pode envolver consideravelmente mais complexidade. Para obter a cobertura completa da instalação avançada, consulte as seguintes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalação do servidor de aplicativos](/help/sites-deploying/application-server-install.md)
* [Resolução de problemas](/help/sites-deploying/troubleshooting.md)
* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuração](/help/sites-deploying/configuring.md)
* [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md)
* [comércio eletrônico](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artigos explicativos de configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Práticas recomendadas    ](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma de AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [O que é o AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
