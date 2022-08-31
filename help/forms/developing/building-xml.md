---
title: Como usar o serviço de script de execução no AEM Forms no JEE Workbench para criar dados XML?
description: Uso do serviço de script de execução no AEM Forms no JEE Workbench para criar dados XML
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Uso do serviço de script de execução no AEM Forms no JEE Workbench para criar dados XML {#using-execute-script-service-forms-jee-workbench}

Há muito XML envolvido com o AEM Forms em workflows de Gerenciamento de Processos JEE, por exemplo: As informações XML podem ser criadas em um processo e enviadas para um aplicativo Flex no AEM Forms no JEE Workspace, usadas para configurações do sistema ou para transmitir informações de e para formulários. Há muitas instâncias em que um desenvolvedor do AEM Forms em JEE precisa gerenciar XML, e muitas vezes isso requer que o XML seja gerenciado por meio de um AEM Forms no processo JEE.

Ao lidar com configurações XML simples, pode-se usar a variável `Set Value` , que é um AEM Forms padrão no serviço JEE. Esse serviço define o valor de um ou mais itens de dados no modelo de dados de processo. Para uma lógica condicional muito simples, &quot;se isso, então isso&quot;, esse serviço pode atender à finalidade.

No entanto, em situações mais complexas, o serviço Definir valor não é tão eficaz. Nessas situações, é preciso confiar em um conjunto mais robusto de comandos de programação, como os fornecidos por uma linguagem de programação como o Java. O uso do Java para criar XML complexo pode ser muito mais fácil e claro do que a criação de um documento XML a partir de um texto simples no serviço Definir valor . Além disso, é mais fácil incluir programação condicional em Java do que em um serviço Definir valor.

## Uso do Serviço de Script de Execução em um Processo {#using-execute-script-service-in-process}

Dentro do conjunto do AEM Forms padrão em serviços JEE disponíveis no AEM Forms no JEE Workbench, é o `Execute Script` serviço. Esse serviço permite executar scripts em processos e fornece o `executeScript` para fazer isso.

### Criar um aplicativo e um processo com o serviço &quot;Executar script&quot; definido como uma atividade {#create-an-application}

A criação geral de aplicativos e processos está fora do escopo para este tutorial, mas para obter essa instrução, criamos um aplicativo chamado &quot;DemoApplication02&quot;. Supondo que um aplicativo já tenha sido criado, precisamos criar um processo neste aplicativo para chamar o serviço executeScript. Para adicionar um processo ao aplicativo que inclui a variável `Execute Script` serviço:

1. Clique com o botão direito do mouse no aplicativo e selecione [!UICONTROL Novo]. Em [!UICONTROL Novo] menu de apresentação, selecione [!UICONTROL Processo]. Nomeie o processo de acordo, adicione uma descrição se necessário e selecione o ícone que deseja representar esse processo. Para os fins deste tutorial, criamos um processo e o nomeamos como o  `executeScriptDemoProcess`.
1. Defina seus pontos de partida ou opte por adicionar seus pontos de partida mais tarde.
1. O processo agora é criado e deve ser aberto automaticamente na variável [!UICONTROL Design do processo] janela. Nesta janela, clique no ícone Seletor de atividades na parte superior da janela Design do processo e arraste a nova atividade para a faixa de nado. Nesse momento, a variável [!UICONTROL Janela Definir atividade] deve ser exibida (veja a Figura abaixo).
   ![Definir atividade](assets/define-activity.jpg)
1. O serviço executeScript pode ser encontrado na função `Foundation` conjunto de serviços. O nome dos Serviços lista o objeto como `Execute Script – 1.0` com o nome da Operação `executeScript`. Clique para selecionar este item.
1. Esse processo deve ser criado e, por padrão, a variável [!UICONTROL Propriedades do processo] deve aparecer no painel à esquerda.

#### Adicionar um script ao processo com o serviço &quot;Executar script&quot; {#add-script-to-process-with-execute-script}

Depois que o processo tiver sido criado com a atividade &quot;Executar Script&quot; Service definida, é possível adicionar um script a esse processo. Para adicionar um script a esse processo:

1. Navegue até o [!UICONTROL Propriedades do processo] paleta. Nesta paleta, expanda a variável [!UICONTROL Entrada] e clique no ícone &quot;...&quot;.

1. Na caixa de texto que aparece, escreva o script. Quando o script tiver sido escrito, pressione OK (veja a Figura abaixo).
   ![Executar script](assets/execute-script.jpg)

## Criando XML Usando o Serviço de Script de Execução {#create-xml-execute-script-service}

Depois que um processo tiver sido criado com o serviço Executar Script incluído, é possível usar esse script para criar XML. Você gravaria os scripts descritos abaixo na caixa de texto descrita em Adicionar um script ao processo com a variável `Execute Script` Seção de serviço acima.

**Sobre a tecnologia do serviço de script de execução**

Para saber quais são as habilidades e limitações do serviço Execute Script, é preciso conhecer os fundamentos tecnológicos do serviço. O AEM Forms no JEE usa o analisador Apache Xerces Document Object Model (DOM) para criar e armazenar variáveis XML em processos. Xerces é uma implementação Java da especificação do Modelo de objeto de documento do W3C; defined [here](https://dom.spec.whatwg.org/). A especificação DOM é uma maneira padrão de manipular o XML, que existe desde 1998. A implementação Java do Xerces, Xerces-J, é compatível com o DOM Nível 2 versão 1.0.

As classes Java usadas para armazenar variáveis XML são:

* org.apache.xerces.dom.NodeImpl e

* org.apache.xerces.dom.DocumentImpl

DocumentImpl é uma subclasse de NodeImpl, portanto, pode-se supor que qualquer variável de processo XML seja uma derivação NodeImpl. Você pode encontrar a documentação do NodeImpl [here](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**Um exemplo de criação de XML com o serviço de script de execução**

Este é o exemplo de criação de XML, dentro de um serviço de script de execução. O processo tem uma variável, nó, que é do tipo XML. O resultado final dessa atividade será um documento XML. O que esse documento faz ou como ele se aplica ao processo geral está fora do escopo deste tutorial; em última análise, se resume ao que o XML é necessário fazer no aplicativo geral. Como foi mencionado na introdução, o XML pode ser usado para vários propósitos no AEM Forms em formulários e processos JEE, essa é simplesmente uma explicação de como codificar a atividade de script Execute para produzir um documento XML simples.

Um script Java simples para saída XML seria semelhante a:

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
>que os objetos DOM acima devem ser importados para o script.

O resultado desse script simples é um novo documento XML com um nó de variável definido como:

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**Uso de um loop iterativo para adicionar nós ao XML**

Nós também podem ser adicionados a uma variável XML existente dentro do processo. A variável , o nó , contém o objeto XML que acabamos de criar.

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
