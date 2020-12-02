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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# Configuração inicial {#initial-setup}

## Instâncias de autor e publicação do start {#start-author-and-publish-instances}

Para fins de desenvolvimento e demonstração, será necessário executar um autor e uma instância de publicação.

Para fazer isso, siga as instruções AEM básicas [Introdução](../../help/sites-deploying/deploy.md#getting-started), que resultarão em:

* Ambiente do autor em [localhost:4502](http://localhost:4502/)
* Publicar ambiente em [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* O ambiente do autor é para:

   * Desenvolvimento de sites, modelos e componentes.
   * Tarefas administrativas e de configuração.

* O ambiente publish é para:

   * A experiência da comunidade de publicar e moderar conteúdo.
   * Criação de grupos de comunidade, membros e grupos de membros.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, visualização a documentação em [manuseio básico](../../help/sites-authoring/basic-handling.md) e um [guia rápido para criar páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalar a versão mais recente das comunidades {#install-latest-communities-release}

Este tutorial cria um [site da comunidade de envolvimento](overview.md#engagement-community) e é baseado no pacote de recursos AEM Communities 6.2 versão 1.10.

Para verificar se o pacote de recursos mais recente está instalado, visite:

* [Versões mais recentes](deploy-communities.md#latest-releases)

Para obter um tutorial que cria um [site da comunidade de ativação](overview.md#enablement-community), visite [Introdução ao AEM Communities para Ativação](getting-started-enablement.md).

## Configurar Analytics {#configure-analytics}

Quando [o Adobe Analytics está configurado para o site da comunidade](analytics.md), estão disponíveis informações sobre a atividade da comunidade que melhoram a experiência do membro da comunidade, bem como fornecem feedback aos administradores do site.

A integração com o Adobe Analytics é opcional.

## Configurar email para notificações {#configure-email-for-notifications}

O recurso de notificações, disponível por padrão para todos os sites criados usando o console `Communities Sites`, fornece um canal de email para notificações.

O que é necessário é que o email seja configurado corretamente para o site.

Consulte [Configuração de Email](email.md).

## Ative o serviço de túnel {#enable-the-tunnel-service}

Ao criar um site da comunidade no ambiente do autor, o serviço de túnel possibilita a atribuição de funções a membros da comunidade confiáveis registrados no ambiente de publicação. O serviço de túnel também permite acesso aos membros da comunidade dos [consoles de membros e grupos](members.md) no ambiente do autor.

A convenção é para membros e grupos de membros criados no ambiente publish para *not* serem recriados no ambiente do autor. Para obter mais informações, consulte [Gerenciamento de usuários e grupos de usuários](users.md).

Para obter instruções simples para habilitar o serviço de túnel em uma instância **author**, consulte [Serviço de Túnel](deploy-communities.md#tunnel-service-on-author).

## Função de administrador da comunidade {#community-administrator-role}

Os membros do grupo Administradores da comunidade podem criar sites da comunidade, gerenciar sites, gerenciar membros (eles podem proibir membros da comunidade) e moderar conteúdo.

### Criar usuário {#create-user}

Crie um usuário em *author*, que tenha a função de Administrador da comunidade:

* Na instância do autor

   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)

* Fazer logon com privilégios de administrador

   * Por exemplo, nome de usuário &#39;admin&#39; / senha &#39;admin&#39;

* No console principal, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Segurança]** > **[!UICONTROL Utilizadores]**.
* No menu **Editar**, selecione **[!UICONTROL Adicionar Utilizador]**

* Na caixa de diálogo `Create New User`, digite:

   * **[!UICONTROL ID]**: sírio
   * **[!UICONTROL Endereço]** Emai: sirius.nilson@mailinator.com
   * **[!UICONTROL Senha]**: password
   * **[!UICONTROL Confirmar &amp;senha;]**: password
   * **[!UICONTROL Nome]**: Sirius
   * **[!UICONTROL Sobrenome]**: Nilson

### Atribuir Sirius ao grupo de administradores da comunidade {#assign-sirius-to-community-administrators-group}

Role para baixo até `Add User to Groups`:

* Digite &#39;C&#39; para pesquisar

   * Selecionar `Community Administrators`
   * Selecionar `Community Enablement Managers`

* Selecione **[!UICONTROL Salvar]**.

![create-user](assets/create-user.png)

## Habilitar logon social {#enable-social-login}

Antes que as versões de demonstração de login social com Facebook e Twitter possam ser usadas, é necessário

1. Instale um pacote de correções ou [pacote de recursos mais recente](deploy-communities.md#latestfeaturepack) (para alterações de março de 2017 na API do Facebook).
1. [Ative o provedor OAuth ](social-login.md#adobe-granite-oauth-authentication-handler) no ambiente publish.

Para servidores de produção, é necessário criar os serviços em nuvem necessários para fornecer o logon social.

Consulte [Logon social com Facebook e Twitter](social-login.md).

## Criar tags do tutorial {#create-tutorial-tags}

Crie tags para usar nos tutoriais de envolvimento e ativação, usando a namespace de tag `Tutorial`.

Use o [console de marcação](../../help/sites-administering/tags.md#tagging-console) para criar as seguintes tags:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tags tutoriais](assets/tutorial-tags.png)

Em seguida, siga as instruções para:

1. [Defina as permissões](../../help/sites-administering/tags.md#setting-tag-permissions) da tag.
1. [Publique as tags](../../help/sites-administering/tags.md#publishing-tags).

Pacote de amostra de tags criadas para os Tutorials de Introdução do AEM Communities

[Obter arquivo](assets/tutorial_tags-v63.zip)

## MongoDB para UGC Common Store {#mongodb-for-ugc-common-store}

É recomendável, mas opcional, definir [MSRP](msrp.md) (MongoDB) como o [armazenamento comum](working-with-srp.md) para experimentar a flexibilidade de moderar todo o UGC dos ambientes de publicação e/ou autor.

Para obter instruções, consulte [Como configurar MongoDB para Demo](demo-mongo.md).

Por padrão, a instalação das instâncias do autor e publicação AEM resulta no conteúdo gerado pelo usuário (UGC) sendo armazenado em [armazenamento Tar JCR](../../help/sites-deploying/platform.md) que é acessado usando [JSRP](jsrp.md). O JSRP não é uma loja comum, o que significa que o UGC está visível somente na instância em que foi inserido. Normalmente, o UGC é inserido em uma instância de publicação e não fica visível no ambiente do autor, resultando em todas as tarefas de moderação que precisam usar a instância de publicação.