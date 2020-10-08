---
title: Personalização do servidor
seo-title: Personalização do servidor
description: Personalização do lado do servidor no AEM Communities
seo-description: Personalização do lado do servidor no AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# Personalização do servidor {#server-side-customization}

| **[⇐ Fundamentos de recursos](essentials.md)** | **[Localização da personalização do cliente](client-customize.md)** |
|---|---|
|  | **[Auxiliares da proteção contra a fraude SCF](handlebars-helpers.md)** |

## APIs Java {#java-apis}

>[!NOTE]
>
>A localização do pacote de APIs de Comunidades está sujeita a alterações ao atualizar de uma versão principal para a próxima.

### Interface do SocialComponent {#socialcomponent-interface}

SocialComponents são POJOs que representam um recurso para um recurso do AEM Communities. Idealmente, cada SocialComponent representa um resourceType específico com GETters expostos que fornecem dados ao cliente para que o recurso seja representado com precisão. Toda lógica de negócios e lógica de visualização é encapsulada no SocialComponent, incluindo as informações de sessão do visitante do site, se necessário.

A interface define um conjunto básico de GETters que são necessários para representar um recurso. O importante é que a interface estipula os métodos Map&lt;String, Object> getAsMap() e String toJSONString() necessários para renderizar os modelos Handlebars e expor os endpoints JSON do GET aos recursos.

Todas as classes SocialComponent devem implementar a interface `com.adobe.cq.social.scf.SocialComponent`

### Interface SocialCollectionComponent {#socialcollectioncomponent-interface}

A interface SocialCollectionComponent estende a interface SocialComponent para representar melhor os recursos que são coleções de outros recursos.

Todas as classes SocialCollectionComponent devem implementar a interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface SocialComponentFactory {#socialcomponentfactory-interface}

Uma SocialComponentFactory (fábrica) registra um SocialComponent com a estrutura. A fábrica fornece uma forma de permitir que a estrutura saiba quais componentes sociais estão disponíveis para um determinado tipo de recurso e sua classificação de prioridade quando vários componentes sociais são identificados.

Um SocialComponentFactory é responsável por criar uma instância do SocialComponent selecionado, possibilitando a inserção de todas as dependências necessárias para o SocialComponent da fábrica usando práticas de ID.

Um SocialComponentFactory é um serviço OSGi e tem acesso a outros serviços OSGi que podem ser transmitidos para o SocialComponent por meio de um construtor.

Todas as classes SocialComponentFactory devem implementar a interface `com.adobe.cq.social.scf.SocialComponentFactory`

Uma implementação do método SocialComponentFactory.getPriority() deve retornar o valor mais alto para que a fábrica seja usada para o resourceType fornecido, conforme retornado por getResourceType().

### Interface SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

O SocialComponentFactoryManager (gerente) gerencia todos os SocialComponents registrados com a estrutura e é responsável por selecionar SocialComponentFactory a ser usado para um determinado recurso (resourceType). Se nenhuma fábrica estiver registrada para um determinado resourceType, o gerente retornará uma fábrica com o supertipo mais próximo para o recurso em questão.

Um SocialComponentFactoryManager é um serviço OSGi e tem acesso a outros serviços OSGi que podem ser transmitidos para o SocialComponent por meio de um construtor.

Um identificador do serviço OSGi é obtido invocando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Solicitações de POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Os pontos finais da API HTTP são classes PostOperation definidas pela implementação da `SlingPostOperation` interface (pacote `org.apache.sling.servlets.post`).

A implementação do `PostOperation` endpont define `sling.post.operation` um valor ao qual a operação responderá. Todas as solicitações de POST com um parâmetro:operation definido para esse valor serão delegadas a essa classe de implementação.

O `PostOperation` chama as ações `SocialOperation` que executam as necessárias para a operação.

O `PostOperation` recebe o resultado do `SocialOperation` e retorna a resposta apropriada ao cliente.

#### Classe SocialOperation {#socialoperation-class}

Cada `SocialOperation` endpoint estende a classe AbstractSocialOperation e substitui o método `performOperation()`. Este método executa todas as ações necessárias para concluir a operação e retornar um ou `SocialOperationResult` outro aciona um `OperationException`, caso em que um status de erro HTTP com uma mensagem, se disponível, é retornado no lugar da resposta JSON normal ou do código de status HTTP de sucesso.

A extensão `AbstractSocialOperation` possibilita a reutilização de `SocialComponents` para enviar respostas JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

A `SocialOperationResult` classe é retornada como resultado do `SocialOperation` e é composta por uma mensagem de status HTTP, código de status `SocialComponent`HTTP e mensagem de status HTTP.

O `SocialComponent` representa o recurso que foi afetado pela operação.

Para uma operação Criar, o `SocialComponent` incluído na `SocialOperationResult` representa o recurso recém-criado e para uma operação Atualizar, representa o recurso que foi alterado pela operação. Não `SocialComponent` é retornado para uma operação Excluir.

Os códigos de status HTTP de sucesso usados são:

* 201 para operações de criação
* 200 para operações de atualização
* 204 para operações de exclusão

#### Classe OperationException {#operationexception-class}

Um erro `OperationExcepton` pode ser lançado ao executar uma operação se a solicitação não for válida ou se ocorrer algum outro erro, como erros internos, valores de parâmetros incorretos, permissões inadequadas etc. Um `OperationException` é composto por um código de status HTTP e uma mensagem de erro, que são retornados ao cliente como a resposta ao `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

A estrutura do componente social recomenda que a lógica comercial responsável pela execução da operação não seja implementada dentro da `SocialOperation` classe, mas delegada em um serviço OSGi. O uso de um serviço OSGi para lógica de negócios permite que um `SocialComponent`servidor, atuado por um `SocialOperation` terminal, seja integrado a outro código e tenha uma lógica de negócios diferente aplicada.

Todas as `OperationService` classes se estendem `AbstractOperationService`, permitindo extensões adicionais que podem ser conectadas à operação que está sendo executada. Cada operação no serviço é representada por uma `SocialOperation` classe. A `OperationExtensions` classe pode ser invocada durante a execução da operação chamando os métodos

* `performBeforeActions()`

   Permite pré-verificações/pré-processamento e validações
* `performAfterActions()`

   Permite a modificação adicional de recursos ou invocação de eventos personalizados, workflows etc

#### Classe OperationExtension {#operationextension-class}

`OperationExtension` classes são partes de código personalizadas que podem ser inseridas em uma operação permitindo a personalização de operações para atender às necessidades dos negócios. Os consumidores do componente podem adicionar funcionalidade de forma dinâmica e incremental ao componente. O padrão de extensão/gancho permite que os desenvolvedores se concentrem exclusivamente nas próprias extensões e remove a necessidade de copiar e substituir operações e componentes inteiros.

## Código de exemplo {#sample-code}

O código de amostra está disponível no repositório [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) . Procure projetos com prefixo `aem-communities` ou `aem-scf`.

## Práticas recomendadas     {#best-practices}

Visualização na seção Diretrizes [de](code-guide.md) codificação para obter várias diretrizes de codificação e práticas recomendadas para desenvolvedores AEM Communities.

Consulte também SRP ( [Armazenamento Resource Provider [Provedor de recursos do ]) para UGC](srp.md) para saber mais sobre como acessar conteúdo gerado pelo usuário.

| **[⇐ Fundamentos de recursos](essentials.md)** | **[Localização da personalização do cliente](client-customize.md)** |
|---|---|
|  | **[Auxiliares da proteção contra a fraude SCF](handlebars-helpers.md)** |

