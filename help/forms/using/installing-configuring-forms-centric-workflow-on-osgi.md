---
title: Instalação e configuração do fluxo de trabalho centrado na Forms no OSGi
seo-title: Instalação e configuração do fluxo de trabalho centrado na Forms no OSGi
description: Instale e configure o AEM Forms Interative Communications para criar correspondências de negócios, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
seo-description: Instale e configure o AEM Forms Interative Communications para criar correspondências de negócios, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 2%

---


# Instalação e configuração do fluxo de trabalho centrado na Forms no OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introdução {#introduction}

As empresas coletam e processam dados de vários formulários, sistemas back-end e outras fontes de dados. O processamento de dados envolve procedimentos de revisão e aprovação, tarefas repetitivas e arquivamento de dados. Por exemplo, revisar um formulário e convertê-lo em documento PDF. Quando feitas manualmente, as tarefas repetitivas podem levar muito tempo e recursos.

Você pode usar [fluxo de trabalho centrado na Forms no OSGi](../../forms/using/aem-forms-workflow.md) para criar rapidamente workflows adaptáveis baseados em formulários. Esses workflows podem ajudá-lo a automatizar workflows de revisão e aprovação, workflows de processos comerciais e outras tarefas repetitivas. Esses workflows também ajudam a processar documentos (criar, montar, distribuir e arquivar documentos PDF, adicionar assinaturas digitais para limitar o acesso a documentos, decodificar formulários com códigos de barras e muito mais) e usar o fluxo de trabalho de assinatura Adobe Sign com formulários e documentos.

Depois de configurados, esses workflows podem ser acionados manualmente para concluir um processo definido ou executados de forma programática quando os usuários enviam um formulário ou uma comunicação interativa. O recurso está incluído no pacote complementar AEM Forms.

A AEM Forms é uma poderosa plataforma de classe empresarial. O fluxo de trabalho centrado na Forms no OSGi é apenas um dos recursos do AEM Forms. Para obter a lista completa dos recursos, consulte [Introdução ao AEM Forms](introduction-aem-forms.md).

>[!NOTE]
>
>Com o fluxo de trabalho centrado na Forms no OSGi, você pode criar e implantar rapidamente workflows para várias tarefas na pilha OSGi, sem precisar instalar o recurso completo de Gerenciamento de processos na pilha JEE. Consulte uma [comparação](capabilities-osgi-jee-workflows.md) dos Workflows de AEM centrados na Forms no OSGi e no Process Management no JEE para saber mais sobre as diferenças e similaridades nos recursos.
>
>Após a comparação, se você optar por instalar o recurso Process Management na pilha JEE, consulte [Instalar ou atualizar o AEM Forms no JEE](/help/forms/home.md) para obter informações detalhadas sobre como instalar e configurar a pilha JEE e os recursos do Process Management.

## Topologia de implantação {#deployment-topology}

O pacote complementar AEM Forms é um aplicativo implantado no AEM. É necessário apenas um mínimo de uma instância de autor ou processamento de AEM (autor da produção) para executar o fluxo de trabalho centrado na Forms no recurso OSGi. Uma instância de processamento é uma instância [endurecida do autor de AEM](/help/forms/using/hardening-securing-aem-forms-environment.md). Não execute nenhuma criação real, como criar workflows ou formulários adaptáveis, no autor da produção.

A topologia a seguir indica a topologia para executar o AEM Forms Interative Communications, o Gerenciamento de Correspondência, a captura de dados da AEM Forms e o fluxo de trabalho centralizado na Forms em recursos OSGi. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia recomendada](assets/recommended-topology.png)

O fluxo de trabalho centrado no AEM Forms Forms no OSGi executa AEM Caixa de entrada e AEM interface de criação do modelo de fluxo de trabalho nas instâncias de autor do AEM Forms.

## Requisitos do sistema {#system-requirements}

>[!NOTE]
>
>Vá para a seção [Próximas etapas](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) do documento, se você já instalou o AEM Forms no OSGi, conforme explicado no artigo [instalar e configurar recursos de captura de dados](../../forms/using/installing-configuring-aem-forms-osgi.md).

Antes de começar a instalar e configurar o fluxo de trabalho centrado na Forms no OSGi, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada do hardware e software suportados, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* O caminho de instalação da instância AEM não contém espaços em branco.
* Uma instância AEM está ativa e em execução. Na terminologia AEM, uma &quot;instância&quot; é uma cópia da AEM em execução em um servidor no modo de autor ou publicação. Você precisa de pelo menos uma instância AEM (Autor ou Processamento) para executar o fluxo de trabalho centralizado no Forms no OSGi:

   * **Autor**: Uma instância AEM usada para criar, carregar e editar conteúdo e administrar o site. Depois que o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Processamento:** uma instância de processamento é uma instância  [endurecida AEM ](/help/forms/using/hardening-securing-aem-forms-environment.md) Authorinstance. Você pode configurar uma instância de Autor e endurecê-la depois de executar a instalação.

   * **Publicar**: Uma instância AEM que serve o conteúdo publicado ao público pela Internet ou por uma rede interna.

* Os requisitos de memória são atendidos. O pacote suplementar AEM Forms requer:

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

## Instalar o pacote de complementos do AEM Forms {#install-aem-forms-add-on-package}

O pacote complementar AEM Forms é um aplicativo implantado no AEM. O pacote contém um fluxo de trabalho centrado na Forms no OSGi e outros recursos. Execute as seguintes etapas para instalar o pacote complementar:

1. Abra [Distribuição de software](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]**:
   1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solution]**.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Download]**.
1. Abra [Gerenciador de pacotes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

   Você também pode baixar o pacote por meio do link direto listado no artigo [Versões da AEM Forms](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html).

1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância AEM. **Não reinicie imediatamente o servidor.** Antes de parar o servidor AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no arquivo  [AEM-Installation-Diretory]/crx-quickstart/logs/error.log e o log esteja estável.
1. Repita as etapas de 1 a 7 em todas as instâncias de Autor e Publicação.

## Configurações pós-instalação {#post-installation-configurations}

A AEM Forms tem algumas configurações obrigatórias e opcionais. As configurações obrigatórias incluem a configuração das bibliotecas BouncyCastle e o agente de serialização. As configurações opcionais incluem a configuração do dispatcher e do Adobe Target.

### Configurações obrigatórias pós-instalação {#mandatory-post-installation-configurations}

#### Configurar bibliotecas RSA e BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para inicializar e delegar as bibliotecas:

1. Pare a instância AEM subjacente.
1. Abra o arquivo [AEM de instalação]\crx-quickstart\conf\sling.properties para edição.

   Se você usou [AEM diretório de instalação]\crx-quickstart\bin\start.bat para AEM de start, edite sling.properties localizado em [AEM_root]\crx-quickstart\.

1. Adicione as seguintes propriedades ao arquivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salve e feche o arquivo e start a instância AEM.
1. Repita as etapas de 1 a 4 em todas as instâncias de Autor e Publicação.

#### Configurar o agente de serialização {#configure-the-serialization-agent}

Execute as seguintes etapas em todas as instâncias de Autor e Publicação para adicionar o pacote à lista de permissões:

1. Abra AEM Configuration Manager em uma janela do navegador. O URL padrão é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Procure e abra **Configuração do Firewall de Deserialização**.
1. Adicione o pacote **sun.util.calendário** ao campo **lista de permissões**. Clique em Salvar.
1. Repita as etapas de 1 a 3 em todas as instâncias de Autor e Publicação.

### Configurações opcionais pós-instalação {#optional-post-installation-configurations}

#### Configurar o Dispatcher {#configure-dispatcher}

O Dispatcher está em cache e na ferramenta de balanceamento de carga para AEM. AEM O Dispatcher também ajuda a proteger AEM servidor contra ataques. Você pode aumentar a segurança da sua instância de AEM usando o Dispatcher em conjunto com um servidor Web de classe empresarial. Se você usar [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), execute as seguintes configurações para AEM Forms:

1. Configurar acesso para AEM Forms:

   Abra o arquivo dispatcher.any para edição. Navegue até a seção de filtro e adicione o seguinte filtro à seção de filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salve e feche o arquivo. Para obter informações detalhadas sobre filtros, consulte [Documentação do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure o serviço de filtro de quem indicou:

   Faça logon no gerenciador de configuração Apache Felix como administrador. O URL padrão do gerenciador de configuração é https://&#39;server&#39;:[port_number]/system/console/configMgr. No menu **Configurações**, selecione a opção **Filtro de Quem indicou Apache Sling**. No campo Permitir hosts, digite o nome de host do dispatcher para permitir como uma quem indicou e clique em **Salvar**. O formato da entrada é `https://'[server]:[port]'`.

#### Configurar cache {#configure-cache}

O cache é um mecanismo para reduzir os tempos de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (E/S). O cache de formulários adaptáveis armazena somente o conteúdo HTML e a estrutura JSON de um formulário adaptável sem salvar os dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável.

* Ao usar o cache de formulários adaptáveis, use o [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para armazenar em cache as bibliotecas de clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, mantenha o cache de formulários adaptáveis desativado no servidor usado para desenvolvimento.

Execute as seguintes etapas para configurar o cache de formulários adaptáveis:

1. Vá para AEM gerenciador de configuração do console da Web em `https://'[server]:[port]'/system/console/configMgr`.
1. Clique em **Adaptive Form Configuration Service** para editar os valores de configuração. Na caixa de diálogo editar valores de configuração, especifique o número máximo de formulários ou documentos que uma instância do servidor AEM Forms pode armazenar em cache no campo **Número de adaptáveis Forms**. O valor padrão é 100. Clique em **Salvar**.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Número de adaptáveis Forms como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

#### Configurar Adobe Sign {#configure-adobe-sign}

A Adobe Sign habilita workflows de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os workflows para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras áreas.

Em um fluxo de trabalho comum centrado no Adobe Sign e no Forms no cenário OSGi, um usuário preenche um formulário adaptável para **se aplicar a um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário do aplicativo, um fluxo de trabalho de aprovação/rejeição é iniciado. O provedor de serviço revisa o aplicativo AEM Caixa de entrada e usa a Adobe Sign para assinar eletronicamente o aplicativo. Para habilitar workflows semelhantes de assinatura eletrônica, é possível integrar o Adobe Sign ao AEM Forms.

Para usar o Adobe Sign com o AEM Forms, [Integre o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Próximas etapas {#next-steps}

Você configurou um ambiente para usar o fluxo de trabalho centralizado no Forms em recursos OSGi. Agora, as etapas para usar esse recurso são:

* [Usar o fluxo de trabalho centrado na Forms no OSGi](../../forms/using/aem-forms-workflow.md)
* [Referência da Etapa do Fluxo de Trabalho](/help/sites-developing/workflows-step-ref.md)
* [Pós-processamento de cartas e comunicações interativas](../../forms/using/submit-letter-topostprocess.md)

