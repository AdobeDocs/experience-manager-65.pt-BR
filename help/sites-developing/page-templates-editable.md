---
title: Modelos de página - Editável
seo-title: Modelos de página - Editável
description: Modelos editáveis foram introduzidos em, permitem que não desenvolvedores criem e editem modelos, fornecem modelos que retêm uma conexão dinâmica com quaisquer páginas criadas a partir deles e tornam o componente de página mais genérico
seo-description: Modelos editáveis foram introduzidos em, permitem que não desenvolvedores criem e editem modelos, fornecem modelos que retêm uma conexão dinâmica com quaisquer páginas criadas a partir deles e tornam o componente de página mais genérico
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
translation-type: tm+mt
source-git-commit: 149cdd00f745ad897f506434d7156b8147ef5bae
workflow-type: tm+mt
source-wordcount: '3285'
ht-degree: 8%

---


# Modelos de página - editável {#page-templates-editable}

Modelos editáveis foram introduzidos em:

* Permita que autores especializados [criem e editem modelos](/help/sites-authoring/templates.md).

   * Esses autores especializados são chamados de **autores de modelo**
   * Os autores de modelo devem ser membros do grupo `template-authors`.

* Forneça modelos que mantenham uma conexão dinâmica com quaisquer páginas criadas a partir delas. Isso garante que quaisquer alterações no modelo sejam refletidas nas próprias páginas.
* Torne o componente de página mais genérico para que o componente de página principal possa ser usado sem personalização.

Com modelos editáveis, as partes que fazem uma página são isoladas dentro dos componentes. Você pode configurar as combinações necessárias de componentes em uma interface do usuário, eliminando a necessidade de um novo componente de página ser desenvolvido para cada variação de página.

>[!NOTE]
>
>[Estão também disponíveis ](/help/sites-developing/page-templates-static.md) modelos estáticos.

Este documento:

* Fornece uma visão geral da criação de modelos editáveis

   * Para obter detalhes, consulte [Criação de modelos de página](/help/sites-authoring/templates.md)

* Descreve as tarefas de administrador/desenvolvedor necessárias para criar modelos editáveis
* Descreve os fundamentos técnicos dos modelos editáveis

Este documento supõe que você já esteja familiarizado com a criação e edição de modelos. Consulte o documento de criação [Criação de modelos de página](/help/sites-authoring/templates.md), que detalha os recursos de modelos editáveis como expostos ao autor do modelo.

>[!NOTE]
>
>O tutorial a seguir também pode ser de interesse para configurar um modelo de página editável em um novo projeto:
>[Introdução ao AEM Sites Parte 2 - Criação de uma página básica e um modelo](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Criando um Novo Modelo {#creating-a-new-template}

A criação de modelos editáveis é feita principalmente com o console [modelo e o editor de modelo](/help/sites-authoring/templates.md) por um autor de modelo. Esta seção apresenta uma visão geral deste processo e apresenta uma descrição do que ocorre a nível técnico.

Para obter informações sobre como usar modelos editáveis em um projeto AEM, consulte [Criar um projeto AEM usando Lazybones](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

Ao criar um novo modelo editável:

1. Crie uma pasta [para os modelos](#template-folders). Isso não é obrigatório, mas é uma prática recomendada.
1. Selecione um tipo de modelo [a1/>. ](#template-type) Isso é copiado para criar a definição do modelo [a1/>.](#template-definitions)

   >[!NOTE]
   >
   >Uma seleção de tipos de modelo é fornecida prontamente. Você também pode [criar seus próprios tipos de modelo específicos do site](/help/sites-developing/page-templates-editable.md#creating-template-types), se necessário.

1. Configure a estrutura, as políticas de conteúdo, o conteúdo inicial e o layout do novo modelo.

   **Estrutura**

   * A estrutura permite que você defina componentes e conteúdo para seu modelo.
   * Os componentes definidos na estrutura do modelo não podem ser movidos em uma página resultante ou excluídos de qualquer página resultante.

      * Se você estiver criando um modelo em uma pasta personalizada fora do conteúdo de amostra We.Retail, poderá escolher Componentes do Foundation ou usar [Componentes Principais](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * Se desejar que os autores da página possam adicionar e remover componentes, adicione um sistema de parágrafo ao modelo.
   * Os componentes podem ser desbloqueados e bloqueados novamente para permitir que você defina o conteúdo inicial.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos da estrutura, consulte [Estrutura](/help/sites-developing/page-templates-editable.md#structure) neste documento.

   **Políticas**

   * As políticas de conteúdo definem as propriedades de design de um componente.

      * Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas.
   * Eles são aplicáveis ao modelo (e às páginas criadas com o modelo).

   Para obter detalhes sobre como um autor de modelo define políticas, consulte [Criando Modelos de Página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

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

1. Habilite o modelo e, em seguida, permita-o para árvores de conteúdo específicas.

   * Um modelo pode ser ativado ou desativado para torná-lo disponível ou indisponível para autores de página.
   * Um modelo pode ser disponibilizado ou indisponibilizado para determinadas ramificações de página.

   Para obter detalhes sobre como um autor de modelo ativa um modelo, consulte [Criação de modelos de página](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Para obter detalhes técnicos sobre como ativar um modelo, consulte [Ativar e Permitir um Modelo para Us](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e neste documento

1. Use-o para criar páginas de conteúdo.

   * Ao usar um modelo para criar uma nova página, não há diferenças visíveis e nenhuma indicação entre os modelos estáticos e editáveis.
   * Para o autor da página, o processo é transparente.

   Para obter detalhes sobre como um autor de página usa modelos para criar uma página, consulte [Criação e organização de páginas](/help/sites-authoring/managing-pages.md#templates).

   Para obter detalhes técnicos sobre como criar páginas com modelos editáveis, consulte [Páginas de conteúdo resultante](/help/sites-developing/page-templates-editable.md#resultant-content-pages) neste documento.

>[!TIP]
>
>Nunca insira qualquer informação que precise ser internacionalizada em um modelo. Para fins de internalização, o recurso [localização dos Componentes Principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) é recomendado.

>[!NOTE]
>
>Os modelos são ferramentas poderosas para simplificar o fluxo de trabalho de criação de página. No entanto, muitos modelos podem sobrecarregar os autores e tornar a criação da página confusa. Uma boa regra é manter o número de modelos abaixo de 100.
>
>O Adobe não recomenda ter mais de 1000 modelos devido a possíveis impactos no desempenho.

>[!NOTE]
>
>A biblioteca do cliente do editor assume a presença da namespace `cq.shared` nas páginas de conteúdo e, se ela não estiver presente, o erro do JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` resultará.
>
>Todas as páginas de conteúdo de amostra contêm `cq.shared`, portanto, qualquer conteúdo baseado nelas inclui automaticamente `cq.shared`. No entanto, se você decidir criar suas próprias páginas de conteúdo do zero sem baseá-las no conteúdo de amostra, deverá incluir a namespace `cq.shared`.
>
>Consulte [Usando bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Pastas de Modelo {#template-folders}

Para organizar seus modelos, você pode usar as seguintes pastas:

* **global**
* Específico do site
As pastas específicas do site que você cria para organizar seus modelos são criadas com uma conta com privilégios de administrador.

>[!NOTE]
>
>Mesmo que você possa aninhar suas pastas, quando o usuário as visualização no console **Modelos**, elas são apresentadas como uma estrutura simples.

Em uma instância padrão do AEM, a pasta **global** já existe no console modelo. Isso mantém modelos padrão e atua como um fallback se nenhuma política e/ou tipo de modelo for localizado na pasta atual. Você pode adicionar seus modelos padrão a esta pasta ou criar uma nova pasta (recomendado).

>[!NOTE]
>
>É prática recomendada criar uma nova pasta para manter seus modelos personalizados e não usar a pasta global.

>[!CAUTION]
>
>As pastas devem ser criadas por um usuário com direitos `admin`.

Os tipos de modelo e as políticas são herdados em todas as pastas de acordo com a seguinte ordem de precedência:

1. A pasta atual.
1. Pai(s) da pasta atual.
1. `/conf/global`
1. `/apps`
1. `/libs`

Uma lista de todas as entradas permitidas é criada. Se qualquer configuração se sobrepuser ( `path`/ `label`), somente a instância mais próxima da pasta atual será apresentada ao usuário.

Para criar uma nova pasta, você pode:

* Programaticamente ou com CRXDE Lite
* Usando o navegador de configuração

## Usando CRXDE Lite {#using-crxde-lite}

1. Uma nova pasta (em /conf) pode ser criada para sua instância de forma programática ou com CRXDE Lite.

   Deve ser utilizada a seguinte estrutura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. Em seguida, é possível definir as seguintes propriedades no nó raiz da pasta:

   `<your-folder-name> [sling:Folder]`

   Nome: `jcr:title`

   * Tipo: `String`

   * Valor: O título (para a pasta) que você deseja exibir no console **Modelos**.

1. Em *adicione* às permissões e privilégios de criação padrão (por exemplo, `content-authors`) agora é necessário atribuir grupos e definir os direitos de acesso (ACLs) necessários para que seus autores possam criar modelos na nova pasta.

   O grupo `template-authors` é o grupo padrão que precisa ser atribuído. Consulte a seção a seguir [ACLs e grupos](/help/sites-developing/page-templates-editable.md#acls-and-groups) para obter detalhes.

   Consulte [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management) para obter detalhes completos sobre como gerenciar e atribuir direitos de acesso.

### Usando o navegador de configuração {#using-the-configuration-browser}

1. Vá para **Navegação Global** -> **Ferramentas** > **Navegador de Configuração**.

   As pastas existentes são listadas à esquerda, incluindo a pasta **global**.

1. Clique em **Criar**.
1. Na caixa de diálogo **Criar configuração**, os seguintes campos precisam ser configurados:

   * **Título**: Fornecer um título para a pasta de configuração
   * **Modelos** editáveis: Clique para permitir modelos editáveis nesta pasta

1. Clique em **Criar**

>[!NOTE]
>
>No Navegador de configuração, você pode editar a pasta global e ativar a opção **Modelos editáveis** se desejar criar modelos dentro dessa pasta, no entanto, essa não é a prática recomendada.
>
>Consulte a documentação [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.

### ACLs e grupos {#acls-and-groups}

Depois que as pastas de modelo são criadas (via CRXDE ou com o Navegador de configuração), as ACLs devem ser definidas para os grupos apropriados para as pastas de modelo para garantir a segurança adequada.

As pastas de modelo para a [implementação de referência We.Retail](/help/sites-developing/we-retail.md) podem ser usadas como exemplo.

#### O Grupo de autores de modelo {#the-template-authors-group}

O grupo `template-authors` é o grupo usado para gerenciar o acesso aos modelos e vem como padrão com AEM, mas está vazio. Os usuários devem ser adicionados ao grupo para o projeto/site.

>[!CAUTION]
>
>O grupo `template-authors` é *only* para usuários que devem ser capazes de criar novos modelos.
>
>A edição de modelos é muito poderosa e, se não for feita corretamente, os modelos existentes podem ser quebrados. Portanto, essa função deve ser focada e incluir apenas usuários qualificados.

A tabela a seguir detalha as permissões necessárias para a edição de modelos.

<table>
 <tbody>
  <tr>
   <th>Caminho</th>
   <th>Função / Grupo</th>
   <th>Permissões <br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores do modelo<br /> </td>
   <td>ler, escrever, replicar</td>
   <td>Criadores de modelos que criam, leem, atualizam, excluem e replicam modelos em espaço <code>/conf</code> específico do site</td>
  </tr>
  <tr>
   <td>Usuário da Web anônimo</td>
   <td>leitura</td>
   <td>Usuário da Web anônimo deve ler modelos ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>replicateOs autores de conteúdo precisam ativar os modelos de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>ler, escrever, replicar</td>
   <td>Criadores de modelos que criam, leem, atualizam, excluem e replicam modelos em espaço <code>/conf</code> específico do site</td>
  </tr>
  <tr>
   <td>Usuário da Web anônimo</td>
   <td>leitura</td>
   <td>Usuário da Web anônimo deve ler as políticas ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo precisam ativar as políticas de um modelo de página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor do modelo</td>
   <td>leitura</td>
   <td>O autor do modelo cria um novo modelo com base em um dos tipos de modelo predefinidos.</td>
  </tr>
  <tr>
   <td>Usuário da Web anônimo</td>
   <td>nenhum</td>
   <td>O Usuário Anônimo da Web não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

Este grupo padrão `template-authors` abrange apenas as configurações do projeto, onde todos os membros `template-authors` têm permissão para acessar e criar todos os modelos. Para configurações mais complexas, onde vários grupos de autores de modelo são necessários para separar o acesso a modelos, mais grupos de autores de modelo personalizados devem ser criados. No entanto, as permissões para os grupos de autores de modelo ainda seriam as mesmas.

#### Modelos herdados em /conf/global {#legacy-templates-under-conf-global}

Os modelos não devem mais ser armazenados em `/conf/global`, no entanto, para algumas instalações herdadas ainda pode haver modelos neste local. SOMENTE nessas situações herdadas os seguintes caminhos `/conf/global` devem ser configurados explicitamente.

<table>
 <tbody>
  <tr>
   <th>Caminho</th>
   <th>Função / Grupo</th>
   <th>Permissões <br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autores do modelo</td>
   <td>ler, escrever, replicar</td>
   <td>Criadores de modelos que criam, leem, atualizam, excluem e replicam modelos em <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuário da Web anônimo</td>
   <td>leitura</td>
   <td>Usuário da Web anônimo deve ler modelos ao renderizar uma página</td>
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
   <td>Criadores de modelos que criam, leem, atualizam, excluem e replicam modelos em <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuário da Web anônimo</td>
   <td>leitura</td>
   <td>Usuário da Web anônimo deve ler as políticas ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo precisam ativar as políticas de um modelo de página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autor do modelo</td>
   <td>leitura</td>
   <td>O autor do modelo cria um novo modelo com base em um dos tipos de modelo predefinidos</td>
  </tr>
  <tr>
   <td>Usuário da Web anônimo</td>
   <td>nenhum</td>
   <td>O Usuário Anônimo da Web não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

## Tipo de Modelo {#template-type}

Ao criar um novo modelo, é necessário especificar um tipo de modelo:

* Os tipos de modelo fornecem modelos para um modelo. Ao criar um novo modelo, a estrutura e o conteúdo inicial do tipo de modelo selecionado são usados para criar o novo modelo.

   * O tipo de modelo é copiado para criar o modelo.
   * Após a cópia, a única conexão entre o modelo e o tipo de modelo é uma referência estática para fins de informação.

* Os tipos de modelo permitem que você defina:

   * O tipo de recurso do componente de página.
   * A política do nó raiz, que define os componentes permitidos no editor de modelo.
   * É recomendável definir os pontos de interrupção para a grade responsiva e a configuração do emulador móvel no tipo de modelo. Isso é opcional, pois a configuração também pode ser definida no modelo individual (consulte [Tipo de modelo e Grupos de dispositivos móveis](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM fornece uma pequena seleção de tipos de modelo prontos para uso, como Página HTML5 e Página de formulário adaptável.

   * Exemplos adicionais são fornecidos como parte do conteúdo de amostra [We.Retail](/help/sites-developing/we-retail.md).

* Os tipos de modelo são tipicamente definidos pelos desenvolvedores.

Os tipos de modelo predefinidos são armazenados em:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Você não deve alterar nada no caminho `/libs`. Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar uma correção ou um pacote de recursos).

Os tipos de modelo específicos do site devem ser armazenados no local comparável de:

* `/apps/settings/wcm/template-types`

As definições para seus tipos de modelos personalizados devem ser armazenadas em pastas definidas pelo usuário (recomendado) ou alternativamente em `global`. Por exemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Os tipos de modelo devem respeitar a estrutura correta de pastas (ou seja, `/settings/wcm/...`), caso contrário, os tipos de modelo não serão encontrados.

### Tipo de Modelo e Grupos de Dispositivos Móveis {#template-type-and-mobile-device-groups-br}

Os [grupos de dispositivos](/help/sites-developing/mobile.md#device-groups) usados para um modelo editável (definidos como caminho relativo da propriedade `cq:deviceGroups`) definem quais dispositivos móveis estão disponíveis como emuladores no [modo de layout](/help/sites-authoring/responsive-layout.md) da criação de página. Esse valor pode ser definido em dois locais:

* No tipo de modelo editável
* No modelo editável

Ao criar um novo modelo editável, o valor é copiado do tipo de modelo para o modelo individual. Se o valor não for definido no tipo, ele poderá ser definido no modelo. Depois que um modelo é criado, não há herança do tipo para o modelo.

>[!CAUTION]
>
>O valor de `cq:deviceGroups` deve ser definido como um caminho relativo, como `mobile/groups/responsive`, e não como um caminho absoluto, como `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Com [modelos estáticos](/help/sites-developing/page-templates-static.md), o valor de `cq:deviceGroups` pode ser definido na raiz do site.
>
>Com modelos editáveis, esse valor agora é armazenado no nível do modelo e não é suportado no nível raiz da página.

### Criando Tipos de Modelo {#creating-template-types}

Se você tiver criado um modelo que possa servir como a base de outros modelos, poderá copiar esse modelo como um tipo de modelo.

1. Crie um modelo como você faria com qualquer modelo editável [conforme documentado aqui](/help/sites-authoring/templates.md#creating-a-new-template-template-author), que servirá de base para o seu tipo de modelo.
1. Usando o CRXDE Lite, copie o modelo recém-criado do nó `templates` para o nó `template-types` na pasta de modelo [](/help/sites-developing/page-templates-editable.md#template-folders).
1. Exclua o modelo do nó `templates` na pasta de modelo [](/help/sites-developing/page-templates-editable.md#template-folders).
1. Na cópia do modelo que está sob o nó `template-types`, exclua todas as propriedades `cq:template` e `cq:templateType` `jcr:content`.

Você também pode desenvolver seu próprio tipo de modelo usando um modelo editável de exemplo como base, disponível no GitHub.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir um projeto aem-sites-example-custom-template-type no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definições de Modelo {#template-definitions}

As definições para modelos editáveis são armazenadas [pastas definidas pelo usuário](/help/sites-developing/page-templates-editable.md#template-folders) (recomendado) ou alternativamente em `global`. Por exemplo:

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

Este nó contém propriedades para o modelo:

* **Nome**: `jcr:title`

* **Nome**: `status`

   * ``**Tipo**: `String`

   * **Valor**:  `draft`,  `enabled` ou  `disabled`

### Estrutura {#structure}

Define a estrutura da página resultante:

* É unido ao conteúdo inicial ( `/initial`) ao criar uma nova página.
* As alterações feitas na estrutura serão refletidas em qualquer página criada com o modelo.
* O nó `root` ( `structure/jcr:content/root`) define a lista de componentes que estarão disponíveis na página resultante.

   * Os componentes definidos na estrutura do modelo não podem ser movidos para nenhuma página resultante ou excluídos dela.
   * Depois que um componente é desbloqueado, a propriedade `editable` é definida como `true`.

   * Quando um componente que já contém conteúdo for desbloqueado, esse conteúdo será movido para a ramificação `initial`.

* O nó `cq:responsive` contém definições para o layout responsivo.

### Conteúdo inicial {#initial-content}

Define o conteúdo inicial que uma nova página terá na criação:

* Contém um nó `jcr:content` que é copiado para qualquer nova página.
* É unida à estrutura ( `/structure`) ao criar uma nova página.
* Nenhuma página existente será atualizada se o conteúdo inicial for alterado após a criação.
* O nó `root` contém uma lista de componentes para definir o que estará disponível na página resultante.
* Se o conteúdo for adicionado a um componente no modo de estrutura e esse componente for desbloqueado posteriormente (ou vice-versa), esse conteúdo será usado como conteúdo inicial.

### Layout {#layout}

Quando [editar um modelo você pode definir o layout](/help/sites-authoring/templates.md), isso usa [layout responsivo padrão](/help/sites-authoring/responsive-layout.md) que também pode ser [configurado](/help/sites-administering/configuring-responsive-layout.md).

### Políticas de conteúdo {#content-policies}

As políticas do conteúdo (ou design) definem as propriedades do design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas. Eles são aplicáveis ao modelo (e às páginas criadas com o modelo). As políticas de conteúdo podem ser criadas e selecionadas no editor de modelos.

* A propriedade `cq:policy`, no nó `root`
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornece uma referência relativa à política de conteúdo para o sistema de parágrafo da página.

* A propriedade `cq:policy`, nos nós explícitos de componentes em `root`, fornece links para as políticas dos componentes individuais.

* As definições de política reais são armazenadas em:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Os caminhos das definições de política dependem do caminho do componente. `cq:policy` contém uma referência relativa à configuração propriamente dita.

>[!NOTE]
>
>As páginas criadas a partir de modelos editáveis não ofertas em um modo de Design no editor de páginas.
>
>A árvore `policies` de um modelo editável tem a mesma hierarquia que a configuração do modo de design de um modelo estático em:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>A configuração do modo de design de um modelo estático foi definida por componente de página.

### Políticas da página {#page-policies}

As políticas de página permitem que você defina a [política de conteúdo](#content-policies) para a página (parsys principal), no modelo ou nas páginas resultantes.

### Ativando e permitindo um modelo para uso {#enabling-and-allowing-a-template-for-use}

1. **Ativar o modelo**

   Antes que um modelo possa ser usado, ele deve ser habilitado por:

   * [Habilitando o ](/help/sites-authoring/templates.md#enablingatemplateauthor) modelo do console  **** Modelos.

   * Definindo a propriedade status no nó `jcr:content`.

      * Por exemplo, em:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina a propriedade:

         * Nome: status
         * Tipo: String
         * Valor: `enabled`

1. **Modelos permitidos**

   * [Defina os caminhos de modelo permitidos nas Propriedades da  **página**](/help/sites-authoring/templates.md#allowing-a-template-author) da página ou da página raiz apropriada de uma subramificação.
   * Defina a propriedade:
      `cq:allowedTemplates`
Na 
`jcr:content` nó da ramificação necessária.
   Por exemplo, com um valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de conteúdo resultante {#resultant-content-pages}

Páginas criadas a partir de modelos editáveis:

* São criados com uma subárvore que é unida de `structure` e `initial` no modelo

* Ter referências às informações contidas no modelo e no tipo de modelo. Isso é obtido com um nó `jcr:content` com as propriedades:

   * `cq:template`
Fornece a referência dinâmica ao modelo real; permite que as alterações no modelo sejam refletidas nas páginas reais.

   * `cq:templateType`
Fornece uma referência ao tipo de modelo.

![chlimage_1-71](assets/chlimage_1-71.png)

O diagrama acima mostra como os modelos, o conteúdo e os componentes se interrelacionam:

* Controlador - `/content/<my-site>/<my-page>`
A página resultante que faz referência ao modelo. O conteúdo controla todo o processo. De acordo com as definições, acessa o modelo e os componentes apropriados.

* Configuração - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
O modelo [e as políticas de conteúdo relacionadas](#template-definitions) definem a configuração da página.

* Modelo - pacotes OSGi
O [pacote OSGI](/help/sites-deploying/osgi-configuration-settings.md) implementa a funcionalidade.

* Visualização - `/apps/<my-site>/components`
Nos ambientes autor e publicação, o conteúdo é renderizado por [components](/help/sites-developing/components.md).

Ao renderizar uma página:

* **Modelos**:

   * A propriedade `cq:template` do nó `jcr:content` será referenciada para acessar o modelo que corresponde a essa página.

* **Componentes**:

   * O componente de página unirá a árvore `structure/jcr:content` do modelo à árvore `jcr:content` da página.

   * O componente de página permitirá que o autor edite apenas os nós da estrutura do modelo que foram sinalizados como editáveis (bem como quaisquer filhos).
   * Ao renderizar um componente em uma página, o caminho relativo desse componente será retirado do nó `jcr:content`; o mesmo caminho sob o nó `policies/jcr:content` do modelo será então pesquisado.

      * A propriedade `cq:policy` desse nó aponta para a política de conteúdo real (isto é, ela contém a configuração de design desse componente).

      * Isso permite que você tenha vários modelos que reusam as mesmas configurações de política de conteúdo.
