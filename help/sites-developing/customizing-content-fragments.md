---
title: Personalização e extensão de fragmentos de conteúdo
seo-title: Customizing and Extending Content Fragments
description: Um fragmento de conteúdo estende um ativo padrão.
seo-description: A content fragment extends a standard asset.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 9ad531738ac5e3c9d888f685b47c8b322712a89e
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 2%

---


# Personalização e extensão de fragmentos de conteúdo{#customizing-and-extending-content-fragments}

Um fragmento de conteúdo estende um ativo padrão; consulte:

* [Criação e gerenciamento de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) e [Criação de página com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md) para obter mais informações sobre fragmentos de conteúdo.

* [Gerenciamento de ativos](/help/assets/manage-assets.md) e [Personalização e extensão de ativos](/help/assets/extending-assets.md) para obter mais informações sobre ativos padrão.

## Arquitetura {#architecture}

O básico [componentes](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) de um fragmento de conteúdo são:

* A *Fragmento do conteúdo,*
* consistindo em um ou mais *Elemento de conteúdo* s,
* e que podem ter um ou mais *Variação de conteúdo* s.

Dependendo do tipo de fragmento, modelos ou modelos também são usados:

>[!CAUTION]
>
>[Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) são recomendados para criar todos os novos fragmentos.
>
>Os Modelos de fragmento de conteúdo são usados para todos os exemplos na WKND.

>[!NOTE]
>
>Antes do AEM 6.3, os Fragmentos de conteúdo eram criados com base em modelos em vez de modelos.
>
>Os modelos de Fragmento de conteúdo agora estão obsoletos. Elas ainda podem ser usadas para criar fragmentos, mas é recomendado usar Modelos de fragmento de conteúdo . Nenhum novo recurso será adicionado aos modelos de fragmento e será removido em uma versão futura.

* Modelos de fragmentos do conteúdo:

   * Usado para definir fragmentos de conteúdo que possuem conteúdo estruturado.
   * Os modelos de fragmento de conteúdo definem a estrutura de um fragmento de conteúdo quando ele é criado.
   * Um fragmento faz referência ao modelo; portanto, as alterações no modelo podem/afetarão qualquer fragmento dependente.
   * Os modelos são incorporados aos tipos de dados.
   * As funções para adicionar novas variações, etc., precisam atualizar o fragmento adequadamente.

   >[!CAUTION]
   >
   >Quaisquer alterações em um modelo de fragmento de conteúdo existente podem afetar fragmentos dependentes; isso pode levar a propriedades órfãs nesses fragmentos.

* Modelos de fragmentos de conteúdo:

   * Usado para definir fragmentos de conteúdo simples.
   * Os modelos definem a estrutura (básica, somente texto) de um fragmento de conteúdo quando ele é criado.
   * O modelo é copiado para o fragmento ao ser criado; assim, novas alterações no modelo não serão refletidas nos fragmentos existentes.
   * As funções para adicionar novas variações, etc., precisam atualizar o fragmento adequadamente.
   * [Modelos de fragmento de conteúdo](/help/sites-developing/content-fragment-templates.md) funcionem de forma diferente da de outros mecanismos de modelização no ecossistema de AEM (por exemplo, modelos de página, etc.). Por conseguinte, devem ser consideradas separadamente.
   * Quando baseado em um modelo, o tipo MIME do conteúdo é gerenciado no conteúdo real; isso significa que cada elemento e variação podem ter um tipo MIME diferente.

### Integração com ativos {#integration-with-assets}

O Gerenciamento de fragmentos de conteúdo (CFM) faz parte do AEM Assets como:

* Fragmentos de conteúdo são ativos.
* Eles usam a funcionalidade Ativos existente.
* Eles são totalmente integrados aos Ativos (consoles de administrador etc.).

#### Mapeamento de fragmentos de conteúdo estruturados para ativos {#mapping-structured-content-fragments-to-assets}

![fragmento para ativos estruturados](assets/fragment-to-assets-structured.png)

Fragmentos de conteúdo com conteúdo estruturado (ou seja, com base em um modelo de fragmento de conteúdo) são mapeados para um único ativo:

* Todo o conteúdo é armazenado na variável `jcr:content/data` nó do ativo:

   * Os dados do elemento são armazenados no subnó principal :
      `jcr:content/data/master`

   * As variações são armazenadas em um subnó que leva o nome da variação: por exemplo `jcr:content/data/myvariation`

   * Os dados de cada elemento são armazenados no respectivo subnó como uma propriedade com o nome do elemento: por exemplo, o conteúdo do elemento `text` é armazenado como propriedade `text` on `jcr:content/data/master`

* Os metadados e o conteúdo associado são armazenados abaixo `jcr:content/metadata`
Exceto o título e a descrição, que não são considerados metadados tradicionais e armazenados em 
`jcr:content`

#### Mapeamento de fragmentos de conteúdo simples para ativos {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

Fragmentos de conteúdo simples (com base em um modelo) são mapeados para um composto que consiste em um ativo principal e subativos (opcional):

* Todas as informações não relacionadas ao conteúdo de um fragmento (como título, descrição, metadados, estrutura) são gerenciadas exclusivamente no ativo principal.
* O conteúdo do primeiro elemento de um fragmento é mapeado para a representação original do ativo principal.

   * As variações (se houver) do primeiro elemento são mapeadas para outras representações do ativo principal.

* Elementos adicionais (se existirem) são mapeados para subativos do ativo principal.

   * O conteúdo principal desses elementos adicionais mapeia para a representação original do respectivo subativo.
   * Outras variações (se aplicável) de quaisquer elementos adicionais são mapeadas para outras representações do respectivo subativo.

#### Localização do ativo {#asset-location}

Como ocorre com os ativos padrão, um fragmento de conteúdo é mantido em:

`/content/dam`

#### Permissões de ativos {#asset-permissions}

Para obter mais detalhes, consulte [Fragmento do conteúdo - excluir considerações](/help/assets/content-fragments/content-fragments-delete.md).

#### Integração de recursos {#feature-integration}

* O recurso de Gerenciamento de fragmento de conteúdo (CFM) baseia-se no núcleo de Ativos, mas deve ser o mais independente possível.
* O CFM fornece suas próprias implementações para itens nas visualizações de cartão/coluna/lista; essas são as implementações de renderização de conteúdo do Assets existentes.
* Vários componentes de Ativos foram estendidos para atender a fragmentos de conteúdo.

### Uso de fragmentos de conteúdo em páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>O [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR) agora é recomendado. Consulte [Desenvolvimento dos componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=pt-BR) para obter mais detalhes.

Os fragmentos de conteúdo podem ser referenciados AEM páginas, como qualquer outro tipo de ativo. AEM fornece a [**Fragmento de conteúdo** componente principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) - a [componente que permite incluir fragmentos de conteúdo em suas páginas](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). Você também pode estender, isso **Fragmento de conteúdo** componente principal.

* O componente usa o `fragmentPath` propriedade para fazer referência ao fragmento de conteúdo real. O `fragmentPath` Os bens sejam tratados da mesma forma que as propriedades similares de outros tipos de ativos; por exemplo, quando o fragmento de conteúdo é movido para outro local.

* O componente permite selecionar a variação a ser exibida.
* Além disso, um intervalo de parágrafos pode ser selecionado para restringir a saída; por exemplo, isso pode ser usado para saída de várias colunas.
* O componente permite [conteúdo intermediário](/help/sites-developing/components-content-fragments.md#in-between-content):

   * Aqui, o componente permite colocar outros ativos (imagens, etc.) entre os parágrafos do fragmento referenciado.
   * Para conteúdo intermediário, é necessário:

      * Estar ciente da possibilidade de referências instáveis; o conteúdo intermediário (adicionado ao criar uma página) não tem relacionamento fixo com o parágrafo ao lado do qual está posicionado, inserindo um novo parágrafo (no editor de fragmentos de conteúdo) antes que a posição do conteúdo intermediário possa perder a posição relativa
      * considere os parâmetros adicionais (como variação e filtros de parágrafo) para evitar falsos positivos nos resultados da pesquisa

>[!NOTE]
>
>**Modelo de fragmentos do conteúdo:**
>
>Ao usar um fragmento de conteúdo que foi baseado em um modelo de fragmento de conteúdo em uma página, o modelo é referenciado. Isso significa que, se o modelo não tiver sido publicado no momento em que você publicar a página, ela será sinalizada e o modelo será adicionado aos recursos a serem publicados com a página.
>
>**Modelo do fragmento de conteúdo:**
>
>Ao usar um fragmento de conteúdo que foi baseado em um modelo de fragmento de conteúdo em uma página, não há referência como o modelo foi copiado ao criar o fragmento.

#### Configuração usando o console OSGi {#configuration-using-osgi-console}

A implementação de backend de fragmentos de conteúdo é, por exemplo, responsável por tornar as instâncias de um fragmento usadas em uma página pesquisáveis ou por gerenciar conteúdo de mídia mista. Essa implementação precisa saber quais componentes são usados para renderizar fragmentos e como a renderização é parametrizada.

Os parâmetros para isso podem ser configurados no [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), para o pacote OSGi **Configuração do componente de fragmento de conteúdo**.

* **Tipos de recursos**
Uma lista de 
`sling:resourceTypes` pode ser fornecido para definir componentes que são usados para renderizar fragmentos de conteúdo e onde o processamento em segundo plano deve ser aplicado.

* **Propriedades de referência**
Uma lista de propriedades pode ser configurada para especificar onde a referência ao fragmento é armazenada para o respectivo componente.

>[!NOTE]
>
>Não há mapeamento direto entre a propriedade e o tipo de componente.
>
>AEM simplesmente obtém a primeira propriedade que pode ser encontrada em um parágrafo. Portanto, você deve escolher as propriedades com cuidado.

![captura de tela_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Ainda há algumas diretrizes que você deve seguir para garantir que seu componente seja compatível com o processamento em segundo plano do fragmento de conteúdo:

* O nome da propriedade em que os elementos a serem renderizados são definidos deve ser `element` ou `elementNames`.

* O nome da propriedade em que a variação a apresentar é definida deve ser `variation` ou `variationName`.

* Se a saída de vários elementos for suportada (usando `elementNames` para especificar vários elementos), o modo de exibição real é definido pela propriedade `displayMode`:

   * Se o valor for `singleText` (e há apenas um elemento configurado), o elemento é renderizado como um texto com conteúdo intermediário, suporte para layout, etc. Esse é o padrão para fragmentos, onde apenas um único elemento é renderizado.
   * Caso contrário, uma abordagem muito mais simples será usada (poderia ser chamada de &quot;exibição de formulário&quot;), onde nenhum conteúdo intermediário será suportado e o conteúdo do fragmento será renderizado &quot;como está&quot;.

* Se o fragmento for renderizado para `displayMode` == `singleText` (implicitamente ou explicitamente) as seguintes propriedades adicionais são reproduzidas:

   * `paragraphScope` define se todos os parágrafos, ou apenas um intervalo de parágrafos, devem ser renderizados (valores: `all` vs. `range`)

   * if `paragraphScope` == `range` em seguida, a propriedade `paragraphRange` define o intervalo de parágrafos a serem renderizados

### Integração com outros quadros {#integration-with-other-frameworks}

Os fragmentos de conteúdo podem ser integrados com:

* **Traduções**

   Os Fragmentos de conteúdo são totalmente integrados à variável [Fluxo de trabalho de tradução AEM](/help/sites-administering/tc-manage.md). A nível arquitetônico, isso significa:

   * As traduções individuais de um fragmento de conteúdo são, na verdade, fragmentos separados; por exemplo:

      * Estão localizadas sob raízes linguísticas diferentes:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`

      * mas compartilham exatamente o mesmo caminho relativo abaixo da raiz de idioma:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * Além dos caminhos baseados em regras, não há mais conexão entre as diferentes versões linguísticas de um fragmento de conteúdo; eles são tratados como dois fragmentos separados, embora a interface do usuário forneça os meios de navegar entre as variantes de idioma.
   >[!NOTE]
   >
   >O fluxo de trabalho de tradução de AEM funciona com `/content`:
   >
   >* Como os modelos de fragmento de conteúdo residem em `/conf`, elas não são incluídas nessas traduções. Você pode [internacionalizar as strings da interface do usuário](/help/sites-developing/i18n-dev.md).
   >
   >* Os modelos são copiados para criar o fragmento, de modo que isso esteja implícito.


* **Esquemas de metadados**

   * Fragmentos de conteúdo (re)usar o [esquemas de metadados](/help/assets/metadata-schemas.md), que podem ser definidos com ativos padrão.
   * O CFM fornece seu próprio schema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      isso pode ser estendido se necessário.

   * O respectivo formulário de esquema é integrado ao editor de fragmentos.

## A API de gerenciamento de fragmentos de conteúdo - do lado do servidor {#the-content-fragment-management-api-server-side}

Você pode usar a API do lado do servidor para acessar os fragmentos de conteúdo; consulte:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>É altamente recomendável usar a API do lado do servidor em vez de acessar diretamente a estrutura de conteúdo.

### Principais interfaces {#key-interfaces}

As três interfaces a seguir podem servir como pontos de entrada:

* **Modelo do fragmento** ([ModeloDeFragmento](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   Use `FragmentTemplate.createFragment()` para criar um novo fragmento.

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   Essa interface representa:

   * um modelo de fragmento de conteúdo ou de fragmento de conteúdo do qual criar um fragmento de conteúdo,
   * e (após a criação) a informação estrutural desse fragmento

   Essas informações podem incluir:

   * Acessar dados básicos (título, descrição)
   * Acesse modelos/modelos para os elementos do fragmento:

      * Listar modelos de elemento
      * Obter informações estruturais para um determinado elemento
      * Acessar o modelo de elemento (consulte `ElementTemplate`)
   * Acessar modelos para as variações do fragmento:

      * Listar modelos de variação
      * Obter informações estruturais para uma determinada variação
      * Acesse o modelo de variação (consulte `VariationTemplate`)
   * Obter conteúdo associado inicial

   Interfaces que representam informações importantes:

   * `ElementTemplate`

      * Obter dados básicos (nome, título)
      * Obter conteúdo do elemento inicial
   * `VariationTemplate`

      * Obter dados básicos (nome, título, descrição)






* **Fragmento de conteúdo** ([FragmentoDeConteúdo](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Essa interface permite que você trabalhe com um fragmento de conteúdo de forma abstrata.

   >[!CAUTION]
   >
   >É altamente recomendável acessar um fragmento por meio dessa interface. A alteração direta da estrutura de conteúdo deve ser evitada.

   A interface fornece os meios para:

   * Gerenciar dados básicos (por exemplo, obter nome; get/set title/description)
   * Acessar metadados
   * Elementos de acesso:

      * Elementos de lista
      * Obter elementos por nome
      * Criar novos elementos (consulte [Avisos](#caveats))

      * Acessar dados do elemento (consulte `ContentElement`)
   * Listar variações definidas para o fragmento
   * Criar novas variações globalmente
   * Gerenciar conteúdo associado:

      * Listar coleções
      * Adicionar coleções
      * Remover coleções
   * Acessar o modelo ou o modelo do fragmento

   As interfaces que representam os elementos principais de um fragmento são:

   * **Elemento de conteúdo** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Variações de acesso de um elemento:

         * Listar variações
         * Obter variações por nome
         * Crie novas variações (consulte [Avisos](#caveats))
         * Remover variações (consulte [Avisos](#caveats))
         * Acesse os dados de variação (consulte `ContentVariation`)
      * Atalho para resolver variações (aplicando alguma lógica de fallback adicional específica da implementação se a variação especificada não estiver disponível para um elemento)
   * **Variação de conteúdo** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Sincronização simples, com base nas informações da última modificação

   Todas as três interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) estender o `Versionable` interface, que adiciona recursos de controle de versão, necessários para fragmentos de conteúdo:

   * Criar nova versão do elemento
   * Versões de lista do elemento
   * Obter o conteúdo de uma versão específica do elemento com versão







### Adaptação - Uso de adaptTo() {#adapting-using-adaptto}

Podem ser adaptadas as seguintes condições:

* `ContentFragment` pode ser adaptado para:

   * `Resource` - o recurso Sling subjacente; observe que a atualização do subjacente `Resource` diretamente, requer a reconstrução da variável `ContentFragment` objeto.

   * `Asset` - DAM `Asset` abstração que representa o fragmento de conteúdo; observe que a atualização do `Asset` diretamente, requer a reconstrução da variável `ContentFragment` objeto.

* `ContentElement` pode ser adaptado para:

   * `ElementTemplate` - para aceder às informações estruturais do elemento.

* `FragmentTemplate` pode ser adaptado para:

   * `Resource` - o `Resource` Determinar o modelo referenciado ou o modelo original que foi copiado;

      * alterações efetuadas através da `Resource` não são refletidas automaticamente na variável `FragmentTemplate`.

* `Resource` pode ser adaptado para:

   * `ContentFragment`
   * `FragmentTemplate`

### Avisos {#caveats}

Note-se que:

* A API é implementada para fornecer funcionalidade compatível com a interface do usuário do .
* A API inteira foi projetada para **not** As alterações persistem automaticamente (a menos que observado de outra forma no JavaDoc da API). Portanto, sempre será necessário confirmar o resolvedor de recursos da respectiva solicitação (ou o resolvedor que você está realmente usando).
* Tarefas que podem exigir esforço adicional:

   * Criar/remover novos elementos não atualizará a estrutura de dados de fragmentos simples (com base em um modelo de fragmento).
   * Criar novas variações de `ContentElement` não atualizará a estrutura de dados (mas os criará globalmente a partir de `ContentFragment` ).

   * Remover variações existentes não atualizará a estrutura de dados.

## A API de gerenciamento de fragmento de conteúdo - Lado do cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Para AEM 6.5, a API do lado do cliente é interna.

### Informações adicionais {#additional-information}

Consulte o link a seguir:

* `filter.xml`

   O `filter.xml` O para gerenciamento de fragmentos de conteúdo é configurado de forma que não se sobreponha ao pacote de conteúdo principal do Assets.

## Editar sessões {#edit-sessions}

Uma sessão de edição é iniciada quando o usuário abre um fragmento de conteúdo em uma das páginas do editor. A sessão de edição é concluída quando o usuário deixa o editor selecionando **Salvar** ou **Cancelar**.

### Requisitos {#requirements}

Os requisitos para controlar uma sessão de edição são:

* A edição de um fragmento de conteúdo, que pode abranger várias exibições (= HTML pages), deve ser atômica.
* A edição também deve ser *transacional*; no final da sessão de edição, as alterações devem ser confirmadas (salvas) ou revertidas (canceladas).
* Os casos de borda devem ser manipulados adequadamente; incluem situações como quando o usuário sai da página inserindo um URL manualmente ou usando navegação global.
* Um salvamento automático periódico (a cada x minutos) deve estar disponível para evitar perda de dados.
* Se um fragmento de conteúdo for editado simultaneamente por dois usuários, eles não devem substituir as alterações uns dos outros.

#### Processos {#processes}

Os processos envolvidos são:

* Iniciar uma sessão

   * Uma nova versão do fragmento de conteúdo é criada.
   * O salvamento automático é iniciado.
   * Os cookies estão definidos; eles definem o fragmento editado no momento e que há uma sessão de edição aberta.

* Conclusão de uma sessão

   * O salvamento automático é interrompido.
   * Após confirmação:

      * As últimas informações modificadas são atualizadas.
      * Os cookies são removidos.
   * Após a reversão:

      * A versão do fragmento de conteúdo criada quando a sessão de edição foi iniciada é restaurada.
      * Os cookies são removidos.


* Edição

   * Todas as alterações (salvamento automático incluído) são feitas no fragmento de conteúdo ativo, não em uma área separada e protegida.
   * Portanto, essas alterações são refletidas imediatamente em AEM páginas que fazem referência ao respectivo fragmento de conteúdo

#### Ações {#actions}

As ações possíveis são:

* Inserir uma página

   * Verifique se uma sessão de edição já está presente; verificando o respectivo cookie.

      * Se existir, verifique se a sessão de edição foi iniciada para o fragmento de conteúdo que está sendo editado no momento

         * Se o fragmento atual, restaure a sessão.
         * Caso contrário, tente cancelar a edição do fragmento de conteúdo editado anteriormente e remover os cookies (nenhuma sessão de edição presente posteriormente).
      * Se não houver uma sessão de edição, aguarde a primeira alteração feita pelo usuário (veja abaixo).
   * Verifique se o fragmento de conteúdo já está referenciado em uma página e, nesse caso, exiba as informações apropriadas.



* Alteração de conteúdo

   * Sempre que o usuário altera o conteúdo e não há uma sessão de edição presente, uma nova sessão de edição é criada (consulte [Iniciar uma sessão](#processes)).

* Sair de uma página

   * Se uma sessão de edição estiver presente e as alterações não forem persistentes, uma caixa de diálogo de confirmação modal será exibida para notificar o usuário de conteúdo potencialmente perdido e permitir que ele permaneça na página.

## Exemplos {#examples}

### Exemplo: Acesso a um fragmento de conteúdo existente {#example-accessing-an-existing-content-fragment}

Para isso, é possível adaptar o recurso que representa a API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Por exemplo:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Exemplo: Criação de um novo fragmento de conteúdo {#example-creating-a-new-content-fragment}

Para criar um novo fragmento de conteúdo programaticamente, você precisa usar:

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Por exemplo:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exemplo: Especificação do intervalo de salvamento automático {#example-specifying-the-auto-save-interval}

O intervalo de salvamento automático (medido em segundos) pode ser definido usando o gerenciador de configuração (ConfMgr):

* Nó: `<*conf-root*>/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`
* Tipo: `Long`

* Padrão: `600` (10 minutos); isso é definido em `/libs/settings/dam/cfm/jcr:content`

Para definir um intervalo de salvamento automático de 5 minutos, é necessário definir a propriedade no nó ; por exemplo:

* Nó: `/conf/global/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Modelos de fragmentos do conteúdo {#content-fragment-templates}

Consulte [Modelos de fragmentos do conteúdo](/help/sites-developing/content-fragment-templates.md) para obter informações completas.

## Componentes da autoria de página {#components-for-page-authoring}

Para obter mais informações, consulte

* [Componentes principais - Componente do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) (recomendado)
* [Componentes do fragmento de conteúdo - Componentes da criação de página](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
