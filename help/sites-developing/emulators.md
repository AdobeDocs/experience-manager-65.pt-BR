---
title: Emuladores
description: O AEM permite que os autores visualizem uma página em um emulador que simula o ambiente em que um usuário final visualizará a página
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# Emuladores{#emulators}

{{ue-over-mobile}}

O Adobe Experience Manager (AEM) permite que os autores visualizem uma página em um emulador que simula o ambiente em que um usuário final visualizará a página, por exemplo, em um dispositivo móvel ou em um cliente de email.

A estrutura do emulador de AEM:

* Fornece criação de conteúdo em uma interface simulada, por exemplo, um dispositivo móvel ou um cliente de email (usado para criar informativos).
* Adapta o conteúdo da página de acordo com a interface do usuário simulada.
* Permite a criação de emuladores personalizados.

>[!CAUTION]
>
>Este recurso é compatível somente na interface clássica.

## Características dos emuladores {#emulators-characteristics}

Um emulador:

* É baseado em ExtJS.
* Opera na página DOM.
* Sua aparência é regulada por CSS.
* Suporta plug-ins (por exemplo, o plug-in de rotação de dispositivo móvel).
* Está ativo somente no autor.
* Seu componente base está em `/libs/wcm/emulator/components/base`.

### Como o emulador transforma o conteúdo {#how-the-emulator-transforms-the-content}

O emulador funciona envolvendo o conteúdo do corpo do HTML em DIVs do emulador. Por exemplo, o seguinte código html:

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

* o div com id `cq-emulator` que contém o emulador como um todo e

* a div com id `cq-emulator-content` representando a área de visor/tela/conteúdo do dispositivo em que o conteúdo da página reside.

Novas classes CSS também são atribuídas aos novos divs do emulador: elas representam o nome do emulador atual.

Os plug-ins de um emulador podem estender ainda mais a lista de classes CSS atribuídas, como no exemplo do plug-in de rotação, inserindo uma classe &quot;vertical&quot; ou &quot;horizontal&quot; dependendo da rotação do dispositivo atual.

Dessa forma, a aparência completa do emulador pode ser controlada tendo classes CSS correspondentes às IDs e classes CSS dos divs do emulador.

>[!NOTE]
>
>Recomenda-se que o HTML do projeto envolva o conteúdo do corpo em uma única div, como no exemplo acima. Se o conteúdo do corpo contiver várias tags, talvez haja resultados imprevisíveis.

### Emuladores móveis {#mobile-emulators}

Os emuladores móveis existentes:

* Estão abaixo de /libs/wcm/mobile/components/emulators.
* Estão disponíveis pelo servlet JSON em:

  http://localhost:4502/bin/wcm/mobile/emulators.json

Quando o componente de página depende do componente de página móvel ( `/libs/wcm/mobile/components/page`), a funcionalidade de emulador é automaticamente integrada na página através do seguinte mecanismo:

* O componente de página móvel `head.jsp` inclui o componente de inicialização do emulador associado ao grupo de dispositivos (somente no modo de autor) e a renderização de CSS do grupo de dispositivos por meio de:

  `deviceGroup.drawHead(pageContext);`

* O método `DeviceGroup.drawHead(pageContext)` inclui o componente de inicialização do emulador, ou seja, chama o `init.html.jsp` do componente do emulador. Se o componente emulador não tiver seu próprio `init.html.jsp` e depender do emulador base móvel ( `wcm/mobile/components/emulators/base)`, o script de inicialização do emulador base móvel é chamado de ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* O script de inicialização do emulador base móvel é definido pelo JavaScript:

   * A configuração de todos os emuladores definidos para a página (emulatorConfigs)
   * O gerenciador de emulador que integra a funcionalidade do emulador na página por meio de:

     `emulatorMgr.launch(config)`;

     O gerenciador de emulador é definido por:

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Criação de um emulador móvel personalizado {#creating-a-custom-mobile-emulator}

Para criar um emulador móvel personalizado:

1. Abaixo de `/apps/myapp/components/emulators`, crie o componente `myemulator` (tipo de nó: `cq:Component`).

1. Definir a propriedade `sling:resourceSuperType` como `/libs/wcm/mobile/components/emulators/base`

1. Defina uma biblioteca de cliente CSS com a categoria `cq.wcm.mobile.emulator` para a aparência do emulador: nome = `css`, tipo de nó = `cq:ClientLibrary`

   Como exemplo, você pode consultar o nó `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Se necessário, defina uma biblioteca de cliente JS, por exemplo, para definir um plug-in específico: name = js, node type = cq:ClientLibrary

   Como exemplo, você pode consultar o nó `/libs/wcm/mobile/components/emulators/base/js`

1. Se o emulador suportar funcionalidades específicas definidas por plug-ins (como rolagem por toque), crie um nó de configuração abaixo do emulador: nome = `cq:emulatorConfig`, tipo de nó = `nt:unstructured` e adicione a propriedade que define o plug-in:

   * Nome = `canRotate`, Tipo = `Boolean`, Valor = `true`: para incluir a funcionalidade de rotação.

   * Nome = `touchScrolling`, Tipo = `Boolean`, Valor = `true`: para incluir a funcionalidade de rolagem por toque.

   Mais funcionalidades podem ser adicionadas definindo seus próprios plug-ins.
