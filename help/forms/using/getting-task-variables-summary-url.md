---
title: Obter variáveis de tarefa no URL de resumo
seo-title: Getting Task Variables in Summary URL
description: Como reutilizar as informações sobre uma tarefa e gerar um URL de resumo para resumir ou descrever uma tarefa.
seo-description: How-to reuse the information about a task and generate a Summary URL to summarize or describe a task.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Obter variáveis de tarefa no URL de resumo {#getting-task-variables-in-summary-url}

A página de resumo exibe informações relacionadas à tarefa. Este artigo descreve como você pode reutilizar informações relacionadas à tarefa na página de resumo.

Nesta orquestração de amostra, um funcionário envia um formulário de aplicativo de licença. O formulário de aplicativo é enviado ao gerente do funcionário para aprovação.

1. Crie um renderizador de HTML de amostra (html.esp) para resourceType **Funcionários/PtoApplication**.

   O renderizador assume as seguintes propriedades para serem definidas no nó:

   * ename
   * empid
   * reason
   * duration

   >[!NOTE]
   >
   >Esse renderizador é o modelo de página de resumo.

   O código de amostra a seguir para esse renderizador está contido em:

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

1. Modifique a orquestração para extrair as quatro propriedades dos dados de formulário enviados. Depois disso, crie um nó no CRX do tipo **Funcionários/PtoApplication**, com as propriedades preenchidas.

   1. Criar um processo **criar resumo PTO** e use-o como um subprocesso antes da variável **Atribuir tarefa** na sua orquestração.
   1. Definir **employeeName**, **employeeID**, **ptoReason**, **totalDays** e **nodeName** como variáveis de entrada no novo processo. Essas variáveis serão passadas como dados de formulário enviados.

      Definir também uma variável de saída **ptoNodePath** que será usada ao definir o Url de resumo.

   1. No **criar resumo PTO** use o **definir valor** para definir os detalhes de entrada em um **nodeProperty**(**nodeProps**).

      As chaves neste mapa devem ser as mesmas que as chaves definidas no renderizador de HTML na etapa anterior.

      Além disso, adicione uma **sling:resourceType** chave com valor **Funcionários/PtoApplication** no mapa.

   1. Usar o subprocesso **storeContent** do **ContentRepositoryConnector** no **criar resumo PTO** processo. Esse subprocesso cria um nó CRX.

      São necessárias três variáveis de entrada:

      * **Caminho da pasta**: O caminho onde o novo nó CRX é criado. Defina o caminho como **/conteúdo**.
      * **Nome do nó**: Atribua a variável de entrada nodeName a este campo. Esta é uma string de nome de nó exclusiva.
      * **Tipo de nó**: Definir o tipo como **nt:unstructured**. A saída desse processo é nodePath. O nodePath é o caminho CRX do nó recém-criado. O ndoePath seria a saída final do **criar PTO** processo de resumo.
   1. Envio dos dados de formulário enviados (**employeeName**, **employeeID**, **ptoReason** e **totalDays**) como entrada no novo processo **criar resumo PTO**. Pegue a saída como **ptoSummaryNodePath**.


1. Defina o Url do resumo como uma expressão XPath contendo os detalhes do servidor junto com **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Na área de trabalho do AEM Forms, ao abrir uma tarefa, o Url de resumo acessa o nó CRX e o renderizador de HTML exibe o resumo.

O layout de resumo pode ser alterado sem modificar o processo. O renderizador de HTML exibe o resumo adequadamente.
