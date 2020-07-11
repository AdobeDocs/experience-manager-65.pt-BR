---
title: Instalar e configurar os recursos de captura de dados
seo-title: Instalar e configurar os recursos de captura de dados
description: Instale e configure formulários adaptáveis, PDF forms e formulários HTML5. Configure o Adobe Analytics e o Adobe Target para formulários adaptáveis para analisar o uso de formulários e usuários de públicos alvos com base em seus perfis.
seo-description: Instale e configure formulários adaptáveis, PDF forms e formulários HTML5. Configure o Adobe Analytics e o Adobe Target para formulários adaptáveis para analisar o uso de formulários e usuários de públicos alvos com base em seus perfis.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 1%

---


# Instalar e configurar os recursos de captura de dados{#install-and-configure-data-capture-capabilities}

## Introdução {#introduction}

O AEM Forms fornece um conjunto de formulários para obter dados do usuário final: formulários adaptáveis, formulários HTML5 e PDF forms. Ele também fornece ferramentas para lista de todos os formulários disponíveis em uma página da Web, análise do uso de formulários e usuários de públicos alvos com base em seus perfis. Esses recursos estão incluídos no pacote suplementar de AEM Forms. O pacote complementar é implantado em uma instância de autor ou publicação do AEM.

**Formulários adaptativos:** Esses formulários mudam a aparência com base no tamanho da tela do dispositivo, são envolventes e interativos na natureza. Formulários adaptáveis também podem ser integrados com o Adobe Analytics, o Adobe Sign e o Adobe Target. Isso permitiu que você fornecesse formulários personalizados e experiências orientadas a processos para usuários com base em sua demografia e outros recursos. Também é possível integrar formulários adaptáveis ao Adobe Sign.

**PDF forms** são adequados para impressão perfeita em pixels e captura de informações digitais em um documento PDF. No avatar digital, você pode usar o Adobe Acrobat ou o Acrobat Reader para preencher esses formulários. Você pode hospedar esses formulários em seu site ou usar o portal de formulários para lista nesses formulários em um site do AEM. Você também pode enviar esses formulários por email para outras pessoas como anexos. Esses formulários são mais adequados para ambientes de desktop.

**O HTML5 Forms** é a versão compatível com o navegador dos PDF forms. O HTML5 Forms é adequado para ambientes que não suportam plug-ins PDF. O HTML5 Forms permite a renderização de formulários baseados em XFA em dispositivos móveis e navegadores de desktop nos quais o PDF baseado em XFA não é compatível. Esses formulários são mais adequados para tablets e ambientes para desktop.

O AEM Forms é uma plataforma de classe empresarial avançada e a captura de dados (formulários adaptáveis, PDF forms e HTML5 Forms) é apenas uma das capacidades dos AEM Forms. Para obter a lista completa dos recursos, consulte [Introdução aos AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. É necessário apenas uma instância de AEM Author e AEM Publish para executar recursos de captura de dados de AEM Forms. A topologia a seguir é sugerida para executar os recursos de captura de dados do AEM Forms AEM Forms. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar o recurso de captura de dados do AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada do hardware e software suportados, consulte os requisitos [](/help/sites-deploying/technical-requirements.md)técnicos.

* O caminho de instalação da instância do AEM não contém espaços em branco.
* Uma instância do AEM está ativa e em execução. Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de autor ou publicação. Você precisa de pelo menos duas instâncias do [AEM (um Autor e uma Publicação)](/help/sites-deploying/deploy.md) para executar os recursos de captura de dados do AEM Forms:

   * **Autor**: Uma instância do AEM usada para criar, carregar e editar conteúdo e administrar o site. Depois que o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Publicar**: Uma instância do AEM que fornece o conteúdo publicado ao público pela Internet ou por uma rede interna.

* Os requisitos de memória são atendidos. O pacote suplementar de AEM Forms requer:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* A replicação reversa e a replicação para as instâncias de autor e publicação estão definidas. For details, see [Replication](/help/sites-deploying/replication.md).
* Para sistemas baseados em UNIX:

   * Instale os seguintes pacotes de 32 bits da mídia de instalação:

<table>
 <tbody>
  <tr>
   <td>expatriado</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuídio</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Se o OpenSSL já estiver instalado no servidor, atualize-o para a versão mais recente.
>* Crie libcurl.so, libcrypto.so e libssl.so symlinks que apontam para a versão mais recente das bibliotecas libcurl, libcrypto e libssl, respectivamente.

>



* Instale o seguinte pacote de 64 bits da mídia de instalação:

   * libicu

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. O pacote contém a captura de dados de AEM Forms e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Distribuição [de](https://experience.adobe.com/downloads)software aberta. Você precisa de um Adobe ID para fazer login na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]** :
   1. Selecione **[!UICONTROL Formulários]** na lista suspensa **[!UICONTROL Solução]** .
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos]** do EULA e toque em **[!UICONTROL Download]**.
1. Abra o Gerenciador [de](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) pacotes e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Select the package and click **[!UICONTROL Install]**.

   Você também pode baixar o pacote por meio do link direto listado no artigo de versões [de](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEM Forms.
1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não reinicie imediatamente o servidor.** Antes de parar o servidor de AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` arquivo e o log esteja estável.
1. Repita as etapas de 1 a 4 em todas as instâncias de Autor e Publicação.

## Configurações pós-instalação {#post-installation-configurations}

AEM Forms tem algumas configurações obrigatórias e opcionais. As configurações obrigatórias incluem a configuração das bibliotecas BouncyCastle e o agente de serialização. As configurações opcionais incluem configuração de dispatcher, portal de formulários, Adobe Sign, Adobe Analytics e Adobe Target.

### Configurações obrigatórias pós-instalação {#mandatory-post-installation-configurations}

#### Configurar bibliotecas RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para inicializar e delegar as bibliotecas:

1. Pare a instância subjacente do AEM.
1. Open the `[AEM installation directory]\crx-quickstart\conf\sling.properties` file for editing.

   Se você usou `[AEM installation directory]\crx-quickstart\bin\start.bat` para start do AEM, edite sling.properties localizado em `[AEM_root]\crx-quickstart\`.

1. Adicione as seguintes propriedades ao arquivo sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Salve e feche o arquivo e start a instância do AEM.
1. Repita as etapas de 1 a 4 em todas as instâncias de Autor e Publicação.

#### Configurar o agente de serialização {#configure-the-serialization-agent}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para adicionar o pacote à lista de permissões:

1. Abra o AEM Configuration Manager em uma janela do navegador. O URL padrão é `https://'[server]:[port]'/system/console/configMgr`.
1. Procure **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** e abra a configuração.
1. Adicione o pacote **sun.util.calendário** ao campo de **lista de permissões** . Clique em **Salvar**.
1. Repita as etapas de 1 a 3 em todas as instâncias de Autor e Publicação.

### Configurações opcionais pós-instalação {#optional-post-installation-configurations}

#### Configurar Dispatcher {#configure-dispatcher}

A Dispatcher está armazenando em cache e balanceamento de carga em ferramenta para o AEM. O AEM Dispatcher também ajuda a proteger o servidor AEM contra ataques. Você pode aumentar a segurança de sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial. Se você usar o [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), execute as seguintes configurações para AEM Forms:

1. Configurar acesso para AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte a documentação [da](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)Dispatcher.

1. Configure o serviço de filtro de quem indicou:

   Faça logon no gerenciador de configuração Apache Felix como administrador. O URL padrão do gerenciador de configuração é `https://[server]:[port_number]/system/console/configMgr`. No menu **Configurações** , selecione a opção Filtro **** de Quem indicou Apache Sling. No campo Permitir hosts, digite o nome de host do dispatcher para permitir como uma quem indicou e clique em **Salvar**. O formato da entrada é https://[server]:[port].

#### Configurar cache {#configure-cache}

O cache é um mecanismo para reduzir os tempos de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (E/S). O cache de formulários adaptáveis armazena somente o conteúdo HTML e a estrutura JSON de um formulário adaptável sem salvar os dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável.

* Ao usar o cache de formulários adaptáveis, use o [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para armazenar em cache as bibliotecas clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, mantenha o cache de formulários adaptáveis desativado no servidor usado para desenvolvimento.

Execute as seguintes etapas para configurar o cache de formulários adaptáveis:

1. Vá para o gerenciador de configuração do console da Web do AEM em https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Clique em Configuração **de Canal da Web de Formulário** Adaptável e Comunicação Interativa para editar seus valores de configuração. Na caixa de diálogo Editar valores de configuração, especifique o número máximo de formulários ou documentos que uma instância do servidor AEM Forms pode armazenar em cache no campo **Número de formulários** adaptáveis. O valor padrão é 100. Clique em **Salvar**.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Número de formulários adaptáveis como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

#### Configurar a comunicação SSL para o Modelo de dados de formulário {#configure-ssl-communcation-for-form-data-model}

Você pode habilitar a comunicação SSL para o Modelo de dados de formulário. Para ativar a comunicação SSL para o modelo de dados de Formulário, antes de iniciar qualquer instância do AEM Forms, adicione certificados ao Java Trust Store de todas as instâncias. Você pode executar o comando abaixo para adicionar os certificados: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurar o Adobe Sign {#configure-adobe-sign}

O Adobe Sign permite workflows de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os workflows para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras áreas.

Em um cenário típico de formulários adaptáveis e do Adobe Sign, um usuário preenche um formulário adaptável para **solicitar um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviço para que seja tomada uma ação adicional. O Provedor de serviço revisa o aplicativo e usa o Adobe Sign para marcar o aplicativo aprovado. Para ativar workflows semelhantes de assinatura eletrônica, é possível integrar o Adobe Sign a AEM Forms.

Para usar o Adobe Sign com AEM Forms, [integre o Adobe Sign com AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurar o Adobe Analytics {#configure-adobe-analytics}

O AEM Forms integra-se ao Adobe Analytics, que permite capturar e rastrear métricas de desempenho para seus documentos e formulários publicados. O objetivo da análise dessas métricas é tomar decisões informadas com base nos dados sobre as alterações necessárias para tornar os formulários ou o documento mais utilizáveis.

Para usar o Adobe Analytics com AEM Forms, consulte [Configuração de análises e relatórios](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrar Adobe Target {#integrate-adobe-target}

Seus clientes provavelmente abandonarão um formulário se a experiência que ele oferece não for envolvente. Embora seja frustrante para os clientes, também pode aumentar o volume e o custo de suporte para a sua organização. É crítico e desafiador identificar e fornecer a experiência certa do cliente que aumenta a taxa de conversão. Os formulários do AEM têm a chave para esse problema.

Os formulários AEM se integram ao Adobe Target, uma solução Adobe Marketing Cloud, para oferecer experiências personalizadas e envolventes aos clientes em vários canais digitais. Para usar os formulários adaptativos de teste A/B, [integre o Adobe Target com AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Próximos passos {#next-steps}

Você configurou um ambiente para usar os recursos de captura de dados do AEM Forms. Agora, os próximos passos para usar esse recurso são:

* [Criar seu primeiro formulário adaptável](/help/forms/using/create-your-first-adaptive-form.md)
* [Criar seu primeiro formulário PDF](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introdução ao HTML5 Forms](/help/forms/using/introduction.md)

