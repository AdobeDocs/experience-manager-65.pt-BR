---
title: Gerenciamento de identidade
seo-title: Gerenciamento de identidade
description: Saiba mais sobre o gerenciamento de identidade no AEM.
seo-description: Saiba mais sobre o gerenciamento de identidade no AEM.
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
translation-type: tm+mt
source-git-commit: a268b7046430cc17c8b59b9306cf3533d73bb4a2

---


# Gerenciamento de identidade{#identity-management}

Os visitantes individuais do seu site só podem ser identificados quando você fornece a capacidade de eles fazerem logon. Há várias razões pelas quais você pode desejar fornecer um recurso de logon:

* [AEM](/help/communities/overview.md)CommunitiesOs visitantes do site precisam fazer logon para publicar conteúdo na comunidade.
* [Grupos de usuários fechados](/help/sites-administering/cug.md)

   Talvez seja necessário limitar o acesso ao seu site (ou seções dele) a visitantes específicos.

* [Personalização](/help/sites-administering/personalization.md) Permite que os visitantes configurem certos aspectos de como acessam seu site.

A funcionalidade de logon (e logout) é fornecida por uma [conta com um **Perfil **](#profiles-and-user-accounts), que contém informações adicionais sobre o visitante registrado (usuário). Os processos reais de registro e autorização podem diferir:

* Autoinscrição no website

   Um Site [da](/help/communities/sites-console.md) comunidade pode ser configurado para permitir que os visitantes se registrem automaticamente ou façam logon com suas contas do Facebook ou Twitter.

* Pedido de registro no sítio web

   Para um grupo de usuários fechado, você pode permitir que os visitantes solicitem o registro, mas impor a autorização por meio de um fluxo de trabalho.

* Registrar cada conta do ambiente do autor

   Se você tiver um pequeno número de perfis, que precisarão de autorização mesmo assim, você pode decidir registrar cada um diretamente.

Para permitir que os visitantes se registrem, uma série de componentes e formulários podem ser usados para coletar as informações de identificação necessárias e, em seguida, as informações adicionais (geralmente opcionais) do perfil. Depois de se terem registrado, devem também poder verificar e atualizar os dados que apresentaram.

Funcionalidade adicional pode ser configurada ou desenvolvida:

* Configure qualquer replicação reversa necessária.
* Permita que um usuário remova seu perfil, desenvolvendo um formulário junto com um fluxo de trabalho.

>[!NOTE]
>
>As informações especificadas no perfil também podem ser usadas para fornecer ao usuário conteúdo direcionado por meio de [Segmentos](/help/sites-administering/campaign-segmentation.md) e [Campanhas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## Formulários de registro {#registration-forms}

Um [formulário](/help/sites-authoring/default-components.md#form-component) pode ser usado para coletar as informações de registro e, em seguida, gerar a nova conta e perfil.

Por exemplo, os usuários podem solicitar um novo perfil, usando a página Geometrixx`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![formulário registrado](assets/registerform.png)

Ao enviar a solicitação, a página de perfil é aberta onde o usuário pode fornecer detalhes pessoais.

![profilepage](assets/profilepage.png)

A nova conta também está visível no console [](/help/sites-administering/security.md)Usuários.

## Logon {#login}

O componente de logon pode ser usado para coletar as informações de logon e, em seguida, ativar o processo de logon.

Isso fornece ao visitante os campos padrão de Nome de **usuário** e **Senha**, com um botão **Logon** para ativar o processo de logon quando as credenciais forem inseridas.

Por exemplo, os usuários podem fazer logon ou criar uma nova conta usando a opção **Fazer logon** na barra de ferramentas Geometrixx, que usa a página:

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![login](assets/login.png)

## Desconectando {#logging-out}

Como há um mecanismo de logon, também é necessário um mecanismo de logout. Isso está disponível como a opção **Sair** no Geometrixx.

## Exibindo e Atualizando um Perfil {#viewing-and-updating-a-profile}

Dependendo do formulário de inscrição, o visitante pode ter registrado informações em seu perfil. Eles devem poder ver e/ou atualizar isso em uma fase posterior. Isso pode ser feito com uma forma semelhante; por exemplo, no Geometrixx:

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

Para ver os detalhes do seu perfil, clique em **Meu perfil** no canto superior direito de qualquer página; por exemplo, com a `admin` conta:
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

Você pode exibir outro perfil usando o contexto [](/help/sites-administering/client-context.md) cliente (no ambiente do autor e com privilégios suficientes):

1. Abrir uma página; por exemplo, a página Geometrixx:

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. Clique em **Meu perfil** no canto superior direito. Você verá o perfil da sua conta atual; por exemplo, o administrador.
1. Pressione **control-alt-C** para abrir o contexto do cliente.
1. No canto superior esquerdo do contexto do cliente, clique no botão **Carregar um perfil** .

   ![](do-not-localize/loadprofile.png)

1. Selecione outro perfil na lista suspensa da janela de diálogo; por exemplo, **Alison Parker**.
1. Clique em **OK**.
1. Clique novamente em **Meu perfil**. O formulário será atualizado com os detalhes de Alison.

   ![profilealisão](assets/profilealison.png)

1. Agora você pode usar **Editar perfil** ou **Alterar senha** para atualizar os detalhes.

## Adicionar campos à definição de perfil {#adding-fields-to-the-profile-definition}

É possível adicionar campos à definição do perfil. Por exemplo, para adicionar um campo &quot;Cor favorita&quot; ao perfil do Geometrixx:

1. No console Sites, navegue até Geometrixx Outdoors Site > Inglês > Usuário > Meu perfil.
1. Clique duas vezes na página **Meu perfil** para abri-lo para edição.
1. Na guia **Componentes** do sidekick, expanda a seção **Formulário** .
1. Arraste uma Lista **suspensa do sidekick para o formulário, logo abaixo do campo** Sobre mim **** .
1. Clique duas vezes no componente Lista **** suspensa para abrir a caixa de diálogo para configuração e digite:

   * **Nome do elemento** - `favoriteColor`
   * **Título** - `Favorite Color`
   * **Itens** - Adicionar várias cores como itens
   Clique em **OK** para salvar.

1. Feche a página e retorne ao console **Sites** e ative a página Meu perfil.

   Na próxima vez que você visualizar um perfil, poderá selecionar uma cor favorita:

   ![aparkerfavcolor](assets/aparkerfavcolour.png)

   O campo será salvo na seção de **perfil** da conta de usuário relevante:

   ![aparkercrxdelite](assets/aparkercrxdelite.png)

## Estados de perfil {#profile-states}

Há vários casos de uso que exigem saber se um usuário (ou melhor, seu perfil) está em um estado ** específico ou não.

Isso envolve definir uma propriedade apropriada no perfil do usuário de uma forma que:

* estiver visível e acessível ao usuário
* define dois estados para cada propriedade
* permite alternar entre os dois estados definidos

Isso é feito com:

* [Provedores de estado](#state-providers)

   Gerenciar os dois estados de uma propriedade específica e as transições entre os dois.

* [Fluxos de trabalhos](#workflows)

   Para gerenciar ações relacionadas aos estados.

É possível definir vários estados; por exemplo, no Geometrixx eles incluem:

* inscrição (ou cancelamento de inscrição) em notificações em boletins informativos ou encadeamentos de comentários
* adicionar e remover uma conexão a um amigo

### Provedores de estado {#state-providers}

Um provedor de estado gerencia o estado atual da propriedade em questão, juntamente com as transições entre os dois estados possíveis.

Os provedores de estado são implementados como componentes, portanto, podem ser personalizados para seu projeto. No Geometrixx, isso inclui:

* Assinar/Cancelar assinatura de tópico do fórum
* Adicionar/remover amigos

### Fluxos de trabalhos {#workflows}

Os provedores de estado gerenciam uma propriedade de perfil e seus estados.

É necessário um fluxo de trabalho para implementar as ações relacionadas aos estados. Por exemplo, ao se inscrever para receber notificações, o fluxo de trabalho lidará com a ação de assinatura real; ao cancelar a inscrição das notificações, o fluxo de trabalho processará a remoção do usuário da lista de assinaturas.

## Perfis e contas de usuário {#profiles-and-user-accounts}

Os perfis são armazenados no Repositório de conteúdo como parte da conta[](/help/sites-administering/user-group-ac-admin.md)do usuário.

O perfil pode ser encontrado em `/home/users/geometrixx`:

![chlimage_1-138](assets/chlimage_1-138.png)

Em uma instalação padrão (autor ou publicação) todos têm acesso de leitura a todas as informações de perfil de todos os usuários. todos são um &quot;grupo *incorporado&quot; que contém automaticamente todos os usuários e grupos existentes. A lista de membros não pode ser editada*&quot;.

Esses direitos de acesso são definidos pela seguinte ACL curinga:

/home todos permitem jcr:read rep:wide = */profile*

Isso permite:

* fórum, comentários ou postagens de blog para exibir informações (como ícone ou nome completo) do perfil apropriado
* links para páginas de perfil do geometrixx

Se esse acesso não for apropriado para sua instalação, você poderá alterar essas configurações padrão.

Isso pode ser feito usando a guia Controle **[de](/help/sites-administering/user-group-ac-admin.md#access-right-management)**acesso:

![gestor](assets/aclmanager.png)

## Componentes de perfil {#profile-components}

Uma variedade de componentes de perfil também está disponível para definir os requisitos de perfil do site.

### Campo de senha marcado {#checked-password-field}

Esse componente fornece dois campos para:

* inserir uma senha
* uma verificação para confirmar que a senha foi inserida corretamente.

Com as configurações padrão, o componente será exibido da seguinte forma:

![dc_files_checkedpassword](assets/dc_profiles_checkedpassword.png)

### Foto de avatar do perfil {#profile-avatar-photo}

Esse componente fornece ao usuário um mecanismo para selecionar e carregar um arquivo Avatar Photo.

![dc_profile_avatarphoto](assets/dc_profiles_avatarphoto.png)

### Nome detalhado de perfil {#profile-detailed-name}

Esse componente permite que o usuário insira um nome detalhado.

![dc_files_details_name](assets/dc_profiles_detailedname.png)

### Gênero do perfil {#profile-gender}

Esse componente permite que o usuário insira seu gênero.

![dc_profile_gender](assets/dc_profiles_gender.png)

