---
title: AEM Mobile SetUp
seo-title: AEM Mobile SetUp
description: Siga esta página para configurar o AEM Mobile e, assim, permitir que o usuário crie e gerencie o conteúdo no AEM. Esta página fornece informações sobre a integração da instância do AEM com a conta e o(s) projeto(s) do AEM Mobile On-demand Services com base em nuvem.
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 2%

---

# AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Os clientes existentes de aplicativos AEM Mobile que migram do AEM 6.2 ou 6.3 para o AEM 6.5 podem continuar usando os aplicativos AEM Mobile baixando um [pacote do PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). No entanto, novas instalações do AEM 6.5 não serão compatíveis com a funcionalidade Aplicativos AEM Mobile.

Para usar o AEM para produzir conteúdo para aplicativos AEM Mobile, é necessário integrar a instância do AEM com a conta do AEM Mobile On-demand Services baseada em nuvem e o(s) projeto(s).

Siga estas etapas para configurar o AEM Mobile e, assim, permitir que o usuário crie e gerencie o conteúdo no AEM.

## Provisionamento do AEM Mobile {#aem-mobile-provisioning}

Para começar a usar a configuração do AEM Mobile, é necessário:

* **Solicitar uma chave de API**: Para acessar a API de serviços sob demanda, é necessário solicitar uma chave de API. Para solicitar a chave de API, complete o [forma PDF](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html). Envie o formulário preenchido para o Suporte da Adobe Developer: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Gerar a ID do dispositivo e o token do dispositivo**: Após receber sua chave de API, você pode gerar a ID do dispositivo e o token do dispositivo. Ir para [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) e faça o seguinte:

   * Forneça a chave da API
   * Faça logon com uma Adobe ID adicionada a um projeto do AEM Mobile com as seguintes permissões (consulte as etapas abaixo para criar um projeto)

      * Administração > Gerenciar projetos e usuários
      * Conteúdo > Adicionar e editar conteúdo, excluir conteúdo, exibir conteúdo, publicar conteúdo

Se todas as condições forem atendidas, uma ID de dispositivo e um token de dispositivo serão gerados.

>[!NOTE]
>
>O Adobe ID necessário deve receber acesso em um projeto do AEM Mobile. Consulte [Administração de conta do AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) em Ajuda online.

## Criação de projetos para AEM Mobile {#creating-projects-for-aem-mobile}

Ao criar um projeto, você especifica as configurações para qualquer plataforma que esteja direcionando: Visualizador da Web para iOS, Android, Windows e Desktop. Muitas das configurações de projeto especificadas afetam o comportamento do aplicativo.

A criação de um projeto requer o logon no portal de serviços sob demanda usando uma Adobe ID que tenha uma função de administrador Principal. A edição de um projeto requer uma função de administrador Principal ou uma função de usuário com uma **Gerenciar projetos e usuários** permissão.

>[!NOTE]
>
>Para saber mais sobre como Criar projetos na AEM Mobile, clique em [here](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuração de um conector do AEM Mobile {#configuring-an-aem-mobile-connector}

AEM configuração envolve as seguintes etapas para a configuração do conector. Quando a configuração do conector do AEM Mobile for concluída, o usuário poderá configurar grupos de usuários e permissões.

O conector AEM Mobile On-Demand é usado para vincular conteúdo gerenciado pela AEM Mobile aos serviços sob demanda da Adobe Experience Manager Mobile. Isso permite que os autores de conteúdo criem e gerenciem material para aplicativos móveis usando as ferramentas da AEM, ao mesmo tempo em que usam os serviços sob demanda da AEM Mobile para fácil distribuição de conteúdo móvel.

>[!NOTE]
>
>Esta é uma etapa única para configurar a instância do AEM.

### Configuração do cliente AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Você deve concluir as etapas de configuração para que as integrações do AEM Mobile funcionem corretamente.

1. Ir para a configuração do serviço OSGI

   1. AEM > Ferramentas > Operações > Console da Web
   1. Rolar ou pesquisar por ***Cliente de Serviços On-demand Experience Manager Mobile (era Adobe Digital Publishing Solution Client)***

1. Editar ***Cliente de Serviços On-Demand Experience Manager Mobile***

   1. **(Obrigatório)** Insira os campos obrigatórios:

      1. ID do cliente.
      1. Client Secret.
   1. **(Opcional)** Edite os valores existentes.


1. Salve as alterações.
1. Veja um exemplo de configuração:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuração do AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Ir para Cloud Services

   1. AEM > Ferramentas > Implantação > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Rolar ou pesquisar por ***Serviços sob demanda da Adobe Experience Manager Mobile***

1. Selecionar ***Configurar agora*** ou ***Mostrar configurações*** e selecione o ícone adicionar nova configuração

1. Criar uma nova configuração

   1. Inserir um Título e um Nome
   1. Inserir ID do dispositivo
   1. Inserir Token de Dispositivo
   1. Selecionar ***Testar configuração do dispositivo*** para validar os valores inseridos
   1. Selecione Ok

## Adicionar funções de usuário do AEM Mobile e atribuir permissões {#adding-aem-mobile-user-roles-and-assigning-permissions}

Depois de criar um projeto, você deve criar funções e conceder acesso aos usuários. Somente Administradores Principais podem criar e editar funções. Ao criar uma função, você ativa recursos (ou permissões) para qualquer usuário que receba essas permissões. Por exemplo, você pode criar uma função que inclui permissões para criação de aplicativos e outra função que inclui permissões para criação e publicação de conteúdo.

No desenvolvimento de aplicativos AEM Mobile, existem três funções diferentes:

* Administrador
* Desenvolvedor
* Autor

Para obter mais informações sobre como criar funções com permissões diferentes, como para criação de aplicativos ou para criação e publicação de conteúdo, clique em [Criando Funções de Usuário e Concedendo Acesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) na Ajuda do AEM Mobile.

>[!NOTE]
>
>O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores. Os autores manipulam páginas, que por sua vez se baseiam em modelos e componentes gerados por desenvolvedores de aplicativos. Por fim, os administradores publicam estrategicamente o conteúdo atualizado do aplicativo. Configurar AEM grupos e permissões define suas funções no Painel do aplicativo ou no Centro de controle.
>
>Para obter mais informações sobre o AEM Mobile Dashboard, clique em [here](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Quando terminar de criar funções com permissões diferentes, como para criação de aplicativos ou para criação e publicação de conteúdo, consulte [**Configurar seus usuários e grupos de usuários**](/help/mobile/aem-mobile-configure-users.md) para configurar usuários e grupos para suportar a criação e o gerenciamento de seus aplicativos móveis.

### Recursos adicionais {#additional-resources}

Para entender mais sobre as outras duas funções e responsabilidades para criar um aplicativo AEM Mobile On-demand Services, consulte os seguintes recursos:

* [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Criação de conteúdo AEM para aplicativo AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Para visualizar o conteúdo do aplicativo, incluindo páginas de navegação e artigos, consulte [Visualização com comprovação](/help/mobile/aem-mobile-manage-ondemand-services.md).
