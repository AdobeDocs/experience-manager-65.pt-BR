---
title: Marcação de recursos de ativação
seo-title: Marcação de recursos de ativação
description: A marcação dos recursos de ativação permite filtrar recursos e caminhos de aprendizado à medida que os membros navegam em catálogos
seo-description: A marcação dos recursos de ativação permite filtrar recursos e caminhos de aprendizado à medida que os membros navegam em catálogos
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: fa01c9fad82adb021220631a0536ab77ceb01e31

---


# Marcação de recursos de ativação {#tagging-enablement-resources}

## Visão geral {#overview}

A marcação dos recursos de ativação permite filtrar recursos e caminhos de aprendizado à medida que os membros navegam em [catálogos](functions.md#catalog-function).

Essencialmente:

* [Criar uma namespace](../../help/sites-administering/tags.md#creating-a-namespace) de tags para cada catálogo

   * [Definir permissões de tag](../../help/sites-administering/tags.md#setting-tag-permissions)
   * Somente para membros da comunidade (comunidade fechada)

      * Permitir acesso de leitura para o grupo de membros do site da [comunidade](users.md#publish-group-roles)
   * Para qualquer visitante do site, seja conectado ou anônimo (comunidade aberta)

      * Permitir acesso de leitura para o `Everyone` grupo
   * [Publicar as tags](../../help/sites-administering/tags.md#publishing-tags)



* [Definir o escopo das tags para um site da comunidade](sites-console.md#tagging)

   * [Configurar catálogos que existem na estrutura do site](functions.md#catalog-function)

      * É possível adicionar tags à instância do catálogo para controlar a lista de tags apresentadas nos filtros da interface do usuário.
      * É possível adicionar [pré-filtros](catalog-developer-essentials.md#pre-filters)para restringir os recursos incluídos de um catálogo.

* [Publicar o site da comunidade](sites-console.md#publishing-the-site)
* [Aplique tags aos recursos](resources.md#create-a-resource) de ativação para que eles possam ser filtrados categoricamente
* [Publicar os recursos de ativação](resources.md#publish)

## Tags do site da comunidade {#community-site-tags}

Ao criar ou editar um site da comunidade, a configuração [](sites-console.md#tagging) Marcação define o escopo das tags disponíveis para os recursos do site selecionando um subconjunto de namespaces de tags existentes.

Embora as tags possam ser criadas e adicionadas ao site da comunidade a qualquer momento, é recomendável projetar uma taxonomia antecipadamente, semelhante à criação de um banco de dados. Consulte [Uso de tags](../../help/sites-authoring/tags.md).

Posteriormente, ao adicionar tags a um site da comunidade existente, é necessário salvar a edição antes de poder adicionar a nova tag a uma função de catálogo na estrutura do site.

Para um site da comunidade, depois que o site é publicado e as tags são publicadas, é necessário ativar o acesso de leitura aos membros da comunidade. Consulte [Configuração de permissões](../../help/sites-administering/tags.md#setting-tag-permissions)de tag.

Veja a seguir como ele aparece no CRXDE quando um administrador aplica permissões de leitura `/etc/tags/ski-catalog` para o grupo `Community Enable Members`.

![chlimage_1-420](assets/chlimage_1-420.png)

## Namespaces de tags de catálogo {#catalog-tag-namespaces}

O recurso de catálogo usa tags para se definir. Ao configurar a função de catálogo em um site da comunidade, o conjunto de namespaces de tags a serem escolhidas é definido pelo escopo de espaços de tags definidos para o site da comunidade.

A função Catalog inclui uma configuração de tag que define as tags listadas na interface do usuário do filtro para o catálogo. A configuração &quot;Todas as Namespaces&quot; refere-se ao escopo das namespaces de tags selecionadas para o site da comunidade.

![chlimage_1-421](assets/chlimage_1-421.png)

## Aplicação de tags a recursos de ativação {#applying-tags-to-enablement-resources}

Os recursos de ativação e os caminhos de aprendizado aparecerão em todos os catálogos quando `Show in Catalog` estiver marcado. Adicionar tags a recursos e caminhos de aprendizado permitirá a pré-filtragem em catálogos específicos, bem como a filtragem na interface do usuário do catálogo.

A restrição dos recursos de ativação e dos caminhos de aprendizado para catálogos específicos é realizada com a criação de [pré-filtros](catalog-developer-essentials.md#pre-filters).

A interface do usuário do catálogo permite que os visitantes apliquem um filtro de tags à lista de recursos e caminhos de aprendizado exibidos nesse catálogo.

O administrador que aplica as tags para ativar os recursos deve estar ciente das namespaces de tags associadas aos catálogos, bem como da taxonomia para selecionar uma subtag para uma categorização mais refinada.

Por exemplo, se uma `ski-catalog` namespace foi criada e definida em um catálogo chamado `Ski Catalog`, ela pode ter duas tags-filho: `lesson-1` e `lesson-2`.

Assim, qualquer recurso de ativação marcado com um dos

* catálogo de esqui:lição-1
* catálogo de esqui:lição-2

aparecerá `Ski Catalog` após o recurso de ativação ter sido publicado.

![chlimage_1-422](assets/chlimage_1-422.png)

## Visualizando catálogo na publicação {#viewing-catalog-on-publish}

Depois que tudo tiver sido configurado a partir do ambiente do autor e publicado, a experiência de usar o catálogo para encontrar os recursos de ativação poderá ocorrer no ambiente de publicação.

Se nenhuma namespace de tag for exibida no menu suspenso, verifique se as permissões foram definidas corretamente no ambiente de publicação.

Se as namespaces de tags forem adicionadas e estiverem ausentes, verifique se as tags e o site foram publicados novamente.

Se nenhum recurso de ativação for exibido após selecionar uma tag ao exibir o catálogo, verifique se há uma tag da(s) namespace(s) do catálogo aplicada(s) ao recurso de ativação.

![chlimage_1-423](assets/chlimage_1-423.png)

