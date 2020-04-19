---
title: Apresentação do site de referência We.Gov
seo-title: Apresentação do site de referência We.Gov
description: Use usuários e grupos fictícios para executar tarefas do AEM Forms usando o pacote de demonstração We.Gov.
seo-description: Use usuários e grupos fictícios para executar tarefas do AEM Forms usando o pacote de demonstração We.Gov.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Apresentação do site de referência We.Gov{#we-gov-reference-site-walkthrough}

## Pré-requisitos {#pre-requisites}

Configure o site de referência conforme descrito em [Configurar e configurar o site](../../forms/using/forms-install-configure-gov-reference-site.md)de referência We.Gov.

## História do usuário {#user-story}

* Formulários AEM

   * Captura de dados
   * Integração de dados (MS Dynamics)
   * Adobe Sign

* Fluxo de trabalho
* Comunicações do cliente

   * Canal de impressão
   * Canal da Web

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

O pacote demo We.Gov vem com os seguintes usuários fictícios incorporados:

* **Aya Tan**: Cidadão elegível para um serviço de uma agência governamental

![Usuário fictício](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Analista de negócios da agência We.Gov

![Usuário fictício](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Chefe do We.Gov Agency CX

![Usuário fictício](/help/forms/using/assets/camila_santos.png)

Os seguintes grupos também estão incluídos:

* **Usuários do Forms We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)

* **Usuários do We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)
   * Aya Tan (membro)

### Legenda dos termos de visão geral da demonstração {#demo-overview-terms-legend}

1. **Representar**: Usuários e grupos definidos na demonstração do AEM.
1. **Botão**: Retângulo colorido ou seta circulada para navegação.
1. **Clique**: Para executar uma ação na história do usuário.
1. **Links**: Localizado na parte superior do menu principal no site We.Gov.
1. **Instruções** do usuário: Um conjunto de etapas numéricas a serem seguidas ao navegar pela história do usuário.
1. **Portal** de formulários: *https://&lt;aemserver>:&lt;porta>/content/we-gov/formsportal.html*
1. **Visualização** móvel: usuário We.Gov para replicar uma visualização móvel com um navegador redimensionado.
1. **Visualização** da área de trabalho: Usuário do We.gov para demonstração de visualização em um laptop ou desktop.
1. **Formulário** de pré-filtragem: Formulário no Home page do site We.Gov.
1. **Formulário** adaptável: Formulário de aplicativo de inscrição para demonstração We.gov.

   *https://&lt;aemserver>:&lt;porta>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Site** do Adobe We.Gov: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. **Caixa de entrada** da Adobe: Localizado o ícone [Bell da barra de menus superior](assets/bell.svg) no backend do AEM.

   *https://&lt;aemserver>:&lt;porta>/aem/start.html*

1. **Cliente** de email: Maneira preferencial de visualização de e-mails (Gmail, Outlook)
1. **CTA**: Chamada à ação
1. **Navegar**: Para localizar um ponto de referência específico na página do navegador.

## Demonstração da visualização móvel {#mobile-view-demo}

**Esta seção deve ser realizada antes da manifestação.**

**Instruções do usuário:**

1. Navegue até: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Faça logon com:

   1. **Usuário**: aya.tan
   1. **Senha**: password

1. Redimensione a janela do navegador ou use o emulador do navegador para replicar um tamanho de dispositivo móvel.

### História do usuário Aya (site We.Gov) {#aya-user-story-we-gov-website}

![Usuário fictício](/help/forms/using/assets/aya_tan_new-1.png)

**Esta seção**: Aya é um cidadão. Ela ouve de uma amiga que pode ser qualificada para receber um Serviço de uma agência governamental. Aya navega até o website We.Gov de seu celular para saber mais sobre os serviços para os quais ela está qualificada.

### História do usuário Aya (pré-telas We.Gov) {#aya-user-story-we-gov-pre-screener}

Aya responde a algumas perguntas para confirmar sua qualificação preenchendo um pequeno formulário adaptativo em seu celular.

**Instruções do usuário:**

1. Faça uma seleção em cada campo suspenso.

   >[!NOTE]
   >
   >Se o usuário ganhar mais de US$ 200.000/ano, ele não será elegível.

1. Clique em &quot;**Sou elegível?**” botão.
1. Clique no botão &quot;**Aplicar agora**&quot; para continuar.

   ![Link Aplicar agora](/help/forms/using/assets/apply_now_link.png)

### História do usuário Aya (formulário adaptativo We.Gov) {#aya-user-story-we-gov-adaptive-form}

Aya descobre que ela é qualificada e começa a preencher seu pedido para solicitar serviço em seu dispositivo móvel.

Qualquer pessoa precisa revisar alguns documentos em casa antes de poder concluir a solicitação de serviço. Ela salva e sai do aplicativo.

**Instruções do usuário:**

1. Preencha os campos Informações básicas; os campos a seguir são obrigatórios e os menus suspensos:

   1. Informações básicas

      1. Nome
      1. Nome do meio
      1. Sobrenome
      1. Nome preferencial
      1. DOB
      1. Sexo
   1. Informações de contato

      1. Rua Endereço
      1. Cidade
      1. Número de telefone
      1. CEP
      1. E-mail
      1. Estado
   1. Status marcial

      1. Status da família



1. Use a seguinte lógica **** dinâmica para demonstrar o recurso dinâmico usando a lista suspensa Status **da** família:

   1. **Único**: Mostrar próximo ao painel de parentes
   1. **Casado**: Mostrar painel dependente do casamento
   1. **Divorciado**: Mostrar próximo ao painel de parentes
   1. **Viúvo**: Mostrar próximo ao painel de parentes
   1. **Você tem filhos?**: Botão de opção (Sim/Não) para mostrar o painel dependente do filho.

      1. (Adicionar/Remover) para adicionar/remover vários painéis dependentes.

1. Clique na seta para a direita na barra de menus cinza.
1. Clique no botão Salvar na parte inferior.

   ![Detalhes do formulário adaptável](/help/forms/using/assets/adaptive_form.png)

## Demonstração do desktop {#desktop-demo}

**Esta seção:** Em casa, Aya encontrou as informações de que precisava e retirou o aplicativo do desktop. Aya navega até o portal de formulários online para retomar seu aplicativo. Com uma simples personalização, as agências também podem gerar e enviar automaticamente por email um link para retomar o aplicativo.

### História do usuário Aya (formulário adaptativo contínuo) {#aya-user-story-continued-adaptive-form}

**Instruções do usuário:**

1. Navegue até *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Na barra de navegação, selecione clique em &quot;Serviços **** online&quot;.
1. No painel &quot;Formulários de rascunho&quot;, selecione o &quot;Aplicativo de inscrição para benefícios de saúde&quot; existente.

   ![Aplicativo de Inscrição para Benefícios de Integridade](/help/forms/using/assets/enrollment_application.png)

   A aparência é a mesma, e ela não precisa reinserir nenhum dado.

   **Instruções do usuário:**

1. Clique à direita em Círculo CTA para ir para a próxima seção.

   ![Círculo direito CTA](/help/forms/using/assets/right_circle_cta_new.png)

   O formulário é preenchido até o ponto da última entrada do Aya. Aya inseriu todas as suas informações e está pronta para enviar.

   ![Enviar o formulário adaptativo](/help/forms/using/assets/submit_adaptive_form.png)

   Depois de enviar a Aya, ela recebe um email que abre e está pronta para assinar eletronicamente com o Adobe Sign.

**Instruções do usuário:**

1. Após o envio, uma página de agradecimento será exibida.
1. Navegue até seu Cliente de email e localize o email do Adobe Sign.
1. Clique no link para o Adobe Sign.

   ![Adobe sign link](/help/forms/using/assets/adobe_sign_link.png)

**Instruções do usuário:**

1. Marque a caixa &quot;**Concordo**&quot;.
1. Clique em &quot;**Aceitar**&quot;.
1. Role até a parte inferior do documento revisado.
1. Clique na guia amarela realçada para assinar a documento.

   ![Assine o documento](/help/forms/using/assets/sign_document_new.png) ![Assine o documento de teste](/help/forms/using/assets/sign_test_document.png)

## Agente governamental (George) {#government-agent-george}

![Agente governamental George](/help/forms/using/assets/george_lang-1.png)

**Esta seção:** George é um analista de negócios da agência governamental Aya está solicitando um serviço. George tem um único painel onde ele pode ver todas as solicitações de serviço que lhe foram atribuídas para revisão.

### História do usuário George (Caixa de entrada do AEM) {#george-user-story-aem-inbox}

**Instruções do usuário:**

1. Navegue até *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Clique no ícone do usuário (canto superior direito) e use a opção de menu &quot;**Sair**&quot; ou &quot;**Representar como**&quot; se estiver conectado a um usuário administrativo.

   1. Faça logon com:

      1. **Usuário:** george.lang
      1. **Senha:** password
   1. Ou Representar:

      1. Digite &quot;**George**&quot; no campo &quot;**Representar como**&quot;.

      1. Clique em OK para representar.


1. No canto superior direito, clique no ícone Notificação (sino).
1. Clique em &quot;**Visualização tudo**&quot; para navegar até a Caixa de entrada.
1. Na Caixa de entrada, abra a tarefa mais recente &quot;Análise **do aplicativo de benefícios de** saúde&quot;.

   ![Revisão de Aplicativo de Benefícios à Saúde](/help/forms/using/assets/health_benefits.png)

### George User Story (Caixa de entrada do AEM e MS Dynamics) {#george-user-story-aem-inbox-and-ms-dynamics}

Graças às integrações de dados e aos workflows automatizados, o aplicativo Aya é exibido, juntamente com um registro CRM que foi gerado automaticamente quando os dados foram enviados.

**Instruções do usuário:**

1. Abra e inspecione o formulário adaptativo somente leitura.
1. Clique no botão &quot;**Abrir o MS Dynamics**&quot; para abrir o registro do MS Dynamics em uma nova janela.
1. No CRM, é possível visualizar todas as informações que podem ser atualizadas

   1. Opcionalmente, adicione algumas notas de revisão diretamente no Dynamics.

1. Feche e volte para a Caixa de entrada do AEM.

   ![Registro do MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### História do usuário do George (retornar à caixa de entrada do AEM) {#george-user-story-back-to-aem-inbox}

George aprova o aplicativo de Aya e, graças a um fluxo de trabalho automatizado existente, um email de confirmação também é enviado para Aya.

**Instruções do usuário:**

1. Navegue até o canto superior esquerdo e clique em &quot;**Aprovar**&quot; para aprovar o aplicativo.
1. No modal, você pode deixar uma mensagem para o cliente potencial CX.
1. Clique em Concluído.
1. (Função de cidadão) Abra seu cliente de e-mail para visualização do e-mail enviado para Aya.

   ![Visualização do email enviado para Aya](/help/forms/using/assets/email_client.png)

## Chumbo CX (Camila) {#cx-lead-camila}

![Camila (cliente potencial CX)](/help/forms/using/assets/camila_santos-1.png)

**Esta seção:** Camila, a líder do CX, faz uma chamada telefônica bem-vinda com a Aya para explicar como usar os serviços governamentais para os quais ela foi aprovada.

### História do usuário do Camila (Caixa de entrada do AEM e Microsoft Dynamics) {#camila-user-story-aem-inbox-ms-dynamics}

**Instruções do usuário:**

1. Navegue até *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Clique no ícone do usuário (canto superior direito) e use a opção de menu &quot;**Sair**&quot; ou &quot;**Representar como**&quot; se estiver conectado a um usuário administrativo.

   1. Faça logon com:

      1. **Usuário**: camila.santos
      1. **Senha**: password
   1. Ou Representar:

      1. Digite &quot;**Camila**&quot; no campo &quot;**Representar como**&quot;.

      1. Clique em OK para representar.


1. No canto superior direito, clique no ícone Notificação (sino).
1. Clique em &quot;**Visualização tudo**&quot; para navegar até a Caixa de entrada.
1. Na Caixa de entrada, abra a tarefa &quot;**Nova aprovação** de contato&quot; mais recente.

   ![Nova Aprovação de Contato](/help/forms/using/assets/new_contact_approval.png)

   **Instruções do usuário:**

1. Abra e inspecione o formulário adaptativo somente leitura.
1. Clique no botão &quot;**Abrir o MS Dynamics**&quot; para abrir o registro do MS Dynamics em uma nova janela.
1. No CRM, é possível visualizar todas as informações que podem ser atualizadas

   1. Como opção, adicione uma nova atividade de chamada diretamente no Dynamics.
   1. Abra a seção &quot;**Atividade**&quot;.
   1. Clique na opção &quot;**Nova chamada** telefônica&quot;.
   1. Adicione detalhes de chamada telefônica.
   1. Salve e feche a janela.

1. De volta ao AEM, navegue até o canto superior esquerdo e clique em &quot;**Enviar**&quot; para enviar o aplicativo.
1. No modal, você pode deixar uma mensagem.
1. Clique em Concluído.

   ![Guia](/help/forms/using/assets/activities_tab.png) Atividade ![Confirmar Novo Contato](/help/forms/using/assets/confirm_new_contact.png)

## Cidadão do Kit de Boas-vindas (Aya) {#welcome-kit-citizen-aya}

**Esta seção:** Qualquer usuário recebe um email com um link para uma comunicação interativa que resume seus benefícios e também inclui campos de formulário para preenchimento. Com a declaração de benefícios do PDF anexada e um link para a carta de comunicação interativa no email (com o mesmo tema/marca da comunicação interativa).

### História do usuário Aya (cliente de email) {#aya-user-story-email-client}

**Instruções do usuário:**

1. Localize e abra o e-mail do kit de boas-vindas.
1. Role até o anexo PDF na parte inferior da página.
1. Clique para abrir o anexo PDF.
1. Role de volta para o seu cliente de e-mail e clique em &quot;Kit de boas-vindas **Visualização online**&quot;.

   1. Isso abrirá a versão do canal da Web do mesmo documento.

1. Para obter uma referência rápida ao PDF diretamente:

   *https://&lt;aemserver>:&lt;porta>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Para uma referência rápida ao IC diretamente:

   *https://&lt;aemserver>:&lt;porta>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?canal=web&amp;mode=pré-visualização&amp;wcmmode=disabled*

   ![Link de Comunicação](/help/forms/using/assets/welcome_benefits_handbook.png) Interativa do Manual ![de Benefícios de Boas-Vindas](/help/forms/using/assets/interactive_communication.png)

## Renewal Lembrete (Aya) {#renewal-reminder-citizen-aya}

**Esta seção:** Camila também agenda um lembrete de comunicação, então um ano depois. (Etapa do fluxo de trabalho que automatiza/executa e-mail).

### História do usuário Aya (cliente de email) {#aya-user-story-email-client-1}

**Instruções do usuário:**

1. Navegue até seu cliente de email.
1. Localize e abra o e-mail Renewal Lembrete.
1. Clique no botão &quot;**Enviar um novo aplicativo**&quot; para abrir o formulário adaptável.

   1. Esta seção é intencionalmente deixada vazia para suportar o pré-preenchimento de dados na fase 2.
   ![Email do lembrete de renovação](/help/forms/using/assets/renewal_reminder_email.png)

## líder do Analytics CX (Camila) {#analytics-cx-lead-camila}

**Esta seção:** Camila navega até um painel onde ela pode ver em todo o KPI da agência, como % dos cidadãos que start preenchem um formulário de solicitação de serviço e abandonam, o tempo médio desde a submissão de solicitação até a resposta de aprovação/negação, e estatísticas de envolvimento para os manuais de benefícios que ela enviou aos cidadãos.

### Camila analisa o relatórios Sites (We.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Navegue até *https://&lt;aemserver>:&lt;porta>/sites.html/content*
1. Selecione &quot;Site **We.Gov do** AEM Forms&quot; para visualização nas páginas do site.
1. Selecione uma da página do site (por exemplo, Início) e escolha &quot;**Analytics &amp; Recommendations**&quot;.

   ![Analytics e Recomendações](/help/forms/using/assets/analytics_recommendation.jpg)

1. Nesta página, você verá informações obtidas do Adobe Analytics que pertencem à página Sites do AEM (OBSERVAÇÃO: por padrão, essas informações são atualizadas periodicamente do Adobe Analytics e não são exibidas em tempo real).

   ![Métricas principais do Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De volta à página de visualização da página (acessada na etapa 3.), você também pode visualização as informações de visualização da página alterando a configuração de exibição para itens de visualização na &quot;Visualização **de** Lista&quot;.
1. Localize o menu suspenso &quot;**Visualização**&quot; e selecione &quot;Visualização **de** Lista&quot;.

   ![visualização da Lista no menu suspenso Visualização](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. No mesmo menu, selecione &quot;Configuração **de** Visualização&quot; e selecione as colunas que deseja exibir na seção &quot;**Analytics**&quot;.

   ![Configurar a exibição de colunas](/help/forms/using/assets/view_setting_analytics.jpg)

1. Clique em &quot;**Atualizar**&quot; para disponibilizar as novas colunas.

   ![Disponibilizar novas colunas](/help/forms/using/assets/new_columns_available.jpg)

### Camila revisa o relatórios de formulários (We.Gov Adobe Analytics) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Vá até

   *https://&lt;aemserver>:&lt;porta>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Selecione o formulário adaptativo &quot;Aplicativo de **inscrição para benefícios** de saúde&quot; e selecione a opção &quot;Relatório **do** Analytics&quot;.

   ![Aplicativo de Inscrição para Benefícios de Integridade](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Aguarde a página ser carregada e visualização nos dados do relatório do Analytics.

   ![Dados de relatório do Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)

