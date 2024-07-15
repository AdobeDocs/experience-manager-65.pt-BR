---
title: Gerenciando tarefas em uma hierarquia organizacional usando a Exibição do Gerente
description: Como os gerentes e chefes de organização podem acessar e trabalhar nas tarefas de seus relatórios diretos e indiretos na guia Tarefas no espaço de trabalho do AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: e50974a7-01ac-4a08-bea2-df9cc975c69e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Gerenciando tarefas em uma hierarquia organizacional usando a Exibição do Gerente{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

No espaço de trabalho do AEM Forms, os gerentes agora podem acessar as tarefas atribuídas a qualquer pessoa em sua hierarquia — relatórios diretos ou indiretos — e executar várias ações neles. As tarefas estão disponíveis na guia Tarefa no espaço de trabalho do AEM Forms. As ações compatíveis com as tarefas de subordinados diretos são:

**Encaminhar** - Encaminhar uma tarefa do subordinado direto para qualquer usuário.

**Declaração** - Reclamar uma tarefa de um subordinado direto.

**Reclamação e Abertura** - Reclamar uma tarefa de um subordinado direto e abri-la automaticamente na lista de tarefas pendentes do gerente.

**Rejeitar** - Rejeita uma tarefa encaminhada a um subordinado direto por algum outro usuário. Essa opção está disponível para as tarefas encaminhadas por outros usuários a um subordinado direto.

O AEM Forms restringe o acesso de um usuário somente às tarefas para as quais o usuário tem controle de acesso (ACL). Essa verificação garante que um usuário possa buscar somente as tarefas nas quais tem permissões de acesso. Usando serviços da Web e implementações de terceiros para definir a hierarquia, uma organização pode personalizar a definição de gerente e subordinados diretos para atender às suas necessidades.

1. Crie um DSC. Para obter mais informações, consulte o tópico &quot;Desenvolvendo componentes para o AEM Forms&quot; no guia [Programação com o AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).
1. No DSC, defina uma nova SPI para gerenciamento de hierarquia para definir subordinados diretos e hierarquia dentro dos usuários do AEM Forms. Veja a seguir um exemplo de trecho de código Java™.

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
       It is functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. Crie um arquivo component.xml. Certifique-se de que a spec-id seja a mesma mostrada no trecho de código abaixo. Este é um exemplo de trecho de código que você pode redefinir.

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

1. Implante o DSC por meio do Workbench. Reinicie o serviço `ProcessManagementTeamTasksService`.
1. Talvez seja necessário atualizar o navegador ou fazer logout/logon com o usuário novamente.

A tela a seguir ilustra o acesso às tarefas de subordinados diretos e às ações disponíveis.

![cu_manager_view](assets/cu_manager_view.png)

Acessar tarefas de subordinados diretos e agir nas tarefas
