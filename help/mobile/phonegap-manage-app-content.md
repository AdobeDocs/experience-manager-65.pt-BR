---
title: Criação e gerenciamento de conteúdo do aplicativo
description: O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores. Os autores manipulam páginas, que são baseadas em modelos e componentes gerados por desenvolvedores de aplicativos.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Criação e gerenciamento de conteúdo do aplicativo{#creating-and-managing-app-content}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de [desenvolvedores](#developer), [autores](#author) de conteúdo e [administradores](#administrator). Os autores manipulam páginas, que são baseadas em modelos e componentes gerados por desenvolvedores de aplicativos.

Por fim, os administradores publicam estrategicamente o conteúdo atualizado do aplicativo.

>[!NOTE]
>
>**Pré-requisito**:
>
>Em [Implantação e manutenção](/help/sites-deploying/deploy.md), os desenvolvedores se familiarizaram com os componentes e modelos do sistema no Adobe Experience Manager (AEM).

## O mosaico Gerenciar conteúdo da página {#the-manage-page-content-tile}

>[!CAUTION]
>
>Se você não estiver usando um modelo de aplicativo pronto para uso, é necessário configurar um Manipulador de sincronização de conteúdo para permitir que o novo conteúdo do aplicativo seja publicado no OTA.
>
>Consulte [Mobile com sincronização de conteúdo](/help/mobile/phonegap-contentsync.md) na seção para desenvolvedores, para obter mais detalhes.

Aqui, o conteúdo pode ser criado, editado e excluído no AEM Mobile da mesma maneira que você faria no AEM Sites.

O **bloco Gerenciar Conteúdo da Página** exibe o número de páginas de conteúdo gerenciado e modificado pela última vez para uma carga específica. Você pode detalhar o conteúdo para criar, copiar, mover, excluir e atualizar páginas clicando em cada registro no bloco.

Depois que o conteúdo for atualizado, os administradores poderão publicar uma OTA (carga de atualização de conteúdo) para os clientes por meio do **bloco Gerenciar pacotes de conteúdo.**

![chlimage_1-161](assets/chlimage_1-161.png)

Selecione um dos pacotes de conteúdo listados para criar ou editar conteúdo, como criar, editar ou remover páginas, alterar a navegação e a ordem das páginas, criar ou atualizar conteúdo, como copiar (texto) e mídia.

Observe que *tudo é conteúdo*, o que significa que os estilos de aplicativo, cópia (texto), mídia, páginas, navegação e direcionamento de conteúdo podem ser editados e atualizados OTA, sem precisar ir para uma loja de aplicativos.

Para editar conteúdo do AEM Mobile, *autores de AEM *precisarão de uma sólida compreensão da interface de edição de conteúdo do AEM: [Criação de páginas no AEM.](/help/sites-authoring/qg-page-authoring.md)

## O Bloco Gerenciar Pacotes De Conteúdo {#the-manage-content-packages-tile}

Aqui, os *Administradores de AEM* podem atualizar seus aplicativos de forma rápida e fácil, a fim de fornecer experiências envolventes e conteúdo atualizado para impulsionar o engajamento com a marca e atender às metas comerciais, tudo sem precisar de um reenvio de desenvolvedor ou de uma loja de aplicativos.

![chlimage_1-162](assets/chlimage_1-162.png)

Depois que os *Autores de AEM* adicionarem ou modificarem conteúdo por meio do Bloco Gerenciar Conteúdo, os *Administradores de AEM* poderão enviar essas alterações para os clientes com uma atualização de Pacotes de Conteúdo.

A ação Pacote de Conteúdo permite que o *Autor de AEM* crie e edite o conteúdo da página enquanto a equipe de desenvolvimento faz alterações no design e na implementação de um Aplicativo de Host, incluindo navegação, estilo, lógica do lado do servidor, modelos e componentes. Em seguida, envia essas alterações do OTA para os clientes sem precisar reenviá-las para distribuição nas várias lojas.

**Para publicar conteúdo novo ou atualizado**

Selecione um pacote de conteúdo no bloco, neste exemplo, o pacote em inglês. Observe que uma caixa de diálogo de atualização de conteúdo lista a configuração relevante do *Content Sync*. Se o conteúdo do aplicativo tiver sido modificado desde uma atualização anterior, o status exibirá *Pendente*, como mostrado abaixo.

![chlimage_1-163](assets/chlimage_1-163.png)

Em seguida, selecione a ação **Preparar** na parte superior direita para criar a atualização de conteúdo. Adicione as informações de atualização apropriadas e pressione Concluído.

![chlimage_1-164](assets/chlimage_1-164.png)

O manipulador *Sincronização de Conteúdo* cria os pacotes necessários formando um delta (um pacote de *somente* o que foi alterado). Depois de concluído, esse pacote de conteúdo de atualização foi preparado conforme mostrado abaixo.

A preparação de uma atualização do conteúdo permite que várias atualizações sejam feitas antes de publicá-las no OTA em dispositivos móveis.

>[!NOTE]
>
>O conteúdo dividido pode ser verificado usando o aplicativo AEM Verify antes da publicação.
>
>Consulte [Quickstart móvel para verificação de AEM](/help/mobile/phonegap-mobile-quickstart.md) para obter mais detalhes sobre o aplicativo AEM Verify.

![chlimage_1-165](assets/chlimage_1-165.png)

Quando estiver pronto para fornecer novo conteúdo aos usuários do aplicativo com o OTA de sincronização de conteúdo, selecione **Publish** conforme mostrado abaixo.

![chlimage_1-166](assets/chlimage_1-166.png)

### Próximas etapas {#the-next-steps}

Depois de aprender sobre como Criar e gerenciar conteúdo do aplicativo no painel do aplicativo, consulte os seguintes recursos para outras funções de criação:

* [O mosaico Gerenciar aplicativo](/help/mobile/phonegap-app-details-tile.md)
* [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md)
* [Definições do aplicativo](/help/mobile/phonegap-app-definitions.md)
* [Criação de um novo aplicativo usando o Assistente para criação de aplicativo](/help/mobile/phonegap-create-new-app.md)
* [Importar um aplicativo híbrido existente](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento do Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
