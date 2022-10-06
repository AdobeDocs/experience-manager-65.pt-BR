---
title: Estrutura da interface de usuário habilitada para toque do AEM
seo-title: Structure of the AEM Touch-Enabled UI
description: A interface otimizada para toque, conforme implementada no AEM, tem vários princípios subjacentes e é composta de vários elementos principais
seo-description: The touch-optimized UI, as implemented in AEM, has several underlying principles and is made up of several key elements
uuid: 9a255238-1adc-4a40-9c37-30cb53ffb26c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 55dba890-4847-4986-b272-33480bc1d573
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# Estrutura da interface de usuário habilitada para toque do AEM{#structure-of-the-aem-touch-enabled-ui}

A interface do usuário habilitada para toque do AEM tem vários princípios subjacentes e é composta de vários elementos principais:

## Consoles {#consoles}

### Layout básico e redimensionamento {#basic-layout-and-resizing}

A interface do usuário abrange dispositivos móveis e de desktop, mas em vez de criar dois estilos, o Adobe decidiu usar um estilo que funciona para todas as telas e dispositivos.

Todos os módulos usam o mesmo layout básico, AEM isso pode ser visto como:

![chlimage_1-142](assets/chlimage_1-142.png)

O layout adere a um estilo de design responsivo e se acomodará ao tamanho do dispositivo/janela usado.

Por exemplo, quando a resolução fica abaixo de 1024px (como em um dispositivo móvel), a exibição será ajustada adequadamente:

![chlimage_1-143](assets/chlimage_1-143.png)

### Barra do cabeçalho {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

A barra de cabeçalho mostra elementos globais incluindo:

* o logotipo e o produto/solução específico que você está usando atualmente; para AEM isso também forma um link para a Navegação global
* Pesquisar
* ícone para acessar os recursos de ajuda
* ícone para acessar outras soluções
* um indicador de (e acesso a) quaisquer alertas ou itens da Caixa de entrada que estão aguardando você
* o ícone do usuário, juntamente com um link para o gerenciamento de perfis

### Barra de ferramentas {#toolbar}

Isso é contextual à sua localização e às ferramentas da superfície relevantes para controlar a exibição ou os ativos na página abaixo. A barra de ferramentas é específica do produto, mas há uma compatibilidade entre os elementos.

Em qualquer local, a barra de ferramentas mostra as ações disponíveis no momento:

![chlimage_1-145](assets/chlimage_1-145.png)

Também depende de um recurso estar selecionado no momento:

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

O conteúdo da página é renderizado no quadro de conteúdo. O quadro de conteúdo é completamente independente do editor - para garantir que não haja conflitos devido a CSS ou javascript.

O quadro de conteúdo está na seção à direita da janela, abaixo da barra de ferramentas.

![chlimage_1-148](assets/chlimage_1-148.png)

### Quadro do editor {#editor-frame}

O quadro do editor executa os recursos de edição.

O quadro do editor é um contêiner (abstrato) para todos os *elementos de criação de página*. Ela fica sobre o quadro de conteúdo e inclui:

* a barra de ferramentas superior
* painel lateral
* todas as sobreposições
* qualquer outro elemento de criação de página; por exemplo, a barra de ferramentas do componente

![chlimage_1-149](assets/chlimage_1-149.png)

### Painel lateral {#side-panel}

Ela contém duas guias padrão para permitir que você selecione ativos e componentes; eles podem ser arrastados daqui e soltos na página.

O painel lateral está oculto por padrão. Quando selecionada, ela será exibida no lado esquerdo ou deslizará para cobrir toda a janela (quando o tamanho da janela estiver abaixo de 1024px; como, por exemplo, em um dispositivo móvel).

![chlimage_1-150](assets/chlimage_1-150.png)

### Painel lateral - Ativos {#side-panel-assets}

Na guia Ativos , é possível selecionar entre a faixa de ativos. Também é possível filtrar por um termo específico ou selecionar um grupo.

![chlimage_1-151](assets/chlimage_1-151.png)

### Painel lateral - Grupos de ativos {#side-panel-asset-groups}

Na guia Ativo, há uma lista suspensa que pode ser usada para selecionar os grupos de ativos específicos.

![chlimage_1-152](assets/chlimage_1-152.png)

### Painel lateral - Componentes {#side-panel-components}

Na guia Componentes , é possível selecionar entre as várias opções de componentes. Também é possível filtrar por um termo específico ou selecionar um grupo.

![chlimage_1-153](assets/chlimage_1-153.png)

### Sobreposições {#overlays}

Eles sobrepõem o quadro de conteúdo e são usados pela variável [camadas](#layer) para compreender os mecanismos de como você pode interagir (de forma totalmente transparente) com os componentes e seu conteúdo.

As sobreposições vivem no quadro do editor (com todos os outros elementos de criação de página), embora elas realmente sobreponham os componentes apropriados no quadro de conteúdo.

![chlimage_1-154](assets/chlimage_1-154.png)

### Camada {#layer}

Uma camada é um conjunto de funcionalidades independente que pode ser ativado para:

* fornecer uma exibição diferente da página
* permitir manipular e/ou interagir com uma página

As camadas fornecem funcionalidade sofisticada para a página inteira, em vez de ações específicas em um componente individual.

AEM vem com várias camadas já implementadas para criação de página; incluindo, por exemplo, editar, visualizar e anotar.

>[!NOTE]
>
>Camadas são um conceito poderoso que afeta a exibição do usuário e a interação com o conteúdo da página. Ao desenvolver suas próprias camadas, é necessário garantir que a camada seja limpa ao sair.

### Seletor de camada {#layer-switcher}

O alternador de camadas permite escolher a camada que deseja usar. Quando fechado, indica a camada em uso no momento.

O alternador de camadas está disponível como uma lista suspensa na barra de ferramentas (na parte superior da janela, dentro do quadro do editor).

![chlimage_1-155](assets/chlimage_1-155.png)

### Component Toolbar {#component-toolbar}

Cada instância de um componente revelará a barra de ferramentas ao clicar (uma vez ou com um clique duplo lento). A barra de ferramentas contém as ações específicas (por exemplo, copiar, colar, abrir o editor) que estão disponíveis para a instância do componente (Editável) na página.

Dependendo do espaço disponível, as barras de ferramentas do componente são posicionadas no canto superior ou inferior direito do componente adequado.

![chlimage_1-156](assets/chlimage_1-156.png)

## Informações adicionais {#further-information}

Para obter mais detalhes sobre os conceitos sobre a interface habilitada para toque, continue com o artigo [Conceitos da interface de usuário habilitada para toque do AEM](/help/sites-developing/touch-ui-concepts.md).

Para obter mais informações técnicas, consulte o [Conjunto de documentação JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) para o editor de página habilitado para toque.
