---
title: Atualização para o AEM 6.5 Communities
seo-title: Atualização para o AEM 6.5 Communities
description: Como atualizar de uma versão anterior para AEM Comunidades 6.5
seo-description: Como atualizar de uma versão anterior para AEM Comunidades 6.5
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# Atualização para o AEM 6.5 Communities {#upgrading-to-aem-communities}

Dependendo da topologia e dos recursos de cada site, as seguintes ações podem ser necessárias ao atualizar para o AEM Communities 6.5 ou instalar o pacote de recursos mais recente.

Esta seção é específica para Comunidades e complementa as informações fornecidas em [Atualização para AEM 6.5](/help/sites-deploying/upgrade.md) (plataforma).

## Atualização do AEM 6.1 ou posterior {#upgrading-from-aem-or-later}

### Reindexar Solr {#reindex-solr}

Ao instalar um novo pacote de recursos das Comunidades em uma implantação configurada com MSRP, será necessário:

1. Instale o [pacote de recursos mais recente](/help/communities/deploy-communities.md#latestfeaturepack).
1. Instale os [arquivos de configuração Solr mais recentes](/help/communities/msrp.md#upgrading).
1. Reindexar MSRP
consulte a seção [Ferramenta MSRP Reindex](/help/communities/msrp.md#msrp-reindex-tool).

### Ativação 2.0 {#enablement}

A partir do AEM 6.3, os recursos de ativação não armazenarão mais informações de relatórios no MySQL. A dependência MySQL está lá apenas para rastrear conteúdo SCORM.

Entre em contato com o [atendimento ao cliente](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) para obter assistência na migração de conteúdo do Enablement 1.0.

## Atualização do AEM 6.0 {#upgrading-from-aem}

Se o UGC preexistente precisar ser retido, o meio para fazer isso dependerá se a implantação armazenou o UGC [no local](#on-premise-storage) ou na [nuvem de Adobe](#adobe-cloud-storage).

### Armazenamento Adobe Cloud {#adobe-cloud-storage}

Se o site atualizado foi configurado para usar o armazenamento na nuvem do Adobe, ele pode aparecer (incorretamente) como se todo o UGC tivesse sido perdido, pois os métodos do SRP não conseguirão localizar o UGC pré-existente no local antigo.

Portanto, há a capacidade de instruir o ASRP a usar `AEM 6.0 compatability-mode` para acessar o UGC.

Para todas as instâncias de autor e publicação do AEM 6.3:

* Faça logon com privilégios de administrador.
* Configure [ASRP](/help/communities/asrp.md).
* Siga estas etapas para tornar o UGC pré-existente visível :

   * Navegue até o console da Web:

      * Por exemplo, [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Localize a configuração **AEM Communities Utilities**.
      * Selecione para expandir o painel de configuração:

         * *Desmarcar* `Cloud Storage`

         * Selecione **Salvar**

      ![utilitários](assets/utilities.png)


### Armazenamento local {#on-premise-storage}

Se o site atualizado não tiver usado o armazenamento em nuvem, qualquer UGC pré-existente deverá ser convertido para estar em conformidade com a nova estrutura introduzida no AEM 6.1 Communities em suporte da loja comum.

Para essa finalidade, uma ferramenta de migração de código aberto está disponível no GitHub:
[Ferramenta de Migração UGC do AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### APIs Java {#java-apis}

Ao atualizar do AEM 6.0 para AEM Comunidades sociais 6.3, esteja ciente de que muitas APIs foram reorganizadas em pacotes diferentes. A maioria deve ser facilmente resolvida ao usar um IDE para personalização dos recursos das Comunidades.

Para obter detalhes sobre o pacote SocialUtils obsoleto, visite [SocialUtils Refactoring](/help/communities/socialutils.md).

Consulte também [Usando Maven para Comunidades](/help/communities/maven.md).

### Nenhum modelo de componente JSP {#no-jsp-component-templates}

A [estrutura do componente social](/help/communities/scf.md) (SCF) usa a linguagem de modelo [HandlebarsJS](https://handlebarsjs.com/) (HBS) no lugar de Java Server Pages (JSP) usada antes do AEM 6.0.

No AEM 6.0, os componentes do JSP permaneceram junto com os novos componentes da estrutura do HBS no mesmo local, com os componentes do HBS normalmente localizados em subpastas chamadas &quot;hbs&quot;.

A partir AEM 6.1, os componentes do JSP foram completamente removidos. Para Comunidades, é recomendável substituir todo o uso de componentes JSP por componentes SCF.

## Ferramenta de migração UGC da AEM Communities {#aem-communities-ugc-migration-tool}

A [Ferramenta de Migração UGC do AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) é uma ferramenta de migração de código aberto, disponível no GitHub, que pode ser personalizada para exportar o UGC de versões anteriores de comunidades sociais AEM e importar para o AEM Communities 6.1 ou posterior.

Além de mover o UGC de versões anteriores, também é possível usar a ferramenta para mover o UGC de um [SRP](/help/communities/working-with-srp.md) para outro, como do MSRP para o DSRP.

## Atualização do AEM 5.6.1 ou anterior {#upgrading-from-aem-or-earlier}

Conceitualmente, há três gerações de componentes de comunidades :

**1**. Aproximadamente o CQ 5.4 até o AEM 5.6.0, esses são os  **** componentes de colaboração que armazenaram o UGC no repositório local usando a replicação como um meio de sincronizar o UGC entre plataformas. Outras diferenças envolvem a implementação usando o Java Server Pages (JSP), bem como o recurso de blog que consiste na criação apenas no ambiente do autor.

**Classe 2**: De AEM 5.6.1 a AEM 6.1, esta é uma combinação de  **** componentes  **** sociais. O AEM 6.0 introduziu o novo [social component framework](/help/communities/scf.md) (SCF) e o AEM 6.2 introduziu um [loja UGC comum](/help/communities/working-with-srp.md), onde o UGC é acessado usando um [provedor de recursos de armazenamento](/help/communities/srp.md) (SRP).

**Gen 3**: A partir do AEM 6.2, existem apenas componentes  **** sociais, implementados no SCF como componentes do Handlebars (HBS) que exigem uma escolha de SRP para UGC.
