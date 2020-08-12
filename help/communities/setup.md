---
title: Configuração inicial
seo-title: Configuração inicial
description: Configuração de comunidades
seo-description: Configuração de comunidades
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# Configuração inicial {#initial-setup}

## Instâncias de autor e publicação do start {#start-author-and-publish-instances}

Para fins de desenvolvimento e demonstração, será necessário executar um autor e uma instância de publicação.

Para fazer isso, siga as instruções AEM básicas [Introdução](../../help/sites-deploying/deploy.md#getting-started) , o que resultará em:

* Ambiente do autor em [localhost:4502](http://localhost:4502/)
* Publicar ambiente no [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* O ambiente do autor é para:

   * Desenvolvimento de sites, modelos e componentes.
   * Tarefas administrativas e de configuração.

* O ambiente publish é para:

   * A experiência da comunidade de publicar e moderar conteúdo.
   * Criação de grupos de comunidade, membros e grupos de membros.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, visualização a documentação sobre manuseio [](../../help/sites-authoring/basic-handling.md) básico e um guia [rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).


## Instalar a versão mais recente das comunidades {#install-latest-communities-release}

Este tutorial cria um site [de comunidade de](overview.md#engagement-community) envolvimento e é baseado no pacote de recursos versão 1.10 do AEM Communities 6.2.

Para verificar se o pacote de recursos mais recente está instalado, visite:

* [Versões mais recentes](deploy-communities.md#latest-releases)

Para obter um tutorial que cria um site [de comunidade de](overview.md#enablement-community)ativação, visite [Introdução à AEM Communities para Ativação](getting-started-enablement.md).

## Configurar Analytics {#configure-analytics}

Quando o [Adobe Analytics é configurado para o site](analytics.md)da comunidade, há informações disponíveis sobre a atividade da comunidade que aprimoram a experiência do membro da comunidade, além de fornecer feedback aos administradores do site.

A integração com o Adobe Analytics é opcional.

## Configurar email para notificações {#configure-email-for-notifications}

O recurso de notificações, disponível por padrão para todos os sites criados usando o `Communities Sites` console, fornece um canal de email para notificações.

O que é necessário é que o email seja configurado corretamente para o site.

See [Configuring Email](email.md).

## Ativar o serviço de túnel {#enable-the-tunnel-service}

Ao criar um site da comunidade no ambiente do autor, o serviço de túnel possibilita a atribuição de funções a membros da comunidade confiáveis registrados no ambiente de publicação. O serviço de túnel também permite acesso aos membros da comunidade dos consoles [Membros e Grupos](members.md) no ambiente do autor.

A convenção faz com que membros e grupos de membros criados no ambiente publish *não* sejam recriados no ambiente do autor. Para obter mais informações, consulte [Gerenciamento de usuários e grupos](users.md)de usuários.

Para obter instruções simples para habilitar o serviço de túnel em uma instância do **autor** , consulte Serviço [de](deploy-communities.md#tunnel-service-on-author)Túnel.

## Função de administrador da comunidade {#community-administrator-role}

Os membros do grupo Administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo.

### Criar usuário {#create-user}

Crie um usuário no *autor*, ao qual seja atribuída a função de Administrador da comunidade:

* Na instância do autor

   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)

* Fazer logon com privilégios de administrador

   * Por exemplo, nome de usuário &#39;admin&#39; / senha &#39;admin&#39;

* No console principal, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* No menu **Editar **, selecione**[!UICONTROL Adicionar usuário ]**

* Na `Create New User` caixa de diálogo insira:

   * **[!UICONTROL ID]**: sírio
   * **[!UICONTROL Endereço]** Emai: sirius.nilson@mailinator.com
   * **[!UICONTROL Senha]**: password
   * **[!UICONTROL Confirmar Senha&amp;passado;]**: password
   * **[!UICONTROL Nome]**: Sirius
   * **[!UICONTROL Sobrenome]**: Nilson

### Atribuir Sirius ao grupo de administradores da comunidade {#assign-sirius-to-community-administrators-group}

Role para baixo até `Add User to Groups`:

* Digite &#39;C&#39; para pesquisar

   * Selecionar `Community Administrators`
   * Selecionar `Community Enablement Managers`

* Selecione **[!UICONTROL Salvar]**.

![create-user](assets/create-user.png)

## Ativar login do Social {#enable-social-login}

Antes que as versões de demonstração de login social com Facebook e Twitter possam ser usadas, é necessário

1. Instale um pacote de correções ou o pacote de recursos [mais recente](deploy-communities.md#latestfeaturepack) (para alterações na API do Facebook em março de 2017).
1. [Ative o provedor](social-login.md#adobe-granite-oauth-authentication-handler) OAuth no ambiente publish.

Para servidores de produção, é necessário criar os serviços em nuvem necessários para fornecer o logon social.

Consulte Logon [social com Facebook e Twitter](social-login.md).

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

1. [Defina as permissões](../../help/sites-administering/tags.md#setting-tag-permissions)da tag.
1. [Publique as tags](../../help/sites-administering/tags.md#publishing-tags).

Pacote de amostra de tags criadas para os Tutorials de Introdução do AEM Communities

[Obter arquivo](assets/tutorial_tags-v63.zip)

## MongoDB para UGC Common Store {#mongodb-for-ugc-common-store}

É recomendável, mas opcional, definir o [MSRP](msrp.md) (MongoDB) como o repositório [](working-with-srp.md) comum para experimentar a flexibilidade de moderar todo o UGC dos ambientes de publicação e/ou autor.

Para obter instruções, consulte [Como configurar o MongoDB para demonstração](demo-mongo.md).

Por padrão, a instalação das instâncias do autor e publicação AEM resulta no armazenamento do conteúdo gerado pelo usuário (UGC) no armazenamento [de barra](../../help/sites-deploying/platform.md) JCR acessado usando o [JSRP](jsrp.md). O JSRP não é uma loja comum, o que significa que o UGC está visível somente na instância em que foi inserido. Normalmente, o UGC é inserido em uma instância de publicação e não fica visível no ambiente do autor, resultando em todas as tarefas de moderação que precisam usar a instância de publicação.