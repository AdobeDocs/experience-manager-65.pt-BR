---
title: Criar e gerenciar teste A/B para formulários adaptáveis
description: O AEM Forms é integrado ao Adobe Target, o que permite a execução de testes A/B para formulários adaptáveis para aprimorar a experiência do cliente e melhorar as taxas de conversão.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 2%

---

# Criar e gerenciar teste A/B para formulários adaptáveis{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE Descontinuado]{type=negative tooltip="Este recurso chegou ao fim da vida útil"}

<div class="preview"> O recurso Teste A/B para formulários adaptáveis chegou ao fim da vida útil e não é mais compatível. </div>

## Visão geral {#overview-br}

Seus clientes provavelmente abandonarão um formulário se a experiência que ele oferece não for cativante. Embora seja frustrante para os clientes, também pode aumentar o volume de suporte e os custos para a sua organização. É crítico e desafiador identificar e fornecer a experiência certa ao cliente que aumente a taxa de conversão. O Adobe Experience Manager Forms é a chave para esse problema.

O AEM Forms integra-se ao Adobe Target, uma solução da Adobe Experience Cloud, para fornecer experiências personalizadas e envolventes ao cliente em vários canais digitais. Um dos principais recursos do Target é o teste A/B, que permite configurar rapidamente testes A/B simultâneos, apresentar conteúdo relevante aos usuários direcionados e identificar a experiência que impulsiona um melhor índice de conversão.

Com o Adobe Experience Manager (AEM) Forms, você pode configurar e executar testes A/B em formulários adaptáveis em tempo real. Ele também fornece recursos de relatório prontos para uso e personalizáveis para visualizar o desempenho em tempo real das experiências de seu formulário e identificar aquele que maximiza o engajamento e a conversão do usuário.

## Configurar e integrar o Target no AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Antes de começar a criar e analisar testes A/B para formulários adaptáveis, você deve configurar seu servidor Target e integrá-lo ao AEM Forms.

### Configurar o Target {#set-up-target}

Para integrar o AEM ao Target, verifique se você tem uma conta válida do Adobe Target. Ao se registrar na Adobe Target, você recebe um código de cliente. Você precisa do código de cliente, email associado à conta do Target e senha para se conectar ao AEM com o Target.

O código do cliente identifica a conta de cliente do Adobe Target e é usado como um subdomínio no URL ao chamar o servidor do Adobe Target. Antes de continuar, faça logon no [https://experience.adobe.com/](https://experience.adobe.com/) e, se você tiver acesso, visualize a variável [!DNL Adobe Target] opção no [!UICONTROL Acesso rápido] seção.

### Integrar um servidor do Target em execução ao AEM Forms {#integrate-target-in-aem-forms}

1. No servidor AEM, acesse https://&lt;*hostname*>:&lt;*porta*>/libs/cq/core/content/tools/cloudservices.html.

1. No **Adobe Target** clique em **Exibir configurações** e, em seguida, o **+** ícone para adicionar uma configuração.
Se você estiver configurando um target pela primeira vez, clique em **Configure agora.**

1. Na caixa de diálogo Criar configuração, especifique uma **Título** e, opcionalmente, um **Nome** para a configuração.

1. Clique em **Criar**. A caixa de diálogo Editar componente é aberta.
1. Especifique os detalhes da conta do Target, como código do cliente, email e senha.
1. Selecionar **Rest** na lista suspensa Tipo de API.

1. Clique em **Conectar-se ao Adobe Target** para que você possa inicializar a conexão com o Target. Se a conexão for bem-sucedida, a mensagem Conexão bem-sucedida será exibida. Clique em **OK** na mensagem e, em seguida, em **OK** na caixa de diálogo. A conta do Target está configurada.

1. Crie uma estrutura do Target conforme descrito em [Adicionar uma estrutura](/help/sites-administering/target.md).

1. Acesse https://&lt;*hostname*>:&lt;*porta*>/system/console/configMgr

1. Clique em **Configuração do AEM Forms Target**.
1. Selecione um **Estrutura do Target**.
1. No **URLs do Target** especifique todos os URLs nos quais os testes A/B são executados. Por exemplo, https://&lt;*hostname*>:&lt;*porta*>/ para AEM Forms Server no OSGi ou https://&lt;*hostname*>:&lt;*porta*>/lc/ para AEM Forms Server no JEE.
Considere que você deseja configurar um URL de destino para uma instância de publicação e que seus clientes podem acessá-lo usando o nome do host ou o endereço IP. Nesse caso, você deve configurar ambos como URLs do Target, usando o nome do host e o endereço IP. Se você configurar apenas um dos URLs, seu teste A/B não será executado para clientes provenientes do outro URL. Clique em **+** para especificar vários URLs.

1. Clique em **Salvar**.

Seu servidor Target está integrado ao AEM Forms. Agora você pode ativar o teste A/B se tiver uma licença completa para usar o Adobe Target.

Se você tiver uma licença completa para usar o Adobe Target, inicie o servidor com os seguintes parâmetros depois de integrar o Target ao AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Se a instância do AEM estiver em execução no JBoss®, iniciada como um serviço do turnkey, em `jboss\bin\standalone.conf.bat` arquivo, adicione o parâmetro -Dabtesting.enabled=true na seguinte entrada:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Além do servidor JBoss®, você pode adicionar o argumento -Dabtesting.enabled=true jvm no script de inicialização do servidor para qualquer servidor de aplicativos. Agora é possível criar e executar testes A/B para formulários adaptáveis.

>[!NOTE]
>
>Se você atualizar os URLs do Target configurados posteriormente, atualize todos os testes A/B em execução para que eles apontem para os URLs atuais. Para obter informações sobre a atualização de testes A/B, consulte [Atualizar teste A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).
>

## Criar públicos-alvo no AEM {#create-audiences-within-aem}

O AEM permite criar um público-alvo e usá-lo para um teste A/B. O público-alvo que você cria no AEM está disponível no AEM Forms. Para criar públicos-alvo no AEM, faça o seguinte:

1. Na instância de criação, toque em **Adobe Experience Manager** > **Personalização** > **Públicos-alvo**.

1. Na página Públicos-alvo, toque em **Criar público-alvo > Criar público-alvo**.
1. Na caixa de diálogo Configuração do Adobe Target, selecione uma configuração do Target e clique em **Ok**.
1. Na página Criar novo público-alvo, crie regras. As regras permitem categorizar o público-alvo. Por exemplo, você deseja categorizar públicos com base no sistema operacional. Seu público-alvo A vem do Windows e o público-alvo B vem do Linux®.

   1. Para categorizar um público com base no Windows, na Regra #1, selecione o **SO** tipo de atributo. No menu suspenso Quando, selecione **Janelas.**

   1. Para categorizar públicos-alvo com base no Linux®, na Regra #2, selecione a **SO** tipo de atributo. No **Quando** selecione **Linux®** e clique em **Próxima**.

1. Especifique um nome para o público-alvo criado e clique em **Salvar**.

Você pode selecionar o público-alvo ao configurar o teste A/B para um formulário, conforme mostrado abaixo.

## Criar teste A/B para um formulário adaptável {#create-a-b-test}

1. Ir para **Forms e documentos** em https://&lt;*hostname*>:&lt;*porta*>/aem/forms.html/content/dam/formsanddocuments.

1. Navegue até a pasta que contém o formulário adaptável.
1. Clique em **Selecionar** na barra de ferramentas e selecione o formulário adaptável.
1. Clique em **Mais** na barra de ferramentas e selecione **Configurar o teste A/B**. A página Configurar teste A/B é aberta.

[](assets/ab-test-configure-1.png)

1. Especifique um **Nome da atividade** para o teste A/B.

1. Na lista suspensa Público-alvo, selecione um público-alvo ao qual deseja atender diferentes experiências do formulário. Por exemplo, **Visitantes que usam o Chrome**. A lista de públicos-alvo é preenchida a partir do servidor do Target configurado.

1. No **Distribuição de experiência** para as experiências A e B, especifique a distribuição, em termos de porcentagem, para determinar a distribuição das experiências entre o público total. Por exemplo, se você especificar 40, 60 para as experiências A e B, respectivamente, a experiência A será disponibilizada para 40% do público-alvo e os 60% restantes verão a experiência B.
1. Clique em **Configurar**. Uma caixa de diálogo é exibida para confirmar a criação do teste A/B.
1. Clique em **Editar experiência B** para que você possa abrir o formulário adaptável no modo de edição. Modifique o formulário criando uma experiência diferente da experiência padrão A. As possíveis variações permitidas na Experiência B são alterações em:

   * CSS ou estilo
   * Ordem dos campos em painéis diferentes ou no mesmo painel
   * Layout do painel
   * Títulos do painel
   * Descrição, rótulo e texto de ajuda de um campo
   * Scripts que não afetam ou interrompem o fluxo de envio
   * Validações (cliente e servidor)
   * Tema para experiência B. (Você pode selecionar um tema alternativo para a experiência B)

1. Vá para a interface do Forms e Documentos, selecione o formulário adaptável e clique em **Mais** e selecione **Iniciar teste A/B**.

Seu teste A/B agora está em execução e o público-alvo especificado é disponibilizado aleatoriamente com as experiências com base na distribuição especificada.

## Atualizar o teste A/B {#update-a-b-test}

Você pode atualizar as distribuições de público-alvo e experiência de um teste A/B em execução.

Para atualizar o teste AB:

1. Na interface do Forms e documentos, navegue até a pasta que contém o formulário adaptável em que o teste A/B está sendo executado.
1. Selecione o formulário adaptável.
1. Clique em **Mais** e selecione **Editar teste A/B**. A página Atualizar teste A/B é aberta.

1. Atualize a distribuição de público-alvo e experiência, conforme necessário.
1. Clique em **Atualizar**.

## Exibir e analisar o relatório de teste A/B {#view-and-analyze-a-b-test-report}

Depois de permitir que o teste A/B seja executado pelo período desejado, você pode gerar um relatório e verificar qual experiência resultou em uma melhor conversão. Você pode declarar uma experiência com melhor desempenho como vencedora ou optar por executar outro teste A/B.

Para exibir e analisar o relatório de teste A/B:

1. Selecione o formulário adaptável e clique em **Mais** e clique em **Relatório do teste A/B**. O relatório é exibido.

[](assets/ab-test-report-3.png)

1. Analise o relatório e veja se você tem pontos de dados suficientes para declarar uma das experiências de melhor desempenho como vencedora. Você pode optar por continuar com o mesmo teste A/B por mais tempo ou declarar um vencedor e terminar o teste A/B.
1. Para declarar um vencedor e finalizar o teste A/B, clique no link **Encerrar teste A/B** no painel de relatórios. Uma caixa de diálogo solicita que você declare uma das duas experiências como vencedora. Escolha um vencedor e confirme a finalização do teste A/B.
Como alternativa, primeiro você pode declarar um vencedor clicando no ícone **Declarar vencedor** botão para a respectiva experiência. Ele solicita que você confirme o vencedor. Clique em **Sim** para encerrar o teste A/B.

Se você escolher a experiência A como vencedora, o teste A/B será encerrado e, a partir de agora, somente a Experiência A será disponibilizada para os públicos-alvo.
