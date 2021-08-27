---
title: Modelos de fragmentos do conteúdo
seo-title: Content Fragment Templates
description: Os modelos são selecionados ao criar um fragmento de conteúdo e fornecer ao novo fragmento a estrutura, o elemento e a variação básicos
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: 2ec9625d480eb8cae23f44aa247fce2a519dec31
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 5%

---

# Modelos de fragmentos do conteúdo{#content-fragment-templates}

>[!CAUTION]
>
>[Os ](/help/assets/content-fragments/content-fragments-models.md) modelos de fragmento de conteúdo agora são recomendados para criar todos os seus fragmentos.
>
>Os modelos de fragmento de conteúdo são usados para todos os exemplos no We.Retail.

>[!NOTE]
>
>Antes do AEM 6.3, os Fragmentos de conteúdo eram criados com o uso de modelos em vez de modelos. Os modelos não estão mais disponíveis para criar novos fragmentos, mas os fragmentos criados com esse modelo ainda são compatíveis.

Os modelos são selecionados ao criar um fragmento de conteúdo. Eles fornecem ao novo fragmento a estrutura básica, os elementos e a variação. Os modelos usados para fragmentos de conteúdo estão sujeitos ao Gerenciador de configuração do Granite.

Os templates prontos para uso são mantidos em:

* `/libs/settings/dam/cfm/templates`

Você pode criar modelos específicos do site para fragmentos de conteúdo em:

* `/apps/settings/dam/cfm/templates`
O local para sobrepor modelos prontos ou fornecer modelos específicos do cliente em todo o aplicativo que não devem ser estendidos/alterados no tempo de execução.

* `/conf/global/settings/dam/cfm/templates`
O local para modelos específicos de toda a instância do cliente que precisam ser alterados no tempo de execução.

A ordem de precedência é (em ordem decrescente) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>Você ***não deve*** alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs`) em `/apps`
>
>1. Faça quaisquer alterações em `/apps`

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
     <td>Esse nó é a raiz de cada template. É obrigatório e deve ter um nome exclusivo.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>O título do modelo (exibido no assistente <strong>Criar fragmento</strong>).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>opcional</p> </td>
     <td>Um texto que descreve a finalidade do modelo (exibido no assistente <strong>Criar fragmento</strong>).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>opcional</p> </td>
     <td>Uma matriz com caminhos para coleções que devem ser associados a um fragmento de conteúdo recém-criado por padrão.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, se os subativos que representam os elementos (exceto o elemento principal) do fragmento de conteúdo devem ser criados quando o fragmento de conteúdo é criado; <em>false</em> se tiverem de ser criados "em tempo real".</p> <p><strong>Observação</strong>: atualmente, esse parâmetro deve ser definido como  <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>obrigatório</p> </td>
     <td><p>Versão da estrutura de conteúdo; atualmente suportado:</p> <p><strong>Observação</strong>: atualmente, esse parâmetro deve ser definido como  <code>2</code>.<br /> </p> </td>
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
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>obrigatório</p> </td>
     <td><p>Nó que contém a definição dos elementos do fragmento de conteúdo. É obrigatório e precisa conter pelo menos um nó filho para o elemento <strong>Main</strong>, mas pode conter [1...n] nós filho.</p> <p>Quando o modelo é usado, a subramificação de elementos é copiada para a subramificação de modelo do fragmento.</p> <p>O primeiro elemento (como exibido no CRXDE Lite) é automaticamente considerado como o elemento <i>main</i>; O nome do nó é irrelevante e o nó em si não tem um significado especial, além do fato de ser representado pelo ativo principal; os outros elementos são tratados como subativos.</p> </td>
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
     <td>Esse nó define um elemento. É obrigatório e deve ter um nome exclusivo.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obrigatório</p> </td>
     <td>O título do elemento (exibido no seletor de elemento do editor de fragmentos).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>default: ""</p> </td>
     <td>Conteúdo inicial do elemento; usado somente se <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>default: <code>text/html</code></p> </td>
     <td><p>Tipo de conteúdo inicial do elemento; usado somente se <code>precreateElements</code><i> = </i><code>true</code>; atualmente suportado:</p>
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
     <td><code>variations</code> </td>
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
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>obrigatório se um nó de variação estiver presente</p> </td>
     <td><p>Define uma variação inicial.<br /> A variação é adicionada a todos os elementos do fragmento de conteúdo por padrão.</p> <p>A variação terá o mesmo conteúdo inicial do elemento respectivo (consulte <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obrigatório</p> </td>
     <td>O título da variação (exibido na guia <strong>Variation</strong> do editor de fragmentos (painel esquerdo)).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>padrão: ""</p> </td>
     <td>Um texto que fornece uma descrição da variação <span>(exibida na guia <strong>Variation</strong> do editor de fragmentos (painel esquerdo)).</code></td>
    </tr>
   </tbody>
  </table>
