---
title: Grupos de usuários fechados em AEM
seo-title: Grupos de usuários fechados em AEM
description: Saiba mais sobre Grupos de usuários fechados em AEM.
seo-description: Saiba mais sobre Grupos de usuários fechados em AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
translation-type: tm+mt
source-git-commit: 2142df4f7579e052e18879b437fc43911010b475
workflow-type: tm+mt
source-wordcount: '6890'
ht-degree: 0%

---


# Grupos de usuários fechados em AEM{#closed-user-groups-in-aem}

## Introdução {#introduction}

Desde a AEM 6.3, há uma nova implementação do Grupo de usuários fechado destinada a resolver os problemas de desempenho, escalabilidade e segurança presentes na implementação existente.

>[!NOTE]
>
>Por uma questão de simplicidade, a abreviação do CUG será utilizada ao longo desta documentação.

O objetivo da nova implementação é cobrir a funcionalidade existente quando necessário e, ao mesmo tempo, resolver problemas e limitações de design de versões mais antigas. O resultado é um novo design de CUG com as seguintes características:

* Separação clara dos elementos de autenticação e autorização, que podem ser utilizados individualmente ou em combinação;
* Modelo de autorização dedicado para refletir o acesso restrito de leitura nas árvores de CUG configuradas, sem interferir com outros requisitos de configuração e permissão do controle de acesso;
* Separação entre a configuração do controle de acesso do acesso de leitura restrito, que geralmente é necessário em instâncias de criação, e a avaliação de permissão, que geralmente só é desejada na publicação;
* Edição de acesso restrito de leitura sem escalonamento de privilégios;
* Extensão de tipo de nó dedicada para marcar o requisito de autenticação;
* Caminho de logon opcional associado ao requisito de autenticação.

### A nova implementação personalizada do grupo de usuários {#the-new-custom-user-group-implementation}

Um CUG, como é conhecido no contexto do AEM, consiste nas seguintes etapas:

* Restrinja o acesso de leitura na árvore que precisa ser protegida e permita somente a leitura de principais listados com uma determinada instância CUG ou excluídos da avaliação CUG. Isso é chamado de elemento **license**.
* Impor autenticação em uma determinada árvore e, opcionalmente, especificar uma página de logon dedicada para essa árvore que será excluída subsequentemente. Isso é chamado de elemento **authentication**.

A nova implementação foi concebida para estabelecer uma linha entre a autenticação e os elementos de autorização. A partir do AEM 6.3, é possível restringir o acesso de leitura sem adicionar explicitamente um requisito de autenticação. Por exemplo, se uma determinada instância exigir autenticação completamente ou uma determinada árvore já residir em uma subárvore que já requer autenticação.

Da mesma forma, determinada árvore pode ser marcada com um requisito de autenticação sem alterar a configuração de permissão efetiva. As combinações e os resultados estão listados na seção [Combinando políticas CUG e o requisito de autenticação](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement).

## Visão geral {#overview}

### Autorização: Restrição do acesso de leitura {#authorization-restricting-read-access}

O recurso principal de um CUG está restringindo o acesso de leitura em uma determinada árvore no repositório de conteúdo para todos, exceto os principais selecionados. Em vez de manipular o conteúdo padrão do controle de acesso imediatamente, a nova implementação adota uma abordagem diferente definindo um tipo dedicado de política de controles de acesso que representa um CUG.

#### Política de controle de acesso para CUG {#access-control-policy-for-cug}

Este novo tipo de política tem as seguintes características:

* Política de controle de acesso do tipo org.apache.Jackrabbit.api.security.entitlement.PrincipalSetPolicy (definido pela API Apache Jackrabbit);
* PrincipalSetPolicy concede privilégios a um conjunto modificável de principais;
* Os privilégios concedidos e o âmbito da política são um detalhe de implementação.

A implementação de PrincipalSetPolicy usada para representar CUGs além disso define que:

* As políticas CUG só concedem acesso de leitura a itens JCR regulares (por exemplo, o conteúdo do controle de acesso é excluído);
* O escopo é definido pelo nó controlado de acesso que detém a política CUG;
* As políticas CUG podem ser aninhadas, um CUG aninhado start um novo CUG sem herdar o conjunto principal do CUG &#39;pai&#39;;
* O efeito da política, se a avaliação estiver ativada, será herdado para toda a subárvore até o próximo CUG aninhado.

Essas políticas de CUG são implantadas em uma instância AEM por meio de um módulo de autorização separado, chamado de marcação de autorização de carvalho. Este módulo vem com seu próprio gerenciamento de controles de acesso e avaliação de permissões. Em outras palavras, a configuração de AEM padrão envia uma configuração de repositório de conteúdo Oak que combina vários mecanismos de autorização. Para obter mais informações, consulte [esta página na Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Nesta configuração composta, um novo CUG não substitui o conteúdo existente do controle de acesso anexado ao nó do público alvo, mas é projetado para ser um suplemento que também pode ser removido posteriormente sem afetar o controle de acesso original, que por padrão no AEM seria uma lista do controle de acesso.

Em contraste com a anterior implementação, as novas políticas de CUG são sempre reconhecidas e tratadas como conteúdo do controle de acesso. Isso implica que eles sejam criados e editados usando a API de gerenciamento de controles de acesso JCR. Para obter mais informações, consulte a seção [Gerenciando Políticas de CUG](#managing-cug-policies).

#### Avaliação de permissão das políticas de CUG {#permission-evaluation-of-cug-policies}

Além de um gerenciamento de controles de acesso dedicado para CUGs, o novo modelo de autorização permite condicionalmente habilitar a avaliação de permissões para suas políticas. Isso permite configurar políticas CUG em um ambiente de preparo e ativar somente a avaliação das permissões efetivas depois de replicadas para o ambiente de produção.

A avaliação de permissão para políticas CUG e a interação com o padrão ou qualquer modelo de autorização adicional seguem o padrão projetado para vários mecanismos de autorização no Apache Jackrabbit Oak: um determinado conjunto de permissões é concedido se e somente se todos os modelos concederem acesso. Consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) para obter mais detalhes.

As seguintes características se aplicam à avaliação de permissão associada ao modelo de autorização projetado para manipular e avaliar políticas de CUG:

* Ele só lida com permissões de leitura para nós e propriedades comuns, mas não lendo o conteúdo do controle de acesso
* Ele não lida com permissões de gravação nem com nenhum tipo de permissões necessárias para a modificação de conteúdo JCR protegido (controle de acesso, informações de tipo de nó, controle de versão, bloqueio ou gerenciamento de usuários, entre outros); Essas permissões não são afetadas por uma política CUG e não serão avaliadas pelo modelo de autorização associado. A concessão ou não dessas permissões depende dos outros modelos configurados na configuração de segurança.

O efeito de uma única política de CUG na avaliação das permissões pode resumir-se do seguinte modo:

* O acesso de leitura é negado a todos, exceto aos assuntos que contenham os principais ou principais excluídos enumerados na política;
* A política produz efeitos no nó controlado de acesso que detém a política e as suas propriedades;
* O efeito é adicionalmente herdado na hierarquia - isto é, a árvore de itens definida pelo nó controlado de acesso;
* No entanto, não afeta irmãos nem antepassados do nó controlado de acesso;
* A herança de um determinado CUG é interrompida em um CUG aninhado.

#### Práticas recomendadas     {#best-practices}

As práticas recomendadas a seguir devem ser levadas em conta para a definição de acesso restrito de leitura por meio de CUGs:

* Tome uma decisão consciente sobre se sua necessidade de um CUG é restringir o acesso de leitura ou um requisito de autenticação. No caso deste último, ou se houver necessidade de ambos, consulte a seção Práticas recomendadas para obter detalhes sobre o requisito de autenticação
* Crie um modelo de ameaça para os dados ou conteúdo que precisam ser protegidos para identificar os limites de ameaça e obter uma visão clara sobre a sensibilidade dos dados e as funções associadas ao acesso autorizado
* Modelar o conteúdo do repositório e os CUGs, tendo em mente aspectos e práticas recomendadas gerais relacionados à autorização:

   * Lembre-se de que a permissão de leitura só será concedida se um determinado CUG e a avaliação de outros módulos implantados na concessão de configuração permitirem que um determinado sujeito leia um determinado item do repositório
   * Evite criar CUGs redundantes onde o acesso de leitura já esteja restrito por outros módulos de autorização
   * A necessidade excessiva de CUGs aninhados pode potencialmente destacar problemas no design de conteúdo
   * Uma necessidade muito excessiva de CUGs (por exemplo, em cada página) pode indicar a necessidade de um modelo de autorização personalizado potencialmente mais adequado para atender às necessidades de segurança específicas do aplicativo e do conteúdo em questão.

* Limite os caminhos suportados para políticas CUG a algumas árvores no repositório para permitir desempenho otimizado. Por exemplo, permita apenas CUGs abaixo do nó /content como enviado como valor padrão desde AEM 6.3.
* As políticas de CUG são projetadas para conceder acesso de leitura a um pequeno conjunto de principais. A necessidade de um grande número de principais pode destacar problemas no conteúdo ou no design do aplicativo e deve ser reconsiderada.

### Autenticação: Definindo o requisito de autenticação {#authentication-defining-the-auth-requirement}

As partes relacionadas à autenticação do recurso CUG permitem marcar árvores que exigem autenticação e, opcionalmente, especificar uma página de logon dedicada. De acordo com a versão anterior, a nova implementação permite marcar árvores que exigem autenticação no repositório de conteúdo e ativar condicionalmente a sincronização com o `Sling org.apache.sling.api.auth.Authenticator`responsável por impor o requisito e redirecionar para um recurso de logon.

Esses requisitos são registrados no Autenticador por meio de um serviço OSGi que fornece a propriedade de registro `sling.auth.requirements`. Essas propriedades são então usadas para estender dinamicamente os requisitos de autenticação. Para obter mais detalhes, consulte a [documentação Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definindo o requisito de autenticação com um tipo de combinação dedicado {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Por motivos de segurança, a nova implementação substitui o uso de uma propriedade JCR residual por um tipo de combinação dedicada chamado `granite:AuthenticationRequired`, que define uma única propriedade opcional do tipo STRING para o caminho de logon `granite:loginPath`. Somente as alterações de conteúdo relacionadas a esse tipo de mixagem levarão à atualização dos requisitos registrados no Autenticador Apache Sling. As modificações são rastreadas após a persistência de modificações transitórias e, portanto, exigem uma chamada `javax.jcr.Session.save()` para se tornar efetiva.

O mesmo se aplica à propriedade `granite:loginPath`. Só será respeitado se for definido pelo tipo de mistura relacionado com os requisitos de autenticação. Adicionar uma propriedade residual com esse mesmo nome em um nó JCR não estruturado não mostrará o efeito desejado e a propriedade será ignorada pelo manipulador responsável pela atualização do registro OSGi.

>[!NOTE]
>
>A configuração da propriedade de caminho de login é opcional e só é necessária se a árvore que requer autenticação não puder voltar para a página de logon padrão ou herdada. Consulte [Avaliação do caminho de logon](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) abaixo.

#### Registrando o requisito de autenticação e o caminho de logon com o Sling Authenticator {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Como é esperado que esse tipo de requisito de autenticação esteja limitado a determinados modos de execução e a um pequeno subconjunto de árvores no repositório de conteúdo, o rastreamento do tipo de combinação necessário e das propriedades do caminho de login é condicional e vinculado a uma configuração correspondente que define os caminhos suportados (consulte Opções de configuração abaixo). Consequentemente, somente as alterações dentro do escopo desses caminhos suportados acionarão uma atualização do registro OSGi, em qualquer outro lugar, tanto o tipo de mixin quanto a propriedade serão ignorados.

A configuração de AEM padrão agora utiliza essa configuração permitindo definir a mixin no modo de execução do autor, mas só terá efeito na replicação para a instância de publicação. Consulte [esta página](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) para obter detalhes sobre como o Sling aplica o requisito de autenticação.

A adição do tipo de mistura `granite:AuthenticationRequired` nos caminhos suportados configurados fará com que o registro OSGi do manipulador responsável seja atualizado com uma nova entrada adicional com a propriedade `sling.auth.requirements`. Se um determinado requisito de autenticação especificar a propriedade opcional `granite:loginPath`, o valor será registrado adicionalmente com o Autenticador com um prefixo &#39;-&#39; para ser excluído do requisito de autenticação.

#### Avaliação e herança do requisito de autenticação {#evaluation-and-inheritance-of-the-authentication-requirement}

Espera-se que os requisitos de autenticação do Apache Sling sejam herdados por meio da hierarquia de página ou nó. Os próprios detalhes da herança e a avaliação dos requisitos de autenticação, como ordem e precedência, são considerados detalhes da implementação e não serão documentados neste artigo.

#### Avaliação do caminho de logon {#evaluation-of-login-path}

A avaliação do caminho de login e o redirecionamento para o recurso correspondente na autenticação é atualmente um detalhe de implementação do Manipulador de autenticação do Seletor de login de Granite do Adobe ( `com.day.cq.auth.impl.LoginSelectorHandler`), que é um Apache Sling AuthenticationHandler configurado com AEM por padrão.

Ao chamar `AuthenticationHandler.requestCredentials`, esse manipulador tenta determinar a página de logon de mapeamento para a qual o usuário será redirecionado. Isso inclui as seguintes etapas:

* Distinguir entre a senha expirada e a necessidade de login regular como motivo para o redirecionamento;
* No caso de um login regular, testa se um caminho de login pode ser obtido na seguinte ordem:

   * do LoginPathProvider conforme implementado pelo novo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * da implementação antiga e obsoleta do CUG,
   * nos Mapeamentos de página de logon, conforme definido com `LoginSelectorHandler`,
   * e, finalmente, retorne para a Página de logon padrão, conforme definido com `LoginSelectorHandler`.

* Assim que um caminho de logon válido for obtido por meio das chamadas listadas acima, a solicitação do usuário será redirecionada para essa página.

O público alvo desta documentação é a avaliação do caminho de logon como exposto pela interface interna `LoginPathProvider`. A implementação enviada desde AEM 6.3 comporta-se da seguinte forma:

* O registro de caminhos de login depende da distinção entre a senha expirada e a necessidade de login regular como motivo para o redirecionamento
* No caso de login regular, testa se um caminho de login pode ser obtido na seguinte ordem:

   * de `LoginPathProvider` conforme implementado pelo novo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * da implementação antiga e obsoleta do CUG,
   * nos Mapeamentos de Página de Logon, conforme definido com `LoginSelectorHandler`,
   * e, por fim, voltar para a Página de logon padrão, conforme definido com `LoginSelectorHandler`.

* Assim que um caminho de logon válido for obtido por meio das chamadas listadas acima, a solicitação do usuário será redirecionada para essa página.

O `LoginPathProvider`, conforme implementado pelo novo suporte de requisito de autenticação no Granite, expõe os caminhos de logon conforme definido pelas propriedades `granite:loginPath`, que, por sua vez, são definidas pelo tipo de combinação, conforme descrito acima. O mapeamento do caminho do recurso que contém o caminho de logon e o próprio valor da propriedade é mantido na memória e será avaliado para encontrar um caminho de logon adequado para outros nós na hierarquia.

>[!NOTE]
>
>A avaliação só é executada para solicitações associadas a recursos localizados nos caminhos suportados configurados. Para quaisquer outras solicitações, as formas alternativas de determinar o caminho de logon serão avaliadas.

#### Práticas recomendadas      {#best-practices-1}

Ao definir os requisitos de autenticação, devem ser tidas em conta as seguintes práticas recomendadas:

* Evite aninhar os requisitos de autenticação: colocar um único marcador de requisito de autenticação no start de uma árvore deve ser suficiente e é herdado para toda a subárvore definida pelo nó do público alvo. Os requisitos de autenticação adicionais dentro dessa árvore devem ser considerados redundantes e podem levar a problemas de desempenho ao avaliar o requisito de autenticação dentro do Apache Sling. Com a separação das áreas de autorização e autenticação relacionadas ao CUG, é possível restringir o acesso de leitura por meio do CUG ou de outro tipo de políticas, além de impor a autenticação para toda a árvore.
* Modelo do conteúdo do repositório de modo que os requisitos de autenticação se apliquem a toda a árvore sem a necessidade de excluir as subárvores aninhadas do requisito novamente.
* Para evitar especificar e, posteriormente, registrar caminhos de logon redundantes:

   * depender da herança e evitar definir caminhos de logon aninhados,
   * não defina o caminho de logon opcional para um valor que corresponda ao valor padrão ou herdado,
   * os desenvolvedores do aplicativo devem identificar quais caminhos de logon devem ser configurados nas configurações globais de caminho de login (padrão e mapeamentos) associadas ao `LoginSelectorHandler`.

## Representação no repositório {#representation-in-the-repository}

### Representação de política CUG no repositório {#cug-policy-representation-in-the-repository}

A documentação do Oak aborda como as novas políticas de CUG são refletidas no conteúdo do repositório. Para obter mais informações, consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Requisito de autenticação no repositório {#authentication-requirement-in-the-repository}

A necessidade de um requisito de autenticação separado é refletida no conteúdo do repositório com um tipo de nó de mixin dedicado colocado no nó do público alvo. O tipo de mixin define uma propriedade opcional para especificar uma página de logon dedicada para a árvore definida pelo nó do público alvo.

A página associada ao caminho de logon pode estar localizada dentro ou fora dessa árvore. Será excluído do requisito de autenticação.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gerenciando políticas e requisitos de autenticação do CUG {#managing-cug-policies-and-authentication-requirement}

### Gerenciando Políticas de CUG {#managing-cug-policies}

O novo tipo de políticas de controle de acesso para restringir o acesso de leitura para um CUG é gerenciado usando a API de gerenciamento de controles de acesso JCR e segue os mecanismos descritos com a especificação [JCR 2.0](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html).

#### Definir uma nova política de CUG {#set-a-new-cug-policy}

Código para aplicar uma nova política CUG em um nó que não tinha um CUG definido antes. Observe que `getApplicablePolicies` retornará somente novas políticas que não foram definidas antes. No final, a política precisa de ser reformulada e as mudanças precisam de ser mantidas.

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

#### Editar uma política de CUG existente {#edit-an-existing-cug-policy}

As etapas a seguir são necessárias para editar uma política de CUG existente. Observe que a política modificada precisa ser regravada e as alterações precisam ser mantidas usando `javax.jcr.Session.save()`.

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

### Recuperar Políticas de CUG Efetivas {#retrieve-effective-cug-policies}

O gerenciamento de controles de acesso JCR define um método de melhor esforço para recuperar as políticas que entram em vigor em um determinado caminho. Devido ao fato de que a avaliação das políticas CUG é condicional e depende da configuração correspondente para ser ativada, chamar `getEffectivePolicies` é uma maneira conveniente de verificar se determinada política CUG está sendo aplicada em uma determinada instalação.

>[!NOTE]
>
>Observe a diferença entre `getEffectivePolicies` e o exemplo de código subsequente que apresenta a hierarquia para descobrir se um determinado caminho já faz parte de um CUG existente.

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

Encontrar todos os CUGs aninhados que foram definidos em um determinado caminho independentemente de terem ou não efeito. Para obter mais informações, consulte a seção [Opções de configuração](/help/sites-administering/closed-user-groups.md#configuration-options).

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

#### Gerenciando políticas de CUG por princípio {#managing-cug-policies-by-pincipal}

As extensões definidas por `JackrabbitAccessControlManager` que permitem editar as políticas de controle de acesso por principal não são implementadas com o gerenciamento de controles de acesso CUG, já que, por definição, uma política CUG sempre afeta todos os principais: os listados com `PrincipalSetPolicy` recebem acesso de leitura, enquanto todos os outros principais serão impedidos de ler o conteúdo na árvore definida pelo nó do público alvo.

Os métodos correspondentes sempre retornam uma matriz de política vazia, mas não lançam exceções.

### Gerenciando o requisito de autenticação {#managing-the-authentication-requirement}

A criação, modificação ou remoção de novos requisitos de autenticação é alcançada pela alteração do tipo de nó efetivo do nó do público alvo. A propriedade opcional de caminho de login pode ser gravada usando a API JCR comum.

>[!NOTE]
>
>As modificações em determinado nó de público alvo mencionado acima serão refletidas somente no Autenticador Sling do Apache se `RequirementHandler` tiver sido configurado e o público alvo estiver contido nas árvores definidas pelos caminhos suportados (consulte as Opções de configuração da seção).
>
>Para obter mais informações, consulte [Atribuindo tipos de nós mistos](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Atribuindo tipos de nós mistos) e [Adicionando nós e definindo propriedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 adicionando nós e definindo propriedades)

#### Adicionando um novo requisito de autenticação {#adding-a-new-auth-requirement}

As etapas para criar um novo requisito de autenticação estão detalhadas abaixo. Observe que o requisito só será registrado com o Apache Sling Authenticator se `RequirementHandler` tiver sido configurado para a árvore que contém o nó do público alvo.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Adicionar um novo requisito de autenticação com caminho de logon {#add-a-new-auth-requirement-with-login-path}

Etapas para criar um novo requisito de autenticação incluindo um caminho de logon. Observe que os requisitos e a exclusão do caminho de logon só serão registrados com o Autenticador Apache Sling se `RequirementHandler` tiver sido configurado para a árvore que contém o nó do público alvo.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificar um caminho de logon existente {#modify-an-existing-login-path}

As etapas para alterar um caminho de login existente estão detalhadas abaixo. A modificação só será registrada com o Autenticador Apache Sling se `RequirementHandler` tiver sido configurado para a árvore que contém o nó do público alvo. O valor do caminho de login anterior será removido do registro. O requisito de autenticação associado ao nó do público alvo não é afetado por essa modificação.

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

Etapas para remover um caminho de logon existente. A entrada do caminho de logon só será cancelada do Autenticador Apache Sling se `RequirementHandler` tiver sido configurado para a árvore que contém o nó do público alvo. O requisito de autenticação associado ao nó do público alvo não é afetado.

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

Ou, você pode usar o método abaixo para atingir o mesmo objetivo:

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

Etapas para remover um requisito de autenticação existente. O requisito só será cancelado do Apache Sling Authenticator se `RequirementHandler` tiver sido configurado para a árvore que contém o nó do público alvo.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recuperar requisitos de autenticação efetivos {#retrieve-effective-auth-requirements}

Não há API pública dedicada para ler todos os requisitos de autenticação efetiva, conforme registrado no Autenticador Sling do Apache. No entanto, a lista é exposta no console do sistema em `https://<serveraddress>:<serverport>/system/console/slingauth` na seção &quot;**Authentication Requirements Configuration**&quot;.

A imagem a seguir mostra os requisitos de autenticação de uma instância de publicação AEM com conteúdo de demonstração. O caminho destacado da página da comunidade ilustra como um requisito adicionado pela implementação descrita neste documento é refletido no Apache Sling Authenticator.

>[!NOTE]
>
>Neste exemplo, a propriedade de caminho de login opcional não foi definida. Consequentemente, não foi registrada nenhuma segunda entrada no autenticador.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Recuperar o caminho de logon efetivo {#retrieve-the-effective-login-path}

No momento, não há API pública para recuperar o caminho de logon que entrará em vigor ao acessar anonimamente um recurso que requer autenticação. Consulte a seção Avaliação do caminho de logon para obter detalhes sobre a implementação de como o caminho de logon é recuperado.

Entretanto, observe que, além dos caminhos de logon definidos com esse recurso, há maneiras alternativas de especificar o redirecionamento para o logon, que devem ser levadas em consideração ao projetar o modelo de conteúdo e os requisitos de autenticação de uma determinada instalação AEM.

#### Recuperar o requisito de autenticação herdado {#retrieve-the-inherited-auth-requirement}

Como no caminho de logon, não há uma API pública para recuperar os requisitos de autenticação herdados definidos no conteúdo. A amostra a seguir ilustra como lista todos os requisitos de autenticação que foram definidos com uma hierarquia específica independentemente de terem ou não efeito. Para obter mais informações, consulte [Opções de configuração](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>É recomendável confiar no mecanismo de herança tanto para os requisitos de autenticação quanto para o caminho de logon e evitar a criação de requisitos de autenticação aninhados.
>
>Para obter mais informações, consulte [Requisito de avaliação e herança de autenticação](#evaluation-and-inheritance-of-the-authentication-requirement), [Avaliação do caminho de logon](#evaluation-of-login-path) e [Práticas recomendadas](#best-practices).

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

A tabela a seguir lista as combinações válidas de políticas CUG e o requisito de autenticação em uma instância AEM que tenha ambos os módulos habilitados por meio da configuração.

| **Autenticação necessária** | **Caminho de login** | **Acesso de Leitura Restrito** | **Efeito esperado** |
|---|---|---|---|
| Sim | Sim | Sim | Um determinado usuário só poderá visualização a subárvore marcada com a política CUG se uma avaliação de permissão efetiva conceder acesso. Um usuário não autenticado será redirecionado para a página de logon especificada. |
| Sim | Não | Sim | Um determinado usuário só poderá visualização a subárvore marcada com a política CUG se uma avaliação de permissão efetiva conceder acesso. Um usuário não autenticado será redirecionado para uma página de logon padrão herdada. |
| Sim | Sim | Não | Um usuário não autenticado será redirecionado para a página de logon especificada. Se é permitido ou não visualização a árvore marcada com o requisito de autenticação depende das permissões efetivas dos itens individuais contidos nessa subárvore. Nenhum CUG dedicado restringindo o acesso de leitura no local. |
| Sim | Não | Não | Um usuário não autenticado será redirecionado para uma página de logon padrão herdada. Se é permitido ou não visualização a árvore marcada com o requisito de autenticação depende das permissões efetivas dos itens individuais contidos nessa subárvore. Nenhum CUG dedicado restringindo o acesso de leitura no local. |
| Não | Não | Sim | Um determinado usuário autenticado ou não autenticado só poderá visualização a subárvore marcada com a política CUG se uma avaliação de permissão efetiva conceder acesso. Um usuário não autenticado será tratado igualmente e não será redirecionado para o logon. |

>[!NOTE]
>
>A combinação de &#39;Requisito de autenticação&#39; = Não e &#39;Caminho de logon&#39; = Sim não está listada acima, pois &#39;Caminho de logon&#39; é um atributo opcional associado a um Requisito de autenticação. A especificação de uma propriedade JCR com esse nome sem adicionar o tipo de combinação de definição não terá efeito e será ignorada pelo manipulador correspondente.

## Componentes e configuração do OSGi {#osgi-components-and-configuration}

Esta seção fornece uma visão geral dos componentes do OSGi e das opções de configuração individuais introduzidas com a nova implementação do CUG.

Consulte também a documentação de mapeamento CUG para obter um mapeamento abrangente das opções de configuração entre a implementação antiga e a nova.

### Autorização: Configuração {#authorization-setup-and-configuration}

As novas partes relacionadas à autorização estão contidas no pacote **Autorização Oak CUG** ( `org.apache.jackrabbit.oak-authorization-cug`), que faz parte da instalação padrão AEM. O pacote define um modelo de autorização separado que deve ser implantado como uma forma adicional de gerenciar o acesso de leitura.

#### Configurando a Autorização de CUG {#setting-up-cug-authorization}

A configuração da autorização CUG é descrita em detalhes na [documentação relevante do Apache](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Por padrão, AEM tem autorização CUG implantada em todos os modos de execução. As instruções passo a passo também podem ser usadas para desativar a autorização de CUG nas instalações que exigem uma configuração de autorização diferente.

#### Configuração do filtro de Quem indicou {#configuring-the-referrer-filter}

Você também precisa configurar o [Filtro de Quem indicou Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) com todos os nomes de host que podem ser usados para acessar AEM; por exemplo, por meio de CDN, Balanceador de Carga e qualquer outro.

Se o filtro de quem indicou não estiver configurado, serão observados erros, semelhantes aos seguintes, quando um usuário tentar fazer logon em um site CUG:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Características dos componentes OSGi {#characteristics-of-osgi-components}

Os dois componentes OSGi a seguir foram introduzidos para definir os requisitos de autenticação e especificar caminhos de logon dedicados:

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.Jackrabbit.oak.spi.security.authorized.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>Configuração do Apache Jackrabbit Oak CUG</td>
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

**org.apache.Jackrabbit.oak.spi.security.license.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>Apache Jackrabbit Oak CUG Excluir Lista</td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>Permite excluir o(s) principal(s) com os nomes configurados da avaliação CUG.</td>
  </tr>
  <tr>
   <td>Propriedades de configuração</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Consulte também as Opções de configuração da seção abaixo.</p> </td>
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

* `cugSupportedPaths`: especificar as subárvores que podem conter CUGs. Nenhum valor padrão está definido
* `cugEnabled`: opção de configuração para ativar a avaliação de permissão para as políticas atuais de CUG.

As opções de configuração disponíveis associadas ao módulo de autorização CUG são listadas e descritas com mais detalhes na [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Excluindo Principais da Avaliação de CUG {#excluding-principals-from-cug-evaluation}

Foi adotada a isenção dos principais individuais da avaliação da CUG relativamente à execução anterior. A nova autorização do CUG cobre isso com uma interface exclusiva chamada CugExclude. O Apache Jackrabbit Oak 1.4 é enviado com uma implementação padrão que exclui um conjunto fixo de principais, bem como uma implementação estendida que permite configurar nomes de principais individuais. O último é configurado em AEM instâncias de publicação.

O padrão desde AEM 6.3 impede que os seguintes principais sejam afetados pelas políticas de CUG:

* principais administrativos (usuário administrador, grupo de administradores)
* principais de usuários de serviços
* principal do sistema interno do repositório

Para obter mais informações, consulte a tabela na seção [Configuração padrão desde AEM 6.3](#default-configuration-since-aem) abaixo.

A exclusão do grupo &#39;administradores&#39; pode ser alterada ou expandida no console do sistema na seção de configuração de **Apache Jackrabbit Oak CUG Excluir Lista**.

Como alternativa, é possível fornecer e implantar uma implementação personalizada da interface CugExclude para ajustar o conjunto de principais excluídos em caso de necessidades especiais. Consulte a documentação em [Plug-ability](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obter detalhes e uma implementação de exemplo.

### Autenticação: Configuração {#authentication-setup-and-configuration}

As novas peças relacionadas à autenticação estão contidas no pacote **Adobe Granite Authentication Handler** ( `com.adobe.granite.auth.authhandler` versão 5.6.48). Este pacote faz parte da instalação padrão AEM.

Para configurar a substituição do requisito de autenticação para o suporte obsoleto ao CUG, alguns componentes do OSGi devem estar presentes e ativos em uma determinada instalação AEM. Para obter mais detalhes, consulte **Características dos componentes OSGi** abaixo.

>[!NOTE]
>
>Devido à opção de configuração obrigatória com o RequirementsHandler, as partes relacionadas à autenticação só estarão ativas se o recurso tiver sido ativado especificando um conjunto de caminhos suportados. Com uma instalação de AEM padrão, o recurso é desativado no modo de execução do autor e ativado para /content no modo de execução de publicação.

**Características dos componentes OSGi**

Os dois componentes OSGi a seguir foram introduzidos para definir os requisitos de autenticação e especificar caminhos de logon dedicados:

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
   <td>O serviço OSGi dedicado para requisitos de autenticação que registram um observador para alterações de conteúdo que afetam os requisitos de autenticação (por meio do tipo de mistura <code>granite:AuthenticationRequirement</code>) e caminhos de logon com são expostos ao <code>LoginSelectorHandler</code>. </td>
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

As partes relacionadas à autenticação da regravação de CUG só vêm com uma única opção de configuração associada ao Requisito de Autenticação de Granite do Adobe e ao Manipulador de Caminho de Logon:

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
   <td><p>Rótulo = Caminhos suportados</p> <p>Nome = 'supportedPaths'</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>Caminhos sob os quais os requisitos de autenticação serão respeitados por este manipulador. Deixe essa configuração indefinida se desejar adicionar o tipo de mistura <code>granite:AuthenticationRequirement</code> aos nós sem que eles sejam aplicados (por exemplo, em instâncias do autor). Se estiver ausente, o recurso será desativado. </td>
  </tr>
 </tbody>
</table>

## Configuração padrão desde AEM 6.3 {#default-configuration-since-aem}

Por padrão, novas instalações de AEM usarão as novas implementações tanto para as partes relacionadas à autorização quanto à autenticação do recurso CUG. A implementação antiga &quot;Suporte a CUG (Adobe Granite Closed User Group)&quot; foi substituída e, por padrão, será desativada em todas as instalações AEM. As novas implementações serão ativadas da seguinte maneira:

### Instâncias do autor {#author-instances}

| **&quot;Configuração Apache Jackrabbit Oak CUG&quot;** | **Explicação** |
|---|---|
| Caminhos suportados `/content` | O gerenciamento de controles de acesso para políticas CUG está habilitado. |
| FALSE Ativada para Avaliação de CUG | A avaliação de permissão está desativada. As políticas de CUG não têm efeito. |
| Classificação | 200 | Consulte a documentação do Oak. |

>[!NOTE]
>
>Nenhuma configuração para **Apache Jackrabbit Oak CUG Excluir Lista** e **Requisito de Autenticação Adobe Granite e Manipulador de Caminho de Login** está presente nas instâncias de criação padrão.

### Publicar instâncias {#publish-instances}

| **&quot;Configuração Apache Jackrabbit Oak CUG&quot;** | **Explicação** |
|---|---|
| Caminhos suportados `/content` | O gerenciamento de controles de acesso para políticas CUG está habilitado abaixo dos caminhos configurados. |
| Avaliação de CUG ativada TRUE | A avaliação de permissão está ativada abaixo dos caminhos configurados. As políticas de CUG entram em vigor em `Session.save()`. |
| Classificação | 200 | Consulte a documentação do Oak. |

| **&quot;Apache Jackrabbit Oak CUG Excluir Lista&quot;** | **Explicação** |
|---|---|
| Administradores de nomes principais | Exclui o principal administrador da avaliação CUG. |

| **&quot;Requisito de autenticação do Adobe Granite e manipulador de caminho de logon&quot;** | **Explicação** |
|---|---|
| Caminhos suportados `/content` | Os requisitos de autenticação definidos no repositório por meio do tipo de mistura `granite:AuthenticationRequired` entram em vigor abaixo de `/content` em `Session.save()`. O Sling Authenticator é atualizado. A adição do tipo de mistura fora dos caminhos suportados é ignorada. |

## Desabilitando o requisito de autorização e autenticação do CUG {#disabling-cug-authorization-and-authentication-requirement}

A nova implementação pode ser desabilitada no caso de uma determinada instalação não utilizar CUGs ou usar meios diferentes para autenticação e autorização.

### Desabilitar Autorização de CUG {#disable-cug-authorization}

Consulte a documentação [CUG pluggability](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obter detalhes sobre como remover o modelo de autorização CUG da configuração de autorização composta.

### Desative o requisito de autenticação {#disable-the-authentication-requirement}

Para desativar o suporte para o requisito de autenticação, conforme fornecido pelo módulo `granite.auth.authhandler`, basta remover a configuração associada ao **Requisito de Autenticação de Adobe Granite e Manipulador de Caminho de Login**.

>[!NOTE]
>
>Entretanto, observe que a remoção da configuração não cancelará o registro do tipo de mixina, que ainda era aplicável aos nós sem ter efeito.

## Interação com outros módulos {#interaction-with-other-modules}

### API do Apache Jackrabbit {#apache-jackrabbit-api}

Para alterar o novo tipo de política de controle de acesso usada pelo modelo de autorização CUG, a API definida pelo Apache Jackrabbit foi estendida. Desde a versão 2.11.0 do módulo `jackrabbit-api` define uma nova interface chamada `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, que se estende de `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

O mecanismo de importação do Apache Jackrabbit FileVault foi ajustado para lidar com políticas de controle de acesso do tipo `PrincipalSetPolicy`.

### Distribuição de conteúdo do Apache Sling {#apache-sling-content-distribution}

Consulte a seção acima [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault).

### Replicação de Adobe Granite {#adobe-granite-replication}

O módulo de replicação foi ligeiramente ajustado para poder replicar as políticas de CUG entre diferentes instâncias AEM:

* `DurboImportConfiguration.isImportAcl()` é interpretada literalmente e afetará somente as políticas de controle de acesso que implementam  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` respeitará somente esta configuração para ACLs verdadeiras
* Outras políticas, como instâncias `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` criadas pelo modelo de autorização CUG, sempre serão replicadas e a opção de configuração `DurboImportConfiguration.isImportAcl`() será ignorada.

Há uma limitação da replicação das políticas de CUG. Se uma determinada política CUG for removida sem remover o tipo de nó de mixagem correspondente `rep:CugMixin,`, a remoção não será refletida na replicação. Isso foi resolvido removendo sempre a combinação após a remoção da política. A limitação pode, no entanto, aparecer se o tipo de mistura for adicionado manualmente.

### Manipulador de Autenticação do Adobe Granite {#adobe-granite-authentication-handler}

O manipulador de autenticação **Adobe Granite HTTP Header Authentication Handler** fornecido com o pacote `com.adobe.granite.auth.authhandler` contém uma referência à interface `CugSupport` definida pelo mesmo módulo. É usado para calcular o &#39;realm&#39; em determinadas circunstâncias, voltando para o realm configurado com o manipulador.

Isso foi ajustado para tornar a referência a `CugSupport` opcional, a fim de garantir a compatibilidade retroativa máxima se uma determinada configuração decidir reativar a implementação obsoleta. As instalações que usam a implementação não serão mais extraídas do realm da implementação CUG, mas sempre exibirão o realm conforme definido com **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>Por padrão, o **Adobe Granite HTTP Header Authentication Handler** só está configurado no modo de execução de publicação com a opção &quot;Desativar página de logon&quot; ( `auth.http.nologin`) ativada.

### AEM LiveCopy {#aem-livecopy}

A configuração de CUGs em conjunto com o LiveCopy é representada no repositório pela adição de um nó extra e de uma propriedade extra, da seguinte forma:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ambos os elementos são criados em `cq:Page`. Com o design atual, o MSM trata somente dos nós e propriedades que estão sob o nó `cq:PageContent` (`jcr:content`).

Portanto, os grupos CUG não podem ser revertidos de um blueprint para um Live Copy. Planeje adequadamente isso ao configurar uma Live Copy.

## Alterações com a nova implementação do CUG {#changes-with-the-new-cug-implementation}

A presente seção tem por objetivo fornecer uma panorâmica das alterações introduzidas na característica CUG, bem como uma comparação entre a antiga e a nova implementação. Ele lista as alterações que afetam a forma como o suporte a CUG é configurado e descreve como e por quem os CUGs são gerenciados no conteúdo do repositório.

### Diferenças na configuração e configuração do CUG {#differences-in-cug-setup-and-configuration}

O componente OSGi obsoleto **Adobe Granite Closed User Group (CUG) Support** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) foi substituído por novos componentes para poder manipular separadamente as partes relacionadas à autorização e autenticação da antiga funcionalidade CUG.

## Diferenças no Gerenciamento de CUGs no Conteúdo do Repositório {#differences-in-managing-cugs-in-the-repository-content}

As seções a seguir descrevem as diferenças entre as novas implementações e as antigas, do ponto de vista da implementação e da segurança. Embora a nova implementação tenha como objetivo fornecer a mesma funcionalidade, há alterações sutis que são importantes ao usar o novo CUG.

### Diferenças No Que Respeita À Autorização {#differences-with-regards-to-authorization}

As principais diferenças do ponto de vista da autorização são resumidas na lista seguinte:

**Conteúdo de Controle de acesso dedicado para CUGs**

Na implementação antiga, o modelo de autorização padrão era usado para manipular as políticas de lista de controles de acesso na publicação, substituindo quaisquer ACEs existentes pela configuração exigida pelo CUG. Isto foi desencadeado pela escrita de propriedades regulares e residuais do JCR que foram interpretadas durante a publicação.

Com a nova implementação, a configuração do controle de acesso do modelo de autorização padrão não é afetada por nenhum CUG que esteja sendo criado, modificado ou removido. Em vez disso, um novo tipo de política chamado `PrincipalSetPolicy` é aplicado como conteúdo de controle de acesso adicional ao nó do público alvo. Essa política adicional será localizada como um filho do nó do público alvo e seria um irmão do nó de política padrão, se presente.

**Editar Políticas CUG No Gerenciamento De Controles de acesso**

Essa mudança das propriedades residuais do JCR para uma política de controles de acesso dedicada tem impacto na permissão necessária para criar ou modificar a parte de autorização do recurso CUG. Como isso é considerado uma modificação no conteúdo do controle de acesso, requer `jcr:readAccessControl` e `jcr:modifyAccessControl` privilégios para ser gravado no repositório. Portanto, somente os autores de conteúdo autorizados a modificar o conteúdo do controle de acesso de uma página podem configurar ou modificar esse conteúdo. Isso contrasta com a implementação antiga, na qual a capacidade de gravar propriedades JCR regulares era suficiente, resultando em um escalonamento de privilégio.

**Nó de público alvo Definido pela Política**

Espera-se que as políticas de CUG sejam criadas no nó JCR que define a subárvore a ser sujeita a acesso de leitura restrito. Essa provavelmente será uma página AEM caso o CUG afete a árvore inteira.

Observe que colocar a política CUG somente no nó jcr:content localizado abaixo de uma determinada página restringirá o acesso ao conteúdo s.str de uma determinada página, mas não entrará em vigor em quaisquer páginas semelhantes ou secundárias. Esse pode ser um caso de uso válido e é possível obtê-lo com um editor de repositório que permite aplicar conteúdo de conteúdo de acesso aprimorado. No entanto, contrasta a implementação anterior, onde colocar uma propriedade cq:cugEnabled no nó jcr:content foi mapeada internamente para o nó da página. Esse mapeamento não é mais executado.

**Avaliação de Permissão com Políticas de CUG**

Mudar do suporte antigo a CUG para um modelo de autorização adicional altera a forma como as permissões de leitura eficazes são avaliadas. Conforme descrito na [documentação do Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), um determinado principal permitido para visualização de `CUGcontent` só terá acesso de leitura se a avaliação de permissão de todos os modelos configurados no repositório Oak conceder acesso de leitura.

Em outras palavras, para a avaliação das permissões efetivas, as entradas `CUGPolicy` e do controle de acesso padrão serão consideradas e o acesso de leitura no conteúdo CUG só será concedido se for concedido por ambos os tipos de políticas. Em uma instalação padrão de publicação AEM onde o acesso de leitura à árvore completa `/content` é concedido para todos, o efeito das políticas CUG será o mesmo da implementação antiga.

**Avaliação sob demanda**

O modelo de autorização CUG permite ativar individualmente o gerenciamento de controles de acesso e a avaliação de permissões:

* O gerenciamento de controles de acesso será ativado se o módulo tiver um ou vários caminhos suportados nos quais os CUGs possam ser criados
* a avaliação de permissão só é ativada se a opção **Avaliação de CUG ativada** estiver marcada adicionalmente.

Na nova avaliação de configuração padrão AEM das políticas CUG, ela só é ativada com o modo de execução &quot;publicar&quot;. Consulte os detalhes da configuração padrão [desde AEM 6.3](#default-configuration-since-aem) para obter mais detalhes. Isso pode ser verificado comparando as políticas eficazes de um determinado caminho com as políticas armazenadas no conteúdo. As políticas eficazes só serão exibidas se a avaliação de permissão para CUGs estiver ativada.

Como explicado acima, as políticas de controle de acesso CUG agora são sempre armazenadas no conteúdo, mas a avaliação das permissões efetivas que resultam dessas políticas só será aplicada se **Avaliação CUG ativada** estiver ativada no console do sistema na configuração Apache Jackrabbit Oak **CUG.** Por padrão, ele é ativado somente com o modo de execução &quot;publicar&quot;.

### Diferenças em relação à autenticação {#differences-with-regards-to-authentication}

As diferenças em relação à autenticação são descritas abaixo.

#### Tipo de mistura dedicado para requisito de autenticação {#dedicated-mixin-type-for-authentication-requirement}

Na implementação anterior, os aspectos de autorização e autenticação de um CUG foram acionados por uma única propriedade JCR ( `cq:cugEnabled`). No que diz respeito à autenticação, isso resultou em uma lista atualizada dos requisitos de autenticação, conforme armazenados com a implementação do Autenticador Apache Sling. Com a nova implementação, o mesmo resultado é obtido marcando o nó do público alvo com um tipo de combinação dedicado ( `granite:AuthenticationRequired`).

#### Propriedade Para Excluir Caminho De Logon {#property-for-excluding-login-path}

O tipo de mixin define uma única propriedade opcional chamada `granite:loginPath`, que corresponde basicamente à propriedade `cq:cugLoginPage`. Em contraste com a implementação anterior, a propriedade de caminho de logon só será respeitada se o tipo de nó declarativo for a combinação mencionada. A adição de uma propriedade com esse nome sem definir o tipo de mixin não terá efeito e nem um novo requisito nem uma exclusão para o caminho de login serão reportados ao autenticador.

#### Privilégio para o requisito de autenticação {#privilege-for-authentication-requirement}

A adição ou remoção de um tipo de combinação requer `jcr:nodeTypeManagement` a concessão do privilégio. Na implementação anterior, o privilégio `jcr:modifyProperties` é usado para editar a propriedade residual.

No que diz respeito a `granite:loginPath`, o mesmo privilégio é necessário para adicionar, modificar ou remover a propriedade.

#### Nó de público alvo definido pelo Tipo de combinação {#target-node-defined-by-mixin-type}

Espera-se que os requisitos de autenticação sejam criados no nó JCR que define a subárvore a ser sujeita ao logon forçado. É provável que seja uma Página AEM caso o CUG afete a árvore inteira e a interface do usuário para a nova implementação, consequentemente, adicionará o tipo de combinação de requisito de autenticação no nó da página.

Colocar a política CUG somente no nó jcr:content localizado abaixo de uma determinada página restringirá o acesso ao conteúdo, mas não afetará o nó da página nem as páginas secundárias.

Esse pode ser um cenário válido e é possível com um editor de repositório que permite colocar o mixin em qualquer nó. No entanto, o comportamento contrasta com a implementação anterior, onde colocar uma propriedade cq:cugEnabled ou cq:cugLoginPage no nó jcr:content foi remapeada internamente no nó da página. Esse mapeamento não é mais executado.

#### Caminhos suportados configurados {#configured-supported-paths}

O tipo de combinação `granite:AuthenticationRequired` e a propriedade granite:loginPath só serão respeitados dentro do escopo definido pelo conjunto de **Caminhos Suportados** opções de configuração presentes com o **Requisito de Autenticação de Adobe Granite e Manipulador de Caminho de Logon**. Se nenhum caminho for especificado, o recurso de requisito de autenticação será desabilitado completamente. Nesse caso, o tipo de combinação e a propriedade não têm efeito ao serem adicionados ou definidos para um determinado nó JCR.

### Mapeamento de conteúdo JCR, serviços e configurações OSGi {#mapping-of-jcr-content-osgi-services-and-configurations}

O documento abaixo fornece um mapeamento abrangente dos serviços OSGi, configurações e conteúdo do repositório entre a implementação antiga e a nova.

Mapeamento CUG desde AEM 6.3

[Obter arquivo](assets/cug-mapping.pdf)

## Atualizar CUG {#upgrade-cug}

### Instalações existentes usando o CUG obsoleto {#existing-installations-using-the-deprecated-cug}

A antiga implementação de suporte do CUG foi descontinuada e será removida para versões futuras. É recomendável passar para as novas implementações ao atualizar de versões anteriores à AEM 6.3.

Para instalação AEM atualizada, é importante garantir que somente uma implementação CUG esteja ativada. A combinação do suporte novo e antigo e obsoleto ao CUG não é testada e provavelmente causa um comportamento indesejado:

* colisões no Autenticador Sling no que diz respeito aos requisitos de autenticação
* negado o acesso de leitura quando a configuração de ACL associada ao CUG antigo entra em conflito com uma nova política de CUG.

### Migração de Conteúdo de CUG Existente {#migrating-existing-cug-content}

O Adobe fornece uma ferramenta para migrar para a nova implementação do CUG. Para usá-lo, execute as seguintes etapas:

1. Vá para `https://<serveraddress>:<serverport>/system/console/cug-migration` para acessar a ferramenta.
1. Digite o caminho raiz para o qual deseja verificar os CUGs e pressione o botão **Executar execução a seco**. Isso verificará os CUGs elegíveis para conversão no local selecionado.
1. Depois de revisar os resultados, pressione o botão **Executar migração** para migrar para a nova implementação.

>[!NOTE]
>
>Se você encontrar problemas, será possível configurar um registrador específico no nível **DEBUG** em `com.day.cq.auth.impl.cug` para obter a saída da ferramenta de migração. Consulte [Registro](/help/sites-deploying/configure-logging.md) para obter mais informações sobre como fazer isso.

