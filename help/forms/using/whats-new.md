---
title: Resumo dos novos recursos | AEM 6,5 Forms
seo-title: Resumo dos novos recursos | AEM 6,5 Forms
description: Recursos e melhorias mais recentes em formulários e documentos da solução de gerenciamento de experiências digitais mais avançada do mundo.
seo-description: Recursos e melhorias mais recentes em formulários e documentos da solução de gerenciamento de experiências digitais mais avançada do mundo.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: a417094c1d7b28ec54a6e84303d7a9747bb0c510
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---


# Resumo dos novos recursos | AEM 6.5 Forms{#new-features-summary-aem-forms}

## Relatórios de transação {#transaction-reports}

Os relatórios de transação permitem capturar e rastrear o número de formulários enviados, documentos processados e documentos renderizados. O objetivo do rastreamento dessas transações é tomar uma decisão informada sobre o uso do produto e rebalancear os investimentos em hardware e software. Alguns exemplos de transações incluem:

* Envio de um formulário adaptável, de um formulário HTML5 ou de um conjunto de formulários
* Execução de uma versão impressa ou da Web de uma comunicação interativa
* Conversão de um documento de um formato de arquivo para outro

Para obter informações sobre como configurar e usar relatórios de transação, consulte [Visão Geral dos Relatórios de Transação](../../forms/using/transaction-reports-overview.md).

![Um relatório de transação de amostra](assets/surface_transaction_reporting.png)

## Comunicações interativas {#interactive-communications}

**Definir padrões de exibição de dados**

Os autores do Interative Communication agora podem definir [padrões de exibição de dados](create-interactive-communication.md#datadisplaypatterns) para campos, variáveis e elementos de modelo de dados de formulário. Por exemplo, formatos de data, moeda ou telefone.

**Usar novos tipos de gráficos**

Agora você pode adicionar [gráficos quadráticos e gráficos com várias séries](../../forms/using/chart-component-interactive-communications.md) ao Interative Communications.

**Classificar colunas em uma tabela**

Agora você pode [classificar colunas de uma tabela](../../forms/using/create-interactive-communication.md#sortcolumns) na Comunicação Interativa. É possível vincular e classificar colunas de tabela com objetos de texto estáticos ou de modelo de dados.

**Usar novos componentes em um canal da Web**

Agora você pode adicionar componentes Botão e Separador ao canal da Web. Para obter mais informações, consulte [Adicionar componente Botão ao canal da Web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) e [Componente separador no canal da Web](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Modo de layout para redimensionar componentes**

Agora você pode alternar para [modo Layout](../../forms/using/resize-using-layout-mode.md) para redimensionar componentes no canal Web usando uma interface WYSIWYG.

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

### Use assinaturas digitais baseadas em nuvem da Adobe Sign no Forms adaptável {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Assinaturas digitais baseadas em nuvem ou ](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) assinaturas remotas são uma nova geração de assinaturas digitais que funcionam em computadores, dispositivos móveis e na Web. e atender aos mais altos níveis de conformidade e garantia para autenticação de assinante. Agora você pode [assinar um Formulário adaptável](../../forms/using/working-with-adobe-sign.md) com assinaturas digitais baseadas em nuvem.

#### Incorporar um formulário adaptável ou uma comunicação interativa em aplicativos de página única da AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

A AEM Forms permite que você [incorpore sem problemas um Formulário adaptável](../../forms/using/embed-adaptive-form-aem-sites-spa.md) ou uma Comunicação interativa em um aplicativo de página única (SPA) da AEM Sites. O Formulário adaptativo incorporado e a Comunicação interativa estão totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e a interagir simultaneamente com o formulário adaptável ou com a Comunicação interativa.

#### Ordenar colunas de tabelas de Formulário adaptável {#sort-columns-of-adaptive-form-tables}

Você pode [classificar qualquer coluna de uma tabela de Formulário adaptável](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) em ordem crescente ou decrescente. É possível aplicar a classificação a colunas de tabela com texto estático, propriedades de objetos de modelo de dados ou uma combinação de propriedades de objetos de texto estático e modelo de dados.

#### Restringir a disponibilidade de modelos adaptáveis Forms a caminhos específicos {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Formulários adaptáveis adicionaram suporte para a propriedade cq:allowPaths. A propriedade [restringe a disponibilidade de modelos Adaptive Forms a caminhos específicos](creating-adaptive-form.md#adaptive-form-templates).

#### Adicione caixas de seleção ao formulário adaptativo dinamicamente {#add-check-boxes-to-the-adaptive-form-dynamically}

Agora é possível definir regras para [adicionar caixas de seleção ao Formulário adaptável dinamicamente](../../forms/using/rule-editor.md#setpropertyrule) com base na função personalizada, em um objeto de formulário ou em uma propriedade de objeto.

## Fluxos de trabalho do AEM {#aem-workflows}

### Usar variáveis em Workflows AEM {#use-variables-in-aem-workflows}

As variáveis permitem que as etapas do fluxo de trabalho mantenham e passem metadados pelas etapas do fluxo de trabalho no tempo de execução. Você pode criar diferentes tipos de variáveis para armazenar diferentes tipos de dados. Por exemplo, inteiros, sequências, documentos ou instâncias de modelo de dados de formulário. Geralmente, você usa uma variável ou uma coleção de variáveis quando precisa tomar uma decisão com base no valor que ela contém ou armazenar informações necessárias posteriormente em um processo.

As variáveis são uma extensão da interface [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponível na versão anterior. Ele ajuda a economizar tempo gasto no desenvolvimento de código ECMAScript personalizado usado para recuperar e atualizar valores de metadados. Você continua usando a interface MetaDataMap e o código ECMAScript para manipular metadados. Alguns benefícios do uso de variáveis sobre MetaDataMap e ECMAScript são:

* Armazenar, atualizar e usar dinamicamente valores armazenados em uma variável no fluxo de trabalho sem depender do código personalizado
* Recuperar e atualizar valores diretamente em um modelo de dados de formulário e em um arquivo de dados (XML/JSON ) de um formulário enviado
* Armazene documentos completos em uma variável para executar o processamento de documentos

A etapa Ir para, OU a etapa Dividir e todas as etapas do fluxo de trabalho do AEM Forms suportam variáveis. Você pode usar a interface do MetaDataMap para acessar variáveis em etapas de fluxo de trabalho que não têm suporte nativo para variáveis. Para obter mais informações, consulte [Variáveis em AEM Workflows](../../forms/using/variable-in-aem-workflows.md).

![Configuração de uma variável para em um fluxo de trabalho](assets/variable.png)

#### Use um fluxo de trabalho com Forms adaptável diferente {#use-a-workflow-with-different-adaptive-forms}

Você pode [especificar um Formulário adaptável para atribuir a tarefa](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) e o documento da etapa de registro de workflows centrados em formulários no tempo de execução. Ele permite que um fluxo de trabalho funcione com um Forms adaptável diferente. Você pode decidir o método para selecionar um Formulário adaptável ao projetar o fluxo de trabalho. O Formulário adaptativo pode ser localizado em um caminho absoluto, enviado como carga para o fluxo de trabalho ou disponível em um caminho calculado usando uma variável.

#### Use os recursos de registro aprimorados das etapas do fluxo de trabalho centradas em formulários {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Os recursos de registro das etapas do fluxo de trabalho centradas em formulários são padronizados. Agora, todas as etapas do fluxo de trabalho centradas em formulários produzem registros padronizados semelhantes. Isso ajuda a melhorar a velocidade de depuração.

## Integração de dados {#data-integration}

Agora você pode:

* [Valide ](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) dados de entrada com base em uma lista de restrições. Ele ajuda a garantir que somente dados válidos sejam enviados para a fonte de dados.
* [Substituir ](../../forms/using/configure-data-sources.md#configure-soap-web-services) endpoint padrão definido em um arquivo WSDL (Web Services Description Language).

* [Substituir esquema ](../../forms/using/configure-data-sources.md#configure-restful-web-services) [padrão, host e caminho base ](../../forms/using/configure-data-sources.md#configure-restful-web-services) definidos no arquivo de definição do Swagger.

## Atualizações de plataforma e segurança {#platform-and-security-updates}

### Principais atualizações da plataforma {#major-platform-updates}

A AEM Forms pode ser configurada usando qualquer combinação de sistemas operacionais, servidores de aplicativos, bancos de dados, drivers de banco de dados, JDK, servidores LDAP e servidores de email suportados. Veja a seguir as principais alterações em [plataformas suportadas](../../forms/using/aem-forms-jee-supported-platforms.md):

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
    <li>Perfil WebSphere Liberty</li>
    <li>Oracle WebLogic</li>
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
   <td>Aplicativo AEM Forms<br /> </td>
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

* Entre em contato com o suporte ao Adobe para obter informações sobre como migrar para uma plataforma diferente

#### Novas interfaces de usuário baseadas em HTML5 {#new-html-based-uis}

Em consonância com o EOL planejado do Flash Player do Adobe e a direção geral de migração do conteúdo baseado em Flashes para padrões abertos, AEM 6.5 a Forms substituiu a interface do usuário baseada em Flashes do Monitor de Integridade, Gerenciamento de Processo, Extensão de Reader e Interface do usuário de gerenciamento de Categoria do AEM Forms no Console de administração JEE por uma interface baseada em HTML5.

#### Melhorias na segurança {#security-improvements}

* AEM 6.5 A interface do usuário do console de administração JEE agora é baseada no Apache Struts 2.5.
* O AEM 6.5 Forms agora usa jQuery para 3.2.1 e jQuery UI 1.12.1. Consulte [documentação de atualização](/help/forms/home.md) para obter informações sobre o impacto da alteração.

#### Aprimoramentos de acessibilidade {#accessibility-improvements}

AEM 6.5 A Forms melhorou a acessibilidade do AEM Forms Workspace.
