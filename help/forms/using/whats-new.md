---
title: Resumo dos novos recursos | AEM 6.5 Forms
seo-title: New features summary | AEM 6.5 Forms
description: Recursos e melhorias mais recentes para formulários e documentos da solução de gerenciamento de experiência digital mais avançada do mundo.
seo-description: Latest features and improvements to forms and documents of world’s most advanced digital experience management solution.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 1%

---

# Resumo dos novos recursos | AEM 6.5 Forms{#new-features-summary-aem-forms}

## Relatórios de transação {#transaction-reports}

Relatórios de transação permitem capturar e rastrear o número de formulários enviados, documentos processados e documentos renderizados. O objetivo do rastreamento dessas transações é tomar uma decisão informada sobre o uso do produto e reequilibrar os investimentos em hardware e software. Alguns exemplos de transações incluem:

* Envio de um formulário adaptável, um formulário HTML5 ou um conjunto de formulários
* Representação de uma versão impressa ou da Web de uma comunicação interativa
* Conversão de um documento de um formato de arquivo para outro

Para obter informações sobre como configurar e usar relatórios de transações, consulte [Visão geral dos relatórios de transação](../../forms/using/transaction-reports-overview.md).

![Um exemplo de relatório de transação](assets/surface_transaction_reporting.png)

## Comunicações interativas {#interactive-communications}

**Definir padrões de exibição de dados**

Os autores de Comunicações interativas agora podem definir [padrões de exibição de dados](create-interactive-communication.md#datadisplaypatterns) para campos, variáveis e elementos do modelo de dados de formulário. Por exemplo, formatos de data, moeda ou telefone.

**Usar novos tipos de gráficos**

Agora você pode adicionar [Gráficos de quadrantes e gráficos com várias séries](../../forms/using/chart-component-interactive-communications.md) para Comunicações interativas.

**Classificar colunas em uma tabela**

Agora você pode [classificar colunas de uma tabela](../../forms/using/create-interactive-communication.md#sortcolumns) na Comunicação interativa. É possível vincular e classificar colunas de tabela com objetos de texto estáticos ou de modelo de dados.

**Usar novos componentes em um canal da Web**

Agora é possível adicionar componentes Botão e Separador ao canal da Web. Para obter mais informações, consulte [Componente Adicionar botão ao canal da Web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) e [Componente separador no canal da Web](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Modo Layout para redimensionar componentes**

Agora você pode alternar para [Modo Layout](../../forms/using/resize-using-layout-mode.md) para redimensionar componentes no canal da Web usando uma interface WYSIWYG.

**Aprimoramentos de usabilidade**

Os autores de Comunicações interativas agora podem utilizar várias operações fáceis de usar ao criar correspondências. A lista de operações inclui:

* [Realizar ações de refazer desfeito em canais impressos e da Web](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Adicionar variáveis em um fragmento de documento usando o símbolo @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Adicionar elementos do modelo de dados em um fragmento de documento usando o símbolo @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Excluir ou adicionar um canal Web a uma Comunicação interativa existente](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Vincule elementos de fonte de dados com campos e variáveis usando ações de arrastar e soltar](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Realçar campos e variáveis não vinculados durante a criação da Comunicação interativa](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Executar ações adicionais, como copiar, agrupar ou mais em componentes herdados em um canal da Web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Melhorias no processo de sincronização**

Há várias melhorias no layout do canal da Web gerado automaticamente usando o canal de impressão.

![Gráficos de comunicações interativas](assets/interactive-communication-charts.png)

## Formulários adaptáveis {#adaptive-forms}

### Usar assinaturas digitais baseadas em nuvem do Adobe Sign no Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Assinaturas digitais baseadas em nuvem](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ou assinaturas remotas são uma nova geração de assinaturas digitais que funcionam em computadores, dispositivos móveis e na Web — e atendem aos mais altos níveis de conformidade e garantia para autenticação de assinante. Agora você pode [assinar um formulário adaptável](../../forms/using/working-with-adobe-sign.md) com assinaturas digitais baseadas em nuvem.

#### Incorpore um formulário adaptável ou uma comunicação interativa em aplicativos de página única do AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

O AEM Forms permite [Incorporar um formulário adaptável sem interrupções](../../forms/using/embed-adaptive-form-aem-sites-spa.md) ou Comunicação interativa em um aplicativo de página única (SPA) do AEM Sites. O Formulário adaptativo incorporado e a Comunicação interativa são totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário adaptável ou a Comunicação interativa.

#### Classificar colunas de tabelas de formulário adaptável {#sort-columns-of-adaptive-form-tables}

Você pode [classificar qualquer coluna de uma tabela de Formulário adaptável](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) em ordem crescente ou decrescente. É possível aplicar a classificação a colunas da tabela com texto estático, propriedades de objetos do modelo de dados ou uma combinação de propriedades de objetos de texto estático e de modelo de dados.

#### Restringir a disponibilidade de modelos Forms adaptáveis a caminhos específicos {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Formulários adaptáveis adicionaram suporte à propriedade cq:allowedPaths. A propriedade [restringe a disponibilidade de modelos Adaptive Forms a caminhos específicos](creating-adaptive-form.md#adaptive-form-templates).

#### Adicionar caixas de seleção ao formulário adaptável dinamicamente {#add-check-boxes-to-the-adaptive-form-dynamically}

Agora é possível definir regras para [adicionar caixas de seleção dinamicamente ao formulário adaptável](../../forms/using/rule-editor.md#setpropertyrule) com base em função personalizada, objeto de formulário ou propriedade de objeto.

## Fluxos de trabalho do AEM {#aem-workflows}

### Usar variáveis em fluxos de trabalho AEM {#use-variables-in-aem-workflows}

As variáveis permitem que as etapas do fluxo de trabalho mantenham e transmitam metadados nas etapas do fluxo de trabalho no tempo de execução. Você pode criar diferentes tipos de variáveis para armazenar diferentes tipos de dados. Por exemplo, instâncias de números inteiros, sequências, documentos ou modelos de dados de formulário. Normalmente, você usa uma variável ou uma coleção de variáveis quando precisa tomar uma decisão com base no valor que ela contém ou armazenar informações necessárias posteriormente em um processo.

As variáveis são uma extensão de [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponível na versão anterior. Ajuda a economizar tempo no desenvolvimento de código ECMAScript personalizado usado para recuperar e atualizar valores de metadados. Você continua usando a interface MetaDataMap e o código ECMAScript para manipular metadados. Alguns benefícios do uso de variáveis sobre MetaDataMap e ECMAScript são:

* Armazene, atualize e use dinamicamente os valores armazenados em uma variável no fluxo de trabalho sem depender do código personalizado
* Recuperar e atualizar valores diretamente em um modelo de dados de formulário e em um arquivo de dados (XML/JSON ) de um formulário enviado
* Armazene documentos completos em uma variável para executar o processamento de documentos

A etapa Ir para ou Split e todas as etapas do fluxo de trabalho do AEM Forms suportam variáveis. Você pode usar a interface MetaDataMap para acessar variáveis em etapas de fluxo de trabalho que não têm suporte nativo para variáveis. Para obter mais informações, consulte [Variáveis em fluxos de trabalho AEM](../../forms/using/variable-in-aem-workflows.md).

![Configuração de uma variável para em um fluxo de trabalho](assets/variable.png)

#### Usar um fluxo de trabalho com o Adaptive Forms diferente  {#use-a-workflow-with-different-adaptive-forms}

Você pode [especificar um formulário adaptável para a tarefa de atribuição](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) e o documento de etapa de registro de fluxos de trabalho centrados em formulários no tempo de execução. Ele permite que um fluxo de trabalho funcione com diferentes Forms adaptáveis. Você pode decidir o método para selecionar um formulário adaptável ao projetar o fluxo de trabalho. O formulário adaptável pode ser localizado em um caminho absoluto, enviado como carga para o fluxo de trabalho ou disponível em um caminho calculado usando uma variável.

#### Usar recursos aprimorados de registro de etapas de fluxo de trabalho centradas em formulários {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Os recursos de registro das etapas do fluxo de trabalho centradas em formulários são padronizados. Agora, todas as etapas de fluxo de trabalho centradas em formulários produzem registros padronizados de forma semelhante. Ajuda a melhorar a velocidade de depuração.

## Integração de dados {#data-integration}

Agora você pode:

* [Validar dados de entrada](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) com base em uma lista de restrições. Ajuda a garantir que somente dados válidos sejam enviados para a fonte de dados.
* [Substituir ponto de extremidade padrão](../../forms/using/configure-data-sources.md#configure-soap-web-services) definido em um arquivo WSDL (Web Services Description Language).

* [Substituir padrão](../../forms/using/configure-data-sources.md#configure-restful-web-services) [esquema, host e caminho base](../../forms/using/configure-data-sources.md#configure-restful-web-services) definido no arquivo de definição Swagger.

## Atualizações de plataforma e segurança {#platform-and-security-updates}

### Atualizações importantes da plataforma {#major-platform-updates}

O AEM Forms pode ser configurado usando qualquer combinação de sistemas operacionais, servidores de aplicativos, bancos de dados, drivers de banco de dados, JDK, servidores LDAP e servidores de email compatíveis. Estas são as principais mudanças no [plataformas compatíveis](../../forms/using/aem-forms-jee-supported-platforms.md):

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
    <li>Perfil do WebSphere Liberty</li>
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
     <li>Conector para EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Aplicativo AEM Forms<br /> </td>
   <td>
    <ul>
     <li>Suporte para Windows 8.1</li>
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

&#42; Entre em contato com o Suporte do Adobe para obter informações sobre como migrar para uma plataforma diferente

#### Novas interfaces de usuário baseadas no HTML5 {#new-html-based-uis}

De acordo com o EOL planejado do Flash Player do Adobe e a direção geral da migração do conteúdo baseado em Flashes para padrões abertos, AEM 6.5 a Forms substituiu a interface do usuário baseada em Flash do Monitor de Integridade, Gerenciamento de Processos, Extensão do Reader e Interface do usuário de Gerenciamento de Categorias do AEM Forms no Console de Administração do JEE por HTML UI baseada em5.

#### Melhorias de segurança {#security-improvements}

* O AEM 6.5 Forms na interface do usuário do console de administração JEE agora é baseado no Apache Struts 2.5.
* AEM 6.5 Forms agora usa o jQuery para 3.2.1 e a interface do usuário do jQuery 1.12.1. Consulte, [documentação de atualização](/help/forms/home.md) para o impacto da alteração.

#### Melhorias de acessibilidade {#accessibility-improvements}

O AEM 6.5 Forms melhorou a acessibilidade do AEM Forms Workspace.
