---
title: Suporte a token encapsulado
seo-title: Encapsulated Token Support
description: Saiba mais sobre o suporte ao Encapsulated Token no AEM.
seo-description: Learn about the Encapsulated Token support in AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: ed2cb35593780cd627c15f493e58d3b68c55519b
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# Suporte a token encapsulado{#encapsulated-token-support}

## Introdução {#introduction}

Por padrão, o AEM usa o Manipulador de autenticação de token para autenticar cada solicitação. No entanto, para servir solicitações de autenticação, o Manipulador de Autenticação de Token requer acesso ao repositório para cada solicitação. Isso acontece porque os cookies são usados para manter o estado de autenticação. Logicamente, o estado precisa ser mantido no repositório para validar solicitações subsequentes. Na verdade, isso significa que o mecanismo de autenticação é estático.

Este aspecto reveste-se de especial importância para a escalabilidade horizontal. Em uma configuração de várias instâncias, como o farm de publicação mostrado abaixo, o balanceamento de carga não pode ser obtido de maneira ideal. Com a autenticação de estado, o estado de autenticação persistente só estará disponível na instância em que o usuário é autenticado pela primeira vez.

![chlimage_1-33](assets/chlimage_1-33a.png)

Tome o seguinte cenário como exemplo:

Um usuário pode ser autenticado na instância de publicação um, mas se uma solicitação subsequente for para a instância de publicação dois, essa instância não terá esse estado de autenticação persistente, pois esse estado persistiu no repositório de publicar um e publicar dois terá seu próprio repositório.

A solução para isso é configurar conexões aderentes no nível do balanceador de carga. Com conexões aderentes, um usuário sempre seria direcionado para a mesma instância de publicação. Como consequência, não é possível um equilíbrio de carga verdadeiramente ótimo.

Caso uma instância de publicação se torne indisponível, todos os usuários autenticados nessa instância perderão sua sessão. Isso ocorre porque o acesso ao repositório é necessário para validar o cookie de autenticação.

## Autenticação sem estado com o token encapsulado {#stateless-authentication-with-the-encapsulated-token}

A solução para a escalabilidade horizontal é a autenticação sem estado com o uso do novo suporte de Token Encapsulado no AEM.

O Token Encapsulado é uma parte da criptografia que permite AEM criar e validar com segurança as informações de autenticação offline, sem acessar o repositório. Dessa forma, uma solicitação de autenticação pode ocorrer em todas as instâncias de publicação e sem necessidade de conexões aderentes. Ela também tem a vantagem de melhorar o desempenho da autenticação, pois o repositório não precisa ser acessado para cada solicitação de autenticação.

Você pode ver como isso funciona em uma implantação distribuída geograficamente com autores do MongoMK e instâncias de publicação do TarMK abaixo:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>Observe que o Encapsulated Token é sobre autenticação. Isso garante que o cookie possa ser validado sem ter que acessar o repositório. No entanto, ainda é necessário que o usuário exista em todas as instâncias e que as informações armazenadas nesse usuário possam ser acessadas por cada instância.
>
>Por exemplo, se um novo usuário for criado na instância de publicação número um, devido ao funcionamento do Token Encapsulado, ele será autenticado com êxito na publicação número dois. Se o usuário não existir na segunda instância de publicação, a solicitação ainda não será bem-sucedida.

## Configuração do token encapsulado {#configuring-the-encapsulated-token}

>[!NOTE]
>Todos os manipuladores de autenticação que sincronizam usuários e dependem da autenticação de token (como SAML &amp; OAuth) só funcionarão com tokens encapsulados se:
>
>* As sessões adesivas estão ativadas ou
>
>* Os usuários já são criados no AEM quando a sincronização é iniciada. Isso significa que os tokens encapsulados não serão aceitos em situações em que os manipuladores **criar** durante o processo de sincronização.


Há algumas coisas que você precisa considerar ao configurar o Token encapsulado:

1. Devido à criptografia envolvida, todas as instâncias precisam ter a mesma chave HMAC. Desde o AEM 6.3, o material principal não é mais armazenado no repositório, mas no sistema de arquivos real. Com isso em mente, a melhor maneira de replicar as chaves é copiá-las do sistema de arquivos da instância de origem para a instância de destino para a qual você deseja replicar as chaves. Consulte mais informações em &quot;Replicação da chave HMAC&quot; abaixo.
1. O token encapsulado precisa ser ativado. Isso pode ser feito através do Console da Web.

### Replicação da chave HMAC {#replicating-the-hmac-key}

Para replicar a chave entre instâncias, é necessário:

1. Acesse a instância AEM, normalmente uma instância de autor, que contém o material principal a ser copiado;
1. Localize a variável `com.adobe.granite.crypto.file` no sistema de arquivos local. Por exemplo, neste caminho:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   O `bundle.info` o arquivo dentro de cada pasta identificará o nome do pacote.

1. Navegue até a pasta de dados. Por exemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Copie o HMAC e os arquivos principais.
1. Em seguida, vá para a instância de destino para a qual deseja duplicar a chave HMAC e navegue até a pasta de dados. Por exemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Cole os dois arquivos copiados anteriormente.
1. [Atualizar o pacote de criptografia](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) se a instância de destino já estiver em execução.

1. Repita as etapas acima para todas as instâncias para as quais deseja replicar a chave.

#### Ativação do token encapsulado {#enabling-the-encapsulated-token}

Depois que a chave HMAC tiver sido replicada, você poderá habilitar o Token Encapsulado por meio do Console da Web:

1. Aponte seu navegador para `https://serveraddress:port/system/console/configMgr`
1. Procure uma entrada chamada **Manipulador de Autenticação de Token do Adobe Granite** e clique nele.
1. Na janela a seguir, marque a opção **Ativar suporte a token encapsulado** e pressione **Salvar**.
