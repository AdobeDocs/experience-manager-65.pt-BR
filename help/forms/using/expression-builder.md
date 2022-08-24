---
title: Funções remotas no Construtor de expressões
seo-title: Expression Builder
description: O Construtor de expressões no Gerenciamento de correspondência permite criar expressões e funções remotas.
seo-description: Expression Builder in Correspondence Management lets you create expressions and remote functions.
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Funções remotas no Construtor de expressões{#remote-functions-in-expression-builder}

Usando o Construtor de expressões, é possível criar expressões ou condições que executam cálculos em valores de dados fornecidos pelo Dicionário de dados ou por usuários finais. O Gerenciamento de correspondência usa o resultado da avaliação da expressão para selecionar ativos, como texto, imagens, listas e condições, e inseri-los na correspondência, conforme necessário.

## Criação de expressões e funções remotas com o Construtor de expressões {#creating-expressions-and-remote-functions-with-expression-builder}

O Construtor de expressões usa internamente as bibliotecas EL JSP, de modo que a expressão adere à sintaxe JSPEL. Para obter mais informações, consulte [Expressões de exemplo](#exampleexpressions).

![Builder de expressões](assets/expressionbuilder.png)

### Operadores {#operators}

Os operadores disponíveis para uso em expressões estão disponíveis na barra superior do construtor de expressões.

### Expressões de exemplo {#exampleexpressions}

Estes são alguns exemplos de JSP EL comumente usados que você pode usar em sua solução de Gerenciamento de correspondência:

* Para adicionar dois números: ${number1 + number2}
* Para concatenar duas strings: ${str1} ${str2}
* Para comparar dois números: ${age &lt; 18}

Você pode encontrar mais informações na [Especificação JSP EL](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). O gerenciador de expressões do lado do cliente não é compatível com determinadas variáveis e funções na especificação JSP EL, especificamente:

* Índices de coleção e chaves de mapa (usando o [] notação) não são suportadas em nomes de variáveis para expressões avaliadas no lado do cliente.
* A seguir estão os tipos de parâmetros ou tipos de retorno de funções usadas em expressões:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.util.list
   * java.lang.Short
   * Curto
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Duplo
   * java.lang.Long
   * Longo
   * java.lang.Float
   * Flutuar
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### Função remota {#remote-function}

As funções remotas fornecem a capacidade de usar lógica personalizada em expressões. Você pode gravar uma lógica personalizada para ser usada na expressão como um método em Java e a mesma função pode ser usada dentro de expressões. As funções remotas disponíveis são listadas na guia &quot;Funções remotas&quot;, no lado esquerdo do Editor de expressão.

![remotefunction](assets/remotefunction.png)

#### Adicionar funções remotas personalizadas {#adding-custom-remote-functions}

Você pode criar um pacote personalizado para exportar suas próprias funções remotas para uso dentro de expressões. Para criar um pacote personalizado para exportar suas próprias funções remotas, execute as seguintes tarefas. Ele demonstra como gravar uma função personalizada que utiliza a letra maiúscula da string de entrada.

1. Defina uma interface para o serviço OSGi que contenha métodos que estão sendo exportados para uso pelo Gerenciador de expressões.
1. Declare métodos na interface A e anote-os com a anotação @ServiceMethod (com.adobe.exm.exval.ServiceMethod). O Gerenciador de expressões ignora quaisquer métodos não anotados. A anotação ServiceMethod tem os seguintes atributos opcionais que também podem ser especificados:

   1. **Ativado**: Determina se este método está ativado. O Gerenciador de expressões ignora métodos desativados.
   1. **familyId**: Especifica a família (grupo) do método. Se estiver vazio, o Gerenciador de expressões assumirá que o método pertence à família padrão. Não há registro de famílias (exceto o padrão) a partir das quais as funções são escolhidas. O Expression Manager cria dinamicamente o registro, fazendo uma união de todas as IDs de família especificadas por todas as funções exportadas pelos vários pacotes. Certifique-se de que a ID especificada aqui seja razoavelmente legível, já que também é exibida na interface do usuário de criação de expressão.
   1. **displayName**: Um nome legível para a função. Esse nome é usado para fins de exibição na interface do usuário de criação. Se estiver vazio, o Gerenciador de expressões construirá um nome padrão usando o prefixo e o nome local da função.
   1. **Descrição**: Uma descrição detalhada da função. Essa descrição é usada para fins de exibição na interface do usuário de criação. Se estiver vazio, o Gerenciador de expressões construirá uma descrição padrão usando o prefixo e o nome local da função.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   Os parâmetros dos métodos também podem ser anotados opcionalmente usando a anotação @ServiceMethodParameter (com.adobe.exm.exval.ServiceMethodParameter). Essa anotação é usada apenas para especificar nomes legíveis em humanos e descrições de parâmetros de método para uso na interface do usuário de criação. Verifique se os parâmetros e valores de retorno dos métodos da interface pertencem a um dos seguintes tipos:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.lang.Short
   * Curto
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Duplo
   * java.lang.Long
   * Longo
   * java.lang.Float
   * Flutuar
   * java.util.Calendar
   * java.util.Date
   * java.util.List


1. Defina a implementação da interface, configure-a como um serviço OSGI e defina as seguintes propriedades do serviço:

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

A entrada exm.service=true instrui o Gerenciador de expressões, de que o serviço contém funções remotas adequadas para uso em expressões. O &lt;service_id> deve ser um identificador Java válido (alfanumérico,$, _ sem outros caracteres especiais). Esse valor, com o prefixo REMOTE_ keyword, forma o prefixo usado dentro de expressões. Por exemplo, uma interface com um método anotado bar() e o ID de serviço das propriedades do serviço podem ser referenciados dentro de expressões usando REMOTE_foo:bar().

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

Abaixo estão os arquivos de amostra a serem usados:

* **GoodFunctions.jar.zip** é o arquivo jar com um pacote contendo uma definição de função remota de amostra. Baixe o arquivo GoodFunctions.jar.zip e descompacte-o para obter o arquivo jar.
* **GoodFunctions.zip** é o pacote de código-fonte para definir uma função remota personalizada e criar um pacote para ela.

GoodFunctions.jar.zip

[Obter arquivo](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Obter arquivo](assets/goodfunctions.zip)
