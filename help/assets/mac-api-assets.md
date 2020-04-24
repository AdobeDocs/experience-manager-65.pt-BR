---
title: API HTTP de ativos
description: Saiba mais sobre a implementação, o modelo de dados e os recursos da API HTTP do Assets. Use a API HTTP Assets para executar várias tarefas sobre ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# API HTTP de ativos {#assets-http-api}

## Visão geral {#overview}

A API HTTP Assets permite operações de criação-leitura-atualização-exclusão (CRUD) em Ativos, incluindo binários, metadados, execuções e comentários, juntamente com conteúdo estruturado usando Fragmentos de conteúdo AEM. Ele é exposto em `/api/assets` e é implementado como REST API. Inclui [suporte para Fragmentos](/help/assets/assets-api-content-fragments.md)de conteúdo.

Para acessar a API:

1. Abra o documento de serviço da API em `https://[hostname]:[port]/api.json`.
1. Siga o link de serviço Ativos à esquerda para `https://[hostname]:[server]/api/assets.json`.

A resposta da API é um arquivo JSON para alguns tipos MIME e um código de resposta para todos os tipos MIME. A resposta JSON é opcional e pode não estar disponível, por exemplo, para arquivos PDF. Confie no código de resposta para obter mais análises ou ações.

Depois do tempo de [!UICONTROL desligado], um ativo e suas representações não estão disponíveis por meio da interface da Web Ativos ou por meio da API HTTP. A API retornará uma mensagem de erro 404 se o Tempo [!UICONTROL ligado] estiver no futuro ou Tempo [!UICONTROL desligado] estiver no passado.

## Fragmentos de conteúdo {#content-fragments}

Um fragmento [de](/help/assets/content-fragments.md) conteúdo é um tipo especial de ativo. Pode ser usado para acessar dados estruturados, como textos, números, datas, entre outros. Como há várias diferenças nos `standard` ativos (como imagens ou documentos), algumas regras adicionais se aplicam ao manuseio de fragmentos de conteúdo.

Para obter mais informações, consulte Suporte a fragmentos [de conteúdo na API](/help/assets/assets-api-content-fragments.md)HTTP dos ativos AEM.

## Modelo de dados {#data-model}

A API HTTP Assets expõe dois elementos principais, pastas e ativos (para ativos padrão).

Além disso, expõe elementos mais detalhados para os modelos de dados personalizados que descrevem o conteúdo estruturado em Fragmentos de conteúdo. Consulte Modelos [de dados de fragmento de](/help/assets/assets-api-content-fragments.md#content-fragments) conteúdo para obter mais informações.

### Pastas {#folders}

As pastas são como diretórios em sistemas de arquivos tradicionais. São container para outras pastas ou asserções. As pastas têm os seguintes componentes:

**Entidades**: As entidades de uma pasta são seus elementos filho, que podem ser pastas e ativos.

**Propriedades**:
* `name`  — Nome da pasta. É o mesmo que o último segmento no caminho do URL sem a extensão
* `title` — Título opcional da pasta que pode ser exibida em vez de seu nome

>[!NOTE]
>
>Algumas propriedades da pasta ou do ativo são mapeadas para um prefixo diferente. O `jcr` prefixo de `jcr:title`, `jcr:description`e `jcr:language` é substituído pelo `dc` prefixo. Daí no JSON retornado, `dc:title` e `dc:description` contém os valores de `jcr:title` e `jcr:description`, respectivamente.

**As Pastas de links** expõem três links:
* `self`: Vincular a si mesmo
* `parent`: Link para a pasta pai
* `thumbnail`: (Opcional) link para uma imagem em miniatura de pasta

### Ativos {#assets}

No AEM, um ativo contém os seguintes elementos:

* As propriedades e os metadados do ativo
* Várias representações, como a representação original (que é o ativo carregado originalmente), uma miniatura e várias outras representações. As execuções adicionais podem ser imagens de tamanhos diferentes, codificações de vídeo diferentes ou páginas extraídas do PDF ou do InDesign.
* Comentários opcionais

Para obter informações sobre elementos em Fragmentos de conteúdo, consulte Suporte a fragmentos de [conteúdo na API](/help/assets/assets-api-content-fragments.md#content-fragments)HTTP dos ativos AEM.

No AEM, uma pasta tem os seguintes componentes:

* Entidades: Os filhos do Assets são suas representações.
* Propriedades
* Links

A API HTTP Assets inclui os seguintes recursos:

* Recuperar uma listagem de pastas
* Criar uma pasta
* Criar um ativo
* Atualizar binário de ativo
* Atualizar metadados do ativo
* Criar uma representação de ativo
* Atualizar uma representação de ativo
* Criar um comentário de ativo
* Copiar uma pasta ou um ativo
* Mover uma pasta ou um ativo
* Excluir uma pasta, ativo ou representação

>[!NOTE]
>
>Para facilitar a leitura, os seguintes exemplos omitem a notação cURL completa. Na verdade, a notação correlaciona-se com o [Resty](https://github.com/micha/resty) , que é um invólucro de scripts para `cURL`.

**Pré-requisitos**

* Ir para `https://[aem_server]:[port]/system/console/configMgr`.
* Navegue até Filtro **CSRF do** Adobe Granite.
* Verifique se a propriedade Métodos **de** filtro inclui: POSTAGEM, COLOCAR, EXCLUIR.

## Recuperar uma listagem de pastas {#retrieve-a-folder-listing}

Recupera uma representação Siren de uma pasta existente e de suas entidades filhas (subpastas ou ativos).

**Solicitar**

```
GET /api/assets/myFolder.json
```

**Códigos de resposta**

```
200 - OK - success
404 - NOT FOUND - folder does not exist or is not accessible
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

**Resposta**

A classe da entidade retornada é assets/folder.

As propriedades de entidades contidas são um subconjunto do conjunto completo de propriedades de cada entidade. Para obter uma representação completa da entidade, os clientes devem recuperar o conteúdo do URL apontado pelo link com um `rel` de `self`.

## Create a Folder {#create-a-folder}

Cria um novo `sling`: `OrderedFolder` no caminho determinado. Se um * for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro como nome de nó. Aceitos como dados de solicitação é uma representação SIREEN da nova pasta ou um conjunto de pares nome-valor, codificados como `application/www-form-urlencoded` ou `multipart`/ `form`- `data`, úteis para criar uma pasta diretamente de um formulário HTML. Além disso, as propriedades da pasta podem ser especificadas como parâmetros de query de URL.

A operação falhará com um código de `500` resposta se o nó pai do caminho especificado não existir. Se a pasta já existir, um código de `409` resposta será retornado.

**Parâmetros**

* `name` - Nome da pasta

**Solicitar**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

ou

```
POST /api/assets/* -F"name=myfolder" -F"title=My Folder"
```

**Códigos de resposta**

```
201 - CREATED - on successful creation
409 - CONFLICT - if folder already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Criar um ativo {#create-an-asset}

Cria um ativo DAM no caminho fornecido com o arquivo especificado. Se um * for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro ou o nome do arquivo como nome do nó.

**Parâmetros**

* `name` - Nome do ativo
* `file` - Referência do arquivo

**Solicitar**

```
POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"
```

ou

```
POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"
```

**Códigos de resposta**

```
201 - CREATED - if Asset has been created successfully
409 - CONFLICT - if Asset already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Atualizar binário do ativo {#update-asset-binary}

Atualiza um binário do Assets (execução com o nome original). Isso acionará o fluxo de trabalho padrão de Ativos, se configurado.

**Solicitar**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png
```

**Códigos de resposta**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Atualizar metadados do ativo {#update-asset-metadata}

Atualiza as propriedades de metadados do ativo. Se você atualizar qualquer propriedade na `dc:` namespace, a API atualizará a mesma propriedade na `jcr` namespace. A API não sincroniza as propriedades nas duas namespaces.

**Solicitar**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'
```

**Códigos de resposta**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Criar uma representação de ativo {#create-an-asset-rendition}

Cria uma nova representação de ativo para um ativo. Se o nome do parâmetro de solicitação não for fornecido, o nome do arquivo será usado como nome de execução.

**Parâmetros**

* `name` - Nome da representação
* `file` - Referência do arquivo

**Solicitar**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

ou

```
POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"
```

**Códigos de resposta**

```
201 - CREATED - if Rendition has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Atualizar uma representação de ativo {#update-an-asset-rendition}

As atualizações substituem respectivamente uma representação de ativo pelos novos dados binários.

**Solicitar**

```
PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png
```

**Códigos de resposta**

```
200 - OK - if Rendition has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Criar um comentário de ativo {#create-an-asset-comment}

Cria um novo comentário de ativo.

**Parâmetros**

* `message` - Mensagem
* `annotationData` - Dados de anotação (JSON)

**Solicitar**

```
POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"
```

**Códigos de resposta**

```
201 - CREATED - if Comment has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Copiar uma pasta ou um ativo {#copy-a-folder-or-asset}

Copia uma pasta ou ativo no caminho fornecido para um novo destino.

**Cabeçalhos de solicitação**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - 'F' to prevent overwriting an existing destination
```

**Solicitar**

```
COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"
```

**Códigos de resposta**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Mover uma pasta ou um ativo {#move-a-folder-or-asset}

Move uma pasta ou um ativo no caminho fornecido para um novo destino.

**Cabeçalhos de solicitação**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - either 'T' to force deletion of existing resources or 'F' to prevent overwriting an existing resource.
```

**Solicitar**

```
MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"
```

**Códigos de resposta**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Excluir uma pasta, um ativo ou uma representação {#delete-a-folder-asset-or-rendition}

Exclui um recurso (-tree) no caminho especificado.

**Solicitar**

```
DELETE /api/assets/myFolder
```

ou

```
DELETE /api/assets/myFolder/myAsset.png
```

ou

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**Códigos de resposta**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```
