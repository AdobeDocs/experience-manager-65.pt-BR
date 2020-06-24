---
title: Criar um novo aplicativo do AEM Mobile usando o assistente de criação
seo-title: Criar um novo aplicativo do AEM Mobile usando o assistente de criação
description: Os aplicativos do AEM Mobile são baseados em um plano que define uma estrutura de página e propriedades. Siga esta página para saber como criar um novo aplicativo com base em um modelo de aplicativo.
seo-description: Os aplicativos do AEM Mobile são baseados em um plano que define uma estrutura de página e propriedades. Siga esta página para saber como criar um novo aplicativo com base em um modelo de aplicativo.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Criar um novo aplicativo do AEM Mobile usando o assistente de criação{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos do AEM Mobile são baseados em um plano que define uma estrutura de página e propriedades. Você pode configurar as seguintes propriedades do aplicativo:

* **Título:** O título do aplicativo.
* **Caminho de destino:** O local no repositório onde o aplicativo é armazenado. Deixe o padrão para criar um caminho com base no nome do aplicativo.

* **Nome:** O valor padrão é o valor da propriedade Title com caracteres de espaço removidos. O nome é usado no AEM para fazer referência ao aplicativo, por exemplo, para o nó do repositório que representa o aplicativo.
* **Descrição:** Uma descrição do aplicativo.
* **URL do servidor:** O URL que fornece atualizações de conteúdo OTA (Over-the-Air) ao aplicativo. O valor padrão é o URL do servidor de publicação da instância usada para criar um aplicativo (retirado do serviço externalizador). Observe que essa deve ser uma instância do servidor de publicação em vez de um autor, o que requer autenticação.

Você também pode fornecer um arquivo de imagem para usar como miniatura do aplicativo, selecionar a configuração do PhoneGap Build a ser usada e selecionar a configuração de análise do aplicativo móvel a ser usada. Essa imagem é usada apenas como uma miniatura para representar seu aplicativo móvel no console de aplicativos móveis no Experience Manager.

Existem guias adicionais (e opcionais) para criar o serviço em nuvem e integrar o plug-in do SDK do Adobe Mobile Services ao seu aplicativo.

* Compilação: Clique em gerenciar configurações e configure seu serviço de compilação.phonegap.com aqui. Em seguida, na lista suspensa, você poderá selecionar o serviço de nuvem de construção PhoneGap recém-criado.
* Analytics: Clique em gerenciar configurações e configure o serviço em nuvem SDK [do](https://docs.adobe.com/content/help/en/mobile-services/using/home.html) Adobe Mobile Services. Em seguida, na lista suspensa, você poderá selecionar o Mobile Service recém-criado para integrar ao seu aplicativo móvel.

## Uso de modelos de aplicativo {#using-app-templates}

Os modelos de aplicativos fornecem uma maneira fácil de aproveitar os designs existentes criados pelos desenvolvedores, usados para a criação de novos aplicativos no AEM.

O que é um modelo de aplicativo? Pense nele como uma coleção de modelos de página e componentes que representam uma linha de base ou a base de um aplicativo.
Ao criar um novo aplicativo com base no modelo de outro aplicativo, você obterá um aplicativo que tenha um representante de ponto de partida do aplicativo no qual ele foi criado.

É necessário ter um modelo de aplicativo móvel existente (ou um aplicativo instalado que tenha um modelo de aplicativo) para usar esse recurso.

O pacote de exemplos de aplicativos AEM mais recente inclui uma versão atualizada do aplicativo Geometrixx com um modelo de aplicativo. Como alternativa, você pode instalar o [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) que também fornece um modelo.

Etapas para criar um novo aplicativo com base em um modelo de aplicativo:

1. Navegue até o catálogo de aplicativos do AEM Mobile: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Selecione **Criar** e escolha **Aplicativo** como mostrado abaixo

![chlimage_1-158](assets/chlimage_1-158.png)

Selecione um modelo de aplicativo disponibilizado para você por um desenvolvedor do AEM. Consulte [Estrutura de um aplicativo](/help/mobile/phonegap-structure-an-app.md) do AEM Mobile para obter ajuda para desenvolvedores.

![chlimage_1-159](assets/chlimage_1-159.png)

Preencha os detalhes do novo aplicativo conforme necessário, incluindo a alteração opcional da imagem em miniatura. Esses valores podem ser editados posteriormente no bloco **Gerenciar aplicativo** .

![chlimage_1-160](assets/chlimage_1-160.png)

## Próximas etapas {#the-next-steps}

Consulte os seguintes recursos para saber mais sobre outras funções de criação:

* [O bloco Gerenciar aplicativo](/help/mobile/phonegap-app-details-tile.md)
* [Editar metadados do aplicativo](/help/mobile/phonegap-editmetadata.md)
* [Definições do aplicativo](/help/mobile/phonegap-app-definitions.md)
* [Importar um aplicativo híbrido existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento para Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
