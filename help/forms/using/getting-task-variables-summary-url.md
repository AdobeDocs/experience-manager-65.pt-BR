---
title: Recuperando Variáveis de Tarefa no URL de Resumo
description: Como reutilizar as informações sobre uma tarefa e gerar um URL de resumo para resumir ou descrever uma tarefa.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Recuperando Variáveis de Tarefa no URL de Resumo {#getting-task-variables-in-summary-url}

A página de resumo exibe informações relacionadas à tarefa. Este artigo descreve como você pode reutilizar informações relacionadas à tarefa na página de resumo.

Nesta orquestração de exemplo, um funcionário envia um formulário de inscrição de licença. O formulário de inscrição é então enviado ao gerente do funcionário para aprovação.

1. Crie um renderizador de HTML de amostra (html.esp) para resourseType **Employees/PtoApplication**.

   O renderizador pressupõe que as seguintes propriedades sejam definidas no nó:

   * ename
   * empid
   * motivo
   * duração

   >[!NOTE]
   >
   >Esse renderizador é o modelo da página de resumo.

   O seguinte código de amostra para esse renderizador está contido em:

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. Modifique a orquestração para extrair as quatro propriedades dos dados de formulário enviados. Depois disso, crie um nó no CRX do tipo **Employees/PtoApplication**, com as propriedades preenchidas.

   1. Crie um processo **criar resumo de PTO** e use-o como um subprocesso antes da operação **Atribuir Tarefa** em sua orquestração.
   1. Defina **employeeName**, **employeeID**, **ptoReason**, **totalDays** e **nodeName** como variáveis de entrada em seu novo processo. Essas variáveis serão transmitidas como dados de formulário enviados.

      Defina também uma variável de saída **ptoNodePath**, que é usada ao definir a URL de resumo.

   1. No processo **criar resumo de PTO**, use o componente **definir valor** para definir os detalhes de entrada em um mapa de **nodeProperty**(**nodeProps**).

      As chaves neste mapa devem ser as mesmas definidas no renderizador de HTML na etapa anterior.

      Além disso, adicione uma chave **sling:resourceType** com o valor **Employees/PtoApplication** no mapa.

   1. Use o subprocesso **storeContent** do serviço **ContentRepositoryConnector** no processo **criar resumo PTO**. Esse subprocesso cria um nó CRX.

      São necessárias três variáveis de entrada:

      * **Caminho da pasta**: o caminho onde o novo nó do CRX é criado. Defina o caminho como **/content**.
      * **Nome do nó**: atribua a variável de entrada nodeName a este campo. É uma string exclusiva de nome de nó.
      * **Tipo de Nó**: defina o tipo como **nt:unstructured**. A saída desse processo é nodePath. O nodePath é o caminho CRX do nó recém-criado. O nodePath seria a saída final do processo de resumo **criar PTO**.

   1. Transmita os dados do formulário enviado (**employeeName**, **employeeID**, **ptoReason** e **totalDays**) como entrada para o novo processo **criar resumo PTO**. Usar a saída como **ptoSummaryNodePath**.

1. Defina a Url de resumo como uma expressão XPath contendo os detalhes do servidor junto com **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Na área de trabalho do AEM Forms, ao abrir uma tarefa, o URL de resumo acessa o nó do CRX e o renderizador de HTML exibe o resumo.

O layout de resumo pode ser alterado sem modificar o processo. O renderizador de HTML exibe o resumo apropriadamente.
