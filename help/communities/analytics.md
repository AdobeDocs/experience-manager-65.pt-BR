---
title: Configuração do Analytics para recursos das Comunidades
seo-title: Configuração do Analytics para recursos das Comunidades
description: Configurar o Analytics para Comunidades
seo-description: Configurar o Analytics para Comunidades
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
source-git-commit: fcdadcf691ed5a569a5a40ca070f8ec266ec3eb9
workflow-type: tm+mt
source-wordcount: '2756'
ht-degree: 4%

---

# Configuração do Analytics para recursos das Comunidades {#analytics-configuration-for-communities-features}

## Visão geral {#overview}

A Adobe Analytics e a Adobe Experience Manager (AEM) são soluções da Adobe Marketing Cloud.

O Adobe Analytics pode ser configurado para o AEM Communities de forma que, à medida que um membro interage com os recursos das Comunidades compatíveis, os eventos sejam enviados para o Adobe Analytics a partir do qual os relatórios são gerados.

Por exemplo, quando um membro de um site da comunidade de ativação exibir um recurso de vídeo atribuído a ele, o reprodutor de recursos enviará eventos para o Analytics, incluindo dados de pulsação de vídeo. No site da comunidade, os administradores podem visualizar vários relatórios sobre a reprodução do vídeo.

Além disso, o analytics é necessário para:

* No ambiente de publicação:

   * Relatórios sobre a comunidade [tendências](/help/communities/trends.md)
   * Permitir que os visitantes do site classifiquem por &quot;mais visualizados&quot;, &quot;mais ativos&quot;, &quot;mais curtidos&quot;
   * Exibir contagens em listas UGC

* No ambiente de criação:

   * Exibição dos dados de participação no [console de gerenciamento de membros](/help/communities/members.md) (exibições, postagens, seguidores, curtidas)
   * Resumo de tendências, pulsação de vídeo e dispositivo de vídeo para ativar o recurso [relatórios](/help/communities/reports.md)

Os recursos suportados das Comunidades incluem:

* [Recursos de habilitação](/help/communities/resources.md)
* [Fórum](/help/communities/forum.md)
* [Perguntas e respostas](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Biblioteca de arquivos](/help/communities/file-library.md)
* [Calendário](/help/communities/calendar.md)

Esta seção da documentação descreve como conectar um conjunto de relatórios do Analytics com recursos das Comunidades. As etapas básicas são:

1. [Replicar a ](#replicate-the-crypto-key) chave de criptografia para garantir que a criptografia/descriptografia ocorra corretamente em todas as instâncias AEM
1. Preparar um conjunto de relatórios [do Adobe Analytics](#adobe-analytics-report-suite-for-video-reporting)
1. Criar um serviço de nuvem AEM Analytics [e [framework](#aem-analytics-framework-configuration)](#aem-analytics-cloud-service-configuration)

1. [Ativar o ](#enable-analytics-for-a-community-site) Analytics para um site da comunidade
1. [****](#verify-analytics-to-aem-variable-mapping) Verificar o Analytics para AEM o mapeamento de variável
1. Identificar [publicador primário](#primary-publisher)
1. [](#publish-community-site-and-analytics-cloud-service) Publicar o site da comunidade
1. Configurar [importação de dados de relatório](#obtaining-reports-from-analytics) do Adobe Analytics para o site da comunidade

## Pré-requisitos {#prerequisites}

Para configurar os recursos do Analytics for Communities, é necessário trabalhar com seu representante de conta para configurar uma conta do Adobe Analytics e [conjunto de relatórios](#adobe-analytics-report-suite-for-video-reporting). Uma vez estabelecidas, devem estar disponíveis as seguintes informações:

* **Nome da empresa**

   A empresa associada à conta da Adobe Analytics.

* **Nome de usuário**

   O nome de usuário de logon do usuário autorizado a gerenciar a conta do Analytics
(deve incluir privilégios de acesso ao serviço da Web).

* **Senha**

   A senha de logon do usuário autorizado.

* **Data Center do Analytics**

   O URL do data center do Analytics para a conta.

* **Conjunto de relatórios**

   O nome do conjunto de relatórios do Analytics a ser usado.

## Relatório do Conjunto de relatórios do Adobe Analytics para vídeo {#adobe-analytics-report-suite-for-video-reporting}

Usando o [Gerenciador de conjunto de relatórios](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html) da Adobe Marketing Cloud, os conjuntos de relatórios do Analytics podem ser configurados para que um site da comunidade possa ser habilitado para fornecer relatórios sobre os recursos das Comunidades.

Ao fazer logon em [Adobe Experience Cloud](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html) com [Nome da empresa e Nome do usuário](/help/communities/analytics.md#prerequisites), é possível configurar um conjunto de relatórios novo ou existente para ter:

* [11 Variáveis](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html)  de conversão (eVars)

   * **`evar1`** por meio de  **`evar11`** ativação

   * Pode redefinir a finalidade (renomear) das eVars existentes ou criar novas para usar nos recursos das Comunidades

* [7 Eventos bem-sucedidos](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html)  (eventos)

   * **`event1`** por meio de  **`event7`** ativação

   * tipo **`Counter`**

      * not **`Counter (no subrelations)`**
   * Pode redefinir (renomear) os eventos existentes ou criar novos eventos para usar nos recursos das Comunidades


* [Gerenciamento de vídeo](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * Console de relatórios de vídeo

      * Ativar `Video Core`
      * Selecione Salvar
   * Console de medição do vídeo principal

      * Selecionar `Use Solution Variables`
      * Selecione Salvar


Se estiver usando um **novo conjunto de relatórios**, esteja ciente de que um novo conjunto de relatórios pode ter apenas 4 evars e 6 variáveis de evento, enquanto 11 evars e 7 vars de evento são necessárias para Comunidades.

Se estiver usando um **conjunto de relatórios existente**, pode ser necessário [modificar o mapeamento de variável](#modifying-analytics-variable-mapping) antes de ativar a estrutura do Analytics para um site da comunidade.

Entre em contato com o representante de conta para obter informações sobre as variáveis dedicadas às Comunidades.

>[!CAUTION]
>
>**Se estiver usando um conjunto de relatórios existente que já usa variáveis no**
>
>* **`evar1`** a **`evar11`**
   >
   >
* **`event1`** a **`event7`**
>
>
**Depois, antes de o site da comunidade ser publicado,** é importante restaurar o mapeamento pré-existente, movendo as variáveis de AEM que foram mapeadas automaticamente para as variáveis do Analytics quando o Analytics foi ativado para um site da comunidade.
>
>Para restaurar o mapeamento pré-existente e mover variáveis AEM para outras variáveis do Analytics, consulte a seção sobre [Modificar o mapeamento de variável do Analytics](#modifying-analytics-variable-mapping).
>
>Se isso não for feito, poderá ocorrer perda irrecuperável de dados.

### Análise do Video Heartbeat {#video-heartbeat-analytics}

Quando o Video Heartbeat Analytics está licenciado, um `Marketing Cloud Org Id` é atribuído.

Para ativar o relatório do Video Heartbeat após [configurar o conjunto de relatórios do Analytics para o relatório de vídeo](#adobe-analytics-report-suite-for-video-reporting):

* Criar um [serviço em nuvem do Analytics](#aem-analytics-cloud-service-configuration)
* Ativar [Analytics para um site da comunidade](#enable-analytics-for-a-community-site)
* Associe o `Marketing Cloud Org Id` ao site da comunidade

O `Marketing Cloud Org Id` pode ser inserido no momento de [criação de site da comunidade](/help/communities/sites-console.md#enablement) ou posterior por [modificação](/help/communities/sites-console.md#modifying-site-properties) das propriedades de site da comunidade.

![marketing-org-id](assets/marketing-org-id.png)

Quando a Análise do Video Heartbeat está ativada, o código JavaScript (JS) do reprodutor de vídeo instancia o código da biblioteca do Video Heartbeat (também no JS), que lida com toda a lógica para enviar atualizações de status de vídeo para os servidores de rastreamento de vídeo do Analytics a cada 10 segundos (não configurável) e, eventualmente, enviar um relatório cumulativo da sessão de vídeo para os principais servidores do Analytics.

Se não estiver habilitado, o código da pulsação de vídeo nunca será instanciado e somente o rastreamento do progresso e da posição de retomada do vídeo será mantido no SRP para gerar relatórios.

## Configuração do serviço Analytics Cloud AEM {#aem-analytics-cloud-service-configuration}

Para criar uma nova Integração do Analytics, que integra o Adobe Analytics ao site da comunidade de AEM, usando a interface padrão na instância do autor:

* Na navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**
* Role para baixo até **[!UICONTROL Adobe Analytics]**
* Selecione **[!UICONTROL Configurar agora]** ou **[!UICONTROL Mostrar configurações]**

![cloud-config](assets/cloud-config1.png)

### Caixa de diálogo Criar configuração {#create-configuration-dialog}

* Selecione o ícone `[+]` ao lado de **[!UICONTROL Configurações disponíveis]** para criar uma nova configuração

Na caixa de diálogo Criar configuração , os valores a serem inseridos identificam a configuração.

![create-cloud-config](assets/cloud-config2.png)

* **Título**

   (Obrigatório) Um título de exibição para a configuração.
Por exemplo, digite *Ativar o Analytics da comunidade*

* **Nome**

   (Opcional) Se não especificado, o nome assumirá como padrão um nome de nó válido derivado do título.
Por exemplo, insira *communities*

* **Modelo**

   Selecionar `Adobe Analytics Configuration`

* Selecione **Criar**

   * Inicia a página de configuração e abre a caixa de diálogo `Analytics Settings`

### Caixa de diálogo Configurações do Analytics {#analytics-settings-dialog}

A criação inicial de uma nova configuração do Analytics resulta na exibição da configuração e em uma nova caixa de diálogo para a entrada das Configurações do Analytics. Essa caixa de diálogo requer as [informações de pré-requisito da conta](#prerequisites) obtidas do representante da conta.

![analytics-settings](assets/analytics-settings.png)

* **Empresa**

   A empresa associada à conta da Adobe Analytics.

* **Nome de usuário**

   O nome de usuário de logon do usuário autorizado a gerenciar a conta do Analytics.

* **Senha**

   A senha de logon do usuário autorizado.

* **Centro de dados**

   Selecione o data center do Analytics que hospeda o conjunto de relatórios.

* **Não adicionar a tag de rastreamento à página**

   Deixe como padrão (desmarcado).

* **Usar AppMeasurement**

   Deixe como padrão (desmarcado).

* **Não realizar importações de impressões de página todas as noites (autor)**

   Deixe como padrão (desmarcado).

* **Não realizar importações de impressões de página todas as noites (publicar)**

   Deixe como padrão (desmarcado).

Para salvar as configurações:

* Selecione **Conectar-se ao Analytics**

   * Se não tiver êxito,

      * Verifique se as entradas não contêm espaços à esquerda.
      * Tente um data center diferente.

* Selecione **OK**.

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### Criar estrutura {#create-framework}

Após a configuração bem-sucedida da conexão básica com o Adobe Analytics, é necessário criar ou editar uma estrutura para o site da comunidade. A finalidade da estrutura é mapear as variáveis de recurso (AEM) das Comunidades para variáveis do Analytics (conjunto de relatórios).

* Selecione o ícone `[+]` ao lado de **[!UICONTROL Frameworks disponíveis]** para criar uma nova estrutura

   ![analytics-framework](assets/analytics-framework.png)

* **Título**

   (Obrigatório) Um título de exibição para a estrutura
Por exemplo, digite *Estrutura da comunidade de ativação*.

* **Nome**

   (Opcional) Se não especificado, o nome assumirá como padrão um nome de nó válido derivado do título.
Por exemplo, digite *communities*.

* *Modelo*

   Selecionar `Adobe Analytics Framework`.

* Selecione **Criar**.

A criação da Estrutura do Analytics abre a estrutura para configuração.

## Configuração da estrutura do AEM Analytics {#aem-analytics-framework-configuration}

A finalidade da estrutura é mapear variáveis AEM para variáveis do Analytics (eVars e eventos). As variáveis do Analytics disponíveis para mapeamento são [definidas no conjunto de relatórios](#adobe-analytics-report-suite-for-video-reporting).

![analytics-enablement-framework](assets/analytics-framework1.png)

### Selecionar Conjunto de relatórios {#select-report-suite}

Selecione o conjunto de relatórios que foi configurado para relatórios de vídeo.

Se um conjunto de relatórios ainda não tiver sido criado ou não tiver sido configurado corretamente, consulte a seção anterior:
[Conjunto de relatórios do Adobe Analytics para relatórios de vídeo](#adobe-analytics-report-suite-for-video-reporting)

O Sidekick não é necessário e pode ser minimizado para que não obstrua o acesso às configurações dos Conjuntos de relatórios.

#### Caixa de diálogo Conjuntos de relatórios antes e depois de selecionar &#39;Adicionar item&#39; {#report-suites-dialog-before-and-after-selecting-add-item}

![conjunto de relatórios](assets/report-suite.png)

1. Selecione **Adicionar Item +**.

   Duas caixas suspensas são exibidas.

1. Escolha um `Report suite.`

   Os conjuntos de relatórios associados à conta da Empresa estão disponíveis para seleção.

1. Selecione **Yes** na caixa de diálogo que é aberta:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Escolha um `Run Mode`.

1. Selecione **Publicar**.

![analytics-framework2](assets/analytics-framework2.png)

O serviço e a estrutura de nuvem do Analytics estão concluídos. Os Mapeamentos serão definidos assim que um site da comunidade for criado com este serviço do Analytics ativado.

## Ativar o Analytics para um site da comunidade {#enable-analytics-for-a-community-site}

### Ativar para Novo Site da Comunidade {#enable-for-new-community-site}

Para adicionar o serviço de nuvem do Analytics enquanto [cria um novo site da comunidade](/help/communities/sites-console.md):

* Na etapa 3, na guia [ANALYTICS](/help/communities/sites-console.md#analytics):
   * Marque a caixa de seleção **Ativar o Analytics** .
   * Selecione a estrutura na caixa suspensa .

* Como opção, retorne à configuração da estrutura do Analytics para ajustar os mapeamentos de variáveis.

### Habilitar para site da comunidade existente {#enable-for-existing-community-site}

Para adicionar o serviço de nuvem do Analytics a um [site da comunidade existente](/help/communities/sites-console.md#modifying-site-properties):

* Navegue até o console **Communities > Sites** .
* Selecione o ícone Editar Site do site da comunidade.
* Selecione as CONFIGURAÇÕES.
* Na seção Analytics :
   * Marque a caixa de seleção **Ativar o Analytics** .
   * Escolha a estrutura na caixa suspensa .

* Como opção, retorne à configuração da estrutura do Analytics para ajustar os mapeamentos de variáveis.

### Ativar para sites personalizados {#enable-for-customized-sites}

Para que o rastreamento e a importação do Analytics funcionem corretamente para um site da comunidade, um elemento de página com a classe `scf-js-site-title` e os atributos href devem estar presentes. Somente um desses elementos deve existir na página, como ocorre em um script `sitepage.hbs` não modificado para um site da comunidade. O valor de `siteUrl` é extraído e enviado para o Adobe Analytics como o *caminho do site*.

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

Para um **site da comunidade personalizado** que sobrepõe o script `sitepage.hbs`, verifique se o elemento está presente. A variável `siteUrl` será definida quando renderizada no servidor antes de servir ao cliente.

Para um **site de AEM genérico** que inclui componentes do Communities, mas não é criado com o [assistente de criação de site](/help/communities/sites-console.md), é necessário adicionar o elemento . O valor da href deve ser o caminho para o site. Por exemplo, se o caminho do site for `/content/my/company/en`, use:

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Recursos do Analytics for Communities {#analytics-for-communities-features}

O Analytics é usado automaticamente para vários recursos das Comunidades.

A [configuração OSGi do ambiente do autor](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`, fornece uma listagem dos componentes que foram instrumentados para o Analytics. O mapeamento automático de variáveis é determinado pelos componentes listados.

Se forem criados novos componentes personalizados instrumentados para o Analytics, eles deverão ser adicionados a esta lista de componentes configurados.

### Configuração do componente {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>Os componentes do diário são usados para implementar o recurso de blog.

### Análise mapeada para variáveis de AEM {#mapped-analytics-to-aem-variables}

Depois que o site da comunidade é salvo com o Analytics ativado e a estrutura de configuração de nuvem selecionada, as variáveis de AEM são mapeadas automaticamente para as eVars e os eventos do Analytics que começam com evar1 e event1, respectivamente, e aumentam em 1.

Se estiver usando um conjunto de relatórios existente que mapeou qualquer uma das variáveis dentro de evar1 até evar11 e event1 até event7, será necessário [remapear as variáveis AEM](#modifying-analytics-variable-mapping) e restaurar o mapeamento original.

A seguir, um exemplo de mapeamentos padrão após seguir o tutorial [getting started](/help/communities/getting-started-enablement.md):

![map-analytics](assets/map-analytics1.png)

#### Mapa de eVars enviadas com cada evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Tipo de Ativação<br /> Recurso<br /></strong></td>
   <td><strong>Título do Site<br /></strong></td>
   <td><strong>Tipo de função<br /></strong></td>
   <td><strong>Título do Grupo<br /></strong></td>
   <td><strong>Caminho do Grupo<br /></strong></td>
   <td><strong>Tipo de UGC<br /></strong></td>
   <td><strong>Título do UGC<br /></strong></td>
   <td><strong>Usuário<br /> (Membro)</strong></td>
   <td><strong>Caminho UGC<br /></strong></td>
   <td><strong>Caminho do Site<br /></strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar 4</strong></td>
   <td><strong>eVar 5</strong></td>
   <td><strong>eVar 6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>Reprodução de Recurso event1<br /></strong></td>
   <td><em>(uma sessão gerenciada no quadro branco)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>(uma sessão gerenciada no quadro branco)</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
 </tbody>
</table>

**Exemplos de valores de eVar :**

* *[Tipo](https://www.iana.org/assignments/media-types)* MIME: video/mp4
* *[título](/help/communities/sites-console.md#step13asitetemplate)* do site da comunidade: Comunidades Geometrixx
* *[nome](/help/communities/functions.md)* da função da comunidade: Fórum
* *[nome](/help/communities/creating-groups.md#creating-a-new-group)* do grupo da comunidade: Caminho
* *caminho para o conteúdo* do grupo da comunidade:  `/content/sites/<site name>/en/groups/hiking`
* *[Tipo de recurso do componente UGC](/help/communities/essentials.md)*:  `social/forum/components/hbs/topic`
* *Título* do componente UGC: Tópicos de rastreamento
* *login (authorizableId)*:  `aaron.mcdonald@mailinator.com`
* *Caminho SRP para UGC*:  `/content/usergenerated/asi/.../forum/jmtz-topic3`
ou 
*caminho do componente a seguir*:  `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *caminho para o conteúdo* do site da comunidade:  `/content/sites/<site name>/en`

### Modificação do mapeamento de variável do Analytics {#modifying-analytics-variable-mapping}

O mapeamento de eVars e eventos do Analytics para variáveis de AEM é visível da configuração da estrutura depois que o Analytics é ativado para um site da comunidade.

Depois que o Analytics for ativado e antes que o site da comunidade seja publicado, o mapeamento poderá ser alterado na estrutura, arrastando a eVar ou o evento do Analytics desejado do painel esquerdo e soltando-o na linha relevante na tabela de mapeamento.

Para evitar mapeamentos duplicados, remova a evar ou o evento do Analytics substituído da linha ao passar o mouse sobre ela e selecionar o &quot;X&quot; que aparece à direita do elemento de variável do Analytics.

Se as eVars e os eventos do Communities substituírem os mapeamentos que pré-existiam no conjunto de relatórios e, em seguida, para evitar perda de dados, atribua as variáveis de AEM para os recursos do Communities a outras eVars ou eventos do Analytics e restaure os mapeamentos originais.

>[!CAUTION]
>
>É importante remapear antes que o site da comunidade seja [publicado](#publishing-the-community-site) com o Analytics ativado, caso contrário há risco de perda de dados.

#### Exemplo da Etapa 1: Arrastar a evar14 do Analytics para a tabela de mapeamento {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### Exemplo da Etapa 2: Selecionar &#39;x&#39; para remover evar11 substituído {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### Exemplo da Etapa 3: AEM var eventdata.siteId remapeado para a evar14 do Analytics {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## Publicar o site da comunidade {#publishing-the-community-site}

### Verifique o Analytics para AEM o mapeamento de variáveis {#verify-analytics-to-aem-variable-mapping}

É recomendável verificar o mapeamento de variável antes de publicar o site da comunidade, que também publica o serviço de nuvem e a estrutura do Analytics.

Consulte as seções:

* [Análise mapeada para variáveis de AEM](#mapped-analytics-to-aem-variables)
* [Modificação do mapeamento de variável do Analytics](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Se estiver usando um conjunto de relatórios existente que já usa variáveis no**
>
>* **`evar1`** a **`evar11`**
   >
   >
* **`event1`** a **`event7`**
>
>
**Depois, antes de o site da comunidade ser publicado,** é importante restaurar o mapeamento preexistente e mover as variáveis do AEM Comunidades que foram mapeadas automaticamente (quando o Analytics foi ativado para o site da comunidade) para outras variáveis do Analytics. Esse remapeamento deve ser consistente em todos os componentes das Comunidades.
>
>Se isso não for feito, poderá ocorrer perda irrecuperável de dados.

### Editor principal {#primary-publisher}

Quando a implantação escolhida é um [publish farm](/help/communities/topologies.md#tarmk-publish-farm), uma instância de publicação AEM deve ser identificada como o editor principal para polling Adobe Analytics para que os dados do relatório gravem em [SRP](/help/communities/working-with-srp.md).

Por padrão, a configuração `AEM Communities Publisher Configuration` OSGi identifica sua instância de publicação como o editor principal, de modo que todas as instâncias de publicação em um farm de publicação se autoidentificariam como as primárias.

Portanto, é necessário editar a configuração em todas as instâncias de publicação secundárias para desmarcar a caixa de seleção **Editor Principal**.

Para obter instruções específicas, consulte a seção Editor principal de [Implantação de comunidades](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>É importante que o editor principal seja configurado para impedir a pesquisa de várias instâncias de publicação.

### Replicar a chave de criptografia {#replicate-the-crypto-key}

As credenciais do Adobe Analytics são criptografadas. Para facilitar a replicação ou a transmissão de credenciais de análise criptografadas entre o autor e os editores, todas as instâncias AEM devem compartilhar a mesma chave de criptografia primária.

Para fazer isso, siga as instruções em [Replicate the Crypto Key](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Publicar site da comunidade e serviço do Analytics Cloud {#publish-community-site-and-analytics-cloud-service}

Depois que o serviço de nuvem do Analytics for ativado para um site da comunidade e, se necessário, o [mapping do Analytics para AEM variáveis tiver sido ajustado](#mapped-analytics-to-aem-variables), é necessário replicar a configuração para o ambiente de publicação [(re)publicando o site da comunidade](/help/communities/sites-console.md#publishing-the-site).

## Obter relatórios do Analytics {#obtaining-reports-from-analytics}

### Gerenciamento de relatórios {#report-management}

A configuração [OSGi do autor e do editor principal](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`, é usada para consultar o Analytics.

No autor, as consultas são para relatórios em tempo real.

No editor principal, as consultas são usadas para fornecer informações em preparação para a importação de dados do Analytics do Importador de relatórios.

O padrão do intervalo de query é 10 segundos.

### Importador de relatórios {#report-importer}

Depois que um site da comunidade habilitado para o Analytics for publicado, a configuração do editor principal [OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`, poderá ser configurada para definir o intervalo de pesquisa padrão para as configurações que não estão configuradas individualmente no CRXDE.

O intervalo de sondagem controla a frequência das solicitações ao Adobe Analytics para que os dados sejam obtidos e salvos em [SRP](/help/communities/working-with-srp.md).

Quando os dados podem ser categorizados como &quot;grandes dados&quot;, pesquisas mais frequentes podem colocar uma grande carga no site da comunidade.

A pesquisa padrão **Import range** é definida como 12 horas.

![importador de relatórios](assets/report-importer.png)

### Personalização de relatórios de componentes {#component-report-customization}

Atualmente, para personalizar as métricas para rastrear, os nós são criados no repositório que definem períodos de tempo para os quais gerar um relatório sobre essa métrica.

O tópico do fórum é atualmente o único exemplo dessa personalização:

* No editor principal, faça logon com privilégios administrativos.
* Navegue até [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Por exemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* No nó jcr:content da raiz do idioma (por exemplo, `/content/sites/engage/en/jcr:content),`navegue até o componente configurado para os relatórios do Analytics.
Por exemplo, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Observe os períodos de tempo criados:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Observe o nó `total`.

   * Modificar a propriedade **`interval`** substitui o intervalo do Importador de relatórios .
   * O valor é em segundos e é definido como 4 horas (14400 segundos).

![relatório de componentes](assets/component-report.png)

## Gerenciar dados do usuário no Analytics {#manage-user-data-in-analytics}

O Adobe Analytics fornece APIs que permitem acessar, exportar e excluir dados do usuário. Para obter mais informações, consulte [Enviar solicitações de acesso e exclusão](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

## Recursos {#resources}

* Adobe Experience Cloud: [Ajuda e referência do Analytics](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM: [Integração com Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics com provedores externos](/help/sites-administering/external-providers.md)
