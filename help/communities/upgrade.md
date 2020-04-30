---
title: Atualização para o AEM 6.5 Communities
seo-title: Atualização para o AEM 6.5 Communities
description: Como atualizar de uma versão anterior para o AEM 6.4 Communities
seo-description: Como atualizar de uma versão anterior para o AEM 6.4 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# Atualização para o AEM 6.5 Communities {#upgrading-to-aem-communities}

Dependendo da topologia e dos recursos de cada site, as seguintes ações podem ser necessárias ao atualizar para o AEM Communities 6.5 ou ao instalar o pacote de recursos mais recente.

Esta seção é específica do Communities e complementa as informações fornecidas na [atualização para o AEM 6.5](/help/sites-deploying/upgrade.md) (plataforma).

## Atualização do AEM 6.1 ou posterior {#upgrading-from-aem-or-later}

### Reindexar Solr {#reindex-solr}

Ao instalar um novo pacote de recursos das Comunidades em uma implantação configurada com MSRP, será necessário:

1. Instale o pacote de recursos [mais recente](/help/communities/deploy-communities.md#latestfeaturepack).
1. Instale os arquivos [de configuração Solr](/help/communities/msrp.md#upgrading)mais recentes.
1. Reindexe o MSRPconsulte a seção Ferramenta [de reindexação do](/help/communities/msrp.md#msrp-reindex-tool)MSRP.

### Enablement 2.0 {#enablement}

A partir do AEM 6.3, os recursos de ativação não armazenam mais informações do relatórios no MySQL. A dependência MySQL está disponível somente para rastrear conteúdo SCORM.

Entre em contato com o atendimento [ao](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) cliente para obter assistência na migração de conteúdo do Enablement 1.0.

## Atualização do AEM 6.0 {#upgrading-from-aem}

Se o UGC pré-existente precisar ser retido, então os meios para fazer isso dependerão se a implantação armazenou o UGC [no local](#on-premise-storage) ou na nuvem [da](#adobe-cloud-storage)Adobe.

### Armazenamento da Adobe Cloud {#adobe-cloud-storage}

Se o site atualizado tiver sido configurado para usar o armazenamento em nuvem da Adobe, ele poderá aparecer (incorretamente) como se todo o UGC tivesse sido perdido, já que os métodos SRP não conseguirão localizar o UGC preexistente no local antigo.

Portanto, há a capacidade de instruir o ASRP a usar `AEM 6.0 compatability-mode` para acessar o UGC.

Para todas as instâncias de autor e publicação do AEM 6.3:

* Faça logon com privilégios de administrador.
* Configure o [ASRP](/help/communities/asrp.md).
* Siga estas etapas para tornar o UGC pré-existente visível:

   * Navegue até o console da Web:

      * Por exemplo, [https://&lt;host>:&lt;porta>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Localize a configuração dos utilitários **do** AEM Communities.
      * Selecione para expandir o painel de configuração:

         * *Desmarcar*`Cloud Storage`

         * Selecione **Salvar**
      ![chlimage_1-176](assets/chlimage_1-176.png)


### Armazenamento local {#on-premise-storage}

Se o site atualizado não tiver usado o armazenamento em nuvem, qualquer UGC pré-existente deve ser convertido para estar em conformidade com a nova estrutura introduzida no AEM 6.1 Communities para suportar o armazenamento comum.

Para esse fim, uma ferramenta de migração de código aberto está disponível no GitHub:
Ferramenta de migração UGC do[AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### APIs Java {#java-apis}

Ao atualizar das comunidades sociais do AEM 6.0 para o AEM 6.3 Communities, lembre-se de que muitas APIs foram reorganizadas em pacotes diferentes. A maioria deve ser facilmente resolvida ao usar um IDE para personalização dos recursos das Comunidades.

Para obter detalhes sobre o pacote SocialUtils obsoleto, visite [SocialUtils Refactoring](/help/communities/socialutils.md).

Consulte também [Uso do Maven para comunidades](/help/communities/maven.md).

### Nenhum modelo de componente JSP {#no-jsp-component-templates}

A estrutura [do componente](/help/communities/scf.md) social (SCF) usa a linguagem de modelo [HandlebarsJS](https://www.handlebarsjs.com/) (HBS) no lugar de Java Server Pages (JSP) usada antes do AEM 6.0.

No AEM 6.0, os componentes do JSP permaneceram junto aos novos componentes da estrutura HBS no mesmo local, com os componentes HBS normalmente localizados em subpastas chamadas &quot;hbs&quot;.

A partir do AEM 6.1, os componentes do JSP foram completamente removidos. Para Comunidades, é recomendável substituir todo o uso de componentes JSP por componentes SCF.

## Ferramenta de migração UGC do AEM Communities {#aem-communities-ugc-migration-tool}

A Ferramenta [de migração UGC do](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) AEM Communities é uma ferramenta de migração de código aberto, disponível no GitHub, que pode ser personalizada para exportar o UGC de versões anteriores de comunidades sociais do AEM e importar para o AEM Communities 6.1 ou posterior.

Além de mover o UGC de versões anteriores, também é possível usar a ferramenta para mover o UGC de um [SRP](/help/communities/working-with-srp.md) para outro, como do MSRP para o DSRP.

## Atualização do AEM 5.6.1 ou anterior {#upgrading-from-aem-or-earlier}

Conceitualmente, existem três gerações de componentes de comunidades:

**Geração 1**: Aproximadamente o CQ 5.4 até o AEM 5.6.0, esses são os componentes **collab** que armazenaram o UGC no repositório local usando replicação como meio de sincronizar o UGC entre plataformas. Outras diferenças envolvem a implementação usando Java Server Pages (JSP), bem como o recurso de blog que consiste na criação somente no ambiente do autor.

**Geração 2**: Do AEM 5.6.1 ao AEM 6.1, isso é uma combinação de componentes **collab** e **sociais** . O AEM 6.0 apresentou a nova estrutura [de componentes](/help/communities/scf.md) sociais (SCF) e o AEM 6.2 introduziu uma loja [UGC](/help/communities/working-with-srp.md) comum onde o UGC é acessado usando um provedor [de recursos de](/help/communities/srp.md) armazenamento (SRP).

**Geração 3**: A partir do AEM 6.2, existem apenas componentes **sociais** , implementados no SCF como componentes HBS (Handlebars) que exigem uma escolha de SRP para UGC.
