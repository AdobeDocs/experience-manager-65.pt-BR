---
title: Personalizar a listagem de instâncias de processo
description: Como personalizar as propriedades exibidas na instância do processo no AEM Forms workspace.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 3%

---

# Personalizar a listagem de instâncias de processo {#customizing-the-listing-of-process-instances}

A lista de instâncias de processos é exibida na guia Rastreamento do espaço de trabalho do AEM Forms.

Na lista de instâncias de processos, para cada instância de processo, o espaço de trabalho do AEM Forms mostra algumas propriedades dessa instância. As seguintes propriedades estão disponíveis para cada instância do processo. Essas propriedades são armazenadas como atributos no modelo de componente da instância do processo e estão disponíveis para uso na exibição e no modelo.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>descrição</td>
   <td>Descrição da instância do processo.</td>
  </tr>
  <tr>
   <td>iniciador</td>
   <td>Nome do iniciador da instância do processo.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>ID do iniciador da instância do processo.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Carimbo de data/hora quando o processo é concluído.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID da instância do processo.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Iniciado<br /> 1 = Em execução<br /> 2 = Concluído<br /> 3 = Concluindo<br /> 4 = Terminado<br /> 5 = Encerrando<br /> 6 = Suspenso<br /> 7 = Suspensão<br /> 8 = Cancelando Suspensão</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nome do processo.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Carimbo de data/hora quando o processo foi iniciado.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Matriz de objetos de variáveis de processo. Cada objeto de variável de processo contém <strong>name</strong> (o nome da variável do processo), <strong>value</strong> (valor da variável de processo) e<strong> type</strong> (o tipo de variável de processo).</td>
  </tr>
 </tbody>
</table>

**Exemplo:**

Para exibir a variável `description` da instância do processo no cartão da instância do processo, execute as etapas a seguir.

1. Siga as [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Faça o seguinte:

   1. Copie /libs/ws/js/runtime/templates/processinstance.html para/apps/ws/js/runtime/templates/, se ele não existir. Clique em **Salvar tudo**.
   1. Adicione a descrição do processo div com class = &#39;processDescription&#39; inprocessinstance.html.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Faça o seguinte:

   1. Abra /apps/ws/js/registry.js para edição.
   1. Pesquisar e substituir `text!/lc/libs/ws/js/runtime/templates/processinstance.html`com `text!/lc/`**aplicativos**/ws/js/runtime/templates/processinstance.html.

1. As alterações acima podem exigir uma atualização do arquivo CSS adicionando uma entrada na folha de estilos /apps/ws/css/newStyle.css da seguinte maneira:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement and user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
