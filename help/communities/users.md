---
title: Gerenciar usuários e grupos de usuários
seo-title: Managing Users and User Groups
description: Os usuários do AEM Communities podem se registrar e editar seus perfis
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# Gerenciar usuários e grupos de usuários {#managing-users-and-user-groups}

## Visão geral {#overview}

No AEM Communities, no ambiente de publicação, os usuários podem se registrar e editar seus perfis. Dadas as permissões apropriadas, elas também podem:

* Crie subcomunidades no site da comunidade (consulte [grupos da comunidade](creating-groups.md)).

* [Moderar](moderation.md) conteúdo gerado pelo usuário (UGC).

* Be [privilegiado](#privileged-members-group) para criar entradas para blogs, calendários, QnA e fóruns.

Os usuários registrados no ambiente de publicação são geralmente chamados de *membros da comunidade (membros)* para diferenciá-los de *usuários* no ambiente de criação.

As permissões são concedidas atribuindo membros a um dos [grupos de membros (usuário)](#publish-group-roles) criado dinamicamente quando o site da comunidade é [criado](sites-console.md) ou [modificados](sites-console.md#modifying-site-properties) do ambiente do autor. Ao trabalhar a partir do ambiente de criação, os membros ficam visíveis no ambiente de publicação por meio do [serviço de túnel](#tunnel-service).

Por design, os membros e grupos de membros criados no ambiente de publicação não devem aparecer no ambiente do autor. Usuários e grupos de usuários criados no ambiente de criação têm o objetivo de permanecer no ambiente de criação.

Quando os usuários no autor e os membros no Publish vêm da mesma lista de usuários, como sincronizados do mesmo diretório LDAP, eles não são considerados o mesmo usuário com as mesmas permissões e associação de grupo nos ambientes do autor e de publicação. As funções dos membros e dos utilizadores devem ser estabelecidas separadamente em matéria de publicação e de autor, conforme adequado.

Para um [publicar farm](topologies.md)O , o registro e as modificações feitas em uma instância de publicação precisam ser sincronizados com outras instâncias de publicação para que elas tenham acesso aos mesmos dados do usuário. Para obter detalhes, consulte [Sincronização de usuários](sync.md), que inclui uma seção que descreve [O que acontece quando...](sync.md#what-happens-when).

### Limites de contribuição {#contribution-limits}

Para proteger contra spam, é possível limitar a frequência de publicação de conteúdo dos membros. Além disso, é possível limitar automaticamente as contribuições dos novos membros registrados.

Para obter detalhes, consulte [Limites de contribuição dos membros](limits.md).

### Grupos de usuários criados dinamicamente {#dynamically-created-user-groups}

Quando um novo site da comunidade é criado, novos grupos de usuários são criados dinamicamente com ids exclusivas (uid) e permissões apropriadas para várias funções administrativas necessárias para gerenciar o site da comunidade no ambiente de criação (consulte [Funções do Grupo de Autores](#author-group-roles)) ou o ambiente de publicação (consulte [Publicar funções de grupo](#publish-group-roles)).

Os nomes dos grupos são gerados a partir do nome dado ao site durante [criação de site da comunidade](sites-console.md#step13asitetemplate). As ids exclusivas evitam nomear conflitos para sites de comunidade e grupos de comunidade com nomes semelhantes no mesmo servidor.

Por exemplo, se o nome do site fosse &quot;*engajamento*&quot; para um site intitulado &quot;We.Retail Engage&quot;, um dos grupos de usuários criados seria:

* Comunidade *Mobilizar* Membros

## Ambiente de criação {#author-environment}

### Serviço de túnel {#tunnel-service}

Ao usar o ambiente de criação para [criar sites](sites-console.md), [modificar propriedades do site](sites-console.md#modifying-site-properties) e [gerenciar membros da comunidade e grupos de membros](members.md), é necessário acessar usuários e grupos de usuários registrados no ambiente de publicação.

O serviço de túnel fornece esse acesso usando o agente de replicação do autor.

* Para obter detalhes, consulte [instruções de configuração](deploy-communities.md#tunnel-service-on-author) na página de implantação.

O [Consoles Membros e grupos do Communities](members.md) são para o único objetivo de gerenciar usuários (membros) e grupos de usuários (grupos de membros) registrados somente no ambiente de publicação.

Para gerenciar usuários e grupos de usuários registrados no ambiente de criação, use o [Console de segurança](../../help/sites-administering/security.md)

### Funções do Grupo de Autores {#author-group-roles}

| Se Membro do Grupo... | Função principal |
|---|---|
| administradores | O grupo de administradores consiste em administradores de sistema que têm todas as capacidades de um Administrador da Comunidade, bem como a capacidade de gerenciar o grupo Administradores da Comunidade. |
| Administradores da comunidade | O grupo Administradores da comunidade torna-se automaticamente membro de todos os sites da comunidade e de quaisquer grupos da comunidade criados no site. Um membro inicial do grupo Administradores da Comunidade é o grupo de administradores. No ambiente de criação, os administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem banir membros da comunidade) e moderar conteúdo. |
| Comunidade &lt;*nome do site*> Sitecontentmanager | O Gerente de conteúdo do site da comunidade pode executar a criação tradicional de AEM, a criação de conteúdo e a modificação de páginas para um site da comunidade. |
| Nenhum | Um visitante anônimo do site pode não acessar o ambiente do autor. |

### Administradores do sistema {#system-administrators}

Os membros do grupo de administradores são administradores de sistema que podem executar a configuração inicial de uma instalação AEM para os ambientes de autor e publicação.

Para fins de demonstração e desenvolvimento, o grupo de administradores tem um membro cujo usuário é *administrador* e a senha é *administrador*.

Para ambientes de produção, o grupo de administradores padrão deve ser modificado.

Certifique-se de seguir a [Lista de verificação de segurança](../../help/sites-administering/security-checklist.md).

## Ambiente de publicação {#publish-environment}

### Tornar-se membro {#becoming-a-member}

No ambiente de publicação, dependendo do [configurações](sites-console.md#user-management) do site da comunidade, um visitante do site pode se tornar membro da comunidade:

* Quando o site da comunidade é privado (fechado):
   * Por convite
   * Por ações de um administrador

* Quando o site da comunidade for público (aberto):
   * Por autoregistro
   * Por logon social com a Facebook e a Twitter

>[!NOTE]
>
>Se um visitante do site se registrar como membro de um site aberto da comunidade, ele se tornará automaticamente membro de outros sites abertos da comunidade no mesmo ambiente de publicação.

### Publicar funções de grupo {#publish-group-roles}

| Se Membro do Grupo... | Função principal |
|---|---|
| Comunidade &lt;*nome do site*> Membros | Um membro do site da comunidade é um usuário registrado. Eles podem fazer logon, modificar o perfil, ingressar em um grupo aberto da comunidade, publicar conteúdo na comunidade, enviar mensagens para outros membros e seguir as atividades do site. |
| Comunidade &lt;*nome do site*> Moderadores | Um moderador de site da comunidade é um membro da comunidade confiável que pode moderar o UGC em massa, usando o console de moderação ou no contexto, na página em que o conteúdo é publicado. |
| Comunidade &lt;*nome do site*> &lt;*nome do grupo*> Membros | Um membro do grupo da comunidade é um membro da comunidade que ingressou em um grupo aberto da comunidade ou foi convidado para um grupo fechado da comunidade. Eles têm as habilidades de um membro para esse grupo da comunidade dentro do site. |
| Comunidade &lt;*nome do site*> Groupadministrators | Um administrador de grupo de sites da comunidade é um membro confiável da comunidade que está atribuído para criar e gerenciar subcomunidades (grupos) em um site da comunidade. Inclui a capacidade de fornecer moderação no contexto. |
| *Grupo de Segurança de Membros Privados* | Um grupo de usuários criado e mantido manualmente para restringir a criação de conteúdo. Consulte [Grupo de Membros Privados](#privileged-members-group). |
| Nenhum | Um visitante anônimo do site, que descobre o site, pode visualizar e pesquisar sites da comunidade que permitem acesso anônimo. Para participar e publicar conteúdo, o usuário deve se registrar automaticamente (se permitido) e se tornar um membro da comunidade. |

### Atribuindo Membros para Publicar Funções de Grupo {#assigning-members-to-publish-group-roles}

When [criar um site da comunidade](sites-console.md) no ambiente de criação, ou quando [modificar propriedades do site,](sites-console.md#modifying-site-properties) os membros podem receber várias funções executadas no ambiente de publicação, como moderadores, administradores de grupo, contatos de recursos ou membros privilegiados.

[Ativação do serviço de túnel](sync.md#accessingpublishusersfromauthor) resulta em opções de atribuição serem apresentadas de membros em publicação, em vez de usuários em autor.

Os membros selecionados serão automaticamente atribuídos ao [grupo adequado](#publish-group-roles) e suas associações serão incluídas quando o site da comunidade for (re)publicado.

### Grupo de membros privilegiados {#privileged-members-group}

A finalidade de um grupo de segurança de membros privilegiados é restringir a criação de conteúdo para determinadas funções da comunidade a um subconjunto privilegiado de membros de um site da comunidade.

O grupo de membros privilegiados é um grupo de membros criado e gerenciado usando o [Console de grupos de comunidades](members.md).

Depois que um grupo de membros privilegiados é criado, e com o [serviço de túnel habilitado](sync.md#accessingpublishusersfromauthor), a estrutura de um site da comunidade existente pode ser [modificados](sites-console.md#modify-structure) para editar a configuração de suas funções de comunidade como &quot;Permitir membros privilegiados&quot; e adicionar o grupo criado.

As funções da comunidade que permitem especificar um ou mais grupos de membros privilegiados são:

* [Função do blog](functions.md#blog-function) - Para restringir a criação de novos artigos.
* [Função de calendário](functions.md#calendar-function) - Para restringir a criação de novos eventos.
* [Função do fórum](functions.md#forum-function) - Para restringir a criação de novos tópicos.
* [Função QnA](functions.md#qna-function) - Para restringir a criação de novas perguntas.

Quando uma função da comunidade não é protegida (nenhum grupo de membros privilegiados é atribuído), todos os membros do site da comunidade podem criar conteúdo de recurso (artigos, eventos, tópicos, perguntas).

>[!NOTE]
>
>Adicionar um usuário a um grupo de membros privilegiados de um site da comunidade somente lhes concederá privilégios de criação se também forem membros desse mesmo site da comunidade.

## Criação de membros da comunidade {#creating-community-members}

### Local do Repositório {#repository-location}

Para que determinados recursos funcionem corretamente, é necessário criar usuários e grupos de usuários com os privilégios apropriados.

Quando os membros são criados em `/home/users/community`, elas herdam as ACLs adequadas que dão privilégios de leitura aos perfis dos membros.

Da mesma forma, grupos de usuários personalizados da comunidade (como grupos de membros privilegiados) devem ser criados em `/home/groups/community`.

Usar o [Consoles Membros e grupos do Communities](members.md) criará usuários e grupos nesses caminhos.

Para especificar um caminho personalizado, é necessário usar a interface de usuário de segurança clássica, que pode ser acessada em [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Para conceder privilégios de leitura para caminhos de membro personalizados, em todas as instâncias de publicação defina ACLs semelhantes a `/home/users/community`:

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

Para conceder os privilégios adequados para caminhos de grupos de membros personalizados, como /home/groups/mycompany, em todas as instâncias de publicação defina ACLs semelhantes a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consoles {#consoles}

Há quatro consoles separados disponíveis apenas no ambiente do autor:

| console | Ferramentas, Segurança, Usuários | Ferramentas, segurança, grupos | Comunidades, Membros | Comunidades, Grupos |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gerenciadores | usuários no autor | grupos de usuários no autor | membros ao publicar | grupos de membros ao publicar |
| exige | permissão de administrador | permissão de administrador | permissão de administrador, serviço de túnel, sincronização de usuário para o farm de publicação | permissão de administrador, serviço de túnel, sincronização de usuário para o farm de publicação |

### Função de administradores da comunidade {#community-administrators-role}

Conforme declarado na [Funções do Grupo de Autores](#author-group-roles) no gráfico, os membros do grupo Administradores da Comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem banir membros da comunidade) e moderar conteúdo.

Siga as mesmas etapas que criar e atribuir um usuário à função de gerenciador de ativação, mas adicione c `ommunity-administrators` na guia Grupos do usuário.

### Integração LDAP {#ldap-integration}

AEM suporta o uso do LDAP para autenticação de usuários, bem como a criação de contas de usuários. Isso é detalhado em [Configuração do LDAP com AEM 6](../../help/sites-administering/ldap-config.md).

A seguir estão alguns detalhes de configuração específicos para membros da comunidade e grupos de membros.

1. Configure o LDAP para cada instância de publicação de AEM.
2. [O provedor de identidade LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Sem instruções especiais

3. [O Manipulador de Sincronização](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Defina as seguintes propriedades:

      * **[!UICONTROL Associação automática de usuário]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefixo do caminho do usuário]**: `/community`
      * **[!UICONTROL Prefixo do caminho do grupo]**: `/community`

4. [O módulo de logon externo](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * sem instruções especiais

Isso faz com que os usuários sejam automaticamente atribuídos ao grupo de membros do site da comunidade e ao local do repositório que está sendo `/home/users/community` e `/home/groups/community`, para que herdem as permissões apropriadas para ver o perfil do outro.

* O `User auto membership` deve ser o valor `rep:authorizableId` propriedade, não a `givenName` (nome de exibição) do perfil.

## Sincronizar usuários entre instâncias AEM {#synchronizing-users-among-aem-instances}

Ao usar um [publicar farm](topologies.md), certifique-se de que os usuários tenham o mesmo caminho em cada instância de publicação importando os usuários primeiro para uma instância e [habilitando a sincronização de usuários](sync.md) para o Sling distribuir os usuários para as outras instâncias de publicação.

Ao importar grupos de usuários, para garantir que os grupos de usuários tenham o mesmo caminho em cada instância de publicação, importe para uma instância e [criar um pacote](../../help/sites-administering/package-manager.md#creating-a-new-package) para exportar e instalar esse pacote em todas as outras instâncias de publicação.

Embora a sincronização de grupos de usuários por meio da sincronização de usuários seja incluída em uma versão futura, atualmente, somente a variável *associação* de um grupo de usuários será sincronizado quando a sincronização do usuário for executada.

## Sobre grupos da comunidade {#about-community-groups}

Ao discutir grupos, há dois tópicos distintos:

* **[Grupos da comunidade](overview.md#communitygroups)**

   Grupos da comunidade são subcomunidades que podem ser criadas no ambiente de publicação de um site da comunidade que suporta a criação de grupos da comunidade. A criação de um grupo da comunidade resulta em mais páginas adicionadas ao site e são gerenciadas de maneira semelhante ao site da comunidade principal. Para obter mais informações, visite [Fundamentos do grupo comunitário](essentials-groups.md) para desenvolvedores e [Grupo da comunidade](creating-groups.md) para autores.

* **[Grupos de membros](../../help/sites-administering/security.md)**

   Grupos de membros são os grupos aos quais os membros podem pertencer e são gerenciados por meio do console Grupos . Grande parte da discussão desta página foi dedicada aos grupos de membros. Os grupos de membros criados automaticamente para um site da comunidade, que recebem o prefixo *`Community`*, pode ser designado como um grupo comunitário, pelo que o contexto do debate deve ser considerado.
