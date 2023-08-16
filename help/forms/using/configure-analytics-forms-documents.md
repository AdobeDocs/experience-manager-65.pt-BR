---
title: Configuração de análises e relatórios
seo-title: Configuring analytics and reports
description: Saiba como configurar o Adobe Analytics para descobrir padrões de interação e problemas que os usuários enfrentam ao usar formulários adaptáveis, documentos adaptáveis e formulários HTML5.
seo-description: Learn how to configure Adobe Analytics to discover interaction patterns and problems users face while using adaptive forms, adaptive documents, and HTML5 forms.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 3%

---

# Analytics usando a estrutura Cloud Service {#analyticsusingcloudframework}

O AEM Forms integra-se ao Analytics, o que permite capturar e rastrear as métricas de desempenho dos formulários e documentos publicados. O objetivo por trás da análise dessas métricas é tomar decisões informadas com base em dados sobre as alterações necessárias para tornar os formulários ou documentos mais utilizáveis.

>[!NOTE]
>
>O recurso de análise no AEM Forms está disponível como parte do pacote complementar do AEM Forms. Para obter informações sobre como instalar o pacote complementar, consulte [Instalação e configuração do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>Além do pacote complementar, é necessário ter uma conta do Adobe Analytics e privilégios de administrador na instância do AEM. Para obter informações sobre a solução, consulte [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

Também é possível executar a análise usando o Adobe Launch. Para obter mais informações sobre como integrar o AEM Forms com o Adobe Launch, consulte [Analytics usando o Adobe Launch](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md).

## Visão geral {#overview}

Use o Adobe Analytics para descobrir padrões de interação e problemas que os usuários enfrentam ao usar formulários adaptáveis, formulários HTML5 e comunicação interativa. Pronto para uso, o Adobe analytics rastreia e armazena informações sobre os seguintes parâmetros:

* **Tempo médio de preenchimento**: Tempo médio gasto para preencher o formulário.
* **Representações**: Número de vezes que um formulário é aberto.
* **Rascunhos**: Número de vezes que um formulário é salvo no estado de rascunho.
* **Envios**: Número de vezes que um formulário é enviado.
* **Anular**: Número de vezes que os usuários saem sem preencher o formulário.

Você pode personalizar o Adobe Analytics para adicionar/remover mais parâmetros. Juntamente com as informações acima, o relatório contém as seguintes informações sobre cada painel do HTML5 e o formulário adaptável:

* **Hora**: Tempo gasto no painel e nos campos do painel.
* **Erro**: Número de erros encontrados no painel e nos campos do painel.
* **Ajuda**: Número de vezes que um usuário abre a ajuda de um painel e os campos do painel.

## Criação do conjunto de relatórios {#creating-report-suite}

Os dados do Analytics são armazenados em repositórios específicos do cliente, chamados de conjuntos de relatórios. Para criar um conjunto de relatórios e usar o Adobe Analytics, você deve ter uma conta válida do Adobe Marketing Cloud. Antes de executar as etapas a seguir, verifique se você tem uma conta válida do Adobe Marketing Cloud.

Execute as seguintes etapas para criar um conjunto de relatórios.

1. Fazer logon em [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. No Marketing Cloud, selecione **Admin** > **Admin Console** > **Conjuntos de relatórios**.
1. Selecionar **Criar novo** > **Report Suite** no Gerenciador de conjunto de relatórios.

   ![Criar novo conjunto de relatórios](assets/newreportsuite_new.png)

   Criar novo conjunto de relatórios

1. Verifique se a primeira lista suspensa está definida como **Criar a partir de um modelo** e selecione **Commerce**.
1. Localize o **ID do conjunto de relatórios** e adicione uma nova ID de conjunto de relatórios. Por exemplo, JJEsquire. Uma ID de conjunto de relatórios é exibida abaixo do campo ID de conjunto de relatórios. Inclui um prefixo automático, que geralmente é o nome da empresa.
1. Adicionar novo **Título do site**. Por exemplo, JJEsquire Getting Started Suite. Esse título é usado na interface do Analytics. Use a ID do conjunto de relatórios no seu código.
1. Selecione um **Fuso Horário** na lista suspensa. Todos os dados que entram nesse conjunto de relatórios são registrados com base no fuso horário definido.
1. Deixe a **URL base** e **Página padrão** campos vazios. Esses dois valores são usados somente na interface do Adobe Marketing Cloud para vincular ao seu site.
1. Deixe a **Data de ativação** defina como hoje. A Data de ativação determina o dia em que o conjunto de relatórios é ativado.
1. No **Exibições de página estimadas por dia** tipo 100. Use esse campo para estimar o número de exibições de página que você antecipa para seu site por dia. Essa estimativa permite que o Adobe coloque em prática a quantidade apropriada de hardware para processar os dados que você coletará.
1. Selecione um **Moeda de base** na lista suspensa. Todos os dados de moeda que entram nesse conjunto de relatórios são convertidos e armazenados nesse formato de moeda.
1. Clique em **Criar relatório** Suite. Você deve ver a atualização da página com uma mensagem de que o conjunto de relatórios foi criado com sucesso.
1. Selecione o conjunto de relatórios recém-criado. Navegue até **Editar configurações** > **Geral** > **Configurações gerais da conta**.

   ![Configurações gerais da conta](assets/geographic_settings.png)

   Configurações gerais da conta

1. Na tela Configurações gerais da conta, ative **Relatório de Geografia** e clique em **Salve.**
1. Navegue até **Editar configurações** > **Tráfego** > **Variáveis de tráfego**.
1. No conjunto de relatórios, configure e ative as variáveis de tráfego a seguir.

   * **formName**: Identificador para um formulário adaptável.
   * **formInstance**: Identificador de uma instância de formulário adaptável. Ative Relatórios de caminho para essa variável.
   * **fieldName**: Identificador de um campo de formulário adaptável. Ative Relatórios de caminho para essa variável.
   * **panelName**: Identificador de um painel de formulário adaptável. Ative Relatórios de caminho para essa variável.
   * **formTitle**: Título do formulário.
   * **fieldTitle**: Título do campo de formulário.
   * **panelTitle**: Título do painel de formulário.
   * **analyticsVersion**: versão do form analytics.

1. Navegue até **Editar configurações** > **Conversão** > **Eventos bem-sucedidos**. Defina e ative os seguintes eventos bem-sucedidos:

   | Evento bem-sucedido | Tipo |
   |---|---|
   | abandonar | Contador |
   | renderizar | Contador |
   | panelVisit | Contador |
   | fieldVisit | Contador |
   | save | Contador |
   | erro | Contador |
   | Ajuda com o  | Contador |
   | enviar | Contador |
   | timeSpent | Numérico |

   >[!NOTE]
   >
   >Um número de evento e número de prop usados para configurar o AEM Forms Analytics devem ser diferentes do número de evento e número de prop usados no [Análise do AEM](/help/sites-administering/adobeanalytics.md) configuração.

1. Faça logout da conta do Adobe Marketing Cloud.

## Criação da configuração de Cloud Service {#creating-cloud-service-configuration}

Cloud Service é a informação sobre sua conta Adobe Analytics. A configuração permite que o Adobe Experience Manager (AEM) se conecte ao Adobe Analytics. Crie uma configuração separada para cada conta do Analytics que você usa.

1. Faça logon na instância de autor do AEM como administrador.
1. No canto superior esquerdo, clique em **Adobe Experience Manager** > **Ferramentas** ![ícone de martelo](/help/forms/using/assets/tools.png) > **Cloud Service** > **Cloud Service herdados**.
1. Localizar **Adobe Analytics** ícone. Clique em **Exibir configurações** e prossiga para o clique **[+]** para adicionar nova configuração.

   Se você for um usuário pela primeira vez, clique em **Configurar agora**.

1. Adicione um Título à nova configuração (o preenchimento do campo Nome é opcional). Por exemplo, Minha configuração de análise. Clique em **Criar**.

1. Quando o painel Editar for aberto na página de configuração, preencha os campos:

   * **Empresa**: o nome da sua empresa conforme consta no Adobe Analytics.
   * **Nome de usuário**: o nome usado para fazer logon no Adobe Analytics.
   * **Senha**: a senha do Adobe Analytics para a conta acima.
   * **Centro de dados**: o data center da sua conta da Adobe Analytics.

1. Clique em **Conectar-se ao Analytics**. Uma caixa de diálogo é exibida com a mensagem de que a conexão foi bem-sucedida. Clique em **OK**.

## Criação da estrutura Cloud Service {#creating-cloud-service-framework}

Uma estrutura Adobe Analytics é um conjunto de mapeamentos entre variáveis Adobe Analytics e variáveis AEM. Use uma estrutura para configurar como seus formulários preenchem dados para relatórios do Adobe Analytics. As estruturas são associadas a uma configuração do Adobe Analytics. É possível criar várias estruturas para cada configuração.

1. No console de serviços em nuvem do AEM, clique em **Mostrar configurações**, em Adobe Analytics.
1. Clique em **[+]** ao lado de sua configuração do Analytics.

   ![Configuração do Adobe Analytics](assets/adobe-analytics-cloud-services.png)

   Configuração do Adobe Analytics

1. Digite a **Título** e **Nome** para a estrutura, selecione **Adobe Analytics** e clique em **Criar**. A estrutura é aberta para edição.
1. Na seção Conjuntos de relatórios do pod lateral, clique em **Adicionar item**, em seguida, use o menu suspenso para selecionar a ID de conjunto de relatórios (por exemplo, JJEsquire) com a qual a estrutura interagirá.
1. Ao lado da ID do conjunto de relatórios, selecione as instâncias de servidor para as quais deseja enviar informações.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. Arraste um **Componente do Form Analytics** do **outro** categoria de Sidekick para a estrutura.
1. Para mapear variáveis do Analytics com variáveis definidas no componente, arraste uma variável do Localizador de conteúdo do AEM para um campo no componente de rastreamento.

   ![Mapeamento de variáveis do AEM com variáveis do Adobe Analytics](assets/analytics_new.png)

1. Ative a estrutura usando o **guia página** no sidekick, clique em **Ativar Framework**.

## Configuração do serviço de configuração do AEM Forms Analytics {#configuring-aem-forms-analytics-configuration-service}

1. Na instância do autor, abra o Gerenciador de configuração do console da Web do AEM em `https://<server>:<port>;/system/console/configMgr`.
1. Localizar e abrir a Configuração do AEM Forms Analytics

   ![Serviço de configuração do AEM Forms Analytics](assets/analytics_configuration.png)

   Serviço de configuração do AEM Forms Analytics

1. Especifique os valores apropriados para os seguintes campos e clique em **Salvar**.

   * **Estrutura do SiteCatalyst**: selecione a estrutura/configuração definida na seção Definir uma estrutura para rastreamento.
   * **Linha de base do rastreamento de tempo de campo**: especifique a duração, em segundos, após a qual a visita de campo deve ser rastreada. O valor padrão é 0. Quando o valor é maior que 0 (zero), dois eventos de rastreamento separados são enviados ao servidor do Adobe Analytics. O primeiro evento instrui o servidor do Analytics a interromper o rastreamento do campo encerrado. O segundo evento é enviado após o término da duração especificada. O segundo evento instrui o servidor do Analytics a começar a rastrear o campo visitado. Usar dois eventos separados ajuda a medir com precisão o tempo gasto em um campo. Quando o valor é 0 (zero), o evento de rastreamento único é enviado ao servidor do Adobe Analytics.

   * **cron de sincronização de relatório do Analytics**: especifique a expressão CRON para obter relatórios do Adobe Analytics. O valor padrão é 0 0 2 ? &#42; &#42;.

   * **Tempo limite de busca de relatório:** Especifique a duração, em segundos, para aguardar a resposta do servidor ao relatório de análise. O tempo padrão é de 120 segundos.

   >[!NOTE]
   >
   >Pode levar até 10 segundos a mais para atingir o tempo limite da operação de busca de relatórios e, em seguida, o número especificado de segundos.

1. Repita as etapas 1 a 3 na instância de publicação para configurar o Analytics.

Agora é possível habilitar a análise de formulários e gerar um relatório de análise.

## Ativação do Analytics para um formulário ou documento {#enabling-analytics-for-a-form-or-document}

1. Fazer logon no portal AEM em `https://[hostname]:'port'`.
1. Clique em **Forms > Forms e documentos**, selecione um formulário ou documento e clique em **Ativar o Analytics**. A análise está ativada.

   ![Ativação do Analytics para um formulário ou documento](assets/enable-analytics-1.png)

   Ativação do Analytics para um formulário

   **A.** Botão Ativar o Analytics **B.** Formulário selecionado

   Para obter informações detalhadas sobre a exibição de relatórios de análise de formulários, consulte [Visualização e compreensão de relatórios do AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).
