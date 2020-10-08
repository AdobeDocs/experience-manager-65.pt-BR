---
title: Princípios básicos do site da comunidade
seo-title: Princípios básicos do site da comunidade
description: Exportar e excluir sites da comunidade e criar modelos de site personalizados
seo-description: Exportar e excluir sites da comunidade e criar modelos de site personalizados
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---


# Princípios básicos do site da comunidade {#community-site-essentials}

## Modelo de site personalizado {#custom-site-template}

Um modelo de site personalizado pode ser especificado separadamente para cada cópia de idioma de um site da comunidade.

Para isso:

* Crie um modelo personalizado.
* Sobrepor o caminho padrão do modelo do site.
* Adicione o modelo personalizado ao caminho de sobreposição.
* Especifique o modelo personalizado adicionando uma `page-template` propriedade ao `configuration` nó.

**Modelo** padrão:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Modelo personalizado no caminho** de sobreposição:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propriedade**: page-template

**Tipo**: String

**Valor**: `template-name` (sem extensão)

**Nó** de configuração:

`/content/community site path/lang/configuration`

Por exemplo: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Todos os nós no caminho sobreposto precisam apenas ser do tipo `Folder`.

>[!CAUTION]
>
>Se o modelo personalizado receber o nome *sitepage.hbs*, todos os sites da comunidade serão personalizados.

### Exemplo de modelo de site personalizado {#custom-site-template-example}

Por exemplo, `vertical-sitepage.hbs` é um modelo de site que resulta na colocação de links de menu verticalmente para baixo do lado esquerdo da página, em vez de horizontalmente abaixo do banner.

[Obter arquivo](assets/vertical-sitepage.hbs)Coloque o modelo de site personalizado na pasta de sobreposição:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifique o modelo personalizado adicionando uma `page-template` propriedade ao nó de configuração:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Certifique-se de **Salvar tudo** e replicar o código personalizado para todas as instâncias AEM (o código personalizado não é incluído quando o conteúdo do site da comunidade é publicado no console).

A prática recomendada para replicar código personalizado é [criar um pacote](../../help/sites-administering/package-manager.md#creating-a-new-package) e implantá-lo em todas as instâncias.

## Exportar um site da comunidade {#exporting-a-community-site}

Depois que um site da comunidade é criado, é possível exportar o site como um pacote AEM armazenado no gerenciador de pacotes e disponível para download e upload.

Isso está disponível no console [Sites de](sites-console.md#exporting-the-site)comunidades.

Observe que o UGC e o código personalizado não estão incluídos no pacote do site da comunidade.

Para exportar o UGC, use a Ferramenta [de migração UGC da](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)AEM Communities, uma ferramenta de migração de código aberto disponível no GitHub.

## Excluindo um site da comunidade {#deleting-a-community-site}

A partir do AEM Communities 6.3 Service Pack 1, o ícone Excluir site é exibido ao passar o mouse sobre o site da comunidade a partir do console **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]** . Durante o desenvolvimento, se desejar excluir um site da comunidade e atualizar o start, você poderá usar essa funcionalidade. A exclusão de um site da comunidade remove os seguintes itens associados a esse site:

* [UGC](#user-generated-content)
* [Grupos de usuários](#community-user-groups)
* [Assets](#enablement-assets)
* [Registros do banco de dados](#database-records)

### ID exclusiva do site da comunidade {#community-unique-site-id}

Para identificar a ID de site exclusiva associada ao site da comunidade, use o CRXDE:

* Navegue até a raiz do idioma do site, como `/content/sites/*<site name>*/en/rep:policy`.

* Encontre o `allow<#>` nó com um `rep:principalName` neste formato `rep:principalName = *community-enable-nrh9h-members*`.

* A ID do site é o terceiro componente de `rep:principalName`

   Por exemplo, se `rep:principalName = community-enable-nrh9h-members`

   * **nome** do site = *ativar*
   * **ID** do site = *nrh9h*
   * **ID** exclusiva do site = *enable-nrh9h*

### Conteúdo gerado pelo usuário {#user-generated-content}

Obtenha o projeto Communities-srp-tools do Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Ele contém um servlet para excluir todo o UGC de qualquer SRP.

Todo o UGC pode ser removido ou para um site específico, por exemplo:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Isso só remove o conteúdo gerado pelo usuário (inserido na publicação) e não o conteúdo criado (inserido no autor). Portanto, nós [de](srp.md#shadownodes) sombra não são afetados.

### Grupos de usuários da comunidade {#community-user-groups}

Em todas as instâncias de autor e publicação, no console [de](../../help/sites-administering/security.md)segurança, localize e remova os grupos [de](users.md) usuários que são:

* Prefixo com `community`
* Seguido pela ID de site [exclusiva](#community-unique-site-id)

Por exemplo, `community-engage-x0e11-members`.

### Ativar ativos {#enablement-assets}

No console principal:

* Select **[!UICONTROL Assets]**.
* Entre no modo **[!UICONTROL Selecionar]** .
* Selecione a pasta nomeada com a ID [de site](#community-unique-site-id)exclusiva.
* Selecione **[!UICONTROL Excluir]** (pode ser necessário selecionar de **[!UICONTROL Mais...]**).

### Registros do banco de dados {#database-records}

Não há ferramenta para excluir seletivamente entradas de banco de dados para um site da comunidade de ativação específico.

Quando todos os sites da comunidade estiverem sendo excluídos, solte os ativlementdb e scormenginedb usando o MySQL Workbench.
