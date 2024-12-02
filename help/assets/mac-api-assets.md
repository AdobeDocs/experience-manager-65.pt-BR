---
title: API HTTP [!DNL Assets].
description: Criar, ler, atualizar, excluir, gerenciar ativos digitais usando a API HTTP em [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 1%

---

# API HTTP [!DNL Assets] {#assets-http-api}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

## Visão geral {#overview}

A API HTTP do [!DNL Assets] permite operações create-read-update-delete (CRUD) em ativos digitais, incluindo metadados, representações e comentários, juntamente com conteúdo estruturado usando [!DNL Experience Manager] Fragmentos de conteúdo. Ele é exposto em `/api/assets` e é implementado como REST API. Inclui [suporte para Fragmentos de conteúdo](/help/assets/assets-api-content-fragments.md).

Para acessar a API:

1. Abra o documento de serviço de API em `https://[hostname]:[port]/api.json`.
1. Siga o link do serviço [!DNL Assets] que leva a `https://[hostname]:[server]/api/assets.json`.

A resposta da API é um arquivo JSON para alguns tipos MIME e um código de resposta para todos os tipos MIME. A resposta JSON é opcional e pode não estar disponível, por exemplo, para arquivos PDF. Contar com o código de resposta para análise ou ações adicionais.

Após o [!UICONTROL Tempo Desativado], um ativo e suas representações não estarão disponíveis por meio da interface da Web do [!DNL Assets] e da API HTTP. A API retorna a mensagem de erro 404 se o [!UICONTROL Momento da ativação] estiver no futuro ou o [!UICONTROL Momento da desativação] estiver no passado.

>[!CAUTION]
>
>A [API HTTP atualiza as propriedades de metadados](#update-asset-metadata) no namespace `jcr`. No entanto, a interface do usuário Experience Manager atualiza as propriedades de metadados no namespace `dc`.

## Fragmentos de conteúdo {#content-fragments}

Um [fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md) é um tipo especial de ativo. Ele pode ser usado para acessar dados estruturados, como textos, números, datas, entre outros. Como há várias diferenças para `standard` ativos (como imagens ou documentos), algumas regras adicionais se aplicam à manipulação de fragmentos de conteúdo.

Para obter mais informações, consulte [Suporte a fragmentos de conteúdo na API HTTP do Experience Manager Assets](/help/assets/assets-api-content-fragments.md).

## Modelo de dados {#data-model}

A API HTTP do [!DNL Assets] expõe dois elementos principais, pastas e ativos (para ativos padrão).

Além disso, ele expõe elementos mais detalhados para os modelos de dados personalizados que descrevem o conteúdo estruturado em fragmentos de conteúdo. Consulte [Modelos de dados de fragmento de conteúdo](/help/assets/assets-api-content-fragments.md#content-fragments) para obter mais informações.

### Pastas {#folders}

As pastas são como diretórios em sistemas de arquivos tradicionais. Eles são containers para outras pastas ou asserções. As pastas têm os seguintes componentes:

**Entidades**: as entidades de uma pasta são seus elementos secundários, que podem ser pastas e ativos.

**Propriedades**:

* `name` é o nome da pasta. É o mesmo que o último segmento no caminho do URL sem a extensão.
* `title` é um título opcional da pasta que pode ser exibido em vez do seu nome.

>[!NOTE]
>
>Algumas propriedades da pasta ou do ativo são mapeadas para um prefixo diferente. O prefixo `jcr` de `jcr:title`, `jcr:description` e `jcr:language` foi substituído pelo prefixo `dc`. Portanto, no JSON retornado, `dc:title` e `dc:description` contêm os valores de `jcr:title` e `jcr:description`, respectivamente.

**Links** As pastas expõem três links:

* `self`: Vincular a si mesmo.
* `parent`: Vincular à pasta pai.
* `thumbnail`: (Opcional) link para uma imagem em miniatura da pasta.

### Ativos {#assets}

No Experience Manager, um ativo contém os seguintes elementos:

* As propriedades e os metadados do ativo.
* Várias representações, como a representação original (que é o ativo carregado originalmente), uma miniatura e várias outras representações. Representações adicionais podem ser imagens de diferentes tamanhos, diferentes codificações de vídeo ou páginas extraídas de arquivos PDF ou [!DNL Adobe InDesign].
* Comentários opcionais.

Para obter informações sobre elementos nos Fragmentos de conteúdo, consulte [Suporte a Fragmentos de conteúdo na API HTTP do Experience Manager Assets](/help/assets/assets-api-content-fragments.md#content-fragments).

Em [!DNL Experience Manager] uma pasta tem os seguintes componentes:

* Entidades: os filhos dos ativos são suas representações.
* Propriedades.
* Links.

A API HTTP [!DNL Assets] inclui os seguintes recursos:

* [Recuperar uma listagem de pastas](#retrieve-a-folder-listing).
* [Criar uma pasta](#create-a-folder).
* [Criar um ativo](#create-an-asset).
* [Atualizar binário de ativo](#update-asset-binary).
* [Atualizar metadados de ativos](#update-asset-metadata).
* [Criar uma representação de ativo](#create-an-asset-rendition).
* [Atualize uma representação de ativo](#update-an-asset-rendition).
* [Criar um comentário de ativo](#create-an-asset-comment).
* [Copiar uma pasta ou um ativo](#copy-a-folder-or-asset).
* [Mover uma pasta ou um ativo](#move-a-folder-or-asset).
* [Excluir uma pasta, ativo ou representação](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar a leitura, os exemplos a seguir omitem a notação completa de cURL. Na verdade, a notação se correlaciona com [Resty](https://github.com/micha/resty), que é um wrapper de scripts para `cURL`.

**Pré-requisitos**

* Acessar `https://[aem_server]:[port]/system/console/configMgr`.
* Navegue até **[!UICONTROL Filtro CSRF do Adobe Granite]**.
* Verifique se a propriedade **[!UICONTROL Métodos de Filtro]** inclui: `POST`, `PUT`, `DELETE`.

## Recuperar uma listagem de pastas {#retrieve-a-folder-listing}

Recupera uma representação Sirene de uma pasta existente e de suas entidades filhas (subpastas ou ativos).

**Solicitação**: `GET /api/assets/myFolder.json`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - êxito.
* 404 - NÃO ENCONTRADO - a pasta não existe ou não está acessível.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

**Resposta**: a classe da entidade retornada é um ativo ou uma pasta. As propriedades das entidades contidas são um subconjunto do conjunto completo de propriedades de cada entidade. Para obter uma representação completa da entidade, os clientes devem recuperar o conteúdo da URL apontada pelo link com um `rel` de `self`.

## Criar uma pasta {#create-a-folder}

Cria um novo `sling`: `OrderedFolder` no caminho especificado. Se um `*` for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro como nome do nó. Aceita como dados de solicitação é uma representação Sirene da nova pasta ou um conjunto de pares nome-valor, codificados como `application/www-form-urlencoded` ou `multipart`/ `form`- `data`, úteis para criar uma pasta diretamente de um formulário HTML. Além disso, as propriedades da pasta podem ser especificadas como parâmetros de consulta de URL.

Uma chamada de API falhará com um código de resposta `500` se o nó pai do caminho fornecido não existir. Uma chamada retornará um código de resposta `409` se a pasta já existir.

**Parâmetros**: `name` é o nome da pasta.

**Solicitação**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - na criação bem-sucedida.
* 409 - CONFLITO - se a pasta já existir.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Criar um ativo {#create-an-asset}

Coloque o arquivo fornecido no caminho fornecido para criar um ativo no repositório DAM. Se for fornecido um `*` em vez de um nome de nó, o servlet usará o nome do parâmetro ou o nome do arquivo como nome do nó.

**Parâmetros**: os parâmetros são `name` para o nome do ativo e `file` para a referência do arquivo.

**Solicitação**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se o Ativo foi criado com sucesso.
* 409 - CONFLITO - se o Ativo já existir.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Atualizar um binário de ativo {#update-asset-binary}

Atualiza o binário de um ativo (representação com o nome original). Uma atualização aciona o fluxo de trabalho de processamento de ativos padrão para execução, se estiver configurado.

**Solicitação**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - se o Ativo foi atualizado com êxito.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Atualizar metadados de ativos {#update-asset-metadata}

Atualiza as propriedades dos metadados do ativo. Se você atualizar qualquer propriedade no namespace `dc:`, a API atualizará a mesma propriedade no namespace `jcr`. A API não sincroniza as propriedades nos dois namespaces.

**Solicitação**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - se o Ativo foi atualizado com êxito.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

### Sincronizar atualização de metadados entre o namespace `dc` e `jcr` {#sync-metadata-between-namespaces}

O método da API atualiza as propriedades de metadados no namespace `jcr`. As atualizações feitas usando a interface alteram as propriedades de metadados no namespace `dc`. Para sincronizar os valores de metadados entre o namespace `dc` e `jcr`, você pode criar um fluxo de trabalho e configurar o Experience Manager para executar o fluxo de trabalho na edição do ativo. Use um script ECMA para sincronizar as propriedades de metadados necessárias. O exemplo de script a seguir sincroniza a cadeia de caracteres de título entre `dc:title` e `jcr:title`.

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## Criar uma representação de ativo {#create-an-asset-rendition}

Criar uma representação de ativo para um ativo. Se o nome do parâmetro de solicitação não for fornecido, o nome do arquivo será usado como nome de representação.

**Parâmetros**: os parâmetros são `name` para o nome da representação e `file` como uma referência de arquivo.

**Solicitação**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se a Representação foi criada com sucesso.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Atualizar uma representação de ativo {#update-an-asset-rendition}

As atualizações substituem uma representação de ativo pelos novos dados binários, respectivamente.

**Solicitação**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - se a Representação foi atualizada com sucesso.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Adicionar um comentário em um ativo {#create-an-asset-comment}

Cria um novo comentário de ativo.

**Parâmetros**: os parâmetros são `message` para o corpo da mensagem do comentário e `annotationData` para os dados de Anotação no formato JSON.

**Solicitação**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se o Comentário foi criado com sucesso.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Copiar uma pasta ou um ativo {#copy-a-folder-or-asset}

Copia uma pasta ou ativo disponível no caminho fornecido para um novo destino.

**Solicitar Cabeçalhos**: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para o qual copiar o recurso.
* `X-Depth` - `infinity` ou `0`. Usar `0` copia somente o recurso e suas propriedades, não seus filhos.
* `X-Overwrite` - Use `F` para impedir a substituição de um ativo no destino existente.

**Solicitação**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo foi copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo foi copiado para um destino existente.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Mover uma pasta ou um ativo {#move-a-folder-or-asset}

Move uma pasta ou ativo no caminho determinado para um novo destino.

**Solicitar Cabeçalhos**: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para o qual copiar o recurso.
* `X-Depth` - `infinity` ou `0`. Usar `0` copia somente o recurso e suas propriedades, não seus filhos.
* `X-Overwrite` - Use `T` para forçar a exclusão de recursos existentes ou `F` para impedir a substituição de um recurso existente.

**Solicitação**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

Não use `/content/dam` no URL. Um exemplo de comando para mover ativos e substituir ativos existentes é:

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo foi copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo foi copiado para um destino existente.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Excluir uma pasta, um ativo ou uma representação {#delete-a-folder-asset-or-rendition}

Exclui um recurso (-tree) no caminho fornecido.

**Solicitação**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - se a pasta foi excluída com sucesso.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Dicas e limitações {#tips-best-practices-limitations}

* A [API HTTP atualiza as propriedades de metadados](#update-asset-metadata) no namespace `jcr`. No entanto, a interface do usuário Experience Manager atualiza as propriedades de metadados no namespace `dc`.

* A API HTTP do Assets não retorna os metadados completos. Os namespaces são codificados e somente esses namespaces são retornados. Para obter metadados completos, consulte o caminho do ativo `/jcr_content/metadata.json`.
