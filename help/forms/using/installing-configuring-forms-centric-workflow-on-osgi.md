---
title: Instalação e configuração do fluxo de trabalho centrado em formulários no OSGi
seo-title: Instalação e configuração do fluxo de trabalho centrado em formulários no OSGi
description: Instale e configure o AEM Forms Interative Communications para criar correspondências de negócios, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
seo-description: Instale e configure o AEM Forms Interative Communications para criar correspondências de negócios, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: aaedec7314b0fa8551df560eef2574a53c20d1c5
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 2%

---


# Instalação e configuração do fluxo de trabalho centrado em formulários no OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introdução {#introduction}

As empresas coletam e processam dados de vários formulários, sistemas back-end e outras fontes de dados. O processamento de dados envolve procedimentos de revisão e aprovação, tarefas repetitivas e arquivamento de dados. Por exemplo, revisar um formulário e convertê-lo em documento PDF. Quando feitas manualmente, as tarefas repetitivas podem levar muito tempo e recursos.

Você pode usar o fluxo de trabalho centrado em [formulários no OSGi](../../forms/using/aem-forms-workflow.md) para criar rapidamente workflows adaptáveis baseados em formulários. Esses workflows podem ajudá-lo a automatizar workflows de revisão e aprovação, workflows de processos comerciais e outras tarefas repetitivas. Esses workflows também ajudam a processar documentos (criar, montar, distribuir e arquivar documentos PDF, adicionar assinaturas digitais para limitar o acesso a documentos, decodificar formulários com códigos de barras e muito mais) e usar o fluxo de trabalho de assinatura do Adobe Sign com formulários e documentos.

Depois de configurados, esses workflows podem ser acionados manualmente para concluir um processo definido ou executados de forma programática quando os usuários enviam um formulário ou uma comunicação interativa. O recurso está incluído no pacote suplementar de AEM Forms.

O AEM Forms é uma plataforma poderosa de classe empresarial. O fluxo de trabalho centrado em formulários no OSGi é apenas um dos recursos dos AEM Forms. Para obter a lista completa dos recursos, consulte [Introdução aos AEM Forms](introduction-aem-forms.md).

>[!NOTE]
>
>Com o fluxo de trabalho centrado no Forms no OSGi, você pode criar e implantar rapidamente workflows para várias tarefas na pilha OSGi, sem precisar instalar o recurso completo de Gerenciamento de processos na pilha JEE. Veja uma [comparação](capabilities-osgi-jee-workflows.md) dos Workflows AEM centrados no Forms no OSGi e no Process Management no JEE para saber mais sobre as diferenças e similaridades nos recursos.
>
>Após a comparação, se você optar por instalar o recurso Process Management na pilha JEE, consulte [Instalar ou atualizar AEM Forms no JEE](/help/forms/home.md) para obter informações detalhadas sobre a instalação e configuração da pilha JEE e os recursos do Process Management.

## Topologia de implantação {#deployment-topology}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. É necessário apenas um mínimo de um AEM Author ou instância de processamento (autor da produção) para executar o fluxo de trabalho centrado em formulários no recurso OSGi. Uma instância de processamento é uma instância de AEM Author [endurecida](/help/forms/using/hardening-securing-aem-forms-environment.md) . Não execute nenhuma criação real, como criar workflows ou formulários adaptáveis, no autor da produção.

A topologia a seguir indica a topologia para executar AEM Forms Interative Communications, Correspondence Management, captura de dados de AEM Forms e fluxo de trabalho centrado em formulários em recursos OSGi. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

O fluxo de trabalho centrado no Forms do AEM Forms no OSGi executa a Caixa de entrada do AEM e a interface de criação do Modelo de fluxo de trabalho do AEM nas instâncias do autor dos AEM Forms.

## Requisitos do sistema {#system-requirements}

>[!NOTE]
>
>Vá para a seção [Próximas etapas](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) do documento, se você já tiver instalado AEM Forms no OSGi, como explicado no artigo de [instalação e configuração de recursos](../../forms/using/installing-configuring-aem-forms-osgi.md) de captura de dados.

Antes de começar a instalar e configurar o fluxo de trabalho centrado no Forms no OSGi, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada do hardware e software suportados, consulte os requisitos [](/help/sites-deploying/technical-requirements.md)técnicos.

* O caminho de instalação da instância do AEM não contém espaços em branco.
* Uma instância do AEM está ativa e em execução. Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de autor ou publicação. Você precisa de pelo menos uma instância do AEM (Autor ou Processamento) para executar o fluxo de trabalho centrado no Forms no OSGi:

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

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. O pacote contém um fluxo de trabalho centrado no Forms no OSGi e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Faça logon no servidor [](https://localhost:4502) AEM como administrador e abra o compartilhamento [](https://localhost:4502/crx/packageshare)de pacote. Você precisa de um Adobe ID para fazer logon no compartilhamento de pacote.
1. No compartilhamento [de pacote do](https://localhost:4502/crx/packageshare/login.html)AEM, pesquise nos pacotes de complementos do **AEM 6.5** ou nos **service packs** mais recentes, clique no pacote aplicável ao seu sistema operacional e clique em **Download**. Leia e aceite o contrato de licença e clique em **OK**. Os start de download. Após o download, a palavra **Download** é exibida ao lado do pacote.

   Você também pode usar o número da versão para pesquisar um pacote de complementos. Para obter o número da versão do pacote mais recente, consulte o artigo sobre as versões [de](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Depois que o download for concluído, clique em **Download**. Você é redirecionado para o gerenciador de pacotes. No gerenciador de pacotes, pesquise o pacote baixado e clique em **Instalar**.

   Se você baixar manualmente o pacote por meio do link direto listado no artigo de versões [de](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEM Forms, faça logon no gerenciador de pacotes, clique em **Carregar pacote**, selecione o pacote baixado e clique em Fazer upload. Depois que o pacote for carregado, clique no nome do pacote e clique em **Instalar.**

1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não reinicie imediatamente o servidor.** Antes de parar o servidor AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no arquivo [AEM-Installation-Diretory]/crx-quickstart/logs/error.log e o log esteja estável.
1. Repita as etapas de 1 a 4 em todas as instâncias de Autor e Publicação.

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

#### Configurar Dispatcher {#configure-dispatcher}

A Dispatcher está armazenando em cache e balanceamento de carga em ferramenta para o AEM. O AEM Dispatcher também ajuda a proteger o servidor AEM contra ataques. Você pode aumentar a segurança de sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial. Se você usar o [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), execute as seguintes configurações para AEM Forms:

1. Configurar acesso para AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte a documentação [da](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)Dispatcher.

1. Configure o serviço de filtro de quem indicou:

   Faça logon no gerenciador de configuração Apache Felix como administrador. O URL padrão do gerenciador de configuração é https://&#39;server&#39;:[port_number]/system/console/configMgr. No menu **Configurações** , selecione a opção Filtro **** de Quem indicou Apache Sling. No campo Permitir hosts, digite o nome de host do dispatcher para permitir como uma quem indicou e clique em **Salvar**. The format of the entry is `https://'[server]:[port]'`.

#### Configurar cache {#configure-cache}

O cache é um mecanismo para reduzir os tempos de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (E/S). O cache de formulários adaptáveis armazena somente o conteúdo HTML e a estrutura JSON de um formulário adaptável sem salvar os dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável.

* Ao usar o cache de formulários adaptáveis, use o [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para armazenar em cache as bibliotecas clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, mantenha o cache de formulários adaptáveis desativado no servidor usado para desenvolvimento.

Execute as seguintes etapas para configurar o cache de formulários adaptáveis:

1. Vá para o gerenciador de configuração do console da Web do AEM em `https://'[server]:[port]'/system/console/configMgr`.
1. Clique em Serviço **** de configuração de formulário adaptável para editar seus valores de configuração. Na caixa de diálogo Editar valores de configuração, especifique o número máximo de formulários ou documentos que uma instância do servidor AEM Forms pode armazenar em cache no campo **Número de formulários** adaptáveis. O valor padrão é 100. Clique em **Salvar**.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Número de formulários adaptáveis como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

#### Configurar o Adobe Sign {#configure-adobe-sign}

O Adobe Sign permite workflows de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os workflows para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras áreas.

Em um fluxo de trabalho típico centrado no Adobe Sign e no Forms no cenário OSGi, um usuário preenche um formulário adaptável para **solicitar um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário do aplicativo, um fluxo de trabalho de aprovação/rejeição é iniciado. O provedor de serviço revisa o aplicativo na Caixa de entrada do AEM e usa o Adobe Sign para assinar eletronicamente o aplicativo. Para ativar workflows semelhantes de assinatura eletrônica, é possível integrar o Adobe Sign a AEM Forms.

Para usar o Adobe Sign com AEM Forms, [integre o Adobe Sign com AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Próximos passos {#next-steps}

Você configurou um ambiente para usar o fluxo de trabalho centrado no Forms em recursos OSGi. Agora, as etapas para usar esse recurso são:

* [Uso de fluxo de trabalho centrado em formulários no OSGi](../../forms/using/aem-forms-workflow.md)
* [Referência da Etapa do Fluxo de Trabalho](/help/sites-developing/workflows-step-ref.md)
* [Pós-processamento de cartas e comunicações interativas](../../forms/using/submit-letter-topostprocess.md)

