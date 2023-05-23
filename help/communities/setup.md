---
title: Configuração inicial
seo-title: Initial Setup
description: Configuração de comunidades
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---

# Configuração inicial {#initial-setup}

## Iniciar instâncias de criação e publicação {#start-author-and-publish-instances}

Para fins de desenvolvimento e demonstração, será necessário executar um autor e uma instância de publicação.

Para isso, siga o AEM básico [Introdução](../../help/sites-deploying/deploy.md#getting-started) instruções, o que resultará em:

* Ambiente de autor em [localhost:4502](http://localhost:4502/)
* Publicar ambiente em [localhost:4503](http://localhost:4503/)

Para o AEM Communities,

* O ambiente de criação do é para:

   * Desenvolvimento de sites, modelos e componentes.
   * Tarefas administrativas e de configuração.

* O ambiente de publicação é para:

   * A experiência da comunidade na publicação e moderação de conteúdo.
   * Criação de grupos da comunidade, membros e grupos de membros.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, consulte a documentação em [manuseio básico](../../help/sites-authoring/basic-handling.md) e uma [guia rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalar versão mais recente do Communities {#install-latest-communities-release}

Este tutorial cria um [site da comunidade de engajamento](overview.md#engagement-community) e é baseado no pacote de recursos do AEM Communities 6.2 versão 1.10.

Para verificar se o pacote de recursos mais recente está instalado, visite:

* [Versões mais recentes](deploy-communities.md#latest-releases)

## Configurar Analytics {#configure-analytics}

Quando [O Adobe Analytics está configurado para o site da comunidade](analytics.md)No entanto, informações sobre a atividade da comunidade estão disponíveis para aprimorar a experiência do membro da comunidade e para fornecer feedback aos administradores do site.

A integração com o Adobe Analytics é opcional.

## Configurar email para notificações {#configure-email-for-notifications}

O recurso de notificações, disponível por padrão para todos os sites criados usando o `Communities Sites` fornece um canal de email para notificações.

O que é necessário é que o e-mail seja configurado corretamente para o site.

Consulte [Configuração de email](email.md).

## Habilitar o serviço de túnel {#enable-the-tunnel-service}

Ao criar um site da comunidade no ambiente de criação, o serviço de túnel possibilita atribuir funções a membros confiáveis da comunidade registrados no ambiente de publicação. O serviço de túnel também permite acesso a membros da comunidade a partir do [Consoles Membros e grupos](members.md) no ambiente de criação.

A convenção é para membros e grupos de membros criados no ambiente de publicação para *não* ser recriado no ambiente de criação. Para obter mais informações, consulte [Gerenciar usuários e grupos de usuários](users.md).

Para obter instruções simples para habilitar o serviço de túnel em um **autor** instância, consulte [Serviço de túnel](deploy-communities.md#tunnel-service-on-author).

## Função de administrador da comunidade {#community-administrator-role}

Os membros do grupo Administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo.

### Criar usuário {#create-user}

Criar um usuário em *autor*, a quem foi atribuída a função de Administrador da comunidade:

* Na instância do autor

   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)

* Entrar com privilégios de administrador

   * Por exemplo, nome de usuário &#39;admin&#39; / senha &#39;admin&#39;

* No console principal, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* No **Editar** selecione **[!UICONTROL Adicionar usuário]**

* No `Create New User` caixa de diálogo digite:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Endereço de e-mail]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Senha]**: senha
   * **[!UICONTROL Confirmar Senha&amp;ast;]**: senha
   * **[!UICONTROL Nome]**: Sirius
   * **[!UICONTROL Sobrenome]**: Nilson

### Atribuir a Sirius ao grupo de administradores da comunidade {#assign-sirius-to-community-administrators-group}

Role para baixo até `Add User to Groups`:

* Digite &quot;C&quot; para pesquisar

   * Selecionar `Community Administrators`
   * Selecionar `Community Enablement Managers`

* Selecione **[!UICONTROL Salvar]**.

![create-user](assets/create-user.png)

## Ativar logon social {#enable-social-login}

Antes que as versões de demonstração do logon social com Facebook e Twitter possam ser usadas, é necessário

1. Instalar um fix pack ou [pacote de recursos mais recente](deploy-communities.md#latestfeaturepack) (para alterações de março de 2017 na API do Facebook).
1. [Ativar o provedor OAuth](social-login.md#adobe-granite-oauth-authentication-handler) no ambiente de publicação.

Para servidores de produção, é necessário criar os serviços em nuvem necessários para fornecer logon social.

Consulte [Logon social com a Facebook e o Twitter](social-login.md).

## Criar tags do tutorial {#create-tutorial-tags}

Crie tags para usar nos tutoriais do engage, usando o namespace de tag de `Tutorial`.

Use o [Console de marcação](../../help/sites-administering/tags.md#tagging-console) para criar as seguintes tags:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Em seguida, siga as instruções para:

1. [Definir as permissões da tag](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Publicar as tags](../../help/sites-administering/tags.md#publishing-tags).

Exemplo de pacote de tags criado para os Tutorials de introdução do AEM Communities

[Obter arquivo](assets/tutorial_tags-v63.zip)

## MongoDB para armazenamento comum de UGC {#mongodb-for-ugc-common-store}

É recomendável, mas opcional, definir [MSRP](msrp.md) (MongoDB) como o [armazenamento comum](working-with-srp.md) para experimentar a flexibilidade de moderar todo o UGC de ambientes de publicação e/ou criação.

Para obter instruções, visite [Como configurar o MongoDB para demonstração](demo-mongo.md).

Por padrão, a instalação das instâncias do autor e da publicação AEM resulta no armazenamento do conteúdo gerado pelo usuário (UGC) no [Armazenamento JCR Tar](../../help/sites-deploying/platform.md) que é acessada usando [JSRP](jsrp.md). JSRP não é um armazenamento comum, o que significa que o UGC é visível somente na instância em que foi inserido. Normalmente, o UGC é inserido em uma instância de publicação e não estaria visível no ambiente de criação, resultando em todas as tarefas de moderação que precisam usar a instância de publicação.
