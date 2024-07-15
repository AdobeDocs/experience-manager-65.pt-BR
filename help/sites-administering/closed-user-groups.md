---
title: Grupos de Usuários Fechados no AEM
description: Saiba mais sobre Grupos de usuários fechados e os benefícios que eles trazem à escalabilidade e segurança no AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '6650'
ht-degree: 0%

---

# Grupos de Usuários Fechados no AEM{#closed-user-groups-in-aem}

## Introdução {#introduction}

Desde o AEM 6.3, há uma nova implementação de Grupo de usuários fechado destinada a abordar os problemas de desempenho, escalabilidade e segurança presentes na implementação existente.

>[!NOTE]
>
>Por uma questão de simplicidade, a abreviação CUG é usada em toda esta documentação.

O objetivo da nova implementação é cobrir a funcionalidade existente, onde necessário, enquanto lida com problemas e limitações de design de versões mais antigas. O resultado é um novo design CUG com as seguintes características:

* Separação clara dos elementos de autenticação e autorização, que podem ser utilizados individualmente ou em combinação;
* Modelo de autorização dedicado para refletir o acesso de leitura restrito nas árvores CUG configuradas sem interferir em outros requisitos de configuração e permissão de controle de acesso;
* Separação entre a configuração do controle de acesso do acesso de leitura restrito, que é necessário nas instâncias de criação, e a avaliação de permissão que só é desejada na publicação;
* Edição de acesso de leitura restrito sem escalonamento de privilégio;
* Extensão dedicada do tipo de nó para marcar o requisito de autenticação;
* Caminho de logon opcional associado ao requisito de autenticação.

### A nova implementação do grupo de usuários personalizado {#the-new-custom-user-group-implementation}

Um CUG, como é conhecido no contexto do AEM, consiste nas seguintes etapas:

* Restrinja o acesso de leitura na árvore que deve ser protegida e permita somente leitura para entidades de segurança que estejam listadas com uma determinada instância CUG ou excluídas da avaliação CUG completamente. Isso é chamado de elemento **authorization**.
* Imponha a autenticação em uma determinada árvore e, opcionalmente, especifique uma página de logon dedicada para essa árvore que será excluída. Isso é chamado de elemento **authentication**.

A nova implementação foi projetada para definir uma linha entre os elementos de autenticação e autorização. A partir do AEM 6.3, é possível restringir o acesso de leitura sem adicionar explicitamente um requisito de autenticação. Por exemplo, se uma determinada instância exigir autenticação completa ou se uma determinada árvore já estiver em uma subárvore que requer autenticação.

Da mesma forma, uma determinada árvore pode ser marcada com um requisito de autenticação sem alterar a configuração de permissão efetiva. As combinações e os resultados são listados na seção [Combinando Políticas CUG e o Requisito de Autenticação](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement).

## Visão geral {#overview}

### Autorização: Restrição do acesso de leitura {#authorization-restricting-read-access}

O recurso principal de um CUG está restringindo o acesso de leitura em uma determinada árvore no repositório de conteúdo para todos, exceto entidades selecionadas. Em vez de manipular o conteúdo de controle de acesso padrão dinamicamente, a nova implementação adota uma abordagem diferente, definindo um tipo dedicado de política de controle de acesso que representa um CUG.

#### Política de controle de acesso para CUG {#access-control-policy-for-cug}

Esse novo tipo de política tem as seguintes características:

* Política de controle de acesso do tipo org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (definida pela API Apache Jackrabbit);
* PrincipalSetPolicy concede privilégios a um conjunto modificável de principais;
* Os privilégios concedidos e o escopo da política são um detalhe de implementação.

A implementação de PrincipalSetPolicy usada para representar CUGs também define que:

* As políticas CUG só concedem acesso de leitura a itens JCR comuns (por exemplo, o conteúdo de controle de acesso é excluído);
* O escopo é definido pelo nó controlado por acesso que mantém a política CUG;
* Políticas CUG podem ser aninhadas, um CUG aninhado inicia um novo CUG sem herdar o conjunto principal do CUG &#39;pai&#39;;
* O efeito da política, se a avaliação estiver ativada, é herdado para toda a subárvore até o próximo CUG aninhado.

Essas políticas CUG são implantadas em uma instância AEM por meio de um módulo de autorização separado chamado oak-authorization-cug. Este módulo vem com seu próprio gerenciamento de controle de acesso e avaliação de permissão. Em outras palavras, a configuração padrão do AEM envia uma configuração do repositório de conteúdo do Oak que combina vários mecanismos de autorização. Para obter mais informações, consulte [esta página na Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Nesta configuração composta, um novo CUG não substitui o conteúdo de controle de acesso existente anexado ao nó de destino. Em vez disso, é um suplemento que também pode ser removido posteriormente sem afetar o controle de acesso original, que por padrão no AEM seria uma lista de controle de acesso.

Ao contrário da implementação anterior, as novas políticas CUG são sempre reconhecidas e tratadas como conteúdo de controle de acesso. Isso implica que eles são criados e editados usando a API de gerenciamento de controle de acesso JCR. Para obter mais informações, consulte a seção [Gerenciando Políticas CUG](#managing-cug-policies).

#### Avaliação de Permissão de Políticas CUG {#permission-evaluation-of-cug-policies}

Além de um gerenciamento de controle de acesso dedicado para CUGs, o novo modelo de autorização permite que você ative condicionalmente a avaliação de permissões para suas políticas. Isso permite configurar políticas CUG em um ambiente de preparo e permite a avaliação das permissões efetivas apenas depois de replicadas no ambiente de produção.

A avaliação de permissão para políticas CUG e a interação com o modelo de autorização padrão ou adicional seguem o padrão projetado para vários mecanismos de autorização no Apache Jackrabbit Oak. Ou seja, um determinado conjunto de permissões será concedido se e somente se todos os modelos concederem acesso. Consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) para obter mais detalhes.

As seguintes características se aplicam à avaliação de permissão associada ao modelo de autorização criado para manipular e avaliar as políticas CUG:

* Ela só lida com permissões de leitura para nós e propriedades regulares, mas não lida com o conteúdo de controle de acesso
* Ele não lida com permissões de gravação nem com qualquer tipo de permissão necessária para a modificação de conteúdo JCR protegido (controle de acesso, informações de tipo de nó, controle de versão, bloqueio ou gerenciamento de usuários, entre outros). Essas permissões não são afetadas por uma política CUG e não serão avaliadas pelo modelo de autorização associado. O fato de essas permissões serem concedidas depende dos outros modelos configurados na configuração de segurança.

O efeito de uma única política CUG na avaliação da permissão pode ser resumido da seguinte maneira:

* O acesso de leitura é negado para todos, exceto para assuntos que contenham entidades principais ou entidades principais excluídas listadas na política;
* A política produz efeitos no nó controlado por acesso que detém a política e as suas propriedades;
* O efeito também é herdado abaixo da hierarquia - ou seja, a árvore de itens definida pelo nó controlado por acesso;
* No entanto, não afeta irmãos nem ancestrais do nó controlado por acesso;
* A herança de um determinado CUG é interrompida em um CUG aninhado.

#### Práticas recomendadas {#best-practices}

As seguintes práticas recomendadas devem levar em conta a definição de acesso de leitura restrito por meio de CUGs:

* Tome uma decisão consciente sobre se sua necessidade de um CUG é sobre a restrição do acesso de leitura ou um requisito de autenticação. Se este último, ou se houver necessidade de ambos, consulte a seção sobre Práticas recomendadas para obter detalhes sobre o requisito de autenticação
* Crie um modelo de ameaça para os dados ou conteúdo que devem ser protegidos para identificar limites de ameaça e obter uma visão clara sobre a confidencialidade dos dados e as funções associadas ao acesso autorizado
* Modelar o conteúdo do repositório e os CUGs tendo em mente os aspectos gerais relacionados à autorização e as práticas recomendadas:

   * Lembre-se de que a permissão de leitura só é concedida se um determinado CUG e a avaliação de outros módulos implantados na concessão de configuração permitirem que um determinado sujeito leia um determinado item do repositório
   * Evite criar CUGs redundantes em que o acesso de leitura já esteja restrito por outros módulos de autorização
   * A necessidade excessiva de CUGs aninhados pode potencialmente destacar problemas no design de conteúdo
   * A necessidade excessiva de CUGs (por exemplo, em cada página) pode indicar a necessidade de um modelo de autorização personalizado potencialmente mais adequado para atender às necessidades específicas de segurança do aplicativo e do conteúdo em questão.

* Limite os caminhos compatíveis com políticas CUG a algumas árvores no repositório para permitir um desempenho otimizado. Por exemplo, permita apenas CUGs abaixo do nó /content como enviado como o valor padrão desde o AEM 6.3.
* As políticas CUG são projetadas para conceder acesso de leitura a um pequeno conjunto de princípios. A necessidade de um grande número de princípios pode destacar problemas no design de conteúdo ou aplicativo e deve ser reconsiderada.

### Autenticação: definição do requisito de autenticação {#authentication-defining-the-auth-requirement}

As partes relacionadas à autenticação do recurso CUG permitem marcar árvores que exigem autenticação e, opcionalmente, especificar uma página de logon dedicada. De acordo com a versão anterior, a nova implementação permite marcar árvores que exigem autenticação no repositório de conteúdo. Ela também habilita condicionalmente a sincronização com o `Sling org.apache.sling.api.auth.Authenticator`responsável por aplicar o requisito e redirecionar para um recurso de logon.

Esses requisitos são registrados com o Autenticador por um serviço OSGi que fornece a propriedade de registro `sling.auth.requirements`. Essas propriedades são usadas para estender dinamicamente os requisitos de autenticação. Para obter mais detalhes, consulte a [documentação do Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definição do requisito de autenticação com um tipo de mixin dedicado {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Por motivos de segurança, a nova implementação substitui o uso de uma propriedade JCR residual por um tipo de mixin dedicado chamado `granite:AuthenticationRequired`, que define uma única propriedade opcional do tipo STRING para o caminho de logon `granite:loginPath`. Somente as alterações de conteúdo relacionadas a esse tipo de mixin levam a uma atualização dos requisitos registrados no Apache Sling Authenticator. As modificações são rastreadas após a persistência de quaisquer modificações transitórias e, portanto, exigem uma chamada `javax.jcr.Session.save()` para se tornarem efetivas.

O mesmo se aplica à propriedade `granite:loginPath`. Somente é respeitado se for definido pelo tipo de mixin relacionado ao requisito de autenticação. Adicionar uma propriedade residual com esse mesmo nome em um nó JCR não estruturado não mostra o efeito desejado e a propriedade é ignorada pelo manipulador responsável pela atualização do registro OSGi.

>[!NOTE]
>
>A definição da propriedade do caminho de logon é opcional e necessária somente se a árvore que requer autenticação não puder voltar para a página de logon padrão ou herdada de outra forma. Consulte a [Avaliação do Caminho de Logon](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) abaixo.

#### Registrando o requisito de autenticação e o caminho de logon no Sling Authenticator {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Como esse tipo de requisito de autenticação deve ser limitado a determinados modos de execução e a um pequeno subconjunto de árvores no repositório de conteúdo, o rastreamento do tipo de mixin do requisito e das propriedades do caminho de logon é condicional. E está vinculado a uma configuração correspondente que define os caminhos compatíveis (consulte Opções de configuração abaixo). Portanto, somente as alterações no escopo desses caminhos compatíveis acionam uma atualização do registro OSGi, em outro lugar, o tipo de mixin e a propriedade são ignorados.

A configuração padrão do AEM agora usa essa configuração, permitindo definir o mixin no modo de execução do autor, mas apenas tem efeito após a replicação para a instância de publicação. Consulte [esta página](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) para obter detalhes sobre como o Sling impõe o requisito de autenticação.

Adicionar o tipo de mixin `granite:AuthenticationRequired` nos caminhos com suporte configurados faz com que o registro OSGi do manipulador responsável seja atualizado contendo uma entrada nova e adicional com a propriedade `sling.auth.requirements`. Se um determinado requisito de autenticação especificar a propriedade `granite:loginPath` opcional, o valor também será registrado com o Autenticador com um prefixo &#39;-&#39; a ser excluído do requisito de autenticação.

#### Avaliação e herança do requisito de autenticação {#evaluation-and-inheritance-of-the-authentication-requirement}

Os requisitos de autenticação do Apache Sling são herdados por meio da página ou da hierarquia de nós. Os próprios detalhes da herança e a avaliação dos requisitos de autenticação, como ordem e precedência, são considerados um detalhe de implementação e não serão documentados neste artigo.

#### Avaliação do caminho de login {#evaluation-of-login-path}

A avaliação do caminho de logon e o redirecionamento para o recurso correspondente na autenticação são um detalhe de implementação do Manipulador de autenticação do seletor de logon do Adobe Granite ( `com.day.cq.auth.impl.LoginSelectorHandler`), que é um Apache Sling AuthenticationHandler configurado com AEM por padrão.

Chamando `AuthenticationHandler.requestCredentials`, esse manipulador tenta determinar a página de logon de mapeamento para a qual o usuário é redirecionado. Isso inclui as seguintes etapas:

* Faça a distinção entre senha expirada e necessidade de logon regular como motivo para o redirecionamento;
* Se um logon regular, testa se um caminho de logon pode ser obtido na seguinte ordem:

   * do LoginPathProvider conforme implementado pelo novo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * da implementação CUG antiga e obsoleta,
   * nos Mapeamentos da Página de Logon, conforme definido com o `LoginSelectorHandler`,
   * e, finalmente, volte para a Página de Logon Padrão, conforme definido com o `LoginSelectorHandler`.

* Quando um caminho de logon válido é obtido por meio das chamadas listadas acima, a solicitação do usuário é redirecionada para essa página.

O alvo desta documentação é a avaliação do caminho de logon conforme exposto pela interface interna `LoginPathProvider`. A implementação enviada desde o AEM 6.3 se comporta da seguinte maneira:

* O registro de caminhos de logon depende da distinção entre a senha expirada e a necessidade de logon regular como motivo para o redirecionamento
* Se um logon regular, testa se um caminho de logon pode ser obtido na seguinte ordem:

   * do `LoginPathProvider` conforme implementado pelo novo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * da implementação CUG antiga e obsoleta,
   * nos Mapeamentos da Página de Logon conforme definido com o `LoginSelectorHandler`,
   * e, finalmente, voltar para a Página de Logon Padrão, conforme definido com o `LoginSelectorHandler`.

* Quando um caminho de logon válido é obtido por meio das chamadas listadas acima, a solicitação do usuário é redirecionada para essa página.

O `LoginPathProvider` conforme implementado pelo novo suporte de requisito de autenticação no Granite expõe os caminhos de logon conforme definido pelas propriedades `granite:loginPath`, que por sua vez são definidas pelo tipo de mixin conforme descrito acima. O mapeamento do caminho do recurso que contém o caminho de logon e o próprio valor da propriedade é mantido na memória e é avaliado para localizar um caminho de logon adequado para outros nós na hierarquia.

>[!NOTE]
>
>A avaliação só é executada para solicitações associadas a recursos que estão localizados com nos caminhos compatíveis configurados. Para quaisquer outras solicitações, as maneiras alternativas de determinar o caminho de logon serão avaliadas.

#### Práticas recomendadas {#best-practices-1}

As seguintes práticas recomendadas devem ser consideradas ao definir os requisitos de autenticação:

* Evite aninhar requisitos de autenticação: a inserção de um único marcador de requisito de autenticação no início de uma árvore deve ser suficiente e ser herdada para toda a subárvore definida pelo nó de destino. Os requisitos de autenticação adicionais nessa árvore devem ser considerados redundantes e podem levar a problemas de desempenho ao avaliar o requisito de autenticação no Apache Sling. Com a separação das áreas CUG relacionadas à autorização e autenticação, é possível restringir o acesso de leitura por CUG ou outros tipos de políticas enquanto impõe a autenticação para toda a árvore.
* O conteúdo do repositório de modelo é tal que os requisitos de autenticação se aplicam a toda a árvore, sem a necessidade de excluir subárvores aninhadas do requisito novamente.
* Para evitar especificar e, em seguida, registrar caminhos de logon redundantes:

   * dependem da herança e evitam definir caminhos de logon aninhados,
   * não defina o caminho de logon opcional para um valor que corresponda ao padrão ou a um valor herdado,
   * os desenvolvedores de aplicativos devem identificar quais caminhos de logon devem ser configurados nas configurações de caminho de logon global (padrão e mapeamentos) associadas ao `LoginSelectorHandler`.

## Representação no repositório {#representation-in-the-repository}

### Representação de política CUG no repositório {#cug-policy-representation-in-the-repository}

A documentação do Oak aborda a forma como as novas políticas CUG são refletidas no conteúdo do repositório. Para obter mais informações, consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Requisito de autenticação no repositório {#authentication-requirement-in-the-repository}

A necessidade de um requisito de autenticação separado é refletida no conteúdo do repositório com um tipo de nó de mixin dedicado colocado no nó de destino. O tipo de mixin define uma propriedade opcional para especificar uma página de logon dedicada para a árvore definida pelo nó de destino.

A página associada ao caminho de logon pode estar localizada dentro ou fora dessa árvore. Está excluído do requisito de autenticação.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gerenciando políticas CUG e requisitos de autenticação {#managing-cug-policies-and-authentication-requirement}

### Gerenciando políticas CUG {#managing-cug-policies}

O novo tipo de políticas de controle de acesso para restringir o acesso de leitura de um CUG é gerenciado usando a API de gerenciamento de controle de acesso JCR e segue os mecanismos descritos com a [especificação JCR 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Definir uma nova política CUG {#set-a-new-cug-policy}

Código para aplicar uma nova política CUG em um nó que não tinha um CUG definido anteriormente. Observe que `getApplicablePolicies` retorna somente novas políticas que não tenham sido definidas anteriormente. No final, a política deve ser recuperada e as alterações devem ser persistentes.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Editar uma política CUG existente {#edit-an-existing-cug-policy}

As etapas a seguir são necessárias para editar uma política CUG existente. A política modificada deve ser gravada e as alterações devem ser persistentes usando `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### Recuperar Políticas CUG Efetivas {#retrieve-effective-cug-policies}

O gerenciamento de controle de acesso JCR define um método de melhor esforço para recuperar as políticas que entram em vigor em um determinado caminho. Como a avaliação das políticas CUG é condicional e depende da configuração correspondente a ser habilitada, chamar `getEffectivePolicies` é uma maneira conveniente de verificar se uma determinada política CUG está tendo efeito em uma determinada instalação.

>[!NOTE]
>
>A diferença entre `getEffectivePolicies` e o código de exemplo subsequente que percorre a hierarquia para descobrir se um determinado caminho já faz parte de um CUG existente.

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### Recuperar Políticas CUG Herdadas {#retrieve-inherited-cug-policies}

Encontrar todos os CUGs aninhados que foram definidos em um determinado caminho, independentemente de terem efeito ou não. Para obter mais informações, consulte a seção [Opções de Configuração](/help/sites-administering/closed-user-groups.md#configuration-options).

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### Gerenciando políticas CUG por principal {#managing-cug-policies-by-pincipal}

As extensões definidas por `JackrabbitAccessControlManager` que permitem editar políticas de controle de acesso por entidade de segurança não são implementadas com o gerenciamento de controle de acesso CUG, pois, por definição, uma política CUG sempre afeta todas as entidades de segurança: as listadas com `PrincipalSetPolicy` recebem acesso de leitura, enquanto todas as outras entidades de segurança serão impedidas de ler o conteúdo na árvore definida pelo nó de destino.

Os métodos correspondentes sempre retornam uma matriz de política vazia, mas não lançam exceções.

### Gerenciamento do requisito de autenticação {#managing-the-authentication-requirement}

A criação, modificação ou remoção de um novo requisito de autenticação é alcançada alterando o tipo de nó efetivo do nó de destino. A propriedade de caminho de logon opcional pode ser gravada usando a API JCR comum.

>[!NOTE]
>
>As modificações em um determinado nó de destino mencionado acima só serão refletidas no Apache Sling Authenticator se o `RequirementHandler` tiver sido configurado e o destino estiver contido nas árvores definidas pelos caminhos compatíveis (consulte a seção Opções de configuração).
>
>Para obter mais informações, consulte [Atribuição de tipos de nós de mixin](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Atribuição de tipos de nós de mixin) e [Adição de nós e configuração de propriedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Adição de nós e configuração de propriedades)

#### Adicionando um Novo Requisito de Autenticação {#adding-a-new-auth-requirement}

As etapas para criar um requisito de autenticação são detalhadas abaixo. O requisito só será registrado com o Apache Sling Authenticator se o `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Adicionar um novo requisito de autenticação com caminho de logon {#add-a-new-auth-requirement-with-login-path}

Etapas para criar um requisito de autenticação, incluindo um caminho de logon. O requisito e a exclusão do caminho de logon só serão registrados com o Apache Sling Authenticator se o `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificar um caminho de login existente {#modify-an-existing-login-path}

As etapas para alterar um caminho de logon existente são detalhadas abaixo. A modificação só será registrada com o Apache Sling Authenticator se o `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino. O valor do caminho de logon anterior é removido do registro. O requisito de autenticação associado ao nó de destino não é afetado por essa modificação.

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### Remover um caminho de logon existente {#remove-an-existing-login-path}

Etapas para remover um caminho de logon existente. A entrada do caminho de logon só terá o registro cancelado no Apache Sling Authenticator se o `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino. O requisito de autenticação associado ao nó de destino não é afetado.

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

Ou você pode usar o método abaixo para atingir o mesmo objetivo:

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### Remover um requisito de autenticação {#remove-an-auth-requirement}

Etapas para remover um requisito de autenticação existente. O requisito só terá o registro cancelado do Apache Sling Authenticator se o `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recuperar Requisitos de Autenticação Efetiva {#retrieve-effective-auth-requirements}

Não há API pública dedicada para ler todos os requisitos de autenticação eficazes conforme registrados com o Apache Sling Authenticator. No entanto, a lista é exposta no console do sistema em `https://<serveraddress>:<serverport>/system/console/slingauth` na seção &quot;**Configuração de Requisito de Autenticação**&quot;.

A imagem a seguir mostra os requisitos de autenticação de uma instância de publicação do AEM com conteúdo de demonstração. O caminho destacado da página da comunidade ilustra como um requisito adicionado pela implementação descrita neste documento é refletido no Apache Sling Authenticator.

>[!NOTE]
>
>Neste exemplo, a propriedade de caminho de logon opcional não foi definida. Portanto, nenhuma segunda entrada foi registrada com o autenticador.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Recuperar o caminho de login efetivo {#retrieve-the-effective-login-path}

No momento, não há API pública para recuperar o caminho de logon que entra em vigor ao acessar anonimamente um recurso que requer autenticação. Consulte a seção Avaliação do caminho de logon para obter detalhes de implementação sobre como o caminho de logon é recuperado.

No entanto, observe que, além dos caminhos de logon definidos com esse recurso, há maneiras alternativas de especificar o redirecionamento para o logon, que devem ser consideradas ao projetar o modelo de conteúdo e os requisitos de autenticação de uma determinada instalação do AEM.

#### Recuperar o Requisito de Autenticação Herdado {#retrieve-the-inherited-auth-requirement}

Assim como no caminho de logon, não há API pública para recuperar os requisitos de autenticação herdados definidos no conteúdo. O exemplo a seguir ilustra como listar todos os requisitos de autenticação que foram definidos com uma determinada hierarquia independentemente de terem efeito ou não. Para obter mais informações, consulte [Opções de Configuração](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>É recomendável confiar no mecanismo de herança para requisitos de autenticação e caminho de logon e evitar a criação de requisitos de autenticação aninhados.
>
>Para obter mais informações, consulte [Avaliação e herança do requisito de autenticação](#evaluation-and-inheritance-of-the-authentication-requirement), [Avaliação do caminho de logon](#evaluation-of-login-path) e [Práticas recomendadas](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### Combinando políticas CUG e o requisito de autenticação {#combining-cug-policies-and-the-authentication-requirement}

A tabela a seguir lista as combinações válidas de políticas CUG e o requisito de autenticação em uma instância AEM que tenha ambos os módulos ativados por meio de configuração.

| **Autenticação necessária** | **Caminho de Login** | **Acesso de Leitura Restrito** | **Efeito Esperado** |
|---|---|---|---|
| Sim | Sim | Sim | Um determinado usuário só poderá exibir a subárvore marcada com a política CUG se a avaliação de permissão efetiva conceder acesso. Um usuário não autenticado é redirecionado para a página de logon especificada. |
| Sim | Não | Sim | Um determinado usuário só poderá exibir a subárvore marcada com a política CUG se a avaliação de permissão efetiva conceder acesso. Um usuário não autenticado é redirecionado para uma página de logon padrão herdada. |
| Sim | Sim | Não | Um usuário não autenticado é redirecionado para a página de logon especificada. Se é permitido exibir a árvore marcada com o requisito de autenticação depende das permissões efetivas dos itens individuais contidos nessa subárvore. Nenhum CUG dedicado que restrinja o acesso de leitura está em vigor. |
| Sim | Não | Não | Um usuário não autenticado é redirecionado para uma página de logon padrão herdada. Se é permitido exibir a árvore marcada com o requisito de autenticação depende das permissões efetivas dos itens individuais contidos nessa subárvore. Nenhum CUG dedicado que restrinja o acesso de leitura está em vigor. |
| Não | Não | Sim | Um determinado usuário autenticado ou não autenticado só poderá exibir a subárvore marcada com a política CUG se a avaliação de permissão efetiva conceder acesso. Um usuário não autenticado é tratado igualmente e não é redirecionado para fazer logon. |

>[!NOTE]
>
>A combinação de &#39;Requisito de autenticação&#39; = Não e &#39;Caminho de logon&#39; = Sim não está listada acima, pois &#39;Caminho de logon&#39; é um atributo opcional associado a um Requisito de autenticação. A especificação de uma propriedade JCR com esse nome sem adicionar o tipo de mixin de definição não tem efeito e é ignorada pelo manipulador correspondente.

## Componentes e configuração do OSGi {#osgi-components-and-configuration}

Esta seção fornece uma visão geral dos componentes OSGi e as opções de configuração individuais introduzidas com a nova implementação do CUG.

Consulte também a documentação de mapeamento CUG para obter um mapeamento abrangente das opções de configuração entre a implementação antiga e a nova.

### Autorização: instalação e configuração {#authorization-setup-and-configuration}

As novas partes relacionadas à autorização estão contidas no pacote **Autorização CUG do Oak** ( `org.apache.jackrabbit.oak-authorization-cug`), que faz parte da instalação padrão do AEM. O pacote define um modelo de autorização separado destinado a ser implantado como uma maneira adicional de gerenciar o acesso de leitura.

#### Configurando a autorização CUG {#setting-up-cug-authorization}

A configuração da autorização CUG é descrita em detalhes na [Documentação relevante do Apache](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Por padrão, o AEM tem autorização CUG implantada em todos os modos de execução. As instruções passo a passo também podem ser usadas para desativar a autorização CUG nas instalações que exigem uma configuração de autorização diferente.

#### Configurar o filtro referenciador {#configuring-the-referrer-filter}

Você também deve configurar o [Filtro referenciador Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) com todos os nomes de host que possam ser usados para acessar o AEM; por exemplo, via CDN, Balanceador de carga e outros.

Se o filtro referenciador não estiver configurado, erros, semelhantes aos seguintes, serão vistos quando um usuário tentar fazer logon em um site CUG:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Características dos componentes OSGi {#characteristics-of-osgi-components}

Os dois componentes OSGi a seguir foram introduzidos para definir requisitos de autenticação e especificar caminhos de logon dedicados:

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Rótulo</td>
   <td>Configuração de CUG do Apache Jackrabbit Oak</td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>Configuração de autorização dedicada à configuração e avaliação de permissões de CUG.</td>
  </tr>
  <tr>
   <td>Propriedades de configuração</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Além disso, consulte <a href="#configuration-options">Opções de Configuração</a> abaixo.</p> </td>
  </tr>
  <tr>
   <td>Política de configuração</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referências</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>Rótulo</td>
   <td>Lista de exclusões do Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>Permite excluir entidades principais com os nomes configurados da avaliação CUG.</td>
  </tr>
  <tr>
   <td>Propriedades de configuração</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Consulte também a seção Opções de configuração abaixo.</p> </td>
  </tr>
  <tr>
   <td>Política de configuração</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referências</td>
   <td>ND</td>
  </tr>
 </tbody>
</table>

#### Opções de configuração {#configuration-options}

As principais opções de configuração são:

* `cugSupportedPaths`: especifique as subárvores que podem conter CUGs. Nenhum valor padrão está definido
* `cugEnabled`: opção de configuração para habilitar a avaliação de permissão para as políticas CUG presentes.

As opções de configuração disponíveis associadas ao módulo de autorização CUG são listadas e descritas em mais detalhes na [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Excluindo entidades da avaliação CUG {#excluding-principals-from-cug-evaluation}

A isenção de princípios individuais da avaliação CUG foi adotada a partir da implementação anterior. A nova autorização CUG cobre isso com uma interface dedicada chamada CugExclude. O Apache Jackrabbit Oak 1.4 vem com uma implementação padrão que exclui um conjunto fixo de principais e uma implementação estendida que permite configurar nomes principais individuais. O último é configurado em instâncias de publicação do AEM.

O padrão desde o AEM 6.3 impede que os seguintes principais sejam afetados pelas políticas CUG:

* entidades administrativas (usuário administrador, grupo de administradores)
* principais de usuário do serviço
* principal do sistema interno de repositório

Para obter mais informações, consulte a tabela na seção [Configuração Padrão desde o AEM 6.3](#default-configuration-since-aem) abaixo.

A exclusão do grupo &quot;administradores&quot; pode ser alterada ou expandida no console do sistema na seção de configuração da **Lista de exclusões do Apache Jackrabbit Oak CUG**.

Como alternativa, é possível fornecer e implantar uma implementação personalizada da interface CugExclude para ajustar o conjunto de principais excluídos se houver necessidades especiais. Consulte a documentação sobre [pluggability CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obter detalhes e um exemplo de implementação.

### Autenticação: instalação e configuração {#authentication-setup-and-configuration}

As novas partes relacionadas à autenticação estão contidas no pacote **Manipulador de autenticação do Adobe Granite** ( `com.adobe.granite.auth.authhandler` versão 5.6.48). Este pacote faz parte da instalação padrão do AEM.

Para configurar a substituição do requisito de autenticação para o suporte CUG obsoleto, alguns componentes OSGi devem estar presentes e ativos em uma determinada instalação do AEM. Para obter mais detalhes, consulte **Características dos componentes OSGi** abaixo.

>[!NOTE]
>
>Devido à opção de configuração obrigatória com o RequirementHandler, as partes relacionadas à autenticação só estarão ativas se o recurso tiver sido habilitado por meio da especificação de um conjunto de caminhos compatíveis. Com uma instalação padrão do AEM, o recurso é desativado no modo de execução do autor e ativado para /content no modo de execução de publicação.

**Características dos componentes OSGi**

Os dois componentes OSGi a seguir foram introduzidos para definir requisitos de autenticação e especificar caminhos de logon dedicados:

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirements.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>Rótulo</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>O serviço OSGi dedicado para requisitos de autenticação que registram um observador para alterações de conteúdo que afetam o requisito de autenticação (por meio do tipo de mixin <code>granite:AuthenticationRequirement</code>) e caminhos de logon com são expostos ao <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Propriedades de configuração</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Política de configuração</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>Referências</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler**

| Rótulo | Requisito de autenticação do Adobe Granite e manipulador de caminho de logon |
|---|---|
| Descrição | Implementação do `RequirementHandler` que atualiza os requisitos de autenticação do Apache Sling e a exclusão correspondente para os caminhos de logon associados. |
| Propriedades de configuração | `supportedPaths` |
| Política de configuração | `ConfigurationPolicy.REQUIRE` |
| Referências | ND |

#### Opções de configuração {#configuration-options-1}

As partes relacionadas à autenticação da regravação do CUG vêm apenas com uma única opção de configuração associada ao Requisito de autenticação do Adobe Granite e ao Manipulador de caminho de logon:

**&quot;Requisito de autenticação e Manipulador de caminho de logon&quot;**

<table>
 <tbody>
  <tr>
   <td>Propriedade</td>
   <td>Tipo</td>
   <td>Valor padrão</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td><p>Rótulo = Caminhos compatíveis</p> <p>Nome = 'supportedPaths'</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>Caminhos nos quais os requisitos de autenticação serão respeitados por este manipulador. Deixe essa configuração desdefinida se quiser adicionar o tipo de mixin <code>granite:AuthenticationRequirement</code> aos nós sem aplicá-los (por exemplo, em instâncias de autor). Se ausente, o recurso é desativado. </td>
  </tr>
 </tbody>
</table>

## Configuração padrão desde o AEM 6.3 {#default-configuration-since-aem}

As novas instalações do AEM usarão, por padrão, as novas implementações para as partes relacionadas à autorização e à autenticação do recurso CUG. A implementação antiga &quot;Suporte ao grupo de usuários fechado (CUG) do Adobe Granite&quot; foi descontinuada e será desativada por padrão em todas as instalações de AEM. Em vez disso, as novas implementações serão habilitadas da seguinte maneira:

### Instâncias do autor {#author-instances}

| **&quot;Configuração CUG do Apache Jackrabbit Oak&quot;** | **Explicação** |
|---|---|
| Caminhos com Suporte `/content` | O gerenciamento de controle de acesso para políticas CUG está habilitado. |
| Avaliação de CUG habilitada FALSE | A avaliação de permissões está desabilitada. As políticas CUG não têm efeito. |
| Classificação | 200 | Consulte a documentação do Oak. |

>[!NOTE]
>
>Nenhuma configuração da **Lista de Exclusões do Apache Jackrabbit Oak CUG** e do **Requisito de Autenticação do Adobe Granite e Manipulador de Caminho de Logon** está presente nas instâncias de criação padrão.

### Instâncias do Publish {#publish-instances}

| **&quot;Configuração CUG do Apache Jackrabbit Oak&quot;** | **Explicação** |
|---|---|
| Caminhos com Suporte `/content` | O gerenciamento de controle de acesso para políticas CUG está habilitado abaixo dos caminhos configurados. |
| CUG Evaluation Enabled TRUE (Avaliação de CUG ativada TRUE) | A avaliação de permissões está habilitada abaixo dos caminhos configurados. As políticas CUG entram em vigor em `Session.save()`. |
| Classificação | 200 | Consulte a documentação do Oak. |

| **&quot;Lista de Exclusões do Apache Jackrabbit Oak CUG&quot;** | **Explicação** |
|---|---|
| Administradores de nomes principais | Exclui a entidade de segurança de administradores da avaliação CUG. |

| **&quot;Requisito de autenticação do Adobe Granite e Manipulador de caminho de logon&quot;** | **Explicação** |
|---|---|
| Caminhos com Suporte `/content` | Os requisitos de autenticação conforme definidos no repositório pelo tipo de mixin `granite:AuthenticationRequired` entram em vigor abaixo de `/content` em `Session.save()`. O Sling Authenticator é atualizado. A adição do tipo de mixin fora dos caminhos compatíveis é ignorada. |

## Desabilitando Requisito de Autorização e Autenticação CUG {#disabling-cug-authorization-and-authentication-requirement}

A nova implementação pode ser desabilitada completamente caso uma determinada instalação não use CUGs ou use meios diferentes para autenticação e autorização.

### Desabilitar autorização CUG {#disable-cug-authorization}

Consulte a documentação de [pluggability CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obter detalhes sobre como remover o modelo de autorização CUG da configuração de autorização composta.

### Desativar o requisito de autenticação {#disable-the-authentication-requirement}

Para desabilitar o suporte para o requisito de autenticação fornecido pelo módulo `granite.auth.authhandler`, é suficiente remover a configuração associada ao **Requisito de Autenticação do Adobe Granite e Manipulador de Caminho de Logon**.

>[!NOTE]
>
>Observe, no entanto, que a remoção da configuração não cancelará o registro do tipo de mixin, que ainda era aplicável a nós sem ter efeito.

## Interação com outros módulos {#interaction-with-other-modules}

### API Apache Jackrabbit {#apache-jackrabbit-api}

Para refletir o novo tipo de política de controle de acesso usado pelo modelo de autorização CUG, a API definida pelo Apache Jackrabbit foi estendida. Desde a versão 2.11.0 do módulo `jackrabbit-api`, define uma nova interface chamada `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, que se estende de `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

O mecanismo de importação do Apache Jackrabbit FileVault foi ajustado para lidar com políticas de controle de acesso do tipo `PrincipalSetPolicy`.

### Distribuição de conteúdo do Apache Sling {#apache-sling-content-distribution}

Consulte a seção [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) acima.

### Replicação do Adobe Granite {#adobe-granite-replication}

O módulo de replicação foi levemente ajustado para poder replicar as políticas CUG entre instâncias AEM diferentes:

* `DurboImportConfiguration.isImportAcl()` é interpretado literalmente e afetará somente as políticas de controle de acesso que implementam `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` respeitará somente esta configuração para ACLs verdadeiras
* Outras políticas, como `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` instâncias criadas pelo modelo de autorização CUG, sempre serão replicadas e a opção de configuração `DurboImportConfiguration.isImportAcl`() será ignorada.

Há uma limitação da replicação de políticas CUG. Se uma determinada política CUG for removida sem remover o tipo de nó de mixin correspondente `rep:CugMixin,`, a remoção não será refletida na replicação. Isso tem sido resolvido sempre removendo o mixin após a remoção da política. A limitação pode, no entanto, ser exibida se o tipo de mixin for adicionado manualmente.

### Manipulador de autenticação do Adobe Granite {#adobe-granite-authentication-handler}

O manipulador de autenticação **Manipulador de Autenticação do Cabeçalho HTTP do Adobe Granite** enviado com o pacote `com.adobe.granite.auth.authhandler` contém uma referência à interface `CugSupport` definida pelo mesmo módulo. É usado para calcular o &quot;realm&quot; em determinadas circunstâncias, recorrendo ao realm configurado com o manipulador.

Isso foi ajustado para tornar a referência a `CugSupport` opcional para garantir o máximo de compatibilidade com versões anteriores se uma determinada configuração decidir reativar a implementação obsoleta. As instalações que usam a implementação não obterão mais o realm extraído da implementação CUG, mas sempre exibirão o realm como definido com o **Manipulador de Autenticação do Cabeçalho HTTP do Adobe Granite**.

>[!NOTE]
>
>Por padrão, o **Manipulador de autenticação do cabeçalho HTTP do Adobe Granite** só é configurado no modo de execução de publicação com a opção &quot;Desabilitar página de logon&quot; ( `auth.http.nologin`) habilitada.

### Live Copy do AEM {#aem-livecopy}

A configuração de CUGs com Live Copy é representada no repositório pela adição de um nó extra e uma propriedade extra, da seguinte maneira:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ambos os elementos são criados em `cq:Page`. Com o design atual, o MSM manipula apenas nós e propriedades que estão sob o nó `cq:PageContent` (`jcr:content`).

Portanto, os grupos CUG não podem ser implantados em Live Copies de blueprints. Planeje isso ao configurar a Live Copy.

## Alterações com a nova implementação de CUG {#changes-with-the-new-cug-implementation}

O objetivo desta seção é fornecer uma visão geral das alterações feitas no recurso CUG e uma comparação entre a implementação antiga e a nova implementação. Ele lista as alterações que afetam a forma como o suporte a CUG é configurado e descreve como e por quem os CUGs são gerenciados no conteúdo do repositório.

### Diferenças na instalação e configuração do CUG {#differences-in-cug-setup-and-configuration}

O componente OSGi obsoleto **Suporte ao CUG (Grupo de Usuários Fechado) do Adobe Granite** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) foi substituído por novos componentes para poder manipular separadamente as partes relacionadas à autorização e à autenticação da funcionalidade anterior do CUG.

## Diferenças no gerenciamento de CUGs no conteúdo do repositório {#differences-in-managing-cugs-in-the-repository-content}

As seções a seguir descrevem as diferenças entre as implementações antigas e novas do ponto de vista da implementação e da segurança. Embora a nova implementação tenha como objetivo fornecer a mesma funcionalidade, há alterações sutis que são importantes ao usar o novo CUG.

### Diferenças Em Relação À Autorização {#differences-with-regards-to-authorization}

As principais diferenças do ponto de vista da autorização são resumidas na lista seguinte:

**Conteúdo de controle de acesso dedicado para CUGs**

Na implementação antiga, o modelo de autorização padrão era usado para manipular as políticas de lista de controle de acesso na publicação, substituindo quaisquer ACEs existentes pela configuração exigida pelo CUG. Isso foi acionado pela gravação de propriedades JCR residuais e regulares que foram interpretadas na publicação.

Com a nova implementação, a configuração do controle de acesso do modelo de autorização padrão não é afetada por qualquer CUG que esteja sendo criado, modificado ou removido. Em vez disso, um novo tipo de política chamado `PrincipalSetPolicy` é aplicado como conteúdo de controle de acesso adicional ao nó de destino. Essa política adicional está localizada como um filho do nó de destino e seria semelhante ao nó de política padrão, se presente.

**Editando Políticas CUG No Gerenciamento de Controle de Acesso**

Essa mudança de propriedades residuais do JCR para uma política dedicada de controle de acesso tem um impacto na permissão necessária para criar ou modificar a parte de autorização do recurso CUG. Como isso é considerado uma modificação para acessar o conteúdo do controle, é necessário que os privilégios `jcr:readAccessControl` e `jcr:modifyAccessControl` sejam gravados no repositório. Portanto, somente os autores de conteúdo com direito a modificar o conteúdo de controle de acesso de uma página podem configurar ou modificar esse conteúdo. Isso contrasta com a implementação antiga, em que a capacidade de gravar propriedades JCR regulares era suficiente, resultando em um aumento de privilégio.

**Nó De Destino Definido Pela Política**

Crie políticas CUG no nó JCR definindo a subárvore para estar sujeita a acesso restrito de leitura. Essa provavelmente será uma página AEM caso o CUG afete toda a árvore.

Colocar a política CUG somente no nó jcr:content localizado abaixo de uma determinada página restringe o acesso ao conteúdo s.str de uma determinada página, mas não terá efeito em nenhum irmão ou página secundária. Esse pode ser um caso de uso válido e é possível obtê-lo com um editor de repositório que permite a aplicação de conteúdo de acesso refinado. No entanto, contrasta com a implementação anterior, em que a inserção de uma propriedade cq:cugEnabled no nó jcr:content era remapeada internamente para o nó da página. Esse mapeamento não é mais executado.

**Avaliação de Permissão com Políticas CUG**

A mudança do suporte ao CUG antigo para um modelo de autorização adicional altera a maneira como as permissões de leitura eficazes são avaliadas. Conforme descrito na [Documentação do Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), um determinado principal com permissão para exibir `CUGcontent` só receberá acesso de leitura se a avaliação de permissão de todos os modelos configurados no repositório do Oak conceder acesso de leitura.

Em outras palavras, para a avaliação das permissões efetivas, as entradas de controle de acesso `CUGPolicy` e padrão são consideradas e o acesso de leitura no conteúdo CUG só é concedido se for concedido por ambos os tipos de políticas. Em uma instalação de publicação padrão do AEM em que o acesso de leitura à árvore completa do `/content` é concedido a todos, o efeito das políticas CUG é o mesmo da implementação antiga.

**Avaliação sob demanda**

O modelo de autorização CUG permite ativar individualmente o gerenciamento de controle de acesso e a avaliação de permissão:

* o gerenciamento de controle de acesso será ativado se o módulo tiver um ou vários caminhos suportados onde os CUGs possam ser criados
* a avaliação de permissão só será habilitada se a opção **Avaliação CUG Habilitada** também estiver marcada.

Na nova avaliação da configuração padrão do AEM das políticas CUG, ela só é ativada com o modo de execução &quot;publicar&quot;. Consulte os detalhes na [configuração padrão desde o AEM 6.3](#default-configuration-since-aem) para obter mais detalhes. Isso pode ser verificado comparando as políticas eficazes de um determinado caminho com as políticas armazenadas no conteúdo. As políticas efetivas só serão exibidas caso a avaliação de permissão para CUGs esteja ativada.

Como explicado acima, as políticas de controle de acesso CUG agora são sempre armazenadas no conteúdo, mas a avaliação das permissões efetivas resultantes dessas políticas só será aplicada se **Avaliação CUG Habilitada** estiver ativada no console do sistema na Configuração **CUG do Apache Jackrabbit Oak.** Por padrão, está habilitado somente com o modo de execução &#39;publicar&#39;.

### Diferenças Em Relação À Autenticação {#differences-with-regards-to-authentication}

As diferenças em relação à autenticação são descritas abaixo.

#### Tipo De Mixin Dedicado Para Requisito De Autenticação {#dedicated-mixin-type-for-authentication-requirement}

Na implementação anterior, os aspectos de autorização e autenticação de um CUG eram acionados por uma única propriedade JCR ( `cq:cugEnabled`). No que diz respeito à autenticação, isso resultou em uma lista atualizada de requisitos de autenticação, conforme armazenados com a implementação do Apache Sling Authenticator. Com a nova implementação, o mesmo resultado é obtido marcando o nó de destino com um tipo de mixin dedicado ( `granite:AuthenticationRequired`).

#### Propriedade Para Excluir O Caminho De Logon {#property-for-excluding-login-path}

O tipo de mixin define uma única propriedade opcional chamada `granite:loginPath`, que basicamente corresponde à propriedade `cq:cugLoginPage`. Ao contrário da implementação anterior, a propriedade do caminho de logon só é respeitada se o tipo de nó declarante for o mixin mencionado. Adicionar uma propriedade com esse nome sem definir o tipo de mixin não tem efeito e nem um novo requisito nem uma exclusão para o caminho de logon são relatados ao autenticador.

#### Privilégio Para Requisito De Autenticação {#privilege-for-authentication-requirement}

Adicionar ou remover um tipo de mixin requer o privilégio `jcr:nodeTypeManagement` concedido. Na implementação anterior, o privilégio `jcr:modifyProperties` é usado para editar a propriedade residual.

No que diz respeito a `granite:loginPath`, o mesmo privilégio é necessário para adicionar, modificar ou remover a propriedade.

#### Nó de Destino Definido pelo Tipo de Mixin {#target-node-defined-by-mixin-type}

Crie requisitos de autenticação no nó JCR definindo a subárvore para estar sujeita a logon imposto. Essa provavelmente será uma página AEM caso o CUG afete toda a árvore e a interface do usuário para a nova implementação, portanto, adiciona o tipo de mixin de requisito de autenticação no nó da página.

Colocar a política CUG somente no nó jcr:content localizado abaixo de uma determinada página restringe somente o acesso ao conteúdo. No entanto, isso não afeta o próprio nó da página nem as páginas secundárias.

Esse cenário pode ser válido e é possível com um editor de repositório que permite colocar o mixin em qualquer nó. No entanto, o comportamento contrasta com a implementação anterior, em que a inserção de uma propriedade cq:cugEnabled ou cq:cugLoginPage no nó jcr:content foi remapeada internamente para o nó da página. Esse mapeamento não é mais executado.

#### Caminhos suportados configurados {#configured-supported-paths}

O tipo de mixin `granite:AuthenticationRequired` e a propriedade granite:loginPath somente serão respeitados no escopo definido pelo conjunto da opção de configuração **Caminhos com Suporte** presente no **Requisito de Autenticação do Granite para Adobe e Manipulador de Caminho de Logon**. Se nenhum caminho for especificado, o recurso de requisito de autenticação será completamente desabilitado. Nesse caso, o tipo de mixin ou a propriedade têm efeito quando são adicionados ou definidos para um determinado nó JCR.

### Mapeamento de conteúdo JCR, serviços OSGi e configurações {#mapping-of-jcr-content-osgi-services-and-configurations}

O documento abaixo fornece um mapeamento abrangente dos serviços, configurações e conteúdo do repositório OSGi entre a implementação antiga e a nova.

Mapeamento de CUG desde o AEM 6.3

[Obter arquivo](assets/cug-mapping.pdf)

## Atualizar CUG {#upgrade-cug}

### Instalações existentes usando o CUG obsoleto {#existing-installations-using-the-deprecated-cug}

A implementação antiga de suporte ao CUG foi descontinuada e será removida para em versões futuras. É recomendável mudar para as novas implementações ao atualizar de versões anteriores ao AEM 6.3.

Para uma instalação atualizada do AEM, é importante garantir que apenas uma implementação CUG esteja habilitada. A combinação do novo e do antigo suporte CUG obsoleto não é testada e provavelmente causará um comportamento indesejado:

* colisões no Sling Authenticator em relação aos requisitos de autenticação
* Acesso de leitura negado quando a configuração da ACL associada ao CUG antigo colide com uma nova política CUG.

### Migração de conteúdo CUG existente {#migrating-existing-cug-content}

O Adobe fornece uma ferramenta para migrar para a nova implementação CUG. Para usá-lo, execute as seguintes etapas:

1. Vá para `https://<serveraddress>:<serverport>/system/console/cug-migration` para acessar a ferramenta.
1. Digite o caminho raiz que você deseja verificar CUGs e pressione o botão **Executar simulação**. Isso verifica os CUGs qualificados para conversão no local selecionado.
1. Depois de analisar os resultados, pressione o botão **Executar migração** para migrar para a nova implementação.

>[!NOTE]
>
>Se você tiver problemas, é possível configurar um agente de log específico no nível **DEBUG** em `com.day.cq.auth.impl.cug` para obter o resultado da ferramenta de migração. Consulte [Log](/help/sites-deploying/configure-logging.md) para obter mais informações sobre como fazer isso.
