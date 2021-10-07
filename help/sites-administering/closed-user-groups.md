---
title: Grupos de usuários fechados em AEM
seo-title: Closed User Groups in AEM
description: Saiba mais sobre Grupos de usuários fechados no AEM.
seo-description: Learn about Closed User Groups in AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '6872'
ht-degree: 0%

---

# Grupos de usuários fechados em AEM{#closed-user-groups-in-aem}

## Introdução {#introduction}

Desde o AEM 6.3, há uma nova implementação do Grupo de usuários fechado destinada a solucionar os problemas de desempenho, escalabilidade e segurança presentes com a implementação existente.

>[!NOTE]
>
>Por uma questão de simplicidade, a abreviatura do CUG será usada em toda esta documentação.

O objetivo da nova implementação é cobrir a funcionalidade existente, quando necessário, ao mesmo tempo que lida com problemas e limitações de design de versões mais antigas. O resultado é um novo desenho CUG com as seguintes características:

* Separação clara dos elementos de autenticação e de autorização, que podem ser utilizados individualmente ou em combinação;
* Modelo de autorização dedicado para refletir a restrição do acesso de leitura nas árvores de CUG configuradas sem interferir com outros requisitos de configuração e permissão do controlo de acesso;
* Separação entre a configuração de controle de acesso do acesso restrito de leitura, que geralmente é necessária em instâncias de criação, e a avaliação de permissão, que geralmente é desejada apenas na publicação;
* Edição do acesso restrito de leitura sem escalação de privilégios;
* Extensão de tipo de nó dedicada para marcar o requisito de autenticação;
* Caminho de logon opcional associado ao requisito de autenticação.

### A nova implementação de grupo de usuários personalizado {#the-new-custom-user-group-implementation}

Um CUG, como é conhecido no contexto de AEM, consiste nas seguintes etapas:

* Restrinja o acesso de leitura na árvore que precisa ser protegida e permita somente leitura para entidades principais listadas com uma determinada instância CUG ou excluídas totalmente da avaliação CUG. Isso é chamado de elemento **authorization**.
* Impor autenticação em uma determinada árvore e, opcionalmente, especificar uma página de logon dedicada para essa árvore que será excluída subsequentemente. Isso é chamado de elemento **authentication**.

A nova implementação foi projetada para traçar uma linha entre a autenticação e os elementos de autorização. A partir do AEM 6.3, é possível restringir o acesso de leitura sem adicionar explicitamente um requisito de autenticação. Por exemplo, se uma determinada instância exigir autenticação completamente ou uma determinada árvore já residir em uma subárvore que já requer autenticação.

Da mesma forma, uma determinada árvore pode ser marcada com um requisito de autenticação sem alterar a configuração de permissão efetiva. As combinações e os resultados são listados na seção [Combining CUG Policies and the Authentication Requirements](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement).

## Visão geral {#overview}

### Autorização: Restrição do acesso de leitura {#authorization-restricting-read-access}

O recurso principal de um CUG está restringindo o acesso de leitura em uma determinada árvore no repositório de conteúdo para todos, exceto entidades selecionadas. Em vez de manipular o conteúdo de controle de acesso padrão dinamicamente, a nova implementação adota uma abordagem diferente definindo um tipo dedicado de política de controle de acesso que representa um CUG.

#### Política de Controle de Acesso para CUG {#access-control-policy-for-cug}

Este novo tipo de política tem as seguintes características:

* Política de controle de acesso do tipo org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (definido pela API Apache Jackrabbit);
* O PrincipalSetPolicy concede privilégios a um conjunto modificável de entidades principais;
* Os privilégios concedidos e o âmbito da política são um pormenor de implementação.

A implementação de PrincipalSetPolicy usada para representar CUGs além disso define que:

* As políticas de CUG só concedem acesso de leitura a itens JCR comuns (por exemplo, o conteúdo de controle de acesso é excluído);
* O escopo é definido pelo nó controlado de acesso que detém a política CUG;
* As políticas de CUG podem ser aninhadas, um CUG aninhado inicia um novo CUG sem herdar o conjunto principal do CUG &#39;pai&#39;;
* O efeito da política, se a avaliação estiver ativada, será herdado para toda a subárvore até o próximo CUG aninhado.

Essas políticas de CUG são implantadas em uma instância de AEM por meio de um módulo de autorização separado chamado oak-authorization-cug. Este módulo vem com seu próprio gerenciamento de controle de acesso e avaliação de permissões. Em outras palavras, a configuração de AEM padrão envia uma configuração de repositório de conteúdo do Oak que combina vários mecanismos de autorização. Para obter mais informações, consulte [esta página na Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Nesta configuração composta, um novo CUG não substitui o conteúdo de controle de acesso existente anexado ao nó de destino, mas é projetado para ser um suplemento que também pode ser removido posteriormente sem afetar o controle de acesso original, que por padrão no AEM seria uma lista de controle de acesso.

Ao contrário da anterior implementação, as novas políticas de CUG são sempre reconhecidas e tratadas como conteúdo de controle de acesso. Isso implica que eles sejam criados e editados usando a API de gerenciamento de controle de acesso JCR. Para obter mais informações, consulte a seção [Gerenciando Políticas de CUG](#managing-cug-policies) .

#### Avaliação de Permissão de Políticas de CUG {#permission-evaluation-of-cug-policies}

Além de um gerenciamento dedicado de controle de acesso para CUGs, o novo modelo de autorização permite habilitar condicionalmente a avaliação de permissão para suas políticas. Isso permite configurar as políticas de CUG em um ambiente de preparo e ativar a avaliação das permissões efetivas somente depois de replicadas para o ambiente de produção.

A avaliação de permissão para políticas CUG e a interação com o modelo de autorização padrão ou adicional seguem o padrão projetado para vários mecanismos de autorização no Apache Jackrabbit Oak: um determinado conjunto de permissões é concedido somente se e somente se todos os modelos concederem acesso. Consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) para obter mais detalhes.

As seguintes características se aplicam à avaliação de permissão associada ao modelo de autorização criado para manipular e avaliar as políticas de CUG:

* Ele trata somente permissões de leitura de nós e propriedades comuns, mas não lê o conteúdo de controle de acesso
* Ele não lida com permissões de gravação nem com qualquer tipo de permissão necessária para modificação de conteúdo JCR protegido (controle de acesso, informações de tipo de nó, controle de versão, bloqueio ou gerenciamento de usuários, entre outros); Essas permissões não são afetadas por uma política CUG e não serão avaliadas pelo modelo de autorização associado. A concessão ou não dessas permissões depende dos outros modelos configurados na configuração de segurança.

O efeito de uma única política de CUG sobre a avaliação de permissões pode resumir-se do seguinte modo:

* O acesso de leitura é negado para todos, exceto para assuntos que contenham princípios ou princípios excluídos enumerados na política;
* A política entra em vigor no nó controlado de acesso que detém a política e suas propriedades;
* O efeito é adicionalmente herdado na hierarquia - ou seja, a árvore de itens definida pelo nó controlado de acesso;
* Contudo, não afeta irmãos nem ancestrais do nó controlado de acesso;
* A herança de um determinado CUG é interrompida em um CUG aninhado.

#### Práticas recomendadas     {#best-practices}

As seguintes práticas recomendadas devem ser consideradas para definir o acesso restrito de leitura por meio de CUGs:

* Tome uma decisão consciente sobre se a necessidade de um CUG é restringir o acesso de leitura ou um requisito de autenticação. No caso deste último, ou se houver necessidade de ambos, consulte a seção sobre Práticas recomendadas para obter detalhes sobre o requisito de autenticação
* Crie um modelo de ameaça para os dados ou conteúdo que precisam ser protegidos para identificar limites de ameaça e obter uma imagem clara sobre a sensibilidade dos dados e as funções associadas ao acesso autorizado
* Modelar o conteúdo do repositório e os CUGs mantendo em mente os aspectos relacionados à autorização geral e as práticas recomendadas:

   * Lembre-se que a permissão de leitura só será concedida se um determinado CUG e a avaliação de outros módulos implantados na concessão de configuração permitirem que um determinado assunto leia um determinado item de repositório
   * Evite criar CUGs redundantes, onde o acesso de leitura já está restrito por outros módulos de autorização
   * Necessidade excessiva de CUGs aninhados pode potencialmente destacar problemas no design de conteúdo
   * A necessidade muito excessiva de CUGs (por exemplo, em cada página única) pode indicar a necessidade de um modelo de autorização personalizado potencialmente mais adequado para atender às necessidades específicas de segurança do aplicativo e do conteúdo em questão.

* Limite os caminhos compatíveis com políticas CUG para algumas árvores no repositório para permitir desempenho otimizado. Por exemplo, permita apenas CUGs abaixo do nó /content como enviado como o valor padrão desde a AEM 6.3.
* As políticas de CUG são projetadas para conceder acesso de leitura a um pequeno conjunto de principais. A necessidade de um grande número de entidades principais pode destacar problemas no conteúdo ou no design do aplicativo e deve ser reconsiderada.

### Autenticação: Definição do requisito de autenticação {#authentication-defining-the-auth-requirement}

As partes relacionadas à autenticação do recurso CUG permitem marcar árvores que exigem autenticação e, opcionalmente, especificar uma página de logon dedicada. De acordo com a versão anterior, a nova implementação permite marcar árvores que exigem autenticação no repositório de conteúdo e habilitar condicionalmente a sincronização com o `Sling org.apache.sling.api.auth.Authenticator`responsável por, em última análise, impor o requisito e redirecionar para um recurso de logon.

Esses requisitos são registrados no Autenticador por meio de um serviço OSGi que fornece a propriedade de registro `sling.auth.requirements`. Essas propriedades são então usadas para estender dinamicamente os requisitos de autenticação. Para obter mais detalhes, consulte a [Documentação do Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definição do requisito de autenticação com um tipo de combinação dedicado {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Por motivos de segurança, a nova implementação substitui o uso de uma propriedade JCR residual por um tipo mixin dedicado chamado `granite:AuthenticationRequired`, que define uma única propriedade opcional do tipo STRING para o caminho de logon `granite:loginPath`. Somente as alterações de conteúdo relacionadas a esse tipo mixin levarão à atualização dos requisitos registrados no Apache Sling Authenticator. As modificações são rastreadas com a persistência de qualquer modificação transitória e, portanto, exigem uma chamada `javax.jcr.Session.save()` para se tornarem efetivas.

O mesmo se aplica à propriedade `granite:loginPath` . Ele só será respeitado se for definido pelo tipo mixin relacionado ao requisito de autenticação. Adicionar uma propriedade residual com esse mesmo nome em um nó JCR não estruturado não mostrará o efeito desejado e a propriedade será ignorada pelo manipulador responsável pela atualização do registro OSGi.

>[!NOTE]
>
>A configuração da propriedade de caminho de logon é opcional e somente necessária se a árvore que requer autenticação não puder voltar para a página de logon padrão ou herdada de outra forma. Consulte a [Avaliação do caminho de logon](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) abaixo.

#### Registrando o requisito de autenticação e o caminho de logon com o autenticador do Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Como esse tipo de requisito de autenticação deve ser limitado a determinados modos de execução e a um pequeno subconjunto de árvores no repositório de conteúdo, o rastreamento do tipo mixin de requisito e as propriedades do caminho de login é condicional e vinculado a uma configuração correspondente que define os caminhos suportados (consulte Opções de configuração abaixo). Consequentemente, somente as alterações no escopo desses caminhos compatíveis acionarão uma atualização do registro OSGi, em qualquer outro lugar, tanto o tipo mixin quanto a propriedade serão ignorados.

A configuração de AEM padrão agora usa essa configuração ao permitir a definição do mixin no modo de execução do autor, mas somente ter efeito na replicação para a instância de publicação. Consulte [esta página](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) para obter detalhes sobre como o Sling aplica o requisito de autenticação.

Adicionar o tipo mixin `granite:AuthenticationRequired` nos caminhos compatíveis configurados fará com que o registro OSGi do manipulador responsável seja atualizado contendo uma nova entrada adicional com a propriedade `sling.auth.requirements`. Se um determinado requisito de autenticação especificar a propriedade `granite:loginPath` opcional, o valor será registrado adicionalmente com o Autenticador com um prefixo &#39;-&#39; para ser excluído do requisito de autenticação.

#### Avaliação e herança do requisito de autenticação {#evaluation-and-inheritance-of-the-authentication-requirement}

Espera-se que os requisitos de autenticação do Apache Sling sejam herdados por meio da hierarquia de página ou nó. Os próprios detalhes da herança e a avaliação dos requisitos de autenticação, como ordem e precedência, são considerados um detalhe de implementação e não serão documentados neste artigo.

#### Avaliação do caminho de logon {#evaluation-of-login-path}

A avaliação do caminho de logon e do redirecionamento para o recurso correspondente na autenticação é atualmente um detalhe de implementação do Manipulador de Autenticação do Seletor de Logon do Adobe Granite ( `com.day.cq.auth.impl.LoginSelectorHandler`), que é um Manipulador de Autenticação do Apache Sling configurado com AEM por padrão.

Ao chamar `AuthenticationHandler.requestCredentials`, esse manipulador tenta determinar a página de logon de mapeamento para a qual o usuário será redirecionado. Isso inclui as seguintes etapas:

* Distinguir entre a senha expirada e a necessidade de fazer logon regularmente como motivo do redirecionamento;
* No caso de um logon regular, o testa se um caminho de logon pode ser obtido na seguinte ordem:

   * do LoginPathProvider conforme implementado pelo novo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * da implementação antiga e obsoleta do CUG,
   * nos Mapeamentos de página de logon, conforme definido com o `LoginSelectorHandler`,
   * e, por fim, retorne à Página de logon padrão, conforme definido com o `LoginSelectorHandler`.

* Assim que um caminho de logon válido for obtido por meio das chamadas listadas acima, a solicitação do usuário será redirecionada para essa página.

O target desta documentação é a avaliação do caminho de logon como exposto pela interface interna `LoginPathProvider`. A implementação enviada desde o AEM 6.3 se comporta da seguinte maneira:

* O registro de caminhos de logon depende da distinção entre senha expirada e a necessidade de logon regular como motivo do redirecionamento
* No caso de logon regular, o testa se um caminho de logon pode ser obtido na seguinte ordem:

   * do `LoginPathProvider` conforme implementado pelo novo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * da implementação antiga e obsoleta do CUG,
   * nos Mapeamentos de página de logon, conforme definido com o `LoginSelectorHandler`,
   * e, por fim, voltar para a Página de logon padrão, conforme definido com o `LoginSelectorHandler`.

* Assim que um caminho de logon válido for obtido por meio das chamadas listadas acima, a solicitação do usuário será redirecionada para essa página.

O `LoginPathProvider` conforme implementado pelo novo suporte a requisito de autenticação no Granite expõe os caminhos de logon conforme definido pelas propriedades `granite:loginPath`, que, por sua vez, são definidas pelo tipo mixin conforme descrito acima. O mapeamento do caminho do recurso que mantém o caminho de logon e o próprio valor da propriedade são mantidos na memória e serão avaliados para localizar um caminho de logon adequado para outros nós na hierarquia.

>[!NOTE]
>
>A avaliação é executada somente para solicitações associadas a recursos localizados nos caminhos compatíveis configurados. Para quaisquer outras solicitações, as maneiras alternativas de determinar o caminho de logon serão avaliadas.

#### Práticas recomendadas     {#best-practices-1}

As práticas recomendadas a seguir devem ser consideradas ao definir os requisitos de autenticação:

* Evite aninhar os requisitos de autenticação: colocar um único marcador de requisito de autenticação no início de uma árvore deve ser suficiente e é herdado para toda a subárvore definida pelo nó de destino. Os requisitos de autenticação adicionais nessa árvore devem ser considerados redundantes e podem levar a problemas de desempenho ao avaliar o requisito de autenticação no Apache Sling. Com a separação das áreas de CUG relacionadas à autorização e autenticação, é possível restringir o acesso de leitura por meio de CUG ou outro tipo de política, ao mesmo tempo que impõe a autenticação para toda a árvore.
* Conteúdo do repositório de modelo de modo que os requisitos de autenticação se apliquem a toda a árvore sem a necessidade de excluir novamente subárvores aninhadas do requisito.
* Para evitar especificar e registrar subsequentemente caminhos de login redundantes:

   * confiar na herança e evitar definir caminhos de logon aninhados,
   * não defina o caminho de logon opcional como um valor que corresponda ao valor padrão ou herdado,
   * os desenvolvedores de aplicativos devem identificar quais caminhos de login devem ser configurados nas configurações globais de caminho de login (padrão e mapeamentos) associadas ao `LoginSelectorHandler`.

## Representação no Repositório {#representation-in-the-repository}

### Representação de Política de CUG no Repositório {#cug-policy-representation-in-the-repository}

A documentação do Oak cobre como as novas políticas CUG são refletidas no conteúdo do repositório. Para obter mais informações, consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Requisito de autenticação no repositório {#authentication-requirement-in-the-repository}

A necessidade de um requisito de autenticação separado é refletida no conteúdo do repositório com um tipo de nó mixin dedicado colocado no nó de destino. O tipo mixin define uma propriedade opcional para especificar uma página de logon dedicada para a árvore definida pelo nó do público-alvo.

A página associada ao caminho de logon pode estar localizada dentro ou fora dessa árvore. Ele será excluído do requisito de autenticação.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gerenciando Políticas e Requisito de Autenticação do CUG {#managing-cug-policies-and-authentication-requirement}

### Gerenciando Políticas de CUG {#managing-cug-policies}

O novo tipo de políticas de controle de acesso para restringir o acesso de leitura para um CUG é gerenciado usando a API de gerenciamento de controle de acesso JCR e segue os mecanismos descritos com a [especificação JCR 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Definir uma nova política CUG {#set-a-new-cug-policy}

Código para aplicar uma nova política CUG em um nó que não tinha um CUG definido anteriormente. Observe que `getApplicablePolicies` retornará somente novas políticas que não foram definidas anteriormente. No final, a política precisa de ser reformulada e as alterações precisam de ser mantidas.

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
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Editar uma Política CUG Existente {#edit-an-existing-cug-policy}

As etapas a seguir são necessárias para editar uma política CUG existente. Observe que a política modificada precisa ser gravada novamente e as alterações precisam ser persistentes usando `javax.jcr.Session.save()`.

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

### Recuperar Políticas Efetivas de CUG {#retrieve-effective-cug-policies}

O gerenciamento de controle de acesso JCR define um método de melhor esforço para recuperar as políticas que entrarão em vigor em um determinado caminho. Devido ao fato de que a avaliação das políticas de CUG é condicional e depende da configuração correspondente a ser habilitada, chamar `getEffectivePolicies` é uma maneira conveniente de verificar se uma determinada política de CUG está entrando em vigor em uma determinada instalação.

>[!NOTE]
>
>Observe a diferença entre `getEffectivePolicies` e o exemplo de código subsequente que sobe a hierarquia para descobrir se um determinado caminho já faz parte de um CUG existente.

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

#### Recuperar Políticas de CUG Herdadas {#retrieve-inherited-cug-policies}

Encontrar todos os CUGs aninhados que foram definidos em um determinado caminho independentemente de terem ou não efeito. Para obter mais informações, consulte a seção [Opções de configuração](/help/sites-administering/closed-user-groups.md#configuration-options) .

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

#### Gerenciando Políticas de CUG por Pincipal {#managing-cug-policies-by-pincipal}

As extensões definidas por `JackrabbitAccessControlManager` que permitem editar as políticas de controle de acesso por princípio não são implementadas com o gerenciamento de controle de acesso CUG, pois, por definição, uma política CUG sempre afeta todos os principais: os listados com o `PrincipalSetPolicy` recebem acesso de leitura, enquanto todos os outros principals serão impedidos de ler o conteúdo na árvore definida pelo nó de destino.

Os métodos correspondentes sempre retornam um conjunto de políticas vazio, mas não lançarão exceções.

### Gerenciamento do requisito de autenticação {#managing-the-authentication-requirement}

A criação, modificação ou remoção de novos requisitos de autenticação é realizada alterando o tipo de nó efetivo do nó de destino. A propriedade opcional de caminho de login pode ser gravada usando a API JCR comum.

>[!NOTE]
>
>As modificações em um determinado nó de destino mencionado acima serão refletidas somente no Apache Sling Authenticator se `RequirementHandler` tiver sido configurado e o destino estiver contido nas árvores definidas pelos caminhos suportados (consulte a seção Opções de configuração).
>
>Para obter mais informações, consulte [Atribuição de tipos de nó Mixin](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Atribuição de tipos de nó Mixin) e [Adição de nós e propriedades de configuração](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Adição de nós e propriedades de configuração)

#### Adicionar um novo requisito de autenticação {#adding-a-new-auth-requirement}

As etapas para criar um novo requisito de autenticação estão detalhadas abaixo. Observe que o requisito só será registrado com o Apache Sling Authenticator se `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Adicionar um novo requisito de autenticação com o caminho de logon {#add-a-new-auth-requirement-with-login-path}

Etapas para criar um novo requisito de autenticação, incluindo um caminho de logon. Observe que o requisito e a exclusão para o caminho de logon só serão registrados com o Apache Sling Authenticator se `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificar um caminho de logon existente {#modify-an-existing-login-path}

As etapas para alterar um caminho de logon existente são detalhadas abaixo. A modificação só será registrada com o Apache Sling Authenticator se `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino. O valor do caminho de logon anterior será removido do registro. O requisito de autenticação associado ao nó de destino não é afetado por essa modificação.

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

Etapas para remover um caminho de logon existente. A entrada do caminho de logon só será cancelada do registro do Apache Sling Authenticator se `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino. O requisito de autenticação associado ao nó de destino não é afetado.

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

Ou você pode usar o método abaixo para atingir a mesma finalidade:

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

Etapas para remover um requisito de autenticação existente. O requisito só será cancelado de registro do Apache Sling Authenticator se `RequirementHandler` tiver sido configurado para a árvore que contém o nó de destino.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recuperar requisitos de autenticação efetivos {#retrieve-effective-auth-requirements}

Não há API pública dedicada para ler todos os requisitos de autenticação efetivos conforme registrado no Apache Sling Authenticator. No entanto, a lista é exposta no console do sistema em `https://<serveraddress>:<serverport>/system/console/slingauth` na seção &quot;**Configuração de requisito de autenticação**&quot;.

A imagem a seguir mostra os requisitos de autenticação de uma instância de publicação de AEM com conteúdo de demonstração. O caminho destacado da página da comunidade ilustra como um requisito adicionado pela implementação descrita neste documento é refletido no Apache Sling Authenticator.

>[!NOTE]
>
>Neste exemplo, a propriedade de caminho de logon opcional não foi definida. Consequentemente, não foi registrada uma segunda entrada no autenticador.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Recuperar o caminho de logon efetivo {#retrieve-the-effective-login-path}

No momento, não há API pública para recuperar o caminho de logon que terá efeito ao acessar anonimamente um recurso que requer autenticação. Consulte a seção Avaliação do caminho de logon para obter detalhes de implementação sobre como o caminho de logon é recuperado.

No entanto, observe que, além dos caminhos de login definidos com esse recurso, há maneiras alternativas de especificar o redirecionamento para o logon, que devem ser consideradas ao projetar o modelo de conteúdo e os requisitos de autenticação de uma determinada instalação AEM.

#### Recuperar o requisito de autenticação herdado {#retrieve-the-inherited-auth-requirement}

Assim como no caminho de logon, não há API pública para recuperar os requisitos de autenticação herdados definidos no conteúdo. A amostra a seguir ilustra como listar todos os requisitos de autenticação que foram definidos com uma determinada hierarquia independentemente de terem efeito ou não. Para obter mais informações, consulte [Opções de configuração](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>É recomendável confiar no mecanismo de herança tanto para requisitos de autenticação e caminho de logon quanto para evitar a criação de requisitos de autenticação aninhados.
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

### Combinação de políticas CUG e do requisito de autenticação {#combining-cug-policies-and-the-authentication-requirement}

A tabela a seguir lista as combinações válidas de políticas CUG e o requisito de autenticação em uma instância AEM que tem ambos os módulos ativados por meio da configuração.

| **Autenticação necessária** | **Caminho de logon** | **Acesso de Leitura Restrito** | **Efeito esperado** |
|---|---|---|---|
| Sim | Sim | Sim | Um determinado usuário só poderá visualizar a subárvore marcada com a política CUG se uma avaliação de permissão efetiva conceder acesso. Um usuário não autenticado será redirecionado para a página de logon especificada. |
| Sim | Não | Sim | Um determinado usuário só poderá visualizar a subárvore marcada com a política CUG se uma avaliação de permissão efetiva conceder acesso. Um usuário não autenticado será redirecionado para uma página de logon padrão herdada. |
| Sim | Sim | Não | Um usuário não autenticado será redirecionado para a página de logon especificada. Se é permitido ou não exibir a árvore marcada com o requisito de autenticação, depende das permissões efetivas dos itens individuais contidos nessa subárvore. Nenhum CUG dedicado restringindo o acesso de leitura em vigor. |
| Sim | Não | Não | Um usuário não autenticado será redirecionado para uma página de logon padrão herdada. Se é permitido ou não exibir a árvore marcada com o requisito de autenticação, depende das permissões efetivas dos itens individuais contidos nessa subárvore. Nenhum CUG dedicado restringindo o acesso de leitura em vigor. |
| Não | Não | Sim | Um determinado usuário autenticado ou não autenticado só poderá visualizar a subárvore marcada com a política CUG se uma avaliação de permissão efetiva conceder acesso. Um usuário não autenticado será tratado igualmente e não será redirecionado para o logon. |

>[!NOTE]
>
>A combinação de &#39;Requisito de autenticação&#39; = Não e &#39;Caminho de logon&#39; = Sim não está listada acima, pois o &#39;Caminho de logon&#39; é um atributo opcional associado a um Requisito de autenticação. Especificar uma propriedade JCR com esse nome sem adicionar o tipo de mixin de definição não terá efeito e será ignorado pelo manipulador correspondente.

## Componentes e configuração do OSGi {#osgi-components-and-configuration}

Estas seções fornecem uma visão geral dos componentes OSGi e das opções de configuração individuais introduzidas com a nova implementação CUG.

Consulte também a documentação de mapeamento CUG para obter um mapeamento abrangente das opções de configuração entre a implementação antiga e a nova.

### Autorização: Configuração e configuração {#authorization-setup-and-configuration}

As novas partes relacionadas à autorização estão contidas no pacote **Oak CUG Authorization** ( `org.apache.jackrabbit.oak-authorization-cug`), que faz parte da instalação padrão AEM. O pacote define um modelo de autorização separado destinado a ser implantado como uma maneira adicional de gerenciar o acesso de leitura.

#### Configurando a Autorização de CUG {#setting-up-cug-authorization}

A configuração da autorização de CUG é descrita em detalhes na [documentação relevante do Apache](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Por padrão, AEM tem a autorização CUG implantada em todos os modos de execução. As instruções passo a passo também podem ser usadas para desativar a autorização de CUG nas instalações que requerem uma configuração de autorização diferente.

#### Configuração do filtro de referência {#configuring-the-referrer-filter}

Você também precisa configurar o [Filtro do Referenciador do Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) com todos os nomes de host que podem ser usados para acessar AEM; por exemplo, via CDN, Balanceador de carga e qualquer outro.

Se o filtro do referenciador não estiver configurado, erros, semelhantes aos seguintes, serão vistos quando um usuário tentar fazer logon em um site CUG:

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
   <td>Etiqueta</td>
   <td>Configuração do Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>Configuração de autorização dedicada à configuração e avaliação das permissões de CUG.</td>
  </tr>
  <tr>
   <td>Propriedades de configuração</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Além disso, consulte <a href="#configuration-options">Opções de configuração</a> abaixo.</p> </td>
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
   <td>Etiqueta</td>
   <td>Lista de exclusões do Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>Permite excluir o(s) principal(s) com o(s) nome(s) configurado(s) da avaliação de CUG.</td>
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
* `cugEnabled`: opção de configuração para habilitar a avaliação de permissão para as políticas CUG atuais.

As opções de configuração disponíveis associadas ao módulo de autorização de CUG são listadas e descritas com mais detalhes na [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Excluindo Principais da Avaliação de CUG {#excluding-principals-from-cug-evaluation}

Foi adotada a isenção de fundos próprios individuais da avaliação do CUG relativamente à anterior aplicação. A nova autorização de CUG cobre isso com uma interface dedicada chamada CugExclude. O Apache Jackrabbit Oak 1.4 é fornecido com uma implementação padrão que exclui um conjunto fixo de principais, bem como uma implementação estendida que permite configurar nomes de principais individuais. O último é configurado AEM instâncias de publicação.

O padrão desde o AEM 6.3 impede que os seguintes principais sejam afetados pelas políticas de CUG:

* principais administrativos (usuário administrador, grupo de administradores)
* principais de usuários de serviços
* principal do sistema interno do repositório

Para obter mais informações, consulte a tabela na seção [Configuração padrão desde AEM 6.3](#default-configuration-since-aem) abaixo.

A exclusão do grupo &#39;administradores&#39; pode ser alterada ou expandida no console do sistema na seção de configuração de **Apache Jackrabbit Oak CUG Exclude List**.

Como alternativa, é possível fornecer e implantar uma implementação personalizada da interface CugExclude para ajustar o conjunto de principais excluídos em caso de necessidades especiais. Consulte a documentação em [CUG pluggability](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obter detalhes e um exemplo de implementação.

### Autenticação: Configuração e configuração {#authentication-setup-and-configuration}

As novas partes relacionadas à autenticação estão contidas no pacote **Adobe Granite Authentication Handler** ( `com.adobe.granite.auth.authhandler` versão 5.6.48). Este pacote faz parte da instalação padrão AEM.

Para configurar a substituição do requisito de autenticação para o suporte obsoleto ao CUG, alguns componentes do OSGi devem estar presentes e ativos em uma determinada instalação AEM. Para obter mais detalhes, consulte **Características dos componentes OSGi** abaixo.

>[!NOTE]
>
>Devido à opção de configuração obrigatória com o RequerienteHandler, as partes relacionadas à autenticação só estarão ativas se o recurso tiver sido ativado ao especificar um conjunto de caminhos suportados. Com uma instalação de AEM padrão, o recurso é desativado no modo de execução do autor e ativado para /content no modo de execução de publicação.

**Características dos componentes OSGi**

Os 2 componentes OSGi a seguir foram introduzidos para definir requisitos de autenticação e especificar caminhos de logon dedicados:

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirements.impl.RequirementsService**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>O serviço OSGi dedicado para requisitos de autenticação que registra um observador para alterações de conteúdo que afetam o requisito de autenticação (por meio do tipo mixin <code>granite:AuthenticationRequirement</code>) e os caminhos de login com são expostos ao <code>LoginSelectorHandler</code>. </td>
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

**com.adobe.granite.auth.requirements.impl.DefaultRequirementsHandler**

| Etiqueta | Requisito de autenticação do Adobe Granite e manipulador de caminho de logon |
|---|---|
| Descrição | `RequirementHandler` implementação que atualiza os requisitos de autenticação do Apache Sling e a exclusão correspondente para os caminhos de logon associados. |
| Propriedades de configuração | `supportedPaths` |
| Política de configuração | `ConfigurationPolicy.REQUIRE` |
| Referências | ND |

#### Opções de configuração {#configuration-options-1}

As partes relacionadas à autenticação da regravação do CUG são fornecidas apenas com uma única opção de configuração associada ao Requisito de Autenticação do Adobe Granite e ao Manipulador do Caminho de Logon:

**&quot;Requisitos de autenticação e manipulador de caminho de logon&quot;**

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
   <td>Definir&lt;Cadeia de Caracteres&gt;</td>
   <td>-</td>
   <td>Caminhos sob os quais os requisitos de autenticação serão respeitados por esse manipulador. Deixe essa configuração indefinida se quiser adicionar o tipo mixin <code>granite:AuthenticationRequirement</code> aos nós sem aplicá-los (por exemplo, em instâncias do autor). Se estiver faltando, o recurso será desativado. </td>
  </tr>
 </tbody>
</table>

## Configuração padrão desde o AEM 6.3 {#default-configuration-since-aem}

Por padrão, novas instalações de AEM usarão as novas implementações tanto para as partes relacionadas à autorização quanto à autenticação do recurso CUG. A implementação antiga &quot;Suporte a CUG (Adobe Granite Closed User Group)&quot; foi descontinuada e será desabilitada por padrão em todas as instalações de AEM. As novas implementações serão ativadas da seguinte maneira:

### Instâncias do autor {#author-instances}

| **&quot;Configuração Apache Jackrabbit Oak CUG&quot;** | **Explicação** |
|---|---|
| Caminhos compatíveis `/content` | O gerenciamento de controle de acesso para políticas CUG está habilitado. |
| FALSE Habilitado para Avaliação de CUG | A avaliação de permissão está desativada. As políticas de CUG não têm efeito. |
| Classificação | 200 | Consulte a documentação do Oak. |

>[!NOTE]
>
>Nenhuma configuração para **Apache Jackrabbit Oak CUG Exclude List** e **Adobe Granite Authentication Requirements e Login Path Handler** está presente nas instâncias de criação padrão.

### Publicar instâncias {#publish-instances}

| **&quot;Configuração Apache Jackrabbit Oak CUG&quot;** | **Explicação** |
|---|---|
| Caminhos compatíveis `/content` | O gerenciamento de controle de acesso para políticas CUG é ativado abaixo dos caminhos configurados. |
| Avaliação de CUG Ativada VERDADEIRO | A avaliação de permissão é ativada abaixo dos caminhos configurados. As políticas de CUG têm efeito em `Session.save()`. |
| Classificação | 200 | Consulte a documentação do Oak. |

| **&quot;Lista de exclusões do Apache Jackrabbit Oak CUG&quot;** | **Explicação** |
|---|---|
| Administradores de nomes principais | Exclui o principal de administradores da avaliação de CUG. |

| **&quot;Requisito de autenticação do Adobe Granite e manipulador de caminho de logon&quot;** | **Explicação** |
|---|---|
| Caminhos compatíveis `/content` | Os requisitos de autenticação conforme definidos no repositório por meio do tipo mixin `granite:AuthenticationRequired` têm efeito abaixo de `/content` em `Session.save()`. O Sling Authenticator é atualizado. A adição do tipo mixin fora dos caminhos suportados é ignorada. |

## Desabilitando o Requisito de Autenticação e Autorização CUG {#disabling-cug-authorization-and-authentication-requirement}

A nova implementação pode ser completamente desativada caso uma determinada instalação não utilize CUGs ou utilize diferentes meios de autenticação e autorização.

### Desativar Autorização de CUG {#disable-cug-authorization}

Consulte a documentação [CUG pluggability](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obter detalhes sobre como remover o modelo de autorização CUG da configuração de autorização composta.

### Desativar o requisito de autenticação {#disable-the-authentication-requirement}

Para desabilitar o suporte para o requisito de autenticação, conforme fornecido pelo módulo `granite.auth.authhandler`, é suficiente remover a configuração associada ao **Requisito de autenticação Adobe Granite e Manipulador de caminho de logon**.

>[!NOTE]
>
>Observe, no entanto, que a remoção da configuração não cancelará o registro do tipo mixin, que ainda era aplicável aos nós sem ter efeito.

## Interação com outros módulos {#interaction-with-other-modules}

### API Apache Jackrabbit {#apache-jackrabbit-api}

Para refletir o novo tipo de política de controle de acesso usada pelo modelo de autorização CUG, a API definida pelo Apache Jackrabbit foi estendida. Desde a versão 2.11.0 do módulo `jackrabbit-api` define uma nova interface chamada `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, que se estende de `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

O mecanismo de importação do Apache Jackrabbit FileVault foi ajustado para lidar com políticas de controle de acesso do tipo `PrincipalSetPolicy`.

### Distribuição de conteúdo do Apache Sling {#apache-sling-content-distribution}

Consulte a seção acima [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault).

### Replicação de Adobe Granite {#adobe-granite-replication}

O módulo de replicação foi ligeiramente ajustado para poder replicar as políticas de CUG entre diferentes instâncias de AEM:

* `DurboImportConfiguration.isImportAcl()` é interpretado literalmente e afetará somente as políticas de controle de acesso que implementam  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` respeitará essa configuração somente para ACLs verdadeiras
* Outras políticas, como instâncias `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` criadas pelo modelo de autorização CUG, sempre serão replicadas e a opção de configuração `DurboImportConfiguration.isImportAcl`() será ignorada.

Há uma limitação da replicação das políticas de CUG. Se uma determinada política CUG for removida sem remover o tipo de nó mixin correspondente `rep:CugMixin,`, a remoção não será refletida na replicação. Isto tem sido resolvido sempre eliminando a mistura após a remoção das políticas. A limitação pode, no entanto, aparecer se o tipo mixin for adicionado manualmente.

### Manipulador de autenticação do Adobe Granite {#adobe-granite-authentication-handler}

O manipulador de autenticação **Adobe Granite HTTP Header Authentication Handler** fornecido com o pacote `com.adobe.granite.auth.authhandler` contém uma referência à interface `CugSupport` definida pelo mesmo módulo. É usado para calcular o &#39;realm&#39; em determinadas circunstâncias, voltando para o realm configurado com o manipulador.

Isso foi ajustado para tornar a referência a `CugSupport` opcional, a fim de garantir a compatibilidade retroativa máxima se uma determinada configuração decidir reativar a implementação obsoleta. As instalações que usam a implementação não obterão mais o realm extraído da implementação CUG, mas sempre exibirão o realm conforme definido com **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>Por padrão, o **Adobe Granite HTTP Header Authentication Handler** só é configurado no modo de execução de publicação com a opção &quot;Desativar página de logon&quot; ( `auth.http.nologin`) ativada.

### AEM LiveCopy {#aem-livecopy}

A configuração de CUGs junto com o LiveCopy é representada no repositório pela adição de um nó extra e uma propriedade extra, da seguinte maneira:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ambos os elementos são criados em `cq:Page`. Com o design atual, o MSM manipula apenas nós e propriedades que estão sob o nó `cq:PageContent` (`jcr:content`).

Portanto, os grupos CUG não podem ser distribuídos para Live Copies de Blueprints. Planeje isso ao configurar a Live Copy.

## Alterações com a Nova Implementação de CUG {#changes-with-the-new-cug-implementation}

O objetivo desta seção é fornecer uma visão geral das alterações feitas ao recurso CUG, bem como uma comparação entre a implementação antiga e a nova. Ele lista as alterações que afetam a forma como o suporte ao CUG é configurado e descreve como e por quem os CUGs são gerenciados no conteúdo do repositório.

### Diferenças na configuração e configuração do CUG {#differences-in-cug-setup-and-configuration}

O componente OSGi obsoleto **Adobe Granite Closed User Group (CUG) Support** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) foi substituído por novos componentes para poder manipular separadamente as partes relacionadas à autorização e autenticação da antiga funcionalidade CUG.

## Diferenças no gerenciamento de CUGs no conteúdo do repositório {#differences-in-managing-cugs-in-the-repository-content}

As seções a seguir descrevem as diferenças entre as implementações antigas e novas das perspectivas de implementação e segurança. Embora a nova implementação tenha como objetivo fornecer a mesma funcionalidade, há alterações sutis que são importantes saber ao usar o novo CUG.

### Diferenças Em Matéria De Autorização {#differences-with-regards-to-authorization}

As principais diferenças do ponto de vista da autorização são resumidas na lista seguinte:

**Conteúdo de Controle de Acesso Dedicado para CUGs**

Na implementação antiga, o modelo de autorização padrão era usado para manipular as políticas da lista de controle de acesso na publicação, substituindo quaisquer ACEs existentes pela configuração exigida pelo CUG. Isso foi acionado ao escrever propriedades JCR regulares e residuais que foram interpretadas na publicação.

Com a nova implementação, a configuração do controle de acesso do modelo de autorização padrão não é afetada por nenhum CUG que está sendo criado, modificado ou removido. Em vez disso, um novo tipo de política chamado `PrincipalSetPolicy` é aplicado como conteúdo de controle de acesso adicional ao nó de destino. Essa política adicional estará localizada como um filho do nó de destino e seria um irmão do nó de política padrão, se presente.

**Editando Políticas de CUG no Gerenciamento de Controle de Acesso**

Essa mudança de propriedades residuais do JCR para uma política de controle de acesso dedicada tem impacto na permissão necessária para criar ou modificar a parte de autorização do recurso CUG. Como isso é considerado uma modificação para acessar o conteúdo de controle, ele requer os privilégios `jcr:readAccessControl` e `jcr:modifyAccessControl` para ser gravado no repositório. Portanto, somente os autores de conteúdo autorizados a modificar o conteúdo de controle de acesso de uma página podem configurar ou modificar esse conteúdo. Isso contrasta com a implementação antiga, na qual a capacidade de gravar propriedades JCR regulares era suficiente, resultando em um escalonamento de privilégios.

**Nó De Destino Definido Pela Política**

Espera-se que as políticas de CUG sejam criadas no nó JCR que define a subárvore a ser sujeita a acesso de leitura restrito. Essa provavelmente será uma página AEM caso o CUG afete a árvore inteira.

Observe que colocar a política CUG somente no nó jcr:content localizado abaixo de uma determinada página restringirá o acesso ao conteúdo s.str de uma determinada página, mas não terá efeito em quaisquer páginas irmãs ou páginas filhas. Esse pode ser um caso de uso válido e é possível fazer isso com um editor de repositório que permite aplicar conteúdo de acesso refinado. No entanto, contrasta a implementação anterior, em que a colocação de uma propriedade cq:cugEnabled no nó jcr:content foi remapeada internamente para o nó da página. Esse mapeamento não é mais executado.

**Avaliação de Permissão com Políticas de CUG**

Mudar do suporte antigo a CUG para um modelo de autorização adicional altera a maneira como as permissões de leitura efetivas são avaliadas. Conforme descrito na [documentação do Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), um determinado principal permitido visualizar o `CUGcontent` só terá acesso de leitura se a avaliação de permissão de todos os modelos configurados no repositório Oak conceder acesso de leitura.

Em outras palavras, para a avaliação das permissões efetivas, tanto as entradas `CUGPolicy` quanto as entradas padrão de controle de acesso serão consideradas e o acesso de leitura no conteúdo CUG só será concedido se for concedido por ambos os tipos de políticas. Em uma instalação de publicação de AEM padrão em que o acesso de leitura à árvore completa `/content` é concedido para todos, o efeito das políticas de CUG será o mesmo da implementação antiga.

**Avaliação por demanda**

O modelo de autorização CUG permite ativar individualmente o gerenciamento de controle de acesso e a avaliação de permissão:

* o gerenciamento do controle de acesso será ativado se o módulo tiver um ou vários caminhos compatíveis, onde os CUGs podem ser criados
* a avaliação de permissão só será ativada se a opção **CUG Evaluation Enabled** estiver marcada adicionalmente.

Na nova AEM avaliação de configuração padrão das políticas de CUG, ela só é ativada com o modo de execução &quot;publicar&quot;. Consulte os detalhes sobre a configuração padrão [desde o AEM 6.3](#default-configuration-since-aem) para obter mais detalhes. Isso pode ser verificado comparando as políticas eficazes de um determinado caminho com as políticas armazenadas no conteúdo. Políticas eficazes serão exibidas somente no caso de a avaliação de permissão para CUGs estar habilitada.

Como explicado acima, as políticas de controle de acesso CUG agora são sempre armazenadas no conteúdo, mas a avaliação das permissões efetivas que resultam dessas políticas só será aplicada se **CUG Evaluation Enabled** estiver ativada no console do sistema na Configuração do Apache Jackrabbit Oak **CUG.** Por padrão, ele é ativado somente com o modo de execução &quot;publicar&quot;.

### Diferenças Em Relação À Autenticação {#differences-with-regards-to-authentication}

As diferenças em relação à autenticação são descritas abaixo.

#### Tipo De Mistura Dedicado Para Requisitos De Autenticação {#dedicated-mixin-type-for-authentication-requirement}

Na implementação anterior, tanto os aspectos de autorização quanto de autenticação de um CUG foram acionados por uma única propriedade JCR ( `cq:cugEnabled`). No que diz respeito à autenticação, isso resultou em uma lista atualizada de requisitos de autenticação como armazenados com a implementação do Apache Sling Authenticator. Com a nova implementação, o mesmo resultado é obtido ao marcar o nó do target com um tipo mixin dedicado ( `granite:AuthenticationRequired`).

#### Propriedade Para Excluir O Caminho De Logon {#property-for-excluding-login-path}

O tipo mixin define uma única propriedade opcional chamada `granite:loginPath`, que corresponde basicamente à propriedade `cq:cugLoginPage`. Em contraste com a implementação anterior, a propriedade de caminho de logon só será respeitada se o tipo de nó declarativo for o mixin mencionado. Adicionar uma propriedade com esse nome sem definir o tipo mixin não terá efeito e nem um novo requisito nem uma exclusão para o caminho de logon serão relatados ao autenticador.

#### Requisito De Privilégio Para Autenticação {#privilege-for-authentication-requirement}

Adicionar ou remover um tipo mixin requer que o privilégio `jcr:nodeTypeManagement` seja concedido. Na implementação anterior, o privilégio `jcr:modifyProperties` é usado para editar a propriedade residual.

No que diz respeito a `granite:loginPath`, é necessário o mesmo privilégio para adicionar, modificar ou remover a propriedade.

#### Nó De Destino Definido Pelo Tipo De Mistura {#target-node-defined-by-mixin-type}

Espera-se que os requisitos de autenticação sejam criados no nó JCR que define a subárvore a ser sujeita ao logon forçado. É provável que seja uma Página AEM caso o CUG afete toda a árvore e a interface do usuário para a nova implementação adicionará, consequentemente, o tipo de mixin de requisito de autenticação no nó da página.

Colocar a política CUG somente no nó jcr:content localizado abaixo de uma determinada página restringirá o acesso ao conteúdo, mas não terá efeito no próprio nó da página nem em nenhuma página filho.

Esse pode ser um cenário válido e é possível com um editor de repositório que permite colocar o mixin em qualquer nó. No entanto, o comportamento contrasta a implementação anterior, onde colocar uma propriedade cq:cugEnabled ou cq:cugLoginPage no nó jcr:content foi remapeada internamente no nó da página. Esse mapeamento não é mais executado.

#### Caminhos compatíveis configurados {#configured-supported-paths}

Tanto o tipo mixin `granite:AuthenticationRequired` quanto a propriedade granite:loginPath só serão respeitados dentro do escopo definido pelo conjunto da opção de configuração **Caminhos Suportados** presente com o **Requisito de Autenticação do Adobe Granite e Manipulador de Caminho de Logon**. Se nenhum caminho for especificado, o recurso de requisito de autenticação será desativado completamente. Nesse caso, o tipo mixin ou a propriedade têm efeito ao serem adicionados ou definidos para um determinado nó JCR.

### Mapeamento de conteúdo JCR, serviços e configurações OSGi {#mapping-of-jcr-content-osgi-services-and-configurations}

O documento abaixo fornece um mapeamento abrangente dos serviços OSGi, configurações e conteúdo do repositório entre a implementação antiga e a nova.

Mapeamento CUG desde AEM 6.3

[Obter arquivo](assets/cug-mapping.pdf)

## Atualizar CUG {#upgrade-cug}

### Instalações existentes usando o CUG obsoleto {#existing-installations-using-the-deprecated-cug}

A implementação de suporte para CUG antiga foi descontinuada e será removida para em versões futuras. É recomendável migrar para as novas implementações ao atualizar de versões anteriores à AEM 6.3.

Para a instalação AEM atualizada, é importante garantir que apenas uma implementação CUG esteja habilitada. A combinação do novo e do antigo suporte a CUG obsoleto não é testada e provavelmente causará um comportamento indesejado:

* colisões no Sling Authenticator no que diz respeito aos requisitos de autenticação
* negado acesso de leitura quando a configuração da ACL associada ao CUG antigo colida com uma nova política CUG.

### Migração de Conteúdo CUG Existente {#migrating-existing-cug-content}

O Adobe fornece uma ferramenta para migrar para a nova implementação CUG. Para usá-lo, execute as seguintes etapas:

1. Vá para `https://<serveraddress>:<serverport>/system/console/cug-migration` para acessar a ferramenta.
1. Insira o caminho raiz para o qual você deseja verificar os CUGs e pressione o botão **Execute dry run**. Isso verificará os CUGs elegíveis para conversão no local selecionado.
1. Depois de revisar os resultados, pressione o botão **Executar migração** para migrar para a nova implementação.

>[!NOTE]
>
>Se tiver problemas, é possível configurar um logger específico no nível **DEBUG** em `com.day.cq.auth.impl.cug` para obter a saída da ferramenta de migração. Consulte [Registro](/help/sites-deploying/configure-logging.md) para obter mais informações sobre como fazer isso.
