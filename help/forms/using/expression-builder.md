---
title: Funções remotas no Construtor de expressões
description: O Construtor de expressões no Gerenciamento de correspondências permite criar expressões e funções remotas.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Funções remotas no Construtor de expressões{#remote-functions-in-expression-builder}

Usando o Construtor de expressões, você pode criar expressões ou condições que executam cálculos em valores de dados fornecidos pelo Dicionário de dados ou pelos usuários finais. O Gerenciamento de correspondências usa o resultado da avaliação da expressão para selecionar ativos como texto, imagens, listas e condições e inseri-los na correspondência, conforme necessário.

## Criar expressões e funções remotas com o construtor de expressões {#creating-expressions-and-remote-functions-with-expression-builder}

O Construtor de expressões usa internamente bibliotecas JSP EL, de modo que a expressão adere à sintaxe JSPEL. Para obter mais informações, consulte [Expressões de exemplo](#exampleexpressions).

![Construtor de Expressões](assets/expressionbuilder.png)

### Operadores {#operators}

Os operadores disponíveis para uso em expressões estão disponíveis na barra superior do construtor de expressões.

### Expressões de exemplo {#exampleexpressions}

Estes são alguns exemplos de JSP EL usados com frequência que você pode usar na solução de Gerenciamento de correspondência:

* Para adicionar dois números: ${number1 + number2}
* Para concatenar duas cadeias de caracteres: ${str1} ${str2}
* Para comparar dois números: ${age &lt; 18}

Você pode encontrar mais informações na [especificação JSP EL](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). O gerenciador de expressões do lado do cliente não suporta determinadas variáveis e funções na especificação JSP EL, especificamente:

* Índices de coleção e chaves de mapa (usando a notação []) não têm suporte em nomes de variáveis para expressões avaliadas no lado do cliente.
* A seguir estão os tipos de parâmetros ou tipos de retorno das funções usadas em expressões:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.util.list
   * java.lang.Short
   * Short
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Duplo
   * java.lang.Long
   * Longo
   * java.lang.Float
   * Flutuante
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### Função remota {#remote-function}

As funções remotas fornecem a capacidade de usar lógica personalizada em expressões. Você pode escrever uma lógica personalizada para ser usada na expressão como um método em Java, e a mesma função pode ser usada dentro das expressões. As funções remotas disponíveis são listadas na guia &quot;Funções remotas&quot; no lado esquerdo do Editor de expressão.

![remotefunction](assets/remotefunction.png)

#### Adicionar funções remotas personalizadas {#adding-custom-remote-functions}

Você pode criar um pacote personalizado para exportar suas próprias funções remotas para uso em expressões internas. Para criar um pacote personalizado para exportar suas próprias funções remotas, execute as tarefas a seguir. Ele demonstra como gravar uma função personalizada que coloca sua string de entrada em maiúsculas.

1. Defina uma interface para o serviço OSGi contendo métodos que estão sendo exportados para uso pelo Gerenciador de Expressões.
1. Declare os métodos na interface A e anote-os com a anotação @ServiceMethod (com.adobe.exm.expeval.ServiceMethod). O Gerenciador de expressões ignora todos os métodos não anotados. A anotação ServiceMethod tem os seguintes atributos opcionais que também podem ser especificados:

   1. **Habilitado**: determina se este método está habilitado. O Gerenciador de Expressões ignora métodos desativados.
   1. **familyId**: especifica a família (grupo) do método. Se estiver vazio, o Gerenciador de expressões presume que o método pertence à família padrão. Não há registro de famílias (exceto a padrão) a partir das quais as funções são escolhidas. O Gerenciador de expressão cria dinamicamente o registro, unindo todas as IDs de família especificadas por todas as funções exportadas pelos vários pacotes. Certifique-se de que a ID especificada aqui possa ser lida razoavelmente, pois é exibida também na interface do usuário da criação de expressões.
   1. **displayName**: um nome legível para a função. Esse nome é usado para fins de exibição na interface do usuário de criação. Se estiver vazio, o Gerenciador de Expressões construirá um nome padrão usando o prefixo da função e o nome local.
   1. **Descrição**: uma descrição detalhada da função. Essa descrição é usada para fins de exibição na interface do usuário de criação. Se estiver vazio, o Gerenciador de Expressões construirá uma descrição padrão usando o prefixo da função e o nome local.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   Os parâmetros dos métodos também podem ser anotados opcionalmente usando a anotação @ServiceMethodParameter (com.adobe.exm.expeval.ServiceMethodParameter). Essa anotação é usada apenas para especificar nomes e descrições legíveis por humanos de parâmetros de método para uso na interface do usuário de criação. Certifique-se de que os parâmetros e valores de retorno dos métodos da interface pertençam a um dos seguintes tipos:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.lang.Short
   * Short
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Duplo
   * java.lang.Long
   * Longo
   * java.lang.Float
   * Flutuante
   * java.util.Calendar
   * java.util.Date
   * java.util.List

1. Defina a implementação da interface, configure-a como um serviço OSGI e defina as seguintes propriedades de serviço:

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

A entrada exm.service=true instrui o Gerenciador de expressão de que o serviço contém funções remotas adequadas para uso em expressões. O valor &lt;service_id> deve ser um identificador Java válido (alfanumérico,$, _ sem outros caracteres especiais). Esse valor, com o prefixo da palavra-chave REMOTE_, forma o prefixo que é usado dentro das expressões. Por exemplo, uma interface com um método bar() anotado e a ID de serviço foo nas propriedades de serviço, pode ser referenciada dentro de expressões usando REMOTE_foo:bar().

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

Abaixo estão exemplos de arquivos a serem usados:

* **GoodFunctions.jar.zip** é o arquivo jar com um pacote que contém uma definição de função remota de amostra. Baixe o arquivo GoodFunctions.jar.zip e descompacte-o para obter o arquivo jar.
* **GoodFunctions.zip** é o pacote de código-fonte para definir uma função remota personalizada e criar um pacote para ela.

GoodFunctions.jar.zip

[Obter arquivo](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Obter arquivo](assets/goodfunctions.zip)
