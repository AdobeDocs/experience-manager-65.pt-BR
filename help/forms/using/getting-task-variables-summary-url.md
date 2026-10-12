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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%
---
# Recuperando Variáveis de Tarefa no URL de Resumo {#getting-task-variables-in-summary-url}

A página de resumo exibe informações relacionadas à tarefa. Este artigo descreve como você pode reutilizar informações relacionadas à tarefa na página de resumo.

Nesta orquestração de exemplo, um funcionário envia um formulário de inscrição de licença. O formulário de inscrição é então enviado ao gerente do funcionário para aprovação.

1. Crie um renderizador de HTML de exemplo (html.esp) para resourseType **Employees/PtoApplication**.

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

      As chaves neste mapa devem ser as mesmas definidas no renderizador do HTML na etapa anterior.

      Além disso, adicione uma chave **sling:resourceType** com o valor **Employees/PtoApplication** no mapa.

   1. Use o subprocesso **storeContent** do serviço **ContentRepositoryConnector** no processo **criar resumo PTO**. Esse subprocesso cria um nó CRX.

      São necessárias três variáveis de entrada:

      * **Caminho da pasta**: o caminho onde o novo nó do CRX é criado. Defina o caminho como **/content**.
      * **Nome do nó**: atribua a variável de entrada nodeName a este campo. É uma string exclusiva de nome de nó.
      * **Tipo de nó**: defina o tipo como **nt:unstructured**. A saída desse processo é nodePath. O nodePath é o caminho CRX do nó recém-criado. O nodePath seria a saída final do processo de resumo **criar PTO**.

   1. Transmita os dados do formulário enviado (**employeeName**, **employeeID**, **ptoReason** e **totalDays**) como entrada para o novo processo **criar resumo PTO**. Usar a saída como **ptoSummaryNodePath**.

1. Defina a Url de resumo como uma expressão XPath contendo os detalhes do servidor junto com **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Na área de trabalho do AEM Forms, ao abrir uma tarefa, o URL do resumo acessa o nó do CRX e o renderizador do HTML exibe o resumo.

O layout de resumo pode ser alterado sem modificar o processo. O renderizador do HTML exibe o resumo apropriadamente.
