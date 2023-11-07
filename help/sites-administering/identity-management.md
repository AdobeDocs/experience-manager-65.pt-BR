---
title: Gerenciamento de identidade
seo-title: Identity Management
description: Saiba mais sobre o funcionamento interno do gerenciamento de identidade no AEM.
seo-description: Learn about identity management in AEM.
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 2%

---


# Gerenciamento de identidade{#identity-management}

Os visitantes individuais do seu site só podem ser identificados quando você fornece a capacidade de fazer logon. Há vários motivos pelos quais você pode querer fornecer um recurso de logon:

* [AEM Communities](/help/communities/overview.md)Os visitantes do site são necessários para fazer logon e publicar conteúdo na comunidade.
* [Grupos de usuários fechados](/help/sites-administering/cug.md)

  Talvez seja necessário limitar o acesso ao seu site (ou a seções dele) para visitantes específicos.

* [Personalização](/help/sites-administering/personalization.md) Permitir que os visitantes configurem determinados aspectos de como acessam o site.

A funcionalidade de logon (e logout) é fornecida por um [conta com um **Perfil**](#profiles-and-user-accounts), que contém informações adicionais sobre o visitante registrado (usuário). Os processos reais de registro e autorização podem diferir:

* Autorregistro no site

  A [Site da comunidade](/help/communities/sites-console.md) O pode ser configurado para permitir que os visitantes se registrem ou façam logon com suas contas do Facebook ou do Twitter.

* Solicitação de registro no site

  Para um grupo de usuários fechado, você pode permitir que os visitantes solicitem o registro, mas impor a autorização por meio de um fluxo de trabalho.

* Registrar cada conta do ambiente de criação

  Se você tiver um pequeno número de perfis que precisarão de autorização de qualquer maneira, poderá optar por registrar cada perfil diretamente.

Para permitir que os visitantes se registrem, uma série de componentes e formulários podem ser usados para coletar as informações de identificação necessárias e, em seguida, as informações de perfil adicionais (geralmente opcionais). Depois de se registrarem, também devem poder verificar e atualizar os dados que enviaram.

Funcionalidades adicionais podem ser configuradas ou desenvolvidas:

* Configure qualquer replicação reversa necessária.
* Permitir que um usuário remova seu perfil, desenvolvendo um formulário junto com um fluxo de trabalho.

>[!NOTE]
>
>As informações especificadas no perfil também podem ser usadas para fornecer conteúdo direcionado ao usuário por meio do [Segmentos](/help/sites-administering/campaign-segmentation.md) e [Campanhas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## Forms de registro {#registration-forms}

A [formulário](/help/sites-authoring/default-components.md#form-component) O pode ser usado para coletar as informações de registro e gerar a nova conta e perfil.

Por exemplo, os usuários podem solicitar um novo perfil, usando a página Geometrixx
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![Exemplo de formulário de registro](assets/registerform.png)

Ao enviar a solicitação, a página de perfil é aberta, onde o usuário pode fornecer detalhes pessoais.

![Exemplo de página de perfil](assets/profilepage.png)

A nova conta também está visível no [Console de usuários](/help/sites-administering/security.md).

## Logon {#login}

O componente de logon pode ser usado para coletar as informações de logon e ativar o processo de logon.

Isso fornece ao visitante os campos padrão de **Nome de usuário** e **Senha**, com um **Logon** botão para ativar o processo de logon quando as credenciais forem inseridas.

Por exemplo, os usuários podem fazer logon ou criar uma conta usando a **Conectar** na barra de ferramentas do Geometrixx, que usa a página:

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![Exemplo de página de logon](assets/login.png)

## Efetuando logout {#logging-out}

Como há um mecanismo de logon, também é necessário um mecanismo de logout. Isso está disponível como **Sair** no Geometrixx.

## Exibir e atualizar um perfil {#viewing-and-updating-a-profile}

Dependendo do formulário de registro, o visitante pode ter registrado informações em seu perfil. Eles devem ser capazes de exibir e/ou atualizar isso em um estágio posterior. Isso pode ser feito com um formulário semelhante; por exemplo, no Geometrixx:

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

Para ver os detalhes do seu perfil, clique em **Meu perfil** no canto superior direito de qualquer página; por exemplo, com a tag `admin` conta:
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

É possível exibir outro perfil usando a variável [contexto do cliente](/help/sites-administering/client-context.md) (no ambiente de criação e com privilégios suficientes):

1. Abra uma página; por exemplo, a página Geometrixx:

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. Clique em **Meu perfil** no canto superior direito. Você verá o perfil da conta atual; por exemplo, o administrador.
1. Pressione **control-alt-C** para abrir o contexto do cliente.
1. No canto superior esquerdo do contexto do cliente, clique na **Carregar um perfil** botão.

   ![Carregar um ícone de perfil](do-not-localize/loadprofile.png)

1. Selecione outro perfil na lista suspensa na janela de diálogo; por exemplo, **Alison Parker**.
1. Clique em **OK**.
1. Clique novamente em **Meu perfil**. O formulário será atualizado com os detalhes de Alison.

   ![Exemplo de perfil de Alison](assets/profilealison.png)

1. Agora você pode usar **Editar perfil** ou **Alterar senha** para atualizar os detalhes.

## Adicionar campos à definição do perfil {#adding-fields-to-the-profile-definition}

É possível adicionar campos à definição do perfil. Por exemplo, para adicionar um campo &quot;Cor favorita&quot; ao perfil do Geometrixx:

1. No console Sites, navegue até Geometrixx Outdoors Site > Inglês > Usuário > Meu perfil.
1. Clique duas vezes na guia **Meu perfil** para abri-la para edição.
1. No **Componentes** guia do sidekick expanda a **Formulário** seção.
1. Arraste um **Lista suspensa** do sidekick para o formulário, logo abaixo do **Sobre mim** campo.
1. Clique duas vezes no ícone **Lista suspensa** para abrir a caixa de diálogo de configuração e inserir:

   * **Nome do elemento** - `favoriteColor`
   * **Título** - `Favorite Color`
   * **Itens** - Adicionar várias cores como itens

   Clique em **OK** para salvar.

1. Feche a página e retorne à **Sites** e ative a página Meu perfil.

   Na próxima vez que visualizar um perfil, você poderá selecionar uma cor favorita:

   ![Campo de amostra de cor favorita de Alison Parker](assets/aparkerfavcolour.png)

   O campo será salvo sob o **perfil** seção da conta de usuário relevante:

   ![Dados de Alison Parker no CRXDE](assets/aparkercrxdelite.png)

## Estados do perfil {#profile-states}

Há vários casos de uso que exigem saber se um usuário (ou seu perfil) está em uma *estado específico* ou não.

Isso envolve definir uma propriedade apropriada no perfil do usuário de forma que:

* está visível e acessível ao usuário
* define dois estados para cada propriedade
* permite alternar entre os dois estados definidos

Isso é feito com:

* [Provedores de Estado](#state-providers)

  Para gerenciar os dois estados de uma propriedade específica e as transições entre os dois.

* [Fluxos de trabalhos](#workflows)

  Para gerenciar ações relacionadas aos estados.

Vários estados podem ser definidos; por exemplo, em Geometrixx, eles incluem:

* assinatura (ou cancelamento de assinatura) de notificações em informativos ou threads de comentários
* adicionar e remover uma conexão com um amigo

### Provedores de Estado {#state-providers}

Um provedor de estado gerencia o estado atual da propriedade em questão, juntamente com as transições entre os dois estados possíveis.

Os provedores de estado são implementados como componentes, portanto, podem ser personalizados para o seu projeto. No Geometrixx, incluem-se:

* Assinar/Cancelar assinatura de tópico do fórum
* Adicionar/Remover Amigo

### Fluxos de trabalhos {#workflows}

Os provedores de estado gerenciam uma propriedade de perfil e seus estados.

Um workflow é necessário para implementar as ações relacionadas aos estados. Por exemplo, ao assinar notificações, o fluxo de trabalho tratará a ação de assinatura real; ao cancelar a assinatura das notificações, o fluxo de trabalho tratará da remoção do usuário da lista de assinatura.

## Perfis e contas de usuário {#profiles-and-user-accounts}

Os perfis são armazenados no repositório de conteúdo como parte da[conta de usuário](/help/sites-administering/user-group-ac-admin.md).

O perfil pode ser encontrado em `/home/users/geometrixx`:

![Perfis como vistos no CRXDE](assets/chlimage_1-138.png)

Em uma instalação padrão (autor ou publicação), todos têm acesso de leitura a todas as informações de perfil de todos os usuários. todo mundo é &quot;*Grupo interno que contém automaticamente todos os usuários e grupos existentes. A lista de membros não pode ser editada*&quot;.

Esses direitos de acesso são definidos pela seguinte ACL curinga:

/home todos permitem jcr:read rep:glob = &#42;/profile&#42;

Isso permite:

* fórum, comentários ou publicações do blog para exibir informações (como ícone ou nome completo) do perfil apropriado
* links para páginas de perfil do geometrixx

Se esse acesso não for adequado para a sua instalação, você poderá alterar essas configurações padrão.

Isso pode ser feito usando o **[Controle de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management)** guia:

![Gerenciando ACLs no CRXDE](assets/aclmanager.png)

## Componentes do perfil {#profile-components}

Uma faixa de componentes de perfil também está disponível para definir os requisitos de perfil do seu local.

### Campo de senha marcado {#checked-password-field}

Esse componente fornece dois campos para:

* a entrada de uma senha
* uma verificação para confirmar se a senha foi inserida corretamente.

Com as configurações padrão, o componente será exibido da seguinte maneira:

![Caixa de diálogo Verificar senha](assets/dc_profiles_checkedpassword.png)

### Foto de avatar do perfil  {#profile-avatar-photo}

Esse componente fornece ao usuário um mecanismo para selecionar e fazer upload de um arquivo de foto de avatar.

![Seletor de avatar](assets/dc_profiles_avatarphoto.png)

### Nome detalhado de perfil {#profile-detailed-name}

Esse componente permite que o usuário insira um nome detalhado.

![Caixa de diálogo de nome detalhado](assets/dc_profiles_detailedname.png)

### Gênero do perfil {#profile-gender}

Esse componente permite que o usuário insira seu gênero.

![Seletor de gênero](assets/dc_profiles_gender.png)
