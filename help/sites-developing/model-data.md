---
title: Modelagem de dados - Modelo de David Nuescheler
description: Recomendações de modelagem de conteúdo de David Nuescheler
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# Modelagem de dados - Modelo de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Origem {#source}

Os detalhes a seguir são ideias e comentários expressos por David Nuescheler.

David foi cofundador e CTO da Day Software AG, líder no fornecimento de software global de gerenciamento de conteúdo e infraestrutura de conteúdo, adquirido pela Adobe em 2010. Agora David é bolsista e VP de Tecnologia Empresarial na Adobe e também lidera o desenvolvimento da JSR-170, a API (Application Programming Interface, interface de programação de aplicativo) do Java™ Content Repository (JCR), o padrão de tecnologia para gerenciamento de conteúdo.

Outras atualizações também podem ser vistas em [https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel](https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel).

## Introdução do David {#introduction-from-david}

Em várias discussões, descobri que os desenvolvedores estão um pouco desconfortáveis com os recursos e funcionalidades apresentados pelo JCR na modelagem de conteúdo. Ainda não há guia e pouca experiência sobre como modelar conteúdo em um repositório e por que um modelo de conteúdo é melhor que o outro.

Enquanto no mundo relacional, o setor de software tem experiência em como modelar dados, ele ainda está nos estágios iniciais do espaço de repositório de conteúdo.

Gostaria de começar a preencher este vazio expressando minhas opiniões sobre como o conteúdo deve ser modelado. Minha esperança é que isso possa algum dia se formar em algo mais significativo para a comunidade de desenvolvedores, que não seja apenas &quot;minha opinião&quot;, mas algo que seja mais aplicável em geral. Então considerem isso como minha primeira facada em rápida evolução.

>[!NOTE]
>
>Aviso: essas diretrizes expressam minhas visões pessoais, às vezes controversas. Aguardo com expectativa a oportunidade de debater estas orientações e de as aperfeiçoar.

## Sete regras simples {#seven-simple-rules}

### Regra #1: Dados primeiro, estrutura depois. Talvez. {#rule-data-first-structure-later-maybe}

#### Explicação {#explanation-1}

Recomendo não me preocupar com uma estrutura de dados declarada no sentido da ERD. Inicialmente.

Aprenda a amar nt:unstructured (&amp; amigos) em desenvolvimento.

Meu resultado final: a estrutura é cara e muitas vezes é totalmente desnecessária declarar explicitamente a estrutura para o armazenamento subjacente.

Há um contrato implícito sobre a estrutura que seu aplicativo usa inerentemente. Digamos que eu armazene a data de modificação de uma publicação do blog em uma propriedade lastModified. Meu aplicativo sabe automaticamente para ler a data de modificação a partir dessa mesma propriedade novamente, não há realmente necessidade de declarar isso explicitamente.

Outras restrições de dados, como restrições obrigatórias ou restrições de tipo e valor, só devem ser aplicadas quando necessário por motivos de integridade dos dados.

#### Exemplo {#example-1}

O exemplo acima de uso de um `lastModified` A propriedade Date, por exemplo, no nó &quot;publicação do blog&quot;, não significa que haja necessidade de um tipo de nó especial. Eu definitivamente usaria `nt:unstructured` para os nós de postagem de blog, pelo menos inicialmente. Como no meu aplicativo de blog, tudo o que vou fazer é exibir a última data modificada de qualquer maneira (possivelmente &quot;pedir por&quot;), mal me importo se é uma data. Como eu implicitamente confio em meu aplicativo de escrita de blog para colocar uma &quot;data&quot; lá de qualquer maneira, realmente não há necessidade de declarar a presença de um `lastModified` de um tipo de nó.

### Regra #2: Direcione a hierarquia de conteúdo; não deixe que isso aconteça. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explicação {#explanation-2}

A hierarquia de conteúdo é um ativo valioso. Não deixe que isso aconteça; desenhe-o. Se você não tiver um nome &quot;bom&quot; em formato legível por humanos para um nó, isso provavelmente é algo que você deve reconsiderar. Números arbitrários dificilmente são um &quot;bom nome&quot;.

Embora possa ser fácil colocar rapidamente um modelo relacional existente em um modelo hierárquico, deve-se colocar algum pensamento nesse processo.

Em minha experiência, se você pensar em controle de acesso e contenção como bons drivers para a hierarquia de conteúdo. Pense nisso como se fosse seu sistema de arquivos. Talvez até use arquivos e pastas para modelá-lo em seu disco local.

Pessoalmente, prefiro convenções de hierarquia em vez do sistema de digitação de nó inicialmente e introduzo a digitação mais tarde.

>[!CAUTION]
>
>A forma como um repositório de conteúdo é estruturado também pode afetar o desempenho. Para obter o melhor desempenho, o número de nós secundários anexados a nós individuais em um repositório de conteúdo não deve exceder 1.000.
>
>Consulte [Quantos dados o CRX pode manipular?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html)

#### Exemplo {#example-2}

Eu modelaria um simples sistema de blogues da seguinte maneira. Inicialmente, eu nem me importo com os respectivos tipos de nó que eu uso neste momento.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Acho que uma das coisas que se torna evidente é que a estrutura do conteúdo é entendida com base no exemplo, sem maiores explicações.

O que pode ser inesperado inicialmente é por que eu não armazenaria os &quot;comentários&quot; com o &quot;post&quot;, que é devido ao controle de acesso que eu gostaria de ser aplicado de uma forma razoavelmente hierárquica.

Usando o modelo de conteúdo acima, posso permitir facilmente que o usuário &quot;anônimo&quot; &quot;crie&quot; comentários, mas manter o usuário anônimo em uma base somente leitura para o restante do espaço de trabalho.

### Regra #3: os espaços de trabalho são para clone(), merge() e update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explicação {#explanation-3}

Se você não usar `clone()`, `merge()` ou `update()` métodos em seu aplicativo, um único espaço de trabalho é provavelmente o caminho a seguir.

&quot;Nós correspondentes&quot; é um conceito definido na especificação do JCR. Basicamente, ela se resume a nós que representam o mesmo conteúdo, em diferentes espaços de trabalho chamados de.

O JCR introduz o conceito abstrato de espaços de trabalho, o que deixa muitos desenvolvedores sem clareza sobre o que fazer com eles. Gostaria de propor que você use os espaços de trabalho para testar o seguinte.

Se você tiver uma sobreposição considerável de nós &quot;correspondentes&quot; (essencialmente os nós com a mesma UUID) em vários espaços de trabalho, você provavelmente colocará os espaços de trabalho em bom uso.

Se não houver sobreposição de nós com a mesma UUID, você provavelmente está usando workspaces.

Não use espaços de trabalho para controle de acesso. A visibilidade do conteúdo para um grupo específico de usuários não é um bom argumento para separar itens em espaços de trabalho diferentes. O JCR apresenta o &quot;Controle de acesso&quot; no repositório de conteúdo para permitir isso.

Os espaços de trabalho são os limites de referências e consultas.

#### Exemplo {#example-3}

Use espaços de trabalho para coisas como:

* v1.2 do seu projeto versus v1.3 do seu projeto
* um estado de conteúdo &quot;desenvolvimento&quot;, &quot;QA&quot; e &quot;publicado&quot;

Não use espaços de trabalho para coisas como:

* diretórios iniciais de usuário
* conteúdo distinto para públicos-alvo diferentes, como público, privado, local etc.
* caixas de entrada de e-mail para usuários diferentes

### Regra #4: Cuidado com irmãos de mesmo nome. {#rule-beware-of-same-name-siblings}

#### Explicação {#explanation-4}

O Same Name Irmãos (SNS) foi introduzido na especificação para permitir compatibilidade com estruturas de dados projetadas para e expressas por XML e, portanto, são valiosas para JCR. No entanto, o SNS vem com sobrecarga e complexidade para o repositório.

Qualquer caminho no repositório de conteúdo que contenha um SNS em um de seus segmentos de caminho se torna muito menos estável. Se um SNS for removido ou reordenado, ele terá um impacto nos caminhos de todos os outros SNS e seus filhos.

Para importação de XML ou interação com XML existente, o SNS pode ser necessário e útil, mas nunca usei o SNS (e nunca pretendo usá-lo) em meus modelos de dados de &quot;campo verde&quot;.

#### Exemplo {#example-4}

Utilização

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

Em vez de

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regra #5: As referências são consideradas prejudiciais. {#rule-references-considered-harmful}

#### Explicação {#explanation-5}

As referências implicam integridade referencial. É importante entender que as referências não apenas adicionam um custo adicional ao repositório que gerencia a integridade referencial, mas também são caras do ponto de vista da flexibilidade do conteúdo.

Pessoalmente, sempre uso referências quando realmente não consigo lidar com uma referência pendente e, de outra forma, uso um caminho, um nome ou uma UUID de sequência para fazer referência a outro nó.

#### Exemplo {#example-5}

Vamos supor que eu permita &quot;referências&quot; de um documento (a) para outro documento (b). Se eu modelar essa relação usando propriedades de referência, significa que os dois documentos estão vinculados no nível do repositório. Não consigo exportar/importar o documento (a) individualmente, pois o destino da propriedade de referência pode não existir. Outras operações como mesclagem, atualização, restauração ou clone também são afetadas.

Portanto, eu modelaria essas referências como &quot;referências fracas&quot; (no JCR v1.0, isso essencialmente se resume a propriedades de string que contêm o uuid do nó de destino) ou simplesmente usaria um caminho. Às vezes, o caminho é mais significativo para começar.

Eu acho que há casos de uso em que um sistema realmente não pode funcionar se uma referência é pendente, mas eu simplesmente não posso vir com um bom &quot;real&quot;, mas exemplo simples da minha experiência direta.

### Regra #6: Arquivos são arquivos. {#rule-files-are-files}

#### Explicação {#explanation-6}

Se um modelo de conteúdo expor algo que até mesmo cheira remotamente como um arquivo ou uma pasta, tento usar (ou estender de) `nt:file`, `nt:folder`, e `nt:resource`.

Em minha experiência, muitos aplicativos genéricos permitem a interação implícita com nt:folder e nt:files e sabem como lidar e exibir esses eventos se eles forem enriquecidos com metainformações adicionais. Por exemplo, uma interação direta com implementações de servidor de arquivos como CIF ou WebDAV que assenta sobre o JCR fica implícita.

Eu acho que como regra geral um poderia usar o seguinte: Se você deve armazenar o nome do arquivo e o tipo MIME então `nt:file`/ `nt:resource` O é um bom jogo. Se você tiver vários &quot;arquivos&quot;, nt:folder é um bom lugar para armazená-los.

Se você precisar adicionar informações meta para seu recurso, digamos uma propriedade &quot;author&quot; ou &quot;description&quot;, estenda `nt:resource` não o `nt:file`. Raramente estendo nt:file e estendo com frequência `nt:resource`.

#### Exemplo {#example-6}

Vamos supor que alguém gostaria de fazer upload de uma imagem para uma entrada de blog em:

```xml
/content/myblog/posts/iphone_shipping
```

E talvez a reação inicial seria adicionar uma propriedade binária contendo a figura.

Embora existam bons casos de uso para usar apenas uma propriedade binária (digamos que o nome seja irrelevante e o tipo MIME esteja implícito), neste caso, recomendo a seguinte estrutura para meu exemplo de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regra #7: As IDs são más. {#rule-ids-are-evil}

#### Explicação {#explanation-7}

Em bancos de dados relacionais, as IDs são um meio necessário para expressar relações, portanto, as pessoas tendem a usá-las em modelos de conteúdo também. Principalmente pelas razões erradas.

Se o modelo de conteúdo estiver cheio de propriedades que terminam em &quot;Id&quot;, é provável que você não esteja usando a hierarquia corretamente.

É verdade que alguns nós precisam de uma identificação estável ao longo de seu ciclo de vida; menos do que você pode pensar. Mas `mix:referenceable` O tem esse mecanismo integrado no repositório, de modo que não há necessidade de criar um meio adicional de identificar um nó de maneira estável.

Lembre-se também de que os itens podem ser identificados por caminho. E, na medida em que os &quot;symlinks&quot; são mais adequados para a maioria dos usuários do que os links físicos em um sistema de arquivos UNIX®, um caminho faz sentido para que a maioria dos aplicativos se refira a um nó de destino.

Mais importante ainda, é **mix**:referenceable, o que significa que ele pode ser aplicado a um nó no momento em que você realmente deve referenciá-lo.

Portanto, apenas porque você gostaria de poder fazer referência a um nó do tipo &quot;Documento&quot;, não significa que o tipo de nó &quot;Documento&quot; tenha que se estender de `mix:referenceable` de forma estática. Isso ocorre porque ele pode ser adicionado dinamicamente a qualquer instância do &quot;Documento&quot;.

#### Exemplo {#example-7}

Uso:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

Em vez de:

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
