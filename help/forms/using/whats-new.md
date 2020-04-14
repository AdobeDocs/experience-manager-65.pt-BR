---
title: Resumo dos novos recursos| Formulários AEM 6.5
seo-title: Resumo dos novos recursos| Formulários AEM 6.5
description: Recursos e melhorias mais recentes em formulários e documentos da solução de gerenciamento de experiências digitais mais avançada do mundo.
seo-description: Recursos e melhorias mais recentes em formulários e documentos da solução de gerenciamento de experiências digitais mais avançada do mundo.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Resumo dos novos recursos| Formulários AEM 6.5{#new-features-summary-aem-forms}

## Relatórios de transação {#transaction-reports}

Os relatórios de transação permitem capturar e rastrear o número de formulários enviados, documentos processados e documentos renderizados. O objetivo do rastreamento dessas transações é tomar uma decisão informada sobre o uso do produto e rebalancear os investimentos em hardware e software. Alguns exemplos de transações incluem:

* Envio de um formulário adaptável, de um formulário HTML5 ou de um conjunto de formulários
* Execução de uma versão impressa ou da Web de uma comunicação interativa
* Conversão de um documento de um formato de arquivo para outro

Para obter informações sobre como configurar e usar relatórios de transação, consulte Visão geral [dos relatórios de](../../forms/using/transaction-reports-overview.md)transação.

![Um relatório de transação de amostra](assets/surface_transaction_reporting.png)

## Comunicações interativas {#interactive-communications}

**Definir padrões de exibição de dados**

Os autores do Interative Communication agora podem definir padrões [de exibição de](create-interactive-communication.md#datadisplaypatterns) dados para campos, variáveis e elementos de modelo de dados de formulário. Por exemplo, formatos de data, moeda ou telefone.

**Usar novos tipos de gráficos**

Agora você pode adicionar gráficos e gráficos [Quadrantes com várias séries](../../forms/using/chart-component-interactive-communications.md) ao Interative Communications.

**Classificar colunas em uma tabela**

Agora é possível [classificar colunas de uma tabela](../../forms/using/create-interactive-communication.md#sortcolumns) na Comunicação interativa. É possível vincular e classificar colunas de tabela com objetos de texto estáticos ou de modelo de dados.

**Usar novos componentes em um canal da Web**

Agora você pode adicionar componentes Botão e Separador ao canal da Web. Para obter mais informações, consulte [Adicionar componente de Botão ao canal](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) da Web e ao componente [Separador no canal](../../forms/using/create-interactive-communication.md#separatorcomponent)da Web.

**Modo de layout para redimensionar componentes**

Agora você pode alternar para o modo [](../../forms/using/resize-using-layout-mode.md) Layout para redimensionar componentes no canal da Web usando uma interface WYSIWYG.

**Melhorias na usabilidade**

Os autores do Interative Communication agora podem utilizar várias operações fáceis de usar ao criar correspondências. A lista de operações inclui:

* [Realizar ações de desfazer e refazer em canais da Web e da impressão](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Adicionar variáveis em um fragmento de documento usando o símbolo @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Adicionar elementos de modelo de dados em um fragmento de documento usando o símbolo @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Excluir ou adicionar um canal da Web a uma comunicação interativa existente](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Vincular elementos de fonte de dados a campos e variáveis usando ações de arrastar e soltar](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Realçar campos e variáveis não vinculados ao criar o Interative Communication](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Executar ações adicionais, como copiar, agrupar ou mais, em componentes herdados em um canal da Web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Melhorias no processo de sincronização**

Há várias melhorias no layout do canal da Web gerado automaticamente usando o canal Imprimir.

![Gráficos de Comunicações Interativas](assets/interactive-communication-charts.png)

## Formulários adaptáveis {#adaptive-forms}

### Usar assinaturas digitais baseadas em nuvem do Adobe Sign nos formulários adaptativos {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Assinaturas](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) digitais ou remotas baseadas em nuvem são uma nova geração de assinaturas digitais que funcionam em computadores, dispositivos móveis e na Web. e atender aos mais altos níveis de conformidade e garantia para autenticação de assinante. Agora você pode [assinar um Formulário](../../forms/using/working-with-adobe-sign.md) adaptável com assinaturas digitais baseadas em nuvem.

#### Incorporar um formulário adaptável ou uma comunicação interativa em aplicativos de página única do AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

O AEM Forms permite incorporar [perfeitamente um Formulário](../../forms/using/embed-adaptive-form-aem-sites-spa.md) adaptável ou uma comunicação interativa em um aplicativo de página única (SPA) do AEM Sites. O Formulário adaptativo incorporado e a Comunicação interativa estão totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e a interagir simultaneamente com o formulário adaptável ou com a Comunicação interativa.

#### Ordenar colunas de tabelas de Formulário adaptável {#sort-columns-of-adaptive-form-tables}

É possível [classificar qualquer coluna de uma tabela](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) de Formulário adaptável em ordem crescente ou decrescente. É possível aplicar a classificação a colunas de tabela com texto estático, propriedades de objetos de modelo de dados ou uma combinação de propriedades de objetos de texto estático e modelo de dados.

#### Restringir a disponibilidade de modelos de formulários adaptáveis a caminhos específicos {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Formulários adaptáveis adicionaram suporte para a propriedade cq:allowPaths. A propriedade [restringe a disponibilidade de modelos de Formulários adaptáveis a caminhos](../../forms/using/creating-adaptive-form.md#main-pars-text)específicos.

#### Adicionar caixas de seleção ao formulário adaptativo dinamicamente {#add-check-boxes-to-the-adaptive-form-dynamically}

Agora, é possível definir regras para [adicionar caixas de seleção ao Formulário adaptável dinamicamente](../../forms/using/rule-editor.md#setpropertyrule) com base na função personalizada, em um objeto de formulário ou em uma propriedade de objeto.

## Fluxos de trabalho do AEM {#aem-workflows}

### Usar variáveis em Workflows AEM {#use-variables-in-aem-workflows}

As variáveis permitem que as etapas do fluxo de trabalho mantenham e passem metadados pelas etapas do fluxo de trabalho no tempo de execução. Você pode criar diferentes tipos de variáveis para armazenar diferentes tipos de dados. Por exemplo, inteiros, sequências, documentos ou instâncias de modelo de dados de formulário. Geralmente, você usa uma variável ou uma coleção de variáveis quando precisa tomar uma decisão com base no valor que ela contém ou armazenar informações necessárias posteriormente em um processo.

As variáveis são uma extensão da interface [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponível na versão anterior. Ele ajuda a economizar tempo gasto no desenvolvimento de código ECMAScript personalizado usado para recuperar e atualizar valores de metadados. Você continua usando a interface MetaDataMap e o código ECMAScript para manipular metadados. Alguns benefícios do uso de variáveis sobre MetaDataMap e ECMAScript são:

* Armazenar, atualizar e usar dinamicamente valores armazenados em uma variável no fluxo de trabalho sem depender do código personalizado
* Recuperar e atualizar valores diretamente em um modelo de dados de formulário e em um arquivo de dados (XML/JSON ) de um formulário enviado
* Armazene documentos completos em uma variável para executar o processamento de documentos

A etapa Ir para ou a etapa Dividir e todas as etapas do fluxo de trabalho do AEM Forms suportam variáveis. Você pode usar a interface do MetaDataMap para acessar variáveis em etapas de fluxo de trabalho que não têm suporte nativo para variáveis. Para obter mais informações, consulte [Variáveis em Workflows](../../forms/using/variable-in-aem-workflows.md)AEM.

![Configuração de uma variável para em um fluxo de trabalho](assets/variable.png)

#### Usar um fluxo de trabalho com diferentes Formulários adaptativos {#use-a-workflow-with-different-adaptive-forms}

É possível [especificar um Formulário adaptável para atribuir tarefa](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) e documento da etapa de registro de workflows centrados em formulários no tempo de execução. Ele permite que um fluxo de trabalho funcione com diferentes Formulários adaptativos. Você pode decidir o método para selecionar um Formulário adaptável ao projetar o fluxo de trabalho. O Formulário adaptativo pode ser localizado em um caminho absoluto, enviado como carga para o fluxo de trabalho ou disponível em um caminho calculado usando uma variável.

#### Usar recursos de registro aprimorados de etapas de fluxo de trabalho centradas em formulários {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Os recursos de registro das etapas do fluxo de trabalho centradas em formulários são padronizados. Agora, todas as etapas do fluxo de trabalho centradas em formulários produzem registros padronizados semelhantes. Isso ajuda a melhorar a velocidade de depuração.

## Integração de dados {#data-integration}

Agora você pode:

* [Valide os dados](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) de entrada com base em uma lista de restrições. Ele ajuda a garantir que somente dados válidos sejam enviados para a fonte de dados.
* [Substitua o endpoint](../../forms/using/configure-data-sources.md#configure-soap-web-services) padrão definido em um arquivo WSDL (Web Services Description Language).

* [Substitua o](../../forms/using/configure-data-sources.md#configure-restful-web-services) esquema padrão [, o host e o caminho](../../forms/using/configure-data-sources.md#configure-restful-web-services) base definidos no arquivo de definição do Swagger.

## Atualizações de plataforma e segurança {#platform-and-security-updates}

### Principais atualizações da plataforma {#major-platform-updates}

O AEM Forms pode ser configurado usando qualquer combinação de sistemas operacionais, servidores de aplicativos, bancos de dados, drivers de banco de dados, JDK, servidores LDAP e servidores de email suportados. Veja a seguir as principais mudanças nas plataformas [](../../forms/using/aem-forms-jee-supported-platforms.md)suportadas:

<table>
 <tbody>
  <tr>
   <td>Componente</td>
   <td>Suporte removido</td>
  </tr>
  <tr>
   <td>Sistemas operacionais</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Servidores de aplicativos<br /> </td>
   <td>
    <ul>
     <li>Oracle Weblogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Bancos de dados</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Servidores LDAP</td>
   <td>
    <ul>
     <li>Microsoft Ative Diretory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Servidores de email</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Conectores</td>
   <td>
    <ul>
     <li>Conector para Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
   <td>
    <ul>
     <li>Suporte ao Windows 8.1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* Entre em contato com o suporte da Adobe para obter informações sobre como migrar para uma plataforma diferente

#### Novas interfaces de usuário baseadas em HTML5 {#new-html-based-uis}

Em consonância com o EOL planejado do Adobe Flash Player e a direção geral de migrar o conteúdo baseado em Flash para padrões abertos, o AEM 6.5 Forms substituiu a interface do usuário baseada em Flash do Monitor de integridade, do Gerenciamento de processos, do Reader Extension e da interface de gerenciamento de Categorias do AEM Forms no JEE Administration Console por uma interface baseada em HTML5.

#### Melhorias na segurança {#security-improvements}

* O AEM 6.5 Forms na interface do console de administração JEE agora é baseado no Apache Struts 2.5.
* O AEM 6.5 Forms agora usa jQuery para 3.2.1 e jQuery UI 1.12.1. Consulte a documentação [de](/help/forms/home.md) atualização para conhecer o impacto da alteração.

#### Aprimoramentos de acessibilidade {#accessibility-improvements}

O AEM 6.5 Forms melhorou a acessibilidade do AEM Forms Workspace.
