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

| **[Feature Essentials](essentials.md)** | **[Personalização no lado do cliente ^](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ^](handlebars-helpers.md)** |

## APIs Java™ {#java-apis}

>[!NOTE]
>
>A localização do pacote de APIs do Communities está sujeita a alterações ao atualizar de uma versão principal para a próxima.

### Interface do SocialComponent {#socialcomponent-interface}

SocialComponents são POJOs que representam um recurso de um recurso do AEM Communities. Idealmente, cada SocialComponent representa um resourceType específico com GETters expostos que fornecem dados ao cliente para que o recurso seja representado com precisão. Toda lógica de negócios e visualização é encapsulada no SocialComponent, incluindo as informações de sessão do visitante do site, se necessário.

A interface define um conjunto básico de GETters necessários para representar um recurso. É importante observar que a interface estipula o Map&lt;string object=&quot;&quot;> Os métodos getAsMap() e String toJSONString() necessários para renderizar modelos Handlebars e expor pontos de extremidade GET JSON para recursos.

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

Os endpoints de POST da API HTTP são classes PostOperation definidas pela implementação do `SlingPostOperation` interface (pacote) `org.apache.sling.servlets.post`).

A variável `PostOperation` conjuntos de implementação de endpoint `sling.post.operation` a um valor ao qual a operação responde. Todas as solicitações POST com um parâmetro:operation definido para esse valor são delegadas a essa classe de implementação.

A variável `PostOperation` chama a variável `SocialOperation` que executa as ações necessárias para a operação.

A variável `PostOperation` recebe o resultado da variável `SocialOperation` e retorna a resposta apropriada ao cliente.

#### Classe SocialOperation {#socialoperation-class}

Each `SocialOperation` endpoint estende a classe AbstractSocialOperation e substitui o método `performOperation()`. Este método executa todas as ações necessárias para concluir a operação e retornar uma `SocialOperationResult` ou então jogue um `OperationException`. Nesse caso, um status de erro HTTP com uma mensagem, se disponível, é retornado no lugar da resposta JSON normal ou do código de status HTTP de sucesso.

Extensão `AbstractSocialOperation` possibilite a reutilização de `SocialComponents` para enviar respostas JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

A variável `SocialOperationResult` é retornada como o resultado da variável `SocialOperation` e é composto por um `SocialComponent`, código de status HTTP e mensagem de status HTTP.

A variável `SocialComponent` representa o recurso que foi afetado pela operação.

Para uma operação Criar, a variável `SocialComponent` incluído na `SocialOperationResult` representa o recurso criado e, para uma operação Update, representa o recurso que foi alterado pela operação. Não `SocialComponent` é retornado para uma operação Delete.

Os códigos de status HTTP bem-sucedidos usados são:

* 201 para Criar operações
* 200 para operações de atualização
* 204 para operações de exclusão

#### Classe OperationException {#operationexception-class}

Um `OperationExcepton` é lançado ao executar uma operação se a solicitação não for válida ou ocorrer algum outro erro. Por exemplo, erros internos, valores de parâmetro incorretos ou permissões inadequadas. Um `OperationException` é composto de um código de status HTTP e uma mensagem de erro, que são retornados ao cliente como resposta à `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

A estrutura da componente social recomenda que a lógica de negócios responsável pela execução da operação não seja implementada dentro do `SocialOperation` classe, mas delegado a um serviço OSGi. Usar um serviço OSGi para lógica de negócios permite uma `SocialComponent`, atuadas por um `SocialOperation` ponto de extremidade, para ser integrado a outro código e ter uma lógica de negócios diferente aplicada.

Todos `OperationService` extensão de classes `AbstractOperationService`, permitindo extensões adicionais que podem se conectar à operação que está sendo executada. Cada operação no serviço é representada por um `SocialOperation` classe. A variável `OperationExtensions` classe pode ser chamada durante a execução da operação chamando os métodos

* `performBeforeActions()`

  Permite pré-verificações/pré-processamento e validações
* `performAfterActions()`

  Permite editar mais recursos ou chamar eventos, fluxos de trabalho personalizados etc.

#### Classe OperationExtension {#operationextension-class}

A variável `OperationExtension` as classes são partes personalizadas de código que podem ser inseridas em uma operação, permitindo a personalização de operações para atender às necessidades dos negócios. Os consumidores do componente podem adicionar funcionalidade de forma dinâmica e incremental ao componente. O padrão de extensão/gancho permite que os desenvolvedores se concentrem exclusivamente nas próprias extensões e remove a necessidade de copiar e substituir operações e componentes inteiros.

## Código de exemplo {#sample-code}

O código de amostra está disponível no [GitHub da Adobe Experience Cloud](https://github.com/Adobe-Marketing-Cloud) repositório. Procurar projetos com prefixo `aem-communities` ou `aem-scf`.

## Práticas recomendadas {#best-practices}

Exibir o [Diretrizes de codificação](code-guide.md) para várias diretrizes de codificação e práticas recomendadas para desenvolvedores do AEM Communities.

Consulte também [Provedor de recurso de armazenamento (SRP) para UGC](srp.md) para saber mais sobre como acessar conteúdo gerado pelo usuário.

| **[Feature Essentials](essentials.md)** | **[Personalização no lado do cliente ^](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ^](handlebars-helpers.md)** |
