---
title: Dicas de codificação
seo-title: Dicas de codificação
description: Dicas para codificação do AEM
seo-description: Dicas para codificação do AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Dicas de codificação{#coding-tips}

## Use taglibs ou HTL o máximo possível {#use-taglibs-or-htl-as-much-as-possible}

A inclusão de scriptlets em JSPs dificulta a depuração de problemas no código. Além disso, ao incluir scripts em JSPs, é difícil separar a lógica comercial da camada de visualização, o que é uma violação do Princípio de Responsabilidade Única e do padrão de design MVC.

### Gravar código legível {#write-readable-code}

O código é escrito uma vez, mas lido muitas vezes. Gastar algum tempo antes para limpar o código que escrevemos vai pagar dividendos pela estrada enquanto nós e outros desenvolvedores precisamos lê-lo mais tarde.

### Escolher nomes reveladores de intenção {#choose-intention-revealing-names}

O ideal é que outro programador não tenha que abrir um módulo para entender o que ele faz. Do mesmo modo, eles deveriam ser capazes de dizer o que um método faz sem lê-lo. Quanto melhor pudermos assinar essas ideias, mais fácil será a leitura de nosso código e mais rápido seremos capazes de escrever e mudar nosso código.

Na base de código do AEM, as seguintes convenções são usadas:


* Uma única implementação de uma interface é nomeada `<Interface>Impl`, isto é, `ReaderImpl`.
* Várias implementações de uma interface são nomeadas `<Variant><Interface>`, ou seja, `JcrReader` e `FileSystemReader`.
* Classes base abstratas são nomeadas `Abstract<Interface>` ou `Abstract<Variant><Interface>`.
* Os pacotes são nomeados `com.adobe.product.module`.  Cada artefato Maven ou pacote OSGi deve ter seu próprio pacote.
* As implementações Java são colocadas em um pacote impl abaixo de sua API.


Observe que essas convenções não precisam necessariamente ser aplicadas às implementações do cliente, mas é importante que as convenções sejam definidas e aplicadas para que o código possa permanecer preservável.

O ideal é que os nomes revelem a sua intenção. Um teste de código comum para quando os nomes não são tão claros quanto deveriam ser é a presença de comentários explicando para que serve a variável ou o método:

<table>
 <tbody>
  <tr>
   <td><p><strong>Não limpo</strong></p> </td>
   <td><p><strong>Limpar</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //tempo decorrido em dias</p> </td>
   <td><p>int eternedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get imagens<br /> marcadas Lista pública getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {0}</p> </td>
  </tr>
 </tbody>
</table>

### Não se repita {#don-t-repeat-yourself}

DRY indica que o mesmo conjunto de códigos nunca deve ser duplicado. Isso também se aplica a coisas como literais de cordas. A duplicação de código abre a porta para defeitos sempre que algo tem que mudar e deve ser procurado e eliminado.

### Evitar regras de CSS nu {#avoid-naked-css-rules}

As regras de CSS devem ser específicas ao elemento de destino no contexto do aplicativo. Por exemplo, uma regra de CSS aplicada a *.content.center* seria excessivamente ampla e poderia causar impacto em um monte de conteúdo no sistema, exigindo que outras pessoas substituíssem esse estilo no futuro. *.myapp-centertext* seria uma regra mais específica, pois está especificando *texto* centralizado no contexto do aplicativo.

### Eliminar o uso de APIs obsoletas {#eliminate-usage-of-deprecated-apis}

Quando uma API está obsoleta, é sempre melhor encontrar a nova abordagem recomendada em vez de depender da API obsoleta. Isso garantirá upgrades mais suaves no futuro.

### Gravar código localizável {#write-localizable-code}

Quaisquer strings que não estejam sendo fornecidas por um autor devem ser vinculadas em uma chamada para o dicionário i18n do AEM por meio de *I18n.get()* em JSP/Java e *CQ.I18n.get()* no JavaScript. Essa implementação retornará a sequência de caracteres transmitida a ela se nenhuma implementação for encontrada, de modo que isso oferece a flexibilidade de implementar a localização após implementar os recursos no idioma principal.

### Escapar caminhos de recursos para segurança {#escape-resource-paths-for-safety}

Embora os caminhos no JCR não devam conter espaços, a presença deles não deve fazer com que o código quebre. Jackrabbit fornece uma classe de utilitário de Texto com métodos *escape()* e *escapePath()* . Para JSPs, a interface do usuário Granite expõe uma função EL ** granite:encodeURIPath().

### Use a API XSS e/ou HTL para proteger contra ataques de script entre sites {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

O AEM fornece uma API XSS para limpar parâmetros facilmente e garantir a segurança contra ataques de script entre sites. Além disso, o HTL tem essas proteções incorporadas diretamente à linguagem de modelo. Uma planilha de API está disponível para download em [Desenvolvimento - Diretrizes e Práticas](/help/sites-developing/dev-guidelines-bestpractices.md)recomendadas.

### Implemente o registro adequado {#implement-appropriate-logging}

Para código Java, o AEM oferece suporte a slf4j como a API padrão para mensagens de registro e deve ser usado em conjunto com as configurações disponibilizadas pelo console do OSGi para garantir a consistência na administração. O Slf4j expõe cinco níveis diferentes de log. Recomendamos usar as seguintes diretrizes ao escolher o nível em que registrar uma mensagem:

* ERRO: Quando algo está quebrado no código e o processamento não pode continuar. Isso geralmente ocorre como resultado de uma exceção inesperada. Geralmente, é útil incluir rastreamentos de pilha nesses cenários.
* AVISO: Quando algo não funcionou corretamente, mas o processamento pode continuar. Isso frequentemente resultará de uma exceção que esperávamos, como *PathNotFoundException*.
* INFORMAÇÕES: Informações úteis ao monitorar um sistema. Lembre-se de que esse é o padrão e que a maioria dos clientes deixará isso em vigor em seus ambientes. Portanto, não o utilize excessivamente.
* DEPURAÇÃO: Informações de nível mais baixo sobre o processamento. Útil ao depurar um problema com o suporte.
* TRACE: As informações de nível mais baixo, como métodos de entrada/saída. Normalmente, isso só será usado por desenvolvedores.

No caso do JavaScript, o *console.log* deve ser usado somente durante o desenvolvimento e todas as declarações de log devem ser removidas antes da versão.

### Evitar programação de cultos de carga {#avoid-cargo-cult-programming}

Evite copiar o código sem entender o que ele faz. Na dúvida, é sempre melhor perguntar a alguém que tenha mais experiência com o módulo ou a API que você não está claro.
