---
title: Personalização do lado do servidor
seo-title: Server-side Customization
description: Personalização do lado do servidor no AEM Communities
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Personalização do lado do servidor {#server-side-customization}

| **[Fundamentos dos recursos ⇐](essentials.md)** | **[Personalização do lado do cliente](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers †](handlebars-helpers.md)** |

## APIs Java {#java-apis}

>[!NOTE]
>
>A localização do pacote de APIs do Communities está sujeita a alterações ao atualizar de uma versão principal para a próxima.

### Interface do SocialComponent {#socialcomponent-interface}

Os componentes sociais são POJOs que representam um recurso para um recurso do AEM Communities. Idealmente, cada SocialComponent representa um resourceType específico com GETters expostos que fornecem dados ao cliente para que o recurso seja representado com precisão. Toda lógica de negócios e lógica de visualização é encapsulada no SocialComponent, incluindo as informações de sessão do visitante do site, se necessário.

A interface define um conjunto básico de GETters que são necessários para representar um recurso. Importante: a interface estipula o Mapa&lt;string object=&quot;&quot;> os métodos getAsMap() e String toJSONString() necessários para renderizar modelos Handlebars e expor os endpoints JSON do GET para os recursos.

Todas as classes SocialComponent devem implementar a interface `com.adobe.cq.social.scf.SocialComponent`

### Interface do SocialCollectionComponent {#socialcollectioncomponent-interface}

A interface SocialCollectionComponent estende a interface SocialComponent para representar melhor os recursos que são coleções de outros recursos.

Todas as classes SocialCollectionComponent devem implementar a interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface do SocialComponentFactory {#socialcomponentfactory-interface}

Um SocialComponentFactory (fábrica) registra um SocialComponent com a estrutura. A fábrica fornece um meio de permitir que a estrutura saiba quais componentes sociais estão disponíveis para um determinado tipo de recurso e sua classificação de prioridade quando vários componentes sociais são identificados.

Um SocialComponentFactory é responsável pela criação de uma instância do SocialComponent selecionado, permitindo inserir todas as dependências necessárias para o SocialComponent da fábrica usando práticas de ID.

Um SocialComponentFactory é um serviço OSGi e tem acesso a outros serviços OSGi que podem ser passados para o SocialComponent por meio de um construtor.

Todas as classes SocialComponentFactory devem implementar a interface `com.adobe.cq.social.scf.SocialComponentFactory`

Uma implementação do método SocialComponentFactory.getPriority() deve retornar o valor mais alto para que a fábrica seja usada para o resourceType fornecido, conforme retornado por getResourceType().

### Interface do SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

O SocialComponentFactoryManager (gerente) gerencia todos os SocialComponents registrados com a estrutura e é responsável por selecionar o SocialComponentFactory a ser usado para um determinado recurso (resourceType). Se não houver fábricas registradas para um resourceType específico, o gerente retornará uma fábrica com o supertipo mais próximo para o recurso em questão.

Um SocialComponentFactoryManager é um serviço OSGi e tem acesso a outros serviços OSGi que podem ser passados para o SocialComponent por meio de um construtor.

Um identificador para o serviço OSGi é obtido chamando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Solicitações do POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Os pontos de extremidade POST da API HTTP são classes PostOperation definidas pela implementação do `SlingPostOperation` interface (pacote) `org.apache.sling.servlets.post`).

O `PostOperation` conjuntos de implementação de endpont `sling.post.operation` a um valor ao qual a operação responderá. Todas as solicitações de POST com um parâmetro:operation definido para esse valor serão delegadas a essa classe de implementação.

O `PostOperation` chama o `SocialOperation` que executa as ações necessárias para a operação.

O `PostOperation` recebe o resultado do `SocialOperation` e retorna a resposta apropriada ao cliente.

#### Classe SocialOperation {#socialoperation-class}

Cada `SocialOperation` endpoint estende a classe AbstractSocialOperation e substitui o método `performOperation()`. Este método executa todas as ações necessárias para concluir a operação e retornar um `SocialOperationResult` ou, caso contrário, coloque uma `OperationException`, nesse caso, um status de erro HTTP com uma mensagem, se disponível, é retornado no lugar da resposta JSON normal ou do código de status HTTP bem-sucedido.

Extensão `AbstractSocialOperation` permite a reutilização de `SocialComponents` para enviar respostas JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

O `SocialOperationResult` A classe é retornada como resultado da `SocialOperation` e é composto por um `SocialComponent`, código do status HTTP e mensagem de status HTTP.

O `SocialComponent` representa o recurso que foi afetado pela operação.

Para uma operação Criar , a variável `SocialComponent` incluídos na `SocialOperationResult` representa o recurso recém-criado e, para uma operação Update , representa o recurso que foi alterado pela operação. Não `SocialComponent` é retornado para uma operação Delete .

Os códigos de status HTTP bem-sucedidos usados são:

* 201 para criar operações
* 200 para operações de atualização
* 204 para operações de exclusão

#### Classe OperationException {#operationexception-class}

Um `OperationExcepton` pode ser lançado ao executar uma operação se a solicitação não for válida ou se algum outro erro ocorrer, como erros internos, valores de parâmetros incorretos, permissões inadequadas etc. Um `OperationException` é composto de um código de status HTTP e uma mensagem de erro, que são retornados ao cliente como a resposta ao `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

A estrutura do componente social recomenda que a lógica de negócios responsável pela execução da operação não seja implementada no `SocialOperation` , mas delegadas a um serviço OSGi. Usar um serviço OSGi para lógica de negócios permite `SocialComponent`, que tenha sido `SocialOperation` endpoint, para ser integrado a outro código e ter uma lógica comercial diferente aplicada.

Todos `OperationService` extensões de classes `AbstractOperationService`, permitindo extensões adicionais que podem ser conectadas à operação que está sendo executada. Cada operação no serviço é representada por um `SocialOperation` classe . O `OperationExtensions` A classe pode ser invocada durante a execução da operação chamando os métodos

* `performBeforeActions()`

   Permite pré-verificações/pré-processamento e validações
* `performAfterActions()`

   Permite modificação adicional de recursos ou chamada de eventos personalizados, fluxos de trabalho etc

#### Classe OperationExtension {#operationextension-class}

`OperationExtension` classes são partes de código personalizadas que podem ser inseridas em uma operação que permite a personalização de operações para atender às necessidades dos negócios. Os consumidores do componente podem adicionar funcionalidade de forma dinâmica e incremental ao componente. O padrão de extensão/gancho permite que os desenvolvedores se concentrem exclusivamente nas próprias extensões e remove a necessidade de copiar e substituir operações e componentes inteiros.

## Código de exemplo {#sample-code}

O código de amostra está disponível na seção [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) repositório. Procure projetos com o prefixo ou `aem-communities` ou `aem-scf`.

## Práticas recomendadas     {#best-practices}

Visualize o [Diretrizes de codificação](code-guide.md) para obter várias diretrizes de codificação e práticas recomendadas para desenvolvedores do AEM Communities.

Consulte também [Provedor de recursos de armazenamento (SRP) para UGC](srp.md) para saber mais sobre como acessar conteúdo gerado pelo usuário.

| **[Fundamentos dos recursos ⇐](essentials.md)** | **[Personalização do lado do cliente](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers †](handlebars-helpers.md)** |
