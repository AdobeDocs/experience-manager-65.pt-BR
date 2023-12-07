---
title: Fundamentos de SRP e UGC
description: Visão geral do provedor de recursos de armazenamento e do conteúdo gerado pelo usuário
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Fundamentos de SRP e UGC {#srp-and-ugc-essentials}

## Introdução {#introduction}

Se não estiver familiarizado com o provedor de recursos de armazenamento (SRP) e seu relacionamento com o conteúdo gerado pelo usuário (UGC), visite [Armazenamento de conteúdo da comunidade](working-with-srp.md) e [Visão geral do provedor de recursos de armazenamento](srp.md).

Esta seção da documentação fornece algumas informações essenciais sobre SRP e UGC.

## API StorageResourceProvider {#storageresourceprovider-api}

A API SocialResourceProvider (SRP API) é uma extensão de várias APIs do provedor de recursos Sling. Ele inclui suporte para paginação e incremento atômico (útil para contagem e pontuação).

As consultas são necessárias para os componentes do SCF, pois há a necessidade de classificar por data, utilidade, número de votos e assim por diante. Todas as opções de SRP têm mecanismos de consulta flexíveis que não dependem da segmentação.

O local de armazenamento SRP incorpora o caminho do componente. A API SRP deve sempre ser usada para acessar o UGC, pois o caminho raiz depende da opção SRP selecionada, como ASRP, MSRP ou JSRP.

A API SRP não é uma classe abstrata, é uma interface. Uma implementação personalizada não deve ser realizada com ligeireza, pois os benefícios de melhorias futuras nas implementações internas não serão percebidos ao atualizar para uma nova versão.

Os meios de usar a API SRP são por meio de utilitários fornecidos, como os encontrados no pacote SocialResourceUtilities.

Ao atualizar do AEM 6.0 ou anterior, será necessário migrar o UGC para todos os SRPs, para os quais uma ferramenta de Código aberto está disponível. Consulte [Atualização para o AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Historicamente, os utilitários para acessar UGC foram encontrados no pacote SocialUtils, que não existe mais.
>
>Para obter utilitários de substituição, consulte [Refatoração de SocialUtils](socialutils.md).

## Método do utilitário para acessar o UGC {#utility-method-to-access-ugc}

Para acessar o UGC, use um método do pacote SocialResourceUtilities que retorne um caminho adequado para acessar o UGC do SRP e substitua o método obsoleto encontrado no pacote SocialUtils.

Veja a seguir um exemplo mínimo do uso do método resourceToUGCStoragePath() em um servlet:

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

Para outras substituições de SocialUtils, consulte [Refatoração de SocialUtils](socialutils.md).

Para obter diretrizes de codificação, visite [Acesso ao UGC com SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>O caminho que resourceToUGCStoragePath() retorna é *não* adequado para [Verificação de ACL](srp.md#for-access-control-acls).

## Método do utilitário para acessar ACLs {#utility-method-to-access-acls}

Algumas implementações de SRP, como ASRP e MSRP, armazenam conteúdo da comunidade em bancos de dados que não fornecem verificação de ACL. Os nós de sombra fornecem um local no repositório local ao qual as ACLs podem ser aplicadas.

Usando a API SRP, todas as opções SRP executam a mesma verificação do local de sombra antes de todas as operações CRUD.

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
>O caminho retornado por resourceToACLPath() é *não* adequado para [acesso ao UGC](#utility-method-to-access-acls) próprio.

## Locais de armazenamento relacionados ao UGC {#ugc-related-storage-locations}

As descrições a seguir do local de armazenamento podem ser úteis ao desenvolver com JSRP ou talvez MSRP. No momento, não há interface do usuário para acessar o UGC armazenado no ASRP, pois há para JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) e MSRP (ferramentas MongoDB).

**Localização do componente**

Quando um membro insere o UGC no ambiente de publicação, ele interage com um componente como parte de um site de AEM.

Um exemplo desse componente é o [componente comentários](http://localhost:4502/content/community-components/en/comments.html) que existe no [Guia de componentes da comunidade](components-guide.md) local. O caminho para o nó do comentário no repositório local é:

* Caminho do componente = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Local do nó de sombra**

A criação do UGC também cria uma [nó de sombra](srp.md#about-shadow-nodes-in-jcr) às quais as ACLs necessárias são aplicadas. O caminho para o nó de sombra correspondente no repositório local é o resultado de anexar o caminho raiz do nó de sombra ao caminho do componente:

* Caminho raiz = `/content/usergenerated`
* Nó de sombra do comentário = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Local do UGC**

O UGC é criado em nenhum desses locais e deve ser acessado somente usando um [método de utilitário](#utility-method-to-access-ugc) que chama a API SRP.

* Caminho raiz = `/content/usergenerated/asi/srp-choice`
* Nó UGC para JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Esteja ciente*, para JSRP, o nó UGC *somente* estar presente na instância do AEM (autor ou publicação) em que foi inserida. Se inserido em uma instância de publicação, a moderação não será possível no console de moderação do autor.

## Informações relacionadas {#related-information}

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
