---
title: Como usar o serviço de execução de script no AEM Forms no JEE Workbench para criar dados XML?
description: Usar o serviço de script de execução no AEM Forms no JEE Workbench para criar dados XML
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 361f0a5f2d1484cf594edfda73250c5690ed7cab
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Usar o serviço de script de execução no AEM Forms no JEE Workbench para criar dados XML {#using-execute-script-service-forms-jee-workbench}

Há muito XML envolvido com workflows de gerenciamento de processos do AEM Forms no JEE, por exemplo: informações XML podem ser criadas em um processo e enviadas para um aplicativo do Flex no AEM Forms no JEE Workspace, usadas para configurações de sistemas ou transmitindo informações de e para formulários. Há muitas instâncias em que um desenvolvedor do AEM Forms no JEE precisa gerenciar XML e, muitas vezes, isso requer que o XML seja gerenciado por meio de um processo do AEM Forms no JEE.

Ao lidar com configurações XML simples, é possível usar o serviço `Set Value`, que é um AEM Forms padrão no serviço JEE. Este serviço define o valor de um ou mais itens de dados no modelo de dados de processo. Para cenários de lógica condicional simples &quot;se isso, então aquilo&quot;, esse serviço pode atender à finalidade.

No entanto, em situações mais complexas, o serviço de Definir valor não é tão eficaz. Nessas situações, é necessário confiar em um conjunto mais robusto de comandos de programação, como os fornecidos por uma linguagem de programação como o Java™. Usar o Java™ para criar XML complexos pode ser muito mais fácil e mais claro do que criar um documento XML a partir de texto simples no serviço de Definir valor. Além disso, é mais fácil incluir programação condicional em Java™ do que em um serviço de Definir valor.

## Uso do Serviço de Execução de Script em um Processo {#using-execute-script-service-in-process}

No conjunto dos serviços padrão do AEM Forms no JEE disponíveis no AEM Forms no JEE Workbench, está o serviço `Execute Script`. Este serviço permite que você execute scripts em processos e fornece a operação `executeScript` para fazer isso.

### Criar um aplicativo e um processo com o serviço &quot;Executar script&quot; definido como uma atividade {#create-an-application}

Em geral, a criação de aplicativos e processos está fora do escopo deste tutorial, mas por causa dessa instrução, um aplicativo chamado &quot;DemoApplication02&quot; foi criado. Supondo que um aplicativo já tenha sido criado, é necessário criar um processo nesse aplicativo para chamar o serviço executeScript. Para adicionar um processo ao aplicativo que inclui o serviço `Execute Script`:

1. Clique com o botão direito do mouse no aplicativo e selecione **[!UICONTROL Novo]**. No menu deslizante **[!UICONTROL Novo]**, selecione **[!UICONTROL Processo]**. Nomeie o processo, adicione uma descrição, se necessário, e selecione o ícone que deseja representar esse processo. Para os fins deste tutorial, criamos um processo e o nomeamos como `executeScriptDemoProcess`.
1. Defina seus pontos iniciais ou opte por adicionar seus pontos iniciais posteriormente.
1. O processo foi criado e deve ser aberto automaticamente na janela [!UICONTROL Design do Processo]. Nesta janela, clique no ícone Seletor de atividades na parte superior da janela Design do processo e arraste a nova atividade para a pista de natação. Neste ponto, a [!UICONTROL Janela Definir Atividade] deve aparecer (veja a Figura abaixo).
   ![Definir Atividade](assets/define-activity.jpg)
1. O serviço executeScript pode ser encontrado no conjunto de serviços `Foundation`. O nome de Serviços lista o objeto como `Execute Script – 1.0` com o nome de Operação `executeScript`. Clique para selecionar este item.
1. Esse processo agora deve ser criado e, por padrão, a janela [!UICONTROL Propriedades do processo] deve aparecer no painel à esquerda.

#### Adicionar um script ao processo com o serviço &quot;Executar script&quot; {#add-script-to-process-with-execute-script}

Depois que o processo tiver sido criado com a atividade &quot;Executar Script&quot; Service definida, é possível adicionar um script a esse processo. Para adicionar um script a esse processo:

1. Navegue até a paleta [!UICONTROL Propriedades do processo]. Nesta paleta, expanda a seção [!UICONTROL Entrada] e clique no ícone &quot;...&quot;.

1. Na caixa de texto exibida, escreva o script. Quando o script tiver sido gravado, pressione OK (veja a Figura abaixo).
   ![Executar Script](assets/execute-script.jpg)

## Criando XML Usando o Serviço de Script de Execução {#create-xml-execute-script-service}

Depois que um processo é criado com o serviço Executar script incluído, é possível usar esse script para criar XML. Você pode escrever os scripts descritos abaixo na caixa de texto descrita na seção Adicionar um script ao processo com o Serviço `Execute Script` acima.

>[!NOTE]
>
> Se o código do script JAVA exceder 10 linhas, é recomendável adicionar o código aos DSCs personalizados (Componentes do serviço de documento) em vez de gravá-lo diretamente no processo. Os DSCs personalizados melhoram a capacidade de manutenção, a reutilização e o desempenho, mantendo os fluxos de trabalho leves. A referência a esses componentes em workflows garante melhor eficiência da execução e evita possíveis lentidões causadas pelo processamento de grandes blocos de código no fluxo de trabalho.


**Sobre a Tecnologia do Serviço Executar Script**

Para saber quais são as habilidades e limitações do serviço Execute Script, é preciso conhecer os fundamentos tecnológicos do serviço. O AEM Forms no JEE usa o analisador do Apache Xerces Document Object Model (DOM) para criar e armazenar variáveis XML em processos. Xerces é uma implementação Java™ da [especificação de Modelo de Objeto de Documento](https://dom.spec.whatwg.org/) da W3C. A especificação DOM é uma maneira padrão de manipular XML que existe desde 1998. A implementação Java™ do Xerces, Xerces-J, é compatível com a versão 1.0 do DOM Nível 2.

As classes Java™ usadas para armazenar variáveis XML são:

* org.apache.xerces.dom.NodeImpl e

* org.apache.xerces.dom.DocumentImpl

DocumentImpl é uma subclasse de NodeImpl, então pode-se supor que qualquer variável de processo XML é uma derivação de NodeImpl. Consulte a documentação de [NodeImpl](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html) para obter mais detalhes.

**Criação de Exemplo XML Usando o Serviço de Execução de Script**

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

**Usando um loop Iterativo para Adicionar Nós ao XML**

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

// found the top-level node

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
