---
title: Modelos de página - Editável
seo-title: Page Templates - Editable
description: Modelos editáveis foram introduzidos no, permitem que não desenvolvedores criem e editem modelos, fornecem modelos que mantêm uma conexão dinâmica com qualquer página criada a partir deles e tornam o componente de página mais genérico
seo-description: Editable templates have been introduced to, allow non-developers to create and edit templates, provide templates that retain a dynamic connection to any pages created from them, and make the page component more generic
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: d30bfb9e67d0a2a0e870ee0841ed14060def7756
workflow-type: tm+mt
source-wordcount: '3252'
ht-degree: 10%

---

# Modelos de página - Editável {#page-templates-editable}

Os modelos editáveis foram introduzidos em:

* Permitir autores especializados [criar e editar modelos](/help/sites-authoring/templates.md).

   * Esses autores especializados são chamados de **autores de modelos**
   * Os autores do modelo devem ser membros do `template-authors` grupo.

* Forneça modelos que mantenham uma conexão dinâmica com qualquer página criada a partir delas. Isso garante que todas as alterações no modelo sejam refletidas nas próprias páginas.
* Tornar o componente de página mais genérico para que o componente de página principal possa ser usado sem personalização.

Com modelos editáveis, as partes que fazem uma página são isoladas nos componentes. Você pode configurar as combinações necessárias de componentes em uma interface do usuário, eliminando a necessidade de um novo componente de página ser desenvolvido para cada variação de página.

>[!NOTE]
>
>[Modelos estáticos](/help/sites-developing/page-templates-static.md) também estão disponíveis.

Este documento:

* Fornece uma visão geral da criação de modelos editáveis

   * Para obter detalhes, consulte [Criação de modelos de página](/help/sites-authoring/templates.md)

* Descreve as tarefas de administrador/desenvolvedor necessárias para criar modelos editáveis
* Descreve os fundamentos técnicos dos modelos editáveis

Este documento pressupõe que você já está familiarizado com a criação e edição de modelos. Consulte o documento de criação [Criação de modelos de página](/help/sites-authoring/templates.md), que detalha os recursos de modelos editáveis conforme expostos ao autor do modelo.

>[!NOTE]
>
>O tutorial a seguir também pode ser de interesse para configurar um modelo de página editável em um novo projeto:
>[Introdução ao AEM Sites Parte 2 - Criação de uma página base e um modelo](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Criação de um novo modelo {#creating-a-new-template}

A criação de modelos editáveis é feita principalmente com o [console modelo e editor de modelo](/help/sites-authoring/templates.md) por um autor de modelo. Esta seção fornece uma visão geral desse processo e apresenta uma descrição do que ocorre a nível técnico.

Para obter informações sobre como usar modelos editáveis em um projeto AEM, consulte [Criação de um projeto AEM usando Lazybones](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

Ao criar um novo modelo editável:

1. Crie um [pasta dos modelos](#template-folders). Isso não é obrigatório, mas é uma prática recomendada.
1. Selecione um [tipo de modelo](#template-type). Isso é copiado para criar o [definição de modelo](#template-definitions).

   >[!NOTE]
   >
   >Uma seleção de tipos de modelo é fornecida pronta para uso. Você também pode [criar seus próprios tipos de modelo específicos de site](/help/sites-developing/page-templates-editable.md#creating-template-types) se necessário.

1. Configure a estrutura, as políticas de conteúdo, o conteúdo inicial e o layout do novo template.

   **Estrutura**

   * A estrutura permite definir componentes e conteúdo para o modelo.
   * Os componentes definidos na estrutura do modelo não podem ser movidos em uma página resultante ou excluídos de qualquer página resultante.

      * Se você estiver criando um modelo em uma pasta personalizada fora do conteúdo de amostra We.Retail, poderá escolher Componentes de base ou usar [Componentes principais](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * Se desejar que os autores da página possam adicionar e remover componentes, adicione um sistema de parágrafo ao modelo.
   * Os componentes podem ser desbloqueados e bloqueados novamente para permitir que você defina o conteúdo inicial.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos da estrutura, consulte [Estrutura](/help/sites-developing/page-templates-editable.md#structure) neste documento.

   **Políticas**

   * As políticas de conteúdo definem as propriedades de design de um componente.

      * Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas.
   * Eles são aplicáveis ao modelo (e às páginas criadas com o modelo).

   Para obter detalhes sobre como um autor de modelo define políticas, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos das políticas, consulte [Políticas de conteúdo](/help/sites-developing/page-templates-editable.md#content-policies) neste documento.

   **Conteúdo inicial**

   * O Conteúdo inicial define o conteúdo que será exibido quando uma página for criada pela primeira vez com base no modelo.
   * O conteúdo inicial pode ser editado pelos autores da página.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Para obter detalhes técnicos sobre o conteúdo inicial, consulte [Conteúdo inicial](/help/sites-developing/page-templates-editable.md#initial-content) neste documento.

   **Layout**

   * É possível definir o layout do modelo para um intervalo de dispositivos.
   * O Layout responsivo para modelos funciona como na criação de página.

   Para obter detalhes sobre como um autor de modelo define o layout do modelo, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Para obter detalhes técnicos sobre o layout do modelo, consulte [Layout](/help/sites-developing/page-templates-editable.md#layout) neste documento.

1. Ative o modelo e permita árvores de conteúdo específico.

   * Um modelo pode ser ativado ou desativado para torná-lo disponível ou indisponível para os autores da página.
   * Um modelo pode ser disponibilizado ou indisponibilizado para determinadas ramificações de página.

   Para obter detalhes sobre como um autor de modelo habilita um modelo, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Para obter detalhes técnicos sobre como ativar um modelo, consulte [Ativar e permitir um modelo para nós](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e neste documento

1. Use-o para criar páginas de conteúdo.

   * Ao usar um modelo para criar uma nova página, não há diferenças visíveis e nenhuma indicação entre os modelos estáticos e editáveis.
   * Para o autor da página, o processo é transparente.

   Para obter detalhes sobre como um autor de página usa modelos para criar uma página, consulte [Criar e organizar páginas](/help/sites-authoring/managing-pages.md#templates).

   Para obter detalhes técnicos sobre como criar páginas com modelos editáveis, consulte [Páginas de conteúdo resultante](/help/sites-developing/page-templates-editable.md#resultant-content-pages) neste documento.

>[!TIP]
>
>Nunca insira qualquer informação que precise ser internacionalizada em um modelo. Para fins de internalização, o [recurso de localização dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=pt-BR) são recomendadas.

>[!NOTE]
>
>Os modelos são ferramentas eficientes para simplificar o fluxo de trabalho de criação de página. No entanto, usar modelos em excesso pode sobrecarregar os autores e tornar confusa a criação da página. Uma boa regra geral é manter o número de modelos abaixo de 100.
>
>A Adobe não recomenda ter mais de 1000 modelos devido a possíveis impactos no desempenho.

>[!NOTE]
>
>A biblioteca cliente do editor assume a presença do `cq.shared` namespace nas páginas de conteúdo e se estiver ausente do erro de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` resultará em .
>
>Todas as páginas de conteúdo de exemplo contêm `cq.shared`, portanto, qualquer conteúdo baseado neles inclui automaticamente `cq.shared`. No entanto, se você decidir criar suas próprias páginas de conteúdo do zero sem basear-nas no conteúdo de amostra, deverá incluir a variável `cq.shared` namespace.
>
>Consulte [Usar bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Pastas de modelo {#template-folders}

Para organizar seus modelos, você pode usar as seguintes pastas:

* **global**
* Específico do site As pastas específicas do site que você cria para organizar seus modelos são criadas com uma conta que contém privilégios de administrador.

>[!NOTE]
>
>Mesmo que você possa aninhar suas pastas, quando o usuário as visualiza no **Modelos** Eles são apresentados como uma estrutura plana.

Em uma instância padrão do AEM, a pasta **global** já existe no console modelo. Isso mantém modelos padrão e atua como um fallback se nenhuma política e/ou tipo de modelo for localizado na pasta atual. Você pode adicionar seus modelos padrão a esta pasta ou criar uma nova pasta (recomendado).

>[!NOTE]
>
>É prática recomendada criar uma nova pasta para manter seus modelos personalizados e não usar a pasta global.

>[!CAUTION]
>
>As pastas devem ser criadas por um usuário com `admin` direitos.

Os tipos e políticas de modelo são herdados em todas as pastas de acordo com a seguinte ordem de precedência:

1. A pasta atual.
1. Pai(s) da pasta atual.
1. `/conf/global`
1. `/apps`
1. `/libs`

Uma lista de todas as entradas permitidas é criada. Se alguma configuração se sobrepõe ( `path`/ `label`), somente a instância mais próxima da pasta atual é apresentada ao usuário.

Para criar uma nova pasta, você pode fazer o seguinte:

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

   * Valor: O título (para a pasta) que você deseja exibir no **Modelos** console.

1. Em *adição* às permissões e privilégios de criação padrão (por exemplo, `content-authors`) agora é necessário atribuir grupos e definir os direitos de acesso necessários (ACLs) para que os autores possam criar modelos na nova pasta.

   O `template-authors` grupo é o grupo padrão que precisa ser atribuído. Consulte a seguinte seção [ACLs e grupos](/help/sites-developing/page-templates-editable.md#acls-and-groups) para obter detalhes.

   Consulte [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management) para obter detalhes completos sobre a gestão e atribuição de direitos de acesso.

### Usar o navegador de configuração {#using-the-configuration-browser}

1. Ir para **Navegação global** -> **Ferramentas** > **Navegador de configuração**.

   As pastas existentes são listadas à esquerda, incluindo o **global** pasta.

1. Clique em **Criar**.
1. No **Criar configuração** os seguintes campos precisam ser configurados:

   * **Título**: Forneça um título para a pasta de configuração
   * **Modelos editáveis**: Marque para permitir modelos editáveis nesta pasta

1. Clique em **Criar**

>[!NOTE]
>
>No Navegador de configuração, você pode editar a pasta global e ativar o **Modelos editáveis** , se desejar criar modelos nessa pasta, no entanto, essa não é a prática recomendada.
>
>Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) documentação para obter mais informações.

### ACLs e grupos {#acls-and-groups}

Depois que as pastas de modelo são criadas (via CRXDE ou com o Navegador de configuração), as ACLs devem ser definidas para os grupos apropriados para as pastas de modelo para garantir a segurança adequada.

As pastas de modelo para a [Implementação de referência We.Retail](/help/sites-developing/we-retail.md) pode ser usado como exemplo.

#### O Grupo de autores de modelo {#the-template-authors-group}

O `template-authors` grupo é o grupo usado para gerenciar o acesso a modelos e vem como padrão com AEM, mas está vazio. Os usuários devem ser adicionados ao grupo para o projeto/site.

>[!CAUTION]
>
>O `template-authors` grupo é *only* para usuários que devem ser capazes de criar novos templates.
>
>A edição de modelos é muito poderosa e, se não for feita, os modelos existentes podem ser quebrados. Portanto, essa função deve ser focada e incluir apenas usuários qualificados.

A tabela a seguir detalha as permissões necessárias para a edição de modelo.

<table>
 <tbody>
  <tr>
   <th>Caminho </th>
   <th>Função / Grupo</th>
   <th>Permissões<br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores do modelo<br /> </td>
   <td>ler, escrever, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em um site específico <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>leitura</td>
   <td>O Usuário Anônimo da Web deve ler modelos ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>replicateContent autores precisam ativar os modelos de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>ler, escrever, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em um site específico <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>leitura</td>
   <td>O Usuário Anônimo da Web deve ler as políticas ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo precisam ativar as políticas de um modelo de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor do modelo</td>
   <td>leitura</td>
   <td>O autor do modelo cria um novo modelo com base em um dos tipos de modelo predefinidos.</td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>nenhum</td>
   <td>O Usuário Anônimo da Web não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

Esse padrão `template-authors` abrange apenas as configurações do projeto, em que todas as `template-authors` os membros têm permissão para acessar e criar todos os modelos. Para configurações mais complexas, onde vários grupos de autores de modelo são necessários para separar o acesso a modelos, mais grupos de autores de modelo personalizados devem ser criados. No entanto, as permissões para os grupos de autores de modelo ainda seriam as mesmas.

#### Modelos herdados em /conf/global {#legacy-templates-under-conf-global}

Os modelos não devem mais ser armazenados em `/conf/global`, no entanto, para algumas instalações herdadas ainda pode haver modelos neste local. SOMENTE em tais situações herdadas deve `/conf/global` os caminhos devem ser configurados explicitamente.

<table>
 <tbody>
  <tr>
   <th>Caminho </th>
   <th>Função / Grupo</th>
   <th>Permissões<br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autores do modelo</td>
   <td>ler, escrever, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>leitura</td>
   <td>O Usuário Anônimo da Web deve ler modelos ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo precisam ativar os modelos de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>ler, escrever, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>leitura</td>
   <td>O Usuário Anônimo da Web deve ler as políticas ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo precisam ativar as políticas de um modelo de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autor do modelo</td>
   <td>leitura</td>
   <td>O autor do modelo cria um novo modelo com base em um dos tipos de modelo predefinidos</td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>nenhum</td>
   <td>O Usuário Anônimo da Web não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

## Tipo de modelo {#template-type}

Ao criar um novo modelo, você precisa especificar um tipo de modelo:

* Os tipos de modelo fornecem modelos para um modelo de maneira eficaz. Ao criar um novo template, a estrutura e o conteúdo inicial do tipo de template selecionado são usados para criar o novo template.

   * O tipo de modelo é copiado para criar o modelo.
   * Após a cópia, a única conexão entre o modelo e o tipo de modelo é uma referência estática para fins de informação.

* Os tipos de templates permitem definir:

   * O tipo de recurso do componente de página.
   * A política do nó raiz, que define os componentes permitidos no editor de modelo.
   * É recomendável definir os pontos de interrupção para a grade responsiva e a configuração do emulador móvel no tipo de modelo. Isso é opcional, pois a configuração também pode ser definida no modelo individual (consulte [Tipo de modelo e grupos de dispositivos móveis](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM fornece uma pequena seleção de tipos de modelo prontos para uso, como Página do HTML5 e Página do formulário adaptável.

   * Exemplos adicionais são fornecidos como parte do [We.Retail](/help/sites-developing/we-retail.md) conteúdo de exemplo.

* Os tipos de modelo geralmente são definidos pelos desenvolvedores.

Os tipos de modelo prontos para uso são armazenados em:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Você não deve alterar nada na variável `/libs` caminho. Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).

Os tipos de modelo específicos do site devem ser armazenados no local comparável de:

* `/apps/settings/wcm/template-types`

As definições dos tipos de modelos personalizados devem ser armazenadas em pastas definidas pelo usuário (recomendado) ou, alternativamente, em `global`. Por exemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Os tipos de modelo devem respeitar a estrutura correta da pasta (ou seja, `/settings/wcm/...`), caso contrário, os tipos de modelo não serão encontrados.

### Tipo de modelo e grupos de dispositivos móveis {#template-type-and-mobile-device-groups-br}

O [grupos de dispositivos](/help/sites-developing/mobile.md#device-groups) usado para um modelo editável (definido como caminho relativo da propriedade) `cq:deviceGroups`) defina quais dispositivos móveis estão disponíveis como emuladores no [modo de layout](/help/sites-authoring/responsive-layout.md) da criação de página. Esse valor pode ser definido em dois lugares:

* No tipo de modelo editável
* No modelo editável

Ao criar um novo modelo editável, o valor é copiado do tipo de modelo para o modelo individual. Se o valor não estiver definido no tipo , ele poderá ser definido no template. Depois que um template é criado, não há herança do tipo para o template.

>[!CAUTION]
>
>O valor de `cq:deviceGroups` deve ser definido como um caminho relativo, como `mobile/groups/responsive` e não como um caminho absoluto, como `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Com [modelos estáticos](/help/sites-developing/page-templates-static.md), o valor de `cq:deviceGroups` pode ser definido na raiz do site.
>
>Com modelos editáveis, esse valor agora é armazenado no nível do modelo e não é compatível no nível da raiz da página.

### Criação de tipos de modelo {#creating-template-types}

Se você criou um template que pode servir como base de outros templates, é possível copiar esse template como um tipo de template.

1. Criar um modelo como você faria com qualquer modelo editável [conforme documentado aqui](/help/sites-authoring/templates.md#creating-a-new-template-template-author), que servirá de base para o seu tipo de modelo.
1. Usando o CRXDE Lite, copie o modelo recém-criado da `templates` para `template-types` nó sob o [pasta de modelos](/help/sites-developing/page-templates-editable.md#template-folders).
1. Excluir o modelo do `templates` nó sob o [pasta de modelos](/help/sites-developing/page-templates-editable.md#template-folders).
1. Na cópia do modelo que está sob o `template-types` nó, excluir tudo `cq:template` e `cq:templateType` propriedades de todas `jcr:content` nós.

Você também pode desenvolver seu próprio tipo de modelo usando um modelo editável de exemplo como base, disponível no GitHub.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-sites-example-custom-template-type no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definições de modelo {#template-definitions}

Definições para modelos editáveis são armazenadas [pastas definidas pelo usuário](/help/sites-developing/page-templates-editable.md#template-folders) (recomendado) ou alternativamente em `global`. Por exemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

O nó raiz do modelo é do tipo `cq:Template` com uma estrutura esquelética de:

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

Esse nó contém as propriedades do template:

* **Nome**: `jcr:title`

* **Nome**: `status`

   * **Tipo**: `String`

   * **Valor**: `draft`, `enabled` ou `disabled`

### Estrutura {#structure}

Define a estrutura da página resultante:

* É mesclado com o conteúdo inicial ( `/initial`) ao criar uma nova página.
* As alterações feitas na estrutura serão refletidas em qualquer página criada com o modelo.
* O `root` ( `structure/jcr:content/root`) define a lista de componentes que estarão disponíveis na página resultante.

   * Os componentes definidos na estrutura do modelo não podem ser movidos para ou excluídos de qualquer página resultante.
   * Depois que um componente é desbloqueado, a variável `editable` está definida como `true`.

   * Depois que um componente que já contém conteúdo for desbloqueado, esse conteúdo será movido para o `initial` ramificação.

* O `cq:responsive` nó contém definições para o layout responsivo.

### Conteúdo inicial {#initial-content}

Define o conteúdo inicial que uma nova página terá após a criação:

* Contém um `jcr:content` nó que é copiado para qualquer página nova.
* É mesclado com a estrutura ( `/structure`) ao criar uma nova página.
* Nenhuma página existente será atualizada se o conteúdo inicial for alterado após a criação.
* O `root` contém uma lista de componentes para definir o que estará disponível na página resultante.
* Se o conteúdo for adicionado a um componente no modo de estrutura e esse componente for subsequentemente desbloqueado (ou vice-versa), esse conteúdo será usado como conteúdo inicial.

### Layout {#layout}

When [editar um modelo, você pode definir o layout](/help/sites-authoring/templates.md), isso usa [layout responsivo padrão](/help/sites-authoring/responsive-layout.md) isso também pode ser [configurado](/help/sites-administering/configuring-responsive-layout.md).

### Políticas de conteúdo {#content-policies}

As políticas do conteúdo (ou design) definem as propriedades do design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas. Eles são aplicáveis ao modelo (e às páginas criadas com o modelo). As políticas de conteúdo podem ser criadas e selecionadas no editor de modelo.

* A propriedade `cq:policy`, no `root` nó
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornece uma referência relativa à política de conteúdo para o sistema de parágrafo da página.

* A propriedade `cq:policy`, nos nós explícitos de componente em `root`, fornecer links para as políticas dos componentes individuais.

* As definições reais de política são armazenadas em:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Os caminhos das definições de política dependem do caminho do componente. `cq:policy` mantém uma referência relativa à própria configuração.

>[!NOTE]
>
>As páginas criadas a partir de modelos editáveis não oferecem um modo de Design no editor de páginas.
>
>O `policies` a árvore de um modelo editável tem a mesma hierarquia que a configuração do modo de design de um modelo estático em:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>A configuração do modo de design de um modelo estático foi definida por componente de página.

### Políticas da página {#page-policies}

As políticas de página permitem definir a variável [política de conteúdo](#content-policies) para a página (parsys principal), no modelo ou nas páginas resultantes.

### Ativar e permitir o uso de um modelo {#enabling-and-allowing-a-template-for-use}

1. **Ativar o modelo**

   Antes de um modelo poder ser usado, ele deve ser habilitado por:

   * [Ativação do template](/help/sites-authoring/templates.md#enablingatemplateauthor) do **Modelos** console.

   * Definir a propriedade de status na `jcr:content` nó .

      * Por exemplo, em:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina a propriedade :

         * Nome: status
         * Tipo: String
         * Valor: `enabled`

1. **Modelos permitidos**

   * [Defina os caminhos de Modelo permitidos no **Propriedades da página**](/help/sites-authoring/templates.md#allowing-a-template-author) da página ou página raiz apropriada de uma subramificação.
   * Defina a propriedade :
      `cq:allowedTemplates`
No 
`jcr:content` nó da ramificação necessária.
   Por exemplo, com um valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de conteúdo resultante {#resultant-content-pages}

Páginas criadas a partir de modelos editáveis:

* São criados com uma subárvore que é unida a partir de `structure` e `initial` no modelo

* Ter referências às informações contidas no modelo e tipo de modelo. Isso é feito com uma `jcr:content` com as propriedades:

   * `cq:template`
Fornece a referência dinâmica ao modelo real; permite que as alterações no modelo sejam refletidas nas páginas reais.

   * `cq:templateType`
Fornece uma referência ao tipo de modelo.

![chlimage_1-71](assets/chlimage_1-71.png)

O diagrama acima mostra como os modelos, o conteúdo e os componentes se relacionam:

* Controlador - `/content/<my-site>/<my-page>`
A página resultante que faz referência ao modelo. O conteúdo controla todo o processo. De acordo com as definições, ele acessa o modelo e os componentes apropriados.

* Configuração - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
O [modelo e políticas de conteúdo relacionadas](#template-definitions) defina a configuração da página.

* Modelo - Pacotes OSGi O [Pacotes OSGI](/help/sites-deploying/osgi-configuration-settings.md) implemente a funcionalidade.

* Exibir - `/apps/<my-site>/components`
Nos ambientes do autor e de publicação, o conteúdo é renderizado por [componentes](/help/sites-developing/components.md).

Ao renderizar uma página:

* **Modelos**:

   * O `cq:template` propriedade da `jcr:content` será referenciado para acessar o modelo que corresponde a essa página.

* **Componentes**:

   * O componente de página mesclará o `structure/jcr:content` árvore do modelo com o `jcr:content` da página.

   * O componente de página permitirá que o autor edite apenas os nós da estrutura do modelo que foram sinalizados como editáveis (bem como qualquer filho).
   * Ao renderizar um componente em uma página, o caminho relativo desse componente será retirado do `jcr:content` nó; o mesmo caminho sob o `policies/jcr:content` O nó do template será pesquisado.

      * O `cq:policy` a propriedade desse nó aponta para a política de conteúdo real (ou seja, contém a configuração de design desse componente).

      * Isso permite ter vários modelos que reutilizam as mesmas configurações de política de conteúdo.
