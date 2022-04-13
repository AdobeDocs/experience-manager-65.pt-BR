---
title: Configuração manual da integração com o Adobe Target
seo-title: Manually Configuring the Integration with Adobe Target
description: Saiba como configurar manualmente a integração com o Adobe Target.
seo-description: Learn how to manually configure the integration with Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
source-git-commit: 813441a61baa560c9d317a5519b9e0c0d1da7a6e
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 4%

---

# Configuração manual da integração com o Adobe Target {#manually-configuring-the-integration-with-adobe-target}

Você pode modificar as configurações do assistente de aceitação que você fez ao usar o assistente ou pode fazer a integração manualmente com o Adobe Target sem usar o assistente.

## Modificar as configurações do Assistente de aceitação {#modifying-the-opt-in-wizard-configurations}

O [Assistente de opt-in](/help/sites-administering/opt-in.md) that [integra AEM ao Adobe Target](/help/sites-administering/target.md) O cria automaticamente uma configuração de nuvem do Target chamada Configuração do Target provisionada. O assistente também cria uma estrutura do Target para a configuração de nuvem chamada Estrutura do Target Provisionada. Você pode modificar as propriedades da configuração e da estrutura da nuvem, se necessário.

Você também pode configurar o Adobe Target para usar o Adobe Target como fonte de relatórios ao direcionar conteúdo configurando a configuração do A4T Analytics Cloud.

Para localizar a configuração de nuvem e a estrutura, acesse **Cloud Services** via **Ferramentas** > **Implantação** > **Cloud**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)) Abaixo do Adobe Target, clique ou toque **Mostrar configurações**.

### Propriedades de Configuração do Target Provisionado {#provisioned-target-configuration-properties}

Os seguintes valores de propriedade são usados na configuração da nuvem Configuração do Target Provisionada que o assistente de Opt-in cria:

* **Código do cliente:** Conforme inserido no assistente de Opt-in.
* **E-mail:** Conforme inserido no assistente de Opt-in.
* **Senha:** Conforme inserido no assistente de Opt-in.
* **Tipo de API:** REST
* **Sincronizar segmentos do Adobe Target:** Selecionado.

* **Biblioteca do cliente:** mbox.js.
* **Use o DTM para fornecer a biblioteca do cliente:** Não selecionado. Selecione esta opção se você [usar o DTM](/help/sites-administering/dtm.md) ou outro sistema de gerenciamento de tags para hospedar o arquivo mbox.js ou AT.js. O Adobe recomenda usar o DTM em vez de AEM para entregar a biblioteca do .

* **Mbox.js personalizada:** Nenhum especificado para que o arquivo mbox.js padrão seja usado. Especifique um arquivo mbox.js personalizado para usar, conforme necessário. Somente será exibido se tiver selecionado mbox.js.
* **AT.js personalizada:** Nenhum especificado para que o arquivo AT.js padrão seja usado. Especifique um arquivo AT.js personalizado para usar, conforme necessário. Somente será exibido se tiver selecionado AT.js.

>[!NOTE]
>
>No AEM 6.3, é possível selecionar o arquivo da Biblioteca do Target, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), que é uma nova biblioteca de implementação do Adobe Target, projetada para implementações típicas da Web e aplicativos de página única.
>
>A AT.js oferece várias melhorias em relação à biblioteca mbox.js:
>
>* Tempos de carregamento de página aprimorados para implementações da Web
>* Segurança aprimorada
>* Melhores opções de implementação para aplicativos de página única
>* A AT.js contém os componentes que foram incluídos na target.js, portanto, target.js não é mais chamada


### Propriedades da Estrutura do Target Provisionada {#provisioned-target-framework-properties}

A Estrutura do Target provisionada que o assistente de Opt-in cria é configurada para enviar dados de contexto do armazenamento de dados do perfil. A idade e os itens de dados de gênero da loja são enviados para o Target por padrão. Sua solução provavelmente requer que parâmetros adicionais sejam enviados.

![chlimage_1-158](assets/chlimage_1-158.png)

Você pode configurar a estrutura para enviar informações de contexto adicionais ao Target, conforme descrito em [Adicionar uma estrutura do Target](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Configuração do A4T Analytics Cloud {#configuring-a-t-analytics-cloud-configuration}

Você pode configurar o Adobe Target para usar o Adobe Analytics como fonte de relatórios ao direcionar conteúdo.

>[!NOTE]
>
>A Autenticação de Credenciais de Usuário (herdada) não funciona com o A4T (para Target e Analytics). Dessa forma, os clientes devem usar a autenticação IMS em vez da autenticação User-Credential.

Para fazer isso, você precisa especificar a configuração da nuvem A4T com a qual conectar a configuração da nuvem do Adobe Target:

1. Navegar para **Cloud Services** através da **Logotipo AEM** > **Ferramentas** > **Implantação** > **Cloud Services**.
1. No **Adobe Target** seção , clique em **Configurar agora**.
1. Reconecte-se à configuração do Adobe Target.
1. No **Configuração do A4T Analytics Cloud** selecione a estrutura no menu suspenso.

   >[!NOTE]
   >
   >Somente as configurações do Analytics que estão habilitadas para A4T estão disponíveis.
   >
   >Ao configurar o A4T com AEM, você pode ver uma entrada ausente de referência de configuração. Para selecionar a estrutura do analytics, faça o seguinte:
   >
   >1. Navegar para **Ferramentas** > **Geral** > **CRXDE Lite**.
   1. Navegue até o [Caixa de diálogo de configuração do A4T Analytics](#a4t-analytics-config-dialog) (veja abaixo)
   1. Definir a propriedade **disable** para **false**.
   1. Toque ou clique **Salvar tudo**.


#### Caixa de diálogo de configuração do A4T Analytics {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

Clique em **OK**. Ao direcionar conteúdo com o Adobe Target, você pode [selecione sua fonte de relatórios](/help/sites-authoring/content-targeting-touch.md).

## Integração manual com o Adobe Target {#manually-integrating-with-adobe-target}

Integre manualmente o ao Adobe Target em vez de usar o assistente de aceitação.

>[!NOTE]
O arquivo da Biblioteca do Target, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html)O é uma nova biblioteca de implementação do Adobe Target, projetada para implementações típicas da Web e aplicativos de página única. O Adobe recomenda usar a AT.js em vez da mbox.js como a biblioteca do cliente.
A AT.js oferece várias melhorias em relação à biblioteca mbox.js:
* Tempos de carregamento de página aprimorados para implementações da Web
* Segurança aprimorada
* Melhores opções de implementação para aplicativos de página única
* A AT.js contém os componentes que foram incluídos na target.js, portanto, target.js não é mais chamada
>
Você pode selecionar AT.js ou mbox.js no **Biblioteca do cliente** menu suspenso.

### Criação de uma configuração da nuvem do Target {#creating-a-target-cloud-configuration}

Para permitir que o AEM interaja com o Adobe Target, crie uma configuração de nuvem do Target. Para criar a configuração, forneça o código de cliente do Adobe Target e as credenciais do usuário.

Você cria a configuração da nuvem do Target apenas uma vez, pois pode associar a configuração a várias campanhas AEM. Se você tiver vários códigos de cliente Adobe Target, crie uma configuração para cada código de cliente.

É possível configurar a configuração da nuvem para sincronizar segmentos do Adobe Target. Se você habilitar a sincronização, os segmentos serão importados do Target em segundo plano assim que a configuração da nuvem for salva.

Use o procedimento a seguir para criar uma configuração de nuvem do Target no AEM:

1. Navegar para **Cloud Services** através da **Logotipo AEM** > **Ferramentas** > **Implantação** > **Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   O **Adobe Marketing Cloud** a página de visão geral é aberta.

1. No **Adobe Target** seção , clique em **Configurar agora**.
1. No **Criar configuração** caixa de diálogo:

   1. Forneça uma configuração **Título**.
   1. Selecione o **Configuração do Adobe Target** modelo .
   1. Clique em **Criar**.

   A caixa de diálogo Editar é aberta.

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   Ao configurar o A4T com AEM, você pode ver uma entrada ausente de referência de configuração. Para selecionar a estrutura do analytics, faça o seguinte:
   1. Navegar para **Ferramentas** > **Geral** > **CRXDE Lite**.
   1. Navegar para **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Definir a propriedade **disable** para **false**.
   1. Toque ou clique **Salvar tudo**.


1. Na caixa de diálogo , forneça valores para essas propriedades.

   * **Código do cliente**: o Código do cliente da conta do Target
   * **E-mail**: o email da conta do Target.
   * **Senha**: a senha da conta do Target.
   * **Tipo de API**: REST ou XML
   * **Configuração do A4T Analytics Cloud**: Selecione a configuração de nuvem do Analytics usada para métricas e metas de atividade do Target. Isso é necessário se estiver usando o Adobe Analytics como fonte de relatórios ao direcionar conteúdo. Se você não vir a configuração da nuvem, consulte a observação em [Configuração do A4T Analytics Cloud](#configuring-a-t-analytics-cloud-configuration).

   * **Usar direcionamento preciso:** Por padrão, essa caixa de seleção está marcada. Se selecionada, a configuração do serviço de nuvem aguardará o contexto carregar antes de carregar o conteúdo. Veja a observação a seguir.
   * **Sincronizar segmentos do Adobe Target:** Selecione essa opção para baixar segmentos definidos no Target para usá-los em AEM. Você deve selecionar essa opção quando a propriedade Tipo de API for REST, pois os segmentos em linha não são compatíveis e você sempre precisa usar segmentos do Target. (Observe que o termo AEM de &quot;segmento&quot; equivale ao &quot;público-alvo&quot; do Target.)
   * **Biblioteca do cliente:** Selecione se deseja a biblioteca do cliente mbox.js ou AT.js.
   * **Usar o DTM para fornecer a biblioteca do cliente** - Selecione essa opção para usar AT.js ou mbox.js do DTM ou de outro sistema de gerenciamento de tags. Você deve [configurar a integração do DTM](/help/sites-administering/dtm.md) para usar essa opção. O Adobe recomenda usar o DTM em vez de AEM para entregar a biblioteca do .
   * **Mbox.js personalizada**: Deixe em branco caso tenha marcado a caixa do DTM ou para usar a mbox.js padrão. Como alternativa, carregue seu mbox.js personalizado. Somente será exibido se tiver selecionado mbox.js.
   * **AT.js personalizada**: Deixe em branco se tiver marcado a caixa do DTM ou para usar o AT.js padrão. Como alternativa, carregue sua AT.js personalizada. Somente será exibido se tiver selecionado AT.js.

   >[!NOTE]
   Por padrão, quando você opta pelo assistente de configuração do Adobe Target, o Direcionamento preciso é ativado.
   Direcionamento preciso significa que a configuração do serviço de nuvem aguarda o contexto ser carregado antes de carregar o conteúdo. Como resultado, em termos de desempenho, o direcionamento preciso pode criar um atraso de alguns milissegundos antes de carregar o conteúdo.
   O direcionamento preciso é sempre ativado na instância do autor. No entanto, na instância de publicação, é possível desativar o direcionamento preciso globalmente, limpando a marca de seleção ao lado de Direcionamento preciso na configuração do serviço de nuvem (**http://localhost:4502/etc/cloudservices.html**). Você também pode ativar e desativar o direcionamento preciso para componentes individuais, independentemente da sua configuração na configuração do serviço de nuvem.
   Se tiver ***já*** componentes direcionados criados e você altera essa configuração, suas alterações não afetam esses componentes. Você deve fazer alterações diretamente nesses componentes.

1. Clique em **Conectar-se ao Target** para inicializar a conexão com o Target. Se a conexão for bem-sucedida, a mensagem **Conexão bem-sucedida** é exibida. Clique em **OK** na mensagem e depois **OK** na caixa de diálogo.

   Se não conseguir se conectar ao Target, consulte a [solução de problemas](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) seção.

### Adicionar uma estrutura do Target {#adding-a-target-framework}

Após configurar a configuração da nuvem do Target, adicione uma estrutura do Target. A estrutura identifica os parâmetros padrão enviados para o Adobe Target a partir do [Contexto do cliente](/help/sites-administering/client-context.md) ou [ContextHub](/help/sites-developing/ch-configuring.md) componentes. O Target usa os parâmetros para determinar os segmentos que se aplicam ao contexto atual.

Você pode criar várias estruturas para uma única configuração do Target. Várias estruturas são úteis quando você precisa enviar um conjunto diferente de parâmetros para o Target para diferentes seções do seu site. Crie uma estrutura para cada conjunto de parâmetros que você precisa enviar. Associe cada seção do seu site à estrutura apropriada. Observe que uma página da Web pode usar somente uma estrutura de cada vez.

1. Na página Configuração do Target , clique no botão **+** (sinal de mais) ao lado de Frameworks disponíveis.
1. Na caixa de diálogo Criar estrutura , especifique um **Título**, selecione o **Adobe Target Framework** e clique em **Criar**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   A página da estrutura é aberta. O Sidekick fornece componentes que representam informações da [Contexto do cliente](/help/sites-administering/client-context.md) ou [ContextHub](/help/sites-developing/ch-configuring.md) que podem mapear.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Arraste o componente Contexto do Cliente que representa os dados que você deseja usar para mapear para o destino de soltar. Como alternativa, arraste a **Armazenamento do ContextHub** para a estrutura.

   >[!NOTE]
   Ao mapear, os parâmetros são enviados para uma mbox por meio de strings simples. Não é possível mapear matrizes do ContextHub.

   Por exemplo, para usar **Dados do perfil** sobre os visitantes do seu site para controlar sua campanha do Target, arraste o **Dados do perfil** para a página. As variáveis de dados de perfil disponíveis para mapeamento para parâmetros do Target são exibidas.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Selecione as variáveis que você deseja tornar visíveis para o sistema Adobe Target selecionando o **Compartilhar** caixa de seleção nas colunas apropriadas.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   A sincronização de parâmetros é uma única maneira - do AEM ao Adobe Target.

Sua estrutura foi criada. Para replicar a estrutura para a instância de publicação, use o **Ativar estrutura** no sidekick.

### Associar atividades à configuração da nuvem do Target  {#associating-activities-with-the-target-cloud-configuration}

Associe seu [Atividades AEM](/help/sites-authoring/activitylib.md) com a configuração da nuvem do Target , para que você possa espelhar as atividades no [Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html).

>[!NOTE]
Os tipos de atividades disponíveis são determinados pelo seguinte:
* Se a opção **xt_only** estiver ativada no inquilino do Adobe Target (clientcode) usado no lado do AEM para se conectar ao Adobe Target, você poderá criar **apenas** atividades XT no AEM.
* Se a opção **xt_only** **não** estiver ativada no inquilino do Adobe Target (clientcode), você poderá criar **** atividades XT e A/B no AEM.
>
**Observação adicional:** a opção **xt_only** é uma configuração aplicada em um determinado inquilino do Target (clientcode) e só pode ser modificada diretamente no Adobe Target. Não é possível ativar ou desativar essa opção no AEM.

### Associar a estrutura do Target ao seu site {#associating-the-target-framework-with-your-site}

Depois de criar uma estrutura do Target no AEM, associe suas páginas da Web à estrutura. Os componentes direcionados nas páginas enviam os dados definidos pela estrutura para o Adobe Target para rastreamento. (Consulte [Direcionamento de conteúdo](/help/sites-authoring/content-targeting-touch.md).)

Quando você associa uma página à estrutura, as páginas filhas herdam a associação.

1. No **Sites** , navegue até o site que deseja configurar.
1. Usar uma [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions) ou [modo de seleção](/help/sites-authoring/basic-handling.md), selecione **Propriedades da exibição.**
1. Selecione o **Cloud Services** guia .
1. Toque/clique **Editar**.
1. Toque/clique **Adicionar configuração** under **Configurações de Cloud Service** e selecione **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Selecione a estrutura desejada em **Referência de configuração**.

   >[!NOTE]
   Certifique-se de selecionar o **estrutura** que você criou, e não a configuração da nuvem do Target na qual ela foi criada.

1. Toque/clique **Concluído**.
1. Ative a página raiz do site para replicá-la no servidor de publicação. (Consulte [Como Publicar Páginas](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   Se a estrutura anexada à página ainda não tiver sido ativada, um assistente será aberto e você poderá publicá-la também.

## Solução de problemas de conexão do Target {#troubleshooting-target-connection-problems}

Execute as seguintes tarefas para solucionar problemas que ocorrem ao se conectar ao Target:

* Certifique-se de que as credenciais de usuário fornecidas estejam corretas.
* Certifique-se de que a instância de AEM possa se conectar ao servidor do Target. Por exemplo, verifique se as regras de firewall não estão bloqueando as conexões de AEM de saída ou se AEM configurado para usar os proxies necessários.
* Procure mensagens úteis no log de erros do AEM. O arquivo error.log está localizado na variável **crx-quickstart/logs** diretório onde o AEM está instalado.
* Ao editar a atividade no Adobe Target, o URL aponta para localhost. Solucione isso definindo o AEM externalizador para o URL correto.
