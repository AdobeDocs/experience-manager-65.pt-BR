---
title: Composite Components em SPAs
description: Saiba como criar seus próprios componentes compostos, componentes compostos de outros componentes que funcionam com o Editor de aplicativo de página única (SPA) AEM.
exl-id: 02b6c698-d169-467a-9168-9fa6181bed6c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Composite Components em SPAs {#composite-components-in-spas}

Os componentes compostos aproveitam a natureza modular dos componentes de AEM ao combinar vários componentes básicos em um único componente. Um caso de uso comum de componente composto é o componente do cartão, feito de uma combinação da imagem e dos componentes do texto.

Quando os componentes compostos são implementados adequadamente na estrutura do Editor de aplicativo de página única (SPA) do AEM, os autores de conteúdo podem arrastar e soltar esses componentes da mesma forma que fazem com qualquer outro componente, mas ainda têm a capacidade de editar individualmente cada componente que compõe o componente composto.

Este artigo demonstra como você pode adicionar um componente composto ao seu aplicativo de página única para funcionar perfeitamente com o Editor de SPA de AEM.

## Caso de uso  {#use-case}

Este artigo usará o componente de cartão típico como exemplo de caso de uso. Os cartões são um elemento comum da interface do usuário para muitas experiências digitais e normalmente são compostos de uma imagem e texto ou legenda associados. Um autor deseja poder arrastar e soltar o cartão inteiro, mas pode editar individualmente a imagem do cartão, bem como personalizar o texto associado.

## Pré-requisitos {#prerequisites}

Os modelos a seguir para suportar os casos de uso de componentes compostos exigem os seguintes pré-requisitos.

* Sua instância de desenvolvimento de AEM está sendo executada localmente na porta 4502 com um projeto de amostra.
* Você tem um aplicativo React externo funcional [habilitado para edição no AEM.](spa-edit-external.md)
* O aplicativo React é carregado no editor de AEM [usando o componente Página remota.](spa-remote-page.md)

## Adicionar componentes compostos a um SPA {#adding-composite-components}

Há três modelos diferentes para implementar seu componente composto, dependendo da implementação do SPA no AEM.

* [O componente não existe no seu projeto de AEM.](#component-does-not-exist)
* [O componente existe em seu projeto do AEM, mas o conteúdo necessário não.](#content-does-not-exist)
* [O componente e seu conteúdo necessário existem no projeto do AEM.](#both-exist)

As seções a seguir fornecem exemplos da implementação de cada caso usando o componente de cartão como exemplo.

### O componente não existe no seu projeto de AEM. {#component-does-not-exist}

Comece criando os componentes que farão parte do componente composto, ou seja, os componentes da imagem e seu texto.

1. Crie o componente de texto no seu projeto de AEM.
1. Adicione o `resourceType` do projeto no `editConfig` nó .

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. Use o `withMappable` auxiliar para ativar a edição do componente.

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

O componente de texto será semelhante ao seguinte.

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

Se você criar um componente de imagem de maneira semelhante, poderá combiná-lo com o `AEMText` em um novo componente de cartão, usando a imagem e os componentes de texto como filhos.

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

Esse componente composto resultante agora pode ser colocado em qualquer lugar no aplicativo e o adicionará espaços reservados para um componente de texto e imagem no Editor de SPA. Na amostra abaixo, o componente de cartão é adicionado ao componente inicial abaixo do título.

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

Isso exibirá um espaço reservado vazio para um texto e uma imagem no editor. Ao inserir valores para eles usando o editor, eles são armazenados no caminho de página especificado, ou seja, `/content/wknd-spa/home`  no nível da raiz com os nomes especificados em `itemPath`.

![Componente de placa composta no editor](assets/composite-card.png)

### O componente existe em seu projeto do AEM, mas o conteúdo necessário não. {#content-does-not-exist}

Nesse caso, o componente de cartão já é criado em seu projeto de AEM contendo o título e os nós de imagem. Os nós filhos (texto e imagem) têm os tipos de recursos correspondentes.

![Estrutura do nó do componente da placa](assets/composite-node-structure.png)

Em seguida, você pode adicioná-lo ao seu SPA e recuperar o conteúdo.

1. Crie um componente correspondente no SPA para isso. Certifique-se de que os componentes filho sejam mapeados para seus tipos de recursos AEM correspondentes no projeto SPA. Neste exemplo, usamos o mesmo `AEMText` e `AEMImage` componentes como detalhados [no caso anterior.](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. Como não há conteúdo para a variável `imagecard` , adicione o cartão à página. Inclua o contêiner existente do AEM no SPA.
   * Se já houver um contêiner no projeto do AEM, podemos incluir no SPA e adicionar o componente ao contêiner do AEM.
   * Verifique se o componente de cartão está mapeado para o tipo de recurso correspondente no SPA.

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. Adicione o `wknd-spa/components/imagecard` componente para os componentes permitidos para o componente de contêiner [no modelo da página.](/help/sites-authoring/templates.md)

Agora a variável `imagecard` pode ser adicionado diretamente ao contêiner no editor de AEM.

![Placa composta no editor](assets/composite-card.gif)

### O componente e seu conteúdo necessário existem no projeto do AEM. {#both-exist}

Se o conteúdo existir no AEM, ele poderá ser incluído diretamente no SPA fornecendo o caminho para o conteúdo.

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![Caminho composto na estrutura do nó](assets/composite-path.png)

O `AEMCard` componente é igual ao definido [no caso de uso anterior.](#content-does-not-exist) Aqui, o conteúdo definido na localização acima no projeto AEM está incluído na SPA .
