---
title: Mapeamento de grupo de usuários personalizado no AEM 6.5
seo-title: Mapeamento de grupo de usuários personalizado no AEM 6.5
description: Saiba como o Mapeamento de grupo de usuários personalizado funciona no AEM.
seo-description: Saiba como o Mapeamento de grupo de usuários personalizado funciona no AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Segurança
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---

# Mapeamento de grupo de usuários personalizado no AEM 6.5 {#custom-user-group-mapping-in-aem}

## Comparação do conteúdo do JCR relacionado ao CUG {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Versões AEM mais antigas</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugEnabled</p> <p>Declarando tipo de nó: N/A, propriedade residual</p> </td>
   <td><p>Autorização:</p> <p>Nó: rep:cugPolicy do tipo de nó rep:CugPolicy</p> <p>Declarando tipo de nó: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autenticação:</p> <p>Tipo de mistura: granite:AuthenticationRequired</p> </td>
   <td><p>Para restringir o acesso de leitura, uma política CUG dedicada é aplicada ao nó de destino.</p> <p>OBSERVAÇÃO: As políticas só podem ser aplicadas nos caminhos compatíveis configurados.</p> <p>Os nós com o nome rep:cugPolicy e tipo rep:CugPolicy são protegidos e não podem ser gravados usando chamadas de API JCR comuns; em vez disso, use o gerenciamento de controle de acesso JCR.</p> <p>Consulte <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">esta página</a> para obter mais informações.</p> <p>Para impor o requisito de autenticação em um nó, é suficiente adicionar o tipo mixin granite:AuthenticationRequired.</p> <p>OBSERVAÇÃO: Apenas respeitado abaixo dos caminhos compatíveis configurados.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugPrincipals</p> <p>Declarando tipo de nó: NA, propriedade residual</p> </td>
   <td><p>Propriedade: rep:principalNames</p> <p>Declarando tipo de nó: rep:CugPolicy</p> </td>
   <td><p>A propriedade que contém os nomes dos principais que têm permissão para ler o conteúdo abaixo do CUG restrito está protegida e não pode ser gravada usando chamadas de API JCR regulares; em vez disso, use o gerenciamento de controle de acesso JCR.</p> <p>Consulte <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">esta página</a> para obter mais detalhes sobre a implementação.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugLoginPage</p> <p>Declarando tipo de nó: NA, propriedade residual</p> </td>
   <td><p>Propriedade: granite:loginPath (opcional)</p> <p>Declarando tipo de nó: granite:AuthenticationRequired</p> </td>
   <td><p>Um nó JCR que tenha o tipo mixin granite:AuthenticationRequired definido, pode definir opcionalmente um caminho de logon alternativo.</p> <p>OBSERVAÇÃO: Apenas respeitado abaixo dos caminhos compatíveis configurados.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugRealm</p> <p>Declarando tipo de nó: NA, propriedade residual</p> </td>
   <td>ND</td>
   <td>Não há mais suporte para a nova implementação.</td>
  </tr>
 </tbody>
</table>

## Comparação de serviços OSGi {#comparison-of-osgi-services}

**Versões AEM mais antigas**

Rótulo: Suporte para CUG (Adobe Granite Closed User Group)

Nome: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Rótulo: Configuração do Apache Jackrabbit Oak CUG

   Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy = OBRIGATÓRIO

* Rótulo: Lista de exclusões do Apache Jackrabbit Oak CUG

   Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy = OBRIGATÓRIO

* Nome: com.adobe.granite.auth.requirements.impl.RequirementsService
* Rótulo: Requisito de autenticação do Adobe Granite e manipulador de caminho de logon

   Nome: com.adobe.granite.auth.requirements.impl.DefaultRequirementsHandler

   ConfigurationPolicy = OBRIGATÓRIO

**Comentários**

* Configuração da autorização do CUG e ativação/desativação da avaliação.
Serviço para configurar a lista de exclusão de entidades principais que não devem ser afetadas pela autorização do CUG.

   >[!NOTE]
   > 
   >Se `CugExcludeImpl` não estiver configurado, o `CugConfiguration` voltará ao padrão.

   É possível plug-in de uma implementação CugExclude personalizada em caso de necessidades especiais.

* Componente OSGi implementando LoginPathProvider que expõe um caminho de logon correspondente para LoginSelectorHandler. Ela tem uma referência obrigatória a um RequerHandler, que é usada para registrar o observador que escuta os requisitos de autenticação alterados armazenados no conteúdo por meio do tipo mixin granite:AuthenticationRequired .
* Componente OSGi implementando o RequirementsHandler que notifica o SlingAuthenticator sobre alterações a requisitos autorais.

   Como a política de configuração para este componente é REQUIRE, ela só será ativada se um conjunto de caminhos suportados for especificado.

   Habilitar o serviço iniciará o RequerimentoService.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
