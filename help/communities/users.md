---
title: Gerenciar usuários e grupos de usuários
description: Os usuários do AEM Communities podem se registrar e editar seus perfis
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Gerenciar usuários e grupos de usuários {#managing-users-and-user-groups}

## Visão geral {#overview}

No AEM Communities, no ambiente de publicação, os usuários podem se registrar e editar seus perfis. Dadas as permissões apropriadas, eles também podem:

* Crie subcomunidades no site da comunidade (consulte [grupos da comunidade](creating-groups.md)).

* [Moderar](moderation.md) conteúdo gerado pelo usuário (UGC).

* Tenha [privilégios](#privileged-members-group) para criar entradas para blogs, calendários, QnA e fóruns.

Os usuários registrados no ambiente de publicação geralmente são chamados de *membros da comunidade (membros)* para diferenciá-los de *usuários* no ambiente de criação.

As permissões são concedidas pela atribuição de membros a um dos [grupos de membros (usuários)](#publish-group-roles) criados dinamicamente quando o site da comunidade é [criado](sites-console.md) ou [modificado](sites-console.md#modifying-site-properties) do ambiente de criação. Ao trabalhar no ambiente de criação, os membros ficam visíveis no ambiente de publicação por meio do [serviço de túnel](#tunnel-service).

Por design, os membros e grupos de membros criados no ambiente de publicação não devem aparecer no ambiente de autor. Os usuários e grupos de usuários criados no ambiente de criação também devem permanecer no ambiente de criação.

Quando os usuários no autor e os membros na publicação vêm da mesma lista de usuários, como os sincronizados do mesmo diretório LDAP, eles não são considerados o mesmo usuário com as mesmas permissões e associação de grupo nos ambientes do autor e de publicação. As funções dos membros e usuários devem ser estabelecidas separadamente em publicação e criação, conforme apropriado.

Para um [farm de publicação](topologies.md), o registro e as modificações feitas em uma instância de publicação precisam ser sincronizados com outras instâncias de publicação para que elas tenham acesso aos mesmos dados do usuário. Para obter detalhes, consulte [Sincronização de Usuário](sync.md), que inclui uma seção descrevendo [O que Acontece Quando...](sync.md#what-happens-when).

### Limites de contribuição {#contribution-limits}

Para proteção contra spam, é possível limitar a frequência de publicação de conteúdo por parte dos membros. Além disso, é possível limitar automaticamente as contribuições dos membros recém-registrados.

Para obter detalhes, consulte [Limites de contribuição de membros](limits.md).

### Grupos de usuários criados dinamicamente {#dynamically-created-user-groups}

Quando um novo site da comunidade é criado, novos grupos de usuários são criados dinamicamente com ids exclusivas (uid) e permissões apropriadas para várias funções administrativas necessárias para gerenciar o site da comunidade no ambiente de criação (consulte [Funções de grupo de autores](#author-group-roles)) ou no ambiente de publicação (consulte [Funções de grupo do Publish](#publish-group-roles)).

Os nomes dos grupos são gerados a partir do nome dado ao site durante a [criação do site da comunidade](sites-console.md#step13asitetemplate). As IDs exclusivas evitam conflitos de nomes para sites de comunidades com nomes semelhantes e grupos de comunidades no mesmo servidor.

Por exemplo, se o nome do site fosse &quot;*engage*&quot; para um site intitulado &quot; Engage&quot;, um dos grupos de usuários criados seria:

* Membros da Comunidade *Envolver*

## Ambiente de criação {#author-environment}

### Serviço de túnel {#tunnel-service}

Ao usar o ambiente de criação para [criar sites](sites-console.md), [modificar propriedades do site](sites-console.md#modifying-site-properties) e [gerenciar membros da comunidade e grupos de membros](members.md), é necessário acessar usuários e grupos de usuários registrados no ambiente de publicação.

O serviço de túnel fornece esse acesso usando o agente de replicação no autor.

* Para obter detalhes, consulte [instruções de configuração](deploy-communities.md#tunnel-service-on-author) na página de implantação.

Os [consoles Membros e grupos de comunidades](members.md) são somente para fins de gerenciamento de usuários (membros) e grupos de usuários (grupos de membros) registrados apenas no ambiente de publicação.

Para gerenciar usuários e grupos de usuários registrados no ambiente de criação, use o [Console de segurança](../../help/sites-administering/security.md)

### Funções dos grupos de autores {#author-group-roles}

| Se Membro do Grupo... | Função Primária |
|---|---|
| administradores | O grupo de administradores consiste em administradores do sistema que têm todas as habilidades de um Administrador da comunidade e a capacidade de gerenciar o grupo de Administradores da comunidade. |
| Administradores da comunidade | O grupo Administradores da comunidade se torna automaticamente membro de todos os sites da comunidade e de quaisquer grupos criados no site. Um membro inicial do grupo Administradores da comunidade é o grupo de administradores. No ambiente de criação, os administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo. |
| Comunidade &lt;*nome do site*> Sitecontentmanager | O Gerenciador de conteúdo do site da comunidade é capaz de criar páginas de AEM tradicionais, criar conteúdo e modificar páginas para um site da comunidade. |
| Nenhum | Um visitante anônimo do site pode não acessar o ambiente do autor. |

### Administradores do sistema {#system-administrators}

Os membros do grupo de administradores são administradores do sistema que podem executar a configuração inicial de uma instalação do AEM para os ambientes do autor e de publicação.

Para fins de demonstração e desenvolvimento, o grupo de administradores tem um membro cuja ID de usuário é *admin* e a senha é *admin*.

Para ambientes de produção, o grupo de administradores padrão deve ser modificado.

Certifique-se de seguir a [Lista de Verificação de Segurança](../../help/sites-administering/security-checklist.md).

## Ambiente de publicação {#publish-environment}

### Tornar-se um membro {#becoming-a-member}

No ambiente de publicação, dependendo das [configurações](sites-console.md#user-management) do site da comunidade, um visitante do site pode se tornar um membro da comunidade:

* Quando o site da comunidade é privado (fechado):
   * Por convite
   * Por ações de um administrador

* Quando o site da comunidade for público (aberto):
   * Por autorregistro
   * Ao fazer logon em redes sociais com o Facebook e o Twitter

>[!NOTE]
>
>Se um visitante do site se registrar como membro de um site de comunidade aberto, ele se tornará automaticamente membro de outros sites de comunidade abertos no mesmo ambiente de publicação.

### Funções de grupo do Publish {#publish-group-roles}

| Se Membro do Grupo... | Função Primária |
|---|---|
| Membros da comunidade &lt;*nome do site*> | Um membro do site da comunidade é um usuário registrado. Eles podem fazer logon, modificar o perfil, participar de um grupo aberto da comunidade, publicar conteúdo na comunidade, enviar mensagens para outros membros e seguir as atividades do site. |
| Comunidade &lt;*nome do site*> Moderadores | Um moderador de site da comunidade é um membro confiável da comunidade que pode moderar o UGC em massa, usando o console de moderação ou em contexto, na página em que o conteúdo é publicado. |
| Comunidade &lt;*nome do site*> &lt;*nome do grupo*> Membros | Um membro de um grupo da comunidade é um membro da comunidade que entrou em um grupo aberto da comunidade ou foi convidado para um grupo fechado da comunidade. Eles têm as habilidades de um membro para aquele grupo comunitário dentro do site. |
| Comunidade &lt;*nome do site*> Administradores de grupo | Um administrador de grupo do site da comunidade é um membro confiável da comunidade atribuído para criar e gerenciar subcomunidades (grupos) em um site da comunidade. Está incluída a capacidade de fornecer moderação no contexto. |
| *Grupo de Segurança de Membros Privilegiados* | Um grupo de usuários criado e mantido manualmente com o objetivo de restringir a criação de conteúdo. Consulte [Grupo de membros privilegiados](#privileged-members-group). |
| Nenhum | Um visitante anônimo do site, que descobre o site, pode visualizar e pesquisar sites da comunidade que permitem acesso anônimo. Para participar e publicar conteúdo, o usuário deve se registrar (se permitido) e se tornar membro da comunidade. |

### Atribuindo Membros a Funções de Grupos Publish {#assigning-members-to-publish-group-roles}

Ao [criar um site da comunidade](sites-console.md) no ambiente de criação ou ao [modificar propriedades do site,](sites-console.md#modifying-site-properties) os membros poderão receber várias funções executadas no ambiente de publicação, como moderadores, administradores de grupos, contatos de recursos ou membros privilegiados.

[Habilitar o serviço de túnel](sync.md#accessingpublishusersfromauthor) resulta em escolhas de atribuição apresentadas de membros na publicação em vez de usuários na criação.

Os membros selecionados serão atribuídos automaticamente ao [grupo apropriado](#publish-group-roles) e suas associações serão incluídas quando o site da comunidade for (re)publicado.

### Grupo de membros privilegiados {#privileged-members-group}

A finalidade de um grupo de segurança de membros privilegiados é restringir a criação de conteúdo para determinadas funções da comunidade a um subconjunto privilegiado de membros de um site da comunidade.

O grupo de membros privilegiados é um grupo de membros criado e gerenciado pelo [console Grupos de Comunidades](members.md).

Após a criação de um grupo de membros privilegiados, e com o [serviço de túnel ativado](sync.md#accessingpublishusersfromauthor), a estrutura de um site de comunidade existente pode ser [modificada](sites-console.md#modify-structure) para editar a configuração de suas funções de comunidade como &#39;Permitir membros privilegiados&#39; e adicionar o grupo criado.

As funções da comunidade que permitem a especificação de um ou mais grupos de membros privilegiados são:

* [Função de blog](functions.md#blog-function) - Para restringir a criação de novos artigos.
* [Função de calendário](functions.md#calendar-function) - Para restringir a criação de novos eventos.
* [Função do fórum](functions.md#forum-function) - Para restringir a criação de novos tópicos.
* [Função QnA](functions.md#qna-function) - Para restringir a criação de novas perguntas.

Quando uma função da comunidade não for protegida (nenhum grupo de membros privilegiados foi atribuído), todos os membros do site da comunidade poderão criar conteúdo de recursos (artigos, eventos, tópicos, perguntas).

>[!NOTE]
>
>Adicionar um usuário a um grupo de membros privilegiados para um site da comunidade só concederá privilégios se ele também for membro desse mesmo site da comunidade.

## Criação de membros da comunidade {#creating-community-members}

### Local do repositório {#repository-location}

Para que certos recursos funcionem corretamente, é necessário criar usuários e grupos de usuários com os privilégios apropriados.

Quando os membros são criados em `/home/users/community`, eles herdam as ACLs apropriadas que dão privilégios de leitura aos perfis dos membros.

Da mesma forma, os grupos personalizados de usuários da comunidade (como grupos de membros privilegiados) devem ser criados em `/home/groups/community`.

O uso dos [consoles Membros e grupos das comunidades](members.md) criará usuários e grupos nesses caminhos.

Para especificar um caminho personalizado, é necessário usar a interface de segurança clássica, acessível em [https://&lt;servidor>:&lt;porta>/useradmin](http://localhost:4503/useradmin).

Para conceder privilégios de leitura para caminhos de membros personalizados, em todas as instâncias de publicação, defina ACLs semelhantes a `/home/users/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

Para conceder os privilégios adequados para caminhos de grupos de membros personalizados, como /home/groups/mycompany, em todas as instâncias de publicação, defina ACLs semelhantes a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consoles {#consoles}

Há quatro consoles separados disponíveis somente no ambiente de criação:

| console | Ferramentas, Segurança, Usuários | Ferramentas, Segurança, Grupos | Comunidades, Membros | Comunidades, Grupos |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gerencia | usuários no autor | grupos de usuários no autor | membros na publicação | grupos de membros na publicação |
| exige | permissão de administrador | permissão de administrador | permissão de administrador, serviço de túnel, sincronização de usuário para farm de publicação | permissão de administrador, serviço de túnel, sincronização de usuário para farm de publicação |

### Função dos administradores da comunidade {#community-administrators-role}

Conforme declarado no gráfico [Funções do grupo de autores](#author-group-roles), os membros do grupo Administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo.

Siga as mesmas etapas que criar e atribuir um usuário à função de gerente de ativação, mas adicione o grupo c `ommunity-administrators` na guia Grupos do usuário.

### Integração de LDAP {#ldap-integration}

O AEM suporta o uso do LDAP para autenticação de usuários e criação de contas de usuário. Isto está detalhado em [Configurando o LDAP com AEM 6](../../help/sites-administering/ldap-config.md).

A seguir estão alguns detalhes de configuração específicos para membros da comunidade e grupos de membros.

1. Configure o LDAP para cada instância de publicação do AEM.
2. [O Provedor de Identidade LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Sem instruções especiais

3. [O Manipulador de sincronização](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Defina as seguintes propriedades:

      * **[!UICONTROL Associação automática de usuário]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefixo de Caminho do Usuário]**: `/community`
      * **[!UICONTROL Prefixo do Caminho do Grupo]**: `/community`

4. [O módulo de login externo](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * nenhuma instrução especial

Isso faz com que os usuários sejam automaticamente atribuídos ao grupo de membros do site da comunidade e o local do repositório seja `/home/users/community` e `/home/groups/community`, para que eles herdem as permissões apropriadas para ver o perfil um do outro.

* O valor `User auto membership` deve ser a propriedade `rep:authorizableId`, não o `givenName` (nome de exibição) do perfil.

## Sincronização de usuários entre instâncias AEM {#synchronizing-users-among-aem-instances}

Ao usar um [farm de publicação](topologies.md), verifique se os usuários têm o mesmo caminho em cada instância de publicação importando os usuários primeiro para uma instância e [habilitando a sincronização de usuários](sync.md) com o Sling para distribuir os usuários para as outras instâncias de publicação.

Se estiver importando grupos de usuários, para garantir que eles tenham o mesmo caminho em cada instância de publicação, importe para uma instância e [crie um pacote](../../help/sites-administering/package-manager.md#creating-a-new-package) para exportação e instale-o em todas as outras instâncias de publicação.

Embora a sincronização de grupos de usuários por meio da sincronização de usuários seja incluída em uma versão futura, atualmente somente a *associação* de um grupo de usuários será sincronizada quando a sincronização de usuários for executada.

## Sobre grupos da comunidade {#about-community-groups}

Ao discutir grupos, há dois tópicos distintos:

* **[Grupos da comunidade](overview.md#communitygroups)**

  Grupos de comunidades são as subcomunidades que podem ser criadas no ambiente de publicação de um site de comunidades que ofereça suporte à criação de grupos de comunidades. A criação de um grupo da comunidade resulta na adição de mais páginas ao site e é gerenciada de uma maneira semelhante ao site da comunidade pai. Para obter mais informações, visite o [Community Group Essentials](essentials-groups.md) para desenvolvedores e o [Community Group](creating-groups.md) para autores.

* **[Grupos de membros](../../help/sites-administering/security.md)**

  Grupos de membros são os grupos aos quais os membros podem pertencer e são gerenciados por meio do console Grupos. A maior parte da discussão nesta página foi dedicada aos grupos de membros. Os grupos membros criados automaticamente para um site da comunidade, que têm o prefixo *`Community`*, podem ser chamados de grupos da comunidade. Portanto, o contexto da discussão deve ser considerado.
