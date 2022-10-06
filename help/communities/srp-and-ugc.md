---
title: Princípios básicos de SRP e UGC
seo-title: SRP and UGC Essentials
description: Visão geral do provedor de recursos de armazenamento e do conteúdo gerado pelo usuário
seo-description: Storage resource provider and user-generated content overview
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# Princípios básicos de SRP e UGC {#srp-and-ugc-essentials}

## Introdução {#introduction}

Se não estiver familiarizado com o provedor de recursos de armazenamento (SRP) e seu relacionamento com o conteúdo gerado pelo usuário (UGC), visite [Armazenamento de conteúdo da comunidade](working-with-srp.md) e [Visão geral do provedor de recursos de armazenamento](srp.md).

Esta seção da documentação fornece algumas informações essenciais sobre o SRP e o UGC.

## API StorageResourceProvider {#storageresourceprovider-api}

A API SocialResourceProvider (API SRP) é uma extensão de várias APIs do Provedor de recursos Sling. Inclui suporte para paginação e incremento atômico (útil para contagem e pontuação).

As consultas são necessárias para componentes do SCF, pois há a necessidade de classificar por data, utilidade, número de votos e assim por diante. Todas as opções de SRP têm mecanismos de consulta flexíveis que não dependem do agrupamento.

O local de armazenamento SRP incorpora o caminho do componente. A API SRP deve ser sempre usada para acessar o UGC, pois o caminho raiz depende da opção SRP selecionada, como ASRP, MSRP ou JSRP.

A API SRP não é uma classe abstrata, é uma interface. Uma implementação personalizada não deve ser realizada de ânimo leve, pois os benefícios de futuras melhorias nas implementações internas seriam desperdiçados ao atualizar para uma nova versão.

Os meios de usar a API SRP são por meio de utilitários fornecidos, como aqueles encontrados no pacote SocialResourceUtilities.

Ao atualizar do AEM 6.0 ou anterior, será necessário migrar o UGC para todos os SRPs, para os quais uma ferramenta de fonte aberta está disponível. Consulte [Atualização para o AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Historicamente, os utilitários para acessar o UGC foram encontrados no pacote SocialUtils, que não existe mais.
>
>Para obter utilitários de substituição, consulte [Refatoração do SocialUtils](socialutils.md).

## Método do utilitário para acessar o UGC {#utility-method-to-access-ugc}

Para acessar o UGC, use um método do pacote SocialResourceUtilities que retorna um caminho adequado para acessar o UGC do SRP e substitui o método obsoleto encontrado no pacote SocialUtils .

A seguir, há um exemplo mínimo de uso do método resourceToUGCStoragePath() em um servlet:

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

Para outras substituições do SocialUtils , consulte [Refatoração do SocialUtils](socialutils.md).

Para obter diretrizes de codificação, visite [Acesso ao UGC com SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>O caminho resourceToUGCStoragePath() retorna é *not* adequado para [Verificação de ACL](srp.md#for-access-control-acls).

## Método do utilitário para acessar ACLs {#utility-method-to-access-acls}

Algumas implementações de SRP, como ASRP e MSRP, armazenam o conteúdo da comunidade em bancos de dados que não fornecem verificação de ACL. Os nós de sombra fornecem um local no repositório local ao qual as ACLs podem ser aplicadas.

Usando a API SRP, todas as opções de SRP executam a mesma verificação do local de sombra antes de todas as operações de CRUD.

Para verificar as ACLs, use um método que retorne um caminho adequado para verificar as permissões aplicadas ao UGC do recurso.

A seguir, um exemplo simples de uso do método resourceToACLPath() em um servlet:

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
>O caminho retornado por resourceToACLPath() é *not* adequado para [acesso ao UGC](#utility-method-to-access-acls) próprio.

## Locais de armazenamento relacionados ao UGC {#ugc-related-storage-locations}

As descrições a seguir do local de armazenamento podem ser úteis no desenvolvimento com JSRP ou talvez MSRP. No momento, não há interface do usuário para acessar o UGC armazenado no ASRP, pois há para JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) e MSRP (ferramentas MongoDB).

**Localização do componente**

Quando um membro entra no UGC no ambiente de publicação, ele interage com um componente como parte de um site de AEM.

Um exemplo desse componente é o [componente comentários](http://localhost:4502/content/community-components/en/comments.html) que existe no [Guia de componentes da comunidade](components-guide.md) site. O caminho para o nó de comentário no repositório local é:

* Caminho do componente = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Localização do nó sombra**

A criação do UGC também cria um [nó sombra](srp.md#about-shadow-nodes-in-jcr) às quais as ACLs necessárias são aplicadas. O caminho para o nó de sombra correspondente no repositório local é o resultado do prefixo do caminho raiz do nó de sombra ao caminho do componente:

* Caminho raiz = `/content/usergenerated`
* Nó sombra do comentário = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Localização UGC**

O UGC é criado em nenhum desses locais e deve ser acessado somente usando um [método utilitário](#utility-method-to-access-ugc) que chama a API SRP.

* Caminho raiz = `/content/usergenerated/asi/srp-choice`
* Nó UGC para JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Esteja ciente*, para JSRP, o nó UGC *only* estar presente na instância de AEM (autor ou publicação) em que foi inserida. Se inserido em uma instância de publicação, a moderação não será possível no console de moderação do autor.

## Informações relacionadas {#related-information}

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração do SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para os métodos de utilitário SRP atuais.
