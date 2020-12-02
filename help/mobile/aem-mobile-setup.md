---
title: AEM Mobile SetUp
seo-title: AEM Mobile SetUp
description: Siga esta página para configurar o AEM Mobile e permitir que o usuário crie e gerencie o conteúdo no AEM. Esta página fornece informações sobre a integração da instância de AEM com a conta e os projetos AEM Mobile On-demand Services baseados em nuvem.
seo-description: Siga esta página para configurar o AEM Mobile e permitir que o usuário crie e gerencie o conteúdo no AEM. Esta página fornece informações sobre a integração da instância de AEM com a conta e os projetos AEM Mobile On-demand Services baseados em nuvem.
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 1%

---


# AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Os clientes existentes de aplicativos AEM Mobile que migram do AEM 6.2 ou 6.3 para o AEM 6.5 podem continuar usando os aplicativos AEM Mobile baixando um pacote [do PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Entretanto, novas instalações do AEM 6.5 não oferecerão suporte à funcionalidade Aplicativos AEM Mobile.

Para usar o AEM para produzir conteúdo para aplicativos AEM Mobile, é necessário integrar a instância do AEM com a conta e o projeto do AEM Mobile On-demand Services baseados em nuvem.

Siga estas etapas para configurar o AEM Mobile e permitir que o usuário crie e gerencie o conteúdo no AEM.

## AEM Mobile Provisioning {#aem-mobile-provisioning}

Para começar a usar a configuração da AEM Mobile, é necessário:

* **Solicite uma chave** de API: Para acessar a On-Demand Services API, é necessário solicitar uma chave da API. Para solicitar a chave da API, preencha o [formulário PDF](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html). Envie o formulário preenchido para o Suporte ao desenvolvedor do Adobe: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Gerar a ID do dispositivo e o token** do dispositivo: Depois de receber sua chave da API, você pode gerar a ID do dispositivo e o token do dispositivo. Vá para [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) e faça o seguinte:

   * Forneça a chave da API
   * Faça logon com um Adobe ID que você adicionou a um projeto da AEM Mobile com as seguintes permissões (consulte as etapas abaixo para criar um projeto)

      * Administração > Gerenciar projetos e usuários
      * Conteúdo > Adicionar e editar conteúdo, Excluir conteúdo, Visualização conteúdo, Publicar conteúdo

Se todas as condições forem atendidas, uma ID do dispositivo e um token do dispositivo serão gerados.

>[!NOTE]
>
>A Adobe ID necessária deve receber acesso em um AEM Mobile Project. Consulte [Administração de contas para AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) na Ajuda online.

## Criação de projetos para AEM Mobile {#creating-projects-for-aem-mobile}

Ao criar um projeto, você especifica as configurações para qualquer plataforma que estiver definindo como meta: Visualizador da Web para iOS, Android, Windows e desktop. Muitas das configurações de projeto especificadas afetam o comportamento do aplicativo.

A criação de um projeto requer o logon no portal de serviços sob demanda usando um Adobe ID com uma função de administrador Principal. A edição de um projeto requer uma função de administrador Principal ou uma função de usuário com uma permissão **Gerenciar projetos e usuários**.

>[!NOTE]
>
>Para saber mais sobre Criar projetos no AEM Mobile, clique [aqui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configurando um AEM Mobile Connector {#configuring-an-aem-mobile-connector}

AEM configuração envolve as seguintes etapas para a configuração do conector. Quando a configuração do conector AEM Mobile estiver concluída, o usuário poderá configurar grupos de usuários e permissões.

O conector AEM Mobile On-Demand é usado para vincular conteúdo gerenciado pela AEM Mobile aos serviços sob demanda da Adobe Experience Manager Mobile. Isso permite que os autores de conteúdo criem e gerenciem material para aplicativos móveis usando as ferramentas da AEM enquanto usam os serviços sob demanda da AEM Mobile para fácil distribuição de conteúdo móvel.

>[!NOTE]
>
>Esta é uma etapa única para configurar a instância AEM.

### Configurando o AEM Mobile On-demand Services Client {#configuring-aem-mobile-on-demand-services-client}

É necessário concluir as etapas de configuração para que as integrações AEM Mobile funcionem corretamente.

1. Ir para a configuração do serviço OSGI

   1. AEM > Ferramentas > Operações > Console da Web
   1. Role ou procure ***Experience Manager Mobile On-demand Services Client (era Adobe Digital Publishing Solution Client)***

1. Editar ***Experience Manager Mobile On-demand Services Client***

   1. **(Obrigatório)** Digite os campos obrigatórios:

      1. ID do cliente.
      1. Client Secret.
   1. **(Opcional)** Edite valores existentes.


1. Salve as alterações.
1. Veja um exemplo de configuração:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuração do AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Ir para Cloud Services

   1. AEM > Ferramentas > Implantação> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Role ou pesquise por ***Adobe Experience Manager Mobile On-demand Services***

1. Selecione ***Configurar agora*** ou ***Mostrar configurações*** e selecione o ícone adicionar nova configuração

1. Criar uma nova configuração

   1. Insira um Título e Nome
   1. Inserir ID do dispositivo
   1. Digite o token do dispositivo
   1. Selecione ***Testar Configuração do Dispositivo*** para validar os valores inseridos
   1. Selecione Ok

## Adicionar funções de usuário do AEM Mobile e atribuir permissões {#adding-aem-mobile-user-roles-and-assigning-permissions}

Depois de criar um projeto, você deve criar funções e conceder acesso aos usuários. Somente administradores Principais podem criar e editar funções. Ao criar uma função, você ativa recursos (ou permissões) para qualquer usuário ao qual essas permissões são atribuídas. Por exemplo, você pode criar uma função que inclua permissões para criação de aplicativos e outra função que inclua permissões para criação e publicação de conteúdo.

No desenvolvimento de aplicativos AEM Mobile, existem três funções diferentes:

* Administrador
* Desenvolvedor
* Autor

Para obter mais informações sobre a criação de funções com permissões diferentes, como para criação de aplicativos ou para criação e publicação de conteúdo, clique em [Criação de funções de usuário e concessão de acesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) na Ajuda do AEM Mobile.

>[!NOTE]
>
>O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores. Os autores manipulam páginas, que por sua vez são baseadas em modelos e componentes gerados pelos desenvolvedores do aplicativo. Por fim, os administradores publicam estrategicamente o conteúdo atualizado do aplicativo. A configuração AEM Grupos e Permissões define suas funções no Painel do aplicativo ou no Centro de controle.
>
>Para obter mais informações sobre o Painel AEM Mobile, clique [aqui](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Quando terminar de criar funções com permissões diferentes, como para criar aplicativos ou para criar e publicar conteúdo, consulte [**Configurar seus grupos de usuários e usuários**](/help/mobile/aem-mobile-configure-users.md) para configurar seus usuários e grupos para suportar a criação e o gerenciamento de seus aplicativos móveis.

### Recursos adicionais {#additional-resources}

Para saber mais sobre as outras duas funções e responsabilidades para criar um aplicativo AEM Mobile On-demand Services, consulte os seguintes recursos:

* [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Criação AEM conteúdo para aplicativos AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Para pré-visualização do conteúdo do aplicativo, incluindo páginas de navegação e artigos, consulte [Visualizar com o Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md).
