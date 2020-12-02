---
title: Estruturar um aplicativo
seo-title: Estruturar um aplicativo
description: Siga esta página para saber mais sobre como criar a estrutura de um aplicativo. Esta página descreve como estruturar modelos e componentes junto com informações sobre JavaScript e CSS Clientlibs.
seo-description: Siga esta página para saber mais sobre como criar a estrutura de um aplicativo. Esta página descreve como estruturar modelos e componentes junto com informações sobre JavaScript e CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---


# Estruturar um aplicativo{#structure-an-app}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Um projeto da AEM Mobile envolve um conjunto diversificado de tipos de conteúdo, incluindo páginas, bibliotecas de clientes JavaScript e CSS, componentes AEM reutilizáveis, configurações de Sincronização de conteúdo e conteúdo do shell de aplicativo PhoneGap. Basear seu novo aplicativo AEM Mobile no [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) é uma boa maneira de inserir todos os diferentes tipos de conteúdo em nossa estrutura recomendada para facilitar a portabilidade e a manutenção a longo prazo.

## Conteúdo da página {#page-content}

As páginas do aplicativo devem estar todas localizadas abaixo de /content/mobileapps para que sejam reconhecidas pelo console do AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Por AEM convenção, a primeira página do aplicativo deve ser um redirecionamento para um dos filhos, que serve como o idioma padrão do aplicativo (&#39;en&#39; nos casos do Geometrixx e do Starter Kit). A página de local de nível superior normalmente é herdada do componente &#39;splash-page&#39; da base (/libs/mobileapps/components/splash-page) que cuida da inicialização necessária para suportar a instalação de atualizações de Sincronização de conteúdo ao ar (o código contentInit pode ser encontrado em /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modelos e componentes {#templates-and-components}

O modelo e o código do componente do aplicativo devem estar localizados em /apps/&lt;nome da marca>/&lt;nome do aplicativo>. Em conformidade com a convenção, você deve colocar o modelo e o código do componente em /apps/&lt;nome da marca>/&lt;nome do aplicativo>. Esse padrão deve ser familiar para desenvolvedores que já trabalharam com o Site em AEM. Normalmente, é seguido como /apps/ está bloqueado para acesso anônimo por padrão nas instâncias de publicação. Assim, seu código JSP bruto está oculto de possíveis atacantes.

Os modelos específicos do aplicativo podem ser configurados para serem apresentados somente usando o nó de propriedade `allowedPaths` no próprio modelo e definindo seu valor como &#39;/content/mobileapps(/.&amp;ast;)?&#39; - ou mesmo algo mais específico se o modelo só deve ser utilizado para um único aplicativo. As propriedades `allowedParents` e `allowedChildren` também podem ser aproveitadas para obter um controle muito refinado de quais modelos estarão disponíveis para um autor com base no local em que a nova página está sendo criada.

Ao criar um novo componente de página do aplicativo do zero, é recomendável definir sua propriedade `sling:resourceSuperType` como &#39;mobileapps/components/angle/ng-page&#39;. Isso configurará sua página para criação e renderização como um aplicativo de página única e permitirá que você sobreponha quaisquer arquivos .jsp que seu componente precise alterar. Como ng-page não inclui nenhuma estrutura de interface de usuário, um desenvolvedor normalmente acabará sobrepondo (pelo menos) &#39;template.jsp&#39; (sobreposto de /libs/mobileapps/components/angular/ng-page/template.jsp).

Os componentes de página autoráveis, que desejam aproveitar AngularJS, têm um componente `sling:resourceSuperType` equivalente localizado em /libs/mobileapps/components/angular/ng-component que pode ser sobreposto e personalizado da mesma maneira.

## JavaScript e Clientlibs CSS {#javascript-and-css-clientlibs}

Quando se trata de bibliotecas de clientes, há algumas opções disponíveis para o desenvolvedor de onde colocá-las no repositório. O seguinte padrão é oferecido como orientação, mas não é um requisito difícil.

Se o código do cliente puder ficar por conta própria e não estiver relacionado a um componente específico do aplicativo - o que significa que ele pode ser reutilizado em outros aplicativos - recomendamos armazená-lo em /etc/clientlibs/&lt;nome da marca>/&lt;nome da biblioteca>. Por outro lado, se a clientlib for específica de um único aplicativo, você poderá aninhá-la como um filho do nó de design do aplicativo; /etc/designs/phonegap/&lt;nome da marca>/&lt;nome do aplicativo>/clientlibs. A categoria deste clientlib não deve ser usada por outras libs e deve ser usada para incorporar outras libs, conforme necessário. Seguir esses padrões evita que o desenvolvedor tenha que adicionar novas configurações de Sincronização de conteúdo sempre que uma biblioteca cliente for adicionada ao aplicativo, em vez de simplesmente atualizar a propriedade &quot;embeds&quot; da clientlib de design do aplicativo. Por exemplo, observe o nó de configuração Geometrixx clientlibs-all Content Sync em /content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all.

Se o código do lado do cliente estiver estreitamente associado a um componente específico, coloque-o em uma biblioteca do cliente aninhada abaixo da localização do componente em /apps/ e incorpore-o à categoria do cliente &#39;design&#39; do aplicativo.

## Configuração do PhoneGap {#phonegap-configuration}

Cada aplicativo AEM Mobile contém um diretório que hospeda os arquivos de configuração usados pela interface de linha de comando PhoneGap [e ](https://github.com/phonegap/phonegap-cli)PhoneGap build](https://build.phonegap.com/) para transformar seu conteúdo da Web em um aplicativo executável. [ Por exemplo, na amostra de Geometrixx, esse diretório (/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content) está localizado como parte do Shell; uma decisão de design tomada devido ao fato de conter apenas conteúdo que não pode ser atualizado ao ar, como plug-ins que lidam com as APIs do dispositivo e a configuração do próprio aplicativo.

Neste diretório, você também encontrará vários [ganchos do Cordova](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) que podem ser usados para instalar plug-ins, colocar arquivos de recursos em seus locais específicos da plataforma e outras ações que devem ser executadas como parte da compilação. Observação: como alternativa ao download de cada plug-in como parte da criação, você pode seguir o padrão do aplicativo Kitchen Sink e [incluir código fonte do plug-in](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) com o restante do projeto do aplicativo.

## Próximas etapas {#the-next-steps}

Depois de saber mais sobre a estrutura do aplicativo, consulte [Criar e editar aplicativos usando o console do aplicativo](/help/mobile/phonegap-apps-console.md).
