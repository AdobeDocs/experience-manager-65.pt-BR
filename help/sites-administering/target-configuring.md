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
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 30%

---

# Configuração manual da integração com o Adobe Target {#manually-configuring-the-integration-with-adobe-target}

Você pode modificar as configurações do assistente de aceitação feitas ao usar o assistente ou integrar manualmente ao Adobe Target sem usar o assistente.

## Modificação das configurações do assistente de aceitação {#modifying-the-opt-in-wizard-configurations}

A variável [Assistente de aceitação](/help/sites-administering/opt-in.md) que [integra o AEM ao Adobe Target](/help/sites-administering/target.md) O cria automaticamente uma configuração da nuvem do Target chamada Configuração do Target provisionado. O assistente também cria uma estrutura do Target para a configuração da nuvem chamada Estrutura do Target provisionada. Você pode modificar as propriedades da configuração e da estrutura da nuvem, se necessário.

Você também pode configurar o Adobe Target para usar o Adobe Target como fonte de relatórios ao direcionar conteúdo definindo a Configuração do Analytics Cloud A4T.

Para localizar a configuração da nuvem e a estrutura, acesse **Cloud Services** via **Ferramentas** > **Implantação** > **Nuvem**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)) Abaixo do Adobe Target, clique ou toque em **Exibir configurações**.

### Propriedades de Configuração do Alvo Provisionado {#provisioned-target-configuration-properties}

Os seguintes valores de propriedade são usados na configuração da nuvem da Configuração do Target provisionada criada pelo assistente de Opt-in:

* **Código do cliente:** Conforme inserido no assistente de Opt-in.
* **E-mail:** Conforme inserido no assistente de Opt-in.
* **Senha:** Conforme inserido no assistente de Opt-in.
* **Tipo de API:** REST
* **Sincronizar Segmentos Do Adobe Target:** Selecionado.

* **Biblioteca do cliente:** mbox.js.
* **Usar DTM para disponibilizar a biblioteca do cliente:** Não selecionado. Selecione esta opção se você [usar DTM](/help/sites-administering/dtm.md) ou outro sistema de gerenciamento de tags para hospedar o arquivo mbox.js ou AT.js. A Adobe recomenda usar o DTM em vez do AEM para fornecer a biblioteca.

* **Mbox.js personalizada:** Nenhum especificado, para que o arquivo mbox.js padrão seja usado. Especifique um arquivo mbox.js personalizado que deseja usar, conforme necessário. Aparece somente se você selecionou mbox.js.
* **AT.js personalizada:** Nenhum especificado, para que o arquivo AT.js padrão seja usado. Especifique um arquivo AT.js personalizado que deseja usar, conforme necessário. Aparece somente se tiver selecionado AT.js.

>[!NOTE]
>
>No AEM 6.3, é possível selecionar o arquivo Biblioteca do Target, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/)- uma nova biblioteca de implementação do Adobe Target, projetada para implementações típicas da Web e aplicativos de página única.
>
>A AT.js oferece várias melhorias em relação à biblioteca mbox.js:
>
>* Tempos de carregamento de página aprimorados para implementações da Web
>* Segurança aprimorada
>* Melhores opções de implementação para aplicativos de página única
>* A AT.js contém os componentes que foram incluídos na target.js, portanto, não é mais chamada para o target.

<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Propriedades da Estrutura de Destino Provisionada {#provisioned-target-framework-properties}

A Estrutura de destino provisionada que o assistente de Opt-in cria está configurada para enviar dados de contexto do armazenamento de Dados do perfil. A idade e os itens de dados de gênero do armazenamento são enviados para o Target por padrão. Sua solução provavelmente requer o envio de parâmetros adicionais.

![Estrutura de Destino Provisionada](assets/chlimage_1-158.png)

Você pode configurar a estrutura para enviar informações de contexto adicionais ao Target, conforme descrito em [Adição de uma estrutura do Target](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Definição da Configuração do A4T Analytics Cloud {#configuring-a-t-analytics-cloud-configuration}

Você pode configurar o Adobe Target para usar o Adobe Analytics como fonte de relatórios ao direcionar conteúdo.

>[!NOTE]
>
>A Autenticação de credencial de usuário (herdada) não funciona com o A4T (tanto para o Target quanto para o Analytics). Dessa forma, os clientes devem usar a autenticação IMS em vez da autenticação de credencial do usuário.

Para fazer isso, você especifica com qual configuração de nuvem do A4T deve se conectar à configuração de nuvem do Adobe Target:

1. Navegue até **Cloud Services** por meio da **Logotipo do AEM** > **Ferramentas** > **Implantação** > **Cloud Services**.
1. Na seção **Adobe Target**, clique em **Configurar agora**.
1. Reconecte-se à configuração do Adobe Target.
1. No **Configuração do A4T Analytics Cloud** selecione a estrutura.

   >[!NOTE]
   >
   >Somente as configurações do Analytics habilitadas para A4T estão disponíveis.
   >
   >Ao configurar o A4T com AEM, você pode ver uma entrada ausente na referência Configuração. Para poder selecionar a estrutura de análise, faça o seguinte:
   >
   >1. Navegue até **Ferramentas** > **Geral** > **CRXDE Lite**.
   1. Navegue até a [Caixa de diálogo Configuração do A4T Analytics](#a4t-analytics-config-dialog) (veja abaixo)
   1. Definir a propriedade **disable** para **false**.
   1. Toque ou clique **Salvar tudo**.

#### Caixa de diálogo Configuração do A4T Analytics {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

Clique em **OK**. Ao direcionar conteúdo com o Adobe Target, você pode [selecione sua fonte de relatório](/help/sites-authoring/content-targeting-touch.md).

## Integração manual com o Adobe Target {#manually-integrating-with-adobe-target}

Integrar manualmente ao Adobe Target em vez de usar o assistente de aceitação.

>[!NOTE]
>
O arquivo da biblioteca do Target, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/), é uma nova biblioteca de implementação do Adobe Target, projetada para implementações típicas da Web e aplicativos de página única. A Adobe recomenda usar a AT.js como a biblioteca de cliente, em vez da mbox.js.
>
A AT.js oferece várias melhorias em relação à biblioteca mbox.js:
>
* Tempos de carregamento de página aprimorados para implementações da Web
* Segurança aprimorada
* Melhores opções de implementação para aplicativos de página única
* A AT.js contém os componentes que foram incluídos na target.js, portanto, a target.js não é mais chamada
>
É possível selecionar AT.js ou mbox.js no menu suspenso **Biblioteca do cliente**.

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Criação de uma configuração da nuvem do Target {#creating-a-target-cloud-configuration}

Para permitir que o AEM interaja com o Adobe Target, crie uma configuração da nuvem do Target. Para criar a configuração, forneça o código de cliente do Adobe Target e as credenciais do usuário.

Você precisa criar a configuração da nuvem do Target apenas uma vez, pois é possível associá-la a várias campanhas do AEM. Se você tiver vários códigos de cliente do Adobe Target, crie uma configuração para cada código de cliente.

É possível definir a configuração da nuvem para sincronizar segmentos do Adobe Target. Se você habilitar a sincronização, os segmentos serão importados do Target em segundo plano quando a configuração da nuvem for salva.

Use o procedimento a seguir para criar uma configuração da nuvem do Target no AEM:

1. Navegue até **Cloud Services** por meio da **Logotipo do AEM** > **Ferramentas** > **Cloud Services** > **Cloud Services herdados**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   A variável **Cloud Services** visão geral é aberta.

1. Na seção **Adobe Target**, clique em **Configurar agora**.
1. Na caixa de diálogo **Criar configuração**:

   1. Forneça um **Título** à configuração.
   1. Selecione o modelo da **Configuração do Adobe Target**.
   1. Clique em **Criar**.

   A caixa de diálogo de edição é aberta.

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   >
   Ao configurar o A4T com AEM, você pode ver uma entrada ausente na referência Configuração. Para poder selecionar a estrutura de análise, faça o seguinte:
   >
   1. Navegue até **Ferramentas** > **Geral** > **CRXDE Lite**.
   1. Navegue até **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Definir a propriedade **disable** para **false**.
   1. Toque ou clique **Salvar tudo**.

1. Na caixa de diálogo, forneça valores para essas propriedades.

   * **Código do cliente**: o código do cliente da conta do Target
   * **E-mail**: o email da conta do Target.
   * **Senha**: a senha da conta do Target.
   * **Tipo de API**: REST ou XML
   * **Configuração do A4T Analytics Cloud**: selecione a configuração do Analytics Cloud usada para métricas e metas da atividade de direcionamento. Essa configuração é necessária se estiver usando o Adobe Analytics como fonte de relatórios ao direcionar conteúdo. Se você não vir a configuração da nuvem, consulte a observação em [Definição da Configuração do A4T Analytics Cloud](#configuring-a-t-analytics-cloud-configuration).

   * **Usar direcionamento preciso:** por padrão, essa caixa de seleção está marcada. Se selecionada, a configuração do Cloud Service aguarda o contexto ser carregado antes de carregar o conteúdo. Veja a observação a seguir.
   * **Sincronizar segmentos do Adobe Target:** Selecione esta opção para baixar segmentos definidos no Target e usá-los no AEM. Selecione essa opção quando a propriedade Tipo de API for REST, pois os segmentos em linha não são compatíveis e você deve usar segmentos do Target. (O termo AEM de &quot;segmento&quot; é equivalente ao termo &quot;público-alvo&quot; do Target.)
   * **Biblioteca do cliente:** Selecione se deseja a biblioteca do cliente mbox.js ou AT.js.
   * **Usar DTM para disponibilizar a biblioteca do cliente** : selecione essa opção para usar AT.js ou mbox.js do DTM ou outro sistema de gerenciamento de tags. Configurar [a integração do DTM](/help/sites-administering/dtm.md) para usar essa opção. A Adobe recomenda usar o DTM em vez do AEM para fornecer a biblioteca.
   * **mbox.js personalizada**: Deixe em branco se tiver marcado a caixa do DTM ou para usar a mbox.js padrão. Como alternativa, carregue a mbox.js personalizada. Aparece somente se você selecionou mbox.js.
   * **AT.js personalizada**: Deixe em branco se tiver marcado a caixa do DTM ou para usar a AT.js padrão. Como alternativa, faça upload do seu AT.js personalizado. Aparece somente se tiver selecionado AT.js.

   >[!NOTE]
   >
   Por padrão, quando você opta pelo assistente de configuração do Adobe Target, o Direcionamento preciso é ativado.
   >
   Direcionamento preciso significa que a configuração do Cloud Service aguarda o contexto ser carregado antes de carregar o conteúdo. Como resultado, em termos de desempenho, o direcionamento preciso pode criar um atraso de alguns milissegundos antes de carregar o conteúdo.
   >
   O direcionamento preciso é sempre ativado na instância do autor. No entanto, na instância de publicação, é possível desativar o direcionamento preciso globalmente, limpando a marca de seleção ao lado de Direcionamento preciso na configuração do Cloud Service (**http://localhost:4502/etc/cloudservices.html**). Você também pode ativar e desativar o direcionamento preciso para componentes individuais, independentemente das suas definições na configuração do Cloud Service.
   >
   Se você ***já*** tiver criado componentes direcionados e alterar essa configuração, suas alterações não afetarão esses componentes. Altere esses componentes diretamente.

1. Clique em **Conectar-se ao Target** para inicializar a conexão com o Target. Se a conexão for bem-sucedida, a mensagem **Conexão bem-sucedida** será exibida. Clique em **OK** na mensagem e, em seguida, em **OK** na caixa de diálogo.

   Se não conseguir se conectar ao Target, consulte a seção [solução de problemas](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems).

### Adicionar uma estrutura do Target {#adding-a-target-framework}

Após definir a configuração da nuvem do Target, adicione uma estrutura do Target. A estrutura identifica os parâmetros padrão enviados para o Adobe Target a partir das [Client Context](/help/sites-administering/client-context.md) ou [ContextHub](/help/sites-developing/ch-configuring.md) componentes. O Target usa os parâmetros para determinar os segmentos que se aplicam ao contexto atual.

Você pode criar várias estruturas para uma única configuração do Target. Várias estruturas são úteis quando você deve enviar um conjunto diferente de parâmetros ao Target para diferentes seções do seu site. Crie uma estrutura para cada conjunto de parâmetros enviados. Associe cada seção do site à estrutura apropriada. Uma página da Web pode usar somente uma estrutura por vez.

1. Na página de configuração do Target, clique no link **+** (sinal de adição) ao lado de Estruturas disponíveis.
1. Na caixa de diálogo Criar estrutura, especifique um **Título**, selecione a **estrutura do Adobe Target** e clique em **Criar**.

   ![Caixa de diálogo Criar estrutura](assets/chlimage_1-161.png)

   A página de estrutura é aberta. O Sidekick fornece componentes que representam informações do [Client Context](/help/sites-administering/client-context.md) ou [ContextHub](/help/sites-developing/ch-configuring.md) que você pode mapear.

   ![Componentes da estrutura](assets/chlimage_1-162.png)

1. Arraste o componente Contexto do cliente que representa os dados que você deseja usar para mapear até a zona de destino. Como alternativa, arraste o componente de **Armazenamento do ContextHub** para a estrutura.

   >[!NOTE]
   >
   Ao mapear, os parâmetros são enviados para uma mbox por meio de sequências de caracteres simples. Não é possível mapear matrizes do ContextHub.

   Por exemplo, para usar **Dados do perfil** sobre os visitantes do seu site para controlar sua campanha do Target, arraste o **Dados do perfil** componente à página. As variáveis de dados de perfil disponíveis para mapeamento para parâmetros do Target são exibidas.

   ![Dados do perfil](assets/chlimage_1-163.png)

1. Selecione as variáveis que você deseja tornar visíveis para o sistema do Adobe Target marcando a caixa de seleção **Compartilhar** nas colunas apropriadas.

   ![Compartilhar](assets/chlimage_1-164.png)

   >[!NOTE]
   >
   A sincronização de parâmetros é uma via de mão única - do AEM para o Adobe Target.

Sua estrutura foi criada. Para replicar a estrutura para a instância de publicação, use a opção **Ativar estrutura** no sidekick.

### Associação de atividades com a configuração de nuvem do Target  {#associating-activities-with-the-target-cloud-configuration}

Associe seu [Atividades do AEM](/help/sites-authoring/activitylib.md) com sua configuração da nuvem do Target, para que você possa espelhar as atividades em [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
Os tipos de atividades disponíveis são determinados pelo seguinte:
>
>
* Se a variável **xt_only** estiver ativada no locatário do Adobe Target (clientcode) usado no lado do AEM para se conectar ao Adobe Target, você poderá criar **somente** Atividades XT no AEM.
>
* Se a variável **xt_only** opção é **não** ativada no locatário do Adobe Target (clientcode), será possível criar **ambos** Atividades XT e A/B no AEM.
>
**Nota adicional:** **xt_only** é uma configuração aplicada em um determinado locatário do Target (clientcode) e só pode ser modificada diretamente no Adobe Target. Não é possível ativar ou desativar essa opção no AEM.

### Associar a estrutura do Target ao seu site {#associating-the-target-framework-with-your-site}

Depois de criar uma estrutura do Target no AEM, associe suas páginas da Web à estrutura. Os componentes direcionados nas páginas enviam os dados definidos pela estrutura para o Adobe Target para rastreamento. (Consulte [Direcionamento de conteúdo](/help/sites-authoring/content-targeting-touch.md).)

Quando você associa uma página à estrutura, as páginas secundárias herdam a associação.

1. No **Sites** console, navegue até o site que deseja configurar.
1. Usar um dos [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions) ou [modo de seleção](/help/sites-authoring/basic-handling.md), selecione **Propriedades da exibição.**
1. Selecione a guia **Cloud Services**.
1. Toque/clique em **Editar**.
1. Toque/clique **Adicionar configuração** em **Configurações do Cloud Service** e selecione **Adobe Target**.

   ![Adicionar configuração](assets/chlimage_1-165.png)

1. Selecione a estrutura desejada em **Referência de configuração**.

   >[!NOTE]
   >
   Certifique-se de selecionar as opções **estrutura** que você criou e não a configuração da nuvem do Target na qual ela foi criada.

1. Toque/clique **Concluído**.
1. Ative a página raiz do site para replicá-la no servidor de publicação. (Consulte [Como Publicar Páginas](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   >
   Se a estrutura anexada à página ainda não tiver sido ativada, um assistente será aberto para que você também possa publicá-la.

## Resolução de Problemas de Conexão do Target {#troubleshooting-target-connection-problems}

Para solucionar problemas que ocorrem ao se conectar ao Target, você pode executar as seguintes tarefas:

* Verifique se as credenciais de usuário fornecidas estão corretas.
* Verifique se a instância do AEM pode se conectar ao servidor do Target. Por exemplo, verifique se as regras de firewall não estão bloqueando as conexões de saída com o AEM ou se o AEM está configurado para usar os proxies necessários.
* Procure mensagens úteis no registro de erros do AEM. O arquivo error.log está no estado **crx-quickstart/logs** diretório onde o AEM está instalado.
* Ao editar a atividade no Adobe Target, o URL aponta para o host local. Resolva esse problema definindo o Externalizador de AEM para o URL correto.
