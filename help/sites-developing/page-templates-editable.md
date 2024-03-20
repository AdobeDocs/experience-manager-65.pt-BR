---
title: Modelos de página - Editável
description: Foram introduzidos modelos editáveis que permitem que não desenvolvedores criem e editem modelos, fornecem modelos que mantêm uma conexão dinâmica com qualquer página criada a partir deles e tornam o componente de página mais genérico
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3186'
ht-degree: 4%

---

# Modelos de página - Editável {#page-templates-editable}

Foram introduzidos modelos editáveis para:

* Permitir que autores especializados [criar e editar modelos](/help/sites-authoring/templates.md).

   * Tais autores especializados são chamados **autores de modelo**
   * Os autores do modelo devem ser membros do `template-authors` grupo.

* Forneça modelos que mantenham uma conexão dinâmica com qualquer página criada a partir deles. Isso garante que qualquer alteração no modelo seja refletida nas próprias páginas.
* Torne o componente da página mais genérico para que o componente da página principal possa ser usado sem personalização.

Com modelos editáveis, as partes que fazem uma página são isoladas dentro de componentes. Você pode configurar as combinações necessárias de componentes em uma interface de usuário, de modo a eliminar a necessidade de um novo componente de página ser desenvolvido para cada variação de página.

>[!NOTE]
>
>[Modelos estáticos](/help/sites-developing/page-templates-static.md) também estão disponíveis.

Este documento:

* Fornece uma visão geral da criação de modelos editáveis

   * Para obter mais detalhes, consulte [Criação de modelos de página](/help/sites-authoring/templates.md)

* Descreve as tarefas de administrador/desenvolvedor necessárias para criar modelos editáveis
* Descreve os fundamentos técnicos de modelos editáveis

Este documento supõe que você já esteja familiarizado com a criação e edição de modelos. Consulte o documento de criação [Criação de modelos de página](/help/sites-authoring/templates.md), que detalha os recursos dos modelos editáveis conforme expostos ao autor do modelo.

>[!NOTE]
>
>O tutorial a seguir também pode ser interessante para configurar um modelo de página editável em um novo projeto:
>[Introdução ao AEM Sites Parte 2 - Criação de uma página base e um modelo](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html)

## Criação de um novo modelo {#creating-a-new-template}

A criação de modelos editáveis é feita principalmente com o [console de modelos e editor de modelos](/help/sites-authoring/templates.md) por um autor de modelo. Esta seção fornece uma visão geral desse processo e segue com uma descrição do que ocorre em nível técnico.

Para obter informações sobre como usar modelos editáveis em um projeto AEM, consulte [Criação de um projeto AEM usando Lazybones](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478).

Ao criar um modelo editável, você:

1. Criar um [pasta dos modelos](#template-folders). Esta pasta não é obrigatória, mas é uma prática recomendada.
1. Selecione um [tipo de modelo](#template-type). Este tipo é copiado para criar o [definição do modelo](#template-definitions).

   >[!NOTE]
   >
   >Uma seleção de tipos de modelo é fornecida pronta para uso. Também é possível [criar seus próprios tipos de modelo específicos do site](/help/sites-developing/page-templates-editable.md#creating-template-types), se necessário.

1. Configure a estrutura, as políticas de conteúdo, o conteúdo inicial e o layout do novo modelo.

   **Estrutura**

   * A estrutura permite definir os componentes e o conteúdo para o modelo.
   * Os componentes definidos na estrutura do modelo não podem ser movidos em uma página resultante nem excluídos de qualquer página resultante.

      * Se você estiver criando um modelo em uma pasta personalizada fora da `We.Retail` conteúdo de amostra, você pode escolher Componentes de base ou usar [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html).

   * Se desejar que os autores de página possam adicionar e remover componentes, adicione um sistema de parágrafo ao modelo.
   * Os componentes podem ser desbloqueados e bloqueados novamente para permitir que você defina o conteúdo inicial.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos da estrutura, consulte [Estrutura](/help/sites-developing/page-templates-editable.md#structure) neste documento.

   **Políticas**

   * As políticas de conteúdo definem as propriedades de design de um componente.

      * Por exemplo, os componentes disponíveis ou as dimensões mínima/máxima.

   * Essas políticas são aplicáveis ao modelo (e páginas criadas com o modelo).

   Para obter detalhes sobre como um autor de modelo define políticas, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos das políticas, consulte [Políticas de conteúdo](/help/sites-developing/page-templates-editable.md#content-policies) neste documento.

   **Conteúdo inicial**

   * O Conteúdo inicial define o conteúdo que aparece quando uma página é criada pela primeira vez com base no modelo.
   * O conteúdo inicial pode ser editado pelos autores da página.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Para obter detalhes técnicos sobre o conteúdo inicial, consulte [Conteúdo inicial](/help/sites-developing/page-templates-editable.md#initial-content) neste documento.

   **Layout**

   * Você pode definir o layout do modelo para um intervalo de dispositivos.
   * O Layout responsivo para modelos funciona como na criação de página.

   Para obter detalhes sobre como um autor de modelo define o layout do modelo, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Para obter detalhes técnicos sobre o layout do modelo, consulte [Layout](/help/sites-developing/page-templates-editable.md#layout) neste documento.

1. Ative o modelo e, em seguida, aguarde-o para árvores de conteúdo específicas.

   * Um modelo pode ser ativado ou desativado para disponibilizá-lo ou indisponibilizá-lo para os autores da página.
   * Um modelo pode ser disponibilizado ou indisponibilizado para determinadas ramificações de página.

   Para obter detalhes sobre como um autor de modelo habilita um modelo, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Para obter detalhes técnicos sobre a ativação de um template, consulte [Ativar e permitir um modelo para nós](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e neste documento

1. Use-a para criar páginas de conteúdo.

   * Ao usar um modelo para criar uma página, não há diferença visível e nenhuma indicação entre modelos estáticos e editáveis.
   * Para o autor da página, o processo é transparente.

   Para obter detalhes sobre como um autor de página usa modelos para criar uma página, consulte [Criar e organizar páginas](/help/sites-authoring/managing-pages.md#templates).

   Para obter detalhes técnicos sobre como criar páginas com modelos editáveis, consulte [Páginas de conteúdo resultante](/help/sites-developing/page-templates-editable.md#resultant-content-pages) neste documento.

>[!TIP]
>
>Nunca insira qualquer informação que deve ser internacionalizada em um modelo. Para efeitos de internalização, a [recurso de localização dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=pt-BR) é recomendada.

>[!NOTE]
>
>Os modelos são ferramentas eficientes para simplificar o fluxo de trabalho de criação de página. No entanto, usar modelos em excesso pode sobrecarregar os autores e tornar confusa a criação da página. Uma boa regra geral é manter o número de modelos abaixo de 100.
>
>A Adobe não recomenda ter mais de 1000 modelos devido a possíveis impactos no desempenho.

>[!NOTE]
>
>A biblioteca cliente do editor presume a presença do `cq.shared` namespace nas páginas de conteúdo. Se estiver ausente, resultará no erro JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Todos os exemplos de páginas de conteúdo contêm `cq.shared`, portanto, qualquer conteúdo baseado nelas inclui automaticamente `cq.shared`. No entanto, se você decidir criar suas próprias páginas de conteúdo do zero sem baseá-las em conteúdo de amostra, não deixe de incluir o `cq.shared` namespace.
>
>Consulte [Uso de bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Pastas de Modelos {#template-folders}

Para organizar os templates, você pode usar as seguintes pastas:

* **global**
* Específico do site As pastas específicas do site que você cria para organizar seus modelos são criadas com uma conta que tem privilégios de administrador.

>[!NOTE]
>
>Mesmo que você possa aninhar suas pastas, quando o usuário as visualizar no **Modelos** console, eles são apresentados como uma estrutura plana.

Em uma instância padrão do AEM, a variável **global** a pasta existe no console modelo. Essa pasta retém modelos padrão e atua como um fallback se nenhuma política e/ou tipo de modelo for encontrado na pasta atual. Você pode adicionar seus modelos padrão a esta pasta ou criar uma pasta (recomendado).

>[!NOTE]
>
>É uma prática recomendada criar uma pasta para armazenar seus modelos personalizados e não usar a pasta global.

>[!CAUTION]
>
>As pastas devem ser criadas por um usuário com `admin` direitos.

Os tipos de modelo e as políticas são herdados em todas as pastas de acordo com a seguinte ordem de precedência:

1. A pasta atual.
1. Pai ou pais da pasta atual.
1. `/conf/global`
1. `/apps`
1. `/libs`

Uma lista de todas as entradas permitidas é criada. Se alguma configuração se sobrepor ( `path`/ `label`), somente a instância mais próxima à pasta atual é apresentada ao usuário.

Para criar uma pasta, faça o seguinte:

* Programaticamente ou com CRXDE Lite
* Usar o navegador de configuração

## Uso do CRXDE Lite {#using-crxde-lite}

1. Uma nova pasta (em /conf) pode ser criada para sua instância de forma programática ou com o CRXDE Lite.

   Deve ser utilizada a seguinte estrutura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. Em seguida, você pode definir as seguintes propriedades no nó raiz da pasta:

   `<your-folder-name> [sling:Folder]`

   Nome: `jcr:title`

   * Tipo: `String`

   * Valor: o título (da pasta) que você deseja exibir na variável **Modelos** console.

1. Entrada *adição* às permissões e privilégios de criação padrão (por exemplo, `content-authors`), atribua grupos e defina os direitos de acesso (ACLs) necessários para que seus autores possam criar modelos na nova pasta.

   A variável `template-authors` grupo é o grupo padrão que deve ser atribuído. Consulte a seguinte seção [ACLs e grupos](/help/sites-developing/page-templates-editable.md#acls-and-groups) para obter detalhes.

   Consulte [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management) para obter detalhes completos sobre gerenciamento e atribuição de direitos de acesso.

### Usar o navegador de configuração {#using-the-configuration-browser}

1. Ir para **Navegação global** > **Ferramentas** > **Navegador de configuração**.

   As pastas existentes são listadas à esquerda, incluindo a **global** pasta.

1. Clique em **Criar**.
1. No **Criar configuração** , os seguintes campos deverão ser configurados:

   * **Título**: forneça um título para a pasta de configuração
   * **Modelos editáveis**: selecione para permitir modelos editáveis nesta pasta

1. Clique em **Criar**

>[!NOTE]
>
>No Navegador de configuração, você pode editar a pasta global e ativar o **Modelos editáveis** opção se quiser criar templates dentro dessa pasta. No entanto, essa prática não é uma prática recomendada.
>
>Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.

### ACLs e grupos {#acls-and-groups}

Depois que as pastas de modelo forem criadas (por meio do CRXDE ou com o Navegador de configuração), as ACLs deverão ser definidas para os grupos apropriados para as pastas de modelo, a fim de garantir a segurança adequada.

As pastas de modelo para o [`We.Retail` implementação de referência](/help/sites-developing/we-retail.md) pode ser usado como exemplo.

#### O grupo de autores de modelo {#the-template-authors-group}

A variável `template-authors` group é o grupo usado para gerenciar o acesso a modelos e vem com AEM por padrão, mas está vazio. Os usuários devem ser adicionados ao grupo para o projeto/site.

>[!CAUTION]
>
>A variável `template-authors` o grupo é *somente* para usuários que devem ser capazes de criar modelos.
>
>A edição de modelos é avançada e, se não for feita corretamente, os modelos existentes poderão ser corrompidos. Portanto, essa função deve ser focalizada e incluir apenas usuários qualificados.

A tabela a seguir detalha as permissões necessárias para a edição de modelos.

<table>
 <tbody>
  <tr>
   <th>Caminho</th>
   <th>Função/Grupo</th>
   <th>Permissões<br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores do modelo<br /> </td>
   <td>ler, gravar, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em sites específicos <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>ler</td>
   <td>O usuário da Web anônimo deve ler os modelos ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>replicateContent autores devem ativar os modelos de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>ler, gravar, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em sites específicos <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>ler</td>
   <td>O Usuário Anônimo da Web deve ler as políticas ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo devem ativar as políticas de um modelo de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor do modelo</td>
   <td>ler</td>
   <td>O autor do modelo cria um modelo com base em um dos tipos de modelo predefinidos.</td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>nenhum</td>
   <td>O usuário da Web anônimo não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

Este padrão `template-authors` grupo abrange apenas as configurações do projeto, em que todas as `template-authors` os membros têm permissão para acessar e criar todos os modelos. Para configurações mais complexas, em que há necessidade de vários grupos de autores de modelo para separar o acesso aos modelos, mais grupos de autores de modelo personalizados devem ser criados. No entanto, as permissões para os grupos de autores de modelo ainda seriam as mesmas.

#### Modelos herdados em /conf/global {#legacy-templates-under-conf-global}

Não armazenar modelos no `/conf/global`. No entanto, para algumas instalações herdadas, ainda pode haver modelos neste local. *Somente* em tais situações herdadas devem ser `/conf/global` caminhos sejam configurados explicitamente.

<table>
 <tbody>
  <tr>
   <th>Caminho</th>
   <th>Função/Grupo</th>
   <th>Permissões<br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autores do modelo</td>
   <td>ler, gravar, replicar</td>
   <td>Autores de modelos que criam, leem, atualizam, excluem e replicam modelos no <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>ler</td>
   <td>O usuário da Web anônimo deve ler os modelos ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo devem ativar os modelos de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>ler, gravar, replicar</td>
   <td>Autores de modelos que criam, leem, atualizam, excluem e replicam modelos no <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>ler</td>
   <td>O Usuário Anônimo da Web deve ler as políticas ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo devem ativar as políticas de um modelo de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autor do modelo</td>
   <td>ler</td>
   <td>O autor do modelo cria um modelo com base em um dos tipos de modelo predefinidos</td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>nenhum</td>
   <td>O usuário da Web anônimo não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

## Tipo de modelo {#template-type}

Ao criar um modelo, especifique um tipo de modelo:

* Os tipos de modelo fornecem modelos para um modelo de maneira eficaz. Ao criar um template, a estrutura e o conteúdo inicial do tipo de template selecionado são usados para criar o template.

   * O tipo de modelo é copiado para criar o modelo.
   * Depois que a cópia ocorre, a única conexão entre o modelo e o tipo de modelo é uma referência estática para fins de informação.

* Os tipos de modelo permitem definir:

   * O tipo de recurso do componente de página.
   * A política do nó raiz, que define os componentes permitidos no editor de modelo.
   * A Adobe recomenda que você defina os pontos de interrupção para a grade responsiva e a configuração do emulador móvel em no tipo de modelo. Essa etapa é opcional, pois a configuração também pode ser definida no template individual (consulte [Tipo de modelo e grupos de dispositivos móveis](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* O AEM fornece uma pequena seleção de tipos de modelo prontos para uso, como Página HTML5 e Página de formulário adaptável.

   * Exemplos adicionais são fornecidos como parte do [`We.Retail`](/help/sites-developing/we-retail.md) conteúdo de amostra.

* Os tipos de modelo normalmente são definidos pelos desenvolvedores.

Os tipos de template prontos para uso são armazenados em:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Não altere nada no `/libs` caminho. O motivo é porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído ao aplicar um hotfix ou pacote de recursos).

Os tipos de modelo específicos do site devem ser armazenados no local comparável do:

* `/apps/settings/wcm/template-types`

As definições para seus tipos de modelos personalizados devem ser armazenadas em pastas definidas pelo usuário (recomendado) ou, como alternativa, em `global`. Por exemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Os tipos de template devem respeitar a estrutura de pasta correta (ou seja, `/settings/wcm/...`), caso contrário, os tipos de template não serão encontrados.

### Tipo de modelo e grupos de dispositivos móveis {#template-type-and-mobile-device-groups-br}

A variável [grupos de dispositivos](/help/sites-developing/mobile.md#device-groups) usado para um modelo editável (definido como caminho relativo da propriedade) `cq:deviceGroups`) definir quais dispositivos móveis estão disponíveis como emuladores no [modo de layout](/help/sites-authoring/responsive-layout.md) da criação de páginas. Esse valor pode ser definido em dois lugares:

* No tipo de modelo editável
* No modelo editável

Ao criar um modelo editável, o valor é copiado do tipo de modelo para o modelo individual. Se o valor não estiver definido no tipo, ele poderá ser definido no template. Depois que um modelo é criado, não há herança do tipo para o modelo.

>[!CAUTION]
>
>O valor de `cq:deviceGroups` deve ser definido como um caminho relativo, como `mobile/groups/responsive` e não como um caminho absoluto, como `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Com [modelos estáticos](/help/sites-developing/page-templates-static.md), o valor de `cq:deviceGroups` pode ser definido na raiz do site.
>
>Com modelos editáveis, esse valor agora é armazenado no nível do modelo e não é compatível no nível raiz da página.

### Criação de Tipos de Modelo {#creating-template-types}

Se você tiver criado um modelo que possa servir como base de outros modelos, poderá copiá-lo como um tipo de modelo.

1. Crie um modelo como faria com qualquer modelo editável [conforme documentado aqui](/help/sites-authoring/templates.md#creating-a-new-template-template-author), que pode servir como base para o tipo de template.
1. Usando o CRXDE Lite, copie o modelo recém-criado do `templates` para o nó `template-types` sob o nó [pasta modelo](/help/sites-developing/page-templates-editable.md#template-folders).
1. Exclua o modelo da variável `templates` sob o nó [pasta modelo](/help/sites-developing/page-templates-editable.md#template-folders).
1. Na cópia do modelo que está sob o `template-types` nó, excluir tudo `cq:template` e `cq:templateType` propriedades de todos `jcr:content` nós.

Você também pode desenvolver seu próprio tipo de modelo usando um modelo editável de exemplo como base, disponível no GitHub.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-sites-example-custom-template-type no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Baixar o projeto como [um arquivo ZIP](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master)

## Definições de modelo {#template-definitions}

As definições para modelos editáveis são armazenadas [pastas definidas pelo usuário](/help/sites-developing/page-templates-editable.md#template-folders) (recomendado) ou, em alternativa, no `global`. Por exemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

O nó raiz do modelo é do tipo `cq:Template` com uma estrutura de esqueleto de:

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Os principais elementos são:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

Este nó retém propriedades para o modelo:

* **Nome**: `jcr:title`

* **Nome**: `status`

   * **Tipo**: `String`

   * **Valor**: `draft`, `enabled`ou `disabled`

### Estrutura {#structure}

Define a estrutura da página resultante:

* É mesclado com o conteúdo inicial ( `/initial`) ao criar uma página.
* As alterações feitas na estrutura são refletidas em qualquer página criada com o modelo.
* A variável `root` ( `structure/jcr:content/root`) define a lista de componentes que estão disponíveis na página resultante.

   * Os componentes definidos na estrutura do modelo não podem ser movidos para ou excluído de qualquer página resultante.
   * Depois que um componente é desbloqueado, a variável `editable` propriedade está definida como `true`.

   * Depois que um componente que já contém conteúdo é desbloqueado, esse conteúdo é movido para a tag `initial` filial.

* A variável `cq:responsive` o nó contém definições para o layout responsivo.

### Conteúdo inicial {#initial-content}

Define o conteúdo inicial que uma nova página tem na criação:

* Contém um `jcr:content` que é copiado para qualquer página nova.
* É mesclado com a estrutura ( `/structure`) ao criar uma página.
* Quaisquer páginas existentes serão atualizadas se o conteúdo inicial for alterado após a criação.
* A variável `root` O nó contém uma lista de componentes para definir o que está disponível na página resultante.
* Se o conteúdo for adicionado a um componente no modo de estrutura e esse componente for posteriormente desbloqueado (ou vice-versa), esse conteúdo será usado como conteúdo inicial.

### Layout {#layout}

Quando [ao editar um modelo, é possível definir o layout](/help/sites-authoring/templates.md), esta prática usa [layout responsivo padrão](/help/sites-authoring/responsive-layout.md) que também pode ser [configurado](/help/sites-administering/configuring-responsive-layout.md).

### Políticas de conteúdo {#content-policies}

As políticas de conteúdo (ou design) definem as propriedades de design de um componente, como a disponibilidade do componente ou as dimensões mínimas/máximas. Essas políticas são aplicáveis ao modelo (e páginas criadas com o modelo). As políticas de conteúdo podem ser criadas e selecionadas no editor de modelo.

* A propriedade `cq:policy`, no `root` nó
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornece uma referência relativa à política de conteúdo para o sistema de parágrafos da página.

* A propriedade `cq:policy`, nos nós componente-explícito em `root`, fornecem links para as políticas de componentes individuais.

* As definições de políticas reais são armazenadas em:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Os caminhos das definições de política dependem do caminho do componente. A variável `cq:policy` mantém uma referência relativa à própria configuração.

>[!NOTE]
>
>As páginas criadas a partir de modelos editáveis não oferecem um modo Design no editor de páginas.
>
>A variável `policies` a árvore de um modelo editável tem a mesma hierarquia que a configuração do modo de design de um modelo estático em:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>A configuração do modo de design de um modelo estático foi definida por componente de página.

### Políticas da página {#page-policies}

As políticas de página permitem definir a variável [política de conteúdo](#content-policies) para a página (parsys principal), no modelo ou nas páginas resultantes.

### Ativação e permissão de um modelo para uso {#enabling-and-allowing-a-template-for-use}

1. **Ativar o modelo**

   Antes de ser usado, um template deve ser ativado por um dos seguintes:

   * [Habilitação do modelo](/help/sites-authoring/templates.md#enablingatemplateauthor) do **Modelos** console.

   * Definir a propriedade de status na variável `jcr:content` nó.

      * Por exemplo, em:
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina a propriedade:

         * Nome: status
         * Tipo: String
         * Valor: `enabled`

1. **Modelos permitidos**

   * [Defina os caminhos do Modelo permitidos no **Propriedades da página**](/help/sites-authoring/templates.md#allowing-a-template-author) da página apropriada ou da página raiz de uma subramificação.
   * Defina a propriedade:
     `cq:allowedTemplates`
No `jcr:content` nó da ramificação necessária.

   Por exemplo, com um valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de conteúdo resultante {#resultant-content-pages}

Páginas criadas a partir de modelos editáveis:

* São criados com uma subárvore que é mesclada de `structure` e `initial` no modelo

* Ter referências às informações mantidas no modelo e no tipo de modelo. Você pode obter essa funcionalidade com um `jcr:content` com as propriedades:

   * `cq:template`
Fornece a referência dinâmica ao modelo real; permite que as alterações no modelo sejam refletidas nas páginas reais.

   * `cq:templateType`
Fornece uma referência ao tipo de template.

![chlimage_1-71](assets/chlimage_1-71.png)

O diagrama acima mostra como os modelos, o conteúdo e os componentes se inter-relacionam:

* Controlador - `/content/<my-site>/<my-page>`
A página resultante que faz referência ao modelo. O conteúdo controla todo o processo. De acordo com as definições, ele acessa o modelo e os componentes apropriados.

* Configuração - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
A variável [modelo e políticas de conteúdo relacionado](#template-definitions) defina a configuração da página.

* Modelo - Pacotes OSGi O [Pacotes OSGi](/help/sites-deploying/osgi-configuration-settings.md) implementar a funcionalidade.

* Exibir - `/apps/<my-site>/components`
Nos ambientes do autor e de publicação, o conteúdo é renderizado por [componentes](/help/sites-developing/components.md).

Ao processar uma página:

* **Modelos**:

   * A variável `cq:template` propriedade de seu `jcr:content` é referenciado para acessar o modelo que corresponde a essa página.

* **Componentes**:

   * O componente Página mescla as variáveis `structure/jcr:content` árvore do modelo com o `jcr:content` árvore da página.

   * O componente de Página permite que o autor edite apenas os nós da estrutura do modelo que foram sinalizados como editáveis (e quaisquer secundários).
   * Ao renderizar um componente em uma página, o caminho relativo desse componente é retirado do `jcr:content` nó; o mesmo caminho sob o `policies/jcr:content` do modelo é pesquisado.

      * A variável `cq:policy` a propriedade desse nó aponta para a política de conteúdo real (ou seja, ele retém a configuração de design desse componente).

      * Essa funcionalidade permite que você tenha vários templates que reutilizam as mesmas configurações de política de conteúdo.
