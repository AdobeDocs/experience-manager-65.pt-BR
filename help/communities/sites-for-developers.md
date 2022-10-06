---
title: Fundamentos do site da comunidade
seo-title: Community Site Essentials
description: Como exportar e excluir sites da comunidade e criar modelos de site personalizados
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# Fundamentos do site da comunidade {#community-site-essentials}

## Modelo de site personalizado {#custom-site-template}

Um modelo de site personalizado pode ser especificado separadamente para cada cópia de idioma de um site da comunidade.

Para fazer isso:

* Crie um modelo personalizado.
* Sobreponha o caminho padrão do modelo do site.
* Adicione o modelo personalizado ao caminho de sobreposição.
* Especifique o modelo personalizado adicionando um `page-template` para a `configuration` nó .

**Modelo padrão**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Modelo personalizado no caminho de sobreposição**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propriedade**: modelo de página

**Tipo**: String

**Valor**: `template-name` (sem extensão)

**Nó de configuração**:

`/content/community site path/lang/configuration`

Por exemplo: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Todos os nós no caminho sobreposto só precisam ser do tipo `Folder`.

>[!CAUTION]
>
>Se o modelo personalizado receber o nome *sitepage.hbs*, todos os sites da comunidade serão personalizados.

### Exemplo de modelo de site personalizado {#custom-site-template-example}

Como exemplo, `vertical-sitepage.hbs` é um modelo de site que resulta no posicionamento dos links de menu verticalmente no lado esquerdo da página, em vez de horizontalmente abaixo do banner.

[Obter arquivo](assets/vertical-sitepage.hbs)
Coloque o modelo de site personalizado na pasta de sobreposição:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifique o modelo personalizado adicionando um `page-template` para o nó de configuração:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Certifique-se de **Salvar tudo** e replicar o código personalizado para todas as instâncias AEM (o código personalizado não é incluído quando o conteúdo do site da comunidade é publicado do console).

A prática recomendada para replicar código personalizado é [criar um pacote](../../help/sites-administering/package-manager.md#creating-a-new-package) e implante-o em todas as instâncias.

## Exportar um site de comunidade {#exporting-a-community-site}

Depois que um site da comunidade é criado, é possível exportar o site como um pacote de AEM armazenado no gerenciador de pacotes e disponível para download e upload.

Isso está disponível no [Console de sites das comunidades](sites-console.md#exporting-the-site).

Observe que o UGC e o código personalizado não estão incluídos no pacote de site da comunidade.

Para exportar o UGC, use o [Ferramenta de migração UGC da AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration), uma ferramenta de migração de código aberto disponível no GitHub.

## Excluindo um site da comunidade {#deleting-a-community-site}

A partir do AEM Communities 6.3 Service Pack 1, o ícone Excluir site é exibido ao passar o mouse sobre o site da comunidade a partir do **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]** console. Durante o desenvolvimento, se desejar excluir um site da comunidade e começar a usar o novo, você pode usar essa funcionalidade. Excluir um site da comunidade remove os seguintes itens associados a ele:

* [UGC](#user-generated-content)
* [Grupos de usuários](#community-user-groups)
* [Assets](#enablement-assets)
* [Registros do banco de dados](#database-records)

### ID exclusiva do site da comunidade {#community-unique-site-id}

Para identificar a ID de site exclusiva associada ao site da comunidade, usando o CRXDE:

* Navegue até a raiz de idioma do site, como `/content/sites/*<site name>*/en/rep:policy`.

* Encontre a `allow<#>` nó com um `rep:principalName` neste formato `rep:principalName = *community-enable-nrh9h-members*`.

* A ID do site é o terceiro componente do `rep:principalName`

   Por exemplo, se `rep:principalName = community-enable-nrh9h-members`

   * **nome do site** = *habilitar*
   * **ID do site** = *nrh9h*
   * **ID de site exclusiva** = *enable-nrh9h*

### Conteúdo gerado pelo usuário {#user-generated-content}

Obtenha o projeto communities-srp-tools do Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Ele contém um servlet para excluir todo o UGC de qualquer SRP.

Todo o UGC pode ser removido ou para um site específico, por exemplo:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Isso remove somente o conteúdo gerado pelo usuário (inserido na publicação) e não o conteúdo criado (inserido no autor). Por conseguinte, [nós sombra](srp.md#shadownodes) não são afetadas.

### Grupos de usuários da comunidade {#community-user-groups}

Em todas as instâncias de autor e publicação, no [console de segurança](../../help/sites-administering/security.md), localize e remova o [grupos de usuários](users.md) que são:

* Prefixado com `community`
* Seguido de [id de site exclusiva](#community-unique-site-id)

Por exemplo, `community-engage-x0e11-members`.

### Ativar ativos {#enablement-assets}

No console principal:

* Selecionar **[!UICONTROL Ativos]**.
* Enter **[!UICONTROL Selecionar]** modo.
* Selecione a pasta nomeada com o [identificador exclusivo do site](#community-unique-site-id).
* Selecionar **[!UICONTROL Excluir]** (pode ser necessário selecionar de **[!UICONTROL Mais...]**).

### Registros do banco de dados {#database-records}

Não há ferramenta para excluir seletivamente entradas de banco de dados de um site específico da comunidade de ativação.

Quando todos os sites da comunidade estiverem sendo excluídos, solte o enablementdb e o scormenginedb usando o MySQL Workbench.
