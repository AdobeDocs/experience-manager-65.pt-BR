---
title: Dicas de codificação
description: Dicas para codificar AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Dicas de codificação{#coding-tips}

## Use taglibs ou HTL o máximo possível {#use-taglibs-or-htl-as-much-as-possible}

A inclusão de scriptlets em JSPs dificulta a depuração de problemas no código. Além disso, ao incluir scriptlets em JSPs, é difícil separar a lógica de negócios da camada de exibição, o que é uma violação do Princípio de Responsabilidade Única e do padrão de design do MVC.

### Gravar código legível {#write-readable-code}

O código é gravado uma vez, mas lido várias vezes. Gastar algum tempo antes para limpar o código escrito paga dividendos adiante à medida que você e outros desenvolvedores o leem mais tarde.

### Escolher nomes reveladores de intenção {#choose-intention-revealing-names}

Idealmente, outro programador não deve ter que abrir um módulo para entender o que ele faz. Da mesma forma, eles devem ser capazes de dizer o que um método faz sem lê-lo. Quanto melhor você se inscrever nessas ideias, mais fácil será ler o código e mais rápido poderá escrever e alterar o código.

Na base de código AEM, as seguintes convenções são usadas:


* Uma única implementação de uma interface é chamada de `<Interface>Impl`, ou seja, `ReaderImpl`.
* Várias implementações de uma interface são nomeadas como `<Variant><Interface>`, ou seja, `JcrReader` e `FileSystemReader`.
* As classes base abstratas são nomeadas `Abstract<Interface>` ou `Abstract<Variant><Interface>`.
* Os pacotes são nomeados `com.adobe.product.module`. Cada artefato Maven ou pacote OSGi deve ter seu próprio pacote.
* As implementações do Java™ são colocadas em um pacote impl abaixo da API.


Essas convenções não se aplicam necessariamente às implementações do cliente, mas é importante que elas sejam definidas e seguidas para que o código possa ser mantido.

Idealmente, os nomes devem revelar sua intenção. Um teste de código comum para quando os nomes não são tão claros quanto deveriam ser é a presença de comentários explicando para que serve a variável ou o método:

<table>
 <tbody>
  <tr>
   <td><p><strong>Não claro</strong></p> </td>
   <td><p><strong>Limpar</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //tempo decorrido em dias</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> getItems() de Lista pública {}</p> </td>
   <td><p>lista pública getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### Não se repita  {#don-t-repeat-yourself}

DRY indica que o mesmo conjunto de códigos nunca deve ser duplicado. Isso também se aplica a coisas como literais de string. A duplicação de código abre a porta para defeitos sempre que algo precisa mudar e deve ser buscado e eliminado.

### Evitar regras CSS nuas {#avoid-naked-css-rules}

As regras CSS devem ser específicas para o elemento de destino no contexto do aplicativo. Por exemplo, uma regra CSS aplicada a *.content .center* seria muito abrangente e poderia potencialmente acabar afetando muitos conteúdos em seu sistema, exigindo que outros substituíssem esse estilo no futuro. Considerando que *.myapp-centertext* seria uma regra mais específica, uma vez que especifica os *texto* no contexto do aplicativo.

### Eliminar o uso de APIs obsoletas {#eliminate-usage-of-deprecated-apis}

Quando uma API é descontinuada, é sempre melhor encontrar a nova abordagem recomendada em vez de depender da API descontinuada. Isso garantirá atualizações mais tranquilas no futuro.

### Gravar código localizável {#write-localizable-code}

Qualquer string que não estiver sendo fornecida por um autor deve ser encapsulada em uma chamada para o dicionário AEM i18n por meio de *I18n.get()* em JSP/Java e *CQ.I18n.get()* no JavaScript. Essa implementação retornará a string passada para ela se nenhuma implementação for encontrada, portanto, oferece a flexibilidade de implementar a localização após implementar os recursos no idioma principal.

### Evitar caminhos de recursos para segurança {#escape-resource-paths-for-safety}

Embora os caminhos no JCR não devam conter espaços, a presença deles não deve causar a quebra do código. O Jackrabbit fornece uma classe de utilitário de texto com *escape()* e *escapePath()* métodos. Para JSPs, a interface do usuário do Granite expõe uma *granite:encodeURIPath() EL* função.

### Usar a API XSS e/ou o HTL para proteger contra ataques de script entre sites {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

O AEM fornece uma API XSS para limpar facilmente os parâmetros e garantir a segurança contra ataques de script entre sites. Além disso, o HTL tem essas proteções incorporadas diretamente na linguagem de modelo. Uma folha de características da API está disponível para download em [Desenvolvimento - diretrizes e práticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementar o registro apropriado {#implement-appropriate-logging}

Para o código Java™, o AEM é compatível com o slf4j como a API padrão para mensagens de registro e deve ser usado com as configurações disponibilizadas pelo console OSGi para fins de consistência na administração. O Slf4j expõe cinco níveis de log diferentes. O Adobe recomenda usar as seguintes diretrizes ao escolher em qual nível registrar uma mensagem:

* ERRO: quando algo está com defeito no código, o processamento não pode continuar. Isso frequentemente ocorrerá como resultado de uma exceção inesperada. É útil incluir rastreamentos de pilha nesses cenários.
* AVISO: quando algo não funcionou corretamente, mas o processamento pode continuar. Isso será frequentemente o resultado de uma exceção que esperávamos, como uma *PathNotFoundException*.
* INFO: informações que seriam úteis ao monitorar um sistema. Lembre-se de que esse é o padrão e que a maioria dos clientes deixará isso em vigor em seus ambientes. Portanto, não o use excessivamente.
* DEBUG: Informações de nível inferior sobre processamento. Útil ao depurar um problema com suporte.
* TRACE: As informações de nível mais baixo, como métodos de entrada/saída. Normalmente, isso só será usado por desenvolvedores.

No caso do JavaScript, *console.log* O só deve ser usado durante o desenvolvimento e todas as instruções de log devem ser removidas antes da versão.

### Evite programação cult de carga {#avoid-cargo-cult-programming}

Evite copiar o código sem entender seu funcionamento. Em caso de dúvida, é sempre melhor perguntar a alguém que tem mais experiência com o módulo ou a API que você não sabe ao certo.
