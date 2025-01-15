---
title: Configuração do AEM Mobile
description: Siga esta página para configurar o AEM Mobile e, assim, permitir que o usuário crie e gerencie o conteúdo no Adobe Experience Manager (AEM). Esta página fornece informações sobre a integração da instância do AEM com a conta e os projetos do AEM Mobile On-demand Services baseados em nuvem.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 1%

---

# Configuração do AEM Mobile{#aem-mobile-setup}

{{ue-over-mobile}}

>[!CAUTION]
>
>Os clientes de aplicativos móveis do Adobe Experience Manager (AEM) que estão migrando do AEM 6.2 ou 6.3 para o AEM 6.5 podem continuar a usar os aplicativos da AEM Mobile baixando um pacote do Compartilhamento de pacotes. No entanto, as novas instalações do AEM 6.5 não oferecem suporte à funcionalidade de aplicativos do AEM Mobile.

Para usar o AEM para produzir conteúdo para aplicativos do AEM Mobile, é necessário integrar a instância do AEM à conta e aos projetos do AEM Mobile On-demand Services com base em nuvem.

Siga estas etapas para configurar o AEM Mobile e, assim, permitir que o usuário crie e gerencie o conteúdo no AEM.

## Provisionamento do AEM Mobile {#aem-mobile-provisioning}

Para começar a usar o AEM Mobile, você deve:

* **Solicitar uma chave de API**: para acessar a API de serviços por demanda, solicite uma chave de API. Para solicitar a chave de API, preencha o [formulário PDF](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Envie o formulário preenchido para o Suporte da Adobe Developer: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Gerar a ID do Dispositivo e o Token do Dispositivo**: depois de receber a chave de API, você poderá gerar a ID do dispositivo e o token do dispositivo. Vá para `https://aex.aemmobile.adobe.com` e faça o seguinte:

   * Forneça a chave de API
   * Faça logon com uma Adobe ID adicionada a um projeto do AEM Mobile com as seguintes permissões (consulte as etapas abaixo para criar um projeto)

      * Administração > Gerenciar projetos e usuários
      * Conteúdo > Adicionar e editar conteúdo, Excluir conteúdo, Exibir conteúdo, Conteúdo do Publish

Se todas as condições forem atendidas, uma ID do dispositivo e um Token do dispositivo serão gerados.

>[!NOTE]
>
>O Adobe ID necessário deve receber acesso em um projeto do AEM Mobile. Consulte [Administração de Conta para o AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) na Ajuda Online.

## Criação de projetos para o AEM Mobile {#creating-projects-for-aem-mobile}

Ao criar um projeto, especifique as configurações para qualquer plataforma de destino: iOS, Android™, Windows e Desktop Web Viewer. Muitas das configurações de projeto especificadas afetam o comportamento do aplicativo.

A criação de um projeto requer que você faça logon no portal dos serviços por demanda usando uma Adobe ID que tenha a função de administrador principal. A edição de um projeto requer uma função de Administrador Mestre ou uma função de usuário com a permissão **Gerenciar Projetos e Usuários**.

>[!NOTE]
>
>Para saber mais sobre como Criar Projetos no AEM Mobile, clique [aqui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuração de um conector do AEM Mobile {#configuring-an-aem-mobile-connector}

A configuração do AEM envolve as seguintes etapas para a configuração do conector. Quando a configuração do conector do AEM Mobile estiver concluída, o usuário poderá configurar grupos de usuários e permissões.

O conector AEM Mobile On-Demand é usado para vincular o conteúdo gerenciado do AEM Mobile com os serviços On-Demand da Adobe Experience Manager Mobile. Isso permite que os autores de conteúdo criem e gerenciem material para aplicativos móveis usando ferramentas do AEM e, ao mesmo tempo, usando os serviços on-demand da AEM Mobile para fácil distribuição de conteúdo móvel.

>[!NOTE]
>
>Essa é uma etapa única para configurar a instância do AEM.

### Configuração do cliente AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Conclua as etapas de configuração para que as integrações do AEM Mobile funcionem corretamente.

1. Ir para a configuração do serviço OSGI

   1. AEM > Ferramentas > Operações > Console da Web
   1. Role ou pesquise por ***Experience Manager Mobile On-demand Services Client (era o Adobe Digital Publishing Solution Client)***

1. Editar ***Cliente do Mobile On-demand Services do Experience Manager***

   1. **(Obrigatório)** Insira os campos obrigatórios:

      1. ID do cliente.
      1. Segredo do cliente.

   1. **(Opcional)** Editar valores existentes.

1. Salve as alterações.
1. Este é um exemplo de configuração:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuração do AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Ir para Cloud Service.

   1. AEM > Ferramentas > Implantação> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Rolar ou pesquisar por ***Adobe Experience Manager Mobile On-demand Services***

1. Selecione ***Configurar agora*** ou ***Mostrar configurações*** e selecione o ícone de adição de configuração.

1. Criar uma configuração

   1. Insira um Título e Nome
   1. Inserir ID do dispositivo
   1. Inserir token do dispositivo
   1. Selecione ***Testar Configuração de Dispositivo*** para poder validar os valores inseridos
   1. Selecione OK

## Adicionar funções de usuário do AEM Mobile e atribuir permissões {#adding-aem-mobile-user-roles-and-assigning-permissions}

Depois de criar um projeto, você deve criar funções e conceder acesso aos usuários. Somente administradores mestres podem criar e editar funções. Ao criar uma função, você habilita recursos (ou permissões) para os usuários aos quais essas permissões forem atribuídas. Por exemplo, você pode criar uma função que inclua permissões para a criação de aplicativos e outra que inclua permissões para criação e publicação de conteúdo.

No desenvolvimento de aplicativos do AEM Mobile, existem três funções diferentes:

* Administrador
* Desenvolvedor
* Autor

Para obter mais informações sobre como criar funções com permissões diferentes, como para a criação de aplicativos ou para criar e publicar conteúdo, clique em [Como Criar Funções de Usuário e Conceder Acesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) na Ajuda do AEM Mobile.

>[!NOTE]
>
>O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores. Os autores manipulam páginas, que por sua vez são baseadas em modelos e componentes gerados por desenvolvedores de aplicativos. Por fim, os administradores publicam estrategicamente o conteúdo atualizado do aplicativo. A configuração de grupos e permissões de AEM define suas funções no Painel de controle do aplicativo ou no Centro de controle.
>
>Consulte [Painel do AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Quando terminar de criar funções com permissões diferentes, como para criação de aplicativos ou para criação e publicação de conteúdo, consulte [**Configurar grupos de usuários e usuários**](/help/mobile/aem-mobile-configure-users.md). Isso pode ajudar você a configurar usuários e grupos para oferecer suporte à criação e ao gerenciamento de aplicativos móveis.

### Recursos adicionais {#additional-resources}

Para entender mais sobre as outras duas funções e responsabilidades para criar um aplicativo AEM Mobile On-demand Services, consulte os seguintes recursos:

* [Desenvolvimento de conteúdo AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Criação de conteúdo AEM para aplicativo AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Para visualizar o conteúdo do aplicativo, incluindo navegar pelas páginas e artigos, consulte [Visualização com simulação](/help/mobile/aem-mobile-manage-ondemand-services.md).
