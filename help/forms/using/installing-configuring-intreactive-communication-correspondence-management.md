---
title: Instalar e configurar o Interative Communications
seo-title: Instalar e configurar o Interative Communications
description: Instale e configure o AEM Forms Interative Communications para criar correspondências de negócios, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
seo-description: Instale e configure o AEM Forms Interative Communications para criar correspondências de negócios, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: a18a018181a779b9f48ef3e39c26410a1bc4919b
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---


# Instalar e configurar o Interative Communications{#install-and-configure-interactive-communications}

## Introdução {#introduction}

O AEM Form tem a capacidade de centralizar a criação, a montagem, o gerenciamento e o delivery de documentos seguros e interativos, como correspondentes comerciais, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas. Esse recurso é conhecido como comunicação interativa. O recurso está incluído no pacote suplementar de AEM Forms. O pacote complementar é implantado em uma instância de autor ou publicação do AEM.

Você pode usar o recurso de comunicação interativa para produzir comunicação em vários formatos. Por exemplo, Web e PDF. Você pode integrar comunicação interativa com o fluxo de trabalho do AEM para processar e fornecer a comunicação montada aos clientes no canal de sua escolha. Por exemplo, enviar uma comunicação para o usuário final por email.

Se você estiver atualizando de uma versão anterior e já tiver investido no gerenciamento de correspondência, poderá instalar o pacote [de](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) compatibilidade para continuar usando o gerenciamento de correspondência. Para obter informações sobre as diferenças entre a comunicação interativa e o gerenciamento de correspondência, consulte Visão geral [da comunicação](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)interativa.

O AEM Forms é uma plataforma poderosa de classe empresarial. A comunicação interativa é apenas uma das capacidades dos AEM Forms. Para obter a lista completa dos recursos, consulte [Introdução aos AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. Você precisa de apenas um AEM Author e uma instância de Processamento para executar o recurso Interative Communications. A topologia a seguir indica a topologia para executar AEM Forms Interative Communications, Correspondence Management, captura de dados de AEM Forms e fluxo de trabalho centrado em formulários em recursos OSGi. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

O AEM Forms Interative Communications executa interfaces de administrador, criação e usuário agente nas instâncias de Autor do AEM Forms. As instâncias de Publicação hospedam a versão final das comunicações interativas prontas para consumo pelos usuários finais.

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar os recursos interativos de comunicação e gerenciamento de correspondência dos AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada do hardware e software suportados, consulte os requisitos [](/help/sites-deploying/technical-requirements.md)técnicos.

* O caminho de instalação da instância do AEM não contém espaços em branco.
* Uma instância do AEM está ativa e em execução. Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de autor ou publicação. Você precisa de pelo menos uma instância do AEM (Autor ou Processamento) para executar os recursos de comunicação interativa e gerenciamento de correspondência do AEM Forms:

   * **Autor**: Uma instância do AEM usada para criar, carregar e editar conteúdo e administrar o site. Depois que o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Processando:** Uma instância de processamento é uma instância de AEM Author [endurecida](/help/forms/using/hardening-securing-aem-forms-environment.md) . Você pode configurar uma instância de Autor e endurecê-la depois de executar a instalação.

   * **Publicar**: Uma instância do AEM que fornece o conteúdo publicado ao público pela Internet ou por uma rede interna.

* Os requisitos de memória são atendidos. O pacote suplementar de AEM Forms requer:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* Requisitos adicionais para sistemas baseados em UNIX: Se você estiver usando o sistema operacional baseado em UNIX, instale os seguintes pacotes da mídia de instalação do respectivo sistema operacional.

<table>
 <tbody>
  <tr>
   <td>expatriado</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuídio</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
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

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. O pacote contém AEM Forms de comunicação interativa, gerenciamento de correspondência e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Distribuição [de](https://experience.adobe.com/downloads)software aberta. Você precisa de um Adobe ID para fazer login na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]** :
   1. Selecione **[!UICONTROL Formulários]** na lista suspensa **[!UICONTROL Solução]** .
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos]** do EULA e toque em **[!UICONTROL Download]**.
1. Abra o Gerenciador [de](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) pacotes e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Select the package and click **[!UICONTROL Install]**.

   Você também pode baixar o pacote por meio do link direto listado no artigo de versões [de](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não reinicie imediatamente o servidor.** Antes de parar o servidor AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no arquivo [AEM-Installation-Diretory]/crx-quickstart/logs/error.log e o log esteja estável.
1. Repita as etapas de 1 a 7 em todas as instâncias de Autor e Publicação.

## Configurações pós-instalação {#post-installation-configurations}

AEM Forms tem algumas configurações obrigatórias e opcionais. As configurações obrigatórias incluem a configuração das bibliotecas BouncyCastle e o agente de serialização. As configurações opcionais incluem a configuração do dispatcher e do Adobe Target.

### Configurações obrigatórias pós-instalação {#mandatory-post-installation-configurations}

#### Configurar bibliotecas RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para inicializar e delegar as bibliotecas:

1. Pare a instância subjacente do AEM.
1. Abra o diretório [\crx-quickstart\conf\sling.properties de instalação do]AEM para edição.

   Se você usou o diretório [\crx-quickstart\bin\start.bat de instalação do]AEM para start AEM, edite sling.properties localizado em [AEM_root]\crx-quickstart\.

1. Adicione as seguintes propriedades ao arquivo sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Salve e feche o arquivo e start a instância do AEM.
1. Repita as etapas de 1 a 4 em todas as instâncias de Autor e Publicação.

#### Configurar o agente de serialização {#configure-the-serialization-agent}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para adicionar o pacote à lista de permissões:

1. Abra o AEM Configuration Manager em uma janela do navegador. O URL padrão é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Pesquise e abra a Configuração **do firewall de** desserialização.
1. Adicione o pacote **sun.util.calendário** ao campo de **lista de permissões** . Clique em Salvar.
1. Repita as etapas de 1 a 3 em todas as instâncias de Autor e Publicação.

### Configurações opcionais pós-instalação {#optional-post-installation-configurations}

#### Instalar Pacote de Compatibilidade {#install-compatibility-package}

A comunicação interativa é a abordagem padrão e recomendada para criar comunicações com o cliente no AEM 6.5 Forms. Se você atualizou ou migrou de uma versão anterior e planeja continuar usando letras (Gerenciamento de correspondência), instale o pacote [Compatibilidade do](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)AEMFD.

O pacote Compatibilidade do AEMFD permite que você use os seguintes ativos do AEM 6.4 Forms, AEM 6.3 Forms e AEM 6.2 Forms em AEM 6.5 Forms:

* Fragmentos de Documento
* Cartas
* Dicionários de dados
* Formulários adaptáveis modelos e páginas obsoletos

#### Configurar Dispatcher {#configure-dispatcher}

A Dispatcher está armazenando em cache e balanceamento de carga em ferramenta para o AEM. O AEM Dispatcher também ajuda a proteger o servidor AEM contra ataques. Você pode aumentar a segurança de sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial. Se você usar o [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), execute as seguintes configurações para AEM Forms:

1. Configurar acesso para AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte a documentação [da](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)Dispatcher.

1. Configure o serviço de filtro de quem indicou:

   Faça logon no gerenciador de configuração Apache Felix como administrador. O URL padrão do gerenciador de configuração é https://&#39;server&#39;:[port_number]/system/console/configMgr. No menu **Configurações** , selecione a opção Filtro **** de Quem indicou Apache Sling. No campo Permitir hosts, digite o nome de host do dispatcher para permitir como uma quem indicou e clique em **Salvar**. O formato da entrada é https://&#39;[server]:[port]&#39;.

#### Integrar Adobe Target {#integrate-adobe-target}

Seus clientes provavelmente abandonarão uma comunicação interativa se a experiência que ela oferece não for interessante. Embora seja frustrante para os clientes, também pode aumentar o volume e o custo de suporte para a sua organização. É crítico e desafiador identificar e fornecer a experiência certa do cliente que aumenta a taxa de conversão. Os formulários do AEM têm a chave para esse problema.

Os formulários AEM se integram ao Adobe Target, uma solução Adobe Marketing Cloud, para oferecer experiências personalizadas e envolventes aos clientes em vários canais digitais. Para usar o Adobe Target para personalizar uma comunicação interativa, [integre o Adobe Target com AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurar a comunicação SSL para o Modelo de dados de formulário  {#configure-ssl-communcation-for-form-data-model}

Você pode habilitar a comunicação SSL para o Modelo de dados de formulário. Para ativar a comunicação SSL para o modelo de dados de Formulário, antes de iniciar qualquer instância do AEM Forms, adicione certificados ao Java Trust Store de todas as instâncias. Você pode executar o comando abaixo para adicionar os certificados:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Próximos passos {#next-steps}

Você configurou um ambiente para usar os recursos interativos de comunicação e gerenciamento de correspondência. Agora, os passos para usar esse recurso são:

* [Visão geral do gerenciamento de correspondência](/help/forms/using/interactive-communications-overview.md)

* [Criar uma comunicação interativa](../../forms/using/create-interactive-communication.md)

* [Criar uma carta de gerenciamento de correspondência](../../forms/using/create-letter.md)

