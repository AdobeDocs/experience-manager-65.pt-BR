---
title: Estrutura da interface do usuário habilitada para toque do Adobe Experience Manager
description: A interface otimizada para toque, conforme implementada no Adobe Experience Manager, tem vários princípios subjacentes e é composta de vários elementos-chave
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 2%

---

# Estrutura da interface do usuário habilitada para toque do Adobe Experience Manager{#structure-of-the-aem-touch-enabled-ui}

A interface habilitada para toque do Adobe Experience Manager (AEM) tem vários princípios subjacentes e é composta por vários elementos-chave:

## Consoles {#consoles}

### Layout básico e redimensionamento {#basic-layout-and-resizing}

A interface do usuário atende aos dispositivos móveis e de desktop, no entanto, em vez de criar dois estilos, o Adobe decidiu usar um estilo que funciona para todas as telas e dispositivos.

Todos os módulos usam o mesmo layout básico; no AEM, isso pode ser visto como:

![chlimage_1-142](assets/chlimage_1-142.png)

O layout segue um estilo de design responsivo e se acomoda ao tamanho do dispositivo/janela que você está usando.

Por exemplo, quando a resolução cai para menos de 1024 px (como em um dispositivo móvel), a tela é ajustada de acordo:

![chlimage_1-143](assets/chlimage_1-143.png)

### Barra do cabeçalho {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

A barra de cabeçalho mostra elementos globais incluindo:

* o logotipo e o produto/solução específica que você está usando atualmente; para o AEM, isso também forma um link para a Navegação global
* Pesquisar
* ícone para acessar os recursos de ajuda
* ícone para acessar outras soluções
* um indicador de (e acesso a) qualquer alerta ou item da Caixa de entrada que esteja esperando por você
* o ícone do usuário, junto com um link para o gerenciamento do perfil

### Barra de ferramentas {#toolbar}

Isso é contextual à sua localização e às ferramentas de superfícies relevantes para controlar a exibição ou os ativos na página abaixo. A barra de ferramentas é específica do produto, mas há alguns elementos em comum.

Em qualquer local, a barra de ferramentas mostra as ações disponíveis no momento:

![chlimage_1-145](assets/chlimage_1-145.png)

Também depende se um recurso está selecionado:

![chlimage_1-146](assets/chlimage_1-146.png)

### Painel esquerdo {#left-rail}

O painel esquerdo pode ser aberto/oculto, conforme necessário, para mostrar:

* **Linha do tempo**
* **Referências**
* **Filtro**

O padrão é **Somente conteúdo** (painel oculto).

![chlimage_1-147](assets/chlimage_1-147.png)

## Criação de página {#page-authoring}

Ao criar páginas, as áreas estruturais são as seguintes.

### Quadro de conteúdo {#content-frame}

O conteúdo da página é renderizado no quadro de conteúdo. O quadro de conteúdo é independente do editor, para garantir que não haja conflitos devido ao CSS ou ao JavaScript.

O quadro de conteúdo está na seção à direita da janela, na barra de ferramentas.

![chlimage_1-148](assets/chlimage_1-148.png)

### Quadro do editor {#editor-frame}

O quadro do editor reconhece os recursos de edição.

O quadro do editor é um contêiner (abstrato) para todas as *elementos de criação de página*. Ela fica na parte superior do quadro de conteúdo e inclui:

* a barra de ferramentas superior
* o painel lateral
* todas as sobreposições
* qualquer outro elemento de criação da página; por exemplo, a barra de ferramentas do componente

![chlimage_1-149](assets/chlimage_1-149.png)

### Painel lateral {#side-panel}

Ela contém duas guias padrão que permitem selecionar ativos e componentes. Eles podem ser arrastados daqui e soltos na página.

O painel lateral fica oculto por padrão. Quando selecionado, ele será mostrado no lado esquerdo ou deslizará para cobrir a janela inteira (quando o tamanho da janela estiver abaixo de uma largura de 1024 px; como, por exemplo, em um dispositivo móvel).

![chlimage_1-150](assets/chlimage_1-150.png)

### Painel lateral - Ativos {#side-panel-assets}

Na guia Ativos, é possível selecionar dentre uma variedade de ativos. Você também pode filtrar por um termo específico ou selecionar um grupo.

![chlimage_1-151](assets/chlimage_1-151.png)

### Painel lateral - Grupos de ativos {#side-panel-asset-groups}

Na guia Ativo, há uma lista suspensa que você pode usar para selecionar os grupos de ativos específicos.

![chlimage_1-152](assets/chlimage_1-152.png)

### Painel lateral - Componentes {#side-panel-components}

Na guia Componentes, é possível selecionar dentre uma variedade de componentes. Você também pode filtrar por um termo específico ou selecionar um grupo.

![chlimage_1-153](assets/chlimage_1-153.png)

### Sobreposições {#overlays}

Eles sobrepõem o quadro de conteúdo e são usados pelo [camadas](#layer) para conhecer os mecanismos de como você pode interagir (de forma transparente) com os componentes e seu conteúdo.

As sobreposições ficam no quadro do editor (com todos os outros elementos de criação de página), embora elas realmente sobreponham os componentes apropriados no quadro de conteúdo.

![chlimage_1-154](assets/chlimage_1-154.png)

### Camada {#layer}

Uma camada é um conjunto independente de funcionalidades que pode ser ativada para:

* forneça uma visualização diferente da página
* permitem manipular e/ou interagir com uma página

As camadas fornecem funcionalidade sofisticada para a página inteira, em vez de ações específicas em um componente individual.

O AEM vem com várias camadas já implementadas para a criação de páginas; incluindo, por exemplo, editar, visualizar, anotar.

>[!NOTE]
>
>As camadas são um conceito eficiente que afeta a visualização e a interação do usuário com o conteúdo da página. Ao desenvolver suas próprias camadas, você deve garantir que a camada seja limpa ao sair.

### Alternador de camada {#layer-switcher}

O alternador de camadas permite escolher a camada que deseja usar. Quando fechada, indica a camada em uso no momento.

O alternador de camadas está disponível como uma lista suspensa na barra de ferramentas (na parte superior da janela, dentro do quadro do editor).

![chlimage_1-155](assets/chlimage_1-155.png)

### Component Toolbar {#component-toolbar}

Cada instância de um componente revela sua barra de ferramentas quando clicado (uma vez ou com um clique duplo lento). A barra de ferramentas contém as ações específicas (por exemplo, copiar, colar, abrir editor) que estão disponíveis para a instância do componente (Editável) na página.

Dependendo do espaço disponível, as barras de ferramentas do componente são posicionadas no canto superior ou inferior direito do componente apropriado.

![chlimage_1-156](assets/chlimage_1-156.png)

## Informações adicionais {#further-information}

Para obter mais detalhes sobre os conceitos da interface habilitada para toque, leia [Conceitos da interface habilitada para toque por AEM](/help/sites-developing/touch-ui-concepts.md).

Para obter mais informações técnicas, consulte [Conjunto de documentação JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) para o editor de páginas habilitado para toque.
