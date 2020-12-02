---
title: Criação e gerenciamento de conteúdo do aplicativo
seo-title: Criação e gerenciamento de conteúdo do aplicativo
description: O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores.  Os autores manipulam as páginas, que por sua vez são baseadas em modelos e componentes gerados pelos desenvolvedores do aplicativo.
seo-description: O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de desenvolvedores, autores de conteúdo e administradores.  Os autores manipulam as páginas, que por sua vez são baseadas em modelos e componentes gerados pelos desenvolvedores do aplicativo.
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---


# Criação e gerenciamento de conteúdo do aplicativo{#creating-and-managing-app-content}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

O gerenciamento de conteúdo do aplicativo requer um esforço coletivo de [desenvolvedores](#developer), conteúdo [autores](#author) e [administradores](#administrator). Os autores manipulam as páginas, que por sua vez são baseadas em modelos e componentes gerados pelos desenvolvedores do aplicativo.

Por fim, os administradores publicam estrategicamente o conteúdo atualizado do aplicativo.

>[!NOTE]
>
>**Pré-requisitos**:
>
>Em [Implantação e manutenção](/help/sites-deploying/deploy.md), os desenvolvedores se familiarizaram com AEM sistema de componentes e modelos.

## O mosaico Gerenciar conteúdo da página {#the-manage-page-content-tile}

>[!CAUTION]
>
>Se você não estiver usando um modelo de aplicativo predefinido, para permitir que o novo conteúdo do aplicativo seja publicado no OTA, é necessário configurar um manipulador de Sincronização de conteúdo.
>
>Consulte [Dispositivo móvel com sincronização de conteúdo](/help/mobile/phonegap-contentsync.md) na seção do desenvolvedor para obter mais detalhes.

Aqui, o conteúdo pode ser criado, editado e excluído no AEM Mobile da mesma forma que você faria no AEM Sites.

O bloco **Gerenciar conteúdo da página** exibe o número de páginas do conteúdo gerenciado e modificado pela última vez para uma carga específica. É possível detalhar o conteúdo para criar, copiar, mover, excluir e atualizar páginas clicando em cada registro no bloco.

Depois que o conteúdo for atualizado, os administradores poderão publicar uma carga de atualização de conteúdo no ar (OTA) para os clientes por meio do bloco **Gerenciar pacotes de conteúdo.**

![chlimage_1-161](assets/chlimage_1-161.png)

Selecione um dos pacotes de conteúdo listados para criar ou editar conteúdo, como criar, editar ou remover páginas, alterar a navegação e a ordem da página, criar ou atualizar conteúdo, como copiar (texto) e mídia.

Observe que *tudo é content*, ou seja, estilos de aplicativo, copiar (texto), mídia, páginas, navegação e definição de metas de conteúdo podem ser editados e atualizados no OTA, sem um percurso para uma loja de aplicativos.

Para editar o conteúdo do AEM Mobile, *os autores AEM *precisarão de uma sólida compreensão AEM interface de edição de conteúdo: [Criação de páginas em AEM.](/help/sites-authoring/qg-page-authoring.md)

## O mosaico Gerenciar pacotes de conteúdo {#the-manage-content-packages-tile}

Aqui, *AEM Administradores* podem atualizar seus aplicativos de forma rápida e fácil para fornecer experiências envolventes e conteúdo atualizado para impulsionar o envolvimento da marca e atingir os objetivos de negócios, tudo isso sem a necessidade de uma nova solicitação de desenvolvedor ou loja de aplicativos.

![chlimage_1-162](assets/chlimage_1-162.png)

Depois que *Autores do AEM* adicionarem ou modificarem conteúdo por meio do bloco Gerenciar conteúdo, *AEM Administradores* poderão encaminhar essas alterações para clientes com uma atualização de Pacotes de conteúdo.

A ação Pacote de conteúdo permite que o *Autor do AEM* crie e edite conteúdo da página enquanto a equipe de desenvolvimento altera o design e a implementação de um aplicativo host, incluindo navegação, estilo, lógica do lado do servidor, modelos e componentes, e depois envia essas alterações para os clientes sem precisar reenviar para as várias lojas para distribuição.

**Para publicar conteúdo novo ou atualizado**

Selecione um pacote de conteúdo do bloco, neste exemplo, o pacote em inglês. Observe que uma caixa de diálogo de atualização de conteúdo lista a configuração relevante *Content Sync*. Se o conteúdo do aplicativo tiver sido modificado desde uma atualização anterior, o status exibirá *Pendente*, como mostrado abaixo.

![chlimage_1-163](assets/chlimage_1-163.png)

Em seguida, selecione a ação **Stage** na parte superior direita para criar a nova atualização de conteúdo. Adicione as informações de atualização apropriadas e pressione Concluído.

![chlimage_1-164](assets/chlimage_1-164.png)

O manipulador *Content Sync* cria os pacotes necessários formando um delta (um pacote de *only* o que foi alterado). Depois de concluído, este pacote de conteúdo de atualização foi preparado conforme mostrado abaixo.

O armazenamento temporário de uma atualização no conteúdo permite que várias atualizações sejam feitas antes de serem publicadas na OTA para dispositivos móveis.

>[!NOTE]
>
>O conteúdo preparado pode ser verificado usando o aplicativo AEM Verificar antes de publicar.
>
>Consulte [Início rápido móvel para AEM Verificar](/help/mobile/phonegap-mobile-quickstart.md) para obter mais detalhes sobre AEM Verificar aplicativo.

![chlimage_1-165](assets/chlimage_1-165.png)

Quando estiver pronto para fornecer novo conteúdo para os usuários do aplicativo com Content Sync OTA, selecione **Publicar** como mostrado abaixo.

![chlimage_1-166](assets/chlimage_1-166.png)

### Próximas etapas {#the-next-steps}

Depois de saber mais sobre Criar e gerenciar conteúdo do aplicativo no painel do aplicativo, consulte os seguintes recursos para outras funções de criação:

* [O bloco Gerenciar aplicativo](/help/mobile/phonegap-app-details-tile.md)
* [Editar metadados do aplicativo](/help/mobile/phonegap-editmetadata.md)
* [Definições do aplicativo](/help/mobile/phonegap-app-definitions.md)
* [Criar um novo aplicativo usando o Assistente para criação de aplicativo](/help/mobile/phonegap-create-new-app.md)
* [Importar um aplicativo híbrido existente](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento para Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
