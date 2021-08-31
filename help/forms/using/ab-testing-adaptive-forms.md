---
title: Criar e gerenciar o teste A/B para formulários adaptáveis
seo-title: Create and manage A/B test for adaptive forms
description: O AEM Forms integra-se ao Adobe Target, que permite a execução de testes A/B para formulários adaptáveis, a fim de melhorar a experiência do cliente e as taxas de conversão.
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 1def8ff7bc90e2ab82ce8b50277a97da9709c78c
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# Criar e gerenciar o teste A/B para formulários adaptáveis{#create-and-manage-a-b-test-for-adaptive-forms}

## Visão geral {#overview-br}

Seus clientes provavelmente abandonarão um formulário se a experiência que ele oferece não for envolvente. Embora seja frustrante para os clientes, também é possível aumentar o volume e o custo de suporte para sua organização. É importante e desafiador identificar e fornecer a experiência correta do cliente que aumenta a taxa de conversão. A Adobe Experience Manager Forms mantém a chave para esse problema.

O AEM Forms integra-se com a Adobe Target, uma solução da Adobe Marketing Cloud, para fornecer experiências personalizadas e envolventes para o cliente em vários canais digitais. Um dos principais recursos do Target é o teste A/B, que permite configurar rapidamente testes A/B simultâneos, apresentar conteúdo relevante para usuários direcionados e identificar a experiência que direciona melhor taxa de conversão.

Com o AEM Forms, você pode configurar e executar testes A/B em formulários adaptáveis em tempo real. Ele também fornece recursos de relatório prontos e personalizáveis para visualizar o desempenho em tempo real de suas experiências de formulário e identificar aquele que maximiza o envolvimento e a conversão do usuário.

## Configurar e integrar o Target no AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Antes de começar a criar e analisar testes A/B para formulários adaptáveis, é necessário configurar o servidor Target e integrá-lo ao AEM Forms.

### Configurar Target {#set-up-target}

Para integrar o AEM com o Target, verifique se você tem uma conta Adobe Target válida. Ao se registrar no Adobe Target, você recebe um código de cliente. Você precisa do código de cliente, email associado à conta do Target e senha para se conectar AEM com o Target.

O Código do cliente identifica a conta do cliente do Adobe Target e é usado como um subdomínio no URL ao chamar o servidor do Adobe Target. Antes de continuar, faça logon em [https://experience.adobe.com/](https://experience.adobe.com/) e, se você tiver acesso, visualize a opção [!DNL Adobe Target] na seção [!UICONTROL Acesso rápido].

### Integração do Target ao AEM Forms {#integrate-target-in-aem-forms}

Execute as seguintes etapas para integrar um servidor Target em execução com o AEM Forms:

1. No servidor AEM, vá para https://*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. Na seção **Adobe Target**, clique em **Mostrar configurações** e, em seguida, no ícone **+** para adicionar uma nova configuração.
Se você estiver configurando o target pela primeira vez, clique em **Configurar agora.**

1. Na caixa de diálogo Criar configuração, especifique um **Título** e, opcionalmente, um **Nome** para a configuração.

1. Clique em **Criar**. A caixa de diálogo Editar componente é aberta.
1. Especifique os detalhes da conta do Target, como código de cliente, email e senha.
1. Selecione **Rest** na lista suspensa Tipo de API .

1. Clique em **Conectar-se ao Adobe Target** para inicializar a conexão com o Target. Se a conexão for bem-sucedida, será exibida a mensagem Connection successful (Conexão bem-sucedida). Clique em **OK** na mensagem e em **OK** na caixa de diálogo. A conta do Target está configurada.

1. Crie uma estrutura do Target conforme descrito em [Adicionar uma estrutura](/help/sites-administering/target.md).

1. Vá para https://&lt;*hostname*:&lt;*port*>/system/console/configMgr.

1. Clique em **Configuração do AEM Forms Target**.
1. Selecione um **Estrutura do Target**.
1. No campo **URLs do Target** , especifique todos os URLs nos quais os testes A/B serão executados. Por exemplo, https://&lt;*hostname*:&lt;*port*>/ para servidor AEM Forms em OSGi ou https://&lt;*hostname*>:&lt;*port*>/lc/ para servidor AEM Forms no JEE.
Considere que você deseja configurar um URL do Target para uma instância de publicação e seus clientes podem acessá-lo usando o nome do host ou o endereço IP, será necessário configurar ambos como URLs do Target - usando o nome do host e o endereço IP. Se você configurar apenas um dos URLs, o teste A/B não será executado para clientes que vêm do outro URL. Clique em **+** para especificar vários URLs.

1. Clique em **Salvar**.

O servidor do Target é integrado ao AEM Forms. Agora é possível ativar o teste A/B se você tiver uma licença completa para utilizar o Adobe Target.

Se você tiver uma licença completa para utilizar o Adobe Target, inicie o servidor com os seguintes parâmetros após integrar o Target com o AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Se a instância AEM estiver em execução no JBoss, iniciada como um serviço de turnkey, no arquivo `jboss\bin\standalone.conf.bat`, adicione o parâmetro -Dabtesting.enabled=true na seguinte entrada:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Além do servidor jboss, você pode adicionar o argumento jvm -Dabtesting.enabled=true no script de inicialização do servidor para qualquer servidor de aplicativos. Agora é possível criar e executar testes A/B para formulários adaptáveis.

>[!NOTE]
>
>Se você atualizar os URLs do Target configurados posteriormente, atualize quaisquer testes A/B em execução para que eles apontem para os URLs atuais. Para obter informações sobre como atualizar testes A/B, consulte [Atualizar teste A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).

## Criar públicos no AEM {#create-audiences-within-aem}

AEM permite criar um público-alvo e usá-lo para um teste A/B. O público-alvo criado no AEM está disponível no AEM Forms. Execute as seguintes etapas para criar públicos-alvo no AEM:

1. Na instância de criação, toque em **Adobe Experience Manager** > **Personalização** > **Públicos-alvo**.

1. Na página Públicos-alvo , toque em **Criar público-alvo > Criar público-alvo**.
1. Na caixa de diálogo Configuração do Adobe Target, selecione uma configuração do Target e clique em **Ok**.
1. Na página Criar novo público-alvo , crie regras. As regras permitem categorizar o público-alvo. Por exemplo, você deseja categorizar os públicos-alvo com base no sistema operacional. Seu público-alvo A vem do Windows e o público-alvo B vem do Linux.

   1. Para categorizar o público-alvo com base no Windows, na Regra 1, selecione o tipo de atributo **OS**. Na lista suspensa Quando , selecione **Windows.**

   1. Para categorizar o público-alvo com base no Linux, na Regra nº 2, selecione o tipo de atributo **OS**. No menu suspenso **When**, selecione **Linux** e clique em **Next**.

1. Especifique um nome para o público-alvo criado e clique em **Salvar**.

Você pode selecionar o público-alvo ao configurar o teste A/B para um formulário, conforme mostrado abaixo.

## Criar teste A/B {#create-a-b-test}

Execute as etapas a seguir para criar um teste A/B para um formulário adaptável.

1. Vá para **Forms &amp; Documents** em https://&lt;*hostname*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Navegue até a pasta que contém o formulário adaptável.
1. Clique na ferramenta **Selecione** na barra de ferramentas e selecione o formulário adaptável.
1. Clique em **Mais** na barra de ferramentas e selecione **Configurar testes A/B**. A página Configurar teste A/B é aberta.

[ ](assets/ab-test-configure-1.png)

1. Especifique um **Nome da atividade** para o teste A/B.

1. Na lista suspensa Público-alvo , selecione um público-alvo para o qual deseja fornecer diferentes experiências do formulário. Por exemplo, **Visitantes usando o Chrome**. A lista de públicos-alvo é preenchida no servidor do Target configurado.

1. Nos campos **Experience Distribution** das experiências A e B, especifique a distribuição, em termos de porcentagem, para determinar a distribuição de experiências entre o público-alvo total. Por exemplo, se você especificar 40, 60 para as experiências A e B, respectivamente, a experiência A será veiculada em 40% do público-alvo e os 60% restantes verão a experiência B.
1. Clique em **Configurar**. Uma caixa de diálogo é exibida para confirmar a criação do teste A/B.
1. Clique em **Editar Experiência B** para abrir o formulário adaptável no modo de edição. Modifique o formulário para criar uma experiência diferente da experiência padrão A. As possíveis variações permitidas na Experiência B são alterações em:

   * CSS ou estilo
   * Ordem dos campos em diferentes painéis ou no mesmo painel
   * Layout do painel
   * Títulos do painel
   * Descrição, rótulo e texto de ajuda de um campo
   * Scripts que não afetam ou quebram o fluxo de envio
   * Validações (cliente e servidor)
   * Tema para a experiência B. (Você pode selecionar um tema alternativo para a experiência B)

1. Vá para a interface Forms e Documentos, selecione o formulário adaptável, clique em **Mais** e selecione **Iniciar testes A/B**.

Agora, o teste A/B está em execução e o público-alvo especificado será fornecido aleatoriamente às experiências com base na distribuição especificada.

## Atualizar teste A/B {#update-a-b-test}

Você pode atualizar as distribuições de público-alvo e experiência de um teste A/B em execução. Para fazer isso:

1. Na interface do usuário de Forms e documentos, navegue até a pasta que contém o formulário adaptável no qual o teste A/B está sendo executado.
1. Selecione o formulário adaptável.
1. Clique em **Mais** e selecione **Editar teste A/B**. A página Atualizar teste A/B é aberta.

1. Atualize as distribuições de público-alvo e experiência, conforme necessário.
1. Clique em **Atualizar**.

## Exibir e analisar relatório de teste A/B {#view-and-analyze-a-b-test-report}

Depois de permitir que o teste A/B seja executado durante o período desejado, você pode gerar um relatório e verificar qual experiência resultou em uma melhor conversão. Você pode declarar a experiência de melhor desempenho um vencedor ou optar por executar outro teste A/B. Para fazer isso, execute as seguintes etapas:

1. Selecione o formulário adaptável, clique em **Mais** e clique em **Relatório de Teste A/B**. O relatório é exibido.

[ ](assets/ab-test-report-3.png)

1. Analise o relatório e veja se você tem pontos de dados suficientes para declarar uma das experiências de melhor desempenho como vencedora. Você pode optar por continuar com o mesmo teste A/B por mais tempo ou declarar um vencedor e encerrar o teste A/B.
1. Para declarar um vencedor e encerrar o teste A/B, clique no botão **End A/B test** no painel de relatórios. Uma caixa de diálogo solicita que você declare uma das duas experiências como vencedora. Escolha um vencedor e confirme para encerrar o teste A/B.
Como alternativa, você pode primeiro declarar um vencedor clicando no botão **Declarar vencedor** para a respectiva experiência. Ele solicita que você confirme o vencedor. Clique em **Yes** para encerrar o teste A/B.

Se você escolheu a experiência A como vencedora, o teste A/B será encerrado e, daqui para frente, somente a Experiência A será veiculada para todos os públicos.
