---
title: Conexão com o Adobe Analytics e criação de estruturas
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: Saiba mais sobre como conectar o AEM ao SiteCatalyst e criar estruturas.
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: bbd18486a77d7b46454aacff23147b38860bd895
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 7%

---

# Conexão com o Adobe Analytics e criação de estruturas {#connecting-to-adobe-analytics-and-creating-frameworks}

Para rastrear dados da Web de suas páginas AEM no Adobe Analytics, crie uma configuração do Adobe Analytics Cloud Services e uma estrutura do Adobe Analytics:

* **Configuração do Adobe Analytics:** As informações sobre sua conta da Adobe Analytics. A configuração do Adobe Analytics permite que o AEM se conecte ao Adobe Analytics. Crie uma configuração do Adobe Analytics para cada conta que você usar.
* **Estrutura do Adobe Analytics:** Um conjunto de mapeamentos entre as propriedades do conjunto de relatórios do Adobe Analytics e as variáveis do CQ. Use uma estrutura para configurar como os dados do site preenchem os relatórios do Adobe Analytics. As estruturas são associadas a uma configuração do Adobe Analytics. É possível criar várias estruturas para cada configuração.

Quando você associa uma página da Web a uma estrutura, a estrutura executa o rastreamento para essa página e seus descendentes. As exibições de página podem ser recuperadas do Adobe Analytics e exibidas no console Sites.

## Pré-requisitos {#prerequisites}

### Conta do Adobe Analytics {#adobe-analytics-account}

Para rastrear dados do AEM no Adobe Analytics, é necessário ter uma conta válida do Adobe Experience Cloud Adobe Analytics.

A conta do Adobe Analytics deve:

* Têm **Administrador** privilégios
* Ser atribuído à **Acesso aos serviços da Web** grupo de usuários.

>[!CAUTION]
>
>Fornecendo **Administrador** privilégios (no Adobe Analytics) não são suficientes para permitir que um usuário se conecte do AEM ao Adobe Analytics. A conta também deve ter **Acesso aos serviços da Web** privilégios.

![chlimage_1-67](assets/chlimage_1-67.png)

Antes de continuar, verifique se suas credenciais permitem fazer logon no Adobe Analytics. Por uma das seguintes formas:

* [Logon no Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Logon no Adobe Analytics](https://sc.omniture.com/login/)

### Configuração do AEM para usar seus data centers da Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [data centers](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) colete, processe e armazene dados associados ao seu conjunto de relatórios do Adobe Analytics. Configure o AEM para usar o data center que hospeda o conjunto de relatórios do Adobe Analytics. O data center é mencionado em seu contrato. Entre em contato com um administrador em sua organização para obter essas informações.

Se necessário, use o seguinte para ser direcionado ao data center correto: `https://api.omniture.com/`.

Se sua empresa exigir a coleta ou a recuperação de dados de um data center específico, use o seguinte:

| Centro de dados | URL |
|---|---|
| Londres | `https://api3.omniture.com/` |
| Cingapura | `https://api4.omniture.com/` |
| Oregon | `https://api5.omniture.com/` |

Use o [Console da Web para configurar o pacote OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Cliente HTTP do Adobe AEM Analytics**. Adicione o **URL do centro de dados** para o data center que hospeda um conjunto de relatórios para o qual suas páginas AEM coletam dados.

![aa-07](assets/aa-07.png)

1. Abra o console Web no navegador da Web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Para acessar o console, digite suas credenciais.

   >[!NOTE]
   >
   >Para saber se você tem acesso a esse console, entre em contato com o administrador do site.

1. Selecione o item de configuração chamado **Cliente HTTP do Adobe AEM Analytics**.
1. Para adicionar o URL de um data center, pressione o botão + ao lado da guia **URLs do data center** e digite o URL na caixa.

1. Para remover um URL da lista, clique no botão - ao lado do URL.
1. Clique em Salvar.

## Configuração da conexão com o Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM.
>
>A variável [Plug-in do ActivityMap fornecido pela Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=pt-BR) deve ser usada.

## Configuração do para o Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM.
>
>A variável [Plug-in do ActivityMap fornecido pela Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=pt-BR) deve ser usada.

## Criação de uma estrutura do Adobe Analytics {#creating-a-adobe-analytics-framework}

Para a ID do conjunto de relatórios (RSID) que você está usando, é possível controlar quais instâncias do servidor (autor, publicação ou ambas) contribuem com dados para o conjunto de relatórios:

* **Todos**: informações do autor e da instância de publicação preenchem o Conjunto de relatórios.
* **Autor**: somente as informações da instância do autor preenchem o Conjunto de relatórios.
* **Publish**: somente as informações da instância de publicação preenchem o Conjunto de relatórios.

>[!NOTE]
>
>A seleção do tipo de instância do servidor não restringe chamadas para o Adobe Analytics, apenas controla quais chamadas incluem o RSID.
>
>Por exemplo, uma estrutura é configurada para usar a variável *diiweretail* o conjunto de relatórios e o autor são a instância de servidor selecionada. Quando as páginas são publicadas junto com a estrutura, as chamadas ainda são feitas para o Adobe Analytics, no entanto, essas chamadas não contêm a RSID. Somente as chamadas da instância do autor incluem a RSID.

1. Usar **Navegação**, selecione **Ferramentas**, **Cloud Service**, depois **Cloud Service herdados**.
1. Navegue até **Adobe Analytics** e selecione **Exibir configurações**.
1. Clique em **[+]** ao lado da configuração do Adobe Analytics.

1. No **Criar estrutura** diálogo:

   * Especifica um **Título**.
   * Opcionalmente, é possível especificar a variável **Nome**, para o nó que armazena os detalhes da estrutura no repositório.
   * Selecionar **Estrutura do Adobe Analytics**

   E clique em **Criar**.

   A estrutura é aberta para edição.

1. No **Conjuntos de relatórios** (lado direito do painel principal), clique em **Adicionar item**. Em seguida, use o menu suspenso para selecionar a ID do conjunto de relatórios (por exemplo, `geometrixxauth`) com o qual a estrutura interage.

   >[!NOTE]
   >
   >O localizador de conteúdo à esquerda é preenchido com variáveis do Adobe Analytics (Variáveis do SiteCatalyst) ao selecionar uma ID de conjunto de relatórios.

1. Para selecionar as instâncias do servidor para as quais deseja enviar informações para o Conjunto de relatórios, use o **Modo de execução** (ao lado da ID do conjunto de relatórios).

   ![aa-framework-01](assets/aa-framework-01.png)

1. Para disponibilizar a estrutura na instância de publicação do site, no **Página** do sidekick, clique em **Ativar Framework.**

### Definição das configurações de servidor para o Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

O sistema de estrutura permite alterar as configurações do servidor em cada estrutura do Adobe Analytics.

>[!CAUTION]
>
>Essas configurações determinam para onde seus dados são enviados e como, portanto, é fundamental que você *não alterar estas configurações* e deixe que seu representante da Adobe Analytics o configure.

Comece abrindo o painel. Pressione a seta para baixo ao lado de **Servidores**:

![server_001](assets/server_001.png)

* **Servidor de controle**

   * contém o URL usado para enviar chamadas do Adobe Analytics

      * `cname` - o padrão é a conta do Adobe Analytics *Nome da empresa*
      * `d1` - corresponde ao data center para o qual as informações são enviadas (seja `d1`, `d2`ou `d3`)
      * `sc.omtrdc.net` - nome do domínio

* **Servidor de rastreamento protegido**

   * Tem os mesmos segmentos que o servidor de rastreamento
   * Usado para enviar dados de páginas seguras (`https://`)

* **Namespace do visitante**

   * O namespace determina a primeira parte do URL de rastreamento.
   * Por exemplo, alterar o namespace para **CNAME** faz com que as chamadas feitas para o Adobe Analytics pareçam **CNAME.d1.omtrdc.net** em vez do padrão.

## Associar uma página a uma estrutura do Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Quando uma página é associada a uma estrutura do Adobe Analytics, a página envia dados para o Adobe Analytics quando a página é carregada. As variáveis que a página preenche são mapeadas e recuperadas das variáveis do Adobe Analytics na estrutura. Por exemplo, as exibições de página são recuperadas do Adobe Analytics.

Os descendentes da página herdam a associação com a estrutura. Por exemplo, ao associar a página raiz do site a uma estrutura, todas as páginas do site são associadas à estrutura.

1. No **Sites** selecione a página que deseja configurar com o rastreamento.
1. Abra o **[Propriedades da página](/help/sites-authoring/editing-page-properties.md)**, diretamente do console ou do editor de páginas.
1. Abra a guia ** Cloud Service**.

1. Use o **Adicionar configuração** para selecionar **Adobe Analytics** nas opções disponíveis. Se a herança for colocada, desative-a antes que o seletor fique disponível.

1. O seletor suspenso de **Adobe Analytics** está anexado às opções disponíveis. Selecione a configuração de estrutura necessária.

1. Selecionar **Salvar e fechar**.
1. Para ativar a página e quaisquer configurações/arquivos conectados, **[Publish](/help/sites-authoring/publishing-pages.md)** a página.
1. A etapa final é visitar a página na instância de publicação e pesquisar uma palavra-chave (por exemplo, berinjela) usando o **Pesquisar** componente.
1. Você pode verificar as chamadas feitas ao Adobe Analytics usando uma ferramenta apropriada; por exemplo, [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. Usando o exemplo fornecido, a chamada deve conter o valor inserido (ou seja, berinjela) em eVar7 e a lista de eventos deve conter event3.

### Visualizações de página {#page-views}

Quando uma página é associada a uma estrutura do Adobe Analytics, o número de exibições de página pode ser mostrado na exibição em Lista do console Sites.

Consulte [Visualização de dados de análise de página](/help/sites-authoring/page-analytics-using.md) para obter mais detalhes.

### Configuração do intervalo de importação {#configuring-the-import-interval}

Configure a instância apropriada do **Importador de Sling de relatório do Adobe AEM Analytics** serviço:

* **Tentativas de busca**: Número de tentativas de buscar um relatório em fila.
O padrão é `6`.

* **Atraso de busca**: o número de milissegundos entre tentativas de buscar um relatório na fila.
O padrão é `10000`. Como está em milissegundos, corresponde a 10 segundos.

* **Frequência de busca**: A `cron` para determinar a frequência de busca do Relatório do Analytics.
O padrão é `0 0 0/12 * * ?`; isso corresponde a 12 buscas a cada hora.

Para configurar esse serviço OSGi, você pode usar o [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou um [Nó osgiConfig no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (o serviço PID é `com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporterScheduler`).

## Editar configurações e/ou estruturas do Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Como ocorre ao criar uma configuração ou estrutura do Adobe Analytics, navegue até o (herdado) **Cloud Service** tela. Selecionar **Exibir configurações**, em seguida, clique no link para a configuração específica que deseja atualizar.

Ao editar uma configuração do Adobe Analytics, pressione **Editar** quando estiver na própria página de configuração para abrir a variável **Editar componente** diálogo.

## Exclusão de estruturas Adobe Analytics {#deleting-adobe-analytics-frameworks}

Para excluir uma estrutura Adobe Analytics, primeiro [abra-o para edição](#editing-adobe-analytics-configurations-and-or-frameworks).

Em seguida, selecione **Excluir estrutura** do **Página** guia do sidekick.
