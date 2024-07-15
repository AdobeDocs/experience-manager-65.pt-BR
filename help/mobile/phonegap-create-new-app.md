---
title: Criação de um aplicativo do AEM Mobile usando o assistente de criação
description: Os aplicativos do AEM Mobile são baseados em um blueprint que define a estrutura e as propriedades da página. Siga esta página para saber como criar um aplicativo com base em um modelo de aplicativo.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---

# Criação de um aplicativo do AEM Mobile usando o assistente de criação{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos do AEM Mobile são baseados em um blueprint que define a estrutura e as propriedades da página. Você pode configurar as seguintes propriedades do aplicativo:

* **Título:** O título do aplicativo.
* **Caminho de Destino:** O local no repositório onde o aplicativo está armazenado. Deixe o padrão para criar um caminho com base no nome do aplicativo.

* **Nome:** o valor padrão é o valor da propriedade Title com caracteres de espaço removidos. O nome é usado no AEM para fazer referência ao aplicativo, por exemplo, para o nó do repositório que representa o aplicativo.
* **Descrição:** Uma descrição do aplicativo.
* **URL do Servidor:** A URL que fornece atualizações de conteúdo OTA (Over-the-Air) para o aplicativo. O valor padrão é o URL do servidor de publicação da instância usada para criar um aplicativo (retirado do serviço do externalizador). Observe que essa deve ser uma instância do servidor de publicação, em vez de um autor, o que requer autenticação.

Você também pode fornecer um arquivo de imagem para usar como miniatura do aplicativo, selecionar a configuração de PhoneGap Build a ser usada e selecionar a configuração de análise do aplicativo móvel a ser usada. Essa imagem só é usada como uma miniatura para representar seu aplicativo móvel no console de aplicativos móveis no Experience Manager.

Existem guias adicionais (e opcionais) para o serviço de nuvem de build e para integrar o plug-in SDK do Adobe Mobile Services ao seu aplicativo.

* Build: clique em gerenciar configurações e configure o serviço de build build.phonegap.com aqui. Em seguida, no menu suspenso, é possível selecionar o serviço de nuvem do PhoneGap Build recém-criado.
* Analytics: clique em gerenciar configurações e configure o serviço de nuvem [SDK do Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/using/home.html). Em seguida, no menu suspenso, é possível selecionar o Mobile Service recém-criado para integrar ao aplicativo móvel.

## Utilização de modelos de aplicativo {#using-app-templates}

Os modelos de aplicativo oferecem uma maneira fácil de usar os designs existentes criados pelos desenvolvedores, usados para a criação de novos aplicativos no AEM.

O que é um modelo de aplicativo? Pense nisso como uma coleção de modelos de página e componentes que representam uma linha de base ou base de um aplicativo.
Ao criar um aplicativo com base no modelo de outro aplicativo, você obterá um aplicativo que tem um ponto de partida representativo do aplicativo no qual ele foi criado.

Você deve ter um modelo de aplicativo móvel existente (ou um aplicativo instalado que tenha um modelo de aplicativo) para usar este recurso.

O pacote de amostras mais recente dos aplicativos AEM inclui uma versão atualizada do aplicativo Geometrixx com um modelo de aplicativo. Como alternativa, você pode instalar o [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit), que também fornece um modelo.

Etapas para criar um aplicativo com base em um modelo de aplicativo:

1. Navegue até o catálogo de aplicativos do AEM Mobile: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Selecione **Criar** e escolha **Aplicativo** conforme mostrado abaixo

![chlimage_1-158](assets/chlimage_1-158.png)

Selecione um modelo de aplicativo disponibilizado a você por um desenvolvedor de AEM. Consulte [Estrutura de um aplicativo AEM Mobile](/help/mobile/phonegap-structure-an-app.md) para obter assistência para desenvolvedores.

![chlimage_1-159](assets/chlimage_1-159.png)

Preencha os detalhes do seu novo aplicativo conforme necessário, incluindo, opcionalmente, a alteração da imagem em miniatura. Esses valores podem ser editados posteriormente no bloco **Gerenciar Aplicativo**.

![chlimage_1-160](assets/chlimage_1-160.png)

## Próximas etapas {#the-next-steps}

Consulte os seguintes recursos para saber mais sobre outras funções de criação:

* [O mosaico Gerenciar aplicativo](/help/mobile/phonegap-app-details-tile.md)
* [Edição de metadados do aplicativo](/help/mobile/phonegap-editmetadata.md)
* [Definições do aplicativo](/help/mobile/phonegap-app-definitions.md)
* [Importar um aplicativo híbrido existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento do Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
