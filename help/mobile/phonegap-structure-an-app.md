---
title: Estrutura de um aplicativo
seo-title: Structure an App
description: Siga esta página para saber como criar a estrutura de um aplicativo. Esta página descreve como estruturar modelos e componentes junto com informações sobre JavaScript e CSS Clientlibs.
seo-description: Follow this page to learn about how to create structure of an app. This page describes how to structure templates and components along with information on JavaScript and CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# Estrutura de um aplicativo{#structure-an-app}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Um projeto do AEM Mobile envolve um conjunto diverso de tipos de conteúdo, incluindo páginas, bibliotecas de clientes JavaScript e CSS, componentes AEM reutilizáveis, configurações de Sincronização de conteúdo e conteúdo do shell de aplicativo PhoneGap. Basear seu novo aplicativo AEM Mobile no [Kit inicial](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) é uma boa maneira de inserir todos os diferentes tipos de conteúdo em nossa estrutura recomendada para facilitar a portabilidade e a manutenção a longo prazo.

## Conteúdo da página {#page-content}

As páginas do seu aplicativo devem estar localizadas abaixo de /content/mobileapps para serem reconhecidas pelo console do AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Por AEM convenção, a primeira página do aplicativo deve ser um redirecionamento para um dos filhos, que serve como o idioma padrão do aplicativo (&#39;en&#39; nos casos do Geometrixx e do Starter Kit). A página de local de nível superior normalmente herda do componente de base &#39;splash-page&#39; (/libs/mobileapps/components/splash-page) que cuida da inicialização necessária para suportar a instalação de atualizações de Sincronização de conteúdo ao ar (o código contentInit pode ser encontrado em /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modelos e componentes {#templates-and-components}

O modelo e o código do componente do aplicativo devem estar localizados em /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. Em conformidade com a convenção, você deve colocar o modelo e o código do componente em /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. Esse padrão deve ser familiar aos desenvolvedores que já trabalharam com o Site no AEM. Normalmente, é seguido como /apps/ está bloqueado para acesso anônimo por padrão em instâncias de publicação. Dessa forma, seu código JSP bruto está oculto de possíveis atacantes.

Os modelos específicos do aplicativo podem ser configurados para serem apresentados apenas usando o `allowedPaths` nó de propriedade no próprio template e definindo seu valor para &#39;/content/mobileapps(/.&amp;ast;)?&#39; - ou até mesmo algo mais específico, se o modelo for utilizável apenas para um único aplicativo. O `allowedParents` e `allowedChildren` As propriedades também podem ser aproveitadas para obter um controle muito refinado de quais modelos estarão disponíveis para um autor com base no local em que a nova página está sendo criada.

Ao criar um novo componente de página do aplicativo do zero, é recomendável definir seu `sling:resourceSuperType` propriedade para &#39;mobileapps/components/angular/ng-page&#39;. Isso configurará a página para criação e renderização como um aplicativo de página única e permitirá que você sobreponha quaisquer arquivos .jsp que seu componente precise alterar. Como a ng-page não inclui nenhuma estrutura de interface do usuário, um desenvolvedor normalmente acabará sobrepondo (pelo menos) &quot;template.jsp&quot; (sobreposto de /libs/mobileapps/components/angular/ng-page/template.jsp).

Os componentes de página autoráveis, que desejam utilizar o AngularJS, têm um equivalente `sling:resourceSuperType` componente localizado em /libs/mobileapps/components/angular/ng-component, que pode ser sobreposto e personalizado da mesma maneira.

## Clientlibs de JavaScript e CSS {#javascript-and-css-clientlibs}

Quando se trata de bibliotecas de clientes, há algumas opções disponíveis para o desenvolvedor de onde colocá-las no repositório. O seguinte padrão é oferecido como orientação, mas não é um requisito difícil.

Se o código do lado do cliente puder ficar por conta própria e não estiver relacionado a um componente específico de seu aplicativo - o que significa que pode ser reutilizado em outros aplicativos - recomendamos armazená-lo em /etc/clientlibs/&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. Por outro lado, se a clientlib for específica de um único aplicativo, você poderá aninhá-la como filha do nó de design do seu aplicativo; /etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs. Esta categoria da clientlib não deve ser usada por outras libs e deve ser usada para incorporar outras libs, conforme necessário. Seguir esses padrões evita que o desenvolvedor tenha que adicionar novas configurações de Sincronização de conteúdo sempre que uma biblioteca do cliente for adicionada ao aplicativo, em vez disso, basta atualizar a propriedade &quot;embeds&quot; da clientlib de design do aplicativo. Por exemplo, dê uma olhada no nó de configuração da Sincronização de conteúdo tudo/clientlibs do Geometrixx em /content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all.

Se o código do lado do cliente estiver totalmente acoplado a um componente específico, coloque esse código em uma biblioteca do cliente aninhada abaixo do local do componente em /apps/ e incorpore-o à categoria da clientlib &quot;design&quot; do aplicativo.

## Configuração do PhoneGap {#phonegap-configuration}

Cada aplicativo do AEM Mobile contém um diretório que hospeda os arquivos de configuração usados pelo PhoneGap [interface da linha de comando](https://github.com/phonegap/phonegap-cli) e [Build do PhoneGap](https://build.phonegap.com/) para transformar seu conteúdo da Web em um aplicativo executável. Na amostra do Geometrixx, por exemplo, esse diretório (/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content) está localizado como parte do Shell; uma decisão de design tomada devido ao fato de conter apenas conteúdo que não pode ser atualizado ao ar, como plug-ins que lidam com APIs de dispositivo e a configuração do próprio aplicativo.

Nesse diretório, você também encontrará vários [Ganchos Cordova](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) que podem ser usados para instalar plug-ins, colocar arquivos de recursos em locais específicos da plataforma e outras ações que devem ser executadas como parte da build. Observação: como alternativa ao download de cada plug-in como parte da build, você pode seguir o padrão do aplicativo Sink da Cozinha e [incluir código fonte do plug-in](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) com o resto do projeto do aplicativo.

## Próximas etapas {#the-next-steps}

Depois de saber mais sobre a estrutura do aplicativo, consulte [Criação e edição de aplicativos usando o console do aplicativo](/help/mobile/phonegap-apps-console.md).
