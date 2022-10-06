---
title: Configuração inicial
seo-title: Initial Setup
description: Como configurar comunidades
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# Configuração inicial {#initial-setup}

## Iniciar instâncias de autor e publicação {#start-author-and-publish-instances}

Para fins de desenvolvimento e demonstração, será necessário executar um autor e uma instância de publicação.

Para fazer isso, siga as AEM básicas [Introdução](../../help/sites-deploying/deploy.md#getting-started) instruções, que resultarão em:

* Ambiente de criação em [localhost:4502](http://localhost:4502/)
* Publicar ambiente em [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* O ambiente de criação é para:

   * Desenvolvimento de sites, modelos e componentes.
   * Tarefas administrativas e de configuração.

* O ambiente de publicação serve para:

   * A experiência da comunidade de publicação e moderação de conteúdo.
   * Criação de grupos de comunidade, membros e grupos de membros.

>[!NOTE]
>
>Se não estiver familiarizado com AEM, visualize a documentação em [tratamento básico](../../help/sites-authoring/basic-handling.md) e [guia rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instale a versão mais recente das comunidades {#install-latest-communities-release}

Este tutorial cria um [site da comunidade de engajamento](overview.md#engagement-community) e é baseado no pacote de recursos do AEM Communities 6.2 versão 1.10.

Para garantir que o pacote de recursos mais recente esteja instalado, visite:

* [Versões mais recentes](deploy-communities.md#latest-releases)

Para um tutorial que cria um [site da comunidade de ativação](overview.md#enablement-community), visita [Introdução ao AEM Communities para ativação](getting-started-enablement.md).

## Configurar Analytics {#configure-analytics}

When [O Adobe Analytics está configurado para o site da comunidade](analytics.md), estão disponíveis informações sobre a atividade da comunidade que melhoram a experiência do membro da comunidade e fornecem feedback aos administradores do site.

A integração com o Adobe Analytics é opcional.

## Configurar email para notificações {#configure-email-for-notifications}

O recurso de notificações, disponível por padrão para todos os sites criados usando o `Communities Sites` , fornece um canal de email para notificações.

O que é necessário é que o email seja configurado corretamente para o site.

Consulte [Configuração de email](email.md).

## Ative o serviço de túnel {#enable-the-tunnel-service}

Ao criar um site da comunidade no ambiente de criação, o serviço de túnel possibilita a atribuição de funções a membros confiáveis da comunidade registrados no ambiente de publicação. O serviço de túnel também permite acesso aos membros da comunidade do [Consoles Membros e grupos](members.md) no ambiente de criação.

A convenção é para membros e grupos de membros criados no ambiente de publicação para *not* ser recriado no ambiente do autor. Para obter mais informações, consulte [Gerenciar usuários e grupos de usuários](users.md).

Para obter instruções simples para habilitar o serviço de túnel em um **autor** instância, consulte [Serviço de túnel](deploy-communities.md#tunnel-service-on-author).

## Função de administrador da comunidade {#community-administrator-role}

Os membros do grupo Administradores da Comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem banir membros da comunidade) e moderar conteúdo.

### Criar usuário {#create-user}

Criar um usuário em *autor*, a quem é atribuída a função de Administrador da Comunidade:

* Na instância do autor

   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)

* Fazer logon com privilégios de administrador

   * Por exemplo, nome de usuário &#39;admin&#39; / senha &#39;admin&#39;

* No console principal, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* No **Editar** selecione **[!UICONTROL Adicionar usuário]**

* No `Create New User` centro de diálogo:

   * **[!UICONTROL ID]**: sírio
   * **[!UICONTROL Endereço Emai]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Senha]**: senha
   * **[!UICONTROL Confirmar &amp;senha;]**: senha
   * **[!UICONTROL Nome]**: Sirius
   * **[!UICONTROL Sobrenome]**: Nilson

### Atribuir Sirius ao Grupo de Administradores da Comunidade {#assign-sirius-to-community-administrators-group}

Role para baixo até `Add User to Groups`:

* Digite &#39;C&#39; para pesquisar

   * Selecionar `Community Administrators`
   * Selecionar `Community Enablement Managers`

* Selecione **[!UICONTROL Salvar]**.

![create-user](assets/create-user.png)

## Ativar o logon do Social {#enable-social-login}

Antes que as versões de demonstração do logon social com o Facebook e o Twitter possam ser usadas, é necessário

1. Instale um pacote de correções ou [pacote de recursos mais recente](deploy-communities.md#latestfeaturepack) (para alterações na API do Facebook em março de 2017).
1. [Ativar o provedor OAuth](social-login.md#adobe-granite-oauth-authentication-handler) no ambiente de publicação.

Para servidores de produção, é necessário criar os serviços em nuvem necessários para fornecer logon social.

Consulte [Logon no Social com Facebook e Twitter](social-login.md).

## Criar tags tutoriais {#create-tutorial-tags}

Crie tags para usar nos tutoriais de engajamento e ativação, usando o namespace de tag de `Tutorial`.

Use o [Console de marcação](../../help/sites-administering/tags.md#tagging-console) para criar as seguintes tags:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tags tutoriais](assets/tutorial-tags.png)

Siga as instruções para:

1. [Defina as permissões da tag](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Publicar as tags](../../help/sites-administering/tags.md#publishing-tags).

Pacote de exemplo de tags criadas para o Tutorials de introdução do AEM Communities

[Obter arquivo](assets/tutorial_tags-v63.zip)

## MongoDB para UGC Common Store {#mongodb-for-ugc-common-store}

É recomendável, mas opcional, definir [MSRP](msrp.md) (MongoDB) como o [loja comum](working-with-srp.md) para experimentar a flexibilidade da moderação de todo o UGC de ambientes de publicação e/ou autor.

Para obter instruções, visite [Como configurar o MongoDB para demonstração](demo-mongo.md).

Por padrão, a instalação das instâncias de autor e publicação AEM resulta no armazenamento do conteúdo gerado pelo usuário (UGC) em [Armazenamento JCR Tar](../../help/sites-deploying/platform.md) acessado usando [JSRP](jsrp.md). O JSRP não é um armazenamento comum, o que significa que o UGC é visível somente na instância em que foi inserido. Normalmente, o UGC é inserido em uma instância de publicação e não fica visível no ambiente do autor, resultando em todas as tarefas de moderação que precisam usar a instância de publicação.
