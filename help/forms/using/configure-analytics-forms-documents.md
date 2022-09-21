---
title: Configuração de análises e relatórios
seo-title: Configuring analytics and reports
description: Saiba como configurar o Adobe Analytics para descobrir padrões e problemas de interação enfrentados pelos usuários ao usar formulários adaptáveis, documentos adaptáveis e formulários HTML5.
seo-description: Learn how to configure Adobe Analytics to discover interaction patterns and problems users face while using adaptive forms, adaptive documents, and HTML5 forms.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
source-git-commit: 66631fd0813f623f3321072fc00fd90f7fa33d21
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 1%

---

# Analytics usando a Estrutura do Cloud Service {#analyticsusingcloudframework}

O AEM Forms integra-se ao Analytics, que permite capturar e rastrear métricas de desempenho para seus formulários e documentos publicados. O objetivo por trás da análise dessas métricas é tomar decisões informadas com base em dados sobre as alterações necessárias para tornar os formulários ou documentos mais utilizáveis.

>[!NOTE]
>
>O recurso de análise no AEM Forms está disponível como parte do pacote complementar do AEM Forms. Para obter informações sobre como instalar o pacote complementar, consulte [Instalação e configuração do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>Além do pacote complementar, você precisa de uma conta Adobe Analytics e privilégios de administrador na instância do AEM. Para obter informações sobre a solução, consulte [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

Também é possível executar análises usando o Adobe Launch. Para obter mais informações sobre como integrar o AEM Forms com o Adobe Launch, consulte [Analytics usando o Adobe Launch](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md).

## Visão geral {#overview}

Você pode usar o Adobe Analytics para descobrir padrões e problemas de interação que os usuários enfrentam ao usar formulários adaptáveis, formulários HTML5 e comunicação interativa. Imediatamente, o Adobe Analytics rastreia e armazena informações sobre os seguintes parâmetros:

* **Tempo médio de preenchimento**: Tempo médio gasto para preencher o formulário.
* **Representações**: Número de vezes que um formulário é aberto.
* **Rascunhos**: Número de vezes que um formulário é salvo no estado de rascunho.
* **Submissões**: Número de vezes que um formulário é enviado.
* **Abortar**: Número de vezes que os usuários saem sem preencher o formulário.

Você pode personalizar o Adobe Analytics para adicionar/remover mais parâmetros. Juntamente com as informações acima, o relatório contém as seguintes informações sobre cada painel do HTML5 e formulário adaptável:

* **Hora**: Tempo gasto no painel e nos campos do painel.
* **Erro**: Número de erros encontrados no painel e nos campos do painel.
* **Ajuda**: Número de vezes que um usuário abre a ajuda de um painel e os campos do painel.

## Criar conjunto de relatórios {#creating-report-suite}

Os dados do Analytics são armazenados em repositórios específicos do cliente chamados de conjuntos de relatórios. Para criar um conjunto de relatórios e usar o Adobe Analytics, é necessário ter uma conta Adobe Marketing Cloud válida. Antes de executar as etapas a seguir, verifique se você tem uma conta Adobe Marketing Cloud válida.

Execute as etapas a seguir para criar um conjunto de relatórios.

1. Faça logon em [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. No Marketing Cloud , selecione **Administrador** > **Admin Console** > **Conjuntos de relatórios**.
1. Selecionar **Criar novo** > **Conjunto de relatórios** no Gerenciador de conjunto de relatórios.

   ![Criar novo conjunto de relatórios](assets/newreportsuite_new.png)

   Criar novo conjunto de relatórios

1. Certifique-se de que a primeira lista suspensa esteja definida como **Criar a partir de um modelo** e depois selecione **Comércio**.
1. Localize a variável **ID do conjunto de relatórios** e adicionar uma nova ID do conjunto de relatórios. Por exemplo, JJEsquire. Uma ID de conjunto de relatórios é exibida abaixo do campo ID de conjunto de relatórios . Ele inclui um prefixo automático, que geralmente é o nome da empresa.
1. Adicionar novo **Título do Site**. Por exemplo, JJEsquire Introdução ao Suite. Este título é usado na interface do usuário do Analytics. Use a ID do conjunto de relatórios no seu código.
1. Selecione um **Fuso Horário** na lista suspensa. Todos os dados que entram nesse conjunto de relatórios são registrados com base no fuso horário definido.
1. Deixe o **URL básica** e **Página Padrão** campos vazios. Esses dois valores são usados somente na interface do Adobe Marketing Cloud para vincular ao seu site.
1. Deixe o **Data de ativação** definido como hoje. A Data de ativação determina o dia em que o conjunto de relatórios é ativado.
1. No **Exibições de página estimadas por dia** , digite 100. Use este campo para estimar o número de exibições de página que você prevê para seu site por dia. Essa estimativa permite que o Adobe instale a quantidade apropriada de hardware para processar os dados que você coletará.
1. Selecione um **Moeda de base** na lista suspensa. Todos os dados de moeda que entram neste conjunto de relatórios são convertidos e armazenados neste formato de moeda.
1. Clique em **Criar relatório** Suite. Você deve ver a atualização da página com uma mensagem de que seu conjunto de relatórios foi criado com êxito.
1. Selecione o Conjunto de relatórios recém-criado. Navegar para **Editar configurações** > **Geral** > **Configurações gerais da conta**.

   ![Configurações gerais da conta](assets/geographic_settings.png)

   Configurações gerais da conta

1. Na tela Configurações gerais da conta , ative **Relatórios de geografia** e clique em **Salvar.**
1. Navegar para **Editar configurações** > **Tráfego** > **Variáveis de tráfego**.
1. No conjunto de relatórios, configure e ative as seguintes variáveis de tráfego.

   * **formName**: Identificador para um formulário adaptável.
   * **formInstance**: Identificador de uma instância de formulário adaptável. Habilite relatórios de Caminho para essa variável.
   * **fieldName**: Identificador de um campo de formulário adaptável. Habilite relatórios de Caminho para essa variável.
   * **panelName**: Identificador de um painel de formulário adaptável. Habilite relatórios de Caminho para essa variável.
   * **formTitle**: Título do formulário.
   * **fieldTitle**: Título do campo de formulário.
   * **panelTitle**: Título do painel de formulário.
   * **analyticsVersion**: Versão da análise de formulário.

1. Navegar para **Editar configurações** > **Conversão** > **Eventos bem-sucedidos**. Defina e ative os seguintes eventos bem-sucedidos:

   | Evento bem-sucedido | Tipo |
   |---|---|
   | abandono | Contador |
   | renderizar | Contador |
   | panelVisit | Contador |
   | fieldVisit | Contador |
   | save | Contador |
   | erro | Contador |
   | Ajuda com o  | Contador |
   | submit | Contador |
   | timeSpent | Numérico |

   >[!NOTE]
   >
   >Um número de evento e número de propriedade usados para configurar a análise do AEM Forms devem ser diferentes do número de evento e do número de propriedade usados em [Análise de AEM](/help/sites-administering/adobeanalytics.md) configuração.

1. Faça logoff da conta do Adobe Marketing Cloud.

## Criação da configuração do Cloud Service {#creating-cloud-service-configuration}

A configuração do Cloud Service é uma informação sobre sua conta do Adobe Analytics. A configuração permite que o Adobe Experience Manager (AEM) se conecte ao Adobe Analytics. Crie uma configuração separada para cada conta do Analytics usada.

1. Faça logon na instância do autor do AEM como administrador.
1. No canto superior esquerdo, clique em **Adobe Experience Manager** > **Ferramentas** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **Cloud Services herdados**.
1. Localizar **Adobe Analytics** ícone . Clique em **Mostrar configurações** e, em seguida, continue a clicar em **[+]** para adicionar nova configuração.

   Se você for um usuário novo, clique em **Configurar agora**.

1. Adicione um Título à nova configuração (o preenchimento do campo Nome é opcional). Por exemplo, a configuração Minha análise . Clique em **Criar**.

1. Quando o painel Editar abrir a página de configuração, preencha os campos:

   * **Empresa**: O nome da sua empresa como em destaque no Adobe Analytics.
   * **Nome do usuário**: O nome usado para fazer logon no Adobe Analytics.
   * **Senha**: A senha do Adobe Analytics para a conta acima.
   * **Data Center**: O data center de sua conta da Adobe Analytics.

1. Clique em **Conectar-se ao Analytics**. Uma caixa de diálogo é exibida com a mensagem de que a conexão foi bem-sucedida. Clique em **OK**.

## Criação de uma estrutura Cloud Service {#creating-cloud-service-framework}

Uma estrutura Adobe Analytics é um conjunto de mapeamentos entre variáveis Adobe Analytics e variáveis AEM. Use uma estrutura para configurar como seus formulários preenchem dados para os relatórios do Adobe Analytics. As Frameworks estão associadas a uma configuração do Adobe Analytics. Você pode criar várias estruturas para cada configuração.

1. No console de serviços em nuvem do AEM, clique em **Mostrar configurações**, em Adobe Analytics.
1. Clique no botão **[+]** ao lado da configuração do Analytics.

   ![Configuração do Adobe Analytics](assets/adobe-analytics-cloud-services.png)

   Configuração do Adobe Analytics

1. Digite um **Título** e **Nome** para a estrutura, selecione **Adobe Analytics** Framework e clique em **Criar**. A estrutura é aberta para edição.
1. Na seção Conjuntos de relatórios do pod lateral, clique em **Adicionar item**, em seguida, use o menu suspenso para selecionar a ID do conjunto de relatórios (por exemplo, JJEsquire) com a qual a estrutura interagirá.
1. Ao lado da ID do conjunto de relatórios, selecione as instâncias do servidor para as quais deseja enviar informações.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. Arraste um **Componente de análise de formulário** do **other** categoria de SideKick na estrutura.
1. Para mapear variáveis do Analytics com variáveis definidas no componente, arraste uma variável AEM Localizador de conteúdo para um campo no componente de rastreamento.

   ![Mapeamento AEM variáveis com variáveis Adobe Analytics](assets/analytics_new.png)

1. Ative a estrutura usando o **guia página** no sidekick, clique em **Ativar estrutura**.

## Configuração do serviço de configuração do AEM Forms Analytics {#configuring-aem-forms-analytics-configuration-service}

1. Na instância do autor, abra AEM Gerenciador de Configuração do Console da Web em `https://<server>:<port>;/system/console/configMgr`.
1. Localize e abra a Configuração do AEM Forms Analytics

   ![Serviço de configuração do AEM Forms Analytics](assets/analytics_configuration.png)

   Serviço de configuração do AEM Forms Analytics

1. Especifique os valores apropriados para os seguintes campos e clique em **Salvar**.

   * **Estrutura do SiteCatalyst**: Selecione a estrutura/configuração definida na seção Configurar uma estrutura para rastreamento .
   * **Linha de base de rastreamento de tempo do campo**: Especifique a duração, em segundos, após a qual a visita de campo deve ser rastreada. O valor padrão é 0. Quando o valor é maior que 0 (zero), dois eventos de rastreamento separados são enviados para o servidor do Adobe Analytics. O primeiro evento instrui o servidor do Analytics a parar de rastrear o campo encerrado. O segundo evento é enviado após o período especificado. O segundo evento instrui o servidor do analytics a iniciar o rastreamento do campo visitado. Usar dois eventos separados ajuda a medir com precisão o tempo gasto em um campo. Quando o valor é 0 (zero), um único evento de rastreamento é enviado para o servidor do Adobe Analytics.

   * **Cron de sincronização de relatórios do Analytics**: Especifique a expressão de pesquisa para buscar relatórios do Adobe Analytics. O valor padrão é 0 0 2 ? &#42; &#42;.

   * **Buscar tempo limite do relatório:** Especifique a duração, em segundos, para aguardar o servidor responder ao relatório de análise. O tempo padrão é de 120 segundos.
   >[!NOTE]
   >
   >Pode levar até 10 segundos a mais para a operação de busca de relatório de tempo limite do que o número especificado de segundos.

1. Repita as etapas 1 a 3 na instância de publicação para configurar o analytics.

Agora, é possível ativar o Analytics para formulários e gerar um relatório de análise.

## Ativação do analytics para um formulário ou documento {#enabling-analytics-for-a-form-or-document}

1. Faça logon no AEM portal em `https://[hostname]:'port'`.
1. Clique em **Forms > Forms e documentos**, selecione um formulário ou documento e clique em **Ativar o Analytics**. A análise está ativada.

   ![Ativação do analytics para um formulário ou documento](assets/enable-analytics-1.png)

   Ativação do analytics para um formulário

   **A.** Botão Ativar o Analytics **B.** Formulário selecionado

   Para obter informações detalhadas sobre a exibição de relatórios analíticos de formulários, consulte [Visualização e compreensão dos relatórios de análise do AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).
