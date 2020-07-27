---
title: 'Usar metadados em uma notificação por email '
seo-title: 'Usar metadados em uma notificação por email '
description: Usar metadados para preencher informações em uma notificação por email do fluxo de trabalho de formulários
seo-description: Usar metadados para preencher informações em uma notificação por email do fluxo de trabalho de formulários
uuid: 9075b64e-1934-44d5-8b16-aa6e95e93da9
topic-tags: publish
discoiquuid: d48b5137-c866-43cd-925b-7a6a8eac8c0b
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---


# Usar metadados em uma notificação por email {#use-metadata-in-an-email-notification}

Você pode usar a etapa Atribuir Tarefa para criar e atribuir tarefas a um usuário ou grupo. Quando uma tarefa é atribuída a um usuário ou grupo, uma notificação por email é enviada para o usuário definido ou para cada membro do grupo definido. Uma notificação [por](../../forms/using/use-custom-email-template-assign-task-step.md) email típica contém um link da tarefa atribuída e informações relacionadas à tarefa.

Você pode usar metadados em um modelo de email para preencher dinamicamente as informações em uma notificação por email. Por exemplo, o valor do título, a descrição, a data de vencimento, a prioridade, o fluxo de trabalho e a última data na notificação por email a seguir são selecionados dinamicamente no tempo de execução (quando uma notificação por email é gerada).

![Modelo de email padrão](assets/default_email_template_metadata_new.png)

Os metadados são armazenados em pares de valores chave. Você pode especificar a chave no modelo de email e ela é substituída por um valor no tempo de execução (quando uma notificação por email é gerada). Por exemplo, na amostra de código abaixo, &quot;$ {workitem_title} &quot; é uma chave. É substituído pelo valor &quot;Loan-Request&quot; no tempo de execução.

```html
subject=Task Assigned - ${workitem_title}

message=<html><body>\n\
 <table style="width: 480px; font-family: Helvetica, Arial, sans-serif; border: 0; padding: 0; vertical-align: top; text-align: left; word-wrap: break-word; margin: 16px auto; color:#323232; background-color:#FFFCF9; border-collapse: collapse;">\n\
  <tbody>\n\
   <tr>\n\
    <td style="height: 100px; width: 480px; background-color: #FFE0CB; border-top: 5pt solid black; font-family: Helvetica, Arial, sans-serif; font-weight: bold; font-size: 15px; line-height: 20px; padding: 12px; color: #707070;">\n\
      Sample Company\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="font-family: Helvetica, Arial, sans-serif; height: auto; background-color: #FFFCF9; padding: 32px 16px 20px 16px; ">\n\
     <pre style="font-size: 13px; font-family: Helvetica, Arial, sans-serif;  font-weight: normal; color: #323232;"> Hello ${workitem_assignee},\n\
 The following task has been assigned to you:</pre>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="width: 480px;">\n\
     <table style="height: auto; width: 480px; background-color:#FFFBF9; font-family: Helvetica, Arial, sans-serif; border-collapse: collapse;">\n\
      <tbody>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> TITLE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_title}</p>\n\
        </td>\n\
       </tr>\n\
                            <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DESCRIPTION</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_description}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DUE DATE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_due_date}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> PRIORITY</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_priority}</p>\n\
        </td>\n\
       </tr>\n\
       <tr>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> WORKFLOW</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_workflow}</p>\n\
        </td>\n\
       </tr>\n\
      </tbody>\n\
     </table>\n\
    </td>\n\
   </tr>\n\
   <tr style = "text-align: center; vertical-align: middle;">\n\
    <td style="padding:48px 0 72px 0;"> \n\
     <a href="${workitem_url}" target="_blank" style="background-color: #1EBBBB; font-size: 18px; line-height: 25px; font-weight: bold; color: #FFFFFF; text-decoration: none; padding: 15px 15px 15px 15px;">Open Task</a>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="border-top: solid 1px #EDEAE7; padding: 16px;">\n\
     <p><span style="font-size: 12px; font-weight: normal; font-style: italic; color: #919191;">This is an automatically generated email. Please do not reply to this email.</code></p>\n\
    </td>\n\
   </tr>\n\
  </tbody>\n\
 </table>\n\
</body>\n\
</html>\n\
```

## Usar metadados gerados pelo sistema em uma notificação por email {#using-system-generated-metadata-in-an-email-notification}

Um aplicativo AEM Forms fornece várias variáveis de metadados (pares de valores chave) prontos para uso. Você pode usar essas variáveis em um modelo de email. O valor da variável é baseado no aplicativo de formulários associado. A tabela a seguir lista todas as variáveis de metadados disponíveis na caixa:

<table>
 <tbody> 
  <tr> 
   <td>Chave</td> 
   <td>Descrição</td> 
  </tr> 
  <tr> 
   <td>workitem_title</td> 
   <td>Título do aplicativo de formulários associado.</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>URL para acessar o aplicativo de formulários associado.</td> 
  </tr> 
  <tr> 
   <td>workitem_description</td> 
   <td>Descrição do aplicativo de formulários associado.</td> 
  </tr> 
  <tr> 
   <td>workitem_priority</td> 
   <td>Prioridade especificada para o aplicativo de formulários associado.</td> 
  </tr> 
  <tr> 
   <td>workitem_due_date</td> 
   <td>Última data para agir no aplicativo de formulários associado.</td> 
  </tr> 
  <tr> 
   <td>workitem_workflow</td> 
   <td>Nome do fluxo de trabalho associado ao aplicativo de formulários.</td> 
  </tr> 
  <tr> 
   <td>workitem_assign_timestamp</td> 
   <td>Data e hora em que o item de fluxo de trabalho foi atribuído ao destinatário atual.</td> 
  </tr> 
  <tr> 
   <td>workitem_assignee</td> 
   <td>Nome do destinatário presente.</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>URL do servidor do autor. Por exemplo, https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>URL do servidor de publicação. Por exemplo, https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## Usar metadados personalizados em uma notificação por email {#using-custom-metadata-in-an-email-notification}

Você também pode usar metadados personalizados em uma notificação por email. Os metadados personalizados contêm informações além dos metadados gerados pelo sistema. Por exemplo, detalhes de política recuperados de um banco de dados. Você pode usar um pacote ECMAScript ou OSGi para adicionar metadados personalizados no repositório crx:

### Usar o ECMAScript para adicionar metadados personalizados  {#use-ecmascript-to-add-custom-metadata}

[O ECMAScript](https://en.wikipedia.org/wiki/ECMAScript) é uma linguagem de script. É usado para aplicativos de servidor e scripts do cliente. Execute as seguintes etapas para usar o ECMAScript para adicionar metadados personalizados para um modelo de email:

1. Faça logon no CRX DE com uma conta administrativa. O URL é https://&#39;[server]:[port]&#39;/crx/de/index.jsp

1. Navegue até /apps/fd/painel/scripts/metadataScripts. Crie um arquivo com a extensão .ecma. Por exemplo, usermetadata.ecma

   Se o caminho mencionado acima não existir, crie-o.

1. Adicione o código ao arquivo .ecma que tem a lógica de gerar metadados personalizados em pares de valores chave. Por exemplo, o código ECMAScript a seguir gera metadados personalizados para uma política de seguro:

   ```javascript
   function getUserMetaData()  {
       //Commented lines below provide an overview on how to set user metadata in map and return it.
       var HashMap = Packages.java.util.HashMap;
       var valuesMap = new HashMap();
       valuesMap.put("policyNumber", "2017568972695");
       valuesMap.put("policyHolder", "Adobe Systems");
   
       return valuesMap;
   }
   ```

1. Clique em Salvar tudo. Agora, o script está disponível para seleção no modelo de fluxo de trabalho do AEM.

   ![atribuir metadados-tarefa](assets/assigntask-metadata.png)

1. (Opcional) Especifique o título do script:

   Se você não especificar o título, o campo Metadados personalizados exibirá o caminho completo do arquivo ECMAScript. Execute as seguintes etapas para especificar um título significativo para o script:

   1. Expanda o nó de script, clique com o botão direito do mouse no nó **[!UICONTROL jcr:content]** e clique em **[!UICONTROL Mixins]**.
   1. Digite mix:título na caixa de diálogo Editar misturas e clique em **+**.
   1. Adicione uma propriedade com os seguintes valores.

      | Nome | jcr:title |
      |---|---|
      | Tipo | Sequência de caracteres |
      | Valor | Especifique o título do script. Por exemplo, metadados personalizados para o detentor da política. O valor especificado é exibido na etapa de atribuição de tarefa. |

### Usar um pacote OSGi e uma interface Java para adicionar metadados personalizados {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

Você pode usar a interface Java WorkitemUserMetadataService para adicionar metadados personalizados para modelos de email. Você pode criar um pacote OSGi que usa a interface Java WorkitemUserMetadataService e implantá-lo no servidor AEM Forms. Disponibiliza os metadados para seleção na etapa Atribuir Tarefa.

Para criar um pacote OSGi com interface Java, adicione arquivos jar e jar jar [granite do SDK](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) do cliente [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) AEM Forms como dependências externas ao projeto de pacote OSGi. Você pode usar qualquer Java IDE para criar um pacote OSGi. O procedimento a seguir fornece etapas para usar o Eclipse para criar um pacote OSGi:

1. Abra o Eclipse IDE. Navegue até Arquivo > Novo projeto.

1. Na tela Selecionar um assistente, selecione Projeto Maven e clique em Avançar.

1. No projeto New Maven, mantenha os padrões e clique em Next (Avançar). Selecione um arquétipo e clique em Avançar. Por exemplo, maven-archetype-quickstart. Especifique Id de grupo, Id de artefato, versão e pacote para o projeto e clique em Concluir. O projeto é criado.

1. Abra o arquivo pom.xml para edição e substitua todo o conteúdo do arquivo pelo seguinte:

1. Adicione o código fonte que usa a interface Java WorkitemUserMetadataService para adicionar metadados personalizados para modelos de email. Um código de exemplo está listado abaixo:

   ```java
   package com.aem.impl;
   
   import com.adobe.fd.workspace.service.external.WorkitemUserMetadataService;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Properties;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.osgi.framework.Constants;
   
   import java.util.HashMap;
   import java.util.Map;
   
   @Component
   @Service
   @Properties({
           @Property(name = Constants.SERVICE_DESCRIPTION, value = "A sample implementation of a user metadata service."),
           @Property(name = WorkitemUserMetadataService.SERVICE_PROPERTY_LABEL, value = "Default User Metadata Service")})
   
   public class WorkitemUserMetadataServiceImpl
     implements WorkitemUserMetadataService
   {
     public WorkitemUserMetadataServiceImpl() {}
   
     public Map<String, String> getUserMetadataMap()
     {
       HashMap<String, String> metadataMap = null;
       metadataMap = new HashMap();
       metadataMap.put("test_metadata", "tested-interface implementation");
       return metadataMap;
     }
   }
   ```

1. Abra um prompt de comando e navegue até o diretório que contém o projeto do pacote OSGi. Use o seguinte comando para criar o pacote OSGi:

   `mvn clean install`

1. Carregue o pacote em um servidor AEM Forms. Você pode usar o Gerenciador de pacotes de AEM para importar o pacote para o servidor AEM Forms.

Depois que o pacote é importado, você pode selecionar os metadados na etapa Atribuir Tarefa e usá-los como modelo de email.
