---
title: Como usar o serviço de execução de script no AEM Forms no JEE Workbench para criar dados XML?
description: Usar o serviço de script de execução no AEM Forms no JEE Workbench para criar dados XML
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Usar o serviço de script de execução no AEM Forms no JEE Workbench para criar dados XML {#using-execute-script-service-forms-jee-workbench}

Há muitos XML envolvidos com o AEM Forms em workflows de gerenciamento de processos do JEE, por exemplo: informações XML podem ser criadas em um processo e enviadas para um aplicativo do Flex no AEM Forms no JEE Workspace, usadas para configurações de sistemas ou transmitindo informações de e para formulários. Há muitas instâncias em que um desenvolvedor do AEM Forms no JEE precisa gerenciar XML e, muitas vezes, isso requer que o XML seja gerenciado por meio de um processo do AEM Forms no JEE.

Ao lidar com configurações XML simples, é possível usar o `Set Value` serviço, que é um AEM Forms padrão no serviço JEE. Este serviço define o valor de um ou mais itens de dados no modelo de dados de processo. Para cenários de lógica condicional simples &quot;se isso, então aquilo&quot;, esse serviço pode atender à finalidade.

No entanto, em situações mais complexas, o serviço de Definir valor não é tão eficaz. Nessas situações, é necessário confiar em um conjunto mais robusto de comandos de programação, como os fornecidos por uma linguagem de programação como o Java™. Usar o Java™ para criar XML complexos pode ser muito mais fácil e mais claro do que criar um documento XML a partir de texto simples no serviço de Definir valor. Além disso, é mais fácil incluir programação condicional em Java™ do que em um serviço de Definir valor.

## Uso do Serviço de Execução de Script em um Processo {#using-execute-script-service-in-process}

No conjunto dos serviços padrão do AEM Forms no JEE disponíveis no AEM Forms no JEE Workbench, está o `Execute Script` serviço. Este serviço permite que você execute scripts em processos e fornece a `executeScript` operação para fazer isso.

### Criar um aplicativo e um processo com o serviço &quot;Executar script&quot; definido como uma atividade {#create-an-application}

Em geral, a criação de aplicativos e processos está fora do escopo deste tutorial, mas por causa dessa instrução, um aplicativo chamado &quot;DemoApplication02&quot; foi criado. Supondo que um aplicativo já tenha sido criado, é necessário criar um processo nesse aplicativo para chamar o serviço executeScript. Para adicionar um processo ao aplicativo que inclua o `Execute Script` serviço:

1. Clique com o botão direito do mouse no aplicativo e selecione **[!UICONTROL Novo]**. Entrada **[!UICONTROL Novo]** menu deslizante, selecione **[!UICONTROL Processo]**. Nomeie o processo, adicione uma descrição, se necessário, e selecione o ícone que deseja representar esse processo. Para os propósitos deste tutorial, criamos um processo e o nomeamos como  `executeScriptDemoProcess`.
1. Defina seus pontos iniciais ou opte por adicionar seus pontos iniciais posteriormente.
1. O processo agora é criado e deve ser aberto automaticamente no [!UICONTROL Design do processo] janela. Nesta janela, clique no ícone Seletor de atividades na parte superior da janela Design do processo e arraste a nova atividade para a pista de natação. Neste ponto, a variável [!UICONTROL Janela Definir Atividade] (veja a Figura abaixo).
   ![Definir atividade](assets/define-activity.jpg)
1. O serviço executeScript pode ser encontrado no `Foundation` conjunto de serviços. O nome Services lista o objeto como `Execute Script – 1.0` com o nome da Operação `executeScript`. Clique para selecionar este item.
1. Esse processo agora deve ser criado e, por padrão, o [!UICONTROL Propriedades do processo] deve aparecer no painel à esquerda.

#### Adicionar um script ao processo com o serviço &quot;Executar script&quot; {#add-script-to-process-with-execute-script}

Depois que o processo tiver sido criado com a atividade &quot;Executar Script&quot; Service definida, é possível adicionar um script a esse processo. Para adicionar um script a esse processo:

1. Navegue até a [!UICONTROL Propriedades do processo] paleta. Nesta paleta, expanda a variável [!UICONTROL Entrada] e clique no ícone &quot;...&quot;.

1. Na caixa de texto exibida, escreva o script. Quando o script tiver sido gravado, pressione OK (veja a Figura abaixo).
   ![Executar Script](assets/execute-script.jpg)

## Criando XML Usando o Serviço de Script de Execução {#create-xml-execute-script-service}

Depois que um processo é criado com o serviço Executar script incluído, é possível usar esse script para criar XML. Você escreveria os scripts descritos abaixo na caixa de texto descrita em Adicionar um script ao processo com o `Execute Script` seção de serviço acima.

**Sobre a tecnologia do Execute Script Service**

Para saber quais são as habilidades e limitações do serviço Execute Script, é preciso conhecer os fundamentos tecnológicos do serviço. O AEM Forms no JEE usa o analisador do Apache Xerces Document Object Model (DOM) para criar e armazenar variáveis XML em processos. Xerces é uma implementação Java™ da especificação Document Object Model da W3C; definida [aqui](https://dom.spec.whatwg.org/). A especificação DOM é uma maneira padrão de manipular XML que existe desde 1998. A implementação Java™ do Xerces, Xerces-J, é compatível com a versão 1.0 do DOM Nível 2.

As classes Java™ usadas para armazenar variáveis XML são:

* org.apache.xerces.dom.NodeImpl e

* org.apache.xerces.dom.DocumentImpl

DocumentImpl é uma subclasse de NodeImpl, então pode-se supor que qualquer variável de processo XML é uma derivação de NodeImpl. Você pode encontrar a documentação do NodeImpl [aqui](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**Um exemplo de criação XML usando o serviço Executar script**

Este é um exemplo de criação de XML, em um serviço Executar script. O processo tem um nó de variável do tipo XML. O resultado desta atividade é um documento XML. O que esse documento faz ou como se aplica ao processo geral está fora do escopo deste tutorial; em última análise, se resume ao que o XML é necessário fazer no aplicativo geral. Como foi mencionado na introdução, o XML pode ser usado para muitos propósitos no AEM Forms em formulários e processos JEE, esta é simplesmente uma explicação de como codificar a atividade Executar script para produzir um documento XML simples.

Um JavaScript simples para XML de saída seria semelhante a:

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>Os objetos DOM mencionados anteriormente devem ser importados para o script.

O resultado desse script simples é um novo documento XML com um nó de variável definido como:

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**Usando um loop iterativo para adicionar nós ao XML**

Os nós também podem ser adicionados a uma variável XML existente no processo. A variável, nó, contém o objeto XML criado.

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```
