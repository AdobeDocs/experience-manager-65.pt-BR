---
title: Optar pelo Adobe Analytics e Adobe Target
seo-title: Optar pelo Adobe Analytics e Adobe Target
description: Saiba como optar pelo Adobe Analytics e Adobe Target.
seo-description: Saiba como optar pelo Adobe Analytics e Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 0%

---


# Optar pelo Adobe Analytics e Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM tem um procedimento de aceitação para ajudá-lo a se integrar com a Adobe Analytics e a Adobe Target. Isso está disponível prontamente, como uma tarefa pré-carregada atribuída ao grupo de usuários do administrador.

Quando você faz logon como administrador, essa tarefa (**Configuração do Analytics &amp; Targeting**) está disponível na [Caixa de entrada](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). Com base nas credenciais fornecidas, isso ajuda a configurar e integrar esses serviços.

Você tem as seguintes opções para configurar a integração:

* Configure a integração por meio da tarefa.

   Isso pode ser feito imediatamente ou depois, a tarefa permanecerá na Caixa de entrada até que alguma ação seja tomada. Em ambos os casos, a configuração pode ser feita diretamente na interface do usuário ou com o uso de um arquivo `.properties` predefinido.

* Opt out da integração.

   Considere esta opção se preferir [configurar manualmente a integração](/help/sites-administering/marketing-cloud.md). Consulte também [Integração de AEM com Adobe Target e Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* Configure a configuração e o provisionamento usando um script.

## Configuração da integração {#configuring-the-integration}

Opte pela integração com:

* Analytics para permitir o uso de seus recursos de análise e rastreamento de página.
* Público alvo para permitir o uso de seus recursos de personalização.

Para ambas as opções, é necessário fornecer as informações da conta de usuário e especificar as páginas que são rastreadas.

>[!NOTE]
>
>Como opção, você pode fornecer informações de conta do Analytics e do Público alvo usando um arquivo de propriedades lido na inicialização do servidor. Consulte [Fornecendo informações de conta usando um arquivo de propriedades](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

Ao participar da integração, AEM executa as seguintes tarefas:

* Cria as configurações de nuvem que permitem a conexão com o Analytics e o Público alvo.
* Cria as estruturas que determinam os dados que são rastreados.
* Configura as páginas da Web para usar esses serviços.

>[!NOTE]
>
>AT.js é a biblioteca de cliente padrão. Isso é configurado em [configuração de serviços de nuvem de público alvo](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
>O Adobe recomenda usar o AT.js como a biblioteca do cliente.

Para aceitar a tarefa pré-carregada e pronta para uso:

1. Na caixa de entrada, selecione e [Abra **a tarefa Configurar o Analytics e a definição de metas**.](/help/sites-authoring/inbox.md#taking-action-on-an-item)

   ![optin-01](assets/optin-01.png)

1. Para o Analytics:

   1. Digite as informações da conta do usuário para o Analytics e clique no botão **Adicionar** correspondente.
   1. As credenciais apropriadas são autenticadas.
   1. Quando a conta do Analytics for autenticada, selecione o conjunto de relatórios do Analytics a ser usado. AEM recupera os conjuntos de relatórios do Analytics. O status é atualizado para **Adicionado**.

1. Para o Público alvo:

   1. Digite as informações da conta do usuário para o Público alvo e clique no botão **Adicionar** correspondente.
   1. As credenciais apropriadas são autenticadas. O status é atualizado para **Adicionado**.

1. Selecione **Próximo**.
1. Selecione os sites para os quais o Analytics e/ou o Público alvo devem ser usados.

1. Selecione **Concluído** para concluir.

   >[!CAUTION]
   >
   >Depois de optar pela configuração, é necessário publicar o site ou as páginas afetadas para replicar essas alterações na instância de publicação.

## opt out a integração {#opting-out-of-the-integration}

Opt out a integração com o Analytics e o Público alvo quando você:

* Não queira se integrar a esses produtos.
* Preferir configurar as integrações manualmente.

   Para obter informações sobre como configurar as integrações manualmente, consulte [Integração com o Adobe Analytics](/help/sites-administering/adobeanalytics.md) e [Integração com o Adobe Target](/help/sites-administering/target.md).

Para opt out, é necessário concluir a tarefa pré-carregada:

* Na caixa de entrada, selecione e [Conclua **a tarefa Configurar o Analytics e a definição de metas**.](/help/sites-authoring/inbox.md#taking-action-on-an-item)

## Fornecimento de informações de conta usando um arquivo de propriedades {#providing-account-information-using-a-properties-file}

Instale um arquivo de propriedades que AEM a leitura na inicialização do servidor para configurar as propriedades da conta para a integração com o Analytics e o Público alvo. Quando você usa o arquivo de propriedades, o assistente de aceitação usa automaticamente as propriedades do arquivo e a configuração da nuvem é criada de acordo.

O arquivo de propriedades é um arquivo de texto chamado marketingcloud.properties salvo no diretório de trabalho que o processo de AEM está usando (normalmente o mesmo diretório do arquivo JAR). O arquivo inclui as seguintes propriedades:

* analytics.server: O URL do data center do Analytics que você usa.
* analytics.empresa: A empresa associada à sua conta de usuário do Analytics.
* analytics.username: Seu nome de usuário do Analytics.
* analytics.secret: O segredo associado ao nome de usuário do Analytics.
* analytics.reportsuite: O nome do conjunto de relatórios do Analytics a ser usado.
* público alvo.clientcode: O código de cliente associado à sua conta de Público alvo.
* público alvo.email: O endereço de email que você usa para autenticar sua conta do Público alvo.
* público alvo.password: A senha associada ao seu endereço de email.

As propriedades e os valores são separados por sinais iguais (=). As propriedades do Analytics recebem o prefixo `analytics` e as propriedades do Público alvo recebem o prefixo `target`. Para configurar um serviço, forneça valores para todas as propriedades desse serviço. Se você não quiser configurar um serviço, não forneça valores para esse serviço.

O arquivo de exemplo `.properties` a seguir inclui os valores de propriedade para criar uma configuração de nuvem para o Analytics:

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

O procedimento a seguir descreve como participar da integração usando o arquivo de propriedades.

1. Crie o arquivo `marketingcloud.properties` no diretório de trabalho que o processo de AEM está usando (instância do autor).

   >[!NOTE]
   >
   >Normalmente, o diretório de trabalho é o diretório que contém o arquivo jar ou `license.properties`.
   >
   >No entanto, também pode ser definido como um caminho absoluto pela propriedade do sistema:
   >
   >`mac.provisioning.file.container`

1. Adicione os valores de propriedade de acordo com suas contas do Analytics e/ou Públicos alvos.
1. Start ou reinicie o servidor e faça logon usando uma conta de administrador.
1. Abra a tarefa Configurar análise e definição de metas conforme descrito em [Configuração da integração](/help/sites-administering/opt-in.md#configuring-the-integration). Em vez de solicitar suas informações de conta, o assistente usa os valores do arquivo `.properties`.

   Selecione **Adicionar** para o serviço apropriado e continue com o assistente.

   ![optin-02](assets/optin-02.png)

## Sobre as Configurações de nuvem {#about-the-cloud-configurations}

Quando você configura a integração com o Analytics e o Público alvo, AEM cria automaticamente as configurações e estruturas de nuvem necessárias. Por exemplo, a configuração de nuvem do Analytics é chamada de Conta do Analytics provisionada.

Não é necessário alterar as configurações de nuvem. No entanto, você pode configurar as estruturas conforme necessário. (Consulte [Mapeamento de dados de componentes com as propriedades do Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md) e [Adicionar uma estrutura de Públicos alvos](/help/sites-administering/target.md).)

>[!NOTE]
>
>Por padrão, ao optar pelo assistente de configuração do Adobe Target, a Definição de metas precisa está ativada.
>
>Direcionamento preciso significa que a configuração do serviço de nuvem aguarda o contexto ser carregado antes de carregar o conteúdo. Como resultado, em termos de desempenho, o direcionamento preciso pode criar alguns milissegundos de atraso antes de carregar o conteúdo.
>
>A definição de metas precisa está sempre ativada na instância do autor. Entretanto, na instância de publicação, você pode optar por desativar a definição de metas precisa globalmente, apagando a marca de seleção ao lado da Definição de metas precisa na configuração do serviço de nuvem (**http://localhost:4502/etc/cloudservices.html**). Você também pode ativar e desativar a definição de metas precisa para componentes individuais, independentemente de sua configuração na configuração do serviço de nuvem.
>
>Se você ***já*** criou componentes direcionados e alterar essa configuração, suas alterações não afetarão esses componentes. É necessário fazer alterações diretamente nesses componentes.

>[!CAUTION]
>
>Quando você opta pela configuração do Analytics e um `reportsuite` específico é selecionado, a estrutura é restrita ao modo de execução de publicação. Isso significa que o rastreamento só funciona na instância de publicação.
>
>Se o rastreamento for necessário em uma instância de criação, também o valor deverá ser alterado para `all`.

## Configuração e provisionamento via Script {#configuring-the-setup-and-provisioning-via-script}

Como administrador, talvez você queira acionar a configuração e o provisionamento com um script em vez de passar manualmente pelo assistente. Você pode fazer isso:

* Envio de uma solicitação de POST para **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** com os parâmetros necessários.

Quais parâmetros você envia dependem do seguinte:

* Se quiser usar o arquivo **marketingcloud.properties** preenchido com todas as credenciais necessárias, envie os seguintes parâmetros:

   * `automaticProvisioning`= `true`
   * `servicename`=  `analytics|target`
   * `path`=caminho para uma página AEM para anexar as configurações dos serviços em nuvem criados

   Por exemplo, uma solicitação de ondulação que cria configurações do Analytics e do Público alvo e as anexa à página we.retail seria:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* Se você não quiser usar o arquivo **marketingcloud.properties**, você terá que enviar as credenciais, bem como os parâmetros; por exemplo:

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path para uma página AEM para anexar as configurações dos serviços em nuvem criados; vários caminhos podem ser definidos
   * analytics.server= `https://servername`
   * analytics.empresa= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * público alvo.clientcode= `mycompany`
   * público alvo.email= `me@adobe.com`
   * público alvo.password= `password`

   Nesse caso, a solicitação de ondulação que cria as configurações do Analytics e do Público alvo e as anexa à página de varejo virtual seria:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

