---
title: Gerenciamento de tarefas em uma hierarquia organizacional usando a Visualização do Gerenciador
seo-title: Managing tasks in an organizational hierarchy using Manager View
description: Como os gerentes e chefes de organização podem acessar e trabalhar nas tarefas de seus relatórios diretos e indiretos na guia Tarefas no espaço de trabalho do AEM Forms.
seo-description: How managers and organization heads can access and work on the tasks of their direct and indirect reports in the To-do tab in AEM Forms workspace.
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
exl-id: e50974a7-01ac-4a08-bea2-df9cc975c69e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Gerenciamento de tarefas em uma hierarquia organizacional usando a Visualização do Gerenciador{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

Na área de trabalho do AEM Forms, os gerentes agora podem acessar as tarefas atribuídas a qualquer pessoa em sua hierarquia (relatórios diretos ou indiretos) e executar várias ações com eles. As tarefas estão disponíveis na guia To-do no espaço de trabalho do AEM Forms. As ações apoiadas nas tarefas dos relatórios diretos são:

**Avançar** Encaminhe uma tarefa do relatório direto para qualquer usuário.

**Reclamação** Reivindica uma tarefa de relatório direto.

**Reivindicação e abertura** Reivindica uma tarefa de um relatório direto e o abre automaticamente na lista De Tarefas do gerente.

**Rejeitar** Rejeitar uma tarefa encaminhada a um relatório direto por algum outro usuário. Essa opção está disponível para as tarefas encaminhadas por outros usuários a um relatório direto.

O AEM Forms restringe o acesso de um usuário somente às tarefas para as quais o usuário tem controle de acesso (ACL). Essa verificação garante que um usuário possa buscar apenas as tarefas nas quais o usuário tem permissões de acesso. Usando serviços e implementações da Web de terceiros para definir a hierarquia, uma organização pode personalizar a definição de gerente e relatórios diretos para atender às suas necessidades.

1. Crie um DSC. Para obter mais informações, consulte o tópico &quot;Desenvolvimento de componentes para AEM Forms&quot; em [Programação com o AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) guia.
1. No DSC, defina um novo SPI para o gerenciamento de hierarquia para definir relatórios diretos e hierarquia dentro dos usuários do AEM Forms. A seguir, há um exemplo de trecho de código Java™.

   ```java
   public class MyHierarchyMgmtService
   {
        /*
       Input : Principal Oid for a livecycle user
       Output : Returns true when the user is either the service invoker OR his direct/indirect report.
       */
       boolean isInHierarchy(String principalOid) {
   
       }
   
       /*
       Input : Principal Oid for a livecycle user
       Output : List of principal Oids for direct reports of the livecycle user
       A user may get direct reports only for himself OR his direct/indirect reports.
       So the API is functionally equivalent to -
       isInHierarchy(principalOid) ? <return direct reports> : <return empty list>
       */
       List<String> getDirectReports(String principalOid) {
   
       }
   
       /*
       Returns whether a livecycle user has direct reports or not.
       It's functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. Crie um arquivo component.xml. Certifique-se de que a spec-id deve ser a mesma mostrada no trecho de código abaixo. A seguir, há um trecho de código de amostra que pode ser redefinido.

   ```xml
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.SampleDSC</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
         <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
         <services>
           <service name="MyHierarchyMgmtService" title="My hierarchy management service" orchestrateable="false">
           <auto-deploy service-id="MyHierarchyMgmtService" category-id="Sample DSC" major-version="1" minor-version="0" />
           <description>Service for resolving hierarchy management.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.HierarchyManagementProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.hierarchymanagement.MyHierarchyMgmtService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="true" name="isInHierarchy" method="isInHierarchy">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               <operation anonymous-access="true" name="getDirectReports" method="getDirectReports">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.util.List"/>
               </operation>
               <operation anonymous-access="true" name="isManager" method="isManager">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               </operations>
               </service>
         </services>
   </component>
   ```

1. Implante o DSC por meio do Workbench. Reiniciar `ProcessManagementTeamTasksService` serviço.
1. Talvez seja necessário atualizar seu navegador ou fazer logout/login com o usuário novamente.

A tela a seguir ilustra o acesso às tarefas dos relatórios diretos e às ações disponíveis.

![cu_manager_view](assets/cu_manager_view.png)

Acesse as tarefas dos relatórios diretos e execute as tarefas
