---
title: Instalar e configurar as Comunicações interativas
seo-title: Install and configure Interactive Communications
description: Instale e configure as Comunicações interativas do AEM Forms para criar correspondências comerciais, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 7%

---

# Instalar e configurar as Comunicações interativas{#install-and-configure-interactive-communications}

## Introdução {#introduction}

O AEM Form tem a capacidade de centralizar a criação, montagem, gerenciamento e entrega de documentos seguros e interativos, como correspondências comerciais, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas. Esse recurso é conhecido como comunicação interativa. O recurso está incluído no pacote complementar do AEM Forms. O pacote complementar é implantado em uma instância de Autor ou Publicação do AEM.

Você pode usar o recurso de comunicação interativa para produzir comunicação em vários formatos. Por exemplo, web e PDF. É possível integrar a comunicação interativa com o fluxo de trabalho do AEM para processar e entregar a comunicação montada aos clientes no canal de sua escolha. Por exemplo, enviar uma comunicação para o usuário final por email.

Se estiver atualizando de uma versão anterior e já tiver investido no gerenciamento de correspondência, você pode instalar o [pacote de compatibilidade](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) para continuar usando o gerenciamento de correspondência. Para obter informações sobre as diferenças entre a comunicação interativa e o gerenciamento de correspondência, consulte [Visão geral da comunicação interativa](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

O AEM Forms é uma plataforma poderosa de nível empresarial. A comunicação interativa é apenas um dos recursos do AEM Forms. Para obter a lista completa dos recursos, consulte [Introdução ao AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. É necessário ter no mínimo uma instância de Autor e Processamento do AEM para executar o recurso de Comunicações interativas. A topologia a seguir é uma topologia indicativa para executar as Comunicações interativas da AEM Forms, o Gerenciamento de correspondência, a captura de dados da AEM Forms e o fluxo de trabalho centrado na Forms em recursos OSGi. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação do AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

As Comunicações interativas do AEM Forms executam interfaces de administrador, criação e usuário do agente nas instâncias de Autor do AEM Forms. As instâncias de Publicação hospedam a versão final das comunicações interativas que estão prontas para consumo pelos usuários finais.

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar a comunicação interativa e os recursos de gerenciamento de correspondência do AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada de hardware e software compatíveis, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* O caminho de instalação da instância do AEM não contém espaços em branco.
* Uma instância do AEM está em funcionamento. Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de criação ou publicação. Você precisa de pelo menos uma instância AEM (Autor ou Processamento) para executar a comunicação interativa do AEM Forms e os recursos de gerenciamento de correspondência:

   * **Autor**: uma instância do AEM usada para criar, carregar e editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Processando:** Uma instância de processamento é uma [AEM Author protegido](/help/forms/using/hardening-securing-aem-forms-environment.md) instância. Você pode configurar uma instância de Autor e fortalecê-la após executar a instalação.

   * **Publish**: uma instância do AEM que veicula o conteúdo publicado para o público pela Internet ou por uma rede interna.

* Os requisitos de memória são atendidos. O pacote complementar do AEM Forms exige:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft® Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* Requisitos adicionais para sistemas baseados em UNIX: Se você estiver usando o sistema operacional baseado em UNIX, instale os seguintes pacotes da mídia de instalação do respectivo sistema operacional.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softoken-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Instalar pacote complementar do AEM Forms {#install-aem-forms-add-on-package}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. O pacote contém comunicação interativa do AEM Forms, gerenciamento de correspondência e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Clique em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional e selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Baixar]**.
1. Abra [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

   Também é possível baixar o pacote por meio do link direto listado no [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) artigo.

1. Após a instalação do pacote, você será solicitado a reiniciar a instância do AEM. **Não reinicie o servidor imediatamente.** Antes de interromper o AEM Forms Server, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no [AEM-Diretório-Instalação]/crx-quickstart/logs/error.log e o log é estável.
1. Repita as etapas de 1 a 7 em todas as instâncias de Autor e Publicação.

## Configurações pós-instalação {#post-installation-configurations}

O AEM Forms tem algumas configurações obrigatórias e opcionais. As configurações obrigatórias incluem a configuração de bibliotecas BouncyCastle e o agente de serialização. As configurações opcionais incluem a configuração do Dispatcher e do Adobe Target.

### Configurações obrigatórias pós-instalação {#mandatory-post-installation-configurations}

#### Configurar bibliotecas RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Execute as seguintes etapas em todas as instâncias Autor e Publicar para inicializar, delegar as bibliotecas:

1. Interrompa a instância subjacente do AEM.
1. Abra o [Diretório de instalação do AEM]arquivo \crx-quickstart\conf\sling.properties para edição.

   Se você usou [Diretório de instalação do AEM]\crx-quickstart\bin\start.bat para iniciar o AEM e, em seguida, edite o sling.properties em [AEM_root]\crx-quickstart\.

1. Adicione as seguintes propriedades ao arquivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Salve e feche o arquivo e inicie a instância do AEM.
1. Repita as etapas 1 a 4 em todas as instâncias de Autor e Publicação.

#### Configurar o agente de serialização {#configure-the-serialization-agent}

Execute as seguintes etapas em todas as instâncias Autor e Publicar para adicionar o pacote ao arquivo de inclui na lista de permissões:

1. Abra o Gerenciador de configuração do AEM em uma janela do navegador. O URL padrão é https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Pesquisar e abrir **Configuração do firewall de desserialização**.
1. Adicione o **sun.util.calendar** pacote para o **➡ incluir na lista de permissões** campo. Clique em Salvar.
1. Repita as etapas 1 a 3 em todas as instâncias de Autor e Publicação.

### Configurações pós-instalação opcionais {#optional-post-installation-configurations}

#### Instalar pacote de compatibilidade {#install-compatibility-package}

A comunicação interativa é a abordagem padrão e recomendada para criar comunicações com o cliente no AEM 6.5 Forms. Se você tiver atualizado ou migrado de uma versão anterior do e planeja continuar usando as cartas (Gerenciamento de correspondência), instale o [Pacote de compatibilidade do AEMFD](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=en).

O pacote de compatibilidade do AEMFD permite usar os seguintes ativos do AEM 6.4 Forms, AEM 6.3 Forms AEM e 6.2 Forms AEM no 6.5 Forms:

* Fragmentos do documento
* Cartas
* Dicionários de dados
* Modelos e páginas obsoletas dos formulários adaptáveis

#### Configurar o Dispatcher {#configure-dispatcher}

O Dispatcher é a ferramenta de armazenamento em cache e balanceamento de carga do Adobe Experience Manager, e ele é usado em conjunto com um servidor da web de classe empresarial. Se você usar [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR), em seguida, execute as seguintes configurações para o AEM Forms:

1. Configure o acesso para o AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte [Documentação do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR).

1. Configure o serviço de filtro referenciador:

   Faça logon no gerenciador de configurações Apache Felix como administrador. O URL padrão do gerenciador de configurações é https://&#39;server&#39;:[port_number]/system/console/configMgr No **Configurações** selecione o **Filtro referenciador do Apache Sling** opção. No campo Permitir Hosts, informe o nome do host do Dispatcher para permitir isso como um referenciador e clique em **Salvar**. O formato da entrada é https://&#39;[server]:[porta]&#39;.

#### Integrar o Adobe Target {#integrate-adobe-target}

É provável que seus clientes abandonem uma comunicação interativa se a experiência que ela oferece não for atraente. Embora seja frustrante para os clientes, também aumenta o volume de suporte e o custo para a sua organização. É crítico e desafiador identificar e fornecer a experiência certa ao cliente que aumente a taxa de conversão. A AEM Forms é a chave para esse problema.

O AEM forms é integrado ao Adobe Target, uma solução da Adobe Experience Cloud, para fornecer experiências personalizadas e envolventes ao cliente em vários canais digitais. Para usar o Adobe Target para personalizar uma comunicação interativa, [Integrar o Adobe Target com o AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurar a comunicação SSL para o modelo de dados de formulário  {#configure-ssl-communcation-for-form-data-model}

Você pode ativar a comunicação SSL para o Modelo de dados de formulário. Para ativar a comunicação SSL para o modelo de dados de formulário, antes de iniciar qualquer instância do AEM Forms, adicione certificados ao Java™ Trust Store de todas as instâncias. Você pode executar o comando abaixo para adicionar os certificados:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Próximas etapas {#next-steps}

Você configurou um ambiente para usar a comunicação interativa e os recursos de gestão de correspondência. Agora, as etapas para usar o recurso são:

* [Visão geral do gerenciamento de correspondência](/help/forms/using/interactive-communications-overview.md)

* [Criar uma comunicação interativa](../../forms/using/create-interactive-communication.md)

* [Criar uma carta de gerenciamento de correspondência](../../forms/using/create-letter.md)
