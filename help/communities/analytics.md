---
title: Recursos da configuração Analytics para comunidades
seo-title: Recursos da configuração Analytics para comunidades
description: Configurar análises para comunidades
seo-description: Configurar análises para comunidades
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '2760'
ht-degree: 4%

---


# Recursos da configuração Analytics para comunidades {#analytics-configuration-for-communities-features}

## Visão geral {#overview}

O Adobe Analytics e o Adobe Experience Manager (AEM) são ambas soluções de Adobe Marketing Cloud.

O Adobe Analytics pode ser configurado para AEM Communities para que, à medida que um membro interage com os recursos das Comunidades compatíveis, eventos sejam enviados para o Adobe Analytics a partir do qual os relatórios são gerados.

Por exemplo, quando um membro de um site da comunidade de ativação visualização um recurso de vídeo atribuído a ele, o player de recursos enviará eventos para a Analytics, incluindo dados de pulsação de vídeo. No site da comunidade, os administradores podem ver vários relatórios relacionados à reprodução do vídeo.

Além disso, a análise é necessária para:

* No ambiente publish:

   * Relatórios nas [tendências da comunidade](/help/communities/trends.md)
   * Permitir que os visitantes do site classifiquem por &quot;mais visualizados&quot;, &quot;mais ativos&quot;, &quot;mais curtidos&quot;
   * Contagem de Visualizações em listas UGC

* No ambiente do autor:

   * Exibição de dados de participação no console [de gerenciamento de](/help/communities/members.md) membros (visualização, publicações, seguidores, curtidas)
   * Resumo de tendências, pulsação de vídeo e dispositivo de vídeo para ativar [relatórios de recursos](/help/communities/reports.md)

Os recursos das Comunidades suportadas incluem:

* [Recursos de ativação](/help/communities/resources.md)
* [Fórum](/help/communities/forum.md)
* [Perguntas e respostas](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Biblioteca de arquivos](/help/communities/file-library.md)
* [Calendário](/help/communities/calendar.md)

Esta seção da documentação descreve como conectar um conjunto de relatórios da Analytics com os recursos das Comunidades. As etapas básicas são:

1. [Replicar a chave](#replicate-the-crypto-key) de criptografia para garantir que a criptografia/descriptografia ocorra corretamente em todas as instâncias do AEM
1. Preparar um conjunto de [relatórios da Adobe Analytics](#adobe-analytics-report-suite-for-video-reporting)
1. Criar um serviço [e uma](#aem-analytics-cloud-service-configuration) estrutura de [nuvem do AEM Analytics](#aem-analytics-framework-configuration)

1. [Habilitar Analytics](#enable-analytics-for-a-community-site) para um site da comunidade
1. [**Verificar **](#verify-analytics-to-aem-variable-mapping)o mapeamento de variável do Analytics para o AEM
1. Identificar editor [principal](#primary-publisher)
1. [Publicar](#publish-community-site-and-analytics-cloud-service) o site da comunidade
1. Configurar a [importação de dados](#obtaining-reports-from-analytics) de relatório do Adobe Analytics para o site da comunidade

## Pré-requisitos {#prerequisites}

Para configurar os recursos do Analytics for Communities, é necessário trabalhar com seu representante de conta para configurar uma conta da Adobe Analytics e um conjunto de [relatórios](#adobe-analytics-report-suite-for-video-reporting). Uma vez estabelecida, devem estar disponíveis as seguintes informações:

* **Nome da Empresa**

   A empresa associada à conta do Adobe Analytics.

* **Nome de usuário**

   O nome de usuário de logon para o usuário autorizado a gerenciar a conta Analytics (deve incluir privilégios de Acesso ao Serviço da Web).

* **Senha**

   A senha de logon do usuário autorizado.

* **Centro de dados Analytics**

   O URL do centro de dados da Analytics para a conta.

* **Conjunto de relatórios**

   O nome do conjunto de relatórios da Analytics a ser usado.

## Adobe Analytics Report Suite para Relatórios de vídeo {#adobe-analytics-report-suite-for-video-reporting}

Usando o Adobe Marketing Cloud, os conjuntos de relatórios do Analytics [Report Suite Manager](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)podem ser configurados para que um site da comunidade seja habilitado para fornecer relatórios sobre os recursos das Comunidades.

Ao fazer logon na [Adobe Experience Cloud](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html) com o Nome da [Empresa e o Nome](/help/communities/analytics.md#prerequisites)do usuário, é possível configurar um conjunto de relatórios novo ou existente para que:

* [11 Variáveis](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) de conversão (eVars)

   * **`evar1`** por meio **`evar11`** ativado

   * Pode alterar a finalidade (renomear) das eVars existentes ou criar novas para usar nos recursos das Comunidades

* [7 Eventos](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html) bem-sucedidos (eventos)

   * **`event1`** por meio **`event7`** ativado

   * tipo **`Counter`**

      * not **`Counter (no subrelations)`**
   * Pode alterar a finalidade (renomear) dos eventos existentes ou criar novos para usar nos recursos das Comunidades


* [Gerenciamento de vídeo](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * Console de Relatórios de vídeo

      * Ativar `Video Core`
      * Selecione Salvar
   * Console de avaliação do Video Core

      * Selecionar `Use Solution Variables`
      * Selecione Salvar


Se estiver usando um **novo conjunto** de relatórios, esteja ciente de que um novo conjunto de relatórios pode ter apenas 4 e 6 variáveis de evento, enquanto 11 e 7 eventos de vars são necessários para Comunidades.

Se estiver usando um conjunto **de relatórios** existente, talvez seja necessário [modificar o mapeamento](#modifying-analytics-variable-mapping) de variável antes de ativar a estrutura do Analytics para um site da comunidade. Entre em contato com seu representante de conta para obter informações sobre quaisquer preocupações relacionadas às variáveis dedicadas às Comunidades.

>[!CAUTION]
>
>**Se estiver usando um conjunto de relatórios existente que já usa variáveis em**
>
>* **`evar1`** a **`evar11`**
   >
   >
* **`event1`** a **`event7`**
>
>
**Depois, antes de o site da comunidade ser publicado,** é importante restaurar o mapeamento preexistente movendo as variáveis AEM que foram mapeadas automaticamente para variáveis Analytics quando o Analytics foi habilitado para um site da comunidade.
>
>Para restaurar o mapeamento pré-existente e mover variáveis AEM para outras variáveis do Analytics, consulte a seção sobre [Modificação do mapeamento](#modifying-analytics-variable-mapping)de variáveis do Analytics.
>
>Se isso não for feito, poderá ocorrer perda irrecuperável de dados.

### Analytics Video Heartbeat {#video-heartbeat-analytics}

Quando o Video Heartbeat Analytics está licenciado, um `Marketing Cloud Org Id` é atribuído.

Para ativar o relatórios Video Heartbeat após [configurar o conjunto de relatórios da Analytics para o relatórios](#adobe-analytics-report-suite-for-video-reporting)de vídeo:

* Criar um serviço em nuvem da [Analytics](#aem-analytics-cloud-service-configuration)
* Habilitar o [Analytics para um site da comunidade](#enable-analytics-for-a-community-site)
* Associar o site `Marketing Cloud Org Id` ao site da comunidade

O `Marketing Cloud Org Id` pode ser inserido no momento da criação [do site da](/help/communities/sites-console.md#enablement) comunidade ou posteriormente, [modificando](/help/communities/sites-console.md#modifying-site-properties) as propriedades do site da comunidade. [](#aem-analytics-cloud-service-configuration)

![chlimage_1-264](assets/chlimage_1-264.png)

Quando o Video Heartbeat Analytics é ativado, o código JavaScript (JS) do player de vídeo instancia o código da biblioteca de pulsação de vídeo (também no JS), que lida com toda a lógica para enviar atualizações de status de vídeo aos servidores de rastreamento de vídeo da Analytics a cada 10 segundos (não configurável) e, eventualmente, envia um relatório cumulativo da sessão de vídeo aos principais servidores Analytics.

Se não estiver ativado, o código de pulsação de vídeo nunca será instanciado e somente o andamento do vídeo e o rastreamento de posição de retomada serão mantidos no SRP para o relatórios.

## Configuração do Cloud Service do AEM Analytics {#aem-analytics-cloud-service-configuration}

Para criar uma nova integração do Analytics, que integra o Adobe Analytics ao site da comunidade do AEM, use a interface padrão na instância do autor:

* Da navegação global: **[!UICONTROL Ferramentas > Implantação > Cloud Service]**
* Role para baixo até **[!UICONTROL Adobe Analytics]**
* Selecione **[!UICONTROL Configurar agora]** ou **[!UICONTROL Mostrar configurações]**

![chlimage_1-265](assets/chlimage_1-265.png)

### Criar caixa de diálogo de configuração {#create-configuration-dialog}

* Selecione o `[+]` ícone ao lado de **[!UICONTROL Configurações]** disponíveis para criar uma nova configuração

Na caixa de diálogo Criar configuração, os valores a serem inseridos identificam a configuração.

![chlimage_1-266](assets/chlimage_1-266.png)

* **Título**

   (Obrigatório) Um título de exibição para a configuração.
Por exemplo, insira a *Enablement Community Analytics*

* **Nome**

   (Opcional) Se não for especificado, o nome assumirá como padrão um nome de nó válido derivado do título.
For example, enter *communities*

* **Modelo**

   Selecionar `Adobe Analytics Configuration`

* Selecione **Criar**

   * Inicia a página de configuração e abre a caixa de diálogo `Analytics Settings`

### Caixa de diálogo Configurações do Analytics {#analytics-settings-dialog}

A criação inicial de uma nova configuração do Analytics resulta na exibição da configuração e em uma nova caixa de diálogo para a entrada das Configurações do Analytics. Essa caixa de diálogo exige as informações [de conta de](#prerequisites) pré-requisito obtidas do representante da conta.

![chlimage_1-267](assets/chlimage_1-267.png)

* **Empresa**

   A empresa associada à conta do Adobe Analytics.

* **Nome de usuário**

   O nome de usuário de logon do usuário autorizado a gerenciar a conta do Analytics.

* **Senha**

   A senha de logon do usuário autorizado.

* **Centro de dados**

   Selecione o centro de dados da Analytics que hospeda o conjunto de relatórios.

* **Não adicionar a tag de rastreamento à página**

   Deixe como padrão (desmarcado).

* **Usar AppMeasurement**

   Deixe como padrão (desmarcado).

* **Não realizar importações de impressões de página todas as noites (autor)**

   Deixe como padrão (desmarcado).

* **Não realizar importações de impressões de página todas as noites (publicar)**

   Deixe como padrão (desmarcado).

Para salvar as configurações:

* Selecione **Conectar ao Analytics**

   * Se não for bem-sucedido,

      * Verifique se as entradas não contêm espaços à esquerda.
      * Tente um data center diferente.
      * Entre em contato com seu representante de conta.

* Selecione **OK**.

   ![chlimage_1-268](assets/chlimage_1-268.png)

### Criar estrutura {#create-framework}

Após a configuração bem-sucedida da conexão básica com o Adobe Analytics, é necessário criar ou editar uma estrutura para o site da comunidade. A finalidade da estrutura é mapear as variáveis de recurso Comunidades (AEM) para variáveis do Analytics (conjunto de relatórios).

* Selecionar `[+]` ícone ao lado de **[!UICONTROL Frameworks]** disponíveis para criar uma nova estrutura

   ![chlimage_1-269](assets/chlimage_1-269.png)

* **Título**

   (Obrigatório) Um título de exibição para a estruturaPor exemplo, informe *Ativar a estrutura* da comunidade.

* **Nome**

   (Opcional) Se não for especificado, o nome assumirá como padrão um nome de nó válido derivado do título.
For example, enter *communities*.

* *Modelo*

   Selecionar `Adobe Analytics Framework`.

* Selecione **Criar**.

A criação do Analytics Framework abre a estrutura para configuração.

## Configuração do AEM Analytics Framework {#aem-analytics-framework-configuration}

A finalidade da estrutura é mapear variáveis AEM para variáveis Analytics (eVars e eventos). As variáveis Analytics disponíveis para mapeamento são [definidas no conjunto](#adobe-analytics-report-suite-for-video-reporting)de relatórios.

![chlimage_1-270](assets/chlimage_1-270.png)

### Selecionar conjunto de relatórios {#select-report-suite}

Selecione o conjunto de relatórios que foi configurado para o relatórios de vídeo.

Se um conjunto de relatórios ainda não foi criado ou não foi configurado corretamente, consulte a seção anterior:
[Adobe Analytics Report Suite para Relatórios de vídeo](#adobe-analytics-report-suite-for-video-reporting)

O Sidekick não é necessário e pode ser minimizado para que não obstrua o acesso às configurações dos Report Suites.

#### Caixa de diálogo Conjuntos de relatórios antes e depois de selecionar &#39;Adicionar item&#39; {#report-suites-dialog-before-and-after-selecting-add-item}

![chlimage_1-271](assets/chlimage_1-271.png)

1. Selecione **Adicionar item +**.

   Duas caixas suspensas são exibidas.

1. Choose a `Report suite.`

   Os conjuntos de relatórios associados à conta de Empresa estão disponíveis para seleção.

1. Selecione **Sim** na caixa de diálogo que é aberta:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Choose a `Run Mode`.

1. Selecione **Publicar**.

![chlimage_1-272](assets/chlimage_1-272.png)

O serviço e a estrutura da nuvem do Analytics estão concluídos. Os Mapeamentos serão definidos assim que um site da comunidade for criado com este serviço Analytics ativado.

## Habilitar Analytics para um site da comunidade {#enable-analytics-for-a-community-site}

### Ativar para Novo Site da Comunidade {#enable-for-new-community-site}

Para adicionar o serviço de nuvem da Analytics ao [criar um novo site](/help/communities/sites-console.md)da comunidade:

* Na etapa 3, na guia [ANALYTICS](/help/communities/sites-console.md#analytics):
   * Marque a caixa de seleção **Ativar Analytics** .
   * Selecione a estrutura na caixa suspensa.

* Como opção, retorne à configuração da estrutura do Analytics para ajustar os mapeamentos de variáveis.

### Habilitar para site da comunidade existente {#enable-for-existing-community-site}

Para adicionar o serviço de nuvem da Analytics a um site [da comunidade](/help/communities/sites-console.md#modifying-site-properties)existente:

* Navegue até o console **Comunidades > Sites** .
* Selecione o ícone Editar site do site da comunidade.
* Selecione as CONFIGURAÇÕES.
* Na seção Analytics:
   * Marque a caixa de seleção **Ativar Analytics** .
   * Escolha a estrutura na caixa suspensa.

* Como opção, retorne à configuração da estrutura do Analytics para ajustar os mapeamentos de variáveis.

### Ativar para sites personalizados {#enable-for-customized-sites}

Para que o rastreamento e a importação do Analytics funcionem corretamente para um site da comunidade, um elemento de página com os atributos `scf-js-site-title` class e href deve estar presente. Somente um elemento desse tipo deve existir na página, como ocorre em um script não modificado para um site da comunidade. `sitepage.hbs` O valor de `siteUrl` é extraído e enviado para a Adobe Analytics como o caminho *do* site.

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

Para um site **da comunidade** personalizado que sobrepõe o `sitepage.hbs` script, verifique se o elemento está presente. A `siteUrl` variável será definida quando renderizada no servidor antes de servir ao cliente.

Para um site **AEM** genérico que inclui componentes de Comunidades, mas não é criado com o assistente [de criação de](/help/communities/sites-console.md)site, é necessário adicionar o elemento. O valor do href deve ser o caminho para o site. Por exemplo, se o caminho do site for `/content/my/company/en`, use:

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

A configuração [OSGi do ambiente autor](/help/sites-deploying/configuring-osgi.md)`AEM Communities Analytics Component Configuration`fornece uma lista dos componentes que foram instrumentados para o Analytics. O mapeamento automático de variáveis é determinado pelos componentes listados.

Se forem criados novos componentes personalizados instrumentados para o Analytics, eles deverão ser adicionados a essa lista de componentes configurados.

### Configuração do componente {#component-configuration}

![chlimage_1-273](assets/chlimage_1-273.png)

>[!NOTE]
>
>Os componentes do journal são usados para implementar o recurso de blog.


### Variáveis mapeadas do Analytics para o AEM {#mapped-analytics-to-aem-variables}

Quando o site da comunidade for salvo com o Analytics ativado e a estrutura de configuração da nuvem selecionada, as variáveis do AEM serão mapeadas automaticamente para as eVars e eventos do Analytics começando com evar1 e evento1, respectivamente, e aumentando em 1.

Se estiver usando um conjunto de relatórios existente que mapeou qualquer uma das variáveis dentro de evar1 até evar11 e evento1 até evento7, será necessário [remapear as variáveis](#modifying-analytics-variable-mapping) do AEM e restaurar o mapeamento original.

Veja a seguir um exemplo de mapeamentos padrão após seguir o tutorial [de](/help/communities/getting-started-enablement.md)introdução:

![chlimage_1-274](assets/chlimage_1-274.png)

#### Mapa de eVars enviadas com cada evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Tipo de recurso<br /><br /> de ativação</strong></td>
   <td><strong>Título do site<br /></strong></td>
   <td><strong>Tipo de função<br /></strong></td>
   <td><strong>Título do grupo<br /></strong></td>
   <td><strong>Group<br /> Path</strong></td>
   <td><strong>Tipo de UGC<br /></strong></td>
   <td><strong>Título do UGC<br /></strong></td>
   <td><strong>Usuário<br /> (Membro)</strong></td>
   <td><strong>Caminho UGC<br /></strong></td>
   <td><strong>Caminho do site<br /></strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>Reprodução de recursos do evento1<br /></strong></td>
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
   <td><strong>evento2<br /> SCFView</strong></td>
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
   <td><strong>evento3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
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
   <td><strong>evento4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
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
   <td><strong>evento5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
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
   <td><strong>evento6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
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
   <td><strong>evento7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
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
 </tbody>
</table>

**Exemplos de valores de eVar:**

* *[Tipo](https://www.iana.org/assignments/media-types)*MIME: video/mp4
* *[título](/help/communities/sites-console.md#step13asitetemplate)*do site da comunidade: Comunidades Geometrixx
* *[nome](/help/communities/functions.md)*da função da comunidade: Fórum
* *[nome](/help/communities/creating-groups.md#creating-a-new-group)*do grupo da comunidade: Caminho
* *caminho para o conteúdo* do grupo da comunidade: `/content/sites/<site name>/en/groups/hiking`
* *[ResourceType](/help/communities/essentials.md)*do componente UGC:`social/forum/components/hbs/topic`
* *Título* do componente UGC: Tópicos de rastreamento
* *login (authorizedId)*: `aaron.mcdonald@mailinator.com`
* *Caminho SRP para UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
ou 
*caminho do componente a ser seguido*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *caminho para o conteúdo* do site da comunidade: `/content/sites/<site name>/en`

### Modificando o mapeamento de variáveis do Analytics {#modifying-analytics-variable-mapping}

O mapeamento de eVars e eventos Analytics para variáveis AEM é visível da configuração da estrutura depois que o Analytics é ativado para um site da comunidade.

Depois que o Analytics for ativado e antes que o site da comunidade seja publicado, o mapeamento poderá ser alterado na estrutura arrastando a evar ou o evento do Analytics desejado do painel esquerdo e soltando-o na linha relevante na tabela de mapeamento.

Para evitar mapeamentos de duplicado, remova a evar ou o evento do Analytics substituído da linha passando o mouse sobre ela e selecionando o &quot;X&quot; que aparece à direita do elemento de variável do Analytics.

Se as eVars e os eventos das Comunidades substituírem os mapeamentos que existiam no conjunto de relatórios, para evitar perda de dados, atribua as variáveis do AEM para os recursos das Comunidades a outras eVars ou eventos do Analytics e restaure os mapeamentos originais.

>[!CAUTION]
>
>É importante remapear antes que o site da comunidade seja [publicado](#publishing-the-community-site) com a Analytics ativada, caso contrário, há risco de perda de dados.

#### Exemplo Etapa 1: Arrastar a Analytics evar14 para a tabela de mapeamento {#example-step-dragging-analytics-evar-into-mapping-table}

![chlimage_1-275](assets/chlimage_1-275.png)

#### Exemplo Etapa 2: Selecionar &#39;x&#39; para remover evar11 substituído {#example-step-selecting-x-to-remove-replaced-evar}

![chlimage_1-276](assets/chlimage_1-276.png)

#### Exemplo Etapa 3: AEM var eventdata.siteId remapeado para Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![chlimage_1-277](assets/chlimage_1-277.png)

## Publicar o site da comunidade {#publishing-the-community-site}

### Verificar o mapeamento de variáveis Analytics para AEM {#verify-analytics-to-aem-variable-mapping}

É aconselhável verificar o mapeamento de variável antes de publicar o site da comunidade, que também publica o serviço e a estrutura de nuvem da Analytics.

Consulte as seções:

* [Variáveis mapeadas do Analytics para o AEM](#mapped-analytics-to-aem-variables)
* [Modificando o mapeamento de variáveis do Analytics](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Se estiver usando um conjunto de relatórios existente que já usa variáveis em**
>
>* **`evar1`** a **`evar11`**
   >
   >
* **`event1`** a **`event7`**
>
>
**Depois, antes de o site da comunidade ser publicado,** é importante restaurar o mapeamento preexistente e mover as variáveis AEM das Comunidades que foram automaticamente mapeadas (quando o Analytics foi ativado para o site da comunidade) para outras variáveis do Analytics. Esse novo mapeamento deve ser consistente em todos os componentes das Comunidades.
>
>Se isso não for feito, poderá ocorrer perda irrecuperável de dados.

### Editor principal {#primary-publisher}

Quando a implantação escolhida é um farm [de](/help/communities/topologies.md#tarmk-publish-farm)publicação, uma instância de publicação do AEM deve ser identificada como o editor principal para sondar o Adobe Analytics para que os dados do relatório sejam gravados no [SRP](/help/communities/working-with-srp.md).

Por padrão, a configuração do `AEM Communities Publisher Configuration` OSGi identifica sua instância de publicação como o editor principal, de modo que todas as instâncias de publicação em um farm de publicação se autoidentificariam como o principal.

Portanto, é necessário editar a configuração em todas as instâncias de publicação secundárias para desmarcar a caixa de seleção Editor **** primário.

Para obter instruções específicas, consulte a seção principal do editor de [Implantação de comunidades](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>É importante que o editor principal seja configurado para impedir a pesquisa de várias instâncias de publicação.

### Replicar a chave de criptografia {#replicate-the-crypto-key}

As credenciais do Adobe Analytics são criptografadas. Para facilitar a replicação ou a transmissão de credenciais de análise criptografadas entre o autor e os editores, todas as instâncias do AEM devem compartilhar a mesma chave de criptografia primária.

Para fazer isso, siga as instruções em [Replicar a chave](/help/communities/deploy-communities.md#replicate-the-crypto-key)de criptografia.

### Publicar site da comunidade e Cloud Service Analytics {#publish-community-site-and-analytics-cloud-service}

Depois que o serviço em nuvem da Analytics for ativado para um site da comunidade e, se necessário, o [mapeamento das variáveis do Analytics para o AEM for ajustado](#mapped-analytics-to-aem-variables), será necessário replicar a configuração para o ambiente de publicação [(re)publicando o site](/help/communities/sites-console.md#publishing-the-site)da comunidade.

## Obtenção de relatórios da Analytics {#obtaining-reports-from-analytics}

### Gerenciamento de relatórios {#report-management}

A configuração [OSGi do autor e do editor principal,](/help/sites-deploying/configuring-osgi.md)`AEM Communities Analytics Report Management`, é usada para query da Analytics.

No autor, os query são para relatórios em tempo real.

No editor principal, os query são usados para fornecer informações em preparação para a importação de dados analíticos do Importador de relatórios.

O padrão do intervalo de query é 10 segundos.

### Importador de relatórios {#report-importer}

Depois que um site da comunidade habilitado pela Analytics for publicado, a configuração [OSGi do editor principal,](/help/sites-deploying/configuring-osgi.md)`AEM Communities Analytics Report Importer`, poderá ser configurada para definir o intervalo de pesquisa padrão para as configurações que não estão configuradas individualmente no CRXDE.

O intervalo de sondagem controla a frequência de solicitações à Adobe Analytics para que os dados sejam obtidos e salvos no [SRP](/help/communities/working-with-srp.md).

Quando os dados podem ser classificados como &quot;grandes dados&quot;, pesquisas mais frequentes podem colocar uma grande carga no site da comunidade.

O intervalo **padrão de** importação de sondagem é definido como 12 horas.

![chlimage_1-278](assets/chlimage_1-278.png)

### Personalização do relatório do componente {#component-report-customization}

Atualmente, para personalizar as métricas a serem rastreadas, os nós são criados no repositório que define períodos de tempo para os quais gerar um relatório sobre essa métrica.

O tópico do fórum é atualmente o único exemplo dessa personalização:

* No editor principal, faça logon com privilégios administrativos.
* Navegue até [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Por exemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* No nó jcr:content da raiz do idioma (por exemplo, `/content/sites/engage/en/jcr:content),`navegue até o componente configurado para o relatórios Analytics).
Por exemplo, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Observe os períodos de tempo criados:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Observe o `total`nó.

   * Modificar a **`interval`** propriedade substitui o intervalo do Importador de relatórios.
   * O valor é em segundos e é definido como 4 horas (14400 segundos).

![chlimage_1-279](assets/chlimage_1-279.png)

## Gerenciar dados do usuário no Analytics {#manage-user-data-in-analytics}

A Adobe Analytics fornece APIs que permitem acessar, exportar e excluir dados do usuário. Para obter mais informações, consulte [Enviar acesso e excluir solicitações](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

## Recursos {#resources}

* Adobe Experience Cloud: [Ajuda e referência da Analytics](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM: [Integrating with Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics com provedores externos](/help/sites-administering/external-providers.md)
