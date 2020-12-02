---
title: Integração com o Gerenciamento dinâmico de tags do Adobe
seo-title: Integração com o Gerenciamento dinâmico de tags do Adobe
description: Saiba mais sobre a integração com o Gerenciamento dinâmico de tags do Adobe.
seo-description: Saiba mais sobre a integração com o Gerenciamento dinâmico de tags do Adobe.
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '2222'
ht-degree: 1%

---


# Integração com o Gerenciamento dinâmico de tags do Adobe {#integrating-with-adobe-dynamic-tag-management}

Integre [Gerenciamento dinâmico de tags do Adobe](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) ao AEM para que você possa usar as propriedades da Web do Gerenciamento dinâmico de tags para rastrear AEM sites. O Gerenciamento dinâmico de tags permite que os profissionais de marketing gerenciem tags para coletar dados e distribuam dados pelos sistemas de marketing digital. Por exemplo, use o Gerenciamento dinâmico de tags para coletar dados de uso para o seu site AEM e distribuir os dados para análise no Adobe Analytics ou Adobe Target.

Antes de se integrar, é necessário criar a propriedade da Web [Gerenciamento dinâmico de tags](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) que rastreia o domínio do site AEM. As [opções de hospedagem](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) da propriedade da Web devem ser configuradas para que você possa configurar AEM para acessar as bibliotecas do Gerenciamento dinâmico de tags.

Depois de configurar a integração, as alterações nas ferramentas e regras de implantação do Gerenciamento dinâmico de tags não exigem que você altere a configuração do Gerenciamento dinâmico de tags no AEM. As alterações estão automaticamente disponíveis para AEM.

>[!NOTE]
>
>Se você estiver usando o DTM com uma configuração de proxy personalizada, é necessário configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* O 3.x está configurado com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* O 4.x está configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Opções de implantação {#deployment-options}

As seguintes opções de implantação afetam a configuração da integração com o Gerenciamento dinâmico de tags.

### Hospedagem do Gerenciamento dinâmico de tags {#dynamic-tag-management-hosting}

AEM suporta o Gerenciamento dinâmico de tags hospedado na nuvem ou hospedado em AEM.

* Hospedado na nuvem: As bibliotecas de javascript do Gerenciamento dinâmico de tags são armazenadas na nuvem e suas páginas AEM fazem referência a elas diretamente.
* AEM hospedado: O Gerenciamento dinâmico de tags gera bibliotecas de javascript. AEM usa um modelo de fluxo de trabalho para obter e instalar as bibliotecas.

O tipo de hospedagem que sua implementação usa determina algumas das tarefas de configuração e implementação que você executa. Para obter informações sobre as opções de hospedagem, consulte [Hospedagem - guia incorporada](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) na Ajuda do Gerenciamento dinâmico de tags.

### Biblioteca de preparo e produção {#staging-and-production-library}

Decida se a instância do autor AEM usa o código de produção ou de preparo do Gerenciamento dinâmico de tags.

Normalmente, sua instância do autor usa as bibliotecas de preparo do Gerenciamento dinâmico de tags e a instância de produção usa as bibliotecas de produção. Esse cenário permite que você use a instância do autor para testar configurações não aprovadas do Gerenciamento dinâmico de tags.

Se desejar, a instância do autor poderá usar as bibliotecas de produção. Estão disponíveis plug-ins de navegador da Web que permitem alternar entre o uso de bibliotecas de preparo para fins de teste quando as bibliotecas são hospedadas na nuvem.

### Usando o gancho de implantação do Gerenciamento dinâmico de tags {#using-the-dynamic-tag-management-deployment-hook}

Quando AEM hospeda as bibliotecas do Gerenciamento dinâmico de tags, você pode usar o serviço de gancho de implantação do Gerenciamento dinâmico de tags para enviar automaticamente as atualizações da biblioteca para AEM. As atualizações da biblioteca são enviadas quando as alterações são feitas nas bibliotecas, como quando as propriedades da Web do Gerenciamento dinâmico de tags são editadas.

Para usar o gancho de implantação, o Gerenciamento dinâmico de tags deve ser capaz de se conectar à instância AEM que hospeda as bibliotecas. Você deve [habilitar o acesso a AEM](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) para os servidores do Gerenciamento dinâmico de tags.

Em algumas circunstâncias, AEM pode ser inacessível, como quando AEM está por trás de um firewall. Nesses casos, você pode usar a opção importador de pesquisa AEM para recuperar periodicamente as bibliotecas. Uma expressão de trabalho cron determina o agendamento para downloads da biblioteca.

## Habilitando o acesso ao serviço de gancho de implantação {#enabling-access-for-the-deployment-hook-service}

Ative o serviço de gancho de implantação do Gerenciamento dinâmico de tags para acessar AEM para que o serviço possa atualizar as bibliotecas hospedadas AEM. Especifique o endereço IP dos servidores do Gerenciamento dinâmico de tags que atualizam as bibliotecas de preparo e produção, conforme necessário:

* Estágios: `107.21.99.31`
* Produção: `23.23.225.112` e `204.236.240.48`

Execute a configuração usando o [Web Console](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou um nó [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* No Console da Web, use o item Configuração de gancho de implantação do DTM Adobe na página Configuração.
* Para uma configuração OSGi, o PID do serviço é `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`.

A tabela a seguir descreve as propriedades a serem configuradas.

| propriedade Console da Web | propriedade OSGi | Descrição |
|---|---|---|
| Lista técnica de IP do DTM de armazenamento temporário | `dtm.staging.ip.whitelist` | O endereço IP do servidor do Gerenciamento dinâmico de tags que atualiza as bibliotecas de preparo. |
| Lista técnica de IP do DTM de produção | `dtm.production.ip.whitelist` | O endereço IP do servidor do Gerenciamento dinâmico de tags que atualiza as bibliotecas de produção. |

## Criando a Configuração do Gerenciamento dinâmico de tags {#creating-the-dynamic-tag-management-configuration}

Crie uma configuração em nuvem para que a instância AEM possa ser autenticada com o Gerenciamento dinâmico de tags e interagir com sua propriedade da Web.

>[!NOTE]
>
>Evite a inclusão de dois códigos de rastreamento do Adobe Analytics em suas páginas quando sua propriedade da Web do DTM incluir a ferramenta Adobe Analytics e você também estiver usando [Content Insight](/help/sites-authoring/content-insights.md). Em sua [configuração de nuvem do Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics), selecione a opção Não incluir código de rastreamento.

### Configurações gerais {#general-settings}

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Token de API</td>
   <td>O valor da propriedade Token da API da sua conta de usuário do Gerenciamento dinâmico de tags. AEM usa essa propriedade para autenticação com o Gerenciamento dinâmico de tags.</td>
  </tr>
  <tr>
   <td>Empresa</td>
   <td>A empresa à qual sua ID de login está associada.</td>
  </tr>
  <tr>
   <td>Propriedade</td>
   <td>O nome da propriedade da Web que você criou para gerenciar as tags do site AEM.</td>
  </tr>
  <tr>
   <td>Incluir código de produção em Autor</td>
   <td><p>Selecione essa opção para fazer com que as instâncias de autor e publicação do AEM usem a versão de produção das bibliotecas do Gerenciamento dinâmico de tags. </p> <p>Quando essa opção não está selecionada, as Configurações de armazenamento temporário se aplicam à instância do autor e as Configurações de produção se aplicam à instância de publicação.</p> </td>
  </tr>
 </tbody>
</table>

### Propriedades de hospedagem própria - armazenamento temporário e produção {#self-hosting-properties-staging-and-production}

As seguintes propriedades da configuração do Gerenciamento dinâmico de tags permitem AEM hospedagem das bibliotecas do Gerenciamento dinâmico de tags. As propriedades permitem que AEM baixe e instale as bibliotecas. Como opção, você pode atualizar automaticamente as bibliotecas para garantir que elas reflitam quaisquer alterações feitas no aplicativo de gerenciamento dinâmico de tags.

Algumas propriedades usam valores obtidos na seção Download da biblioteca da guia Incorporar para sua propriedade da Web Gerenciamento dinâmico de tags. Para obter informações, consulte [Download da biblioteca](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) na Ajuda do Gerenciamento dinâmico de tags.

>[!NOTE]
>
>Quando você estiver hospedando o pacote Gerenciamento dinâmico de tags no AEM, o Download da biblioteca deverá ser ativado no Gerenciamento dinâmico de tags antes de criar a configuração. Além disso, o Akamai deve estar habilitado porque o Akamai fornece as bibliotecas para download.

Ao hospedar as bibliotecas do Gerenciamento dinâmico de tags no AEM, o AEM configura automaticamente algumas propriedades da propriedade da Web de acordo com sua configuração. Consulte as descrições na tabela a seguir.

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Usar hospedagem própria</td>
   <td>Selecione quando estiver hospedando o arquivo da biblioteca do Gerenciamento dinâmico de tags no AEM. Selecionar essa opção faz com que as outras propriedades desta tabela sejam exibidas.</td>
  </tr>
  <tr>
   <td>URL do pacote de DTM</td>
   <td>O URL a ser usado para baixar a biblioteca do Gerenciamento dinâmico de tags. Obtenha esse valor na seção Download de URLs da página Download da biblioteca do Gerenciamento dinâmico de tags. Por motivos de segurança, esse valor deve ser configurado manualmente.</td>
  </tr>
  <tr>
   <td>Download do fluxo de trabalho</td>
   <td><p>O modelo de fluxo de trabalho a ser usado para baixar e instalar a biblioteca do Gerenciamento dinâmico de tags. O modelo padrão é Download padrão do pacote do DTM. Use esse modelo a menos que você tenha criado um modelo personalizado.</p> <p>Observe que o fluxo de trabalho de download padrão ativa automaticamente as bibliotecas quando elas são baixadas.</p> </td>
  </tr>
  <tr>
   <td>Dica de domínio</td>
   <td><p>(Opcional) O domínio do servidor AEM que está hospedando a biblioteca do Gerenciamento dinâmico de tags. Especifique um valor para substituir o domínio padrão configurado para o serviço <a href="/help/sites-developing/externalizer.md">Externalizador de links do Day CQ</a>.</p> <p>Quando conectado ao Gerenciamento dinâmico de tags, o AEM usa esse valor para configurar o Caminho HTTP de preparo ou o Caminho HTTP de produção das propriedades Download da biblioteca para a propriedade da Web Gerenciamento dinâmico de tags.</p> </td>
  </tr>
  <tr>
   <td>Dica do domínio segura</td>
   <td><p>(Opcional) O domínio do servidor AEM que está hospedando a biblioteca do Gerenciamento dinâmico de tags em HTTPS. Especifique um valor para substituir o domínio padrão configurado para o serviço <a href="/help/sites-developing/externalizer.md">Externalizador de links do Day CQ</a>.</p> <p>Quando conectado ao Gerenciamento dinâmico de tags, o AEM usa esse valor para configurar o Caminho HTTPS de preparo ou o Caminho HTTPS de produção das propriedades Download da biblioteca para a propriedade da Web Gerenciamento dinâmico de tags.</p> </td>
  </tr>
  <tr>
   <td>Segredo compartilhado</td>
   <td><p>(Opcional) O segredo compartilhado a ser usado para descriptografar o download. Obtenha esse valor do campo Segredo compartilhado da página Download da biblioteca do Gerenciamento dinâmico de tags.</p> <p><strong>Observação: </strong> você deve ter as bibliotecas  <a href="https://www.openssl.org/docs/apps/openssl.html"></a> OpenSSL instaladas no computador onde o AEM está instalado para que AEM possa descriptografar as bibliotecas baixadas.</p> </td>
  </tr>
  <tr>
   <td>Ativar o importador de pesquisa</td>
   <td><p>(Opcional) Selecione para baixar e instalar periodicamente a biblioteca do Gerenciamento dinâmico de tags para garantir que você esteja usando uma versão atualizada. Quando selecionado, o Gerenciamento dinâmico de tags não envia solicitações POST HTTP para o URL de gancho de implantação.</p> <p>AEM configura automaticamente a propriedade Implantar URL do gancho das propriedades Download da biblioteca para a propriedade da Web Gerenciamento dinâmico de tags. Quando selecionada, a propriedade é configurada sem valor. Quando não selecionada, a propriedade é configurada com o URL da configuração do Gerenciamento dinâmico de tags.</p> <p>Ative o importador de pesquisa quando o gancho de implantação do Gerenciamento dinâmico de tags não puder se conectar a AEM, por exemplo, quando AEM estiver atrás de um firewall.</p> </td>
  </tr>
  <tr>
   <td>Expressão de programação</td>
   <td>(Aparece e é necessário quando a opção Ativar Importador de Pesquisa está selecionada.) Uma expressão cron que controla quando as bibliotecas do Gerenciamento dinâmico de tags são baixadas.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### Propriedades de hospedagem na nuvem - armazenamento temporário e produção {#cloud-hosting-properties-staging-and-production}

As seguintes propriedades são configuradas para a configuração do Gerenciamento dinâmico de tags quando a Configuração dinâmica de tags é hospedada na nuvem.

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Usar hospedagem própria</td>
   <td>Desmarque essa opção quando o arquivo da biblioteca do Gerenciamento dinâmico de tags estiver hospedado na nuvem.</td>
  </tr>
  <tr>
   <td>Código do cabeçalho</td>
   <td><p>O código do cabeçalho para armazenamento temporário obtido do Gerenciamento dinâmico de tags para seu host. Esse valor é preenchido automaticamente quando você se conecta ao Gerenciamento dinâmico de tags.</p> <p> Para ver o código no Gerenciamento dinâmico de tags, clique na guia Incorporar e clique no nome do host. Expanda a seção Código do cabeçalho e clique em Copiar código incorporado do código incorporado de preparo ou na área Código incorporado de produção, conforme necessário.</p> </td>
  </tr>
  <tr>
   <td>Código de rodapé</td>
   <td><p>O código do rodapé para armazenamento temporário obtido do Gerenciamento dinâmico de tags para seu host. Esse valor é preenchido automaticamente quando você se conecta ao Gerenciamento dinâmico de tags.</p> <p>Para ver o código no Gerenciamento dinâmico de tags, clique na guia Incorporar e clique no nome do host. Expanda a seção Código do rodapé e clique na área Copiar código incorporado do código incorporado de preparo ou Código incorporado de produção, conforme necessário.</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

O procedimento a seguir usa a interface otimizada ao toque para configurar a integração com o Gerenciamento dinâmico de tags.

1. No trilho, clique em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na área Gerenciamento dinâmico de tags, um dos links a seguir é exibido para a adição de uma configuração:

   * Clique em Configurar agora se esta for a primeira configuração que você está adicionando.
   * Clique em Mostrar configurações e, em seguida, clique no link + ao lado de Configurações disponíveis se uma ou mais configurações tiverem sido criadas.

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. Digite um título para a configuração e clique em Criar.
1. No campo Token da API, digite o valor da propriedade Token da API da conta de usuário do Gerenciamento dinâmico de tags.

   Para obter o valor do token da API, entre em contato com o Atendimento ao cliente do DTM.

   >[!NOTE]
   >
   >O token da API não expira até que o usuário do Gerenciamento dinâmico de tags o solicite explicitamente.

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. Clique em Conectar-se ao DTM. AEM autenticação com o Gerenciamento dinâmico de tags e recupera a lista do empresa à qual sua conta está associada.
1. Selecione a Empresa e, em seguida, selecione a Propriedade que você está usando para rastrear seu site AEM.
1. Se você estiver usando o código de preparo na instância do autor, desmarque Incluir código de produção no autor.
1. Forneça valores para as propriedades na guia Configurações de preparo e na guia Configurações de produção, se necessário, e clique em OK.

## Download manual da biblioteca do Gerenciamento dinâmico de tags {#manually-downloading-the-dynamic-tag-management-library}

Baixe manualmente as bibliotecas do Gerenciamento dinâmico de tags para atualizá-las imediatamente no AEM. Por exemplo, baixe manualmente quando quiser testar uma biblioteca atualizada antes que o importador de pesquisa esteja programado para baixar automaticamente a biblioteca.

1. No trilho, clique em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na área Gerenciamento dinâmico de tags, clique em Mostrar configurações e clique em sua configuração.
1. Na área Configurações de preparo ou Configurações de produção, clique no botão Fluxo de trabalho de download do acionador para baixar e implantar o pacote da biblioteca.

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>Os arquivos baixados são armazenados em `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`.
>
>As informações a seguir são obtidas diretamente da sua [configuração do DTM](#creating-the-dynamic-tag-management-configuration).
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`

>



## Associando uma configuração do Gerenciamento dinâmico de tags ao seu site {#associating-a-dynamic-tag-management-configuration-with-your-site}

Associe sua configuração do Gerenciamento dinâmico de tags às páginas do site para que AEM adicione o script necessário às páginas. Associe a página raiz do site à configuração. Todos os descendentes dessa página herdam a associação. Se necessário, é possível substituir a associação em uma página descendente.

Use o procedimento a seguir para associar uma página e os descendentes a uma configuração do Gerenciamento dinâmico de tags.

1. Abra a página raiz do site na interface clássica.
1. Use o Sidekick para abrir as propriedades da página.
1. Na guia Cloud Services, clique em Adicionar serviço, selecione Gerenciamento dinâmico de tags e clique em OK.

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. Use o menu suspenso Gerenciamento dinâmico de tags para selecionar sua configuração e clique em OK.

Use o procedimento a seguir para substituir a associação de configuração herdada de uma página. A substituição afeta a página e todos os descendentes da página.

1. Abra a página na interface clássica.
1. Use o Sidekick para abrir as propriedades da página.
1. Na guia Cloud Services, clique no ícone de cadeado ao lado da propriedade Herdado de e, em seguida, clique em Sim na caixa de diálogo de confirmação.

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. Remova ou selecione uma configuração diferente do Gerenciamento dinâmico de tags e clique em OK.

