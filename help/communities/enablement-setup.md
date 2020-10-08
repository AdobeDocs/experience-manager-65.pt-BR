---
title: Configuração inicial para ativação
seo-title: Configuração inicial
description: Configuração inicial para ativação
seo-description: Configuração inicial para ativação
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---


# Configuração inicial para ativação  {#initial-setup-for-enablement}

## Instâncias de autor e publicação do start {#start-author-and-publish-instances}

Para fins de desenvolvimento e demonstração, será necessário executar uma instância de autor e uma instância de publicação.

Siga as instruções AEM básicas de [Introdução](../../help/sites-deploying/deploy.md#getting-started) que resultarão em

* Ambiente do autor em [localhost:4502](http://localhost:4502/)
* Publicar ambiente no [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* O ambiente do autor é para:

   * Desenvolvimento de sites, modelos, componentes, recursos de ativação e caminhos de aprendizado.
   * Atribuição de membros e grupos de membros para ativar recursos e caminhos de aprendizado.
   * Geração de relatórios em atribuições, visualizações e postagens.
   * Tarefas administrativas e de configuração.

* O ambiente publish é para:

   * Aprendizagem/treinamento com base em tópicos gerenciados pelo Gerenciador de ativação.
   * Recursos de ativação de comentários e classificações e caminhos de aprendizado.
   * Entrar em contato com os contatos de recursos.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, visualização a documentação sobre manuseio [](../../help/sites-authoring/basic-handling.md) básico e um guia [rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalar a versão mais recente das comunidades {#install-latest-communities-release}

Este tutorial cria um site [de comunidade de](overview.md#enablement-community)ativação. Para verificar se o pacote de recursos mais recente está instalado, visite:

* [Versões mais recentes](deploy-communities.md#latest-releases)

Para obter um tutorial que cria um site [de comunidade de](overview.md#engagement-community)envolvimento, visite [Introdução ao AEM Communities](getting-started.md).

## Configurar recursos de ativação {#configure-enablement-features}

Para seguir este tutorial, é necessário instalar e [configurar corretamente a ativação](enablement.md), que requer produtos de terceiros, como MySQL e FFmpeg.

## Configurar Analytics {#configure-analytics}

Quando o [Adobe Analytics está configurado para o site](analytics.md)da comunidade, mais informações estão disponíveis nos [relatórios](reports.md) gerados nos recursos de ativação e caminhos de aprendizado atribuídos aos membros da comunidade (alunos).

## Configurar email para notificações {#configure-email-for-notifications}

O recurso de notificações, disponível por padrão para todos os sites criados usando o `Communities Sites` console, fornece um canal de email para notificações.

O que é necessário é que o email seja configurado corretamente para o site.

See [Configuring Email](email.md).

## Ativar o serviço de túnel {#enable-the-tunnel-service}

Ao criar um site da comunidade no ambiente do autor, o serviço de túnel possibilita a criação e o gerenciamento de usuários e grupos de usuários registrados no ambiente de publicação (membros), a atribuição de funções a membros da comunidade confiáveis e a atribuição de conteúdo a alunos.

Para obter mais informações, consulte [Gerenciamento de usuários e grupos](users.md)de usuários.

Para obter instruções simples para habilitar o serviço de túnel, consulte Serviço [de](deploy-communities.md#tunnel-service-on-author)Túnel.

## Criar tags do tutorial {#create-tutorial-tags}

Crie tags para usar nos tutoriais de envolvimento e ativação, usando a namespace de tags de `Tutorial`.

Use o console [](../../help/sites-administering/tags.md#tagging-console) Marcação para criar as seguintes tags:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tags tutoriais](assets/tutorial-tags.png)

Em seguida, siga as instruções para:

1. [Definir as permissões da tag](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicar as tags](../../help/sites-administering/tags.md#publishing-tags)

Pacote de amostra de tags criadas para os Tutorials de Introdução do AEM Communities

[Obter arquivo](assets/communities_tutorialtags-10.zip)

## Criar membros e grupos de ativação {#create-enablement-members-and-groups}

Para um site da comunidade de ativação, os visitantes do site não devem ser capazes de se [autoregistrar nem usar o login](sites-console.md#user-management)social.

Em vez disso, com o serviço [de](#enable-the-tunnel-service) túnel ativado, o console [](members.md) Membros é usado para registrar novos membros no ambiente de publicação.

Neste tutorial, três membros são criados no ambiente de publicação. Dois membros se tornarão membros de um grupo de usuários atribuído a um caminho de aprendizado, enquanto o terceiro membro se tornará um contato de recurso de ativação.

Um quarto usuário é criado no ambiente do autor e recebe as funções de Administrador das Comunidades e Gerente de Ativação da Comunidade.

>[!NOTE]
>
>Esses membros estão sendo criados antes da criação do site da comunidade do Tutorial *de* ativação.
>
>Se forem criados depois, eles poderão ser adicionados como membros do grupo *de membros do Tutorial de* ativação durante a criação do membro.
>
>Em vez disso, mais tarde, eles serão [atribuídos ao grupo](enablement-create-site.md#assignuserstocommunityenablemembersgroup)de membros.

### Riley Taylor - Inscrito {#riley-taylor-enrollee}

[Crie um membro](members.md#create-new-member) que será adicionado a um grupo de alunos - o grupo Classe de esqui da comunidade.

* **ID**: estrada
* **Email**: riley.taylor@mailinator.com
* **Senha**: password
* **Confirmar senha**: password
* **Nome**: Riley
* **Sobrenome**: Taylor

### Sidney Croft - Inscrito {#sidney-croft-enrollee}

[Crie um segundo membro](members.md#create-new-member) que será adicionado ao grupo Classe de esqui da comunidade.

* **ID**: calçada
* **Email**: sidney.croft@mailinator.com
* **Senha**: password
* **Confirmar senha**: password
* **Nome**: Sidney
* **Sobrenome**: Corte

### Quinn Harper - Ativação do Contato e Moderador de Recursos {#quinn-harper-enablement-resource-contact-and-moderator}

[Crie um membro](members.md#create-new-member) que será adicionado ao grupo de membros do Site da Comunidade depois que o site for criado. Essa associação permitirá que o membro seja atribuído como o Contato [de](resources.md#settings) recursos de ativação quando um recurso de ativação for criado para o site.

* **ID**: quinn
* **Email**: quinn.harper@mailinator.com
* **Senha**: password
* **Confirmar senha**: password
* **Nome**: Quinn
* **Sobrenome**: Harper

### Adicionar um grupo de usuários - Classe de esqui da comunidade {#add-a-user-group-community-ski-class}

[Adicione um novo grupo](members.md#create-new-group) chamado Classe de esqui da comunidade.

* **ID**: classe Community-ski
* **Nome**: Classe Community Ski
* **Descrição**: um grupo de exemplo para atribuir recursos de ativação
* **Adicionar membros ao grupo** &#39;add&#39;:

   * estrada
   * calçada

* Selecione **[!UICONTROL Salvar]**

### Propriedades da classe Ski da comunidade {#community-ski-class-properties}

![propriedades de classe de esqui](assets/ski-class-properties.png)

>[!NOTE]
>
>Durante a criação do site da comunidade, os membros e grupos existentes podem ser adicionados ao grupo de membros do site da comunidade.

## Função de administrador da comunidade {#community-administrator-role}

Os membros do grupo Administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo.

### Criar usuário {#create-user}

Crie um usuário no *autor*, ao qual seja atribuída a função de Administrador da comunidade:

* Na instância do autor

   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)

* Fazer logon com privilégios de administrador

   * Por exemplo, nome de usuário &#39;admin&#39; / senha &#39;admin&#39;

* No console principal, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* No menu **[!UICONTROL Editar]** , selecione **[!UICONTROL Adicionar usuário]**.

* Na `Create New User` caixa de diálogo insira:

   * **ID&amp;ast;**: sírio
   * **Endereço** Emai: sirius.nilson@mailinator.com
   * **Senha&amp;passado;**: password
   * **Confirmar Senha&amp;passado;**: password
   * **Nome**: Sirius
   * **Sobrenome&amp;ast;**: Nilson

### Atribuir Sirius ao grupo de administradores da comunidade {#assign-sirius-to-community-administrators-group}

Role para baixo até `Add User to Groups`:

* Digite &#39;C&#39; para pesquisar

   * Selecionar `Community Administrators`
   * Selecionar `Community Enablement Managers`

* Selecione **[!UICONTROL Salvar]**

![função administrativa](assets/admin-role.png)

