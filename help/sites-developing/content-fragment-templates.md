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
source-git-commit: a2b1bd5462ae1837470e31cfeb87a95af1c69be5
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 5%

---

# Modelos de fragmentos do conteúdo{#content-fragment-templates}

>[!CAUTION]
>
>[Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) são recomendados para criar todos os novos fragmentos de conteúdo.
>
>Os modelos de fragmento de conteúdo são usados para todos os exemplos na WKND.

>[!NOTE]
>
>Antes do AEM 6.3, os Fragmentos de conteúdo eram criados com base em modelos em vez de modelos.
>
>Os modelos de Fragmento de conteúdo agora estão obsoletos. Elas ainda podem ser usadas para criar fragmentos, mas é recomendado usar Modelos de fragmento de conteúdo . Nenhum novo recurso será adicionado aos modelos de fragmento e será removido em uma versão futura.

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
>Você ***must*** não altere nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs`) `/apps`
>
>1. Faça quaisquer alterações no `/apps`

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
     <td>O título do modelo (exibido no <strong>Criar fragmento</strong> assistente).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>opcional</p> </td>
     <td>Um texto que descreve a finalidade do modelo (exibido no <strong>Criar fragmento</strong> assistente).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>opcional</p> </td>
     <td>Uma matriz com caminhos para coleções que devem ser associados a um fragmento de conteúdo recém-criado por padrão.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, se os subativos que representam os elementos (exceto o elemento principal) do fragmento de conteúdo devem ser criados quando o fragmento de conteúdo é criado; <em>false</em> caso devam ser criados "em tempo real".</p> <p><strong>Observação</strong>: atualmente, esse parâmetro deve ser definido como <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>obrigatório</p> </td>
     <td><p>Versão da estrutura de conteúdo; atualmente suportado:</p> <p><strong>Observação</strong>: atualmente, esse parâmetro deve ser definido como <code>2</code>.<br /> </p> </td>
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
     <td><p>Nó que contém a definição dos elementos do fragmento de conteúdo. É obrigatório e precisa conter pelo menos um nó filho para a variável <strong>Principal</strong> , mas pode conter [1..n] nós filho.</p> <p>Quando o modelo é usado, a subramificação de elementos é copiada para a subramificação de modelo do fragmento.</p> <p>O primeiro elemento (como exibido no CRXDE Lite) é automaticamente considerado como sendo o <i>main</i> elemento; O nome do nó é irrelevante e o nó em si não tem um significado especial, além do fato de ser representado pelo ativo principal; os outros elementos são tratados como subativos.</p> </td>
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
     <td>Conteúdo inicial do elemento; somente usado se <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>default: <code>text/html</code></p> </td>
     <td><p>Tipo de conteúdo inicial do elemento; somente usado se <code>precreateElements</code><i> = </i><code>true</code>; atualmente suportado:</p>
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
     <td><p>Define uma variação inicial.<br /> A variação é adicionada a todos os elementos do fragmento de conteúdo por padrão.</p> <p>A variação terá o mesmo conteúdo inicial que o respectivo elemento (consulte <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obrigatório</p> </td>
     <td>O título da variação (exibido no editor de fragmentos <strong>Variação</strong> guia (painel esquerdo).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>padrão: ""</p> </td>
     <td>Um texto que fornece uma descrição da variação <span>(exibido no editor de fragmentos <strong>Variação</strong> guia (painel esquerdo).</code></td>
    </tr>
   </tbody>
  </table>
