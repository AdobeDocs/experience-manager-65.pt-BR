---
title: Fundamentos do site da comunidade
description: Exportação e exclusão de sites da comunidade e criação de modelos de site personalizados
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# Fundamentos do site da comunidade {#community-site-essentials}

## Modelo de site personalizado {#custom-site-template}

Um modelo de site personalizado pode ser especificado separadamente para cada cópia de idioma de um site da comunidade.

Para fazer isso:

* Crie um modelo personalizado.
* Sobrepor o caminho do modelo de site padrão.
* Adicione o modelo personalizado ao caminho de sobreposição.
* Especifique o modelo personalizado adicionando um `page-template` para a propriedade `configuration` nó.

**Modelo padrão**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Modelo personalizado no caminho de sobreposição**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propriedade**: page-template

**Tipo**: String

**Valor**: `template-name` (sem extensão)

**Nó de configuração**:

`/content/community site path/lang/configuration`

Por exemplo: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Todos os nós no caminho sobreposto precisam ser somente do tipo `Folder`.

>[!CAUTION]
>
>Se o modelo personalizado receber o nome *sitepage.hbs*, todos os sites da comunidade serão personalizados.

### Exemplo de modelo de site personalizado {#custom-site-template-example}

Como exemplo, `vertical-sitepage.hbs` é um modelo de site que resulta no posicionamento de links de menu verticalmente no lado esquerdo da página, em vez de horizontalmente abaixo do banner.

[Obter arquivo](assets/vertical-sitepage.hbs)
Coloque o modelo de site personalizado na pasta de sobreposição:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifique o modelo personalizado adicionando um `page-template` ao nó de configuração:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Certifique-se de **Salvar tudo** e replique o código personalizado em todas as instâncias do Adobe Experience Manager (AEM) (o código personalizado não é incluído quando o conteúdo do site da comunidade é publicado no console).

A prática recomendada para replicar o código personalizado é [criar um pacote](../../help/sites-administering/package-manager.md#creating-a-new-package) e implantá-lo em todas as instâncias.

## Exportação de um site da comunidade {#exporting-a-community-site}

Depois que um site da comunidade é criado, é possível exportá-lo como um pacote AEM armazenado no Gerenciador de pacotes e disponível para download e upload.

Isso está disponível no [Console de sites das comunidades](sites-console.md#exporting-the-site).

O UGC e o código personalizado não estão incluídos no pacote do site da comunidade.

Para exportar UGC, use o [Ferramenta de migração UGC do AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration), uma ferramenta de migração de código aberto disponível no GitHub.

## Exclusão de um site da comunidade {#deleting-a-community-site}

A partir do AEM Communities 6.3 Service Pack 1, o ícone Excluir site é exibido ao passar o mouse sobre o site da comunidade de **[!UICONTROL Communities]** > **[!UICONTROL Sites]** console. Durante o desenvolvimento, se for desejado excluir um site da comunidade e começar do zero, você poderá usar essa funcionalidade. A exclusão de um site da comunidade remove os seguintes itens associados a esse site:

* [UGC](#user-generated-content)
* [Grupos de usuários](#community-user-groups)
* [Registros do banco de dados](#database-records)

### ID exclusiva do site da comunidade {#community-unique-site-id}

Para identificar a ID exclusiva do site associada ao site da comunidade, usando o CRXDE:

* Navegue até a raiz de idioma do site, como `/content/sites/*<site name>*/en/rep:policy`.

* Localize o `allow<#>` nó com um `rep:principalName` neste formato `rep:principalName = *community-enable-nrh9h-members*`.

* A ID do site é o terceiro componente do `rep:principalName`

  Por exemplo, se `rep:principalName = community-enable-nrh9h-members`

   * **nome do site** = *habilitar*
   * **ID do site** = *nrh9h*
   * **identificador exclusivo do site** = *enable-nrh9h*

### Conteúdo gerado pelo usuário {#user-generated-content}

Obtenha o projeto communities-srp-tools no GitHub:

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Ele contém um servlet para excluir todo o UGC de qualquer SRP.

Todos os UGC podem ser removidos ou para um site específico, por exemplo:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Isso remove apenas o conteúdo gerado pelo usuário (inserido na publicação) e não o conteúdo criado (inserido no autor). Por conseguinte, [nós de sombra](srp.md#shadownodes) não são afetadas.

### Grupos de usuários da comunidade {#community-user-groups}

Em todas as instâncias de autor e publicação, no [console de segurança](../../help/sites-administering/security.md), localize e remova a variável [grupos de usuários](users.md) que são:

* Prefixado com `community`
* Seguido por [id exclusiva do site](#community-unique-site-id)

Por exemplo, `community-engage-x0e11-members`.
