---
title: Instalar e configurar recursos de captura de dados
description: Instale e configure formulários adaptáveis, PDF forms e HTML5 Forms. Configure o Adobe Analytics e o Adobe Target para formulários adaptáveis para analisar o uso de formulários e direcionar usuários com base em seus perfis.
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin, User, Developer
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, OSGI
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 1%

---

# Instalar e configurar recursos de captura de dados{#install-and-configure-data-capture-capabilities}

## Introdução {#introduction}

O AEM Forms fornece um conjunto de formulários para obter dados do usuário final: formulários adaptáveis, HTML5 Forms e PDF forms. Ele também fornece ferramentas para listar todos os formulários disponíveis em uma página da Web, analisar o uso de formulários e direcionar usuários com base em seus perfis. Esses recursos estão incluídos no pacote complementar do AEM Forms. O pacote complementar é implantado em uma instância de Autor ou Publish do AEM.

**Formulários adaptáveis:** Esses formulários alteram a aparência com base no tamanho da tela do dispositivo, são envolventes e interativos por natureza. O Forms adaptável também pode se integrar ao Adobe Analytics, Adobe Sign e Adobe Target. Ela possibilitou fornecer formulários personalizados e experiências orientadas por processos aos usuários com base em sua demografia e outros recursos. Também é possível integrar formulários adaptáveis ao Adobe Sign.

**PDF forms** são adequados para impressão em pixel perfeito e captura de informações digitais em um documento PDF. No avatar digital, você pode usar o Adobe Acrobat ou o Acrobat Reader para preencher esses formulários. Você pode hospedar esses formulários em seu site ou usar o portal de formulários para listar esses formulários em um site de AEM. Também é possível enviar esses formulários por email para outras pessoas como anexos. Esses formulários são mais adequados para ambientes de desktop.

**HTML5 FORMS** são a versão compatível com o navegador do PDF forms. O HTML5 Forms é adequado para ambientes que não oferecem suporte a plug-ins de PDF. O HTML5 Forms permite a renderização de formulários baseados em XFA em dispositivos móveis e navegadores de desktop nos quais o PDF baseado em XFA não é compatível. Esses formulários são mais adequados para tablets e ambientes de desktop.

O AEM Forms é uma plataforma poderosa de nível empresarial e a captura de dados (formulários adaptáveis, PDF forms e HTML5 Forms) é apenas um dos recursos do AEM Forms. Para obter a lista completa dos recursos, consulte [Introdução ao AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. Você precisa de, no mínimo, um Autor de AEM e uma instância AEM do Publish para executar os recursos de captura de dados do AEM Forms. Sugere-se a seguinte topologia para executar os recursos de captura de dados do AEM Forms AEM Forms. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação do AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar o recurso de captura de dados do AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada de hardware e software compatíveis, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* O caminho de instalação da instância do AEM não contém espaços em branco.
* Uma instância do AEM está em funcionamento. Para usuários do Windows, instale a instância AEM no modo elevado. Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de criação ou publicação. Você precisa de, pelo menos, dois [Instâncias do AEM (um autor e um Publish)](/help/sites-deploying/deploy.md) para executar os recursos de captura de dados do AEM Forms:

   * **Autor**: uma instância do AEM usada para criar, carregar e editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Publish**: uma instância do AEM que veicula o conteúdo publicado para o público pela Internet ou por uma rede interna.

* Os requisitos de memória são atendidos. O pacote complementar do AEM Forms exige:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* A replicação e a replicação inversa das instâncias de autor e publicação estão definidas. Para obter detalhes, consulte [Replicação](/help/sites-deploying/replication.md).
* Para sistemas baseados em UNIX:

   * Instale os seguintes pacotes de 32 bits da mídia de instalação:

<table>
 <tbody>
  <tr>
   <td>expat</td>
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
   <td>nss-softoken-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Se o OpenSSL já estiver instalado no servidor, atualize-o para a versão mais recente.
>* Crie os symlinks libcurl.so, libcrypto.so e libssl.so apontando para a versão mais recente das bibliotecas libcurl, libcrypto e libssl, respectivamente.
>

* Instale o seguinte pacote de 64 bits a partir da mídia de instalação:

   * libicu

* Instalar [Microsoft Visual Studio 2019 de 32 bits Redistribuível](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).


## Instalar pacote complementar do AEM Forms {#install-aem-forms-add-on-package}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. O pacote contém a captura de dados do AEM Forms e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecionar **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional e **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abertura [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e clique em **[!UICONTROL Fazer upload do pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

   Também é possível baixar o pacote por meio do link direto listado no [Versões do AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) artigo.
1. Após a instalação do pacote, você será solicitado a reiniciar a instância do AEM. **Não reinicie o servidor imediatamente.** Antes de interromper o servidor do AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` e o log é estável.

   >[!NOTE]
   >
   > É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

1. Repita as etapas 1 a 7 em todas as instâncias de Autor e Publish.

### (Somente para Windows) Instalação automática de redistribuíveis do Visual Studio {#automatic-installation-visual-studio-redistributables}

Se você instalar uma instância AEM no modo elevado, os redistribuíveis do Visual Studio de 32 bits serão instalados automaticamente durante a instalação do pacote complementar do AEM Forms.

Para avaliar se os redistribuíveis do Visual Studio são instalados automaticamente, abra o `error.log` arquivo disponível no `/crx-repository/logs/` diretório. Os logs incluem a seguinte mensagem:

`Redist <service name> already installed on system, will not attempt re-installation`

Se os redistribuíveis não forem instalados, os registros incluirão a seguinte mensagem:

`Current user does not have elevated privileges, aborting installation of redist <service name>`

Para resolver o problema, reinicie o servidor AEM, instale o AEM no modo elevado e instale o pacote complementar do AEM Forms.

Se a verificação de privilégio falhar, os logs incluirão a seguinte mensagem:

`Privilege escalation check failed with error: <error message>`

## Configurações pós-instalação {#post-installation-configurations}

O AEM Forms tem algumas configurações obrigatórias e opcionais. As configurações obrigatórias incluem a configuração de bibliotecas BouncyCastle e o agente de serialização. As configurações opcionais incluem a configuração do Dispatcher, do portal do Forms, do Adobe Sign, do Adobe Analytics e do Adobe Target.

### Configurações obrigatórias pós-instalação {#mandatory-post-installation-configurations}

#### Configurar bibliotecas RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Execute as seguintes etapas em todas as instâncias do Autor e do Publish para inicializar e delegar as bibliotecas:

1. Interrompa a instância subjacente do AEM.
1. Abra o `[AEM installation directory]\crx-quickstart\conf\sling.properties` arquivo para edição.

   Se você usou `[AEM installation directory]\crx-quickstart\bin\start.bat` para iniciar o AEM, edite o sling.properties localizado em `[AEM_root]\crx-quickstart\`.

1. Adicione as seguintes propriedades ao arquivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salve e feche o arquivo e inicie a instância do AEM.
1. Repita as etapas 1 a 4 em todas as instâncias de Autor e Publish.

#### Configurar o agente de serialização {#configure-the-serialization-agent}

Execute as seguintes etapas em todas as instâncias Autor e Publicar para adicionar o pacote ao arquivo de inclui na lista de permissões:

1. Abra o Gerenciador de configuração do AEM em uma janela do navegador. O URL padrão é `https://'[server]:[port]'/system/console/configMgr`.
1. Pesquisar por **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** e abra a configuração.
1. Adicione o **sun.util.calendar** pacote para o **➡ incluir na lista de permissões** campo. Clique em **Salvar**.
1. Repita as etapas 1 a 3 em todas as instâncias de Autor e Publish.

### Configurações pós-instalação opcionais {#optional-post-installation-configurations}

#### Configurar o Dispatcher {#configure-dispatcher}

O Dispatcher é uma ferramenta de armazenamento em cache e/ou balanceamento de carga do Adobe Experience Manager que pode ser usada em conjunto com um servidor Web de classe empresarial. Se você usar [Dispatcher](https://helpx.adobe.com/pt/experience-manager/dispatcher/using/dispatcher-configuration.html), em seguida, execute as seguintes configurações para o AEM Forms:

1. Configure o acesso para o AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte [Documentação do Dispatcher](https://helpx.adobe.com/pt/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure o serviço de filtro referenciador:

   Faça logon no gerenciador de configurações Apache Felix como administrador. O URL padrão do gerenciador de configurações é `https://[server]:[port_number]/system/console/configMgr`. No **Configurações** selecione o **Filtro referenciador do Apache Sling** opção. No campo Permitir hosts, digite o nome do host do dispatcher para permitir como um referenciador e clique em **Salvar**. O formato da entrada é `https://[server]:[port]`.

#### Configurar cache {#configure-cache}

O cache é um mecanismo para reduzir os tempos de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (E/S). O cache de formulários adaptáveis armazena somente o conteúdo em HTML e a estrutura JSON de um formulário adaptável sem salvar os dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável.

* Ao usar o cache de formulários adaptáveis, use o [Dispatcher AEM](https://helpx.adobe.com/pt/experience-manager/dispatcher/using/dispatcher-configuration.html) para armazenar em cache bibliotecas de clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, mantenha o cache de formulários adaptáveis desativado no servidor usado para desenvolvimento.

Execute as seguintes etapas para configurar o cache de formulários adaptáveis:

1. Acesse o gerenciador de configuração do console da Web do AEM em https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Clique em **Configuração do canal da Web do formulário adaptável e da comunicação interativa** para editar os valores de configuração. Na caixa de diálogo Editar valores de configuração, especifique o número máximo de formulários ou documentos que uma instância do servidor do AEM Forms pode armazenar em cache na **Número de Forms adaptáveis** campo. O valor padrão é 100. Clique em **Salvar**.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Número de Forms adaptáveis como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

#### Configurar comunicação SSL para modelo de dados de formulário {#configure-ssl-communcation-for-form-data-model}

Você pode ativar a comunicação SSL para o Modelo de dados de formulário. Para habilitar a comunicação SSL para o modelo de dados de formulário, antes de iniciar qualquer instância do AEM Forms, adicione certificados ao Java Trust Store de todas as instâncias. Você pode executar o comando abaixo para adicionar os certificados: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurar Adobe Sign {#configure-adobe-sign}

O Adobe Sign habilita fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.

Em um cenário típico de Adobe Sign e formulários adaptáveis, um usuário preenche um formulário adaptável para **solicitar um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que seja tomada uma nova ação. O provedor de serviços analisa o aplicativo e usa o Adobe Sign para marcar o aplicativo como aprovado. Para habilitar fluxos de trabalho de assinatura eletrônica semelhantes, é possível integrar o Adobe Sign com o AEM Forms.

Para usar o Adobe Sign com o AEM Forms, [Integrar o Adobe Sign com o AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurar Adobe Analytics {#configure-adobe-analytics}

O AEM Forms integra-se ao Adobe Analytics, o que permite capturar e rastrear as métricas de desempenho dos formulários e documentos publicados. O objetivo por trás da análise dessas métricas é tomar decisões informadas com base em dados sobre as alterações necessárias para tornar os formulários ou documentos mais utilizáveis.

Para usar o Adobe Analytics com o AEM Forms, consulte [Configuração de análises e relatórios](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrar o Adobe Target {#integrate-adobe-target}

Seus clientes provavelmente abandonarão um formulário se a experiência que ele oferece não for cativante. Embora seja frustrante para os clientes, também pode aumentar o volume de suporte e o custo para a sua organização. É crítico e desafiador identificar e fornecer a experiência certa ao cliente que aumente a taxa de conversão. A AEM Forms é a chave para esse problema.

O AEM forms é integrado ao Adobe Target, uma solução da Adobe Marketing Cloud, para fornecer experiências personalizadas e envolventes ao cliente em vários canais digitais. Para usar o Adobe Target para testar formulários adaptáveis, [Integrar o Adobe Target com o AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Próximas etapas {#next-steps}

Você configurou um ambiente para usar os recursos de captura de dados do AEM Forms. Agora, as próximas etapas para usar o recurso são:

* [Criar o primeiro formulário adaptável](/help/forms/using/create-your-first-adaptive-form.md)
* [Criar o primeiro formulário de PDF](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introdução ao HTML5 Forms](/help/forms/using/introduction.md)
