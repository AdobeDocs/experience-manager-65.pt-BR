---
title: Mapeamento de grupos de usuários personalizados no AEM 6.5
seo-title: Mapeamento de grupos de usuários personalizados no AEM 6.5
description: Saiba como o Mapeamento personalizado de grupos de usuários funciona em AEM.
seo-description: Saiba como o Mapeamento personalizado de grupos de usuários funciona em AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
translation-type: tm+mt
source-git-commit: c2937a1989c6cfe33cc3f56f89c307cb5fb8d272
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# Mapeamento de grupos de usuários personalizados no AEM 6.5 {#custom-user-group-mapping-in-aem}

## Comparação do conteúdo JCR relacionado ao CUG {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Versões anteriores AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugEnabled</p> <p>A declarar o tipo de nó: N/A, propriedade residual</p> </td>
   <td><p>Autorização:</p> <p>Nó: rep:cugPolicy do tipo de nó rep:CugPolicy</p> <p>A declarar o tipo de nó: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autenticação:</p> <p>Tipo de mistura: granite:AuthenticationRequired</p> </td>
   <td><p>Para restringir o acesso de leitura, uma política de CUG dedicada é aplicada ao nó do público alvo.</p> <p>NOTA: As políticas só podem ser aplicadas nos caminhos suportados configurados.</p> <p>Os nós com o nome rep:cugPolicy e o tipo rep:CugPolicy são protegidos e não podem ser gravados usando chamadas regulares de API JCR; em vez disso, use o gerenciamento de controles de acesso JCR.</p> <p>Consulte <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">esta página</a> para obter mais informações.</p> <p>Para impor o requisito de autenticação em um nó, é suficiente adicionar o tipo de mixin granite:AuthenticationRequired.</p> <p>NOTA: Só respeitado abaixo dos caminhos suportados configurados.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugPrincipals</p> <p>A declarar o tipo de nó: NA, propriedade residual</p> </td>
   <td><p>Propriedade: rep:principalNames</p> <p>A declarar o tipo de nó: rep:CugPolicy</p> </td>
   <td><p>A propriedade que contém os nomes dos principais que têm permissão para ler o conteúdo abaixo do CUG restrito está protegida e não pode ser gravada usando chamadas regulares de API JCR; em vez disso, use o gerenciamento de controles de acesso JCR.</p> <p>Consulte <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">esta página</a> para obter mais detalhes sobre a implementação.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugLoginPage</p> <p>A declarar o tipo de nó: NA, propriedade residual</p> </td>
   <td><p>Propriedade: granite:loginPath (opcional)</p> <p>A declarar o tipo de nó: granite:AuthenticationRequired</p> </td>
   <td><p>Um nó JCR que tenha o tipo de combinação granite:AuthenticationRequired definido pode, opcionalmente, definir um caminho de logon alternativo.</p> <p>NOTA: Só respeitado abaixo dos caminhos suportados configurados.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugRealm</p> <p>A declarar o tipo de nó: NA, propriedade residual</p> </td>
   <td>ND</td>
   <td>Não há mais suporte para a nova implementação.</td>
  </tr>
 </tbody>
</table>

## Comparação de serviços OSGi {#comparison-of-osgi-services}

**Versões anteriores AEM**

Rótulo: Suporte a Adobe Granite Closed User Group (CUG)

Nome: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Rótulo: Configuração do Apache Jackrabbit Oak CUG

   Nome: org.apache.Jackrabbit.oak.spi.security.authorized.cug.impl.CugConfiguration

   ConfigurationPolicy = NECESSÁRIO

* Rótulo: Apache Jackrabbit Oak CUG Excluir Lista

   Nome: org.apache.Jackrabbit.oak.spi.security.license.impl.CugExcludeImpl

   ConfigurationPolicy = NECESSÁRIO

* Nome: com.adobe.granite.auth.requirements.impl.RequirementsService
* Rótulo: Requisito de autenticação do Adobe Granite e manipulador de caminho de logon

   Nome: com.adobe.granite.auth.requirements.impl.DefaultRequirementsHandler

   ConfigurationPolicy = NECESSÁRIO

**Comentários**

* Configuração da autorização do CUG e habilitar/desabilitar a avaliação.
Serviço para configurar a lista de exclusão de principais que não devem ser afetados pela autorização CUG.

   >[!NOTE]
   > 
   >Se o não `CugExcludeImpl` estiver configurado, o `CugConfiguration` reverterá para o padrão.

   É possível conectar uma implementação CugExclude personalizada em caso de necessidades especiais.

* Componente OSGi implementando LoginPathProvider que expõe um caminho de logon correspondente ao LoginSeletorHandler. Ela tem uma referência obrigatória a um RequirementsHandler, que é usado para registrar o observador que escuta as alterações nos requisitos de autenticação armazenados no conteúdo por meio do tipo de mixin granite:AuthenticationRequired.
* Componente OSGi implementando o RequirementsHandler que notifica o SlingAuthenticator sobre alterações nos requisitos de autorização.

   Como a política de configuração para este componente é EXIGIR, ela só será ativada se um conjunto de caminhos suportados for especificado.

   Habilitar o serviço iniciará o RequirementsService.

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

