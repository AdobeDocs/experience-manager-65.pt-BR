---
title: Conectar ao Adobe Analytics e Criar Frameworks
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: Saiba mais sobre como conectar AEM ao SiteCatalyst e criar estruturas.
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 6%

---

# Conectar ao Adobe Analytics e Criar Frameworks {#connecting-to-adobe-analytics-and-creating-frameworks}

Para rastrear dados da Web de suas páginas de AEM no Adobe Analytics, crie uma configuração dos Serviços Adobe Analytics Cloud e uma estrutura do Adobe Analytics:

* **Configuração do Adobe Analytics:** As informações sobre sua conta do Adobe Analytics. A configuração do Adobe Analytics permite que o AEM se conecte ao Adobe Analytics. Crie uma configuração do Adobe Analytics para cada conta usada.
* **Adobe Analytics Framework:** Um conjunto de mapeamentos entre as propriedades do conjunto de relatórios do Adobe Analytics e as variáveis CQ. Use uma estrutura para configurar como os dados do seu site preenchem os relatórios do Adobe Analytics. As Frameworks estão associadas a uma configuração do Adobe Analytics. Você pode criar várias estruturas para cada configuração.

Quando você associa uma página da Web a uma estrutura, a estrutura executa o rastreamento dessa página e dos descendentes dessa página. As exibições de página podem ser recuperadas do Adobe Analytics e exibidas no console Sites .

## Pré-requisitos {#prerequisites}

### Conta Adobe Analytics {#adobe-analytics-account}

Para rastrear AEM dados no Adobe Analytics, você deve ter uma conta Adobe Experience Cloud Adobe Analytics válida.

A conta do Adobe Analytics deve:

* Ter **Administrador** privilégios
* Ser atribuído ao **Acesso aos serviços da Web** grupo de usuários.

>[!CAUTION]
>
>Fornecimento **Administrador** privilégios (no Adobe Analytics) não são suficientes para permitir que um usuário se conecte de AEM ao Adobe Analytics. A conta também deve ter **Acesso aos serviços da Web** privilégios.

![chlimage_1-67](assets/chlimage_1-67.png)

Antes de continuar, verifique se suas credenciais permitem fazer logon na Adobe Analytics. Por meio de um dos seguintes procedimentos:

* [Logon no Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Logon no Adobe Analytics](https://sc.omniture.com/login/)

### Configuração de AEM para usar seus data centers da Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [data centers](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) coletar, processar e armazenar dados associados ao seu conjunto de relatórios do Adobe Analytics. Configure AEM para usar o data center que hospeda seu conjunto de relatórios do Adobe Analytics. O data center é mencionado em seu contrato. Entre em contato com um Administrador em sua organização para obter essas informações.

Se necessário, use o seguinte para ser roteado para o data center correto: `https://api.omniture.com/`.

Se sua organização exigir a coleta ou recuperação de dados de um data center específico, use o seguinte:

| Centro de dados | URL |
|---|---|
| Londres | `https://api3.omniture.com/` |
| Cingapura | `https://api4.omniture.com/` |
| Oregon | `https://api5.omniture.com/` |

Use o [Console da Web para configurar o pacote OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Cliente HTTP do Adobe AEM Analytics**. Adicione o **URL do data center** para o data center que hospeda um conjunto de relatórios para o qual suas páginas de AEM coletam dados.

![aa-07](assets/aa-07.png)

1. Abra o console da Web no navegador da Web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Para acessar o console, insira suas credenciais.

   >[!NOTE]
   >
   >Para descobrir se você tem acesso a esse console, entre em contato com o administrador do site.

1. Selecione o item de Configuração chamado **Cliente HTTP do Adobe AEM Analytics**.
1. Para adicionar a URL de um data center, pressione o botão + ao lado do **URLs de data center** e digite o URL na caixa.

1. Para remover um URL da lista, clique no botão - ao lado do URL.
1. Clique em Salvar.

## Configuração da conexão com o Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM.
>
>O [Plug-in do Activity Map fornecido pelo Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=pt-BR) deve ser usada.

## Configuração para o Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM.
>
>O [Plug-in do Activity Map fornecido pelo Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=pt-BR) deve ser usada.

## Criação de uma estrutura do Adobe Analytics {#creating-a-adobe-analytics-framework}

Para a ID do conjunto de relatórios (RSID) que você está usando, é possível controlar quais instâncias do servidor (autor, publicação ou ambas) contribuem com dados para o conjunto de relatórios:

* **Todos**: As informações do autor e da instância de publicação preenchem o Conjunto de relatórios.
* **Autor**: Somente as informações da instância do autor preenchem o Conjunto de relatórios.
* **Publicar**: Somente as informações da instância de publicação preenchem o Conjunto de relatórios.

>[!NOTE]
>
>Selecionar o tipo de instância do servidor não restringe chamadas para o Adobe Analytics, apenas controla quais chamadas incluem o RSID.
>
>Por exemplo, uma estrutura é configurada para usar a variável *diiweretail* conjunto de relatórios e autor é a instância do servidor selecionada. Quando as páginas são publicadas junto com a estrutura, as chamadas ainda são feitas ao Adobe Analytics, no entanto, essas chamadas não contêm o RSID. Somente as chamadas da instância do autor incluem o RSID.

1. Usando **Navegação**, selecione **Ferramentas**, **Cloud Services**, em seguida **Cloud Services herdados**.
1. Rolar para **Adobe Analytics** e selecione **Mostrar configurações**.
1. Clique no botão **[+]** link ao lado da configuração do Adobe Analytics.

1. No **Criar estrutura** caixa de diálogo:

   * Especifica um **Título**.
   * Opcionalmente, é possível especificar a variável **Nome**, para o nó que armazena os detalhes da estrutura no repositório.
   * Selecionar **Adobe Analytics Framework**

   E clique em **Criar**.

   A estrutura é aberta para edição.

1. No **Conjuntos de relatórios** seção do pod lateral (lado direito do painel principal), clique em **Adicionar item**. Em seguida, use o menu suspenso para selecionar a ID do conjunto de relatórios (por exemplo, `geometrixxauth`) com a qual o quadro interage.

   >[!NOTE]
   >
   >O localizador de conteúdo à esquerda é preenchido com variáveis do Adobe Analytics (Variáveis de SiteCatalyst) ao selecionar uma ID de conjunto de relatórios.

1. Para selecionar as instâncias do servidor para as quais deseja enviar informações para o Conjunto de relatórios, use o **Modo de execução** menu suspenso (ao lado da ID do conjunto de relatórios).

   ![aa-framework-01](assets/aa-framework-01.png)

1. Para disponibilizar a estrutura na instância de publicação do site, no **Página** guia do sidekick, clique em **Ativar Estrutura.**

### Definição das configurações de servidor para Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

O sistema de estrutura permite alterar as configurações do servidor em cada estrutura do Adobe Analytics.

>[!CAUTION]
>
>Essas configurações determinam onde seus dados são enviados e como, portanto, é fundamental que você *não altere essas configurações* e permitir que seu representante da Adobe Analytics configure-a.

Comece abrindo o painel. Pressione a seta para baixo ao lado de **Servidores**:

![server_001](assets/server_001.png)

* **Servidor de controle**

   * contém o URL usado para enviar chamadas do Adobe Analytics

      * `cname` - assume como padrão a conta do Adobe Analytics *Nome da empresa*
      * `d1` - corresponde ao centro de dados para o qual a informação é enviada (ou `d1`, `d2`ou `d3`)
      * `sc.omtrdc.net` - nome de domínio

* **Servidor de rastreamento protegido**

   * Tem os mesmos segmentos do servidor de rastreamento
   * Usado para enviar dados de páginas seguras (`https://`)

* **Namespace do visitante**

   * O namespace determina a primeira parte do URL de rastreamento.
   * Por exemplo, alterar o namespace para **CNAME** faz com que as chamadas feitas para o Adobe Analytics pareçam **CNAME.d1.omtrdc.net** em vez do padrão.

## Associar uma página a uma estrutura do Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Quando uma página é associada a uma estrutura do Adobe Analytics, ela envia dados para o Adobe Analytics quando a página é carregada. As variáveis que a página preenche são mapeadas e recuperadas das variáveis do Adobe Analytics na estrutura. Por exemplo, as exibições de página são recuperadas do Adobe Analytics.

Os descendentes da página herdam a associação com a estrutura. Por exemplo, ao associar a página raiz do site a uma estrutura, todas as páginas do site são associadas à estrutura.

1. No **Sites** selecione a página que deseja configurar com o rastreamento.
1. Abra o **[Propriedades da página](/help/sites-authoring/editing-page-properties.md)**, diretamente do console ou do editor de páginas.
1. Abra a guia ** Cloud Services**.

1. Use o **Adicionar configuração** menu suspenso a ser selecionado **Adobe Analytics** nas opções disponíveis. Se a herança estiver em vigor, desative-a antes que o seletor fique disponível.

1. O seletor suspenso para **Adobe Analytics** é anexada às opções disponíveis. Selecione a configuração de estrutura necessária.

1. Selecionar **Salvar e fechar**.
1. Para ativar a página e quaisquer configurações/arquivos conectados, **[Publicar](/help/sites-authoring/publishing-pages.md)** na página.
1. A etapa final é visitar a página na instância de publicação e pesquisar por uma palavra-chave (por exemplo, beringela) usando a **Pesquisar** componente.
1. Você pode verificar as chamadas feitas para o Adobe Analytics usando uma ferramenta apropriada; por exemplo, [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. Usando o exemplo fornecido, a chamada deve conter o valor inserido (ou seja, beringela) no eVar 7 e a lista de eventos deve conter event3.

### Exibições da página {#page-views}

Quando uma página é associada a uma estrutura do Adobe Analytics, o número de exibições de página pode ser exibido na exibição de Lista do console Sites.

Consulte [Visualizar dados de análise da página](/help/sites-authoring/page-analytics-using.md) para obter mais detalhes.

### Configuração do intervalo de importação {#configuring-the-import-interval}

Configure a instância apropriada do **Configuração de Pesquisa Gerenciada do Adobe AEM** serviço:

* **Intervalo de Pesquisa**: O intervalo, em segundos, no qual o serviço recupera dados de exibição de página do Adobe Analytics.
O intervalo padrão é de 43200000 ms (12 horas).

* **Habilitar**: Ative ou desative o serviço. Por padrão, o serviço é ativado.

Para configurar esse serviço OSGi, você pode usar o [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou [nó osgiConfig no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (o PID de serviço é `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Editar configurações e/ou Frameworks do Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Como ao criar uma configuração ou estrutura do Adobe Analytics, navegue até o (herdado) **Cloud Services** tela. Selecionar **Mostrar configurações** e clique no link para a configuração específica que deseja atualizar.

Ao editar uma configuração do Adobe Analytics, pressione **Editar** quando na própria página de configuração abrir o **Editar componente** caixa de diálogo.

## Exclusão de Frameworks Adobe Analytics {#deleting-adobe-analytics-frameworks}

Para excluir uma estrutura do Adobe Analytics, primeiro [abrir para edição](#editing-adobe-analytics-configurations-and-or-frameworks).

Em seguida, selecione **Excluir estrutura** do **Página** guia do sidekick.
