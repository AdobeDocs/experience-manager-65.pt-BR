---
title: Gerenciamento de usuários e grupos de usuários
seo-title: Gerenciamento de usuários e grupos de usuários
description: Os usuários do AEM Communities podem se registrar e editar seus perfis
seo-description: Os usuários do AEM Communities podem se registrar e editar seus perfis
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: 2422ed41b18bc558f0cfc9e80f7eb6f4923aa07c

---


# Managing Users and User Groups {#managing-users-and-user-groups}

## Visão geral {#overview}

No AEM Communities, no ambiente de publicação, os usuários podem se registrar e editar seus perfis. Considerando as permissões apropriadas, eles também podem:

* Crie subcomunidades no site da comunidade (consulte grupos [da](creating-groups.md)comunidade).

* [Moderar](moderation.md) o conteúdo gerado pelo usuário (UGC).

* Esteja [ativando contatos de recursos](resources.md) .

* Tenha [o privilégio](#privileged-members-group) de criar entradas para blogs, calendários, QnA e fóruns.

Os usuários registrados no ambiente de publicação são geralmente chamados de membros da *comunidade (membros)* para diferenciá-los dos *usuários* no ambiente do autor.

As permissões são concedidas atribuindo membros a um dos grupos [de](#publish-group-roles) membros (usuário) criados dinamicamente quando o site da comunidade é [criado](sites-console.md) ou [modificado](sites-console.md#modifying-site-properties) a partir do ambiente do autor. Ao trabalhar a partir do ambiente do autor, os membros ficam visíveis a partir do ambiente de publicação por meio do serviço [de](#tunnel-service)túnel.

Por padrão, os membros e grupos de membros criados no ambiente de publicação não devem aparecer no ambiente do autor. Os usuários e grupos de usuários criados no ambiente do autor devem permanecer no ambiente do autor.

Quando os usuários do autor e os membros da publicação vêm da mesma lista de usuários, como sincronizados do mesmo diretório LDAP, eles não são considerados o mesmo usuário com as mesmas permissões e associação de grupo nos ambientes do autor e da publicação. As funções dos membros e dos utilizadores devem ser estabelecidas separadamente aquando da publicação e do autor, consoante o caso.

Para um farm [de](topologies.md)publicação, o registro e as modificações feitas em uma instância de publicação precisam ser sincronizados com outras instâncias de publicação para que elas tenham acesso aos mesmos dados do usuário. Para obter detalhes, consulte Sincronização [](sync.md)do usuário, que inclui uma seção que descreve [o que acontece quando...](sync.md#what-happens-when).

### Limites de contribuição {#contribution-limits}

Para proteger contra spam, é possível limitar a frequência de publicação de conteúdo dos membros. Além disso, é possível limitar automaticamente as contribuições dos novos membros registrados.

Para obter detalhes, consulte Limites [de contribuição dos](limits.md)membros.

### Grupos de usuários criados dinamicamente {#dynamically-created-user-groups}

Quando um novo site da comunidade é criado, novos grupos de usuários são criados dinamicamente com IDs exclusivas (uid) e permissões apropriadas para várias funções administrativas necessárias para gerenciar o site da comunidade no ambiente do autor (consulte Funções [do grupo do](#author-group-roles)autor) ou no ambiente de publicação (consulte [Publicar funções](#publish-group-roles)do grupo).

Os nomes dos grupos são gerados a partir do nome dado ao site durante a criação [do site da](sites-console.md#step13asitetemplate)comunidade. As IDs exclusivas evitam nomear conflitos para sites da comunidade com nomes semelhantes e grupos da comunidade no mesmo servidor.

Por exemplo, se o nome do site fosse &quot;*engajar*&quot; para um site chamado &quot;We.Retail Engage&quot;, então um dos grupos de usuários criados seria:

* Membros com *participação* na comunidade

## Ambiente de criação {#author-environment}

### Serviço de túnel {#tunnel-service}

Ao usar o ambiente do autor para [criar sites](sites-console.md), [modificar as propriedades](sites-console.md#modifying-site-properties) do site e [gerenciar membros da comunidade e grupos](members.md)de membros, é necessário acessar usuários e grupos de usuários registrados no ambiente de publicação.

O serviço de túnel fornece esse acesso usando o agente de replicação do autor.

* Para obter detalhes, consulte as instruções [de](deploy-communities.md#tunnel-service-on-author) configuração na página de implantação.

Os consoles Membros e Grupos [das Comunidades](members.md) têm como único objetivo gerenciar usuários (membros) e grupos de usuários (grupos de membros) registrados somente no ambiente de publicação.

Para gerenciar usuários e grupos de usuários registrados no ambiente do autor, use o console [Segurança](../../help/sites-administering/security.md)

### Funções do grupo de autores {#author-group-roles}

| Se Membro do Grupo... | Função principal |
|---|---|
| administradores | O grupo de administradores consiste em administradores de sistema que têm todos os recursos de um administrador da comunidade, bem como a capacidade de gerenciar o grupo de administradores da comunidade. |
| Administradores da comunidade | O grupo Administradores da comunidade se torna automaticamente membro de todos os sites da comunidade e de todos os grupos da comunidade criados no site. Um membro inicial do grupo Administradores da comunidade é o grupo de administradores. No ambiente do autor, os administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo. |
| Comunidade &lt;nome *do* site> Sitecontentmanager | O Community Site Content Manager pode executar a criação tradicional do AEM, a criação de conteúdo e a modificação de páginas para um site da comunidade. |
| Gerentes de habilitação da comunidade | O grupo Gerentes de ativação da comunidade consiste em usuários que estão disponíveis para atribuição para gerenciar um grupo de Gerentes de ativação do site da comunidade. |
| Community &lt;nome *do* site > SiteenableAdministradores | O grupo Gerentes de ativação do site da comunidade consiste em usuários que foram atribuídos para gerenciar os [recursos](resources.md)de ativação do site da comunidade. |
| Nenhum | Um visitante de site anônimo pode não acessar o ambiente do autor. |

### Administradores de sistema {#system-administrators}

Os membros do grupo de administradores são administradores de sistema que podem executar a configuração inicial de uma instalação do AEM para o autor e para os ambientes de publicação.

Para fins de demonstração e desenvolvimento, o grupo de administradores tem um membro cujo ID de usuário é *admin* e a senha é *admin*.

Para ambientes de produção, o grupo de administradores padrão deve ser modificado.

Siga a Lista de verificação de [segurança](../../help/sites-administering/security-checklist.md).

## Ambiente de publicação {#publish-environment}

### Tornando-se um membro {#becoming-a-member}

No ambiente publish, dependendo das [configurações](sites-console.md#user-management) do site da comunidade, um visitante do site pode se tornar um membro da comunidade:

* Quando o site da comunidade for privado (fechado):
   * Por convite
   * Por ações de um administrador

* Quando o site da comunidade for público (aberto):
   * Por autoinscrição
   * Por logon social com Facebook e Twitter

>[!NOTE]
>
>Se um visitante do site se registrar como membro de um site aberto da comunidade, ele automaticamente se tornará membro de outros sites abertos da comunidade no mesmo ambiente de publicação.


### Publicar funções de grupo {#publish-group-roles}

| Se Membro do Grupo... | Função principal |
|---|---|
| Membros da comunidade &lt;nome *do* site> | Um membro do site da comunidade é um usuário registrado. Eles podem fazer logon, modificar o perfil, ingressar em um grupo aberto da comunidade, publicar conteúdo na comunidade, enviar mensagens para outros membros e seguir as atividades do site. |
| Moderadores do &lt;nome *do* site> da comunidade | Um moderador de site da comunidade é um membro da comunidade confiável que pode moderar o UGC em massa, usando o console de moderação ou no contexto, na página em que o conteúdo é publicado. |
| Comunidade &lt;nome *do* site> &lt;nome *do* grupo> Membros | Um membro do grupo da comunidade é um membro da comunidade que ingressou em um grupo aberto da comunidade ou foi convidado para um grupo fechado da comunidade. Eles têm as habilidades de um membro para esse grupo da comunidade dentro do site. |
| Comunidade &lt;nome *do* site> Grupos de administradores | Um administrador de grupo de sites da comunidade é um membro da comunidade confiável que é atribuído para criar e gerenciar subcomunidades (grupos) em um site da comunidade. Inclui a capacidade de fornecer moderação no contexto. |
| *Grupo de Segurança de Membros Privilegiados* | Um grupo de usuários criado e mantido manualmente para restringir a criação de conteúdo. Consulte Grupo [de membros](#privileged-members-group)privilegiados. |
| Nenhum | Um visitante anônimo do site, que descobre o site, pode visualização e pesquisar sites da comunidade que permitem acesso anônimo. Para participar e publicar conteúdo, o usuário deve se registrar automaticamente (se permitido) e se tornar um membro da comunidade. |

### Atribuindo Membros para Publicar Funções de Grupo {#assigning-members-to-publish-group-roles}

Ao [criar um site](sites-console.md) da comunidade no ambiente do autor, ou ao [modificar as propriedades do site,](sites-console.md#modifying-site-properties) os membros podem receber várias funções executadas no ambiente de publicação, como moderadores, administradores de grupo, contatos de recursos ou membros privilegiados.

[Habilitar o serviço](sync.md#accessingpublishusersfromauthor) de túnel resulta em opções de atribuição apresentadas de membros ao publicar em vez de usuários ao criar.

Os membros selecionados serão automaticamente atribuídos ao grupo [](#publish-group-roles) apropriado e suas associações serão incluídas quando o site da comunidade for (re)publicado.

### Grupo de membros privilegiados {#privileged-members-group}

A finalidade de um grupo de segurança de membros privilegiados é restringir a criação de conteúdo para determinadas funções da comunidade a um subconjunto privilegiado de membros de um site da comunidade.

O grupo de membros privilegiados é um grupo de membros criado e gerenciado usando o console [Grupos de](members.md)comunidades.

Depois que um grupo de membros privilegiados é criado e com o serviço de [túnel ativado](sync.md#accessingpublishusersfromauthor), a estrutura de um site da comunidade existente pode ser [modificada](sites-console.md#modify-structure) para editar a configuração de suas funções de comunidade como &quot;Permitir membros privilegiados&quot; e adicionar o grupo criado.

As funções da comunidade que permitem especificar um ou mais grupos de membros privilegiados são:

* [Função](functions.md#blog-function) do blog - para restringir a criação de novos artigos.
* [Função](functions.md#calendar-function) de calendário - Para restringir a criação de novos eventos.
* [Função](functions.md#forum-function) do fórum - para restringir a criação de novos tópicos.
* [Função](functions.md#qna-function) QnA - para restringir a criação de novas perguntas.

Quando uma função da comunidade não está protegida (nenhum grupo de membros privilegiados atribuído), todos os membros do site da comunidade têm permissão para criar conteúdo de recursos (artigos, eventos, tópicos, perguntas).

>[!NOTE]
>
>Adicionar um usuário a um grupo de membros privilegiados para um site da comunidade só lhes concederá privilégios de criação se eles também forem membros desse mesmo site da comunidade.


## Criação de membros da comunidade {#creating-community-members}

### Local do repositório {#repository-location}

Para que determinados recursos funcionem corretamente, é necessário criar usuários e grupos de usuários com os privilégios apropriados.

Quando os membros são criados no, `/home/users/community`eles herdam as ACLs adequadas que concedem privilégios de leitura aos perfis dos membros.

Da mesma forma, grupos de usuários personalizados da comunidade (como grupos de membros privilegiados) devem ser criados em `/home/groups/community`.

O uso dos consoles [Membros e Grupos das](members.md) Comunidades criará usuários e grupos nesses caminhos.

Para especificar um caminho personalizado, é necessário usar a interface clássica de segurança, que pode ser acessada em [https://&lt;servidor>:&lt;porta>/useradmin](http://localhost:4503/useradmin).

Para conceder privilégios de leitura para caminhos de membros personalizados, em todas as instâncias de publicação defina ACLs semelhantes a `/home/users/community`:

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

Há quatro consoles separados disponíveis somente no ambiente do autor:

| console | Ferramentas, Segurança, Usuários | Ferramentas, Segurança, Grupos | Comunidades, membros | Comunidades, grupos |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gerencia | usuários no autor | grupos de usuários no autor | membros ao publicar | grupos de membros ao publicar |
| requirements | permissão de administrador | permissão de administrador | permissão de administrador, serviço de túnel, sincronização de usuário para o farm de publicação | permissão de administrador, serviço de túnel, sincronização de usuário para o farm de publicação |

### Função do gerente de habilitação da comunidade {#community-enablement-manager-role}

Normalmente, a capacidade de um visitante do site se registrar automaticamente não é permitida para uma comunidade [de](overview.md#enablement-community) ativação, pois há custos associados a cada membro. Os alunos e os recursos de habilitação são gerenciados por um usuário ao qual é atribuída a [função](#author-group-roles) de `enablement manager` durante a criação [do site no autor (adicionado como membro do grupo](sites-console.md#enablement) `Community <site-name> Siteenablementmanagers`). O também `enablement manager` é responsável por [atribuir recursos](resources.md) de aprendizado aos membros da comunidade no autor.

Somente os usuários que são membros do `Community Enablement Managers` grupo global podem ser selecionados como um `enablement manager` site da comunidade específica.

Para criar um usuário que possa receber a função de `Community Site Enablement Manager`, use o console de segurança da interface clássica para especificar o caminho:

Em uma instância do autor:

1. Conectado com privilégios de administrador, navegue até o console de segurança da interface clássica.

   Por exemplo, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. No menu Editar, selecione **[!UICONTROL Criar usuário]**.
3. Preencha a caixa de `Create User` diálogo.
   * O caminho deve ser `/home/users/community`.
4. Selecione **[!UICONTROL Criar]**.

   ![chlimage_1-130](assets/chlimage_1-130.png)

* No painel esquerdo, procure o usuário recém-criado e selecione para exibir no painel direito.

   ![chlimage_1-131](assets/chlimage_1-131.png)

No painel esquerdo:

1. Desmarque a caixa de pesquisa e selecione **[!UICONTROL Ocultar usuários]**.
2. Localize e arraste `community-enablementmanagers` para a guia **[!UICONTROL Grupos]** do novo usuário exibido no painel direito.

   ![chlimage_1-132](assets/chlimage_1-132.png)

### Função de administradores da comunidade {#community-administrators-role}

Conforme declarado no gráfico Funções [do Grupo de](#author-group-roles) Autores, os membros do grupo Administradores da Comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo.

Siga as mesmas etapas que criar e atribuir um usuário à função de gerenciador [de](#communitysiteenablementmanagerrole)ativação, mas adicione c `ommunity-administrators` grupo na guia Grupos do usuário.

### Integração LDAP {#ldap-integration}

O AEM oferece suporte ao uso do LDAP para autenticação de usuários e criação de contas de usuários. Isso é detalhado em [Configurar o LDAP com o AEM 6](../../help/sites-administering/ldap-config.md).

Veja a seguir alguns detalhes de configuração específicos para membros da comunidade e grupos de membros.

1. Configure o LDAP para cada instância de publicação do AEM.
2. [O provedor de identidade LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Nenhuma instrução especial

3. [O manipulador de sincronização](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Defina as seguintes propriedades:

      * **[!UICONTROL Associação]** automática do usuário: `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefixo]** do caminho do usuário: `/community`
      * **[!UICONTROL Prefixo]** do caminho do grupo: `/community`

4. [O módulo de logon externo](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * nenhuma instrução especial

Isso resulta na atribuição automática de usuários ao grupo de membros do site da comunidade e no local do repositório sendo `/home/users/community` e `/home/groups/community`, de modo que eles herdem as permissões apropriadas para ver o perfil de cada um.

* O `User auto membership` valor deve ser a `rep:authorizableId` propriedade, não o `givenName` (nome de exibição) do perfil.

## Sincronização de usuários entre instâncias do AEM {#synchronizing-users-among-aem-instances}

Ao usar um farm [de](topologies.md)publicação, certifique-se de que os usuários tenham o mesmo caminho em cada instância de publicação importando os usuários primeiro para uma instância e [permitindo a sincronização](sync.md) do usuário para Sling e distribuindo os usuários para as outras instâncias de publicação.

Se estiver importando grupos de usuários, para garantir que os grupos de usuários tenham o mesmo caminho em cada instância de publicação, importe para uma instância, [crie um pacote](../../help/sites-administering/package-manager.md#creating-a-new-package) para exportação e instale esse pacote em todas as outras instâncias de publicação.

Embora a sincronização de grupos de usuários por meio da sincronização de usuários seja incluída em uma versão futura, atualmente, somente a *associação* de um grupo de usuários será sincronizada quando a sincronização do usuário for executada.

## Sobre grupos da comunidade {#about-community-groups}

Ao discutir grupos, há dois tópicos distintos:

* **[Grupos da comunidade](overview.md#communitygroups)**

   Os grupos da comunidade são as subcomunidades que podem ser criadas no ambiente publish para um site da comunidade que suporta a criação de grupos da comunidade. A criação de um grupo da comunidade resulta em mais páginas adicionadas ao site e são gerenciadas de maneira semelhante ao site da comunidade pai. Para obter mais informações, visite [Community Group Essentials](essentials-groups.md) for Developers and [Community Group](creating-groups.md) for author.

* **[Grupos de membros](../../help/sites-administering/security.md)**

   Grupos de membros são os grupos aos quais os membros podem pertencer e são gerenciados pelo console Grupos. Grande parte da discussão desta página foi dedicada aos grupos de membros. Os grupos de membros criados automaticamente para um site da comunidade, que recebem o prefixo *`Community`*, podem ser chamados de grupos da comunidade, portanto, o contexto da discussão deve ser considerado.
