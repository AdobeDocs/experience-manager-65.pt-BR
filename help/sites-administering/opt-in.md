---
title: Ativação do Adobe Analytics e do Adobe Target
description: Saiba como aceitar o Adobe Analytics e o Adobe Target.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 11%

---

# Ativação do Adobe Analytics e do Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

O AEM tem um procedimento de aceitação para ajudar você a se integrar ao Adobe Analytics e ao Adobe Target. Isso está disponível e pronto para uso, como uma tarefa pré-carregada atribuída ao grupo de usuários administrador.

Quando você efetua login como administrador desta tarefa (**Configuração do Analytics e do Targeting**) está disponível no [Caixa de entrada](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). Com base nas credenciais fornecidas, ele ajuda a configurar e integrar esses serviços.

Você tem as seguintes opções para configurar a integração:

* Configure a integração por meio da tarefa.

  Isso pode ser feito imediatamente ou posteriormente, a tarefa permanecerá na Caixa de entrada até que alguma ação seja tomada. Em ambos os casos, a configuração pode ser feita diretamente na interface do usuário ou com o uso de uma configuração `.properties` arquivo.

* Recusar a integração.

  Considere esta opção se preferir [configurar manualmente a integração](/help/sites-administering/marketing-cloud.md). Consulte também [Integração do AEM ao Adobe Target e ao Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* Configure a configuração e o provisionamento usando um script.

## Configurar a integração {#configuring-the-integration}

Aceitar a integração com:

* Analytics para permitir o uso de seus recursos de rastreamento e análise de página.
* Target para permitir o uso de seus recursos de personalização.

Para qualquer uma das opções, é necessário fornecer as informações da conta do usuário e especificar as páginas que são rastreadas.

>[!NOTE]
>
>Opcionalmente, é possível fornecer informações da conta do Analytics e do Target usando um arquivo de propriedades lido na inicialização do servidor. Consulte [Como fornecer informações da conta usando um arquivo de propriedades](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

Quando você opta pela integração, o AEM executa as seguintes tarefas:

* Cria as configurações de nuvem que habilitam a conexão com o Analytics e o Target.
* Cria as estruturas que determinam os dados rastreados.
* Configura as páginas da Web para usar esses serviços.

>[!NOTE]
>
>A AT.js é a biblioteca do cliente padrão. Isso é configurado em seu [configuração dos serviços em nuvem do target](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
>A Adobe recomenda que você use a AT.js como a biblioteca do cliente.

Para aceitar a tarefa pré-carregada e pronta para uso:

1. Do seu [Caixa de entrada, selecione e **Abertura** a Configuração do Analytics e do Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item) tarefa.

   ![optin-01](assets/optin-01.png)

1. Para o Analytics:

   1. Insira as informações da conta do usuário para o Analytics e clique no link correspondente **Adicionar** botão.
   1. As credenciais apropriadas são autenticadas.
   1. Quando a conta do Analytics for autenticada, selecione o conjunto de relatórios do Analytics para usar. O AEM recupera esses conjuntos de relatórios do Analytics. O status é atualizado para **Adicionado**.

1. Para o Target:

   1. Insira as informações da conta do usuário para o Target e clique no link correspondente **Adicionar** botão.
   1. As credenciais apropriadas são autenticadas. O status é atualizado para **Adicionado**.

1. Selecione **Próximo**.
1. Selecione os sites para os quais o Analytics e/ou Target devem ser usados.

1. Selecionar **Concluído** para concluir.

   >[!CAUTION]
   >
   >Depois de optar pela configuração, você precisará publicar o site/páginas afetadas para replicar essas alterações na instância de publicação.

## Recusar a integração {#opting-out-of-the-integration}

Recuse a integração com o Analytics e o Target ao:

* Não quiser integrar a esses produtos.
* Prefira configurar as integrações manualmente.

  Para obter informações sobre como configurar as integrações manualmente, consulte [Integração com o Adobe Analytics](/help/sites-administering/adobeanalytics.md) e [Integração com o Adobe Target](/help/sites-administering/target.md).

Para recusar, você precisa concluir a tarefa pré-carregada:

* Do seu [Caixa de entrada, selecione e **Concluído** a Configuração do Analytics e do Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item) tarefa.

## Como fornecer informações da conta usando um arquivo de propriedades {#providing-account-information-using-a-properties-file}

Instale um arquivo de propriedades que o AEM lê na inicialização do servidor para configurar as propriedades da conta para integração com o Analytics e o Target. Quando você usa o arquivo de propriedades, o assistente de aceitação usa automaticamente as propriedades do arquivo e a configuração da nuvem é criada de acordo.

O arquivo de propriedades é um arquivo de texto chamado marketingcloud.properties que você salva no diretório de trabalho que o processo AEM está usando (normalmente o mesmo diretório do arquivo JAR). O arquivo inclui as seguintes propriedades:

* analytics.server: o URL do data center do Analytics que você usa.
* analytics.company: a empresa associada à conta de usuário do Analytics.
* analytics.username: seu nome de usuário do Analytics.
* analytics.secret: o segredo associado ao nome de usuário do Analytics.
* analytics.reportsuite: o nome do conjunto de relatórios do Analytics que será usado.
* target.clientcode: o código de cliente associado à sua conta do Target.
* target.email: o endereço de email que você usa para autenticar sua conta do Target.
* target.password: a senha associada ao seu endereço de email.

As propriedades e os valores são separados por sinais de igual (=). As propriedades do Analytics recebem o prefixo `analytics`e as propriedades do Target recebem o prefixo `target`. Para configurar um serviço, forneça valores para todas as propriedades desse serviço. Se você não quiser configurar um serviço, não forneça valores para esse serviço.

O exemplo a seguir `.properties` O arquivo inclui os valores de propriedade para criar uma configuração em nuvem do Analytics:

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

O procedimento a seguir descreve como aderir à integração usando o arquivo de propriedades.

1. Crie o `marketingcloud.properties` arquivo no diretório de trabalho que o processo AEM está usando (instância do autor).

   >[!NOTE]
   >
   >O diretório de trabalho geralmente é o diretório que contém o jar ou `license.properties` arquivo.
   >
   >No entanto, também pode ser definido como um caminho absoluto pela propriedade do sistema:
   >
   >`mac.provisioning.file.container`

1. Adicione os valores da propriedade de acordo com suas contas do Analytics e/ou do Target.
1. Inicie ou reinicie o servidor e faça logon usando uma conta de administrador.
1. Abra a tarefa Configurar Analytics e Targeting conforme descrito em [Configurar a integração](/help/sites-administering/opt-in.md#configuring-the-integration). Em vez de solicitar as informações da conta, o assistente usa os valores da variável `.properties` arquivo.

   Selecionar **Adicionar** para o serviço apropriado, prossiga com o assistente.

   ![optin-02](assets/optin-02.png)

## Sobre as configurações em nuvem {#about-the-cloud-configurations}

Ao configurar a integração com o Analytics e o Target, o AEM cria automaticamente as configurações e estruturas de nuvem necessárias. Por exemplo, a configuração de nuvem do Analytics é chamada de Conta provisionada do Analytics.

Não é necessário alterar as configurações de nuvem. No entanto, você pode configurar as estruturas conforme necessário. (Consulte [Mapeamento de dados do componente com propriedades do Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md) e [Adicionar uma estrutura do Target](/help/sites-administering/target.md).)

>[!NOTE]
>
>Por padrão, quando você opta pelo assistente de configuração do Adobe Target, o Direcionamento preciso é ativado.
>
>Direcionamento preciso significa que a configuração do Cloud Service aguarda o contexto ser carregado antes de carregar o conteúdo. Como resultado, em termos de desempenho, o direcionamento preciso pode criar um atraso de alguns milissegundos antes de carregar o conteúdo.
>
>O direcionamento preciso é sempre ativado na instância do autor. No entanto, na instância de publicação, é possível desativar o direcionamento preciso globalmente, limpando a marca de seleção ao lado de Direcionamento preciso na configuração do Cloud Service (**http://localhost:4502/etc/cloudservices.html**). Você também pode ativar e desativar o direcionamento preciso para componentes individuais, independentemente das suas definições na configuração do Cloud Service.
>
>Se você ***já*** tiver criado componentes direcionados e alterar essa configuração, suas alterações não afetarão esses componentes. Você deve alterar esses componentes diretamente.

>[!CAUTION]
>
>Ao optar pela configuração do Analytics e uma configuração `reportsuite` for selecionada, a estrutura será restrita ao modo de execução de publicação. Isso significa que o rastreamento só funciona na instância de publicação.
>
>Se o rastreamento for necessário em uma instância de criação, o valor deverá ser alterado para `all`.

## Configuração e provisionamento via script {#configuring-the-setup-and-provisioning-via-script}

Como administrador, talvez você queira acionar a configuração e o provisionamento com um script em vez de executar manualmente a etapa do assistente. Você pode fazer isso ao:

* Envio de uma solicitação POST para **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** com os parâmetros necessários.

Os parâmetros enviados dependem do seguinte:

* Se quiser usar a variável **marketingcloud.properties** arquivo preenchido com todas as credenciais necessárias, você deve enviar os seguintes parâmetros:

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=caminho para uma página AEM para anexar as configurações dos serviços em nuvem criadas

  Por exemplo, uma solicitação de ondulação que cria configurações do Analytics e do Target e as anexa à página we.retail seria:

  ```shell
  curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
  ```

* Se não quiser usar o plug-in **marketingcloud.properties** , você deverá enviar as credenciais e os parâmetros. Por exemplo:
   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path para uma página do AEM para anexar as configurações dos serviços de nuvem criados; vários caminhos podem ser definidos
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

  Nesse caso, a solicitação de ondulação que cria as configurações do Analytics e do Target e as anexa à página de we-retail seria:

  ```shell
  curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
  ```
