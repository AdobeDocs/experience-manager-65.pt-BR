---
title: Modelagem de Dados - Modelo de David Nuescheler
seo-title: Data Modeling - David Nuescheler's Model
description: Recomendações para a modelagem de conteúdo de David Nuescheler
seo-description: David Nuescheler's content modelling recommendations
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 0%

---

# Modelagem de Dados - Modelo de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Origem {#source}

Os detalhes a seguir são ideias e comentários expressos por David Nuescheler.

David foi cofundador e cofundador do Day Software AG, um provedor líder de software global de gerenciamento de conteúdo e infraestrutura de conteúdo, que foi adquirido pela Adobe em 2010. Ele agora é colega e vice-presidente da Enterprise Technology no Adobe e também lidera o desenvolvimento da JSR-170, a API (Java Content Repository, interface de programação de aplicativos) do Java Content Repository (JCR), o padrão de tecnologia para o gerenciamento de conteúdo.

Outras atualizações também podem ser vistas em [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introdução de David {#introduction-from-david}

Em várias discussões, descobri que os desenvolvedores estão um pouco tranquilos com os recursos e funcionalidades apresentados pelo JCR no que diz respeito à modelagem de conteúdo. Ainda não há guia e pouca experiência sobre como modelar o conteúdo em um repositório e por que um modelo de conteúdo é melhor do que o outro.

Embora no mundo relacional, o setor de software tenha muita experiência em como modelar dados, ainda estamos nos estágios iniciais do espaço do repositório de conteúdo.

Gostaria de começar a preencher este vazio, expressando as minhas opiniões pessoais sobre a forma como o conteúdo deve ser modelado, na esperança de que isso possa algum dia formar algo mais significativo para a comunidade de desenvolvedores, o que não é apenas uma &quot;minha opinião&quot;, mas algo que é mais generalizado. Então considere isto como o primeiro passo que evolui rapidamente.

>[!NOTE]
>
>Isenção de responsabilidade: Estas orientações exprimem as minhas opiniões pessoais, por vezes controversas. Aguardo com expectativa a oportunidade de debater estas orientações e de as aperfeiçoar.

## Sete Regras Simples {#seven-simple-rules}

### Regra nº 1: Primeiro, os dados são estruturados posteriormente. Talvez. {#rule-data-first-structure-later-maybe}

#### Explicação {#explanation-1}

Eu recomendo não me preocupar com uma estrutura de dados declarada em um sentido ERD. Inicialmente.

Aprenda a amar o nt:unstructured (&amp; friends) no desenvolvimento.

Eu acho que Stefano resume bem este.

Meu resultado final: A estrutura é cara e, em muitos casos, é totalmente desnecessário declarar explicitamente a estrutura para o armazenamento subjacente.

Há um contrato implícito sobre a estrutura que seu aplicativo usa inerentemente. Digamos que eu armazene a data de modificação de uma publicação do blog em uma propriedade lastModified . Meu aplicativo saberá automaticamente ler a data de modificação dessa mesma propriedade novamente. Não há necessidade de declarar isso explicitamente.

Outras restrições de dados, como restrições obrigatórias ou de tipo e valor, só devem ser aplicadas quando necessário por motivos de integridade dos dados.

#### Exemplo {#example-1}

O exemplo acima de usar um `lastModified` A propriedade Date no, por exemplo, nó &quot;publicação de blog&quot;, não significa que haja necessidade de um tipo de nó especial. Eu definitivamente usaria `nt:unstructured` para os nós de postagem do meu blog pelo menos inicialmente. Já que no meu aplicativo de blogues tudo o que vou fazer é exibir a última data Modificada de qualquer maneira (possivelmente &quot;ordenar por&quot;) eu mal me importo se é uma Data. Como eu implicitamente confio em meu aplicativo de escrita de blog para colocar uma &quot;data&quot; lá de qualquer maneira, não há necessidade de declarar a presença de um `lastModified` no formulário a do tipo de nó.

### Regra nº 2: Direcione a hierarquia de conteúdo, não deixe que isso aconteça. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explicação {#explanation-2}

A hierarquia de conteúdo é um ativo muito valioso. Então não deixe que isso aconteça, crie. Se você não tem um &quot;bom&quot; nome legível por humanos para um nó, provavelmente é algo que você deveria reconsiderar. Os números arbitrários raramente são um &quot;bom nome&quot;.

Embora possa ser extremamente fácil colocar rapidamente um modelo relacional existente num modelo hierárquico, deve-se pensar um pouco nesse processo.

Na minha experiência, se você pensar no controle de acesso e na contenção, geralmente bons drivers para a hierarquia de conteúdo. Pense nisso como se fosse seu sistema de arquivos. Talvez até use arquivos e pastas para modelá-los em seu disco local.

Pessoalmente, prefiro as convenções de hierarquia do que o sistema de datilografia de nó em muitos casos inicialmente, e introduzo a datilografia mais tarde.

>[!CAUTION]
>
>A maneira como um repositório de conteúdo é estruturado também pode afetar o desempenho. Para melhor desempenho, o número de nós filhos anexados a nós individuais em um repositório de conteúdo geralmente não deve exceder 1.000.
>
>Consulte [Quantos dados o CRX pode manipular?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) para obter mais informações.

#### Exemplo {#example-2}

Eu modelaria um simples sistema de blogues como segue. Por favor, note que inicialmente eu nem me importo com os respectivos tipos de nó que eu uso neste momento.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Penso que uma das coisas que se tornam evidentes é que todos compreendemos a estrutura do conteúdo baseada no exemplo, sem mais explicações.

O que pode ser inesperado inicialmente é por que eu não armazenaria os &quot;comentários&quot; com o &quot;post&quot;, que é devido ao controle de acesso que eu gostaria que fosse aplicado de forma razoavelmente hierárquica.

Usando o modelo de conteúdo acima, posso permitir que o usuário &quot;anônimo&quot; &quot;crie&quot; comentários, mas manter o usuário anônimo em uma base somente leitura para o restante do espaço de trabalho.

### Regra nº 3: Os espaços de trabalho são para clone(), merge() e update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explicação {#explanation-3}

Se você não usar `clone()`, `merge()` ou `update()` métodos no seu aplicativo, um único espaço de trabalho provavelmente é o caminho a seguir.

&quot;Nós correspondentes&quot; é um conceito definido na especificação do JCR. Basicamente, ele se resume a nós que representam o mesmo conteúdo, em diferentes espaços de trabalho chamados .

O JCR apresenta o conceito muito abstrato de espaços de trabalho, o que deixa muitos desenvolvedores pouco claros sobre o que fazer com eles. Gostaria de propor que se pusesse a sua utilização de espaços de trabalho à prova seguinte.

Se você tiver uma sobreposição considerável de nós &quot;correspondentes&quot; (essencialmente os nós com a mesma UUID) em vários espaços de trabalho, provavelmente você colocará os espaços de trabalho em bom uso.

Se não houver sobreposição de nós com o mesmo UUID, você provavelmente está usando espaços de trabalho.

Os espaços de trabalho não devem ser usados para o controle de acesso. A visibilidade do conteúdo para um grupo específico de usuários não é um bom argumento para separar as coisas em espaços de trabalho diferentes. O JCR apresenta &quot;Controle de acesso&quot; no repositório de conteúdo para fornecer isso.

Espaços de trabalho são o limite para referências e consultas.

#### Exemplo {#example-3}

Use espaços de trabalho para coisas como:

* v1.2 do seu projeto vs. a v1.3 do seu projeto
* um estado de &quot;desenvolvimento&quot;, &quot;controle de qualidade&quot; e &quot;publicado&quot; do conteúdo

Não use espaços de trabalho para coisas como:

* diretórios iniciais do usuário
* conteúdo distinto para públicos-alvo diferentes, como público, privado, local, ...
* caixas de entrada de email para usuários diferentes

### Regra nº 4: Cuidado com irmãos de mesmo nome. {#rule-beware-of-same-name-siblings}

#### Explicação {#explanation-4}

Embora os Irmãos com Mesmo nome (SNS) tenham sido introduzidos na especificação para permitir a compatibilidade com estruturas de dados projetadas para e expressas por meio de XML e, portanto, sejam extremamente valiosas para o JCR, os SNS vêm com uma sobrecarga e complexidade substanciais para o repositório.

Qualquer caminho no repositório de conteúdo que contenha um SNS em um de seus segmentos de caminho se torna muito menos estável, se um SNS for removido ou reorganizado, isso terá impacto nos caminhos de todos os outros SNS e seus filhos.

Para importação de XML ou interação com SNS XML existentes, talvez seja necessário e útil, mas nunca usei SNS, e nunca usarei em meus modelos de dados de &quot;campo verde&quot;.

#### Exemplo {#example-4}

Utilização

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

As referências implicam integridade referencial. Eu acho importante entender que as referências não apenas aumentam o custo para o repositório que gerencia a integridade referencial, mas também são caras do ponto de vista de flexibilidade de conteúdo.

Pessoalmente, tenho certeza de que só uso referências quando realmente não consigo lidar com uma referência perigosa e, de outra forma, usar um caminho, um nome ou um UUID de string para fazer referência a outro nó.

#### Exemplo {#example-5}

Vamos supor que permita &quot;referências&quot; de um documento (a) a outro documento (b). Se eu modelar essa relação usando propriedades de referência, significa que os dois documentos estão vinculados em um nível de repositório. Não consigo exportar/importar documento (a) individualmente, pois o destino da propriedade de referência pode não existir. Outras operações como mesclar, atualizar, restaurar ou clonar também são afetadas.

Assim, eu modelaria essas referências como &quot;referências fracas&quot; (no JCR v1.0, isso basicamente se resume a propriedades de sequência que contêm o uuid do nó de destino) ou simplesmente usaria um caminho. Às vezes, o caminho é mais significativo para começar.

Eu acho que existem casos de uso em que um sistema realmente não pode funcionar se uma referência estiver em perigo, mas eu simplesmente não consigo encontrar um bom exemplo &quot;real&quot; mas simples de minha experiência direta.

### Regra nº 6: Os arquivos são arquivos. {#rule-files-are-files}

#### Explicação {#explanation-6}

Se um modelo de conteúdo expor algo que remotamente *cheiros* como um arquivo ou uma pasta que tento usar (ou estender de) `nt:file`, `nt:folder` e `nt:resource`.

Na minha experiência, muitos aplicativos genéricos permitem a interação com nt:folder e nt:files implicitamente e sabem como lidar e exibir esse evento se forem enriquecidos com informações meta adicionais. Por exemplo, uma interação direta com implementações de servidor de arquivos como CIFS ou WebDAV sentados sobre o JCR torna-se implícita.

Penso que, como regra geral, se pode usar o seguinte: Se precisar armazenar o nome do arquivo e o tipo MIME, `nt:file`/ `nt:resource` é uma correspondência muito boa. Se você puder ter vários &quot;arquivos&quot; e o nt:folder é um bom local para armazená-los.

Se você precisar adicionar metainformações para seu recurso, digamos uma propriedade &quot;author&quot; ou &quot;description&quot;, estenda `nt:resource` não a `nt:file`. Raramente estendi o nt:file e estendi com frequência `nt:resource`.

#### Exemplo {#example-6}

Vamos supor que alguém gostaria de carregar uma imagem em uma entrada de blog em:

```xml
/content/myblog/posts/iphone_shipping
```

e talvez a reação inicial do intestino fosse adicionar uma propriedade binária contendo a imagem.

Embora certamente haja bons casos de uso para usar apenas uma propriedade binária (digamos que o nome seja irrelevante e o tipo MIME esteja implícito), nesse caso, eu recomendaria a seguinte estrutura para o meu exemplo de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regra nº 7: As IDs são más. {#rule-ids-are-evil}

#### Explicação {#explanation-7}

Em bancos de dados relacionais, as IDs são um meio necessário para expressar relações, de modo que as pessoas tendem a usá-las em modelos de conteúdo também. Principalmente pelas razões erradas.

Se o modelo de conteúdo estiver cheio de propriedades que terminam em &quot;Id&quot;, você provavelmente não está aproveitando a hierarquia corretamente.

É verdade que alguns nós precisam de uma identificação estável durante todo o seu ciclo de vida. Muito menos do que você pode pensar. mix:referenceable fornece um mecanismo desse tipo integrado no repositório, de modo que não há necessidade de criar um meio adicional de identificar um nó de maneira estável.

Lembre-se também de que os itens podem ser identificados por caminho e, tanto quanto os &quot;links simbólicos&quot; fizerem mais sentido para a maioria dos usuários do que os links rígidos em um sistema de arquivos unix, um caminho faz sentido para a maioria dos aplicativos se referirem a um nó de destino.

Mais importante, é **mix**:referenciável, o que significa que pode ser aplicado a um nó no momento em que você realmente precisa referenciá-lo.

Portanto, digamos que apenas porque você gostaria de fazer referência a um nó do tipo &quot;Documento&quot; não significa que seu tipo de nó &quot;Documento&quot; tenha que se estender de mix:referenceable de forma estática, já que ele pode ser adicionado a qualquer instância do &quot;Documento&quot; dinamicamente.

#### Exemplo {#example-7}

Utilização:

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
