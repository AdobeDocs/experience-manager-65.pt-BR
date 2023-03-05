---
title: Implantação e manutenção
seo-title: Deploying and Maintaining
description: Saiba como começar a instalação do AEM.
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: 9052ed3e89fdc67d94fc60bbff64d42255565767
workflow-type: tm+mt
source-wordcount: '1802'
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
   * [Obtendo o software](#getting-the-software)
   * [Instalação local padrão](#default-local-install)
   * [Instalações do Author e Publish](#author-and-publish-installs)
   * [Diretório de Instalação Desempacotado](#unpacked-install-directory)
   * [Iniciando e Interrompendo](#starting-and-stopping)

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
* [Artigos de instruções sobre configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Práticas recomendadas    ](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [O que é o AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=pt-BR)

## Conceitos básicos {#basic-concepts}

### O que é o AEM? {#what-is-aem}

O Adobe Experience Manager é um sistema cliente-servidor baseado na web para compilar, gerenciar e implantar sites comerciais e serviços relacionados. Corresponde a um número de funções do nível de infraestrutura e do aplicativo em um único pacote integrado.

No nível da infraestrutura, o AEM oferece o seguinte:

* **Servidor de Aplicativos Web**: o AEM pode ser implantado no modo independente (inclui um servidor Web Jetty integrado) ou como um aplicativo Web em um servidor de aplicativos de terceiros.
* **Estrutura de Aplicativo Web**: o AEM incorpora a Sling Web Application Framework, que simplifica a criação de aplicativos Web RESTful orientados a conteúdo.
* **Repositório de conteúdo**: AEM inclui um Java Content Repository (JCR), um tipo de banco de dados hierárquico projetado especificamente para dados não estruturados e semiestruturados. O repositório armazena não apenas o conteúdo voltado para o usuário, mas também todos os códigos, modelos e dados internos usados pelo aplicativo.

Com base nessa base, o AEM também oferece vários recursos no nível de aplicativos para o gerenciamento de:

* **Sites**
* **Aplicativos móveis**
* **Publicações digitais**
* **Forms**
* **Ativos digitais**
* **Communities**
* **Comércio online**

Por fim, os clientes podem usar esses componentes básicos de infraestrutura e nível de aplicativo para criar soluções personalizadas, criando aplicativos próprios.

O servidor AEM é **Baseado em Java** e é executado na maioria dos sistemas operacionais compatíveis com essa plataforma. Toda interação do cliente com o AEM é feita por meio de uma **navegador da web**.

### Cenários de implantação típicos {#typical-deployment-scenarios}

Na terminologia AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor. As instalações de AEM geralmente envolvem pelo menos duas instâncias, normalmente executadas em máquinas separadas:

* **Autor**: uma instância do AEM usada para criar, carregar e editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
* **Publish**: uma instância do AEM que veicula o conteúdo publicado para o público.

Essas instâncias são idênticas em termos de software instalado. Eles são diferenciados somente pela configuração. Além disso, a maioria das instalações usa um dispatcher:

* **Dispatcher**: um servidor Web estático (Apache httpd, Microsoft IIS etc.) aumentado com o módulo dispatcher AEM. Ele armazena em cache páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

Há muitas opções e elaborações avançadas dessa configuração, mas o padrão básico do autor, publicação e dispatcher está no centro da maioria das implantações. Começaremos nos concentrando em um cenário relativamente simples. A discussão sobre as opções avançadas de implantação será realizada em seguida.

As seções a seguir descrevem ambos os cenários:

* **No local**: AEM implantado e gerenciado no ambiente corporativo.

* **Managed Services - Cloud Manager para Adobe Experience Manager**: AEM implantado e gerenciado pelo Adobe Managed Services.

### No local {#on-premise}

Você pode instalar o AEM em servidores em seu ambiente corporativo. As instâncias de instalação típicas incluem: Ambientes de desenvolvimento, teste e publicação. Consulte a [Introdução](/help/sites-deploying/deploy.md#getting%20started) para obter detalhes básicos sobre como obter o software AEM para instalá-lo localmente.

Para saber mais sobre as implantações locais típicas, consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md).

### Managed Services usando o Cloud Manager {#managed-services-using-cloud-manager}

O AEM Managed Services é uma solução completa para o gerenciamento de experiência digital. Ele fornece os benefícios da solução de entrega de experiência na nuvem, além de manter todos os benefícios de controle, segurança e personalização de uma implantação local. O AEM Managed Services permite que os clientes iniciem mais rapidamente, implantando na nuvem e também aproveitando as práticas recomendadas e o suporte do Adobe. As organizações e os usuários empresariais podem envolver os clientes em pouco tempo, impulsionar participação no mercado e se concentrar na criação de campanhas de marketing inovadoras enquanto reduzem a carga sobre a TI.

Com o AEM, os clientes da Managed Services podem obter os seguintes benefícios:

**Lançamento mais rápido:** Com a infraestrutura de nuvem flexível do Adobe Managed Services, as organizações podem planejar, iniciar e otimizar rapidamente experiências digitais bem-sucedidas. O Adobe gerencia a arquitetura de nuvem sem necessidade de capital adicional, hardware ou software e os engenheiros de soluções para clientes do Adobe, ajudam na arquitetura do AEM, no provisionamento, na personalização para conexão com aplicativos de back-end e nas práticas recomendadas de ativação.

**Maior desempenho:** Fornece experiências digitais confiáveis para sua empresa com quatro opções de disponibilidade de serviço: 99,5%, 99,9%, 99,95% e 99,99%. Além disso, permite modelos de backup automático e recuperação de desastres multimodo para ajudar a garantir a confiabilidade e o gerenciamento de contingências.

**Custos otimizados de TI:** A orientação proativa e a experiência ajudam as organizações a se manterem atualizadas sobre a versão mais recente do AEM. O Suporte e manutenção do Adobe Platinum é incluído automaticamente em novas implantações do AMS Enterprise/Basic, oferecendo experiência técnica e operacional para ajudar as organizações a manter seus aplicativos de missão crítica. Recursos básicos gratuitos do Analytics ou do Target oferecem valor adicional especialmente para organizações de médio porte com necessidades limitadas de análise e personalização.

**Maior segurança:** Garante a segurança física, de rede e de dados de nível empresarial ao hospedar os aplicativos do cliente em um recurso de acesso restrito, atrás de sistemas de firewall ou dentro de uma nuvem privada virtual. Ele inclui máquinas virtuais de locatário único com criptografia de armazenamento de dados robusta, antivirais e isolamento de dados.

**Cloud Manager**: o Cloud Manager, parte da oferta do Adobe Experience Manager Managed Services, é um portal de autoatendimento que permite que as organizações gerenciem manualmente o Adobe Experience Manager na nuvem. Ele inclui um pipeline de integração e entrega contínua (CI/CD) de última geração que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações sem comprometer o desempenho ou a segurança. O Cloud Manager só está disponível para clientes do Adobe Managed Service.

Para saber mais sobre o Cloud Manager e seus recursos, consulte [**Guia do usuário do Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html).

## Introdução {#getting-started}

### Pré-requisitos {#prerequisites}

Embora as instâncias de produção geralmente sejam executadas em máquinas dedicadas que executam um sistema operacional oficialmente compatível (consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)), o servidor Experience Manager será executado em qualquer sistema que suporte [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Para fins de familiarização e para desenvolver em AEM, é bastante comum usar uma instância instalada em sua máquina local que executa o Apple OS X ou versões de desktop do Microsoft Windows ou Linux.

No lado do cliente, o AEM funciona com todos os navegadores modernos (**Microsoft Edge**, **Internet Explorer** 11, **Cromo **51+** **, **Firefox **47+, **Safari** 8+) nos sistemas operacionais desktop e tablet. Consulte [Plataformas de cliente compatíveis](/help/sites-deploying/technical-requirements.md#supported-client-platforms) para obter detalhes.

### Obtendo o software {#getting-the-software}

Os clientes com um contrato válido de manutenção e suporte devem ter recebido uma notificação por email com um código e poder baixar o AEM da [**Site de licenciamento do Adobe**](https://licensing.adobe.com/). Os parceiros comerciais podem solicitar acesso para download do [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

O pacote de software AEM está disponível de duas formas:

* **cq-quickstart-6.5.0.jar:** Um executável autônomo *jar* arquivo que inclui tudo o que é necessário para começar a usar o.

* **cq-quickstart-6.5.0.war:** A *guerra* arquivo para implantação em um servidor de aplicativos de terceiros.

Na seção a seguir, descrevemos o **instalação independente**. Para obter detalhes sobre a instalação do AEM em um servidor de aplicativos, consulte [Instalação do Servidor de Aplicativos](/help/sites-deploying/application-server-install.md).

### Instalação local padrão {#default-local-install}

1. Crie um diretório de instalação no computador local. Por exemplo:

   Local de instalação do UNIX: **/opt/aem**

   Local de instalação do Windows: **`C:\Program Files\aem`**

   Da mesma forma, é comum instalar instâncias de amostra em uma pasta logo na área de trabalho. Em qualquer caso, nos referiremos a esse local genericamente como:

   `<aem-install>`

   *Observe que o caminho do diretório de arquivos deve consistir somente em caracteres ASCII dos EUA.*

1. Coloque o **jar** e **licença** arquivos neste diretório:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Se você não fornecer uma `license.properties` arquivo, o AEM redirecionará seu navegador para um **Bem-vindo** na inicialização, onde você pode inserir uma chave de licença. Você precisará solicitar uma chave de licença válida do Adobe se ainda não tiver uma.

1. Para iniciar a instância em um ambiente de GUI, basta clicar duas vezes no **`cq-quickstart-6.5.0.jar`** arquivo.

   Como alternativa, você pode iniciar o AEM na linha de comando:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

O AEM levará alguns minutos para descompactar o arquivo jar, instalar-se e iniciar. O procedimento acima resulta em:

* um **Autor do AEM** instância
* em execução **localhost**
* na porta **4502**

Para acessar a instância, aponte seu navegador para:

**`https://localhost:4502`**

O resultado na instância do autor será configurado automaticamente para se conectar a um **instância de publicação** em **`localhost:4503`**.

### Instalações do Author e Publish {#author-and-publish-installs}

A instalação padrão (uma **autor** instância em **`localhost:4502`**) pode ser alterado simplesmente renomeando o `jar` antes de iniciá-lo pela primeira vez. O padrão de nomenclatura é:

**`cq-<instance-type>-p<port-number>.jar`**

Por exemplo, renomear o arquivo para

**`cq-author-p4502.jar`**

e iniciá-lo resultará em uma instância de autor em execução **`localhost:4502`**.

Da mesma forma, renomear e iniciar o arquivo

**`cq-publish-p4503.jar`**

resultará em uma instância de publicação em execução em **`localhost:4503`**.

Você instalaria essas duas instâncias no, por exemplo

`<aem-install>/author`e

**`<aem-install>/publish`**

Para obter mais detalhes sobre como personalizar a instalação, consulte o seguinte:

* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Modos de execução](/help/sites-deploying/configure-runmodes.md)

### Diretório de Instalação Desempacotado {#unpacked-install-directory}

Quando o jar de início rápido for iniciado pela primeira vez, ele será descompactado no mesmo diretório em um novo subdiretório chamado `crx-quickstart`. Você deve terminar com o seguinte:

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

Se a instância tiver sido instalada da interface do usuário, uma janela do navegador será aberta automaticamente, e uma janela do aplicativo de desktop também será aberta, exibindo o host e a porta da instância e uma chave liga/desliga:

![tela de inicialização](assets/screen_shot_.png)

>[!NOTE]
>
>Se você estiver usando symlinks, dê uma olhada em [problemas com symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Iniciando e Interrompendo {#starting-and-stopping}

Depois que o AEM tiver desempacotado e iniciado pela primeira vez, clicando duas vezes no arquivo jar no diretório de instalação, simplesmente iniciará a instância e ela não a reinstalará.

Para interromper a instância da GUI, basta clicar no link **ligado/desligado** ligue a janela do aplicativo de desktop.

Você também pode parar e iniciar o AEM a partir da linha de comando. Supondo que você já tenha instalado a instância pela primeira vez, a variável **scripts de linha de comando** estão localizados aqui:

**`<aem-install>/crx-quickstart/bin/`**

Esta pasta contém os seguintes scripts de shell bash Unix:

* **`start`**: inicia a instância
* `stop`: interrompe a instância
* **`status`**: relata o status da instância
* **`quickstart`**: usado para configurar as informações de início, se necessário.

Há também **`bat`** para Windows. Para obter informações mais detalhadas, consulte:

* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)

O AEM inicia e redireciona automaticamente seu navegador da Web para a página apropriada, geralmente a página de logon; por exemplo:

`https://localhost:4502/`

![tela de logon](assets/screen_shot_2019-04-08at83533am.png)

Depois de conectado, você terá acesso ao AEM. Para obter mais informações, dependendo da sua função, consulte o seguinte:

* [Criação  ](/help/sites-authoring/home.md)
* [Administração](/help/sites-administering/home.md)
* [Desenvolvimento](/help/sites-developing/home.md)
* [Gerenciar](/help/managing/best-practices.md)

## Implantação avançada {#advanced-deployment}

A seção acima deve fornecer uma boa compreensão das noções básicas da instalação do AEM. No entanto, a instalação de um sistema completo de produção de AEM pode envolver consideravelmente mais complexidade. Para obter uma cobertura completa da instalação avançada, consulte as seguintes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalação independente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalação do servidor de aplicativos](/help/sites-deploying/application-server-install.md)
* [Resolução de problemas](/help/sites-deploying/troubleshooting.md)
* [Início e interrupção da linha de comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuração](/help/sites-deploying/configuring.md)
* [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artigos de instruções sobre configuração](/help/sites-deploying/ht-deploy.md)
* [Console da Web](/help/sites-deploying/web-console.md)
* [Solução de problemas de replicação](/help/sites-deploying/troubleshoot-rep.md)
* [Práticas recomendadas    ](/help/sites-deploying/best-practices.md)
* [Implantação de comunidades](/help/communities/deploy-communities.md)
* [Introdução à plataforma AEM](/help/sites-deploying/platform.md)
* [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md)
* [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [O que é o AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=pt-BR)
