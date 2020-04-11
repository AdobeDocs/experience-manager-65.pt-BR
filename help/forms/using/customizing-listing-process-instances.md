---
title: Personalização da lista de instâncias de processo
seo-title: Personalização da lista de instâncias de processo
description: Como personalizar as propriedades exibidas na instância do processo na área de trabalho do AEM Forms.
seo-description: Como personalizar as propriedades exibidas na instância do processo na área de trabalho do AEM Forms.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Personalização da lista de instâncias de processo {#customizing-the-listing-of-process-instances}

A lista da instância do processo é exibida na guia Rastreamento da área de trabalho do AEM Forms.

Na lista da instância do processo, para cada instância do processo, a área de trabalho do AEM Forms mostra algumas propriedades dessa instância. As seguintes propriedades estão disponíveis para cada instância do processo. Essas propriedades são armazenadas como atributos no modelo de componente da instância do processo e estão disponíveis para uso em sua visualização e modelo.

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
   <td>Carimbo de data e hora quando o processo foi concluído.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID da instância do processo.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Iniciado<br /> 1 = Executando<br /> 2 = Concluído<br /> 3 = Concluindo<br /> 4 = Terminado<br /> 5 = Finalizando<br /> 6 = Suspenso<br /> 7 = Suspendendo<br /> 8 = Cancelando a suspensão</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nome do processo.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Carimbo de data e hora quando o processo começou.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Matriz de objetos de variáveis de processo. Cada objeto de variável de processo contém <strong>nome</strong> (o nome da variável de processo), <strong>valor</strong> (o valor da variável de processo) e tipo<strong></strong> (o tipo de variável de processo).</td>
  </tr>
 </tbody>
</table>

**Exemplo:**

Para exibir a `description` propriedade da instância do processo no cartão de instância do processo, execute as seguintes etapas.

1. Siga as etapas [genéricas para personalização](/help/forms/using/generic-steps-html-workspace-customization.md)da área de trabalho do AEM Forms.
1. Faça o seguinte:

   1. Copie /libs/ws/js/runtime/templates/processinstance.html para/apps/ws/js/runtime/models/, se ele não existir. Clique em **Salvar tudo**.
   1. Adicione div de descrição do processo com class = &#39;processDescription&#39; inprocessinstance.html.

   ```
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Faça o seguinte:

   1. Abra /apps/ws/js/registry.js para edição.
   1. Pesquise e substitua `text!/lc/libs/ws/js/runtime/templates/processinstance.html`por `text!/lc/`**aplicativos **/ws/js/runtime/templates/processinstance.html.

1. As alterações acima podem exigir uma atualização do arquivo CSS, adicionando uma entrada na folha de estilos /apps/ws/css/newStyle.css da seguinte maneira:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
