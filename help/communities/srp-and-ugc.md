---
title: Princípios básicos de SRP e UGC
seo-title: Princípios básicos de SRP e UGC
description: Visão geral do provedor de recursos do Armazenamento e do conteúdo gerado pelo usuário
seo-description: Visão geral do provedor de recursos do Armazenamento e do conteúdo gerado pelo usuário
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# Princípios básicos de SRP e UGC {#srp-and-ugc-essentials}

## Introdução {#introduction}

Se você não estiver familiarizado com o SRP (armazenamento Resource Provider [fornecedor de recursos do ]) e seu relacionamento com o UGC (User-Gered Content Provider [conteúdo gerado pelo usuário]), visite a Visão geral [do Armazenamento](working-with-srp.md) de conteúdo da comunidade e do provedor de recursos do [](srp.md)Armazenamento.

Esta seção da documentação fornece algumas informações essenciais sobre o SRP e o UGC.

## StorageResourceProvider API {#storageresourceprovider-api}

A API SocialResourceProvider (API SRP) é uma extensão de várias APIs do Provedor de recursos Sling. Inclui suporte para paginação e incremento atômico (útil para tally e pontuação).

Os Query são necessários para os componentes do quadro SEPA para os cartões, uma vez que é necessário classificar por data, utilidade, número de votos, etc. Todas as opções de SRP têm mecanismos flexíveis de query que não dependem da definição de baldes.

A localização do armazenamento SRP incorpora o caminho do componente. A API SRP deve ser sempre usada para acessar o UGC, já que o caminho raiz depende da opção SRP selecionada, como ASRP, MSRP ou JSRP.

A API SRP não é uma classe abstrata, é uma interface. Uma implementação personalizada não deve ser realizada com ligeireza, já que os benefícios de futuras melhorias nas implementações internas seriam desperdiçados ao atualizar para uma nova versão.

Os meios para usar a API SRP são utilitários fornecidos, como os encontrados no pacote SocialResourceUtilities.

Durante a atualização do AEM 6.0 ou anterior, será necessário migrar o UGC para todos os SRPs, para os quais uma ferramenta Open Source está disponível. See [Upgrading to AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Historicamente, os utilitários para acessar o UGC foram encontrados no pacote SocialUtils, que não existe mais.
>
>Para obter utilitários de substituição, consulte Refatoração [SocialUtils](socialutils.md).


## Método do utilitário para acessar o UGC {#utility-method-to-access-ugc}

Para acessar o UGC, use um método do pacote SocialResourceUtilities que retorna um caminho adequado para acessar o UGC do SRP e substitui o método obsoleto encontrado no pacote SocialUtils.

Veja a seguir um exemplo mínimo de como usar o método resourceToUGCStoragePath() em um servlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

Para outras substituições do SocialUtils, consulte Refatoração [do SocialUtils](socialutils.md).

Para obter diretrizes de codificação, consulte [Acesso ao UGC com SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>O recurso pathToUGCStoragePath() retorna *não* é adequado para verificação [](srp.md#for-access-control-acls)ACL.


## Método do utilitário para acessar ACLs {#utility-method-to-access-acls}

Algumas implementações SRP, como ASRP e MSRP, armazenam conteúdo da comunidade em bancos de dados que não fornecem verificação de ACL. Os nós de sombra fornecem um local no repositório local ao qual as ACLs podem ser aplicadas.

Usando a API SRP, todas as opções SRP executam a mesma verificação do local da sombra antes de todas as operações CRUD.

Para verificar ACLs, use um método que retorne um caminho adequado para verificar as permissões aplicadas ao UGC do recurso.

Veja a seguir um exemplo simples de como usar o método resourceToACLPath() em um servlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>O caminho retornado por resourceToACLPath() *não* é adequado para [acessar o próprio UGC](#utility-method-to-access-acls) .


## Locais de Armazenamentos relacionados ao UGC {#ugc-related-storage-locations}

As seguintes descrições da localização do armazenamento podem ser úteis ao desenvolver com JSRP ou talvez MSRP. No momento, não há interface para acessar o UGC armazenado no ASRP, como há para JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) e MSRP (ferramentas MongoDB).

**localização do componente**

Quando um membro entra no UGC no ambiente de publicação, ele interage com um componente como parte de um site do AEM.

Um exemplo desse componente é o componente [](http://localhost:4502/content/community-components/en/comments.html) comments que existe no site [Community Components Guide](components-guide.md) . O caminho para o nó de comentário no repositório local é:

* Component path = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**localização do nó sombra**

A criação do UGC também cria um nó [de](srp.md#about-shadow-nodes-in-jcr) sombra ao qual as ACLs necessárias são aplicadas. O caminho para o nó de sombra correspondente no repositório local é o resultado do prefixo do caminho raiz do nó de sombra para o caminho do componente:

* Caminho raiz = `/content/usergenerated`
* Nó sombra de comentários = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Local UGC**

O UGC é criado em nenhum desses locais e só deve ser acessado usando um método [de](#utility-method-to-access-ugc) utilitário que chama a API SRP.

* Caminho raiz = `/content/usergenerated/asi/srp-choice`
* Nó UGC para JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Esteja ciente* de que, para o JSRP, o nó UGC *só* estará presente na instância do AEM (autor ou publicação) na qual foi inserido. Se inserido em uma instância de publicação, a moderação não será possível no console de moderação do autor.

## Informações relacionadas {#related-information}

* [Visão geral](srp.md) do provedor de recursos do Armazenamento - Introdução e visão geral de uso do repositório.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração](socialutils.md) SocialUtils - mapeamento de métodos de utilitários obsoletos para métodos de utilitários SRP atuais.

