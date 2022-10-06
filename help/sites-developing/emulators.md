---
title: Emuladores
seo-title: Emulators
description: AEM permite que os autores visualizem uma página em um emulador que simula o ambiente em que um usuário final visualizará a página
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Emuladores{#emulators}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O Adobe Experience Manager (AEM) permite que os autores visualizem uma página em um emulador que simula o ambiente em que um usuário final visualizará a página, como em um dispositivo móvel ou em um cliente de email.

A estrutura do emulador de AEM:

* Fornece criação de conteúdo em uma interface de usuário simulada, por exemplo, um dispositivo móvel ou um cliente de email (usado para criar informativos).
* Adapta o conteúdo da página de acordo com a interface do usuário simulada.
* Permite a criação de emuladores personalizados.

>[!CAUTION]
>
>Esse recurso é compatível somente na interface do usuário clássica.

## Características dos emuladores {#emulators-characteristics}

Um emulador:

* É baseado em ExtJS.
* Opera no DOM da página.
* Sua aparência é regulamentada por CSS.
* Suporta plug-ins (por exemplo, o plug-in de rotação de dispositivos móveis).
* Está ativo somente no autor.
* Seu componente base está em `/libs/wcm/emulator/components/base`.

### Como o emulador transforma o conteúdo {#how-the-emulator-transforms-the-content}

O emulador funciona embrulhando o conteúdo do corpo de HTML em DIVs do emulador. Por exemplo, o seguinte código html:

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

é transformado no seguinte código html após o início do emulador:

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

Duas tags div foram adicionadas:

* o div com id `cq-emulator` manter o emulador como um todo e

* o div com id `cq-emulator-content` representando a janela de visualização/tela/área de conteúdo do dispositivo na qual o conteúdo da página reside.

Novas classes CSS também são atribuídas aos novos mergulhadores do emulador: eles representam o nome do emulador atual.

Os plug-ins de um emulador podem estender ainda mais a lista de classes CSS atribuídas, como no exemplo do plug-in de rotação, inserindo uma classe &quot;vertical&quot; ou &quot;horizontal&quot; dependendo da rotação atual do dispositivo.

Dessa forma, a aparência completa do emulador pode ser controlada com classes CSS correspondentes às IDs e classes CSS dos mergulhadores.

>[!NOTE]
>
>Recomenda-se que o HTML do projeto envolva o conteúdo do corpo em uma única div, como no exemplo acima. Se o conteúdo do corpo contiver várias tags, pode haver resultados imprevisíveis.

### Emuladores móveis {#mobile-emulators}

Os emuladores móveis existentes:

* Estão abaixo de /libs/wcm/mobile/components/emulators.
* Estão disponíveis através do servlet JSON em:

   http://localhost:4502/bin/wcm/mobile/emulators.json

Quando o componente de página depende do componente de página móvel ( `/libs/wcm/mobile/components/page`), a funcionalidade do emulador é integrada automaticamente na página por meio do seguinte mecanismo:

* O componente de página móvel `head.jsp` O inclui o componente de inicialização do emulador associado do grupo de dispositivos (somente no modo de autor) e a renderização de CSS do grupo de dispositivos por meio de:

   `deviceGroup.drawHead(pageContext);`

* O método `DeviceGroup.drawHead(pageContext)` inclui o componente init do emulador, ou seja, chama a função `init.html.jsp` do componente emulador. Se o componente emulador não tiver seu próprio `init.html.jsp` e depende do emulador de base móvel ( `wcm/mobile/components/emulators/base)`, o script de inicialização do emulador de base móvel é chamado de ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* O script de inicialização do emulador de base móvel define por meio do Javascript:

   * A configuração de todos os emuladores definidos para a página (emulatorConfigs)
   * O gerenciador do emulador que integra a funcionalidade do emulador na página por meio de:

      `emulatorMgr.launch(config)`;

      O gerenciador do emulador é definido por:

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Criando um emulador móvel personalizado {#creating-a-custom-mobile-emulator}

Para criar um emulador móvel personalizado:

1. Abaixo `/apps/myapp/components/emulators` criar o componente `myemulator` (tipo de nó: `cq:Component`).

1. Defina a propriedade `sling:resourceSuperType` para `/libs/wcm/mobile/components/emulators/base`

1. Definir uma biblioteca de cliente CSS com categoria `cq.wcm.mobile.emulator` para a aparência do emulador: name = `css`, tipo de nó = `cq:ClientLibrary`

   Como exemplo, você pode se referir ao nó `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Se necessário, defina uma biblioteca do cliente JS, por exemplo, para definir um plug-in específico: name = js, tipo de nó = cq:ClientLibrary

   Como exemplo, você pode se referir ao nó `/libs/wcm/mobile/components/emulators/base/js`

1. Se o emulador suportar funcionalidades específicas definidas por plug-ins (como a rolagem de toque), crie um nó de configuração abaixo do emulador: name = `cq:emulatorConfig`, tipo de nó = `nt:unstructured` e adicione a propriedade que define o plug-in:

   * Nome = `canRotate`, Tipo = `Boolean`, Valor = `true`: para incluir a funcionalidade de rotação.

   * Nome = `touchScrolling`, Tipo = `Boolean`, Valor = `true`: para incluir a funcionalidade de rolagem de toque.
   Mais funcionalidades podem ser adicionadas definindo seus próprios plug-ins.
