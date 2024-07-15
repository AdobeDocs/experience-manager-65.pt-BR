---
title: Personalização do lado do servidor
description: Saiba mais sobre a personalização do lado do servidor nas comunidades do Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Personalização do lado do servidor {#server-side-customization}

| **[⇐ Feature Essentials](essentials.md)** | **[Personalização no lado do cliente ^](client-customize.md)** |
|---|---|
|   | **[Helpers do Handlebars do SCF ^](handlebars-helpers.md)** |

## APIs Java™ {#java-apis}

>[!NOTE]
>
>A localização do pacote de APIs do Communities está sujeita a alterações ao atualizar de uma versão principal para a próxima.

### Interface do SocialComponent {#socialcomponent-interface}

SocialComponents são POJOs que representam um recurso de um recurso do AEM Communities. Idealmente, cada SocialComponent representa um resourceType específico com GETters expostos que fornecem dados ao cliente para que o recurso seja representado com precisão. Toda lógica de negócios e visualização é encapsulada no SocialComponent, incluindo as informações de sessão do visitante do site, se necessário.

A interface define um conjunto básico de GETters necessários para representar um recurso. É importante observar que a interface estipula os métodos Map&lt;String, Object> getAsMap() e String toJSONString() necessários para renderizar modelos Handlebars e expor pontos de extremidade GET JSON para os recursos.

Todas as classes SocialComponent devem implementar a interface `com.adobe.cq.social.scf.SocialComponent`

### Interface do componente SocialCollection {#socialcollectioncomponent-interface}

A interface SocialCollectionComponent estende a interface SocialComponent para representar melhor os recursos que são coleções de outros recursos.

Todas as classes SocialCollectionComponent devem implementar a interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface do SocialComponentFactory {#socialcomponentfactory-interface}

Um SocialComponentFactory (fábrica) registra um SocialComponent com a estrutura. A fábrica fornece um meio de informar à estrutura quais SocialComponents estão disponíveis para um determinado resourceType e sua classificação de prioridade quando vários SocialComponents são identificados.

Um SocialComponentFactory é responsável pela criação de uma instância do SocialComponent selecionado, permitindo injetar todas as dependências necessárias para o SocialComponent na fábrica usando práticas de ID.

Um SocialComponentFactory é um serviço OSGi e tem acesso a outros serviços OSGi que podem ser passados para o SocialComponent por meio de um construtor.

Todas as classes SocialComponentFactory devem implementar a interface `com.adobe.cq.social.scf.SocialComponentFactory`

Uma implementação do método SocialComponentFactory.getPriority() deve retornar o valor mais alto para a fábrica a ser usada para o resourceType fornecido conforme retornado por getResourceType().

### Interface do SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

O SocialComponentFactoryManager (gerenciador) gerencia todos os SocialComponents registrados com a estrutura e é responsável por selecionar o SocialComponentFactory a ser usado para um determinado recurso (resourceType). Se nenhuma fábrica estiver registrada para um resourceType específico, o gerente retornará uma fábrica com o supertipo mais próximo para o recurso especificado.

Um SocialComponentFactoryManager é um serviço OSGi e tem acesso a outros serviços OSGi que podem ser passados para o SocialComponent por meio de um construtor.

Um identificador para o serviço OSGi é obtido chamando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Solicitações POST {#http-api-post-requests}

#### Classe Pós-Operação {#postoperation-class}

Os pontos de extremidade de POST da API HTTP são classes PostOperation definidas pela implementação da interface `SlingPostOperation` (pacote `org.apache.sling.servlets.post`).

A implementação do ponto de extremidade `PostOperation` define `sling.post.operation` como um valor ao qual a operação responde. Todas as solicitações POST com um parâmetro:operation definido para esse valor são delegadas a essa classe de implementação.

O `PostOperation` chama o `SocialOperation` que executa as ações necessárias para a operação.

O `PostOperation` recebe o resultado de `SocialOperation` e retorna a resposta apropriada ao cliente.

#### Classe SocialOperation {#socialoperation-class}

Cada ponto de extremidade `SocialOperation` estende a classe AbstractSocialOperation e substitui o método `performOperation()`. Este método executa todas as ações necessárias para concluir a operação e retornar um `SocialOperationResult`, ou então lança um `OperationException`. Nesse caso, um status de erro HTTP com uma mensagem, se disponível, é retornado no lugar da resposta JSON normal ou do código de status HTTP de sucesso.

Estender `AbstractSocialOperation` possibilita a reutilização de `SocialComponents` para enviar respostas JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

A classe `SocialOperationResult` é retornada como resultado de `SocialOperation` e é composta por `SocialComponent`, código de status HTTP e mensagem de status HTTP.

`SocialComponent` representa o recurso que foi afetado pela operação.

Para uma operação Criar, o `SocialComponent` incluído no `SocialOperationResult` representa o recurso criado e, para uma operação Atualizar, ele representa o recurso que foi alterado pela operação. Nenhum `SocialComponent` foi retornado para uma operação Delete.

Os códigos de status HTTP bem-sucedidos usados são:

* 201 para Criar operações
* 200 para operações de atualização
* 204 para operações de exclusão

#### Classe OperationException {#operationexception-class}

Um `OperationExcepton` é lançado ao executar uma operação se a solicitação não for válida ou ocorrer algum outro erro. Por exemplo, erros internos, valores de parâmetro incorretos ou permissões inadequadas. Um `OperationException` é composto de um código de status HTTP e uma mensagem de erro, que são retornados ao cliente como resposta ao `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

A estrutura do componente social recomenda que a lógica de negócios responsável por executar a operação não seja implementada na classe `SocialOperation`, mas delegada a um serviço OSGi. Usar um serviço OSGi para lógica de negócios permite que um `SocialComponent`, implementado por um ponto de extremidade `SocialOperation`, seja integrado a outro código e tenha uma lógica de negócios diferente aplicada.

Todas as classes `OperationService` estendem `AbstractOperationService`, permitindo extensões adicionais que podem conectar-se à operação que está sendo executada. Cada operação no serviço é representada por uma classe `SocialOperation`. A classe `OperationExtensions` pode ser invocada durante a execução da operação chamando os métodos

* `performBeforeActions()`

  Permite pré-verificações/pré-processamento e validações
* `performAfterActions()`

  Permite editar mais recursos ou chamar eventos, fluxos de trabalho personalizados etc.

#### Classe OperationExtension {#operationextension-class}

As classes `OperationExtension` são pedaços de código personalizados que podem ser inseridos em uma operação, permitindo a personalização de operações para atender às necessidades comerciais. Os consumidores do componente podem adicionar funcionalidade de forma dinâmica e incremental ao componente. O padrão de extensão/gancho permite que os desenvolvedores se concentrem exclusivamente nas próprias extensões e remove a necessidade de copiar e substituir operações e componentes inteiros.

## Código de exemplo {#sample-code}

O código de exemplo está disponível no repositório [Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud). Procurar projetos com prefixo `aem-communities` ou `aem-scf`.

## Práticas recomendadas {#best-practices}

Consulte a seção [Diretrizes de codificação](code-guide.md) para obter várias diretrizes de codificação e práticas recomendadas para desenvolvedores do AEM Communities.

Consulte também [Provedor de Recurso de Armazenamento (SRP) para UGC](srp.md) para saber mais sobre como acessar conteúdo gerado pelo usuário.

| **[⇐ Feature Essentials](essentials.md)** | **[Personalização no lado do cliente ^](client-customize.md)** |
|---|---|
|   | **[Helpers do Handlebars do SCF ^](handlebars-helpers.md)** |
