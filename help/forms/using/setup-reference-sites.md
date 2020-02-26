---
title: Configurar e configurar sites de referência de self-service do We.Finance e Funcionário
seo-title: Configurar e configurar sites de referência de self-service do We.Finance e Funcionário
description: Os sites de referência do AEM Forms mostram como você pode usar o AEM Forms para implementar um fluxo de trabalho completo em uma organização.
seo-description: Os sites de referência do AEM Forms mostram como você pode usar o AEM Forms para implementar um fluxo de trabalho completo em uma organização.
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: 70350add185b932ee604e190aabaf972ff994ba2

---


# Configurar e configurar sites de referência de self-service do We.Finance e Funcionário{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

O AEM Forms fornece uma implementação de referência do site para demonstrar como o AEM Forms ajuda organizações do setor de serviços financeiros e governamentais a transformar suas transações complexas em experiências digitais simples e envolventes em qualquer lugar, a qualquer hora, em qualquer dispositivo.

O site de referência We.Finance cria casos de uso reais para envolver-se com clientes atuais e potenciais, desde o primeiro contato até gerenciar correspondências e transações de forma personalizada e econômica.

Os sites de referência permitem explorar e mostrar os seguintes recursos principais do AEM Forms.

* Experiência de criação simplificada de formulários adaptativos e comunicações interativas envolventes e ágeis.
* Comunicações interativas para criar comunicações interativas, personalizadas e ágeis do cliente que se adaptem à configuração e ao layout do dispositivo.
* Integração de dados para conectar-se a fontes de dados diferentes para pré-preencher e enviar dados de formulário por meio de um modelo de dados de formulário.
* Fluxo de trabalho de formulários para automatizar processos de negócios e fluxos de trabalho.
* Recursos avançados de gerenciamento e processamento de dados do usuário.
* Integração com o Adobe Sign para assinar e enviar formulários adaptáveis com segurança.
* Integração com o Adobe Target para fornecer recomendações direcionadas e realizar testes A/B para maximizar o ROI de um formulário.
* Integração com o Adobe Analytics para medir o desempenho de um formulário ou campanha e tomar decisões informadas.
* Experiência de preenchimento de formulário aprimorada.

Os sites de referência fornecem ativos reutilizáveis que você pode usar como modelos para criar seus próprios ativos.

* Integração com o Adobe Sign para assinar e enviar formulários adaptáveis com segurança.

* Integração com o Adobe Sign para assinar e enviar formulários adaptáveis com segurança.

## Pré-requisitos e etapas para configurar sites de referência {#prerequisites-and-steps-to-set-up-reference-sites}

Antes de configurar o site de referência, verifique se você tem o seguinte:

* **AEM essentials** AEM QuickStart, pacote complementar AEM Forms e pacotes de site de referência. Consulte Versões [](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) do AEM Forms para obter detalhes sobre pacotes de complementos e sites de referência.

* **Um serviço** SMTP Você pode usar qualquer serviço SMTP.

* **Conta de desenvolvedor do Adobe Sign e aplicativo** Adobe Sign API Para usar os recursos de assinatura digital, é necessária a conta de desenvolvedor do Adobe Sign. Consulte [Adobe Sign](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html).

* Uma instância em execução do Microsoft Dynamics 365 para integração com o AEM Forms. Para executar o site de referência, importe os dados de amostra para a instância do Microsoft Dynamics para preencher previamente a comunicação interativa usada no site de referência.
* Uma instância em execução do AEM com o pacote complementar do Forms. Para obter mais informações, consulte [Instalação e configuração do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

Execute as seguintes etapas na sequência recomendada para configurar e configurar os sites de referência.

<table>
 <tbody>
  <tr>
   <th><strong>Etapa</strong></th>
   <th><strong>Configurar</strong></th>
   <th><strong>Notas</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">Instalar e configurar o AEM Forms</a></td>
   <td>Autor e publicação</td>
   <td>Instale e configure as instâncias de autor e publicação do AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="#ssl">Configurar SSL</a></td>
   <td>Autor e publicação<br /> </td>
   <td>Ative HTTP sobre SSL para comunicações seguras com o Adobe Sign.</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">Configurar a configuração do Externalizador de links do Day CQ</a></p> </td>
   <td>Autor e publicação<br /> </td>
   <td><p>Casos de uso do Site de referência enviam emails para diferentes transações. Essa configuração é necessária para a entrega da newsletter por email. Ela garante que URLs e imagens apontem para a instância de publicação. </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">Configurar o serviço de e-mail Day CQ</a></td>
   <td>Autor e publicação</td>
   <td>Obrigatório para comunicação por email.</td>
  </tr>
  <tr>
   <td><a href="#xss">Substituir configuração XSS padrão</a></td>
   <td>Publicação</td>
   <td>Usado para substituir caracteres $, { e } bloqueados pela segurança xss.</td>
  </tr>
  <tr>
   <td><a href="#aemds">Definir configurações do AEM DS</a></td>
   <td>Autor</td>
   <td>Configure o AEM DS para envio de formulário na instância de publicação e nos fluxos de trabalho de processamento na instância do autor.</td>
  </tr>
  <tr>
   <td><a href="#refsite">Implantar pacotes de sites de referência</a></td>
   <td>Autor</td>
   <td>Implantar pacotes de sites de referência na instância do autor do AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">Importar dados de amostra para o Microsoft Dynamics</a></td>
   <td>Autor e publicação</td>
   <td>Importar dados de amostra para aplicativos de cartão de crédito, aplicativos de hipoteca de casa e apresentação de aplicativos de seguro de casa</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">Configurar o serviço em nuvem OAuth para o Microsoft Dynamics</a></td>
   <td>Autor e publicação</td>
   <td>Configure o serviço de nuvem OAuth no AEM Forms para permitir a comunicação entre o AEM Forms e o Microsoft Dynamics. </td>
  </tr>
  <tr>
   <td><a href="#scheduler">Configurar o Adobe Sign Scheduler</a></td>
   <td>Autor e publicação<br /> </td>
   <td>Altere a configuração do agendador para verificar o status a cada dois minutos.</td>
  </tr>
  <tr>
   <td><a href="#sign-service">Configurar o site de referência Serviço da Adobe Sign Cloud</a></td>
   <td>Autor e publicação<br /> </td>
   <td>Uma configuração que vem com pacotes de sites de referência e precisa ser reconfigurada com credenciais válidas.</td>
  </tr>
  <tr>
   <td><a href="#anonymous">Configurar o Serviço de Configuração Comum do Forms para usuários anônimos</a></td>
   <td>Publicação</td>
   <td>A configuração permite a geração de submissão, assinatura e Documento de registro para usuários anônimos.</td>
  </tr>
  <tr>
   <td><a href="#fdm">Modificar o arquivo Rest Service Swagger para Modelo de Dados de Formulário</a></td>
   <td>Autor e publicação<br /> </td>
   <td>Modifique o serviço para seu ambiente.</td>
  </tr>
 </tbody>
</table>

## Instalar e configurar o AEM Forms {#installandconfigureaemform}

Instale e implante o AEM Forms conforme descrito em [Instalação e configuração do AEM Forms no OSGi](../../forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>Configure os agentes de replicação reversa e de replicação se houver mais de uma instância de publicação ou instâncias de autor e publicação em máquinas diferentes.

## Configurar SSL {#ssl}

A configuração SSL é necessária para se comunicar com os servidores Adobe Sign. Para obter etapas detalhadas, consulte [Habilitar HTTP sobre SSL](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>Não configure forçar SSL na `/etc/map` pasta.

## Configurar a configuração do Externalizador de links do Day CQ {#externalizer}

No AEM, o **Externalizador** é um serviço OSGI que permite transformar programaticamente um caminho de recurso (por exemplo, /path/to/my/page) em um URL externo e absoluto (por exemplo, https://www.mycompany.com/path/to/my/page) ao prefixar o caminho com um DNS pré-configurado. Consulte [Externalização de URLs](/help/sites-developing/externalizer.md).

>[!CAUTION]
>
>Não externalize para URL HTTPS se você estiver usando um certificado autoassinado para SSL.
>
>Além disso, use localhost em vez do nome do host para o servidor local.

Execute as seguintes etapas nas instâncias de autor e publicação:

1. Vá para Configuração do OSGi em https://&lt;nome do *host>*:&lt;*porta>*/system/console/configMgr.
1. Localize e toque em Configuração do Externalizador **de links CQ de** dia.
A caixa de diálogo Externalizador de links do Day CQ é aberta para edição da configuração.
1. Na caixa de diálogo Externalizador de links do CQ de dia, no campo Domínios:

   * Na instância do autor, especifique um URL de publicação que possa ser acessado de um sistema externo. Por exemplo, um nome de host ou um servidor da Web de publicação.
   * Na instância de publicação, especifique os URLs de autor e publicação.

1. Nas instâncias de autor e publicação, verifique se o URL do servidor local está especificado no campo Domínios.
1. Toque em **Salvar**. Aguarde um momento para que todos os serviços sejam reiniciados.

## Configurar o serviço de e-mail Day CQ {#cqmail}

A implementação do site de referência requer que os emails sejam enviados para usuários de amostra quando eles preencherem e enviarem formulários. A configuração do serviço Day CQ Mail permite fornecer detalhes do serviço SMTP para enviar emails automatizados aos clientes. See [Configuring Email Notifications](/help/sites-administering/notification.md).

Execute as seguintes etapas para configurar o serviço de email na instância de publicação:

1. Vá para Configuração do OSGi em https://&lt;nome do *host>*:&lt;*porta>*/system/console/configMgr.
1. Localize e toque em **Day CQ Mail Service** para abri-lo para configuração.
1. Forneça o nome do host do servidor SMTP e os valores da porta.
1. Toque em **Salvar.**

>[!NOTE]
>
>Você pode usar seu serviço SMTP corporativo ou serviços públicos como o Gmail. Para configurar o serviço SMTP, consulte a documentação do serviço SMTP.

## Substituir configuração XSS padrão {#xss}

Os modelos de e-mail para o site de referência We.Finance contêm links personalizados em e-mails. Esses links têm espaço reservado como `${placeholder}`. Esses espaços reservados são substituídos pelos valores reais antes do envio de emails. A configuração de proteção XSS padrão para AEM não permite chaves (**{ }**) no URL no conteúdo HTML. No entanto, você pode substituir a configuração padrão executando as seguintes etapas na instância de publicação:

1. Copie `/libs/cq/xssprotection/config.xml` para `/apps/cq/xssprotection/config.xml`.
1. Abrir `/apps/cq/xssprotection/config.xml`.
1. Na `common-regexps` seção, modifique a `onsiteURL` entrada como segue e salve o arquivo.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>As chaves (**{ }**) são incluídas como caracteres aceitos no URL no conteúdo HTML.

Depois de configurar o servidor SMTP, tente preencher um formulário usando a persona Sarah Rose e salve-o como um rascunho. Ao salvar como rascunho, você obtém uma opção para receber o rascunho por email. Ao tocar no botão **Enviar e-mail** , se você receber um e-mail com um link para o rascunho do aplicativo, sua configuração de e-mail será bem-sucedida. Faça logon usando as credenciais da Sarah para ver o rascunho.

## Definir configurações do AEM DS {#aemds}

As configurações do serviço AEM DS são necessárias na instância Publicar para comunicações por email nos casos de uso do site de referência. Para obter etapas detalhadas para configurar o serviço AEM DS na instância Publicar, consulte [Configurar configurações](../../forms/using/configuring-the-processing-server-url-.md)do AEM DS.

Para sites de referência do AEM Forms, no serviço de configurações do AEM DS, especifique o URL do servidor de publicação em vez do URL do servidor de processamento.

>[!CAUTION]
>
>Não coloque `/lc` no URL do servidor de processamento se você estiver configurando-o para OSGi do AEM Forms.

## Implantar pacotes de sites de referência {#refsite}

Instale os pacotes de sites de referência usando o compartilhamento de pacotes.

* [Pacote do site de referência FSI do AEM Forms](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-FSI-REF-SITE)
* [Pacote do site de referência do AEM Forms Gov](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-GOV-REF-SITE)

Para saber mais sobre como usar pacotes e compartilhamento de pacotes, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).

Depois de instalar os pacotes e iniciar as instâncias de autor e publicação, visite os seguintes URLs no seu navegador:

* `https://[server]:[port]/wegov`
* `https://[server]:[port]/wefinance`

Se sua instalação for bem-sucedida, você poderá acessar as páginas de aterrissagem dos sites de referência e We.Finance.

## (Opcional) Importar dados de amostra para o Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

Os sites de referência do aplicativo hipotecário doméstico e do aplicativo de seguro automático estão configurados para usar registros do Microsoft Dynamics. O pacote do site de referência instala uma entidade personalizada e registros de amostra que você pode importar para o Microsoft Dynamics para executar o site de referência. Execute as seguintes etapas para migrar e configurar os dados de amostra:

Para importar a entidade personalizada para o aplicativo de seguro automático:

1. Baixe o pacote da solução **WeFinanceAutoInsurance_1_0.zip** `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` na instância do autor do AEM.
1. Na instância do Microsoft Dynamics, vá até **Configurações > Soluções** e clique em **Importar**. Selecione e importe o pacote.

Para importar a entidade personalizada para o aplicativo de seguro automático:

1. Baixe o pacote **AEMFormsFSIRefsite_1_0.zip** de `https://[author]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`. Selecione e importe o pacote.

1. Na instância do Microsoft Dynamics, vá até **Configurações > Soluções** e clique em **Importar**. Selecione e importe o pacote.

Para importar os registros do cliente e da apólice de seguro:

1. Baixe os arquivos de dados de **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv** e **home** dos seguintes locais na sua instância do autor do AEM:

   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Na instância do Microsoft Dynamics, faça o seguinte:

   * Vá para **Vendas** > Clientes **** We.Finance e clique em **Importar**.

   * Vá para **Vendas** > **We.Finance Auto Insurance** e clique em **Importar**.

   * Vá até **Sales** > **We.Finance Home Mortgage** e clique em **Import**.

## Configurar o serviço em nuvem OAuth para o Microsoft Dynamics {#configure-oauth-cloud-service-for-microsoft-dynamics}

Configure o serviço de nuvem OAuth no AEM Forms para permitir a comunicação entre o AEM Forms e o Microsoft Dynamics. Execute as seguintes etapas para configurar o serviço da OAuth Cloud nas instâncias de autor e publicação do AEM:

1. Na instância do autor do AEM, vá para **Ferramentas** > Serviços **** em nuvem > Fontes **** de dados > **global**. Toque no ícone **Refsite Dynamics Integration** e toque em Propriedades.
1. Vá para a conta do Microsoft Azure Ative Diretory. Adicione o URL de configuração do serviço de nuvem copiado na configuração **Responder URL** para seu aplicativo registrado. Salve a configuração.
1. Na guia Configurações de autenticação, especifique Raiz **do** serviço, Id **do** cliente, Segredo **do** cliente e URL **do** recurso para sua instância do Microsoft Dynamics. Clique em **Conectar-se ao OAuth** que redireciona para a página de logon do Microsoft Dynamics.
1. Forneça suas credenciais de logon. Depois de conectado, você é redirecionado para a página de configuração do serviço em nuvem do AEM Forms. Clique em **Salvar e fechar**. A configuração do serviço de nuvem é salva.
1. Vá para **Formulários** > Integrações **** de dados > **We.Finance**. Selecione Seguro automático (Dinâmico) e clique em Editar. As entidades do Microsoft Dynamics estão listadas na guia Fontes de Dados. Aguarde até que todas as entidades sejam buscadas no Microsoft Dynamics e listadas na guia fontes de dados.
1. Selecione a entidade **** AutoInsuranceRenewal e clique em **Testar objeto** de modelo. Na seção de solicitação de entrada, especifique o valor para a ID do cliente como &quot;900001&quot; e clique em **Testar**. A seção Saída exibe os registros obtidos do Microsoft Dynamics para a ID do cliente 900001.
1. Na seção de solicitação de entrada, especifique o valor para a ID do cliente como &quot;900001&quot; e clique em **Testar**. A seção Saída exibe os registros obtidos do Microsoft Dynamics para a ID do cliente 900001.
1. Repita as etapas de 1 a 6 na instância de publicação.

## Configurar o Adobe Sign Scheduler {#scheduler}

Faça o seguinte nas instâncias de autor e publicação:

1. Vá para o console de configuração da Web do AEM em `https://[server]:[host]/system/console/configMgr`.
1. Localize e toque em Serviço **[!UICONTROL de configuração do]** Adobe Sign para abri-lo para configuração.
1. Configure a Expressão **[!UICONTROL do Agendador de Atualização de]** Status como **0 0/2 * * * ?**.

   >[!NOTE]
   >
   >A configuração do programador acima verifica o status do serviço Adobe Sign a cada dois minutos.

1. Toque em **[!UICONTROL Salvar]**.

## Configurar o site de referência Serviço em nuvem do Adobe Sign {#sign-service}

Faça o seguinte nas instâncias de autor e publicação:

1. Acesse **Ferramentas** > Serviços **da** nuvem > **Adobe Sign** > **global**. Selecione **AEM Forms Reference Site Sign** e toque em Propriedades.

   >[!CAUTION]
   >
   >Certifique-se de que o `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html` URL seja adicionado à lista de URL de redirecionamento da configuração OAuth do aplicativo Adobe Sign API.

1. Especifique a ID do cliente e o segredo da configuração OAuth do aplicativo Adobe Sign.
1. (Opcional) Selecione a opção **[!UICONTROL Ativar o Adobe Sign para anexos também]** e toque em **[!UICONTROL Conectar-se ao Adobe Sign]**. Ele anexa os arquivos anexados a formulários adaptáveis ao documento Adobe Sign correspondente enviado para assinatura.
1. Toque em **[!UICONTROL Conectar-se ao Adobe Sign]** e faça logon com suas credenciais do Adobe Sign.

## Configurar o serviço de configuração comum do Forms {#anonymous}

Faça o seguinte na instância de publicação para permitir acesso a usuários anônimos:

1. Vá para o console de configuração da Web do AEM em `https://[server]:[port]/system/console/configMgr`.
1. Localize e toque em Serviço **[!UICONTROL de configuração comum do]** Forms para abri-lo para configuração.
1. Configure o campo **[!UICONTROL Permitir]** para **[!UICONTROL todos os usuários]**.
1. Toque em **[!UICONTROL Salvar]**.

## Modificar o serviço Restaurar para o modelo de dados de formulário {#fdm}

Faça o seguinte nas instâncias de autor e publicação:

1. Vá para CRXDE em `https://[server]:[port]/crx/de/index.jsp`.
1. Navegue até **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerArquivo** e abra o arquivo swagger.
1. Atualize as configurações de host e porta de acordo com seu ambiente.
1. Salve as configurações.
1. (Somente **instância do** autor) Vá até **Ferramentas** > Serviços **** em nuvem > Fontes **de** dados > **global**. Selecione **roi-rest** e toque em **Properties**.Tap **Authentication Settings** e defina **Authentication Type** como **Basic Authentication**. Especifique `admin`/ `admin`como nome de usuário/senha para acessar o serviço. Toque em **Salvar e fechar**.

## Integrar-se à Marketing Cloud {#integrate-with-marketing-cloud}

Você pode integrar os formulários do AEM com o Adobe Analytics e o Adobe Target. Enquanto o Adobe Analytics ajuda a gerar relatórios e analisar o desempenho de formulários adaptáveis, o Adobe Target ajuda você a fornecer experiências personalizadas e a executar testes A/B para formulários adaptáveis.

Faça o seguinte para configurar o Adobe Analytics e o Adobe Target no AEM Forms.

### Configurar o Adobe Analytics {#configureanalytics}

A integração do AEM Forms com o Adobe Analytics permite monitorar e analisar como seus clientes interagem com seus formulários e documentos. Ajuda a identificar e corrigir áreas com problemas e a agir para aumentar a taxa de conversão.

Para experimentar essa funcionalidade no site de referência, configure sua conta do Analytics conforme descrito em [Configuração de análises e relatórios](../../forms/using/configure-analytics-forms-documents.md).

Para gerar um relatório, os dados semente são agrupados com os sites de referência. Antes de usar dados semente, faça o seguinte:

1. Verifique se as configurações de análise We.Finance estão disponíveis nos serviços da AEM Cloud. Você pode encontrar serviços em nuvem de uma das seguintes maneiras:

   * Navegue até **[!UICONTROL Ferramentas>Serviços em nuvem>Serviços]** herdados em nuvem ou navegue até https://&lt;host>:&lt;porta>/libs/cq/core/content/tools/cloudservices.html.
   * Na página Serviços **[!UICONTROL da]** Cloud, na seção **[!UICONTROL Adobe Analytics]** , clique em `Show Configurations`. Você pode ver as configurações We.Finance disponíveis. Clique para abrir a configuração. Na página de configuração, clique em **[!UICONTROL Editar]**. Forneça Empresa, Nome de usuário, Segredo compartilhado (Senha) e Centro de dados válidos e clique em **[!UICONTROL Conectar-se ao Analytics]**. Após obter a caixa de diálogo Conexão bem-sucedida, clique em **[!UICONTROL OK]** na caixa de diálogo de configuração. Configure a estrutura na configuração do Analytics, conforme descrito em [Configuração do Analytics e Relatórios](../../forms/using/configure-analytics-forms-documents.md).

1. Navegue até https://&lt;*host*>:&lt;*porta*>/system/console/configMgr e faça o seguinte:

   * Na página Configuração **[!UICONTROL do console]** da Web, localize e clique em Configuração **[!UICONTROL do]** AEM Forms Analytics.

   * No campo Estrutura **[!UICONTROL do]** SiteCatalyst da caixa de diálogo Configuração de análise do AEM Forms, selecione we-finance(we-finance) ou we-gov(we-gov).
   * Clique em **[!UICONTROL Salvar]** e deixe a página ser atualizada.

1. Navegue até o gerenciador de formulários em https://&lt;host>:&lt;porta>/aem/forms e faça o seguinte:

   * Abra a pasta We.Finance e selecione o formulário para o qual deseja visualizar o relatório.
   * Clique em Ativar o Analytics na barra de ferramentas de ações. Depois de ativar a análise do formulário, clique em Relatório de análise. Você pode ver um relatório em branco gerado. Depois que um relatório em branco é gerado, é necessário fornecer dados de semente fornecidos com o pacote de resite para gerar o relatório de análise para fins de demonstração.
   Os sites de referência fornecem relatórios analíticos com dados de semente para cartão de crédito, hipoteca doméstica e casos de uso de suporte a crianças.

### Configurar o Target {#configure-target}

O site de referência mostra a integração do AEM Forms com o Adobe Target, que permite incluir conteúdo direcionado e personalizado em documentos adaptáveis. Também permite a criação de testes A/B para formulários adaptáveis.

Para experimentar a integração no site de referência, faça o seguinte para configurar o Target no AEM:

1. Inicie o autor rapidamente com o argumento jvm `-Dabtesting.enabled=true` para ativar o teste A/B no servidor.
   **Observação**: Se a instância do AEM estiver em execução no JBoss, que é iniciado como um serviço da instalação do Turnkey, adicione o `-Dabtesting.enabled=true` parâmetro na seguinte entrada no `jboss\bin\standalone.conf.bat` arquivo:
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. Acesso `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. Na seção **[!UICONTROL Adobe Target]** , clique em **[!UICONTROL Mostrar configurações]**. Você pode ver a Configuração do Target We.Finance disponível. Clique para abrir a configuração. Na página de configuração, clique em **[!UICONTROL Editar]**. A caixa de diálogo **[!UICONTROL Editar componente]** da configuração é aberta.

1. Especifique o código do cliente, o email e a senha associados à sua conta do Target. Selecione o tipo de API como **[!UICONTROL REST]**.
1. Click **[!UICONTROL Connect to Adobe target]**. Depois que a conta do Target for configurada com êxito, clique em **[!UICONTROL OK]**. Você pode ver que a configuração empacotada tem uma estrutura do Target.

1. Ir para `https://<hostname>:<port>/system/console/configMgr`.

1. Clique em Configuração **[!UICONTROL de destino de formulários]** AEM.
1. Selecione uma estrutura do Target.
1. No campo URLs **[!UICONTROL do]** Target, especifique o URL para o AEM Forms. Por exemplo: `https://<hostname>:<port>/`.

1. Clique em **[!UICONTROL Salvar]**.

Os casos de uso do aplicativo de cartão de crédito e do aplicativo hipotecário pessoal demonstram como executar um teste A/B e mostrar um relatório para fins de demonstração. Para saber mais sobre as orientações, consulte a apresentação do site de referência [We.Finance](../../forms/using/finance-reference-site-walkthrough.md).

## Next step {#next-step}

Agora todos estão prontos para explorar o site de referência. Para obter mais informações sobre o fluxo de trabalho e as etapas do site de referência, consulte:

* [Apresentação do site de referência do We.Finance](../../forms/using/finance-reference-site-walkthrough.md)
* [Apresentação do site de referência de autoatendimento do funcionário](../../forms/using/employee-self-service-reference-site.md)

