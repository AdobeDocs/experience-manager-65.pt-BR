---
title: Modelos de fragmentos do conteúdo
description: Os modelos são selecionados ao criar um fragmento de conteúdo e fornecem ao novo fragmento a estrutura básica, o elemento e a variação
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# Modelos de fragmentos do conteúdo{#content-fragment-templates}

>[!CAUTION]
>
>[Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) são recomendadas para criar todos os novos fragmentos de conteúdo.
>
>Os modelos de fragmento de conteúdo são usados para todos os exemplos no WKND.

>[!NOTE]
>
>Antes do AEM 6.3, os fragmentos de conteúdo eram criados com base em modelos em vez de modelos.
>
>Os modelos de Fragmento de conteúdo agora estão obsoletos. Eles ainda podem ser usados para criar fragmentos, mas é recomendável usar Modelos de fragmento de conteúdo. Nenhum novo recurso será adicionado aos modelos de fragmento e será removido em uma versão futura.

Os modelos são selecionados ao criar um fragmento de conteúdo. Eles fornecem o novo fragmento com a estrutura básica, os elementos e a variação. Os modelos usados para fragmentos de conteúdo estão sujeitos ao Granite Configuration Manager.

Os templates prontos para uso são mantidos em:

* `/libs/settings/dam/cfm/templates`

Você pode criar modelos específicos do site para fragmentos de conteúdo em:

* `/apps/settings/dam/cfm/templates`
O local para sobrepor modelos prontos para uso ou fornecer modelos do aplicativo específicos do cliente que não devem ser estendidos/alterados no tempo de execução.

* `/conf/global/settings/dam/cfm/templates`
O local para modelos específicos do cliente em toda a instância que precisam ser alterados no tempo de execução.

A ordem de precedência é (em ordem decrescente) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>Você ***deve*** não alterar nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído ao aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs`) em `/apps`
>
>1. Fazer alterações em `/apps`
>

A estrutura básica de um modelo é mantida em:

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

Sendo a estrutura específica:

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

Mais detalhes sobre os nós e suas propriedades são:

* **Modelo**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Este nó é a raiz de cada modelo. É obrigatório e deve ter um nome exclusivo.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obrigatório<br /> </p> </td>
     <td>O título do modelo (exibido no campo <strong>Criar fragmento</strong> assistente).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>opcional</p> </td>
     <td>Um texto que descreve a finalidade do modelo (exibido no campo <strong>Criar fragmento</strong> assistente).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>opcional</p> </td>
     <td>Uma matriz com caminhos para coleções que devem ser associados a um fragmento de conteúdo recém-criado por padrão.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>obrigatório</p> </td>
     <td><p><code>true</code>, se os subativos que representam os elementos (exceto o elemento principal) do fragmento de conteúdo tiverem que ser criados quando o fragmento de conteúdo for criado; <em>false</em> se eles devem ser criados "em tempo real".</p> <p><strong>Nota</strong>: atualmente, esse parâmetro deve ser definido como <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>obrigatório</p> </td>
     <td><p>Versão da estrutura de conteúdo; atualmente compatível:</p> <p><strong>Nota</strong>: atualmente, esse parâmetro deve ser definido como <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **Elementos**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>obrigatório</p> </td>
     <td><p>Nó que contém a definição dos elementos do fragmento de conteúdo. É obrigatório e precisa conter pelo menos um nó secundário para o <strong>Principal</strong> elemento, mas pode conter [1..n] nós-filhos.</p> <p>Quando o modelo é usado, a sub-ramificação dos elementos é copiada para a sub-ramificação do modelo do fragmento.</p> <p>O primeiro elemento (conforme visualizado em CRXDE Lite) é automaticamente considerado como sendo o <i>main</i> elemento; o nome do nó é irrelevante e o nó em si não tem um significado especial, exceto o fato de que é representado pelo ativo principal; os outros elementos são tratados como subativos.</p> </td>
    </tr>
   </tbody>
  </table>

* **Nome do elemento**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Este nó define um elemento. É obrigatório e deve ter um nome exclusivo.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obrigatório</p> </td>
     <td>O título do elemento (exibido no seletor de elementos do editor de fragmentos).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>padrão: ""</p> </td>
     <td>Conteúdo inicial do elemento; usado somente se <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>padrão: <code>text/html</code></p> </td>
     <td><p>Tipo de conteúdo inicial do elemento; usado somente se <code>precreateElements</code><i> = </i><code>true</code>; atualmente com suporte:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>obrigatório</p> </td>
     <td>O nome interno do elemento; deve ser exclusivo para o tipo de fragmento.</td>
    </tr>
   </tbody>
  </table>

* **Variações**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>opcional</p> </td>
     <td>Esse nó opcional contém a definição das variações iniciais do fragmento de conteúdo.</td>
    </tr>
   </tbody>
  </table>

* **Nome da variação**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>obrigatório se um nó de variação estiver presente</p> </td>
     <td><p>Define uma variação inicial.<br /> A variação é adicionada a todos os elementos do fragmento de conteúdo por padrão.</p> <p>A variação terá o mesmo conteúdo inicial que o respectivo elemento (consulte <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obrigatório</p> </td>
     <td>O título da variação (exibido no editor de fragmentos <strong>Variação</strong> (painel esquerdo).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>padrão: ""</p> </td>
     <td>Um texto que fornece uma descrição da variação <span>(exibido no editor de fragmentos <strong>Variação</strong> (painel esquerdo).</code></td>
    </tr>
   </tbody>
  </table>
