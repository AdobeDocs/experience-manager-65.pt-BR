---
title: Suporte a Fragmentos de conteúdo na API HTTP do AEM Assets
seo-title: Suporte a Fragmentos de conteúdo na API HTTP do AEM Assets
description: Saiba mais sobre o Suporte a fragmentos de conteúdo na API HTTP do AEM Assets.
seo-description: Saiba mais sobre o Suporte a fragmentos de conteúdo na API HTTP do AEM Assets.
uuid: c500d71e-ceee-493a-9e4d-7016745c544c
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: extending-assets
discoiquuid: 03502b41-b448-47ab-9729-e0a66a3389fa
docset: aem65
feature: Fragmentos de conteúdo
role: Profissional de negócios, Administrador
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 3%

---


# Suporte a Fragmentos de conteúdo na API HTTP do AEM Assets{#content-fragments-support-in-aem-assets-http-api}

## Visão geral {#overview}

>[!NOTE]
>
>A [API HTTP de ativos](/help/assets/mac-api-assets.md) abrange:
>
>* API REST de ativos
>* incluindo suporte para Fragmentos de conteúdo

>
>
A implementação atual da API HTTP do AEM Assets é REST.

A API REST do Adobe Experience Manager (AEM) [Assets](/help/assets/mac-api-assets.md) permite que os desenvolvedores acessem o conteúdo (armazenado em AEM) diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir).

A API permite operar o AEM como um CMS (Content Management System) sem periféricos fornecendo serviços de conteúdo a um aplicativo front-end JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON.

Por exemplo, Aplicativos de página única (SPA), baseados em estrutura ou personalizados, exigem conteúdo fornecido através da API HTTP, geralmente no formato JSON.

Embora AEM os Componentes principais forneçam uma API muito abrangente, flexível e personalizável que possa servir as operações de Leitura necessárias para essa finalidade e cuja saída JSON possa ser personalizada, eles exigem AEM saber-fazer de implementação do WCM (Web Content Management), pois devem ser hospedados em páginas (API) que são baseadas em modelos de AEM dedicados. Nem todas as organizações SPA de desenvolvimento têm acesso a esses recursos.

É quando a API REST do Assets pode ser usada. Ela permite que os desenvolvedores acessem ativos (por exemplo, imagens e fragmentos de conteúdo) diretamente, sem precisar primeiro incorporá-los a uma página e entregar seu conteúdo em formato JSON serializado. (Observe que não é possível personalizar a saída JSON da API REST de ativos). A API REST de ativos também permite que os desenvolvedores modifiquem o conteúdo, criando ativos novos, atualizados ou excluindo ativos, fragmentos de conteúdo e pastas existentes.

A API REST de ativos:

* segue o [princípio HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa o [formato SIREN](https://github.com/kevinswiber/siren)

## Pré-requisitos {#prerequisites}

A API REST de ativos está disponível em cada instalação pronta para uso de uma versão AEM recente.

## Principais conceitos {#key-concepts}

A API REST de ativos oferece acesso ao estilo [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) para ativos armazenados em uma instância de AEM. Ele usa o terminal `/api/assets` e requer o caminho do ativo para acessá-lo (sem o `/content/dam` à esquerda).

O método HTTP determina a operação a ser executada:

* **GET**  - para recuperar uma representação JSON de um ativo ou uma pasta
* **POST**  - para criar novos ativos ou pastas
* **PUT**  - para atualizar as propriedades de um ativo ou pasta
* **DELETE**  - para excluir um ativo ou uma pasta

>[!NOTE]
>
>O corpo da solicitação e/ou os parâmetros de URL podem ser usados para configurar algumas dessas operações; por exemplo, defina que uma pasta ou um ativo deve ser criado por uma solicitação **POST**.

O formato exato das solicitações compatíveis é definido na documentação de [API Reference](/help/assets/assets-api-content-fragments.md#api-reference).

### Comportamento transacional {#transactional-behavior}

Todas as solicitações são atômicas.

Isso significa que as solicitações subsequentes (`write`) não podem ser combinadas em uma única transação que pode ter êxito ou falhar como uma única entidade.

### AEM (Ativos) REST API versus AEM Componentes {#aem-assets-rest-api-versus-aem-components}

<table>
 <tbody>
  <tr>
   <td>Aspecto</td>
   <td>API REST de ativos<br /> </td>
   <td>Componente AEM<br /> (componentes que usam Modelos Sling)</td>
  </tr>
  <tr>
   <td>Casos de uso suportados</td>
   <td>Finalidade geral.</td>
   <td><p>Otimizado para consumo em um Aplicativo de página única (SPA), ou qualquer outro contexto (que consome conteúdo).</p> <p>Também pode conter informações de layout.</p> </td>
  </tr>
  <tr>
   <td>Operações suportadas</td>
   <td><p>Criar, Ler, Atualizar, Excluir.</p> <p>Com operações adicionais, dependendo do tipo de entidade.</p> </td>
   <td>Somente leitura.</td>
  </tr>
  <tr>
   <td>Acesso</td>
   <td><p>Pode ser acessado diretamente.</p> <p>Usa o ponto de extremidade <code>/api/assets </code>mapeado para <code>/content/dam</code> (no repositório).</p> <p>Por exemplo, para acessar:<code class="code">
       /content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten</code><br /> solicitação:<br /> <code>/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.model.json</code></p> </td>
   <td><p>Precisa ser referenciado por meio de um componente de AEM em uma página de AEM.</p> <p>Usa o seletor <code>.model</code> para criar a representação JSON.</p> <p>Um exemplo de URL seria semelhante a:<br /> <code>https://localhost:4502/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.model.json</code></p> </td>
  </tr>
  <tr>
   <td>Segurança</td>
   <td><p>Várias opções são possíveis.</p> <p>O OAuth é proposto; pode ser configurado separadamente da configuração padrão.</p> </td>
   <td>Usa AEM configuração padrão.</td>
  </tr>
  <tr>
   <td>Observações arquitetônicas</td>
   <td><p>O acesso de gravação normalmente endereçará uma instância de autor.</p> <p>A leitura também pode ser direcionada a uma instância de publicação.</p> </td>
   <td>Como essa abordagem é somente leitura, ela normalmente será usada para instâncias de publicação.</td>
  </tr>
  <tr>
   <td>Saída</td>
   <td>Saída SIREN baseada em JSON: verboso, mas poderoso. Permite navegar dentro do conteúdo.</td>
   <td>Saída proprietária baseada em JSON; configurável por meio de Modelos do Sling. É difícil implementar a navegação na estrutura de conteúdo (mas não é necessariamente impossível).</td>
  </tr>
 </tbody>
</table>

### Segurança {#security}

Se a API REST do Assets for usada em um ambiente sem requisitos de autenticação específicos, AEM filtro CORS precisará ser configurado corretamente.

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* [Explicação do CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Vídeo - Desenvolvimento do CORS com AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



Em ambientes com requisitos de autenticação específicos, o OAuth é recomendado.

## Recursos disponíveis {#available-features}

Fragmentos de conteúdo são um tipo específico de ativo, consulte [Trabalhar com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md).

Para obter mais informações sobre recursos disponíveis por meio da API, consulte:

* [Recursos disponíveis ](/help/assets/mac-api-assets.md#assets) da API REST de ativos
* [Tipos de entidade](/help/assets/assets-api-content-fragments.md#entity-types)

### Paginação {#paging}

A API REST de ativos suporta paginação (para solicitações do GET) por meio dos parâmetros de URL:

* `offset` - o número da primeira entidade (filho) a recuperar
* `limit` - o número máximo de entidades devolvidas

A resposta conterá informações de paginação como parte da seção `properties` da saída SIREN. Esta propriedade `srn:paging` contém o número total de entidades (filho) ( `total`), o deslocamento e o limite ( `offset`, `limit`) conforme especificado na solicitação.

>[!NOTE]
>
>A paginação normalmente é aplicada em entidades de contêiner (ou seja, pastas ou ativos com representações), pois está relacionada aos filhos da entidade solicitada.

#### Exemplo: Paginação {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Tipos de entidade {#entity-types}

### Pastas {#folders}

As pastas atuam como contêineres para ativos e outras pastas. Eles refletem a estrutura do repositório de conteúdo AEM.

A API REST do Assets expõe o acesso às propriedades de uma pasta; por exemplo, seu nome, título etc. Os ativos são expostos como entidades filhas de pastas.

>[!NOTE]
>
>Dependendo do tipo de ativo, a lista de entidades-filho já pode conter o conjunto completo de propriedades que define a respectiva entidade-filho. Como alternativa, apenas um conjunto reduzido de propriedades pode ser exposto para uma entidade nesta lista de entidades-filho.

### Assets {#assets}

Se um ativo for solicitado, a resposta retornará seus metadados; como título, nome e outras informações, conforme definido pelo respectivo schema de ativos.

Os dados binários de um ativo são expostos como um link SIREN do tipo `content` (também conhecido como `rel attribute`).

Os ativos podem ter várias representações. Normalmente, elas são expostas como entidades secundárias, sendo uma exceção uma representação em miniatura, que é exposta como um link do tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de conteúdo {#content-fragments}

Um [fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md) é um tipo especial de ativo. Eles podem ser usados para acessar dados estruturados, como textos, números, datas, entre outros.

Como há várias diferenças nos ativos *padrão* (como imagens ou áudio), algumas regras adicionais se aplicam ao seu manuseio.

#### Representação {#representation}

Fragmentos de conteúdo:

* Não exponha quaisquer dados binários.
* Estão completamente contidos na saída JSON (dentro da propriedade `properties` ).

* Também são considerados atômicos, ou seja, os elementos e as variações são expostos como parte das propriedades do fragmento vs. como links ou entidades filhas. Isso permite acesso eficiente à carga de um fragmento.

#### Modelos de conteúdo e fragmentos de conteúdo {#content-models-and-content-fragments}

Atualmente, os modelos que definem a estrutura de um fragmento de conteúdo não são expostos por meio de uma API HTTP. Portanto, o *consumidor* precisa saber sobre o modelo de um fragmento (pelo menos um mínimo) - embora a maioria das informações possa ser inferida da carga; como tipos de dados, etc. fazem parte da definição.

Para criar um novo fragmento de conteúdo, o caminho (repositório interno) deve ser fornecido.

#### Conteúdo associado {#associated-content}

O conteúdo associado não está exposto no momento.

## Usar {#using}

O uso pode ser diferente dependendo se você está usando um autor ou um ambiente de publicação AEM, juntamente com seu caso de uso específico.

* A criação é estritamente vinculada a uma instância do autor ([e atualmente não há como replicar um fragmento para publicar usando essa API](/help/assets/assets-api-content-fragments.md#limitations)).
* A entrega é possível de ambos, pois AEM serve o conteúdo solicitado somente no formato JSON.

   * O armazenamento e o delivery de uma instância de autor de AEM devem ser suficientes para aplicativos de biblioteca de mídia por trás do firewall.
   * Para entrega na Web ao vivo, recomenda-se uma instância de publicação de AEM.

>[!CAUTION]
>
>A configuração do dispatcher em instâncias AEM nuvem pode bloquear o acesso a `/api`.

>[!NOTE]
>
>Para obter mais detalhes, consulte a [Referência da API](/help/assets/assets-api-content-fragments.md#api-reference). Especificamente, [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

### Leitura/entrega {#read-delivery}

O uso é via:

`GET /{cfParentPath}/{cfName}.json`

Por exemplo:

`https://localhost:4502/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.json`

A resposta é JSON serializado com o conteúdo estruturado como no fragmento de conteúdo. As referências são fornecidas como URLs de referência.

Dois tipos de operações de leitura são possíveis:

* Ao ler um fragmento de conteúdo específico por caminho, a representação JSON do fragmento de conteúdo é retornada.
* Leitura de uma pasta de fragmentos de conteúdo por caminho: isso retorna as representações JSON de todos os fragmentos de conteúdo dentro da pasta.

### Criar {#create}

O uso é via:

`POST /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do fragmento de conteúdo a ser criado, incluindo qualquer conteúdo inicial que deve ser definido nos elementos do fragmento de conteúdo. É obrigatório definir a propriedade `cq:model` e deve apontar para um modelo de fragmento de conteúdo válido. Se isso não for feito, haverá um erro. Também é necessário adicionar um cabeçalho `Content-Type` que está definido como `application/json`.

### Atualizar {#update}

O uso é via

`PUT /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do que deve ser atualizado para o fragmento de conteúdo especificado.

Pode ser simplesmente o título ou a descrição de um fragmento de conteúdo, um único elemento ou todos os valores e/ou metadados do elemento. Também é obrigatório fornecer uma propriedade `cq:model` válida para atualizações.

### Exclua {#delete}

O uso é via:

`DELETE /{cfParentPath}/{cfName}`

## Limitações           {#limitations}

Existem algumas limitações:

* **As variações não podem ser gravadas e atualizadas.** Se essas variações forem adicionadas a uma carga (por exemplo, para atualizações), serão ignoradas. No entanto, a variação será veiculada pelo delivery ( `GET`).

* **No momento, os modelos de fragmento de conteúdo não são compatíveis**: eles não podem ser lidos ou criados. Para criar um novo fragmento de conteúdo ou atualizar um fragmento de conteúdo existente, os desenvolvedores precisam saber o caminho correto para o modelo de fragmento de conteúdo. Atualmente, o único método para obter uma visão geral desses itens é por meio da interface do usuário de administração.
* **As referências são ignoradas**. Atualmente, não há verificações para determinar se um fragmento de conteúdo existente é referenciado. Portanto, por exemplo, excluir um fragmento de conteúdo pode resultar em problemas em uma página que contém uma referência.

## Códigos de status e mensagens de erro {#status-codes-and-error-messages}

Os seguintes códigos de status podem ser vistos nas circunstâncias relevantes:

* **200 (OK)**

   Retornado quando:

   * solicitando um fragmento de conteúdo por meio de `GET`

   * atualização bem-sucedida de um fragmento de conteúdo via `PUT`

* **201 (Criado)**

   Retornado quando:

   * criação com êxito de um fragmento de conteúdo via `POST`

* **404 (Não encontrado)**

   Retornado quando:

   * o fragmento de conteúdo solicitado não existe

* **500 (Erro interno do servidor)**

   >[!NOTE]
   >
   >Este erro é retornado:
   >
   >
   >
   >    * quando ocorre um erro que não pode ser identificado com um código específico
   >    * quando a carga fornecida não era válida


   A seguir são apresentados cenários comuns quando esse status de erro é retornado, juntamente com a mensagem de erro (monospace) gerada:

   * A pasta pai não existe (ao criar um fragmento de conteúdo via `POST`)
   * Nenhum modelo de fragmento de conteúdo é fornecido (valor nulo), o recurso é nulo (possivelmente um problema de permissão) ou o recurso não é um modelo de fragmento válido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
   * Não foi possível criar o fragmento de conteúdo (possivelmente um problema de permissão):

      * `Could not create content fragment`
   * Não foi possível atualizar o título e ou a descrição:

      * `Could not set value on content fragment`
   * Não foi possível definir metadados:

      * `Could not set metadata on content fragment`
   * O elemento de conteúdo não pôde ser encontrado ou não pôde ser atualizado

      * `Could not update content element`
      * `Could not update fragment data of element`

   As mensagens de erro detalhadas geralmente são retornadas da seguinte maneira:

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## Referência da API {#api-reference}

Consulte aqui para obter referências detalhadas da API:

* [API Adobe Experience Manager Assets - Fragmentos de conteúdo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [API HTTP de ativos](/help/assets/mac-api-assets.md)

   * [Recursos disponíveis](/help/assets/mac-api-assets.md#assets)

## Recursos adicionais {#additional-resources}

Para obter mais informações, consulte:

* [Documentação da API HTTP de ativos](/help/assets/mac-api-assets.md)
* [AEM sessão Gem: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

