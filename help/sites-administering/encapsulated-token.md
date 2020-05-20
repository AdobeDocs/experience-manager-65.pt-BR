---
title: Suporte a token encapsulado
seo-title: Suporte a token encapsulado
description: Saiba mais sobre o suporte a token encapsulado no AEM.
seo-description: Saiba mais sobre o suporte a token encapsulado no AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
translation-type: tm+mt
source-git-commit: 215f062f80e7abfe35698743ce971394d01d0ed6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---


# Suporte a token encapsulado{#encapsulated-token-support}

## Introdução {#introduction}

Por padrão, o AEM usa o Manipulador de autenticação de token para autenticar cada solicitação. No entanto, para atender às solicitações de autenticação, o Token Authentication Handler requer acesso ao repositório para cada solicitação. Isso ocorre porque os cookies são usados para manter o estado de autenticação. Logicamente, o estado precisa ser persistente no repositório para validar solicitações subsequentes. Com efeito, isto significa que o mecanismo de autenticação é estável.

Isto é de particular importância para a escalabilidade horizontal. Em uma configuração de várias instâncias, como o farm de publicação descrito abaixo, o balanceamento de carga não pode ser obtido da maneira ideal. Com a autenticação com estado, o estado de autenticação persistente só estará disponível na instância em que o usuário foi autenticado pela primeira vez.

![chlimage_1-33](assets/chlimage_1-33a.png)

Veja o seguinte cenário como exemplo:

Um usuário pode ser autenticado na instância de publicação um, mas se uma solicitação subsequente for para a instância dois, essa instância não terá esse estado de autenticação persistente, pois esse estado persistiu no repositório de publicar um e publicar dois tem seu próprio repositório.

A solução para isso é configurar conexões rígidas no nível do balanceador de carga. Com conexões aderentes, um usuário sempre seria direcionado para a mesma instância de publicação. Consequentemente, não é possível um equilíbrio de carga verdadeiramente ótimo.

Caso uma instância de publicação fique indisponível, todos os usuários autenticados nessa instância perderão sua sessão. Isso ocorre porque o acesso ao repositório é necessário para validar o cookie de autenticação.

## Autenticação sem estado com o token encapsulado {#stateless-authentication-with-the-encapsulated-token}

A solução para a escalabilidade horizontal é a autenticação sem estado com o uso do novo suporte a token encapsulado no AEM.

O token encapsulado é uma parte da criptografia que permite ao AEM criar e validar com segurança as informações de autenticação offline, sem acessar o repositório. Dessa forma, uma solicitação de autenticação pode ocorrer em todas as instâncias de publicação e sem necessidade de conexões aderentes. Também tem a vantagem de melhorar o desempenho da autenticação, pois o repositório não precisa ser acessado para cada solicitação de autenticação.

Você pode ver como isso funciona em uma implantação distribuída geograficamente com os autores do MongoMK e as instâncias de publicação do TarMK abaixo:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>Observe que o Encapsulated Token é sobre autenticação. Ela garante que o cookie possa ser validado sem precisar acessar o repositório. No entanto, ainda é necessário que o usuário exista em todas as instâncias e que as informações armazenadas nesse usuário possam ser acessadas por cada instância.
>
>Por exemplo, se um novo usuário for criado na instância número um da publicação, devido ao modo como o Token encapsulado funciona, ele será autenticado com êxito na publicação número dois. Se o usuário não existir na segunda instância de publicação, a solicitação ainda não terá êxito.


## Configuração do token encapsulado {#configuring-the-encapsulated-token}

>[!NOTE]
>Todos os manipuladores de autenticação que sincronizam usuários e dependem da autenticação de token (como SAML e OAuth) funcionarão somente com tokens encapsulados se:
>
>* As sessões aderentes estão ativadas ou
   >
   >
* Os usuários já são criados no AEM quando os start de sincronização são executados. Isso significa que os tokens encapsulados não serão suportados em situações em que os manipuladores **criam** usuários durante o processo de sincronização.


Há algumas coisas que você precisa levar em consideração ao configurar o token encapsulado:

1. Devido à criptografia envolvida, todas as instâncias precisam ter a mesma chave HMAC. Desde o AEM 6.3, o material principal não é mais armazenado no repositório, mas no sistema de arquivos real. Com isso em mente, a melhor maneira de replicar as chaves é copiá-las do sistema de arquivos da instância de origem para a instância(s) do público alvo para a qual você deseja replicar as chaves. Consulte mais informações em &quot;Replicando a chave HMAC&quot; abaixo.
1. O token encapsulado precisa ser ativado. Isso pode ser feito por meio do Console da Web.

### Replicação da chave HMAC {#replicating-the-hmac-key}

A chave HMAC está presente como uma propriedade binária do `/etc/key` repositório. Você pode baixá-lo separadamente pressionando o link de **visualização** ao lado dele:

![chlimage_1-35](assets/chlimage_1-35a.png)

Para replicar a chave entre instâncias, é necessário:

1. Acesse a instância do AEM, normalmente uma instância do autor, que contém o material principal a ser copiado;
1. Localize o `com.adobe.granite.crypto.file` pacote no sistema de arquivos local. Por exemplo, neste caminho:

   * &lt;author-aem-install-dir>/crx-quickstart/launch/felix/bundle21
   O `bundle.info` arquivo dentro de cada pasta identificará o nome do pacote.

1. Navegue até a pasta de dados. Por exemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie os arquivos HMAC e master.
1. Em seguida, vá para a instância do público alvo para a qual deseja duplicado a chave HMAC e navegue até a pasta de dados. Por exemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Cole os dois arquivos copiados anteriormente.
1. [Atualize o pacote](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) Crypto se a instância do público alvo já estiver em execução.

1. Repita as etapas acima para todas as instâncias às quais deseja replicar a chave.

#### Ativação do token encapsulado {#enabling-the-encapsulated-token}

Depois que a chave HMAC tiver sido replicada, você poderá ativar o token encapsulado por meio do console da Web:

1. Aponte seu navegador para `https://serveraddress:port/system/console/configMgr`
1. Procure uma entrada chamada **Day CRX Token Authentication Handler** e clique nela.
1. Na janela a seguir, marque a caixa **Ativar suporte** a token encapsulado e pressione **Salvar**.

