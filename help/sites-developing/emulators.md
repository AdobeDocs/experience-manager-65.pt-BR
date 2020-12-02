---
title: Emuladores
seo-title: Emuladores
description: AEM permite que os autores visualizações uma página em um emulador que simula o ambiente no qual um usuário final visualização a página
seo-description: AEM permite que os autores visualizações uma página em um emulador que simula o ambiente no qual um usuário final visualização a página
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Emuladores{#emulators}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

O Adobe Experience Manager (AEM) permite que os autores visualizações uma página em um emulador que simula o ambiente no qual um usuário final visualização a página, como, por exemplo, em um dispositivo móvel ou em um cliente de email.

A estrutura do emulador de AEM:

* Fornece a criação de conteúdo em uma interface de usuário (UI) simulada, por exemplo, um dispositivo móvel ou um cliente de email (usado para criar boletins informativos).
* Adapta o conteúdo da página de acordo com a interface simulada.
* Permite a criação de emuladores personalizados.

>[!CAUTION]
>
>Esse recurso é suportado somente na interface clássica.

## Características dos emuladores {#emulators-characteristics}

Um emulador:

* É baseado em ExtJS.
* Opera na página DOM.
* Sua aparência é regulamentada pelo CSS.
* Suporta plug-ins (por exemplo, o plug-in de rotação de dispositivos móveis).
* Está ativo somente no autor.
* Seu componente básico está em `/libs/wcm/emulator/components/base`.

### Como o Emulador Transforma o Conteúdo {#how-the-emulator-transforms-the-content}

O emulador funciona vinculando o conteúdo do corpo HTML em DIVs do emulador. Por exemplo, o seguinte código html:

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

é transformado no seguinte código html após o start do emulador:

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

* div com a id `cq-emulator` segurando o emulador como um todo e

* a div com a id `cq-emulator-content` que representa a janela de visualização/tela/área de conteúdo do dispositivo na qual o conteúdo da página reside.

As novas classes CSS também são atribuídas aos novos divs do emulador: representam o nome do emulador atual.

Os plug-ins de um emulador podem estender ainda mais a lista das classes CSS atribuídas, como no exemplo do plug-in de rotação, inserindo uma classe &quot;vertical&quot; ou &quot;horizontal&quot; dependendo da rotação atual do dispositivo.

Dessa forma, a aparência completa do emulador pode ser controlada por ter classes CSS correspondentes às classes IDs e CSS do emulador divs.

>[!NOTE]
>
>É recomendável que o HTML do projeto envolva o conteúdo do corpo em uma única div, como no exemplo acima. Se o conteúdo do corpo contiver várias tags, pode haver resultados imprevisíveis.

### Emuladores móveis {#mobile-emulators}

Os emuladores móveis existentes:

* Estão abaixo de /libs/wcm/mobile/components/emuladores.
* Estão disponíveis através do servlet JSON em:

   http://localhost:4502/bin/wcm/mobile/emulators.json

Quando o componente de página depende do componente de página móvel ( `/libs/wcm/mobile/components/page`), a funcionalidade do emulador é integrada automaticamente na página por meio do seguinte mecanismo:

* O componente de página móvel `head.jsp` inclui o componente de inicialização do emulador associado do grupo de dispositivos (somente no modo do autor) e a renderização do CSS pelo grupo de dispositivos através de:

   `deviceGroup.drawHead(pageContext);`

* O método `DeviceGroup.drawHead(pageContext)` inclui o componente de inicialização do emulador, isto é, chama `init.html.jsp` do componente do emulador. Se o componente do emulador não tiver seu próprio `init.html.jsp` e depender do emulador base móvel ( `wcm/mobile/components/emulators/base)`, o script init do emulador base móvel será chamado ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* O script init do emulador de base móvel define por meio do Javascript:

   * A configuração para todos os emuladores definidos para a página (emulatorConfigs)
   * O gerenciador de emuladores que integra a funcionalidade do emulador na página por meio de:

      `emulatorMgr.launch(config)`;

      O gerenciador de emuladores é definido por:

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Criando um emulador móvel personalizado {#creating-a-custom-mobile-emulator}

Para criar um emulador móvel personalizado:

1. Abaixo `/apps/myapp/components/emulators` crie o componente `myemulator` (tipo de nó: `cq:Component`).

1. Defina a propriedade `sling:resourceSuperType` como `/libs/wcm/mobile/components/emulators/base`

1. Defina uma biblioteca de cliente CSS com a categoria `cq.wcm.mobile.emulator` para a aparência do emulador: name = `css`, tipo de nó = `cq:ClientLibrary`

   Como exemplo, você pode fazer referência ao nó `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Se necessário, defina uma biblioteca de cliente JS, por exemplo, para definir um plug-in específico: name = js, tipo de nó = cq:ClientLibrary

   Como exemplo, você pode fazer referência ao nó `/libs/wcm/mobile/components/emulators/base/js`

1. Se o emulador suportar funcionalidades específicas definidas por plug-ins (como rolagem de toque), crie um nó de configuração abaixo do emulador: name = `cq:emulatorConfig`, node type = `nt:unstructured` e adicione a propriedade que define o plug-in:

   * Nome = `canRotate`, Tipo = `Boolean`, Valor = `true`: para incluir a funcionalidade de rotação.

   * Nome = `touchScrolling`, Tipo = `Boolean`, Valor = `true`: para incluir a funcionalidade de rolagem de toque.

   É possível adicionar mais funcionalidades definindo seus próprios plug-ins.

