---
title: Dicas de codificação
seo-title: Coding Tips
description: Dicas para codificação de AEM
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Dicas de codificação{#coding-tips}

## Use taglibs ou HTL o máximo possível {#use-taglibs-or-htl-as-much-as-possible}

A inclusão de scriptlets nos JSPs dificulta a depuração de problemas no código. Além disso, ao incluir scripts em JSPs, é difícil separar a lógica de negócios da camada de visualização, o que é uma violação do Princípio de responsabilidade única e do padrão de design MVC.

### Gravar código legível {#write-readable-code}

O código é escrito uma vez, mas é lido muitas vezes. Passar algum tempo na frente para limpar o código que escrevemos vai pagar dividendos pela estrada, já que nós e outros desenvolvedores precisamos lê-lo mais tarde.

### Escolher nomes reveladores de intenção {#choose-intention-revealing-names}

Idealmente, outro programador não deveria ter que abrir um módulo para entender o que ele faz. Da mesma forma, eles devem ser capazes de dizer o que um método faz sem lê-lo. Quanto melhor pudermos subscrever essas ideias, mais fácil será ler nosso código e mais rápido poderemos escrever e alterar nosso código.

Na base de código AEM, as seguintes convenções são usadas:


* Uma única implementação de uma interface é chamada de `<Interface>Impl`, ou seja `ReaderImpl`.
* Várias implementações de uma interface são nomeadas `<Variant><Interface>`, ou seja `JcrReader` e `FileSystemReader`.
* As classes base abstratas são nomeadas `Abstract<Interface>` ou `Abstract<Variant><Interface>`.
* Os pacotes são nomeados `com.adobe.product.module`.  Cada artefato Maven ou pacote OSGi deve ter seu próprio pacote.
* As implementações do Java são colocadas em um pacote impl abaixo de sua API.


Observe que essas convenções não precisam necessariamente ser aplicadas às implementações do cliente, mas é importante que as convenções sejam definidas e cumpridas para que o código possa permanecer mantenível.

Idealmente, os nomes deveriam revelar a intenção. Um teste de código comum para quando os nomes não são tão claros quanto deveriam ser é a presença de comentários explicando para que é a variável ou o método:

<table>
 <tbody>
  <tr>
   <td><p><strong>Não claro</strong></p> </td>
   <td><p><strong>Limpar</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //tempo decorrido em dias</p> </td>
   <td><p>int beenTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get imagens marcadas<br /> lista pública getItems() {}</p> </td>
   <td><p>Lista pública getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### Não se repita  {#don-t-repeat-yourself}

DRY declara que o mesmo conjunto de códigos nunca deve ser duplicado. Isso também se aplica a coisas como literais de string. A duplicação de código abre a porta para defeitos sempre que algo tem que mudar e deve ser procurado e eliminado.

### Evitar regras de CSS nu {#avoid-naked-css-rules}

As regras de CSS devem ser específicas ao elemento de destino no contexto do aplicativo. Por exemplo, uma regra CSS aplicada a *.content .center* seria muito amplo e poderia afetar muito conteúdo em todo o sistema, exigindo que outros substituíssem esse estilo no futuro. *.myapp-centertext* seria uma regra mais específica, pois está especificando centralizado *texto* no contexto do aplicativo.

### Elimine o uso de APIs obsoletas {#eliminate-usage-of-deprecated-apis}

Quando uma API é obsoleta, é sempre melhor encontrar a nova abordagem recomendada em vez de depender da API obsoleta. Isso garantirá atualizações mais suaves no futuro.

### Gravar código localizável {#write-localizable-code}

Qualquer sequência de caracteres que não esteja sendo fornecida por um autor deve ser encapsulada em uma chamada para o dicionário i18n da AEM por meio de *I18n.get()* em JSP/Java e *CQ.I18n.get()* em JavaScript. Essa implementação retornará a sequência de caracteres transmitida a ela se nenhuma implementação for encontrada, de modo que oferece a flexibilidade de implementar a localização após implementar os recursos no idioma principal.

### Evitar caminhos de recursos para segurança {#escape-resource-paths-for-safety}

Embora os caminhos no JCR não devam conter espaços, a presença deles não deve fazer com que o código quebre. Jackrabbit fornece uma classe de utilitário de Texto com *escape()* e *escapePath()* métodos. Para JSPs, a interface do usuário do Granite expõe um *granite:encodeURIPath() EL* .

### Use a API XSS e/ou o HTL para se proteger contra ataques de script entre sites {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

O AEM fornece uma API XSS para limpar parâmetros facilmente e garantir a segurança de ataques de script entre sites. Além disso, o HTL tem essas proteções incorporadas diretamente à linguagem de modelo. Uma planilha de API está disponível para download em [Desenvolvimento - Diretrizes e práticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementar o registro apropriado {#implement-appropriate-logging}

Para código Java, o AEM oferece suporte ao slf4j como a API padrão para mensagens de registro e deve ser usado em conjunto com as configurações disponibilizadas pelo console OSGi por questões de consistência na administração. O Slf4j expõe cinco níveis diferentes de log. Recomendamos usar as seguintes diretrizes ao escolher em qual nível registrar uma mensagem:

* ERRO: Quando algo está quebrado no código, o processamento não pode continuar. Isso frequentemente ocorrerá como resultado de uma exceção inesperada. Geralmente, é útil incluir rastreamentos de pilha nesses cenários.
* AVISO: Quando algo não funcionou corretamente, mas o processamento pode continuar. Isso será frequentemente o resultado de uma exceção que esperávamos, como uma *PathNotFoundException*.
* INFORMAÇÕES: Informações úteis ao monitorar um sistema. Lembre-se de que esse é o padrão e que a maioria dos clientes deixará isso em vigor em seus ambientes. Portanto, não o use excessivamente.
* DEPURAR: Informações de nível inferior sobre processamento. Útil ao depurar um problema com suporte.
* TRACE: As informações de nível mais baixo, como métodos de entrada/saída. Geralmente, isso só será usado por desenvolvedores.

No caso de JavaScript, *console.log* só deve ser usada durante o desenvolvimento e todas as declarações de log devem ser removidas antes do lançamento.

### Evitar a programação do culto de carga {#avoid-cargo-cult-programming}

Evite copiar o código sem entender o que ele faz. Na dúvida, é sempre melhor perguntar a alguém que tem mais experiência com o módulo ou a API que você não está claro.
