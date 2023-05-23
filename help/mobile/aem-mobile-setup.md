---
title: Configuração do AEM Mobile
seo-title: AEM Mobile SetUp
description: Siga esta página para configurar o AEM Mobile e, assim, permitir que o usuário crie e gerencie o conteúdo no AEM. Esta página fornece informações sobre a integração da instância do AEM com a conta e o(s) projeto(s) do AEM Mobile On-demand Services baseados em nuvem.
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---

# Configuração do AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Os clientes existentes do AEM Mobile Apps que migram do AEM 6.2 ou 6.3 para o AEM 6.5 podem continuar a usar os aplicativos do AEM Mobile baixando um pacote do PackageShare. No entanto, as novas instalações do AEM 6.5 não serão compatíveis com a funcionalidade de aplicativos do AEM Mobile.

Para usar o AEM para produzir conteúdo para aplicativos do AEM Mobile, é necessário integrar a instância do AEM à conta e aos projetos do AEM Mobile On-demand Services com base em nuvem.

Siga estas etapas para configurar o AEM Mobile e, assim, permitir que o usuário crie e gerencie o conteúdo no AEM.

## Provisionamento do AEM Mobile {#aem-mobile-provisioning}

Para começar a usar o AEM Mobile, é necessário:

* **Solicitar uma chave de API**: para acessar a API de serviços por demanda, é necessário solicitar uma chave de API. Para solicitar a chave de API, preencha o [formulário PDF](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Envie o formulário preenchido para o Suporte da Adobe Developer: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Gerar a ID do dispositivo e o token do dispositivo**: depois de receber a chave de API, você pode gerar a ID do dispositivo e o token do dispositivo. Ir para `https://aex.aemmobile.adobe.com` e faça o seguinte:

   * Forneça a chave de API
   * Faça logon com uma Adobe ID adicionada a um projeto do AEM Mobile com as seguintes permissões (consulte as etapas abaixo para criar um projeto)

      * Administração > Gerenciar projetos e usuários
      * Conteúdo > Adicionar e editar conteúdo, Excluir conteúdo, Exibir conteúdo, Publicar conteúdo

Se todas as condições forem atendidas, uma ID do dispositivo e um Token do dispositivo serão gerados.

>[!NOTE]
>
>O Adobe ID necessário deve receber acesso em um projeto do AEM Mobile. Consulte [Administração de contas para o AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) na Ajuda online.

## Criação de projetos para o AEM Mobile {#creating-projects-for-aem-mobile}

Ao criar um projeto, especifique as configurações para qualquer plataforma de destino: iOS, Android, Windows e Desktop Web Viewer. Muitas das configurações de projeto especificadas afetam o comportamento do aplicativo.

A criação de um projeto requer que você faça logon no portal de serviços por demanda usando uma Adobe ID com função de administrador Principal. A edição de um projeto requer uma função de Administrador Principal ou uma função de usuário com uma **Gerenciar projetos e usuários** permissão.

>[!NOTE]
>
>Para saber mais sobre como Criar projetos no AEM Mobile, clique em [aqui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuração de um conector do AEM Mobile {#configuring-an-aem-mobile-connector}

A configuração do AEM envolve as seguintes etapas para a configuração do conector. Quando a configuração do conector do AEM Mobile estiver concluída, o usuário poderá configurar grupos de usuários e permissões.

O conector AEM Mobile On-Demand é usado para vincular o conteúdo gerenciado do AEM Mobile com os serviços On-Demand da Adobe Experience Manager Mobile. Isso permite que os autores de conteúdo criem e gerenciem material para aplicativos móveis usando ferramentas AEM e, ao mesmo tempo, usando os serviços on-demand da AEM Mobile para fácil distribuição de conteúdo móvel.

>[!NOTE]
>
>Essa é uma etapa única para configurar a instância do AEM.

### Configuração do cliente AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Você deve concluir as etapas de configuração para que as integrações do AEM Mobile funcionem corretamente.

1. Ir para a configuração do serviço OSGI

   1. AEM > Ferramentas > Operações > Console da Web
   1. Rolar ou pesquisar ***Cliente Experience Manager Mobile On-demand Services (era o Adobe Digital Publishing Solution Client)***

1. Editar ***Cliente de serviços por demanda do Experience Manager Mobile***

   1. **(Obrigatório)** Insira os campos obrigatórios:

      1. ID do cliente.
      1. Client Secret.
   1. **(Opcional)** Editar valores existentes.


1. Salve as alterações.
1. Este é um exemplo de configuração:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuração do AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Ir para Cloud Services

   1. AEM > Ferramentas > Implantação> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Rolar ou pesquisar ***Adobe Experience Manager Mobile On-demand Services***

1. Selecionar ***Configurar agora*** ou ***Exibir configurações*** e selecione o ícone adicionar nova configuração

1. Criar uma nova configuração

   1. Insira um Título e Nome
   1. Inserir ID do dispositivo
   1. Inserir token do dispositivo
   1. Selecionar ***Testar configuração do dispositivo*** para validar valores inseridos
   1. Selecionar Ok

## Adicionar funções de usuário do AEM Mobile e atribuir permissões {#adding-aem-mobile-user-roles-and-assigning-permissions}

Depois de criar um projeto, você deve criar funções e conceder acesso aos usuários. Somente administradores Principais podem criar e editar funções. Ao criar uma função, você habilita recursos (ou permissões) para os usuários aos quais essas permissões forem atribuídas. Por exemplo, você pode criar uma função que inclua permissões para a criação de aplicativos e outra que inclua permissões para criação e publicação de conteúdo.

No desenvolvimento de aplicativos do AEM Mobile, existem três funções diferentes:

* Administrador
* Desenvolvedor
* Autor

Para obter mais informações sobre como criar funções com permissões diferentes, como para a criação de aplicativos ou para criar e publicar conteúdo, clique em [Criando Atribuições de Usuário e Concedendo Acesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) na Ajuda do AEM Mobile.

>[!NOTE]
>
>O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores. Os autores manipulam páginas, que por sua vez são baseadas em modelos e componentes gerados por desenvolvedores de aplicativos. Por fim, os administradores publicam estrategicamente o conteúdo atualizado do aplicativo. A configuração de grupos e permissões de AEM define suas funções no Painel de controle do aplicativo ou no Centro de controle.
>
>Para obter mais informações sobre o AEM Mobile Dashboard, clique em [aqui](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Quando terminar de criar funções com permissões diferentes, como para criação de aplicativos ou para criação e publicação de conteúdo, consulte [**Configurar usuários e grupos de usuários**](/help/mobile/aem-mobile-configure-users.md) para configurar usuários e grupos para oferecer suporte à criação e ao gerenciamento de aplicativos móveis.

### Recursos adicionais {#additional-resources}

Para entender mais sobre as outras duas funções e responsabilidades para criar um aplicativo AEM Mobile On-demand Services, consulte os seguintes recursos:

* [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Criação de conteúdo AEM para aplicativo AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Para visualizar o conteúdo do aplicativo, incluindo navegar pelas páginas e artigos, consulte [Visualização com simulação](/help/mobile/aem-mobile-manage-ondemand-services.md).
