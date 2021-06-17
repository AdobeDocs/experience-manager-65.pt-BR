---
title: Instalar e configurar recursos de captura de dados
seo-title: Instalar e configurar recursos de captura de dados
description: Instale e configure formulários adaptáveis, PDF forms e HTML5 Forms. Configure o Adobe Analytics e o Adobe Target para formulários adaptáveis para analisar o uso de formulários e direcionar usuários com base em seus perfis.
seo-description: Instale e configure formulários adaptáveis, PDF forms e HTML5 Forms. Configure o Adobe Analytics e o Adobe Target para formulários adaptáveis para analisar o uso de formulários e direcionar usuários com base em seus perfis.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Administrator
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 4%

---

# Instalar e configurar recursos de captura de dados{#install-and-configure-data-capture-capabilities}

## Introdução {#introduction}

O AEM Forms fornece um conjunto de formulários para obter dados do usuário final: formulários adaptáveis, HTML5 Forms e PDF forms. Também fornece ferramentas para listar todos os formulários disponíveis em uma página da Web, analisar o uso de formulários e direcionar usuários com base em seu perfil. Esses recursos estão incluídos no pacote complementar do AEM Forms. O pacote complementar é implantado em uma instância de Autor ou Publicação do AEM.

**Formulários adaptáveis:** esses formulários mudam de aparência com base no tamanho da tela do dispositivo, são envolventes e interativos na natureza. O Adaptive Forms também pode se integrar ao Adobe Analytics, Adobe Sign e Adobe Target. Ele permitiu que você entregasse formulários personalizados e experiências orientadas a processos aos usuários com base em sua demografia e outros recursos. Também é possível integrar formulários adaptáveis ao Adobe Sign.

**Os** formulários PDF são adequados para impressão perfeita em pixels e captura de informações digitais em um documento PDF. No avatar digital, você pode usar Adobe Acrobat ou Acrobat Reader para preencher esses formulários. Você pode hospedar esses formulários em seu site ou usar o portal de formulários para listá-los em um site AEM. Também é possível enviar esses formulários por email para outras pessoas como anexos. Esses formulários são mais adequados para ambientes de desktop.

**Os** formulários HTML5 são a versão compatível com o navegador do PDF forms. O HTML5 Forms é adequado para ambientes que não suportam plug-ins PDF. O HTML5 Forms permite a renderização de formulários baseados em XFA em dispositivos móveis e navegadores de desktop nos quais o PDF baseado em XFA não é suportado. Esses formulários são mais adequados para ambientes de tablets e desktop.

O AEM Forms é uma plataforma avançada de nível empresarial e a captura de dados (formulários adaptáveis, PDF forms e Forms HTML5) é apenas um dos recursos do AEM Forms. Para obter a lista completa de recursos, consulte [Introdução ao AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote do complemento AEM Forms é um aplicativo implantado em AEM. Você precisa de apenas um mínimo de uma instância de AEM Author e AEM Publish para executar recursos de captura de dados do AEM Forms. A topologia a seguir é sugerida para executar os recursos de captura de dados do AEM Forms AEM Forms. Para obter informações detalhadas sobre a topologia, consulte [Topologias de arquitetura e implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar o recurso de captura de dados do AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada de hardware e software suportados, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* O caminho de instalação da instância de AEM não contém espaços em branco.
* Uma instância de AEM está em execução. Para usuários do Windows, instale a instância de AEM no modo elevado. Na terminologia AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de criação ou publicação. Você precisa de pelo menos duas [instâncias AEM (um Autor e uma Publicação)](/help/sites-deploying/deploy.md) para executar os recursos de captura de dados do AEM Forms:

   * **Autor**: Uma instância AEM usada para criar, carregar e editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Publicar**: Uma instância de AEM que disponibiliza o conteúdo publicado ao público pela Internet ou por uma rede interna.

* Os requisitos de memória são cumpridos. O pacote do complemento AEM Forms requer:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* A replicação e a replicação inversa das instâncias de autor e publicação estão definidas. Para obter detalhes, consulte [Replicação](/help/sites-deploying/replication.md).
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
   <td>libuuid</td>
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
>* Crie links simbólicos libcurl.so, libcrypto.so e libssl.so apontando para a versão mais recente das bibliotecas libcurl, libcrypto e libssl, respectivamente.

>



* Instale o seguinte pacote de 64 bits a partir da mídia de instalação:

   * libicu

## Instale o pacote complementar do AEM Forms {#install-aem-forms-add-on-package}

O pacote do complemento AEM Forms é um aplicativo implantado em AEM. O pacote contém a captura de dados do AEM Forms e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Clique em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]**:
   1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solução]**.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar Termos do EULA]** e toque em **[!UICONTROL Download]**.
1. Abra [Gerenciador de pacotes](https://docs.adobe.com/content/help/br/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

   Você também pode baixar o pacote por meio do link direto listado no artigo [AEM Forms releases](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html).
1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não reinicie imediatamente o servidor.** Antes de parar o servidor do AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no  `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` arquivo e o log seja estável.
1. Repita as etapas de 1 a 7 em todas as instâncias de Autor e Publicação.

### (Somente Windows) Instalação automática do Visual Studio redistribuíveis {#automatic-installation-visual-studio-redistributables}

Se você instalar uma instância de AEM no modo elevado, as redistribuíveis do Visual Studio ausentes serão instaladas automaticamente durante a instalação do pacote do complemento AEM Forms.

Para avaliar se as redistribuíveis do Visual Studio são instaladas automaticamente, abra o arquivo `error.log` disponível no diretório `/crx-repository/logs/`. Os logs incluem a seguinte mensagem:

`Redist <service name> already installed on system, will not attempt re-installation`

Se as redistribuíveis não forem instaladas, os logs incluirão a seguinte mensagem:

`Current user does not have elevated privileges, aborting installation of redist <service name>`

Para resolver o problema, reinicie o servidor AEM, instale o AEM no modo elevado e instale o pacote do complemento AEM Forms.

Se a verificação de privilégio falhar, os logs incluirão a seguinte mensagem:

`Privilege escalation check failed with error: <error message>`

## Configurações pós-instalação {#post-installation-configurations}

O AEM Forms tem algumas configurações obrigatórias e opcionais. As configurações obrigatórias incluem a configuração de bibliotecas BouncyCastle e o agente de serialização. As configurações opcionais incluem a configuração do dispatcher, do portal do Forms, do Adobe Sign, do Adobe Analytics e do Adobe Target.

### Configurações obrigatórias pós-instalação {#mandatory-post-installation-configurations}

#### Configurar bibliotecas RSA e BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para inicializar e delegar as bibliotecas:

1. Pare a instância AEM subjacente.
1. Abra o arquivo `[AEM installation directory]\crx-quickstart\conf\sling.properties` para edição.

   Se você usou `[AEM installation directory]\crx-quickstart\bin\start.bat` para iniciar o AEM, edite o sling.properties localizado em `[AEM_root]\crx-quickstart\`.

1. Adicione as seguintes propriedades ao arquivo sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salve e feche o arquivo e inicie a instância de AEM.
1. Repita as etapas 1 a 4 em todas as instâncias de Autor e Publicação.

#### Configurar o agente de serialização {#configure-the-serialization-agent}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para adicionar o pacote à  de lista de permissões:

1. Abra AEM Configuration Manager em uma janela do navegador. O URL padrão é `https://'[server]:[port]'/system/console/configMgr`.
1. Procure por **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** e abra a configuração.
1. Adicione o pacote **sun.util.calendar** ao campo **lista de permissões**. Clique em **Salvar**.
1. Repita as etapas 1 a 3 em todas as instâncias de Autor e Publicação.

### Configurações opcionais pós-instalação {#optional-post-installation-configurations}

#### Configurar o Dispatcher {#configure-dispatcher}

O Dispatcher é uma ferramenta de balanceamento de carga e/ou cache de Adobe Experience Manager da que pode ser usada em conjunto com um servidor da Web de classe empresarial. Se você usar [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), execute as seguintes configurações para o AEM Forms:

1. Configuração do acesso para AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte a [documentação do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure o serviço de filtro do referenciador:

   Faça logon no gerenciador de configuração do Apache Felix como administrador. O URL padrão do gerenciador de configuração é `https://[server]:[port_number]/system/console/configMgr`. No menu **Configurations**, selecione a opção **Apache Sling Referrer Filter**. No campo Permitir hosts , insira o nome do host do dispatcher para permitir como referenciador e clique em **Salvar**. O formato da entrada é `https://[server]:[port]`.

#### Configurar Cache {#configure-cache}

O armazenamento em cache é um mecanismo para reduzir o tempo de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (I/O). O cache de formulários adaptáveis armazena somente o conteúdo HTML e a estrutura JSON de um formulário adaptável sem salvar dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável.

* Ao usar o cache de formulários adaptáveis, use o [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para armazenar em cache as bibliotecas de clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, mantenha o cache de formulários adaptáveis desativado no servidor usado para desenvolvimento.

Execute as seguintes etapas para configurar o cache de formulários adaptáveis:

1. Vá para AEM gerenciador de configuração do console da Web em https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Clique em **Adaptive Form e Interative Communication Web Channel Configuration** para editar seus valores de configuração. Na caixa de diálogo editar valores de configuração, especifique o número máximo de formulários ou documentos que uma instância do servidor do AEM Forms pode armazenar em cache no campo **Number of Adaptive Forms**. O valor padrão é 100. Clique em **Salvar**.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Number of Adaptive Forms como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

#### Configurar a comunicação SSL para o Modelo de dados de formulário {#configure-ssl-communcation-for-form-data-model}

Você pode ativar a comunicação SSL para o Modelo de dados de formulário. Para habilitar a comunicação SSL para o modelo de dados de Formulário, antes de iniciar qualquer instância do AEM Forms, adicione certificados ao Java Trust Store de todas as instâncias. Você pode executar o comando abaixo para adicionar os certificados: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurar o Adobe Sign {#configure-adobe-sign}

O Adobe Sign habilita fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras.

Em um cenário típico de Adobe Sign e formulários adaptáveis, um usuário preenche um formulário adaptável para **se aplicar a um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que você possa realizar mais ações. O provedor de serviços revisa o aplicativo e usa o Adobe Sign para marcar o aplicativo aprovado. Para ativar fluxos de trabalho de assinatura eletrônica semelhantes, você pode integrar o Adobe Sign com o AEM Forms.

Para usar o Adobe Sign com AEM Forms, [Integre o Adobe Sign com AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurar o Adobe Analytics {#configure-adobe-analytics}

O AEM Forms integra-se ao Adobe Analytics, que permite capturar e rastrear métricas de desempenho para seus formulários e documentos publicados. O objetivo por trás da análise dessas métricas é tomar decisões informadas com base em dados sobre as alterações necessárias para tornar os formulários ou documentos mais utilizáveis.

Para usar o Adobe Analytics com AEM Forms, consulte [Configuração de análises e relatórios](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrar Adobe Target {#integrate-adobe-target}

Seus clientes provavelmente abandonarão um formulário se a experiência que ele oferece não for envolvente. Embora seja frustrante para os clientes, também é possível aumentar o volume e o custo de suporte para sua organização. É importante e desafiador identificar e fornecer a experiência correta do cliente que aumenta a taxa de conversão. O AEM forms tem a chave para esse problema.

AEM formulários é integrado ao Adobe Target, uma solução da Adobe Marketing Cloud, para fornecer experiências personalizadas e envolventes para o cliente em vários canais digitais. Para usar o Adobe Target para testar formulários adaptáveis A/B, [Integre o Adobe Target com o AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Próximas etapas {#next-steps}

Você configurou um ambiente para usar os recursos de captura de dados do AEM Forms. Agora, os próximos passos para usar o recurso são:

* [Criar o primeiro formulário adaptável](/help/forms/using/create-your-first-adaptive-form.md)
* [Criar seu primeiro formulário PDF](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introdução ao HTML5 Forms](/help/forms/using/introduction.md)
