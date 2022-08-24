---
title: Apresentação do site de referência We.Gov e We.Finance
seo-title: We.Gov and We.Finance reference site walkthrough
description: Use usuários e grupos fictícios para executar tarefas do AEM Forms usando o pacote de demonstração We.Gov e We.Finance.
seo-description: Use fictitious users and groups to perform AEM Forms tasks using We.Gov and We.Finance demo package.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 1%

---

# Apresentação do site de referência We.Gov e We.Finance {#we-gov-reference-site-walkthrough}

## Pré-requisitos {#pre-requisites}

Configure o site de referência conforme descrito em [Configurar e configurar o site de referência do We.Gov e do We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## História do usuário {#user-story}

* AEM Forms

   * Conversão automática dos formulários
   * Criação  
   * Modelos de dados do formulário/Fontes de dados

* AEM Forms

   * Captura de dados
   * (Opcional) Integração de dados (MS Dynamics)
   * (Opcional) Adobe Sign

* Fluxo de trabalho
* Notificações por email
* (Opcional) Comunicações do cliente

   * Canal de impressão
   * Canal da Web

* Adobe Analytics
* Integrações da fonte de dados

### Usuários e grupos fictícios {#fictitious-users-and-groups}

O pacote de demonstração We.Gov vem com os seguintes usuários fictícios integrados:

* **Aya Tan**: Cidadão elegível para um Serviço de uma agência governamental

![Usuário fictício](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Agência We.Gov - Analista de negócios

![Usuário fictício](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Líder da Agência de Governação da We.Gov CX

![Usuário fictício](/help/forms/using/assets/camila_santos.png)

Os seguintes grupos também estão incluídos:

* **Usuários do We.Gov Forms**

   * George Lang (membro)
   * Camila Santos (membro)

* **Usuários do We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)
   * Aya Tan (membro)

### Legenda de termos de visão geral da demonstração {#demo-overview-terms-legend}

1. **Representar**: Usuários e grupos definidos AEM demonstração.
1. **Botão**: Retângulo colorido ou seta em círculo para navegação.
1. **Clique em**: Para executar uma ação na história do usuário.
1. **Links**: Localizado na parte superior do menu principal do site We.Gov.
1. **Instruções do usuário**: Um conjunto de etapas numéricas a serem seguidas ao navegar pela história do usuário.
1. **Forms Portal**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Exibição móvel**: usuário We.Gov para replicar uma visualização móvel com um navegador redimensionado.
1. **Exibição da área de trabalho**: Usuário do We.gov para visualizar a demonstração em um laptop ou desktop.
1. **Formulário de pré-filtragem**: Formulário na página inicial do site We.Gov.
1. **Formulário adaptável**: Formulário de aplicativo de inscrição para demonstração We.gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Site Adobe We.Gov**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Caixa de entrada Adobe**: Barra de menu superior localizada [Ícone Bell](assets/bell.svg) em AEM back-end.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Cliente de email**: Maneira preferencial de visualizar seus emails (Gmail, Outlook)
1. **CTA**: Chamada à ação
1. **Navegar**: Para localizar um ponto de referência específico na página do navegador.
1. **AFC**: automated forms conversion

## automated forms conversion (Camila) {#automated-forms-conversion}

**Esta seção**: Camila o líder CX tem um formulário PDF existente que foi usado como parte de um processo em papel. Como parte de um esforço de modernização, ela deseja usar esse formulário PDF para criar automaticamente um novo Adaptive Forms moderno.

### automated forms conversion - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Navegar para *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Faça logon com:
   * **Usuário**: camila.santos
   * **Senha**: senha
1. Na página principal, selecione Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC.
1. Camila faz o upload do PDF para o AEM Forms.

   ![Carregar formulário](assets/aftia-upload-form.jpg)

1. Camila, em seguida, seleciona o formulário PDF e os cliques **Iniciar Conversão Automatizada** para iniciar o processo de conversão. Talvez seja necessário clicar em **Substituir conversão** se você tiver convertido o formulário.

   >[!NOTE]
   >
   >Observe que as configurações no AFC são predefinidas para o usuário final, o que significa que elas não devem ser alteradas.

   * **Opcional**: Se desejar usar o tema Accessible Ultramarine, basta clicar no ícone Especificar um tema de formulário adaptável e selecionar o tema Accessible-Ultramarine que aparece na lista de opções.

   ![Iniciar conversão](assets/aftia-start-conversion.jpg)

   ![Tema ultramarino](assets/aftia-upload-conversion-settings.jpg)

   O status da porcentagem concluída é exibido durante a conversão. Quando o status for exibido **Convertido**, clique no botão **output** selecione o formulário adaptável e clique em **Editar** para abrir o formulário convertido.

1. O Camilla então revisa o formulário e garante que todos os campos estejam presentes

   ![Revisar conversão](assets/aftia-review-conversion.jpg)

1. O Camilla começa a editar o formulário. Ela seleciona Painel raiz > Editar (a chave) > seleciona Guias na parte superior no menu suspenso Layout do painel > seleciona a caixa Verificar.

   ![Revisar propriedades](assets/aftia-review-properties.jpg)

1. Em seguida, Camilla adiciona todas as alterações de CSS e campo necessárias para produzir o produto final.

   ![Adicionar CSS](assets/aftia-add-css.jpg)

### Modelo de dados de formulário e fontes de dados (Camila) {#data-sources}

**Esta seção**: Depois que o documento tiver sido convertido e produzido um formulário adaptável, Camila precisará conectar o formulário adaptável a uma fonte de dados.

1. Camila abre as Propriedades no formulário que foi convertido em [automated forms conversion - We.Gov](#automated-forms-conversion-wegov).

1. Camila então seleciona Modelo de formulário > Seleciona o Modelo de dados de formulário na lista suspensa Selecionar de > Seleciona o FDM de inscrição We.gov na lista de opções.

1. Cliques no botão Salvar e fechar.

   ![Seleção do FDM](assets/aftia-select-fdm.jpg)

1. Camila clica no botão **output** , seleciona o formulário adaptável e clica em **Editar** para abrir o formulário We.Gov preenchido.
1. Camila seleciona um campo de formulário adaptável e clica em ![Ícone Configurar](assets/configure-icon.svg). Ela cria vínculo com as entidades do modelo de dados de formulário usando o **Referência de associação** campo. Ela repete essa etapa para todos os campos no formulário adaptável.

### Teste de acessibilidade de formulário (Camila) {#form-accessibility-testing}

Camila também valida que o conteúdo criado é criado de forma correta e totalmente acessível, de acordo com os padrões corporativos.

1. Camila clica no botão **output** , seleciona o formulário adaptável e clica em **Visualizar** para abrir o formulário We.Gov preenchido.

1. Abre a guia Auditoria na Ferramenta de desenvolvedor do Chrome.

1. Executa uma verificação de acessibilidade para validar o formulário adaptável.

   ![Verificação de acessibilidade](assets/aftia-accessibility.jpg)

## Demonstração De Exibição Móvel Do Formulário Adaptável (Aya) {#mobile-view-demo}

**Esta seção deve ser executada antes da demonstração.**

**Instruções do usuário:**

1. Navegue até: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Faça logon com:

   1. **Usuário**: aya.tan
   1. **Senha**: senha

1. Redimensione a janela do navegador ou use o emulador do navegador para replicar um tamanho de dispositivo móvel.

### Site We.Gov (Aya) {#aya-user-story-we-gov-website}

![Usuário fictício](/help/forms/using/assets/aya_tan_new-1.png)

**Esta seção**: Aya é cidadão. Ela ouve de um amigo que pode ser elegível para receber um Serviço de uma agência governamental. Aya navega até o site We.Gov de seu celular para saber mais sobre os serviços para os quais ela está qualificada.

### Pré-Telas We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya responde algumas perguntas para confirmar sua qualificação preenchendo um pequeno formulário adaptável em seu celular.

**Instruções do usuário:**

1. Faça uma seleção em cada campo suspenso.

   >[!NOTE]
   >
   >Se o usuário ganhar mais de US$ 200.000/ano, ele não estará qualificado.

1. Clique no &quot;**Posso?**&quot; botão.
1. Clique no &quot;**Aplicar agora**&quot; para continuar.

   ![Link Aplicar agora](/help/forms/using/assets/apply_now_link.png)

### Formulário Adaptável We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya descobre que ela está qualificada e começa a preencher seu aplicativo para solicitar serviço em seu dispositivo móvel.

Qualquer pessoa precisa revisar alguns documentos em casa antes de concluir o aplicativo de solicitação de serviço. Ela salva e sai do aplicativo de seu dispositivo móvel.

**Instruções do usuário:**

1. Preencha os campos Basic information , os seguintes são campos obrigatórios e lista suspensa:

   1. Informações básicas

      1. Nome
      1. Sobrenome
      1. DOB
      1. Email

1. Use o seguinte **lógica dinâmica** para demonstrar o recurso dinâmico usando o **Status da família** lista suspensa:

   1. **Único**: Mostrar próximo do painel de parentesco
   1. **Casado**: Mostrar painel dependente do marital
   1. **Divorciado**: Mostrar próximo do painel de parentesco
   1. **Viúvo**: Mostrar próximo do painel de parentesco
   1. **Você tem filhos?**: Botão de opção (Sim/Não) para mostrar o painel dependente do filho.

      1. Botão (Adicionar/Remover) para adicionar/remover vários painéis dependentes de filhos.

1. Clique na seta para a direita na barra de menu cinza.
1. Clique no botão Save na parte inferior.

   ![Detalhes do formulário adaptável](/help/forms/using/assets/adaptive_form.png)

## Demonstração do desktop {#desktop-demo}

**Esta seção:** Em casa, Aya encontrou as informações de que precisava e retomou o aplicativo do desktop. Qualquer um navega até o portal de formulários online para retomar seu aplicativo. Com uma personalização simples, as agências também podem gerar e enviar por email automaticamente um link para retomar o aplicativo.

### Formulário Adaptável Continuado (Aya) {#aya-user-story-continued-adaptive-form}

**Instruções do usuário:**

1. Navegar para *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Na barra de navegação, selecione clique em &quot;**Serviços online**&quot;.
1. No painel &quot;Rascunho de Forms&quot;, selecione o &quot;Aplicativo de Inscrição para Benefícios de Saúde&quot; existente.

   ![Aplicativo de Inscrição para Benefícios de Integridade](/help/forms/using/assets/enrollment_application.png)

   A aparência é a mesma e ela não precisa inserir dados novamente.

   **Instruções do usuário:**

1. Clique em CTA do círculo à direita para ir até a próxima seção.

   ![Círculo direito CTA](/help/forms/using/assets/right_circle_cta_new.png)

   O formulário é preenchido até o ponto da última entrada do Aya. Aya inseriu todas as suas informações e está pronta para enviar.

   ![Enviar o formulário adaptável](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Quando Aya preenche o campo de número de telefone, deve preenchê-lo como um número contínuo de 11 dígitos sem traços, espaços ou hifens.

   Depois de enviar, o Aya recebe uma página de agradecimento. Opcionalmente, ela também receberá um email que poderá abrir para assinar o documento de registro eletronicamente com o Adobe Sign.

### Opcional: Adobe Sign (Aya) {#adobe-sign}

**Instruções do usuário:**

1. Navegue até seu Cliente de email e localize o email do Adobe Sign.
1. Clique no link para Adobe Sign.

   ![Link Adobe sign](/help/forms/using/assets/adobe_sign_link.png)

**Instruções do usuário:**

1. Verifique o &quot;**Concordo**&quot;caixa.
1. Clique em &quot;**Aceitar**&quot;.
1. Role até a parte inferior do documento revisado.
1. Clique na guia amarela realçada para assinar o documento.

   ![Assinar o documento](/help/forms/using/assets/sign_document_new.png) ![Assinar o documento de teste](/help/forms/using/assets/sign_test_document.png)

## Agente governamental (George) {#government-agent-george}

![Agente governamental George](/help/forms/using/assets/george_lang-1.png)

**Esta seção:** George é um analista de negócios da agência governamental Aya está solicitando um serviço. George tem um único painel onde pode ver todos os aplicativos de solicitação de serviço que foram atribuídos a ele para revisão.

### Caixa de entrada AEM (George) {#george-user-story-aem-inbox}

**Instruções do usuário:**

1. Navegar para *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Clique no ícone do usuário (canto superior direito) e use o &quot;**Fazer logoff**&quot;, ou o &quot;**Representar como**&quot; se você estiver conectado com um usuário administrativo.

   1. Faça logon com:

      1. **Usuário:** george.lang
      1. **Senha:** senha
   1. Ou Representar:

      1. Tipo &quot;**George**&quot; no &quot;**Representar como**&quot;.

      1. Clique em OK para representar.


1. No canto superior direito, clique no ícone Notificação (sino).
1. Clique em &quot;**Exibir todos**&quot; para navegar até a Caixa de entrada.
1. Na Caixa de entrada, abra o &quot; mais recente **Revisão da Aplicação de Benefícios de Saúde**&quot; tarefa.

   ![Revisão da Aplicação de Benefícios de Saúde](/help/forms/using/assets/health_benefits.png)

### Opcional: AEM Caixa de entrada e MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Graças às integrações de dados e aos fluxos de trabalho automatizados, o aplicativo do Aya é exibido, juntamente com um registro de CRM que foi gerado automaticamente quando os dados foram enviados.

**Instruções do usuário:**

1. Abra e inspecione o formulário adaptável somente leitura.
1. Clique no &quot;**Abrir o MS Dynamics**&quot; para abrir o registro do MS Dynamics em uma nova janela.
1. No CRM, você pode ver todas as informações que podem ser atualizadas

   1. Como opção, adicione algumas notas de revisão diretamente no Dynamics.

1. Feche e volte para AEM Caixa de entrada.

   ![Registro do MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Voltar para AEM Caixa de Entrada (George) {#george-user-story-back-to-aem-inbox}

George aprova o aplicativo de Aya e, graças a um fluxo de trabalho automatizado existente, um email de confirmação também é enviado para Aya.

**Instruções do usuário:**

1. Navegue até o canto superior esquerdo e clique em &quot;**Aprovar**&quot; para aprovar o pedido.
1. Na modal, é possível deixar uma mensagem para o cliente potencial do CX.
1. Clique em Concluído.
1. (Função de cidadão) Abra seu cliente de email para visualizar o email enviado para o Aya.

   ![Exibir o email enviado para o Aya](/help/forms/using/assets/email_client.png)

## Líder CX (Camila) {#cx-lead-camila}

![Camila (cliente potencial CX)](/help/forms/using/assets/camila_santos-1.png)

**Esta seção:** Camila, o líder do CX, faz uma chamada telefônica bem-vinda com a Aya para explicar como usar os serviços governamentais para os quais ela foi aprovada.

### (Opcional) AEM Caixa de entrada e MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Instruções do usuário:**

1. Navegar para *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Clique no ícone do usuário (canto superior direito) e use o &quot;**Fazer logoff**&quot;, ou o &quot;**Representar como**&quot; se você estiver conectado com um usuário administrativo.

   1. Faça logon com:

      1. **Usuário**: camila.santos
      1. **Senha**: senha
   1. Ou Representar:

      1. Tipo &quot;**Camila**&quot; no &quot;**Representar como**&quot;.

      1. Clique em OK para representar.


1. No canto superior direito, clique no ícone Notification (bell) .
1. Clique em &quot;**Exibir todos**&quot; para navegar até a Caixa de entrada.
1. Na Caixa de entrada, abra o &quot; mais recente **Nova Aprovação de Contato**&quot; tarefa.

![Nova Aprovação de Contato](/help/forms/using/assets/new_contact_approval.png)

**(Opcional) Instruções do usuário:**

1. Abra e inspecione o formulário adaptável somente leitura.
1. Clique no &quot;**Abrir o MS Dynamics**&quot; para abrir o registro do MS Dynamics em uma nova janela.
1. No CRM, você pode ver todas as informações que podem ser atualizadas

   1. Como opção, adicione uma nova atividade de chamada diretamente no Dynamics.
   1. Abra o &quot;**Atividades** seção &quot;.
   1. Clique no &quot;**Nova chamada telefônica**&quot;.
   1. Adicione detalhes de chamada telefônica.
   1. Salve e feche a janela .

1. De volta ao AEM, navegue até o canto superior esquerdo e clique em &quot;**Enviar**&quot; para apresentar o pedido.
1. Na modal , é possível deixar uma mensagem.
1. Clique em Concluído.

   ![Guia Atividades](/help/forms/using/assets/activities_tab.png) ![Confirmar Novo Contato](/help/forms/using/assets/confirm_new_contact.png)

## (Opcional) Kit De Boas-Vindas Cidadão (Aya) {#welcome-kit-citizen-aya}

**Esta seção:** O Aya recebe um email contendo um link para uma comunicação interativa que resume seus benefícios e também inclui campos de formulário a serem preenchidos. Com declaração PDF benefícios anexada e link para a carta de comunicação interativa no email (com o mesmo tema/marca da comunicação interativa).

### Notificação De Cliente De Email (Aya) {#aya-user-story-email-client}

**Instruções do usuário:**

1. Localize e abra o email do kit de boas-vindas.
1. Role até PDF attachment na parte inferior da página.
1. Clique em para abrir o anexo PDF.
1. Role para cima em seu cliente de email e clique em &quot;**Exibir kit de boas-vindas online**&quot;.

   1. Isso abrirá a versão do canal da Web do mesmo documento.

1. Para obter uma referência rápida ao PDF diretamente:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Para uma referência rápida ao CI diretamente:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Manual de benefícios de boas-vindas](/help/forms/using/assets/welcome_benefits_handbook.png) ![Link de comunicação interativa](/help/forms/using/assets/interactive_communication.png)

## Cidadão da Lembrete Renovável (Aya) {#renewal-reminder-citizen-aya}

**Esta seção:** Camila também programou um lembrete de comunicação para um ano depois. (Etapa do fluxo de trabalho que automatiza/executa e-mails).

### Notificação De Cliente De Email (Aya) {#aya-user-story-email-client-updated}

**Instruções do usuário:**

1. Navegue até seu cliente de email.
1. Localize e abra o email Lembrete de renovação .
1. Clique no &quot;**Enviar um novo aplicativo**&quot; para abrir o formulário adaptável.

   1. Esta seção é intencionalmente deixada em branco para suportar o pré-preenchimento de dados na fase 2.

   ![Email do lembrete de renovação](/help/forms/using/assets/renewal_reminder_email.png)

## (Opcional) Modelo de dados de formulário (Camila) {#form-data-model}

**Esta seção**: Camila navega até Integrações de dados da AEM Forms, onde pode executar um teste rápido para ver se as informações enviadas para a fonte de dados externa por meio da integração do Modelo de dados de formulário estão realmente presentes.

### Modelo de dados de formulário (Camila) {#form-data-model-camila}

**Esta seção**: Camila navega até a página Fontes de Dados para validar os dados que o servidor replicou no banco de dados Derby.

1. Quando a experiência do usuário estiver concluída e o envio do usuário tiver sido concluído, Camila navegará até a guia Fontes de dados no AEM Forms (**Forms** > **Integrações de dados**)

1. Camila e, em seguida, seleciona AEM Forms **We.gov FDM** e edite o **FDM de Inscrição We.gov**.

1. Camila e, em seguida, seleciona a variável **Contato** > **Serviço de leitura** a ensaiar.

   ![Serviço de leitura de contatos](assets/aftia-contact-read-service.jpg)

1. Camila fornece ao serviço de teste uma id de contato e, em seguida, clica no botão Testar. Por exemplo, 1 ou 2, se você tiver enviado o formulário. Se você não tiver enviado o formulário, nenhum dado será retornado.

   ![Serviço de leitura de contatos](assets/aftia-test-service.jpg)

1. Camila pode então validar se os dados foram inseridos com êxito na fonte de dados.

   * Os dados no Derby DS assemelham-se ao seguinte formato:

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## (Opcional) Analytics (Camila) {#analytics-cx-lead-camila}

**Esta seção:** Camila navega até um painel onde pode visualizar em todo o KPI da agência, como % dos cidadãos que começam a preencher um formulário de solicitação de serviço e abandonam, o tempo médio desde o envio da solicitação até a resposta de aprovação/negação, e as estatísticas de engajamento dos manuais de benefícios que ela enviou aos cidadãos.

### Relatórios de sites da Adobe Analytics (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Navegar para *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Selecione o &quot;**Site We.Gov do AEM Forms**&quot; para visualizar as páginas do site.
1. Selecione uma das páginas do site (por exemplo, Início) e escolha &quot;**Analytics &amp; Recommendations**&quot;.

   ![Analytics e Recomendações](/help/forms/using/assets/analytics_recommendation.jpg)

1. Nesta página, você verá informações buscadas no Adobe Analytics que pertencem à página do AEM Sites (OBSERVAÇÃO: por design, essas informações são atualizadas periodicamente da Adobe Analytics e não são exibidas em tempo real).

   ![Métricas principais do Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De volta à página de visualização (acessada na etapa 3.), você também pode visualizar as informações de visualização da página alterando a configuração de exibição para exibir itens no &quot;**Exibição de lista**&quot;.
1. Localize o &quot;**Exibir**&quot; e selecione &quot;**Exibição de lista**&quot;.

   ![Exibição de lista no menu suspenso Exibição](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. No mesmo menu, selecione &quot;**Exibir configuração**&quot; e selecione as colunas que deseja exibir no &quot;**Analytics** seção &quot;.

   ![Configurar a exibição de colunas](/help/forms/using/assets/view_setting_analytics.jpg)

1. Clique em &quot;**Atualizar**&quot; para disponibilizar as novas colunas.

   ![Disponibilizar novas colunas](/help/forms/using/assets/new_columns_available.jpg)

### Relatórios do Adobe Analytics Forms (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Vá até

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Selecione o &quot;**Aplicativo de Inscrição para Benefícios de Integridade**&quot; e selecione o &quot;**Relatório do Analytics**&quot;.

   ![Aplicativo de Inscrição para Benefícios de Integridade](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Aguarde até que a página seja carregada e exiba os dados do relatório do Analytics.

   ![Dados de relatório do Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
