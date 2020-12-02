---
title: Modelagem de dados - Modelo de David Nuescheler
seo-title: Modelagem de dados - Modelo de David Nuescheler
description: Recomendações de modelagem de conteúdo de David Nuescheler
seo-description: Recomendações de modelagem de conteúdo de David Nuescheler
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---


# Modelagem de dados - Modelo de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Fonte {#source}

Os detalhes a seguir são ideias e comentários expressos por David Nuescheler.

David foi cofundador e CTO da Day Software AG, um fornecedor líder de software global de gestão de conteúdo e infraestrutura de conteúdo, que foi adquirido pela Adobe em 2010. Ele agora é sócio e vice-presidente de tecnologia empresarial na Adobe e também lidera o desenvolvimento da JSR-170, a API (application programming interface, interface de programação de aplicativos) do repositório de conteúdo Java (JCR), o padrão de tecnologia para a gestões de conteúdo.

Outras atualizações também podem ser vistas em [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introdução de David {#introduction-from-david}

Em várias discussões, descobri que os desenvolvedores estão um pouco inquietos com os recursos e funcionalidades apresentados pelo JCR no que diz respeito à modelagem de conteúdo. Ainda não há guia e pouca experiência sobre como modelar o conteúdo em um repositório e por que um modelo de conteúdo é melhor do que o outro.

Enquanto no mundo relacional a indústria de software tem muita experiência em como modelar dados, ainda estamos nos estágios iniciais para o espaço no repositório de conteúdo.

Gostaria de start para preencher este vazio expressando minhas opiniões pessoais sobre como o conteúdo deve ser modelado, esperando que isso possa algum dia se formar em algo mais significativo para a comunidade de desenvolvedores, que não é apenas &quot;minha opinião&quot;, mas algo que é mais generalizado. Então considerem isto como se evoluíssemos rapidamente, primeiro esfaqueando-os.

>[!NOTE]
>
>Isenção de responsabilidade: Essas diretrizes expressam minhas visualizações pessoais, às vezes controversas. Aguardo com expectativa o debate e o aperfeiçoamento destas orientações.

## Sete regras simples {#seven-simple-rules}

### Regra nº 1: Dados primeiro, estrutura depois. Talvez. {#rule-data-first-structure-later-maybe}

#### Explicação {#explanation-1}

Eu recomendo não me preocupar com uma estrutura de dados declarada em um sentido ERD. Inicialmente.

Aprenda a amar nt:unstructed (&amp; amigos) no desenvolvimento.

Eu acho que Stefano resume bem este.

Meu resultado final: A estrutura é dispendiosa e, em muitos casos, é totalmente desnecessário declarar explicitamente a estrutura ao armazenamento subjacente.

Há um contrato implícito sobre a estrutura que seu aplicativo usa inerentemente. Digamos que eu armazene a data de modificação de uma postagem de blog em uma propriedade lastModifid. Meu aplicativo saberá automaticamente ler a data de modificação dessa mesma propriedade novamente, não há necessidade de declarar isso explicitamente.

Outras restrições de dados, como restrições obrigatórias ou de tipo e valor, só devem ser aplicadas quando necessário por razões de integridade dos dados.

#### Exemplo {#example-1}

O exemplo acima de usar uma propriedade `lastModified` Date em, por exemplo, um nó &quot;postagem de blog&quot;, realmente não significa que haja necessidade de um tipo de nó especial. Definitivamente usaria `nt:unstructured` para meus nós de postagem do blog pelo menos inicialmente. Já que no meu aplicativo de blogue tudo o que vou fazer é mostrar a última data Modificada de qualquer forma (possivelmente &quot;ordene por&quot;) eu mal me importo se é uma Data. Como eu implícita a confiança em meu aplicativo de escrita de blog para colocar uma &quot;data&quot; lá de qualquer forma, não há necessidade de declarar a presença de uma data `lastModified` na forma de um tipo de nó.

### Regra nº 2: Direcione a hierarquia de conteúdo, não deixe que isso aconteça. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explicação {#explanation-2}

A hierarquia de conteúdo é um ativo muito valioso. Então não deixe que isso aconteça, projete-o. Se você não tem um &quot;bom&quot; nome legível para um nó, provavelmente é algo que você deveria reconsiderar. Números arbitrários quase nunca são um &quot;bom nome&quot;.

Embora seja extremamente fácil colocar rapidamente um modelo relacional existente em um modelo hierárquico, é preciso pensar nesse processo.

Na minha experiência, se você pensar em controle de acesso e contenção, geralmente bons drivers para a hierarquia de conteúdo. Pense nisso como se fosse o seu sistema de arquivos. Talvez até use arquivos e pastas para modelá-los no disco local.

Pessoalmente, prefiro as convenções de hierarquia do que o sistema de digitação em muitos casos inicialmente, e introduzo a digitação mais tarde.

>[!CAUTION]
>
>A maneira como um repositório de conteúdo é estruturado também pode afetar o desempenho. Para obter o melhor desempenho, o número de nós secundários conectados a nós individuais em um repositório de conteúdo geralmente não deve exceder 1000.
>
>Consulte [Quantos dados o CRX pode lidar?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) para obter mais informações.

#### Exemplo {#example-2}

Eu modelaria um simples sistema de blogues da seguinte maneira. Por favor, observe que inicialmente eu nem me importo com os respectivos tipos de nós que uso neste momento.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Penso que uma das coisas que se torna evidente é que todos nós entendemos a estrutura do conteúdo com base no exemplo, sem mais explicações.

O que pode ser inesperado inicialmente é por que eu não armazenaria os &quot;comentários&quot; com a &quot;postagem&quot;, que é devido ao controle de acesso que eu gostaria de ser aplicado de forma razoavelmente hierárquica.

Usando o modelo de conteúdo acima, posso permitir que o usuário &quot;anônimo&quot; &quot;crie&quot; comentários, mas manter o usuário anônimo somente leitura para o restante da área de trabalho.

### Regra nº 3: Os espaços de trabalho são para clone(), merge() e update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explicação {#explanation-3}

Se você não usar os métodos `clone()`, `merge()` ou `update()` no seu aplicativo, um único espaço de trabalho provavelmente será o caminho a seguir.

&quot;Nós correspondentes&quot; é um conceito definido na especificação do JCR. Basicamente, ele se resume a nós que representam o mesmo conteúdo, em diferentes chamados espaços de trabalho.

O JCR apresenta o conceito muito abstrato de espaços de trabalho, o que deixa muitos desenvolvedores pouco claros sobre o que fazer com eles. Gostaria de propor que a sua utilização dos espaços de trabalho fosse testada.

Se você tiver uma sobreposição considerável de nós &quot;correspondentes&quot; (essencialmente os nós com a mesma UUID) em vários espaços de trabalho, você provavelmente usará os espaços de trabalho.

Se não houver sobreposição de nós com a mesma UUID, você provavelmente está abusando de espaços de trabalho.

Os espaços de trabalho não devem ser usados para o controle de acesso. A visibilidade do conteúdo para um grupo específico de usuários não é um bom argumento para separar as coisas em diferentes espaços de trabalho. O JCR apresenta &quot;Controle de acesso&quot; no repositório de conteúdo para fornecer isso.

Espaços de trabalho são o limite para referências e query.

#### Exemplo {#example-3}

Use espaços de trabalho para coisas como:

* v1.2 do seu projeto versus a v1.3 do seu projeto
* um &quot;desenvolvimento&quot;, &quot;QA&quot; e um estado &quot;publicado&quot; do conteúdo

Não use espaços de trabalho para coisas como:

* diretórios home do usuário
* conteúdo distinto para audiências de públicos alvos diferentes, como público, privado, local, ...
* caixas de entrada de email para usuários diferentes

### Regra nº 4: Cuidado com irmãos de mesmo nome. {#rule-beware-of-same-name-siblings}

#### Explicação {#explanation-4}

Embora os Irmãos com o mesmo nome (SNS) tenham sido introduzidos nas especificações para permitir a compatibilidade com estruturas de dados projetadas para e expressas por meio de XML e, portanto, extremamente valiosas para o JCR, os SNS apresentam uma grande sobrecarga e complexidade para o repositório.

Qualquer caminho no repositório de conteúdo que contenha um SNS em um de seus segmentos de caminho se torna muito menos estável, se um SNS for removido ou reorganizado, isso terá impacto nos caminhos de todos os outros SNS e seus filhos.

Para a importação de XML ou interação com SNS XML existentes, talvez seja necessário e útil, mas nunca usei SNS, e nunca irei usar meus modelos de dados de &quot;campo verde&quot;.

#### Exemplo {#example-4}

Uso

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

em vez de

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regra nº 5: Referências consideradas prejudiciais. {#rule-references-considered-harmful}

#### Explicação {#explanation-5}

As referências implicam integridade referencial. Eu acho importante entender que as referências não apenas aumentam o custo para o repositório que gerencia a integridade referencial, mas também são caras do ponto de vista da flexibilidade do conteúdo.

Pessoalmente, tenho certeza de que só utilizo referências quando realmente não posso lidar com uma referência em modo de espera e, de outra forma, usar um caminho, um nome ou uma string UUID para fazer referência a outro nó.

#### Exemplo {#example-5}

Vamos supor que eu permita &quot;referências&quot; de um documento (a) a outro documento (b). Se eu modelar essa relação usando propriedades de referência, isso significa que os dois documentos estão vinculados em um nível de repositório. Não é possível exportar/importar o documento a) individualmente, uma vez que o público alvo da propriedade de referência pode não existir. Outras operações, como mesclar, atualizar, restaurar ou clonar, também são afetadas.

Então eu modelaria essas referências como &quot;referências fracas&quot; (no JCR v1.0, isso essencialmente se resume a propriedades de sequência que contêm o uuid do nó do público alvo) ou simplesmente usaria um caminho. Às vezes o caminho é mais significativo para começar.

Eu acho que existem casos de uso em que um sistema realmente não pode funcionar se uma referência está caindo, mas eu simplesmente não consigo encontrar um bom &quot;real&quot; mas simples exemplo de minha experiência direta.

### Regra nº 6: Os arquivos são arquivos. {#rule-files-are-files}

#### Explicação {#explanation-6}

Se um modelo de conteúdo expor algo que até mesmo remotamente *cheira* como um arquivo ou uma pasta que tento usar (ou a partir de) `nt:file`, `nt:folder` e `nt:resource`.

Em minha experiência, muitos aplicativos genéricos permitem a interação com nt:folder e nt:files implicitamente e sabem como manipular e exibir esses eventos se estiverem enriquecidos com metadados adicionais. Por exemplo, uma interação direta com implementações de servidor de arquivos como CIFS ou WebDAV sentados sobre o JCR torna-se implícita.

Penso que, como regra geral, poderíamos usar o seguinte: Se você precisar armazenar o nome do arquivo e o tipo MIME, `nt:file`/ `nt:resource` será uma correspondência muito boa. Se você puder ter vários &quot;arquivos&quot; e nt:folder é um bom local para armazená-los.

Se você precisar adicionar informações meta para seu recurso, digamos uma propriedade &quot;autor&quot; ou &quot;descrição&quot;, estenda `nt:resource` não `nt:file`. Eu raramente estendo nt:file e estendo frequentemente `nt:resource`.

#### Exemplo {#example-6}

Vamos supor que alguém gostaria de carregar uma imagem para uma entrada de blog em:

```xml
/content/myblog/posts/iphone_shipping
```

e talvez a reação inicial do intestino seja adicionar uma propriedade binária contendo a imagem.

Embora haja casos de bom uso para usar apenas uma propriedade binária (digamos que o nome seja irrelevante e o mime-type esteja implícito) nesse caso, eu recomendaria a seguinte estrutura para o meu exemplo de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regra nº 7: As IDs são más. {#rule-ids-are-evil}

#### Explicação {#explanation-7}

Em bancos de dados relacionais, as IDs são um meio necessário para expressar relações, de modo que as pessoas tendem a usá-las em modelos de conteúdo também. Principalmente pelas razões erradas.

Se o modelo de conteúdo estiver cheio de propriedades que terminam em &quot;Id&quot;, provavelmente você não está aproveitando a hierarquia corretamente.

É verdade que alguns nós precisam de uma identificação estável durante todo o seu ciclo de vida. Muito menos do que você poderia pensar. mix:referenciável fornece um mecanismo desse tipo integrado no repositório, de modo que não há necessidade de encontrar um meio adicional de identificar um nó de forma estável.

Lembre-se também de que os itens podem ser identificados por caminho, e tanto quanto &quot;links simbólicos&quot; façam mais sentido para a maioria dos usuários do que os links rígidos em um sistema de arquivos unix, um caminho faz sentido para a maioria dos aplicativos se referirem a um nó de público alvo.

Mais importante, é **mix**:referenciável, o que significa que pode ser aplicado a um nó no momento em que você realmente precisa referenciá-lo.

Portanto, digamos que apenas porque você gostaria de ser capaz de fazer referência a um nó do tipo &quot;Documento&quot; não significa que seu tipo de nó &quot;Documento&quot; tenha que se estender de mix:referenciável de forma estática, já que ele pode ser adicionado a qualquer instância do &quot;Documento&quot; dinamicamente.

#### Exemplo {#example-7}

Uso:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

em vez de:

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```

