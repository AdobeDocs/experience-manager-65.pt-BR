---
title: Configuração do AEM Mobile
seo-title: Configuração do AEM Mobile
description: Siga esta página para configurar o AEM Mobile e permitir que o usuário crie e gerencie o conteúdo no AEM. Esta página fornece informações sobre a integração da instância do AEM com a conta e os projetos do AEM Mobile On-Demand Services baseados em nuvem.
seo-description: Siga esta página para configurar o AEM Mobile e permitir que o usuário crie e gerencie o conteúdo no AEM. Esta página fornece informações sobre a integração da instância do AEM com a conta e os projetos do AEM Mobile On-Demand Services baseados em nuvem.
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuração do AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Os clientes existentes de aplicativos do AEM Mobile que migram do AEM 6.2 ou 6.3 para o AEM 6.5 podem continuar usando os aplicativos do AEM Mobile baixando um [pacote do PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Entretanto, novas instalações do AEM 6.5 não oferecerão suporte à funcionalidade de aplicativos do AEM Mobile.

Para usar o AEM para produzir conteúdo para aplicativos do AEM Mobile, é necessário integrar a instância do AEM à conta e aos projetos do AEM Mobile On-Demand Services baseados em nuvem.

Siga estas etapas para configurar o AEM Mobile e, assim, permitir que o usuário crie e gerencie o conteúdo no AEM.

## AEM Mobile Provisioning {#aem-mobile-provisioning}

Para começar a usar a configuração do AEM Mobile, é necessário:

* **Solicite uma chave** de API: Para acessar a On-Demand Services API, é necessário solicitar uma chave da API. Para solicitar a chave da API, preencha o formulário [](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html)PDF. Envie o formulário preenchido ao suporte do Adobe Developer: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Gerar a ID do dispositivo e o token** do dispositivo: Depois de receber sua chave da API, você pode gerar a ID do dispositivo e o token do dispositivo. Vá para [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) e faça o seguinte:

   * Forneça a chave da API
   * Faça logon com uma Adobe ID que você adicionou a um projeto do AEM Mobile com as seguintes permissões (consulte as etapas abaixo para criar um projeto)

      * Administração > Gerenciar projetos e usuários
      * Conteúdo > Adicionar e editar conteúdo, excluir conteúdo, exibir conteúdo, publicar conteúdo

Se todas as condições forem atendidas, uma ID do dispositivo e um token do dispositivo serão gerados.

>[!NOTE]
>
>A ID da Adobe necessária deve receber acesso em um projeto do AEM Mobile. Consulte Administração de [contas para o AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) na Ajuda online.

## Criar projetos para o AEM Mobile {#creating-projects-for-aem-mobile}

Ao criar um projeto, você especifica as configurações para qualquer plataforma que estiver visando: Visualizador da Web para iOS, Android, Windows e desktop. Muitas das configurações de projeto especificadas afetam o comportamento do aplicativo.

A criação de um projeto requer o logon no portal de serviços sob demanda usando uma Adobe ID que tenha uma função de administrador mestre. A edição de um projeto requer uma função de administrador mestre ou uma função de usuário com uma permissão **Gerenciar projetos e usuários** .

>[!NOTE]
>
>Para saber mais sobre Criar projetos no AEM Mobile, clique [aqui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configurar um conector do AEM Mobile {#configuring-an-aem-mobile-connector}

A configuração do AEM envolve as seguintes etapas para a configuração do conector. Quando a configuração do conector do AEM Mobile estiver concluída, o usuário poderá configurar grupos de usuários e permissões.

O conector sob demanda do AEM Mobile é usado para vincular conteúdo gerenciado do AEM Mobile aos serviços sob demanda do Adobe Experience Manager Mobile. Isso permite que os autores de conteúdo criem e gerenciem material para aplicativos móveis usando as ferramentas do AEM enquanto usam os serviços sob demanda do AEM Mobile para fácil distribuição de conteúdo móvel.

>[!NOTE]
>
>Esta é uma etapa única para configurar a instância do AEM.

### Configuração do cliente de serviços sob demanda do AEM Mobile {#configuring-aem-mobile-on-demand-services-client}

Você deve concluir as etapas de configuração para que as integrações do AEM Mobile funcionem corretamente.

1. Ir para a configuração do serviço OSGI

   1. AEM > Ferramentas > Operações > Console da Web
   1. Role ou pesquise pelo ***Experience Manager Mobile On-demand Services Client (era o Adobe Digital Publishing Solution Client)***

1. Editar cliente de serviços sob demanda do ***Experience Manager Mobile***

   1. **(Obrigatório)** Digite os campos obrigatórios:

      1. ID do cliente.
      1. Client Secret.
   1. **(Opcional)** Edite os valores existentes.


1. Salve as alterações.
1. Veja um exemplo de configuração:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuração do AEM Mobile On-Demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Ir para serviços em nuvem

   1. AEM > Ferramentas > Implantação > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Role ou pesquise os serviços sob demanda do ***Adobe Experience Manager Mobile***

1. Selecione ***Configurar agora*** ou ***Mostrar configurações*** e selecione o ícone adicionar nova configuração

1. Criar uma nova configuração

   1. Insira um Título e Nome
   1. Inserir ID do dispositivo
   1. Digite o token do dispositivo
   1. Selecione ***Testar configuração*** do dispositivo para validar os valores inseridos
   1. Selecione Ok

## Adicionar funções de usuário do AEM Mobile e atribuir permissões {#adding-aem-mobile-user-roles-and-assigning-permissions}

Depois de criar um projeto, você deve criar funções e conceder acesso aos usuários. Somente administradores mestre podem criar e editar funções. Ao criar uma função, você ativa recursos (ou permissões) para qualquer usuário ao qual essas permissões são atribuídas. Por exemplo, você pode criar uma função que inclua permissões para criação de aplicativos e outra função que inclua permissões para criação e publicação de conteúdo.

No desenvolvimento de aplicativos do AEM Mobile, existem três funções diferentes:

* Administrador
* Desenvolvedor
* Autor

Para obter mais informações sobre como criar funções com permissões diferentes, como para criar aplicativos ou para criar e publicar conteúdo, clique em [Criar funções de usuário e conceder acesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) na Ajuda do AEM Mobile.

>[!NOTE]
>
>O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores. Os autores manipulam páginas, que por sua vez são baseadas em modelos e componentes gerados pelos desenvolvedores do aplicativo. Finalmente, os administradores publicam estrategicamente o conteúdo atualizado do aplicativo. A configuração de grupos e permissões do AEM define suas funções no Painel do aplicativo ou Centro de controle.
>
>Para obter mais informações sobre o AEM Mobile Dashboard, clique [aqui](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Quando terminar de criar funções com permissões diferentes, como para criar aplicativos ou para criar e publicar conteúdo, consulte [**Configurar grupos **](/help/mobile/aem-mobile-configure-users.md)de usuários e usuários para configurar usuários e grupos que suportem a criação e o gerenciamento de seus aplicativos móveis.

### Additional Resources {#additional-resources}

Para saber mais sobre as outras duas funções e responsabilidades para criar um aplicativo de serviços sob demanda do AEM Mobile, consulte os seguintes recursos:

* [Desenvolver conteúdo do AEM para serviços sob demanda do AEM Mobile](/help/mobile/aem-mobile-on-demand.md)
* [Criação de conteúdo do AEM para o aplicativo de serviços sob demanda do AEM Mobile](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Para visualizar o conteúdo do aplicativo, incluindo páginas de navegação e artigos, consulte [Visualização com comprovação](/help/mobile/aem-mobile-manage-ondemand-services.md).
