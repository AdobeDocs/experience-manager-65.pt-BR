---
title: Resumo dos novos recursos | AEM 6.5 Forms
description: Recursos e melhorias mais recentes em formulários e documentos da solução de gerenciamento de experiência digital mais avançada do mundo.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 2%

---

# Resumo dos novos recursos | AEM 6.5 Forms{#new-features-summary-aem-forms}

## Relatórios de transação {#transaction-reports}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/latest-innovations.html) |
| AEM 6.5 | Este artigo |


Relatórios de transação permitem capturar e rastrear o número de formulários enviados, documentos processados e documentos renderizados. O objetivo por trás do rastreamento dessas transações é tomar uma decisão informada sobre o uso do produto e reequilibrar os investimentos em hardware e software. Alguns exemplos de transações incluem:

* Envio de um formulário adaptável, um formulário HTML5 ou um conjunto de formulários
* Representação de uma versão impressa ou da Web de uma comunicação interativa
* Conversão de um documento de um formato de arquivo para outro

Para obter informações sobre como configurar e usar relatórios de transações, consulte [Visão Geral dos Relatórios de Transação](../../forms/using/transaction-reports-overview.md).

![Um exemplo de relatório de transação](assets/surface_transaction_reporting.png)

## Comunicações interativas {#interactive-communications}

**Definir padrões de exibição de dados**

Os autores de comunicações interativas agora podem definir [padrões de exibição de dados](create-interactive-communication.md#datadisplaypatterns) para campos, variáveis e elementos do modelo de dados de formulário. Por exemplo, formatos de data, moeda ou telefone.

**Usar novos tipos de gráficos**

Agora você pode adicionar [Gráficos de quadrante e gráficos com várias séries](../../forms/using/chart-component-interactive-communications.md) para Comunicações interativas.

**Classificar colunas em uma tabela**

Agora você pode [classificar colunas de uma tabela](../../forms/using/create-interactive-communication.md#sortcolumns) na comunicação interativa. Você pode vincular e classificar colunas da tabela com texto estático ou objetos de modelo de dados.

**Usar novos componentes em um canal da Web**

Agora é possível adicionar os componentes Botão e Separador ao canal da Web. Para obter mais informações, consulte [Adicionar o componente de Botão ao canal da Web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) e [Componente separador no canal da Web](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Modo de layout para redimensionar componentes**

Agora você pode alternar para [Modo de layout](../../forms/using/resize-using-layout-mode.md) para redimensionar componentes no canal da Web usando uma interface WYSIWYG.

**Melhorias de usabilidade**

Os autores de comunicações interativas agora podem utilizar várias operações fáceis de usar ao criar correspondências. A lista de operações inclui:

* [Executar ações desfazer e refazer em canais de impressão e da Web](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Adicionar variáveis em um fragmento de documento usando o símbolo @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Adicionar elementos do modelo de dados em um fragmento de documento usando o símbolo @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Excluir ou adicionar um canal da Web a uma Comunicação interativa existente](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Vincular elementos de fonte de dados a campos e variáveis usando ações de arrastar e soltar](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Realçar campos e variáveis desvinculados ao criar a Comunicação interativa](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Executar ações adicionais, como copiar, agrupar ou mais, em componentes herdados em um canal da Web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Melhorias no processo de sincronização**

Há várias melhorias no layout de canal da Web gerado automaticamente usando o canal de impressão.

![Gráficos de comunicações interativas](assets/interactive-communication-charts.png)

## Adaptive Forms {#adaptive-forms}

### Usar assinaturas digitais baseadas em nuvem do Adobe Sign no Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Assinaturas digitais baseadas em nuvem](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) As assinaturas remotas são uma nova geração de assinaturas digitais que funcionam em computadores de mesa, dispositivos móveis e na Web — e atendem aos mais altos níveis de conformidade e garantia para autenticação de signatário. Agora você pode [assinar um Formulário adaptável](../../forms/using/working-with-adobe-sign.md) com assinaturas digitais baseadas em nuvem.

#### Incorpore um formulário adaptável ou a comunicação interativa nos aplicativos de página única do AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

O AEM Forms permite [incorporar facilmente um Formulário adaptável](../../forms/using/embed-adaptive-form-aem-sites-spa.md) ou Comunicação interativa em um aplicativo de página única (SPA) do AEM Sites. O formulário adaptável incorporado e a comunicação interativa são totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário adaptável ou a Comunicação interativa.

#### Classificar colunas de tabelas do Formulário adaptável {#sort-columns-of-adaptive-form-tables}

Você pode [classificar qualquer coluna de uma tabela de Formulário adaptável](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) em ordem crescente ou decrescente. Você pode aplicar a classificação a colunas de tabela com texto estático, propriedades do objeto de modelo de dados ou uma combinação de texto estático e propriedades do objeto de modelo de dados.

#### Restringir a disponibilidade de modelos do Adaptive Forms a caminhos específicos {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Formulários adaptáveis adicionaram suporte para a propriedade cq:allowedPaths. A propriedade [restringe a disponibilidade dos modelos do Adaptive Forms a caminhos específicos](creating-adaptive-form.md#adaptive-form-templates).

#### Adicionar caixas de seleção ao Formulário adaptável dinamicamente {#add-check-boxes-to-the-adaptive-form-dynamically}

Agora você pode definir regras para [adicionar caixas de seleção ao Formulário adaptável dinamicamente](../../forms/using/rule-editor.md#setpropertyrule) com base na função personalizada, um objeto de formulário ou uma propriedade de objeto.

## Fluxos de trabalho do AEM {#aem-workflows}

### Usar variáveis em fluxos de trabalho do AEM {#use-variables-in-aem-workflows}

As variáveis permitem que as etapas do fluxo de trabalho retenham e transmitam metadados pelas etapas do fluxo de trabalho no tempo de execução. É possível criar diferentes tipos de variáveis para armazenar diferentes tipos de dados. Por exemplo, números inteiros, sequências, documentos ou instâncias de modelo de dados de formulário. Normalmente, você usa uma variável ou uma coleção de variáveis quando precisa tomar uma decisão com base no valor que ela contém ou armazenar informações necessárias posteriormente em um processo.

As variáveis são uma extensão de [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponível na versão anterior. Ajuda a economizar tempo gasto no desenvolvimento do código ECMAScript personalizado usado para recuperar e atualizar valores de metadados. Você continua usando a interface MetaDataMap e o código ECMAScript para manipular metadados. Alguns benefícios do uso de variáveis no MetaDataMap e no ECMAScript são:

* Armazenar, atualizar e usar dinamicamente os valores armazenados em uma variável em todo o fluxo de trabalho, sem depender do código personalizado
* Recuperar e atualizar valores diretamente para um modelo de dados de formulário e arquivo de dados (XML/JSON ) de um formulário enviado
* Armazenar documentos completos em uma variável para executar o processamento de documentos

As etapas Ir para, OU Divisão e todas as etapas de fluxo de trabalho do AEM Forms são compatíveis com variáveis. Você pode usar a interface do MetaDataMap para acessar variáveis em etapas de fluxo de trabalho que não têm suporte nativo para variáveis. Para obter mais informações, consulte [Variáveis em fluxos de trabalho do AEM](../../forms/using/variable-in-aem-workflows.md).

![Configuração de uma variável para em um workflow](assets/variable.png)

#### Usar um fluxo de trabalho com um Forms adaptável diferente  {#use-a-workflow-with-different-adaptive-forms}

Você pode [especificar um Formulário adaptável para a tarefa atribuir](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) e documento de etapa de registro de fluxos de trabalho centrados em formulário no tempo de execução. Ela permite que um fluxo de trabalho funcione com Forms adaptável diferente. É possível decidir o método para selecionar um Formulário adaptável ao criar o fluxo de trabalho. O formulário adaptável pode estar localizado em um caminho absoluto, enviado como carga para o fluxo de trabalho ou disponível em um caminho calculado usando uma variável.

#### Usar recursos de log aprimorados de etapas de fluxo de trabalho centradas em formulários {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Os recursos de registro das etapas de fluxo de trabalho centradas em formulários são padronizados. Agora, todas as etapas de fluxo de trabalho centradas em formulários produzem logs padronizados semelhantes. Isso ajuda a melhorar a velocidade de depuração.

## Integração de dados {#data-integration}

Agora você pode:

* [Validar dados de entrada](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) com base em uma lista de restrições. Isso ajuda a garantir que somente dados válidos sejam enviados para a fonte de dados.
* [Substituir ponto de extremidade padrão](../../forms/using/configure-data-sources.md#configure-soap-web-services) definida em um arquivo WSDL (Web Services Description Language).

* [Substituir padrão](../../forms/using/configure-data-sources.md#configure-restful-web-services) [esquema, host e caminho base](../../forms/using/configure-data-sources.md#configure-restful-web-services) definido no arquivo de definição do Swagger.

## Atualizações de plataforma e segurança {#platform-and-security-updates}

### Principais atualizações da plataforma {#major-platform-updates}

O AEM Forms pode ser configurado usando qualquer combinação de sistemas operacionais, servidores de aplicativos, bancos de dados, drivers de banco de dados, JDK, servidores LDAP e servidores de e-mail compatíveis. A seguir estão as principais alterações [plataformas compatíveis](../../forms/using/aem-forms-jee-supported-platforms.md):

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
     <li>RAC do oracle</li>
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
     <li>Conector do Microsoft Sharepoint 2013</li>
     <li>Conector do EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>aplicativo AEM Forms<br /> </td>
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

&#42; Entre em contato com o Suporte do Adobe para obter informações sobre como migrar para uma plataforma diferente

#### Novas interfaces do usuário baseadas em HTML5 {#new-html-based-uis}

De acordo com o fim da vida útil planejado do Flash Player de Adobe e a direção geral da migração de conteúdo baseado em Flash para padrões abertos, o 6.5 Forms substituiu a interface baseada em Flash do Health Monitor, Process Management, Reader Extension e Category Management UI do AEM Forms HTML no Console de administração do JEE pela interface baseada em AEM5.

#### Melhorias de segurança {#security-improvements}

* A interface do usuário do console de administração do AEM 6.5 Forms no JEE agora é baseada no Apache Struts 2.5.
* O AEM 6.5 Forms agora usa jQuery para 3.2.1 e jQuery UI 1.12.1. Consulte [documentação de atualização](/help/forms/home.md) para o impacto da alteração.

#### Melhorias de acessibilidade {#accessibility-improvements}

O AEM 6.5 Forms melhorou a acessibilidade do AEM Forms Workspace.
