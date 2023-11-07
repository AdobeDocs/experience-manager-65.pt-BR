---
title: Suporte a token encapsulado
description: Saiba mais sobre o suporte a token encapsulado no AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Suporte a token encapsulado{#encapsulated-token-support}

## Introdução {#introduction}

Por padrão, o AEM usa o Manipulador de autenticação de token para autenticar cada solicitação. No entanto, para atender às solicitações de autenticação, o Manipulador de autenticação de token requer acesso ao repositório para cada solicitação. Isso acontece porque os cookies são usados para manter o estado de autenticação. Logicamente, o estado precisa ser mantido no repositório para validar as solicitações subsequentes. Na verdade, isso significa que o mecanismo de autenticação tem estado.

Isso é particularmente importante para a escalabilidade horizontal. Em uma configuração de várias instâncias como o farm de publicação descrito abaixo, o balanceamento de carga não pode ser obtido de maneira ideal. Com a autenticação com monitoração de estado, o estado de autenticação persistente só estará disponível na instância em que o usuário for autenticado pela primeira vez.

![chlimage_1-33](assets/chlimage_1-33a.png)

Considere o seguinte cenário como exemplo:

Um usuário pode ser autenticado na instância de publicação um, mas se uma solicitação subsequente for para a instância de publicação dois, essa instância não terá esse estado de autenticação persistente, pois esse estado persistiu no repositório de publicação um e a instância dois tem seu próprio repositório.

A solução para isso é configurar conexões aderentes no nível do balanceador de carga. Com conexões aderentes, um usuário sempre seria direcionado para a mesma instância de publicação. Como consequência, o balanceamento de carga realmente ideal não é possível.

Se uma instância de publicação se tornar indisponível, todos os usuários autenticados nessa instância perderão sua sessão. Isso ocorre porque o acesso ao repositório é necessário para validar o cookie de autenticação.

## Autenticação sem estado com o token encapsulado {#stateless-authentication-with-the-encapsulated-token}

A solução para escalabilidade horizontal é a autenticação sem estado com o uso do novo suporte a token encapsulado no AEM.

O token encapsulado é uma parte da criptografia que permite ao AEM criar e validar com segurança as informações de autenticação off-line, sem acessar o repositório. Dessa forma, uma solicitação de autenticação pode ocorrer em todas as instâncias de publicação e sem a necessidade de conexões aderentes. Ela também tem a vantagem de melhorar o desempenho da autenticação, pois o repositório não precisa ser acessado para cada solicitação de autenticação.

Você pode ver como isso funciona em uma implantação distribuída geograficamente com autores MongoMK e instâncias de publicação TarMK abaixo:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>O token encapsulado é sobre autenticação. Ela garante que o cookie possa ser validado sem precisar acessar o repositório. No entanto, ainda é necessário que o usuário exista em todas as instâncias e que as informações armazenadas nesse usuário possam ser acessadas por cada instância.
>
>Por exemplo, se um novo usuário for criado na instância de publicação número um, devido ao modo como o token encapsulado funciona, ele será autenticado com êxito na publicação número dois. Se o usuário não existir na segunda instância de publicação, a solicitação ainda não será bem-sucedida.
>

## Configuração do token encapsulado {#configuring-the-encapsulated-token}

>[!NOTE]
>Todos os manipuladores de autenticação que sincronizam usuários e dependem da autenticação de token (como SAML e OAuth) só funcionarão com tokens encapsulados se:
>
>* Sessões adesivas estão ativadas ou
>
>* Os usuários já são criados no AEM quando a sincronização começa. Isso significa que os tokens encapsulados não serão suportados em situações em que os manipuladores **criar** usuários durante o processo de sincronização.

Há algumas coisas que você precisa considerar ao configurar o token encapsulado:

1. Devido à criptografia envolvida, todas as instâncias precisam ter a mesma chave HMAC. Desde o AEM 6.3, o material principal não é mais armazenado no repositório, mas no sistema de arquivos real. Com isso em mente, a melhor maneira de replicar as chaves é copiá-las do sistema de arquivos da instância de origem para o da instância de destino na qual você deseja replicar as chaves. Consulte mais informações em &quot;Replicação da chave HMAC&quot; abaixo.
1. O token encapsulado precisa ser ativado. Isso pode ser feito por meio do Console da Web.

### Replicação da chave HMAC {#replicating-the-hmac-key}

Para replicar a chave entre instâncias, é necessário:

1. Acesse a instância do AEM, normalmente uma instância de autor, que contém o material principal a ser copiado;
1. Localize o `com.adobe.granite.crypto.file` no sistema de arquivos local. Por exemplo, neste caminho:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   A variável `bundle.info` arquivo dentro de cada pasta identificará o nome do pacote.

1. Navegue até a pasta de dados. Por exemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Copie os arquivos HMAC e mestre.
1. Em seguida, vá para a instância de destino para a qual deseja duplicar a chave HMAC e navegue até a pasta de dados. Por exemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Cole os dois arquivos copiados anteriormente.
1. [Atualizar o pacote de criptografia](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) se a instância de destino já estiver em execução.

1. Repita as etapas acima para todas as instâncias para as quais deseja replicar a chave.

#### Ativação do token encapsulado {#enabling-the-encapsulated-token}

Depois que a chave HMAC for replicada, você poderá ativar o Encapsulated Token por meio do console da Web:

1. Aponte seu navegador para `https://serveraddress:port/system/console/configMgr`
1. Procure uma entrada chamada **Manipulador de autenticação de token do Adobe Granite** e clique nela.
1. Na janela a seguir, marque a caixa de seleção **Habilitar suporte a token encapsulado** e pressione **Salvar**.
