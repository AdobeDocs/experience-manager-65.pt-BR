---
title: Instalar e configurar Comunicações interativas
seo-title: Install and configure Interactive Communications
description: Instale e configure as Comunicações interativas do AEM Forms para criar correspondências comerciais, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 7%

---

# Instalar e configurar Comunicações interativas{#install-and-configure-interactive-communications}

## Introdução {#introduction}

AEM Formulário tem a capacidade de centralizar a criação, montagem, gerenciamento e entrega de documentos seguros e interativos, como correspondências comerciais, documentos, demonstrativos, avisos de benefícios, emails de marketing, contas e kits de boas-vindas. Esse recurso é conhecido como comunicação interativa. O recurso está incluído no pacote complementar do AEM Forms. O pacote complementar é implantado em uma instância de Autor ou Publicação do AEM.

Você pode usar o recurso de comunicação interativa para produzir comunicação em vários formatos. Por exemplo, web e PDF. É possível integrar a comunicação interativa com AEM fluxo de trabalho para processar e fornecer a comunicação montada aos clientes no canal de sua escolha. Por exemplo, enviar uma comunicação para o usuário final por email.

Se estiver atualizando de uma versão anterior e já tiver investido no gerenciamento de correspondência, você poderá instalar o [pacote de compatibilidade](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) continuar a utilizar o gerenciamento de correspondência. Para obter informações sobre as diferenças entre a comunicação interativa e o gerenciamento de correspondência, consulte [Visão geral da comunicação interativa](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

O AEM Forms é uma plataforma avançada de nível empresarial. A comunicação interativa é apenas um dos recursos do AEM Forms. Para obter a lista completa de recursos, consulte [Introdução ao AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote do complemento AEM Forms é um aplicativo implantado em AEM. Você precisa de apenas um mínimo de uma instância de Autor e Processamento do AEM para executar o recurso Comunicações interativas. A topologia a seguir é indicativa para executar as Comunicações interativas da AEM Forms, o Gerenciamento de correspondência, a captura de dados da AEM Forms e o fluxo de trabalho centrado na Forms nos recursos OSGi. Para obter informações detalhadas sobre a topologia, consulte [Topologias de arquitetura e implantação do AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

O AEM Forms Interative Communications executa interfaces de administração, criação e usuário agente nas instâncias de Autor do AEM Forms. As instâncias de Publicação hospedam a versão final das comunicações interativas que estão prontas para consumo pelos usuários finais.

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar os recursos interativos de comunicação e gerenciamento de correspondência do AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada de hardware e software suportados, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* O caminho de instalação da instância de AEM não contém espaços em branco.
* Uma instância de AEM está em execução. Na terminologia AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de criação ou publicação. Você precisa de pelo menos uma instância AEM (Autor ou Processamento) para executar os recursos de comunicação interativa e gerenciamento de correspondência do AEM Forms:

   * **Autor**: Uma instância AEM usada para criar, carregar e editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Processamento:** Uma instância de processamento é uma [Autor fortalecido do AEM](/help/forms/using/hardening-securing-aem-forms-environment.md) instância. Você pode configurar uma instância de Autor e endurecê-la após executar a instalação.

   * **Publicar**: Uma instância de AEM que disponibiliza o conteúdo publicado ao público pela Internet ou por uma rede interna.

* Os requisitos de memória são cumpridos. O pacote do complemento AEM Forms requer:

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
   <td>libuuid</td>
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

## Instalar o pacote complementar do AEM Forms {#install-aem-forms-add-on-package}

O pacote do complemento AEM Forms é um aplicativo implantado em AEM. O pacote contém comunicação interativa do AEM Forms, gerenciamento de correspondência e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Clique em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Também é possível usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional e selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Baixar]**.
1. Abra [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

   Também é possível baixar o pacote por meio do link direto listado no [Versões do AEM Forms](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) artigo 10. o

1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não reinicie imediatamente o servidor.** Antes de parar o servidor do AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no [AEM-Installation-Diretory]/crx-quickstart/logs/error.log e o log é estável.
1. Repita as etapas de 1 a 7 em todas as instâncias de Autor e Publicação.

## Configurações pós-instalação {#post-installation-configurations}

O AEM Forms tem algumas configurações obrigatórias e opcionais. As configurações obrigatórias incluem a configuração de bibliotecas BouncyCastle e o agente de serialização. As configurações opcionais incluem a configuração do dispatcher e do Adobe Target.

### Configurações obrigatórias pós-instalação {#mandatory-post-installation-configurations}

#### Configurar bibliotecas RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para inicializar e delegar as bibliotecas:

1. Pare a instância AEM subjacente.
1. Abra o [AEM diretório de instalação]\crx-quickstart\conf\sling.properties para edição.

   Se você usou [AEM diretório de instalação]\crx-quickstart\bin\start.bat para iniciar o AEM, em seguida, edite o sling.properties localizado em [AEM_root]\crx-quickstart\.

1. Adicione as seguintes propriedades ao arquivo sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Salve e feche o arquivo e inicie a instância de AEM.
1. Repita as etapas de 1 a 4 em todas as instâncias de Autor e Publicação.

#### Configurar o agente de serialização {#configure-the-serialization-agent}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para adicionar o pacote à  de lista de permissões:

1. Abra AEM Configuration Manager em uma janela do navegador. O URL padrão é https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Pesquisar e abrir **Configuração do firewall de desserialização**.
1. Adicione o **sun.util.calendar** para **lista de permissões** campo. Clique em Salvar.
1. Repita as etapas de 1 a 3 em todas as instâncias de Autor e Publicação.

### Configurações opcionais pós-instalação {#optional-post-installation-configurations}

#### Instalar Pacote de Compatibilidade {#install-compatibility-package}

A comunicação interativa é a abordagem padrão e recomendada para criar comunicações com clientes no AEM 6.5 Forms. Se você atualizou ou migrou de uma versão anterior e planeja continuar usando cartas (Gerenciamento de correspondência), instale o [Pacote de compatibilidade AEMFD](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT).

O pacote de compatibilidade do AEMFD permite usar os seguintes ativos do AEM 6.4 Forms, AEM 6.3 Forms e AEM 6.2 Forms no AEM 6.5 Forms:

* Fragmentos de documento
* Cartas
* Dicionários de dados
* Modelos e páginas obsoletas de formulários adaptáveis

#### Configurar o Dispatcher {#configure-dispatcher}

O Dispatcher é uma ferramenta de armazenamento em cache e/ou balanceamento de carga do Adobe Experience Manager, que pode ser usado em conjunto com um servidor Web de classe empresarial. Se você usar [Dispatcher](https://helpx.adobe.com/pt/experience-manager/dispatcher/using/dispatcher-configuration.html)e, em seguida, execute as seguintes configurações para o AEM Forms:

1. Configuração do acesso para AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte [Documentação do Dispatcher](https://helpx.adobe.com/pt/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure o serviço de filtro do referenciador:

   Faça logon no gerenciador de configuração do Apache Felix como administrador. O URL padrão do gerenciador de configuração é https://&#39;server&#39;:[port_number]/system/console/configMgr. No **Configurações** selecione o **Filtro de referenciador do Apache Sling** opção. No campo Permitir hosts , insira o nome do host do dispatcher para permitir como referenciador e clique em **Salvar**. O formato da entrada é https://&#39;[server]:[porta]&quot;.

#### Integrar o Adobe Target {#integrate-adobe-target}

Seus clientes provavelmente abandonarão uma comunicação interativa se a experiência que ela oferece não for envolvente. Embora seja frustrante para os clientes, também é possível aumentar o volume e o custo de suporte para sua organização. É essencial e desafiador identificar e fornecer a experiência correta do cliente que aumenta a taxa de conversão. O AEM forms tem a chave para esse problema.

AEM formulários é integrado ao Adobe Target, uma solução da Adobe Marketing Cloud, para fornecer experiências personalizadas e envolventes para o cliente em vários canais digitais. Para usar o Adobe Target para personalizar uma comunicação interativa, [Integrar o Adobe Target ao AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurar comunicação SSL para o Modelo de dados de formulário  {#configure-ssl-communcation-for-form-data-model}

Você pode ativar a comunicação SSL para o Modelo de dados de formulário. Para habilitar a comunicação SSL para o modelo de dados de Formulário, antes de iniciar qualquer instância do AEM Forms, adicione certificados ao Java Trust Store de todas as instâncias. Você pode executar o comando abaixo para adicionar os certificados:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Próximas etapas {#next-steps}

Você configurou um ambiente para usar os recursos interativos de comunicação e gerenciamento de correspondência. Agora, as etapas para usar o recurso são:

* [Visão geral do gerenciamento de correspondência](/help/forms/using/interactive-communications-overview.md)

* [Criar uma comunicação interativa](../../forms/using/create-interactive-communication.md)

* [Criar uma carta de gerenciamento de correspondência](../../forms/using/create-letter.md)
