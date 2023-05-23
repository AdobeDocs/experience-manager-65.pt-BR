---
title: Estruturar um aplicativo
seo-title: Structure an App
description: Siga esta página para saber mais sobre como criar a estrutura de um aplicativo. Esta página descreve como estruturar modelos e componentes juntamente com informações sobre bibliotecas de clientes JavaScript e CSS.
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

# Estruturar um aplicativo{#structure-an-app}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Um projeto do AEM Mobile envolve um conjunto diverso de tipos de conteúdo, incluindo páginas, bibliotecas de clientes JavaScript e CSS, componentes AEM reutilizáveis, configurações de sincronização de conteúdo e conteúdo do shell do aplicativo PhoneGap. Basear seu novo aplicativo AEM Mobile no [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) O é uma boa maneira de incluir todos os diferentes tipos de conteúdo em nossa estrutura recomendada para facilitar a portabilidade e a manutenção a longo prazo.

## Conteúdo da página {#page-content}

As páginas do aplicativo devem estar localizadas abaixo de /content/mobileapps para serem reconhecidas pelo console do AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Por convenção do AEM, a primeira página do aplicativo deve ser um redirecionamento para uma das crianças que serve como idioma padrão do aplicativo (&quot;en&quot; nos casos de Geometrixx e Starter Kit). A página de local de nível superior normalmente herda do componente &quot;página inicial&quot; da base (/libs/mobileapps/components/splash-page) que cuida da inicialização necessária para oferecer suporte à instalação de atualizações de sincronização de conteúdo ao ar (o código contentInit pode ser encontrado em /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modelos e componentes {#templates-and-components}

O modelo e o código do componente do seu aplicativo devem estar localizados em /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. De acordo com a convenção, você deve colocar seu modelo e código de componente em /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. Esse padrão deve ser familiar aos desenvolvedores que já trabalharam com o Site no AEM. Normalmente, é seguido como /apps/ e bloqueado para acesso anônimo por padrão em instâncias de publicação. Portanto, seu código JSP bruto está oculto de possíveis invasores.

Os modelos específicos do aplicativo podem ser configurados para serem apresentados somente usando o `allowedPaths` nó de propriedade no próprio modelo e definindo seu valor como &#39;/content/mobileapps(/.&amp;ast;)?&#39; - ou até mesmo algo mais específico se o modelo só puder ser usado para um único aplicativo. A variável `allowedParents` e `allowedChildren` as propriedades também podem ser aproveitadas para um controle refinado de quais modelos estarão disponíveis para um autor com base no local em que a nova página está sendo criada.

Ao criar um novo componente da página de aplicativo do zero, é recomendável definir sua `sling:resourceSuperType` para &#39;mobileapps/components/angular/ng-page&#39;. Isso configurará a página para criação e renderização como um aplicativo de página única e permitirá que você sobreponha quaisquer arquivos .jsp que seu componente possa precisar alterar. Como a ng-página não inclui nenhuma estrutura de interface do usuário, um desenvolvedor normalmente acabará sobrepondo (pelo menos) &#39;template.jsp&#39; (sobreposto de /libs/mobileapps/components/angular/ng-page/template.jsp).

Os componentes de página possíveis para aproveitar o AngularJS têm um `sling:resourceSuperType` componente localizado em /libs/mobileapps/components/angular/ng-component, que pode ser sobreposto e personalizado da mesma forma.

## Clientlibs JavaScript e CSS {#javascript-and-css-clientlibs}

Quando se trata de bibliotecas de clientes, há algumas opções disponíveis para o desenvolvedor de onde colocá-las no repositório. O seguinte padrão é oferecido para orientação, mas não é um requisito difícil.

Se o código do lado do cliente puder ser criado sozinho e não estiver relacionado a um componente específico do aplicativo, o que significa que ele pode ser reutilizado em outros aplicativos, recomendamos armazená-lo em /etc/clientlibs/&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. Por outro lado, se clientlib for específico para um único aplicativo, você poderá aninhá-lo como filho do nó de design do seu aplicativo; /etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs. A categoria desta clientlib não deve ser usada por outras bibliotecas e deve ser usada para incorporar outras, conforme necessário. Seguir esses padrões evita que o desenvolvedor tenha que adicionar novas configurações de sincronização de conteúdo sempre que uma biblioteca do cliente for adicionada ao aplicativo. Em vez disso, basta atualizar a propriedade &quot;embeds&quot; da clientlib de design do aplicativo. Por exemplo, observe o nó de configuração da sincronização de conteúdo Geometrixx clientlibs-all em /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all.

Se o código do lado do cliente estiver totalmente acoplado a um componente específico, coloque-o em uma biblioteca do cliente aninhada abaixo do local do componente em /apps/ e incorpore sua categoria à clientlib &quot;design&quot; do aplicativo.

## Configuração do PhoneGap {#phonegap-configuration}

Cada aplicativo AEM Mobile contém um diretório que hospeda os arquivos de configuração usados pelo PhoneGap [interface de linha de comando](https://github.com/phonegap/phonegap-cli) e [PhoneGap Build](https://build.phonegap.com/) para transformar seu conteúdo da web em um aplicativo executável. Na amostra do Geometrixx, por exemplo, este diretório (/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content) está localizado como parte do Shell; uma decisão de design feita devido ao fato de que ele contém apenas conteúdo que não pode ser atualizado ao ar, como plug-ins que lidam com APIs de dispositivo e a configuração do próprio aplicativo.

Neste diretório, você também encontrará vários [Ganchos Cordova](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) que pode ser usado para instalar plug-ins, colocar arquivos de recurso em seus locais específicos da plataforma e outras ações que devem ser executadas como parte da build. Observação: como alternativa ao download de cada plug-in como parte da criação, você pode seguir o padrão do aplicativo Coletor de cozinha e [incluir código fonte do plug-in](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) com o restante do projeto de aplicativo.

## Próximas etapas {#the-next-steps}

Depois de conhecer a estrutura do aplicativo, consulte [Criação e edição de aplicativos usando o console de aplicativos](/help/mobile/phonegap-apps-console.md).
