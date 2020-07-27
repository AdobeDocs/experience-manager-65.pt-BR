---
title: Funções remotas no Expressão Builder
seo-title: Builder de expressões
description: O Construtor de Expressões no Gerenciamento de correspondência permite criar expressões e funções remotas.
seo-description: O Construtor de Expressões no Gerenciamento de correspondência permite criar expressões e funções remotas.
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---


# Funções remotas no Expressão Builder{#remote-functions-in-expression-builder}

Usando o Construtor de Expressões, você pode criar expressões ou condições que executam cálculos em valores de dados fornecidos pelo Dicionário de dados ou por usuários finais. O Gerenciamento de correspondência usa o resultado da avaliação da expressão para selecionar ativos como texto, imagens, listas e condições e inseri-los na correspondência, conforme necessário.

## Criação de expressões e funções remotas com o expressão Builder {#creating-expressions-and-remote-functions-with-expression-builder}

O Construtor de Expressões usa internamente bibliotecas JSP EL, de modo que a expressão adere à sintaxe JSPEL. Para obter mais informações, consulte [Exemplo de expressões](#exampleexpressions).

![Builder de expressões](assets/expressionbuilder.png)

### Operadores {#operators}

Os operadores disponíveis para uso no expressão estão disponíveis na barra superior do construtor de expressões.

### expressões de exemplo {#exampleexpressions}

Estes são alguns exemplos de JSP EL comumente usados que podem ser usados na solução Gerenciamento de correspondência:

* Para adicionar dois números: ${number1 + number2}
* Para concatenar duas strings: ${str1} ${str2}
* Para comparar dois números: ${age &lt; 18}

Você pode encontrar mais informações na especificação [](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf)JSP EL. O gerenciador de expressões do cliente não suporta determinadas variáveis e funções na especificação JSP EL, especificamente:

* Os índices de coleção e as chaves de mapa (usando a [] notação) não são suportados em nomes de variáveis para expressão avaliados no cliente.
* A seguir estão os tipos de parâmetros ou tipos de retorno de funções usados no expressão:

   * java.lang.String
   * java.lang.Character
   * Carro
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

As funções remotas fornecem a capacidade de usar a lógica personalizada no expressão. Você pode gravar lógica personalizada para ser usada na expressão como um método em Java e a mesma função pode ser usada dentro do expressão. As funções remotas disponíveis são listadas na guia &quot;Funções remotas&quot;, no lado esquerdo do Editor de Expressões.

![remotefunction](assets/remotefunction.png)

#### Adicionar funções remotas personalizadas {#adding-custom-remote-functions}

Você pode criar um pacote personalizado para exportar suas próprias funções remotas para uso no expressão. Para criar um pacote personalizado para exportar suas próprias funções remotas, execute as seguintes tarefas. Ele demonstra como gravar uma função personalizada que coloca em letra maiúscula sua string de entrada.

1. Defina uma interface para o serviço OSGi que contenha métodos que estão sendo exportados para uso pelo Gerenciador de Expressões.
1. Declare os métodos na interface A e anote-os com a anotação @ServiceMethod (com.adobe.exm.exm.exval.ServiceMethod). O Gerenciador de Expressões ignora todos os métodos não anotados. A anotação ServiceMethod tem os seguintes atributos opcionais que também podem ser especificados:

   1. **Ativado**: Determina se este método está ativado. O Gerenciador de Expressões ignora os métodos desativados.
   1. **familyId**: Especifica a família do método (grupo). Se estiver vazio, o Gerenciador de Expressões assumirá que o método pertence à família padrão. Não há registro de famílias (exceto o padrão) a partir das quais as funções são escolhidas. O Gerenciador de Expressões cria dinamicamente o registro, tirando uma união de todas as IDs de família especificadas por todas as funções exportadas pelos vários pacotes. Certifique-se de que a ID especificada aqui seja razoavelmente legível, já que também é exibida na interface do usuário de criação de expressões.
   1. **displayName**: Um nome legível para a função. Esse nome é usado para fins de exibição na interface do usuário de criação. Se estiver vazio, o Gerenciador de Expressões construirá um nome padrão usando o prefixo e o nome local da função.
   1. **Descrição**: Uma descrição detalhada da função. Essa descrição é usada para fins de exibição na interface do usuário de criação. Se estiver vazio, o Gerenciador de Expressões construirá uma descrição padrão usando o prefixo e o nome local da função.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   Os parâmetros dos métodos também podem ser anotados opcionalmente usando a anotação @ServiceMethodParameter (com.adobe.exm.exm.exval.ServiceMethodParameter). Essa anotação é usada apenas para especificar nomes legíveis por humanos e descrições de parâmetros de métodos para uso na interface do usuário de criação. Verifique se os parâmetros e valores de retorno dos métodos de interface pertencem a um dos seguintes tipos:

   * java.lang.String
   * java.lang.Character
   * Carro
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

A entrada exm.service=true instrui o gerenciador de Expressões de que o serviço contém funções remotas adequadas para uso no expressão. O valor &lt;service_id> deve ser um identificador Java válido (alfanumérico,$, _ sem outros caracteres especiais). Esse valor, prefixado com a palavra-chave REMOTE_, forma o prefixo usado no expressão. Por exemplo, uma interface com um método anotado bar() e a ID do serviço para nas propriedades do serviço podem ser referenciadas no expressão usando REMOTE_foo:bar().

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

* **GoodFunctions.jar.zip** é o arquivo jar com um pacote que contém uma amostra de definição de função remota. Baixe o arquivo GoodFunctions.jar.zip e descompacte-o para obter o arquivo jar.
* **GoodFunctions.zip** é o pacote de código fonte para definir uma função remota personalizada e criar um pacote para ela.

GoodFunctions.jar.zip

[Obter arquivo](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Obter arquivo](assets/goodfunctions.zip)
