---
title: Atualização para o AEM 6.5 Communities
seo-title: Atualização para o AEM 6.5 Communities
description: Como atualizar de uma versão anterior para AEM 6.5 Communities
seo-description: Como atualizar de uma versão anterior para AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: 612d102b5925704ce459ad818554e487ec0d5355
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---


# Atualização para o AEM 6.5 Communities {#upgrading-to-aem-communities}

Dependendo da topologia e dos recursos de cada site, as seguintes ações podem ser necessárias ao atualizar para o AEM Communities 6.5 ou ao instalar o pacote de recursos mais recente.

Esta seção é específica das Comunidades e complementa as informações fornecidas em [Atualização para AEM 6.5](/help/sites-deploying/upgrade.md) (plataforma).

## Atualização do AEM 6.1 ou posterior {#upgrading-from-aem-or-later}

### Reindexar Solr {#reindex-solr}

Ao instalar um novo pacote de recursos das Comunidades em uma implantação configurada com MSRP, será necessário:

1. Instale o [pacote de recursos mais recente](/help/communities/deploy-communities.md#latestfeaturepack).
1. Instale os [arquivos de configuração mais recentes do Solr](/help/communities/msrp.md#upgrading).
1. Reindexar MSRP
consulte a seção [MSRP Reindex Tool](/help/communities/msrp.md#msrp-reindex-tool).

### Ativação 2.0 {#enablement}

A partir do AEM 6.3, os recursos de ativação não armazenam mais informações do relatórios no MySQL. A dependência MySQL está disponível somente para rastrear conteúdo SCORM.

Entre em contato com o [Atendimento ao cliente](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) para obter ajuda na migração de conteúdo do Enablement 1.0.

## Atualização do AEM 6.0 {#upgrading-from-aem}

Se o UGC pré-existente precisar ser retido, então os meios para fazer isso dependerão se a implantação armazenou o UGC [no local](#on-premise-storage) ou na [nuvem de Adobe](#adobe-cloud-storage).

### Armazenamento da Adobe Cloud {#adobe-cloud-storage}

Se o site atualizado tiver sido configurado para usar o armazenamento na nuvem do Adobe, ele poderá aparecer (incorretamente) como se todo o UGC tivesse sido perdido, pois os métodos SRP não conseguirão localizar o UGC preexistente no local antigo.

Portanto, há a capacidade de instruir o ASRP a usar `AEM 6.0 compatability-mode` para acessar o UGC.

Para todas as instâncias de autor e publicação do AEM 6.3:

* Faça logon com privilégios de administrador.
* Configure [ASRP](/help/communities/asrp.md).
* Siga estas etapas para tornar o UGC pré-existente visível:

   * Navegue até o console da Web:

      * Por exemplo, [https://&lt;host>:&lt;porta>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Localize a configuração **AEM Communities Utilities**.
      * Selecione para expandir o painel de configuração:

         * *Desmarcar* `Cloud Storage`

         * Selecione **Salvar**

      ![utilitários](assets/utilities.png)


### Armazenamento local {#on-premise-storage}

Se o site atualizado não tiver usado armazenamento em nuvem, qualquer UGC pré-existente deve ser convertido em conformidade com a nova estrutura introduzida no AEM 6.1 Communities em suporte à loja comum.

Para esse fim, uma ferramenta de migração de código aberto está disponível no GitHub:
[Ferramenta de Migração AEM Communities UGC](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### APIs Java {#java-apis}

Ao atualizar de AEM 6.0 comunidades sociais para AEM 6.3 comunidades, esteja ciente de que muitas APIs foram reorganizadas em diferentes pacotes. A maioria deve ser facilmente resolvida ao usar um IDE para personalização dos recursos das Comunidades.

Para obter detalhes sobre o pacote SocialUtils obsoleto, visite [Refatoração SocialUtils](/help/communities/socialutils.md).

Consulte também [Usando o Maven para Communities](/help/communities/maven.md).

### Nenhum Modelo de Componente JSP {#no-jsp-component-templates}

A [estrutura de componente social](/help/communities/scf.md) (SCF) usa a linguagem de modelo [HandlebarsJS](https://www.handlebarsjs.com/) (HBS) no lugar de Java Server Pages (JSP) usada antes da AEM 6.0.

No AEM 6.0, os componentes do JSP permaneceram junto aos novos componentes do enquadramento do HBS no mesmo local, com os componentes do HBS normalmente localizados em subpastas denominadas &quot;hbs&quot;.

A partir do AEM 6.1, os componentes do JSP foram completamente removidos. Para Comunidades, é recomendável substituir todo o uso de componentes JSP por componentes SCF.

## Ferramenta de migração UGC AEM Communities {#aem-communities-ugc-migration-tool}

A [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) é uma ferramenta de migração de código aberto, disponível no GitHub, que pode ser personalizada para exportar o UGC de versões anteriores de comunidades sociais AEM e importar para o AEM Communities 6.1 ou posterior.

Além de mover o UGC de versões anteriores, também é possível usar a ferramenta para mover o UGC de um [SRP](/help/communities/working-with-srp.md) para outro, como de MSRP para DSRP.

## Atualização do AEM 5.6.1 ou anterior {#upgrading-from-aem-or-earlier}

Conceitualmente, existem três gerações de componentes de comunidades:

**Geração 1**: Aproximadamente o CQ 5.4 até o AEM 5.6.0, esses são os  **** componentes de colaboração que armazenaram o UGC no repositório local usando a replicação como meio de sincronizar o UGC entre plataformas. Outras diferenças envolvem a implementação usando Java Server Pages (JSP), bem como o recurso de blog que consiste na criação somente no ambiente do autor.

**Geração 2**: De AEM 5.6.1 até AEM 6.1, isto é uma mistura de componentes  **** colativos  **** sociais. AEM 6.0 introduziu a nova [estrutura de componente social](/help/communities/scf.md) (SCF) e AEM 6.2 introduziu uma [loja UGC comum](/help/communities/working-with-srp.md) onde o UGC é acessado usando um [provedor de recursos de armazenamento](/help/communities/srp.md) (SRP).

**Geração 3**: A partir AEM 6.2, há apenas componentes  **** sociais, implementados no SCF como componentes HBS (Handlebars) que exigem uma escolha de SRP para UGC.
