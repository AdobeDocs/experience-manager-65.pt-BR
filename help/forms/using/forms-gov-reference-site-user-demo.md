---
title: Apresentação do site de referência do We.Gov e We.Finance
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

# Apresentação do site de referência do We.Gov e We.Finance {#we-gov-reference-site-walkthrough}

## Pré-requisitos {#pre-requisites}

Configure o site de referência conforme descrito em [Configurar o site de referência We.Gov e We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## História de usuário {#user-story}

* AEM Forms

   * Conversão automática dos formulários
   * Criação  
   * Modelos de dados de formulário/Fontes de dados

* AEM Forms

   * Captura de dados
   * (Opcional) Integração de dados (MS Dynamics)
   * (Opcional) Adobe Sign

* Fluxo de trabalho
* Notificações por email
* (Opcional) Comunicações ao cliente

   * Canal de impressão
   * Canal da Web

* Adobe Analytics
* Integrações da fonte de dados

### Usuários e grupos fictícios {#fictitious-users-and-groups}

O pacote de demonstração We.Gov vem com os seguintes usuários fictícios incorporados:

* **Aya Tan**: Cidadão qualificado para um Serviço de uma agência do governo

![Usuário fictício](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Analista de negócios da agência We.Gov

![Usuário fictício](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Líder da We.Gov Agency CX

![Usuário fictício](/help/forms/using/assets/camila_santos.png)

Os seguintes grupos também estão incluídos:

* **Usuários do Forms We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)

* **Usuários do We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)
   * Aya Tan (membro)

### Legenda dos termos da visão geral da demonstração {#demo-overview-terms-legend}

1. **Representar**: Usuários e grupos definidos na demonstração do AEM.
1. **Botão**: Retângulo colorido ou seta circulada para navegação.
1. **Clique em**: para executar uma ação na história do usuário.
1. **Links**: localizado na parte superior do menu principal do site We.Gov.
1. **Instruções do usuário**: um conjunto de etapas numéricas a serem seguidas ao navegar pela história do usuário.
1. **Portal Forms**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Exibição para dispositivos móveis**: Usuário do We.Gov para replicar uma visualização móvel com um navegador redimensionado.
1. **Modo de Exibição de Área de Trabalho**: usuário do We.gov para ver uma demonstração em um laptop ou desktop.
1. **Formulário de pré-triagem**: Formulário na página inicial do site We.Gov.
1. **Formulário adaptável**: Formulário de inscrição para demonstração do We.gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Site Adobe We.Gov**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Caixa de entrada do Adobe**: Barra de menu superior localizada [Ícone de Campainha](assets/bell.svg) no back-end do AEM.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Cliente de e-mail**: a maneira preferida de exibir seus emails (Gmail, Outlook)
1. **CTA**: Chamada para ação
1. **Navegar**: para localizar um ponto de referência específico na página do navegador.
1. **AFC**: AUTOMATED FORMS CONVERSION

## Automated forms conversion (Camila) {#automated-forms-conversion}

**Esta seção**: Camila, o CX Lead, tem um formulário baseado em PDF existente que foi usado como parte de um processo baseado em papel. Como parte de um esforço de modernização, ela deseja usar esse formulário de PDF para criar automaticamente um novo Forms adaptável moderno.

### Automated forms conversion - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Navegue até *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Fazer logon com:
   * **Usuário**: camila.santos
   * **Senha**: senha
1. Na página principal, selecione Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC.
1. Camila faz o upload do PDF para o AEM Forms.

   ![Carregar formulário](assets/aftia-upload-form.jpg)

1. Camilla seleciona o formulário PDF e clica em **Iniciar conversão automática** para iniciar o processo de conversão. Talvez seja necessário clicar em **Substituir conversão** se você tiver convertido o formulário.

   >[!NOTE]
   >
   >Observe que as configurações na AFC são pré-configuradas para o usuário final, o que significa que elas não devem ser alteradas.

   * **Opcional**: Se quiser usar o tema Acessível Ultramarine, basta clicar no botão Especificar um tema de formulário adaptável e selecionar o tema Acessível Ultramarine que aparece na lista de opções.

   ![Iniciar conversão](assets/aftia-start-conversion.jpg)

   ![Tema ultramarino](assets/aftia-upload-conversion-settings.jpg)

   O status da porcentagem concluída é exibido durante a conversão. Quando o status for exibido **Convertido**, clique no link **saída** selecione o formulário adaptável e clique em **Editar** para abrir o formulário convertido.

1. Camilla, então, revisa o formulário e garante que todos os campos estejam presentes

   ![Revisar conversão](assets/aftia-review-conversion.jpg)

1. Camilla então começa a editar o formulário. Ela seleciona Painel raiz > Editar (a chave inglesa) > seleciona Guias na parte superior do menu suspenso Layout do painel > marca a caixa de seleção.

   ![Revisar propriedades](assets/aftia-review-properties.jpg)

1. Em seguida, Camilla adiciona todas as alterações de CSS e de campo necessárias para produzir o produto final.

   ![Adicionar CSS](assets/aftia-add-css.jpg)

### Modelo de dados de formulário e fontes de dados (Camila) {#data-sources}

**Esta seção**: depois que o documento tiver sido convertido e produzido um Formulário adaptável, Camila precisará conectar o Formulário adaptável a uma fonte de dados.

1. Camila abre as Propriedades no formulário que foi convertido em [Automated forms conversion - We.Gov](#automated-forms-conversion-wegov).

1. Camila seleciona Modelo de formulário > Seleciona modelo de dados de formulário na lista suspensa Selecionar de > Seleciona We.gov Inscrição FDM na lista de opções.

1. Cliques no botão Salvar e fechar.

   ![Seleção de FDM](assets/aftia-select-fdm.jpg)

1. Camila clica no **saída** selecione o formulário adaptável e clique em **Editar** para abrir o formulário We.Gov preenchido.
1. Camila seleciona um campo de formulário adaptável e clica em ![Ícone Configurar](assets/configure-icon.svg). Ela cria associações com entidades de modelo de dados de formulário usando o **Referência de vinculação** campo. Ela repete essa etapa para todos os campos no formulário adaptável.

### Teste de acessibilidade de formulários (Camila) {#form-accessibility-testing}

Camila também valida se o conteúdo criado foi criado corretamente e se está totalmente acessível, de acordo com os padrões corporativos.

1. Camila clica no **saída** selecione o formulário adaptável e clique em **Visualizar** para abrir o formulário We.Gov preenchido.

1. Abre a guia Auditoria na Ferramenta de desenvolvedor do Chrome.

1. Executa uma verificação de Acessibilidade para validar o formulário adaptável.

   ![Verificação de acessibilidade](assets/aftia-accessibility.jpg)

## Demonstração Do Modo De Exibição Móvel Do Formulário Adaptável (Aya) {#mobile-view-demo}

**Esta seção deve ser executada antes da demonstração.**

**Instruções do usuário:**

1. Navegue até: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Fazer logon com:

   1. **Usuário**: aya.tan
   1. **Senha**: senha

1. Redimensione a janela do navegador ou use o emulador do navegador para replicar um tamanho de dispositivo móvel.

### Site Do We.Gov (Aya) {#aya-user-story-we-gov-website}

![Usuário fictício](/help/forms/using/assets/aya_tan_new-1.png)

**Esta seção**: Aya é uma cidadã. Ela ouve de uma amiga que ela pode ser elegível para receber um Serviço de uma agência do governo. Aya navega até o site We.Gov em seu celular para saber mais sobre os serviços para os quais está qualificada.

### Pré-Filtrador Do We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya responde a algumas perguntas para confirmar sua elegibilidade preenchendo um pequeno formulário adaptável em seu telefone celular.

**Instruções do usuário:**

1. Faça uma seleção em cada campo suspenso.

   >[!NOTE]
   >
   >Se o usuário ganhar mais de US$ 200.000/ano, não será qualificado.

1. Clique no ícone &quot;**Eu sou elegível?**&quot; botão.
1. Clique no ícone &quot;**Inscreva-se agora**&quot; para continuar.

   ![Link Aplicar agora](/help/forms/using/assets/apply_now_link.png)

### Formulário Adaptável Do We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya descobre que está qualificada e começa a preencher sua solicitação de serviço em seu dispositivo móvel.

Aya precisa revisar alguns documentos em casa antes de concluir a solicitação de serviço. Ela salva e sai do aplicativo do dispositivo móvel.

**Instruções do usuário:**

1. Preencha os campos Basic information (Informações básicas). Os campos e menus suspensos são os seguintes:

   1. Informações básicas

      1. Nome
      1. Sobrenome
      1. DOB
      1. Email

1. Use o seguinte **lógica dinâmica** para demonstrar o recurso dinâmico usando o **Status familiar** lista suspensa:

   1. **Solteiro**: Mostrar próximo do painel principal
   1. **Casado**: Mostrar painel dependente conjugal
   1. **Divorciado**: Mostrar próximo do painel principal
   1. **Viúvo**: Mostrar próximo do painel principal
   1. **Você tem filhos?**: botão de opção (Sim/Não) para mostrar o painel dependente filho.

      1. Botão (Adicionar/Remover) para adicionar/remover vários painéis dependentes filhos.

1. Clique na seta para a direita na barra de menu cinza.
1. Clique no botão Save na parte inferior.

   ![Detalhes do formulário adaptável](/help/forms/using/assets/adaptive_form.png)

## Demonstração do desktop {#desktop-demo}

**Esta seção:** De volta a casa, Aya encontrou as informações de que precisava e retoma o aplicativo a partir de seu desktop. Aya navega até o portal de formulários online para retomar seu aplicativo. Com alguma personalização simples, as agências também podem gerar e enviar automaticamente por email um link para retomar o aplicativo.

### Formulário adaptável contínuo (Aya) {#aya-user-story-continued-adaptive-form}

**Instruções do usuário:**

1. Navegue até *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Na barra de navegação, selecione clique em &quot;**Serviços Online**&quot;.
1. No painel &quot;Rascunho do Forms&quot;, selecione o &quot;Aplicativo de Inscrição para Benefícios de Saúde&quot; existente.

   ![Inscrição para Benefícios de Integridade](/help/forms/using/assets/enrollment_application.png)

   A aparência são as mesmas e ela não precisa inserir os dados novamente.

   **Instruções do usuário:**

1. Clique com o botão direito em Circular CTA para ir até a próxima seção.

   ![CTA de círculo direito](/help/forms/using/assets/right_circle_cta_new.png)

   O formulário é preenchido até o ponto da última entrada de Aya. Aya inseriu todas as informações e está pronto para enviar.

   ![Enviar o formulário adaptável](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Quando Aya preenche o campo de número de telefone, ela deve preenchê-lo como um número contínuo de 11 dígitos sem traços, espaços ou hifens.

   Depois de enviar, Aya recebe uma página de agradecimento. Como opção, ela também receberá um email que poderá abrir para assinar o documento de registro eletronicamente com o Adobe Sign.

### Opcional: Adobe Sign (Aya) {#adobe-sign}

**Instruções do usuário:**

1. Navegue até seu Cliente de e-mail e localize o e-mail do Adobe Sign.
1. Clique no link para o Adobe Sign.

   ![Link do sinal de Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Instruções do usuário:**

1. Marque a opção &quot;**Concordo**&quot;.
1. Clique em &quot;**Aceitar**&quot;.
1. Rolar para a parte inferior do documento revisado.
1. Clique na guia realçada em amarelo para assinar o documento.

   ![Assinar o documento](/help/forms/using/assets/sign_document_new.png) ![Assinar o documento de teste](/help/forms/using/assets/sign_test_document.png)

## Agente do governo (George) {#government-agent-george}

![Agente do governo George](/help/forms/using/assets/george_lang-1.png)

**Esta seção:** George é um analista de negócios da agência governamental Aya é um solicitante de um serviço da. George tem um único painel de controle no qual pode ver todos os aplicativos de solicitação de serviço que foram atribuídos a ele para análise.

### Caixa de entrada AEM (George) {#george-user-story-aem-inbox}

**Instruções do usuário:**

1. Navegue até *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Clique no ícone do usuário (canto superior direito) e use o &quot;**Sair**&quot; ou &quot;**Representar como**&quot; se você estiver conectado no momento com um usuário administrativo.

   1. Fazer logon com:

      1. **Usuário:** george.lang
      1. **Senha:** senha
   1. Ou representar:

      1. Tipo &quot;**George**&quot; na &quot;**Representar como**&quot;.

      1. Clique em OK para representar.


1. No canto superior direito, clique no ícone de Notificação (sino).
1. Clique em &quot;**Exibir todos**&quot; para navegar até a Caixa de entrada.
1. Na Caixa de entrada, abra o &quot; mais recente **Revisão de Aplicativo de Benefícios de Integridade**&quot;.

   ![Revisão de Aplicativo de Benefícios de Integridade](/help/forms/using/assets/health_benefits.png)

### Opcional: Caixa de entrada AEM e MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Graças às integrações de dados e aos fluxos de trabalho automatizados, o aplicativo de Aya é exibido junto com um registro de CRM que foi gerado automaticamente quando os dados foram enviados.

**Instruções do usuário:**

1. Abra e inspecione o formulário adaptável somente leitura.
1. Clique no ícone &quot;**Abrir MS Dynamics**&quot; para abrir o registro do MS Dynamics em uma nova janela.
1. No CRM, é possível ver todas as informações que podem ser atualizadas

   1. Opcionalmente, adicione algumas notas de revisão diretamente no Dynamics.

1. Feche e retorne à Caixa de entrada do AEM.

   ![Registro do MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Voltar para a caixa de entrada AEM (George) {#george-user-story-back-to-aem-inbox}

George aprova a inscrição de Aya e, graças a um fluxo de trabalho automatizado existente, um email de confirmação também é enviado a Aya.

**Instruções do usuário:**

1. Navegue até o canto superior esquerdo e clique em &quot;**Aprovar**&quot; para aprovar o aplicativo.
1. No modal, é possível deixar uma mensagem para o lead do CX.
1. Clique em Concluído.
1. (Função Cidadã) Abra seu cliente de email para ver o email enviado a Aya.

   ![Visualizar o email enviado para Aya](/help/forms/using/assets/email_client.png)

## Líder do CX (Camila) {#cx-lead-camila}

![Camila (CX lead)](/help/forms/using/assets/camila_santos-1.png)

**Esta seção:** Camila, a Líder do CX, faz um telefonema de boas-vindas com Aya para explicar como usar os serviços governamentais para os quais ela foi aprovada.

### (Opcional) Caixa de entrada AEM e MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Instruções do usuário:**

1. Navegue até *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Clique no ícone do usuário (canto superior direito) e use o &quot;**Sair**&quot; ou &quot;**Representar como**&quot; se você estiver conectado no momento com um usuário administrativo.

   1. Fazer logon com:

      1. **Usuário**: camila.santos
      1. **Senha**: senha
   1. Ou representar:

      1. Tipo &quot;**Camila**&quot; na &quot;**Representar como**&quot;.

      1. Clique em OK para representar.


1. No canto superior direito, clique no ícone Notificação (sino).
1. Clique em &quot;**Exibir todos**&quot; para navegar até a Caixa de entrada.
1. Na Caixa de entrada, abra o &quot; mais recente **Aprovação de novo contato**&quot;.

![Aprovação de novo contato](/help/forms/using/assets/new_contact_approval.png)

**(Opcional) Instruções para o usuário:**

1. Abra e inspecione o formulário adaptável somente leitura.
1. Clique no ícone &quot;**Abrir MS Dynamics**&quot; para abrir o registro do MS Dynamics em uma nova janela.
1. No CRM, é possível ver todas as informações que podem ser atualizadas

   1. Como opção, adicione uma nova atividade de chamada diretamente no Dynamics.
   1. Abra o &quot;**Atividades**&quot;.
   1. Clique no ícone &quot;**Nova Chamada Telefônica**&quot;.
   1. Adicionar detalhes da chamada telefônica.
   1. Salve e feche a janela.

1. De volta ao AEM, navegue até o canto superior esquerdo e clique em &quot;**Enviar**&quot; para enviar a solicitação de emprego.
1. Na modal, é possível deixar uma mensagem.
1. Clique em Concluído.

   ![Guia Atividades](/help/forms/using/assets/activities_tab.png) ![Confirmar novo contato](/help/forms/using/assets/confirm_new_contact.png)

## (Opcional) Welcome Kit Citizen (Aya) {#welcome-kit-citizen-aya}

**Esta seção:** Aya recebe um email com um link para uma comunicação interativa que resume seus benefícios e também inclui campos de formulário a serem preenchidos. Com a declaração de benefícios do PDF anexada e o link para a carta de comunicação interativa no e-mail (com o mesmo tema/marca como a comunicação interativa).

### Notificação De Cliente De Email (Aya) {#aya-user-story-email-client}

**Instruções do usuário:**

1. Localize e abra o email do kit de boas-vindas.
1. Role até o anexo PDF na parte inferior da página.
1. Clique em para abrir o anexo PDF.
1. Role para trás em seu cliente de e-mail e clique em &quot;**Exibir kit de boas-vindas online**&quot;.

   1. Isso abrirá a versão do canal da Web do mesmo documento.

1. Para uma referência rápida ao PDF diretamente:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Para uma referência rápida ao CI diretamente:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Manual de benefícios do Welcome](/help/forms/using/assets/welcome_benefits_handbook.png) ![Link de comunicação interativa](/help/forms/using/assets/interactive_communication.png)

## Cidadão lembrete da renovação (Aya) {#renewal-reminder-citizen-aya}

**Esta seção:** Camila também agenda um lembrete de comunicação para que um ano depois. (Etapa de fluxo de trabalho que automatiza/executa e-mail).

### Notificação De Cliente De Email (Aya) {#aya-user-story-email-client-updated}

**Instruções do usuário:**

1. Navegue até seu cliente de e-mail.
1. Localize e abra o email Lembrete de renovação.
1. Clique no ícone &quot;**Enviar uma nova solicitação de emprego**&quot; para abrir o formulário adaptável.

   1. Esta seção foi deixada intencionalmente vazia para suportar o preenchimento prévio de dados na fase 2.

   ![Email de lembrete de renovação](/help/forms/using/assets/renewal_reminder_email.png)

## (Opcional) Modelo de dados de formulário (Camila) {#form-data-model}

**Esta seção**: Camila navega até as Integrações de dados do AEM Forms, onde pode executar um teste rápido para ver se as informações enviadas para a fonte de dados externa por meio da integração do Modelo de dados de formulário estão realmente presentes.

### Modelo de dados de formulário (Camila) {#form-data-model-camila}

**Esta seção**: Camila navega até a página Fontes de Dados para validar os dados que o servidor replicou no banco de dados Derby.

1. Quando a experiência do usuário estiver concluída e o envio do usuário tiver sido concluído, o Camila navegará para a guia Fontes de dados no AEM Forms (**Forms** > **Integrações de dados**)

1. Camila seleciona o AEM Forms **We.gov FDM** e edite o **FDM de inscrição do We.gov**.

1. Camila então seleciona o **Contato** > **Serviço de leitura** a ser testado.

   ![Entrar em contato com o serviço de leitura](assets/aftia-contact-read-service.jpg)

1. Camila então fornece ao serviço de teste uma ID de contato e clica no botão Testar. Por exemplo, 1 ou 2, se você enviou o formulário. Se você não tiver enviado o formulário, nenhum dado será retornado.

   ![Entrar em contato com o serviço de leitura](assets/aftia-test-service.jpg)

1. Camila poderá então validar se os dados foram inseridos com êxito na fonte de dados.

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

**Esta seção:** Camila navega até um painel onde pode ver os KPIs da agência, como % de cidadãos que começam a preencher um formulário de solicitação de serviço e abandonam, o período médio desde o envio da solicitação até a resposta de aprovação/negação e estatísticas de engajamento para os manuais de benefícios que ela enviou aos cidadãos.

### Relatórios do Adobe Analytics Sites (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Navegue até *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Selecione o &quot;**Site do AEM Forms We.Gov**&quot; para visualizar as páginas do site.
1. Selecione uma da página do site (por exemplo, Início) e escolha &quot;**Analytics e Recommendations**&quot;.

   ![Analytics e Recommendation](/help/forms/using/assets/analytics_recommendation.jpg)

1. Nesta página, você verá informações buscadas no Adobe Analytics que pertencem à página do AEM Sites (OBSERVAÇÃO: por design, essas informações são atualizadas periodicamente do Adobe Analytics e não são exibidas em tempo real).

   ![Métricas principais do Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De volta à página de exibição de página (acessada na etapa 3.), você também pode visualizar as informações de exibição de página alterando a configuração de exibição para visualizar os itens na &quot;**Exibição de lista**&quot;.
1. Localize o &quot;**Exibir**&quot;menu suspenso e selecione&quot;**Exibição de lista**&quot;.

   ![Exibição de lista no menu suspenso Exibição](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. No mesmo menu, selecione &quot;**Configuração de exibição**&quot; e selecione as colunas que deseja exibir na lista suspensa &quot;**Analytics**&quot;.

   ![Configurar a exibição de colunas](/help/forms/using/assets/view_setting_analytics.jpg)

1. Clique em &quot;**Atualizar**&quot; para disponibilizar as novas colunas.

   ![Disponibilizar novas colunas](/help/forms/using/assets/new_columns_available.jpg)

### Relatórios do Adobe Analytics Forms (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Vá até

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Selecione o &quot;**Solicitação de Inscrição para Benefícios de Saúde**&quot;formulário adaptável e selecione o&quot;**Relatório do Analytics**&quot;.

   ![Inscrição para Benefícios de Integridade](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Aguarde o carregamento da página e visualize os dados do relatório do Analytics.

   ![Dados de relatório do Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
