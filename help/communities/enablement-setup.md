---
title: Configuração inicial para ativação
seo-title: Initial Setup
description: Configuração inicial para ativação
seo-description: Initial Setup for Enablement
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 2%

---

# Configuração inicial para ativação  {#initial-setup-for-enablement}

## Iniciar instâncias de autor e publicação {#start-author-and-publish-instances}

Para fins de desenvolvimento e demonstração, será necessário executar um autor e uma instância de publicação.

Siga as AEM básicas [Introdução](../../help/sites-deploying/deploy.md#getting-started) instruções que resultarão em

* Ambiente de criação em [localhost:4502](http://localhost:4502/)
* Publicar ambiente em [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* O ambiente de criação é para:

   * Desenvolvimento de sites, modelos, componentes, recursos de ativação e caminhos de aprendizado.
   * Atribuição de membros e grupos de membros para habilitar recursos e caminhos de aprendizado.
   * Geração de relatórios sobre atribuições, exibições e postagens.
   * Tarefas administrativas e de configuração.

* O ambiente de publicação serve para:

   * Aprendizagem/treinamento com base em tópicos gerenciados pelo Gerenciador de ativação.
   * Comentários e classificação de recursos de ativação e caminhos de aprendizado.
   * Entrar em contato com os contatos de recursos.

>[!NOTE]
>
>Se não estiver familiarizado com AEM, visualize a documentação em [tratamento básico](../../help/sites-authoring/basic-handling.md) e [guia rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instale a versão mais recente das comunidades {#install-latest-communities-release}

Este tutorial cria um [site da comunidade de ativação](overview.md#enablement-community). Para garantir que o pacote de recursos mais recente esteja instalado, visite:

* [Versões mais recentes](deploy-communities.md#latest-releases)

Para um tutorial que cria um [site da comunidade de engajamento](overview.md#engagement-community), visita [Introdução ao AEM Communities](getting-started.md).

## Configurar recursos de ativação {#configure-enablement-features}

Para seguir este tutorial, é necessário instalar e instalar corretamente o [configurar ativação](enablement.md), que requer produtos de terceiros, como MySQL e FFmpeg.

## Configurar Analytics {#configure-analytics}

When [O Adobe Analytics está configurado para o site da comunidade](analytics.md), mais informações estão disponíveis no [relatórios](reports.md) gerado em recursos de ativação e caminhos de aprendizado atribuídos a membros da comunidade (aprendentes).

## Configurar email para notificações {#configure-email-for-notifications}

O recurso de notificações, disponível por padrão para todos os sites criados usando o `Communities Sites` , fornece um canal de email para notificações.

O que é necessário é que o email seja configurado corretamente para o site.

Consulte [Configuração de email](email.md).

## Ative o serviço de túnel {#enable-the-tunnel-service}

Ao criar um site da comunidade no ambiente de criação, o serviço de túnel possibilita criar e gerenciar usuários e grupos de usuários registrados no ambiente de publicação (membros), atribuir funções a membros confiáveis da comunidade e atribuir conteúdo a alunos.

Para obter mais informações, consulte [Gerenciar usuários e grupos de usuários](users.md).

Para obter instruções simples para habilitar o serviço de túnel, consulte [Serviço de túnel](deploy-communities.md#tunnel-service-on-author).

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

1. [Defina as permissões da tag](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicar as tags](../../help/sites-administering/tags.md#publishing-tags)

Pacote de exemplo de tags criadas para o Tutorials de introdução do AEM Communities

[Obter arquivo](assets/communities_tutorialtags-10.zip)

## Criar membros e grupos de ativação {#create-enablement-members-and-groups}

Para um site da comunidade de ativação, os visitantes do site não devem ser capazes de [registrar-se automaticamente ou usar logon social](sites-console.md#user-management).

Em vez disso, com o [serviço de túnel](#enable-the-tunnel-service) ativada, a variável [Console de membros](members.md) é usada para registrar novos membros no ambiente de publicação.

Neste tutorial, três membros são criados no ambiente de publicação. Dois membros se tornarão membros de um grupo de usuários atribuído a um caminho de aprendizagem, enquanto o terceiro membro se tornará um contato de recurso de ativação.

Um quarto usuário é criado no ambiente de criação e recebe as funções de Administrador de Comunidades e Gerente de Ativação de Comunidade.

>[!NOTE]
>
>Esses membros estão sendo criados antes da criação do *Tutorial de ativação* site da comunidade.
>
>Se forem criados posteriormente, poderão ser adicionados como membros do *Grupo de membros do tutorial de ativação* durante a criação do membro.
>
>Em vez disso, mais tarde, serão [atribuído ao grupo de membros](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor - Registrando {#riley-taylor-enrollee}

[Criar um membro](members.md#create-new-member) que será adicionado a um grupo de aprendentes - o grupo de classes de esqui da comunidade.

* **ID**: ribeirinho
* **Email**: riley.taylor@mailinator.com
* **Senha**: senha
* **Confirmar senha**: senha
* **Nome**: Riley
* **Sobrenome**: Taylor

### Sidney Croft - Inscrito {#sidney-croft-enrollee}

[Criar um segundo membro](members.md#create-new-member) que serão adicionados ao grupo Classe de Esqui da Comunidade.

* **ID**: calçada
* **Email**: sidney.croft@mailinator.com
* **Senha**: senha
* **Confirmar senha**: senha
* **Nome**: Sidney
* **Sobrenome**: Corte

### Quinn Harper - Contato e Moderador de Recurso de Ativação {#quinn-harper-enablement-resource-contact-and-moderator}

[Criar um membro](members.md#create-new-member) que será adicionado ao grupo de membros do Site da Comunidade depois que o site for criado. Essa associação permitirá que o membro seja atribuído como a ativação [Contato de Recurso](resources.md#settings) quando um recurso de ativação é criado para o site.

* **ID**: quinn
* **Email**: quinn.harper@mailinator.com
* **Senha**: senha
* **Confirmar senha**: senha
* **Nome**: Quinn
* **Sobrenome**: Harper

### Adicionar um grupo de usuários - Classe de esqui da comunidade {#add-a-user-group-community-ski-class}

[Adicionar um novo grupo](members.md#create-new-group) Classe de Esqui da Comunidade nomeada.

* **ID**: classe Community-ski
* **Nome**: Classe de Esqui da Comunidade
* **Descrição**: um grupo de exemplo para atribuir recursos de ativação
* **Adicionar membros ao grupo** &#39;add&#39;:

   * ribeirinho
   * calçada

* Selecione **[!UICONTROL Salvar]**

### Propriedades da Classe de Esquema da Comunidade {#community-ski-class-properties}

![propriedades de classe de esqui](assets/ski-class-properties.png)

>[!NOTE]
>
>Durante a criação do site da comunidade, membros e grupos existentes podem ser adicionados ao grupo de membros do site da comunidade.

## Função de administrador da comunidade {#community-administrator-role}

Os membros do grupo Administradores da Comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem banir membros da comunidade) e moderar conteúdo.

### Criar usuário {#create-user}

Criar um usuário em *autor*, a quem é atribuída a função de Administrador da Comunidade:

* Na instância do autor

   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)

* Fazer logon com privilégios de administrador

   * Por exemplo, nome de usuário &#39;admin&#39; / senha &#39;admin&#39;

* No console principal, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* No **[!UICONTROL Editar]** selecione **[!UICONTROL Adicionar usuário]**.

* No `Create New User` centro de diálogo:

   * **ID&amp;ast;**: sírio
   * **Endereço Emai**: sirius.nilson@mailinator.com
   * **&amp;Senha;**: senha
   * **Confirmar &amp;senha;**: senha
   * **Nome**: Sirius
   * **&amp;Sobrenome;**: Nilson

### Atribuir Sirius ao Grupo de Administradores da Comunidade {#assign-sirius-to-community-administrators-group}

Role para baixo até `Add User to Groups`:

* Digite &#39;C&#39; para pesquisar

   * Selecionar `Community Administrators`
   * Selecionar `Community Enablement Managers`

* Selecione **[!UICONTROL Salvar]**

![função de administrador](assets/admin-role.png)
