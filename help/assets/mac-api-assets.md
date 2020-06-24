---
title: API HTTP de ativos em [!DNL Adobe Experience Manager].
description: Crie, leia, atualize, exclua, gerencie ativos digitais usando a API HTTP em [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 307a1db2e5bbb72d730c89ba14f5ce02b96c108d
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 1%

---


# API HTTP de ativos {#assets-http-api}

## Visão geral {#overview}

A API HTTP Assets permite operações de criação-leitura-atualização-exclusão (CRUD) em ativos digitais, incluindo metadados, execuções e comentários, juntamente com conteúdo estruturado usando Fragmentos [!DNL Experience Manager] de conteúdo. Ele é exposto em `/api/assets` e é implementado como REST API. Inclui [suporte para Fragmentos](/help/assets/assets-api-content-fragments.md)de conteúdo.

Para acessar a API:

1. Abra o documento de serviço da API em `https://[hostname]:[port]/api.json`.
1. Siga o link de serviço Ativos à esquerda para `https://[hostname]:[server]/api/assets.json`.

A resposta da API é um arquivo JSON para alguns tipos MIME e um código de resposta para todos os tipos MIME. A resposta JSON é opcional e pode não estar disponível, por exemplo, para arquivos PDF. Confie no código de resposta para obter mais análises ou ações.

Após o Tempo [!UICONTROL desligado], um ativo e suas representações não estão disponíveis por meio da interface da [!DNL Assets] Web e da API HTTP. A API retornará uma mensagem de erro 404 se o Tempo [!UICONTROL ligado] estiver no futuro ou Tempo [!UICONTROL desligado] estiver no passado.

## Fragmentos de conteúdo {#content-fragments}

Um fragmento [de](/help/assets/content-fragments/content-fragments.md) conteúdo é um tipo especial de ativo. Pode ser usado para acessar dados estruturados, como textos, números, datas, entre outros. Como há várias diferenças nos `standard` ativos (como imagens ou documentos), algumas regras adicionais se aplicam ao manuseio de fragmentos de conteúdo.

Para obter mais informações, consulte Suporte a fragmentos [de conteúdo na API](/help/assets/assets-api-content-fragments.md)HTTP dos ativos Experience Manager.

## Modelo de dados {#data-model}

A API HTTP Assets expõe dois elementos principais, pastas e ativos (para ativos padrão).

Além disso, expõe elementos mais detalhados para os modelos de dados personalizados que descrevem o conteúdo estruturado em Fragmentos de conteúdo. Consulte Modelos [de dados de fragmento de](/help/assets/assets-api-content-fragments.md#content-fragments) conteúdo para obter mais informações.

### Pastas {#folders}

As pastas são como diretórios em sistemas de arquivos tradicionais. São container para outras pastas ou asserções. As pastas têm os seguintes componentes:

**Entidades**: As entidades de uma pasta são seus elementos filho, que podem ser pastas e ativos.

**Propriedades**:

* `name` é o nome da pasta. É o mesmo que o último segmento no caminho do URL sem a extensão.
* `title` é um título opcional da pasta que pode ser exibido em vez de seu nome.

>[!NOTE]
>
>Algumas propriedades da pasta ou do ativo são mapeadas para um prefixo diferente. O `jcr` prefixo de `jcr:title`, `jcr:description`e `jcr:language` é substituído pelo `dc` prefixo. Daí no JSON retornado, `dc:title` e `dc:description` contém os valores de `jcr:title` e `jcr:description`, respectivamente.

**As Pastas de links** expõem três links:

* `self`: Vincule-se a si mesmo.
* `parent`: Link para a pasta pai.
* `thumbnail`: (Opcional) link para uma imagem em miniatura da pasta.

### Ativos {#assets}

No Experience Manager, um ativo contém os seguintes elementos:

* As propriedades e os metadados do ativo.
* Várias representações, como a representação original (que é o ativo carregado originalmente), uma miniatura e várias outras representações. As representações adicionais podem ser imagens de tamanhos diferentes, codificações de vídeo diferentes ou páginas extraídas de arquivos PDF ou [!DNL Adobe InDesign] PDF.
* Comentários opcionais.

Para obter informações sobre elementos em Fragmentos de conteúdo, consulte Suporte a fragmentos de [conteúdo na API](/help/assets/assets-api-content-fragments.md#content-fragments)HTTP dos ativos de Experience Manager.

Em [!DNL Experience Manager] uma pasta há os seguintes componentes:

* Entidades: Os filhos dos ativos são suas representações.
* Propriedades.
* Links.

A API HTTP Assets inclui os seguintes recursos:

* Recuperar uma lista de pastas.
* Criar uma pasta.
* Criar um ativo.
* Atualize o binário do ativo.
* Atualize os metadados do ativo.
* Crie uma representação de ativo.
* Atualizar uma representação de ativo.
* Crie um comentário de ativo.
* Copie uma pasta ou um ativo.
* Mova uma pasta ou um ativo.
* Exclua uma pasta, ativo ou representação.

>[!NOTE]
>
>Para facilitar a leitura, os seguintes exemplos omitem a notação cURL completa. Na verdade, a notação correlaciona-se com o [Resty](https://github.com/micha/resty) , que é um invólucro de scripts para `cURL`.

**Pré-requisitos**

* Acesso `https://[aem_server]:[port]/system/console/configMgr`.
* Navegue até Filtro **[!UICONTROL CSRF do]** Adobe Granite.
* Verifique se a propriedade Métodos **[!UICONTROL de]** filtro inclui: `POST`, `PUT`, `DELETE`.

## Recuperar uma listagem de pastas {#retrieve-a-folder-listing}

Recupera uma representação Siren de uma pasta existente e de suas entidades filhas (subpastas ou ativos).

**Solicitação**: `GET /api/assets/myFolder.json`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - sucesso.
* 404 - NOT FOUND - a pasta não existe ou não está acessível.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

**Resposta**: A classe da entidade retornada é um ativo ou uma pasta. As propriedades de entidades contidas são um subconjunto do conjunto completo de propriedades de cada entidade. Para obter uma representação completa da entidade, os clientes devem recuperar o conteúdo do URL apontado pelo link com um `rel` de `self`.

## Criar uma pasta {#create-a-folder}

Cria um novo `sling`: `OrderedFolder` no caminho determinado. Se um nome `*` for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro como nome de nó. Aceitos como dados de solicitação é uma representação SIREEN da nova pasta ou um conjunto de pares nome-valor, codificados como `application/www-form-urlencoded` ou `multipart`/ `form`- `data`, úteis para criar uma pasta diretamente de um formulário HTML. Além disso, as propriedades da pasta podem ser especificadas como parâmetros de query de URL.

Uma chamada de API falhará com um código de `500` resposta se o nó pai do caminho fornecido não existir. Uma chamada retornará um código de resposta `409` se a pasta já existir.

**Parâmetros**: `name` é o nome da pasta.

**Solicitar**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - sobre criação bem sucedida.
* 409 - CONFLICT - se a pasta já existir.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Criar um ativo {#create-an-asset}

Coloque o arquivo fornecido no caminho fornecido para criar um ativo no repositório DAM. Se um nome `*` for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro ou o nome do arquivo como nome do nó.

**Parâmetros**: Os parâmetros são `name` para o nome do ativo e `file` para a referência do arquivo.

**Solicitar**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se o Ativo tiver sido criado com êxito.
* 409 - CONFLITO - se o Ativo já existir.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Atualizar um binário de ativo {#update-asset-binary}

Atualiza o binário de um ativo (execução com o nome original). Uma atualização aciona o fluxo de trabalho de processamento de ativos padrão para ser executado, se estiver configurado.

**Solicitação**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se Asset (Ativo) tiver sido atualizado com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Atualizar metadados do ativo {#update-asset-metadata}

Atualiza as propriedades de metadados do ativo. Se você atualizar qualquer propriedade na `dc:` namespace, a API atualizará a mesma propriedade na `jcr` namespace. A API não sincroniza as propriedades nas duas namespaces.

**Solicitação**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se Asset (Ativo) tiver sido atualizado com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Criar uma representação de ativo {#create-an-asset-rendition}

Crie uma nova representação de ativo para um ativo. Se o nome do parâmetro de solicitação não for fornecido, o nome do arquivo será usado como nome de execução.

**Parâmetros**: Os parâmetros são `name` para o nome da representação e `file` como uma referência de arquivo.

**Solicitar**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CREATED - se a Renderização tiver sido criada com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Atualizar uma representação de ativo {#update-an-asset-rendition}

As atualizações substituem respectivamente uma representação de ativo pelos novos dados binários.

**Solicitação**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se Renderização tiver sido atualizada com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Adicionar um comentário em um ativo {#create-an-asset-comment}

Cria um novo comentário de ativo.

**Parâmetros**: Os parâmetros são `message` para o corpo da mensagem do comentário e `annotationData` para os dados de anotação no formato JSON.

**Solicitação**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se Comentário tiver sido criado com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Copiar uma pasta ou um ativo {#copy-a-folder-or-asset}

Copia uma pasta ou ativo disponível no caminho fornecido para um novo destino.

**Cabeçalhos** de solicitação: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para copiar o recurso.
* `X-Depth` - quer `infinity` quer `0`. O uso `0` só copia o recurso e suas propriedades, e não seus filhos.
* `X-Overwrite` - Use `F` para evitar a substituição de um ativo no destino existente.

**Solicitação**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo tiver sido copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo tiver sido copiado para um destino existente.
* 412 - PRECONDITION FAILED - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Mover uma pasta ou um ativo {#move-a-folder-or-asset}

Move uma pasta ou um ativo no caminho fornecido para um novo destino.

**Cabeçalhos** de solicitação: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para copiar o recurso.
* `X-Depth` - quer `infinity` quer `0`. O uso `0` só copia o recurso e suas propriedades, e não seus filhos.
* `X-Overwrite` - Use `T` para forçar a exclusão de um recurso existente ou `F` para evitar a substituição de um recurso existente.

**Solicitação**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo tiver sido copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo tiver sido copiado para um destino existente.
* 412 - PRECONDITION FAILED - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Excluir uma pasta, um ativo ou uma representação {#delete-a-folder-asset-or-rendition}

Exclui um recurso (-tree) no caminho fornecido.

**Solicitar**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se a pasta tiver sido excluída com êxito.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.
