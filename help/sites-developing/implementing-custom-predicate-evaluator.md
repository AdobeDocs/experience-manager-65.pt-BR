---
title: Implementação de um Avaliador Predicado Personalizado para o Construtor de Consultas
seo-title: Implementação de um Avaliador Predicado Personalizado para o Construtor de Consultas
description: O Query Builder oferece uma maneira fácil de consultar o repositório de conteúdo
seo-description: O Query Builder oferece uma maneira fácil de consultar o repositório de conteúdo
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Implementação de um Avaliador Predicado Personalizado para o Construtor de Consultas{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Esta seção descreve como estender o Construtor [de](/help/sites-developing/querybuilder-api.md) Consulta implementando um avaliador de predicado personalizado.

## Visão geral {#overview}

O [Query Builder](/help/sites-developing/querybuilder-api.md) oferece uma maneira fácil de consultar o repositório de conteúdo. O CQ é enviado com um conjunto de avaliadores de predicados que ajudam você a lidar com seus dados.

No entanto, talvez você queira simplificar suas consultas implementando um avaliador de predicado personalizado que oculta alguma complexidade e garante uma melhor semântica.

Um predicado personalizado também pode executar outras coisas que não são diretamente possíveis com o XPath, por exemplo:

* como procurar alguns dados de algum serviço
* filtragem personalizada com base no cálculo

>[!NOTE]
>
>Problemas de desempenho devem ser considerados ao implementar um predicado personalizado.

>[!NOTE]
>
>Você pode encontrar exemplos de consultas na seção [Query Builder](/help/sites-developing/querybuilder-api.md) .

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-search-custom-predicate-assessment no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### Prever avaliador em detalhes {#predicate-evaluator-in-detail}

Um avaliador de predicado lida com a avaliação de determinados predicados, que são as restrições de definição de uma consulta.

Ele mapeia uma restrição de pesquisa de nível superior (como &quot;largura > 200&quot;) para uma consulta JCR específica que se encaixa no modelo de conteúdo real (por exemplo, metadata/@width > 200). Ou pode filtrar manualmente os nós e verificar suas restrições.

>[!NOTE]
>
>Para obter mais informações sobre o pacote `PredicateEvaluator` e o `com.day.cq.search` pacote, consulte a documentação [do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)Java.

### Implementação de um avaliador de previsão personalizado para metadados de replicação {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Como exemplo, esta seção descreve como criar um avaliador de predicado personalizado que ajuda os dados com base nos metadados de replicação:

* `cq:lastReplicated` que armazena a data da última ação de replicação

* `cq:lastReplicatedBy` que armazena a ID do usuário que acionou a última ação de replicação

* `cq:lastReplicationAction` que armazena a última ação de replicação (por exemplo, Ativação, Desativação)

#### Consultando metadados de replicação com avaliadores preditivos padrão {#querying-replication-metadata-with-default-predicate-evaluators}

A consulta a seguir busca a lista de nós em `/content` ramificações que foram ativados `admin` desde o início do ano.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Essa consulta é válida, mas difícil de ler, e não destaca a relação entre as três propriedades de replicação. A implementação de um avaliador de predicado personalizado reduzirá a complexidade e melhorará a semântica dessa consulta.

#### Objetivos {#objectives}

O objetivo da consulta `ReplicationPredicateEvaluator` é suportar a consulta acima usando a seguinte sintaxe.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

O agrupamento de metadados de replicação prevê com um avaliador de predicado personalizado ajuda a criar uma consulta significativa.

#### Atualizando dependências Maven {#updating-maven-dependencies}

>[!NOTE]
>
>A configuração de novos projetos do AEM usando o maven está documentada em [Como criar projetos do AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

Primeiro, você precisa atualizar as dependências Maven do seu projeto. O `PredicateEvaluator` é parte do `cq-search` artefato, portanto, ele precisa ser adicionado ao arquivo pom Maven.

>[!NOTE]
>
>O escopo da `cq-search` dependência está definido como `provided` porque `cq-search` será fornecido pelo `OSGi` contêiner.

pom.xml

O trecho a seguir mostra as diferenças, no formato de comparação [unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

[aem-search-custom-predicate-avaliator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### Gravando O ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

O `cq-search` projeto contém a classe `AbstractPredicateEvaluator` abstrata. Isso pode ser estendido com algumas etapas para implementar seu próprio avaliador de predicado personalizado `(PredicateEvaluator`).

>[!NOTE]
>
>O procedimento a seguir explica como criar uma `Xpath` expressão para filtrar dados. Outra opção seria implementar o `includes` método que seleciona os dados em uma base de linha. See the [Java documentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) for more information.

1. Criar uma nova classe Java que se estende `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Faça uma anotação em sua classe com uma `@Component` semelhante a

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   O trecho a seguir mostra as diferenças, no formato de comparação [unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -19,8 +19,11 @@
  */
 package com.adobe.aem.docs.search;

+import org.apache.felix.scr.annotations.Component;
+
 import com.day.cq.search.eval.AbstractPredicateEvaluator;

+@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
 public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

 }
```

[aem-search-custom-predicate-avaliator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>A string `factory`deve ser exclusiva, começando com `com.day.cq.search.eval.PredicateEvaluator/`e terminando com o nome do personalizado `PredicateEvaluator`.

>[!NOTE]
>
>O nome do predicado `PredicateEvaluator` é o nome do predicado, que é usado ao criar consultas.

1. Substituir:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   No método override, você cria uma `Xpath` expressão com base no argumento `Predicate` fornecido.

### Exemplo de um Avaliador Predicado Personalizado para Metadados de Replicação {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

A implementação completa dessa `PredicateEvaluator` pode ser semelhante à seguinte classe.

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```

[aem-search-custom-predicate-avaliator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
