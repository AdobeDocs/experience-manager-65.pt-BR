---
title: Criar e gerenciar o teste A/B para formulários adaptáveis
seo-title: Criar e gerenciar o teste A/B para formulários adaptáveis
description: A AEM Forms integra-se com a Adobe Target, que permite a execução de testes A/B para formulários adaptáveis, a fim de melhorar a experiência do cliente e o taxa de conversão.
seo-description: A AEM Forms integra-se com a Adobe Target, que permite a execução de testes A/B para formulários adaptáveis, a fim de melhorar a experiência do cliente e o taxa de conversão.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---


# Criar e gerenciar o teste A/B para formulários adaptáveis{#create-and-manage-a-b-test-for-adaptive-forms}

## Visão geral {#overview-br}

Seus clientes provavelmente abandonarão um formulário se a experiência que ele oferece não for envolvente. Embora seja frustrante para os clientes, também pode aumentar o volume e o custo de suporte para a sua organização. É crítico e desafiador identificar e fornecer a experiência certa do cliente que aumenta a taxa de conversão. A Adobe Experience Manager Forms mantém a chave para esse problema.

A AEM Forms se integra com a Adobe Target, uma solução Adobe Marketing Cloud, para oferecer experiências personalizadas e envolventes aos clientes em vários canais digitais. Um dos principais recursos do Público alvo é o teste A/B, que permite configurar rapidamente testes A/B simultâneos, apresentar conteúdo relevante para os usuários direcionados e identificar a experiência que direciona uma melhor taxa de conversão.

Com a AEM Forms, você pode configurar e executar testes A/B em formulários adaptáveis em tempo real. Ele também fornece recursos de relatórios prontos e personalizáveis para visualizar o desempenho em tempo real de suas experiências de formulário e identificar aquele que maximiza o envolvimento e a conversão do usuário.

## Configurar e integrar Públicos alvos no AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Antes de começar a criar e analisar testes A/B para formulários adaptáveis, é necessário configurar o servidor do Público alvo e integrá-lo ao AEM Forms.

### Configurar Público alvo {#set-up-target}

Para integrar AEM com o Público alvo, verifique se você tem uma conta Adobe Target válida. Ao se registrar no Adobe Target, você recebe um código de cliente. Você precisa do código do cliente, e-mail associado à conta do Público alvo e senha para se conectar AEM com o Público alvo.

O Código do cliente identifica a conta do cliente Adobe Target e é usado como um subdomínio no URL ao chamar o servidor Adobe Target. Antes de continuar, certifique-se de que suas credenciais permitem fazer logon em [https://testandtarget.omniture.com/](https://testandtarget.omniture.com/).

### Integrar Público alvo no AEM Forms {#integrate-target-in-aem-forms}

Execute as seguintes etapas para integrar um servidor de Público alvo em execução ao AEM Forms:

1. No servidor AEM, vá para https://&lt;*nome do host*>:&lt;*porta*>/libs/cq/core/content/tools/cloudservices.html.

1. Na seção **Adobe Target**, clique em **Mostrar configurações** e no ícone **+** para adicionar uma nova configuração.
Se você estiver configurando o público alvo pela primeira vez, clique em **Configurar agora.**

1. Na caixa de diálogo Criar configuração, especifique um **Título** e, opcionalmente, um **Nome** para a configuração.

1. Clique em **Criar**. A caixa de diálogo Editar componente é aberta.
1. Especifique os detalhes da conta do Público alvo, como código do cliente, email e senha.
1. Selecione **Restaurar** na lista suspensa Tipo de API.

1. Clique em **Ligar ao Adobe Target** para inicializar a ligação ao Público alvo. Se a conexão for bem-sucedida, a mensagem Conexão bem-sucedida será exibida. Clique em **OK** na mensagem e em **OK** na caixa de diálogo. A conta do Público alvo está configurada.

1. Crie uma estrutura de Público alvo conforme descrito em [Adicione uma estrutura](/help/sites-administering/target.md).

1. Vá para https://&lt;*nome do host*>:&lt;*porta*>/system/console/configMgr.

1. Clique em **Configuração do Público alvo AEM Forms**.
1. Selecione uma **Estrutura de Públicos alvos**.
1. No campo **URLs** do Público alvo, especifique todos os URLs nos quais os testes A/B serão executados. Por exemplo, https://&lt;*nome do host*>:&lt;*porta*>/ para servidor AEM Forms em OSGi ou https://&lt;*nome do host*>:&lt;*porta*>/lc/ para servidor AEM Forms em JEE.
Considere que você deseja configurar um URL de Público alvo para uma instância de publicação e seus clientes podem acessá-lo usando o nome do host ou o endereço IP, será necessário configurar ambos como URLs de Público alvo - usando o nome do host e o endereço IP. Se você configurar apenas um dos URLs, seu teste A/B não será executado para clientes que vêm do outro URL. Clique em **+** para especificar vários URLs.

1. Clique em **Salvar**.

Seu servidor de Públicos alvos é integrado ao AEM Forms. Agora você pode ativar o teste A/B se tiver uma licença completa para utilizar o Adobe Target.

Se você tiver uma licença completa para utilizar a Adobe Target, start o servidor com os seguintes parâmetros depois de integrar o Público alvo à AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Se a instância AEM estiver em execução em JBoss, iniciada como um serviço de chave-na-mão, no arquivo `jboss\bin\standalone.conf.bat`, adicione o parâmetro -Dabtesting.enabled=true na seguinte entrada:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Além do servidor de chefe, você pode adicionar o argumento -Dabtesting.enabled=true jvm no script de inicialização do servidor para qualquer servidor de aplicativos. Agora você pode criar e executar testes A/B para formulários adaptáveis.

>[!NOTE]
>
>Se você atualizar os URLs de Público alvo configurados posteriormente, atualize todos os testes A/B em execução para que apontem para os URLs atuais. Para obter informações sobre como atualizar testes A/B, consulte [Atualizar teste A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).


## Criar audiências em AEM {#create-audiences-within-aem}

AEM permite criar uma audiência e usá-la para um teste A/B. A audiência criada no AEM está disponível no AEM Forms. Execute as seguintes etapas para criar audiências no AEM:

1. Na instância de criação, toque em **Adobe Experience Manager** > **Personalização** > **Audiência**.

1. Na página Audiência, toque em **Criar Audiência > Criar Audiência de Público alvo**.
1. Na caixa de diálogo Configuração do Adobe Target, selecione uma configuração de Público alvo e clique em **Ok**.
1. Na página Criar nova Audiência, crie regras. As regras permitem categorizar a audiência. Por exemplo, você deseja categorizar audiências com base no sistema operacional. Sua audiência A vem do Windows e a audiência B vem do Linux.

   1. Para categorizar a audiência com base no Windows, na Regra nº 1, selecione o tipo de atributo **OS**. Na lista suspensa Quando, selecione **Windows.**

   1. Para categorizar a audiência com base no Linux, na Regra nº 2, selecione o tipo de atributo **OS**. Na lista suspensa **Quando**, selecione **Linux** e clique em **Próximo**.

1. Especifique um nome para a audiência criada e clique em **Salvar**.

Você pode selecionar a audiência ao configurar o teste A/B para um formulário, como mostrado abaixo.

## Criar teste A/B {#create-a-b-test}

Execute as seguintes etapas para criar um teste A/B para um formulário adaptável.

1. Vá para **Forms &amp; Documentos** em https://&lt;*nome do host*>:&lt;*porta*>/aem/forms.html/content/dam/formsanddocuments.

1. Navegue até a pasta que contém o formulário adaptável.
1. Clique na ferramenta **Select** na barra de ferramentas e selecione o formulário adaptável.
1. Clique em **Mais** na barra de ferramentas e selecione **Configurar teste A/B**. A página Configurar teste A/B é aberta.

[ ![Página de configuração de teste A/B para formulários adaptáveis](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. Especifique um **Nome da Atividade** para o teste A/B.

1. Na lista suspensa Audiência, selecione uma audiência para a qual deseja fornecer experiências diferentes do formulário. Por exemplo, **Visitantes usando o Chrome**. A lista da audiência é preenchida a partir do servidor de Públicos alvos configurado.

1. Nos campos **Distribuição da experiência** para as experiências A e B, especifique a distribuição, em termos de porcentagem, para determinar a distribuição de experiências entre a audiência total. Por exemplo, se você especificar 40, 60 para as experiências A e B, respectivamente, a experiência A será servida para 40% da audiência e os 60% restantes verão a experiência B.
1. Clique em **Configurar**. Uma caixa de diálogo é exibida para confirmar a criação do teste A/B.
1. Clique em **Editar experiência B** para abrir o formulário adaptável no modo de edição. Modifique o formulário para criar uma experiência diferente da experiência padrão A. As possíveis variações permitidas na Experiência B são alterações em:

   * CSS ou estilo
   * Ordem dos campos em diferentes painéis ou no mesmo painel
   * Layout do painel
   * Títulos do painel
   * Descrição, rótulo e texto de ajuda para um campo
   * Scripts que não afetam ou quebram o fluxo de envio
   * Validações (cliente e servidor)
   * Tema da experiência B. (Você pode selecionar um tema alternativo para a experiência B)

1. Vá para a interface do usuário do Forms e Documentos, selecione o formulário adaptável, clique em **Mais** e selecione **Teste A/B do Start**.

O teste A/B agora está sendo executado e a audiência especificada será fornecida aleatoriamente para as experiências com base na distribuição especificada.

## Atualizar teste A/B {#update-a-b-test}

Você pode atualizar as distribuições de audiência e experiência de um teste A/B em execução. Para isso:

1. Na interface do usuário do Forms e Documentos, navegue até a pasta que contém o formulário adaptável no qual o teste A/B está sendo executado.
1. Selecione o formulário adaptável.
1. Clique em **Mais** e selecione **Editar teste A/B**. A página Atualizar teste A/B é aberta.

1. Atualize as distribuições de audiência e experiência, conforme necessário.
1. Clique em **Atualizar**.

## Visualização e análise do relatório de teste A/B {#view-and-analyze-a-b-test-report}

Depois de permitir que o teste A/B seja executado durante o período desejado, você pode gerar um relatório e verificar qual experiência resultou em uma melhor conversão. Você pode declarar a experiência de melhor desempenho como vencedora ou optar por executar outro teste A/B. Para fazer isso, execute as seguintes etapas:

1. Selecione o formulário adaptável, clique em **Mais** e, em seguida, clique em **Relatório de teste A/B**. O relatório é exibido.

[ ![Relatório de teste A/B](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. Analise o relatório e veja se você tem pontos de dados suficientes para declarar uma das experiências de melhor desempenho como vencedora. Você pode optar por continuar com o mesmo teste A/B por mais tempo ou declarar um vencedor e encerrar o teste A/B.
1. Para declarar um vencedor e encerrar o teste A/B, clique no botão **Encerrar teste A/B** no painel do relatórios. Uma caixa de diálogo solicita que você declare uma das duas experiências como vencedora. Escolha um vencedor e confirme para encerrar o teste A/B.
Como alternativa, você pode primeiro declarar um vencedor clicando no botão **Declarar vencedor** para a respectiva experiência. Ele solicita que você confirme o vencedor. Clique em **Yes** para encerrar o teste A/B.

Se você escolheu a experiência A como vencedora, o teste A/B será finalizado e, para frente, somente a Experiência A será disponibilizada para todas as audiências.
