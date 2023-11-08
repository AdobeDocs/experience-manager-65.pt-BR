---
title: Mapeamento personalizado de grupo de usuários no AEM 6.5
seo-title: Custom User Group Mapping in AEM 6.5
description: Saiba como o Mapeamento personalizado de grupo de usuários funciona no Adobe Experience Manager.
seo-description: Lear how Custom User Group Mapping works in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Mapeamento personalizado de grupo de usuários no AEM 6.5 {#custom-user-group-mapping-in-aem}

## Comparação de conteúdo JCR relacionado ao CUG (grupo de usuários personalizado) {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Versões anteriores do AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugEnabled</p> <p>Tipo de nó declarante: N/D, propriedade residual</p> </td>
   <td><p>Autorização:</p> <p>Nó: rep:cugPolicy do tipo de nó rep:CugPolicy</p> <p>Tipo de nó declarante: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autenticação:</p> <p>Tipo de mixin: granite:AuthenticationRequired</p> </td>
   <td><p>Para restringir o acesso de leitura, uma política CUG dedicada é aplicada ao nó de destino.</p> <p>OBSERVAÇÃO: as políticas só podem ser aplicadas nos caminhos com suporte configurados.</p> <p>Os nós com nome rep:cugPolicy e tipo rep:CugPolicy são protegidos e não podem ser gravados usando chamadas de API JCR regulares; use o gerenciamento de controle de acesso JCR.</p> <p>Consulte <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">esta página</a> para obter mais informações.</p> <p>Para aplicar o requisito de autenticação em um nó, é suficiente adicionar o tipo de mixin granite:AuthenticationRequired.</p> <p>OBSERVAÇÃO: respeitado somente abaixo dos caminhos compatíveis configurados.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugPrincipals</p> <p>Tipo de nó declarante: NA, propriedade residual</p> </td>
   <td><p>Propriedade: rep:principalNames</p> <p>Tipo de nó declarante: rep:CugPolicy</p> </td>
   <td><p>A propriedade que contém os nomes dessas entidades de segurança que têm permissão para ler o conteúdo abaixo do CUG restrito está protegida e não pode ser gravada usando chamadas de API JCR regulares; use o gerenciamento de controle de acesso JCR.</p> <p>Consulte <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">esta página</a> para obter mais detalhes sobre a implementação.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugLoginPage</p> <p>Tipo de nó declarante: NA, propriedade residual</p> </td>
   <td><p>Propriedade: granite:loginPath (opcional)</p> <p>Tipo de nó declarante: granite:AuthenticationRequired</p> </td>
   <td><p>Um nó JCR que tem o tipo de mixin granite:AuthenticationRequired definido pode, opcionalmente, definir um caminho de logon alternativo.</p> <p>OBSERVAÇÃO: respeitado somente abaixo dos caminhos compatíveis configurados.</p> </td>
  </tr>
  <tr>
   <td><p>Propriedade: cq:cugRealm</p> <p>Tipo de nó declarante: NA, propriedade residual</p> </td>
   <td>ND</td>
   <td>Não é mais compatível com a nova implementação.</td>
  </tr>
 </tbody>
</table>

## Comparação de serviços OSGi {#comparison-of-osgi-services}

**Versões anteriores do AEM**

Rótulo: Suporte ao grupo de usuários fechado (CUG) do Adobe Granite

Nome: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Rótulo: Configuração do Apache Jackrabbit Oak CUG

  Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

  Política de configuração = OBRIGATÓRIA

* Rótulo: Lista de exclusões do Apache Jackrabbit Oak CUG

  Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

  Política de configuração = OBRIGATÓRIA

* Nome: com.adobe.granite.auth.requirements.impl.RequirementService
* Rótulo: Requisito de autenticação do Adobe Granite e Manipulador de caminho de logon

  Nome: com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler

  Política de configuração = OBRIGATÓRIA

**Comentários**

* Configuração da autorização CUG e habilitar/desabilitar a avaliação.
Serviço para configurar a lista de exclusão de entidades que não devem ser afetadas pela autorização CUG.

  >[!NOTE]
  > 
  >Se a variável `CugExcludeImpl` não estiver configurado, a variável `CugConfiguration` retorna ao padrão.

  É possível conectar uma implementação personalizada do CugExclude se houver necessidades especiais.

* Componente OSGi que implementa o LoginPathProvider que expõe um caminho de logon correspondente ao LoginSelectorHandler. Ela tem uma referência obrigatória a um RequirementHandler, usado para registrar o observador que escuta os requisitos de autenticação alterados armazenados no conteúdo por meio do tipo de mixin granite:AuthenticationRequired.
* Componente OSGi que implementa RequirementHandler que notifica o SlingAuthenticator sobre alterações nos requisitos de autenticação.

  Como a política de configuração desse componente é REQUIRE, ela só será ativada se um conjunto de caminhos compatíveis for especificado.

  A habilitação do serviço inicia o RequirementService.

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
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation if there are special needs.</p> </td>
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
