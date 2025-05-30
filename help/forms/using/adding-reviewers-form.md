---
title: Associar revisores de envio a um formulário
description: Saiba como associar revisores de envio a um formulário no AEM Forms. Os revisores associados revisam um formulário enviado por meio do portal de formulários.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Associar revisores de envio a um formulário {#associating-submission-reviewers-with-a-form}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

Ao criar um formulário, você pode especificar os usuários que revisam os envios do formulário por meio do portal de formulários e fornecem feedback. Sua organização pode coletar feedback e retrabalhar nos formulários enviados.

O AEM Forms permite associar um grupo de revisores a um formulário. Os usuários adicionados a um grupo de revisão de um formulário veem os envios deste formulário e fornecem feedback.

Os grupos de revisores atribuídos a um formulário só podem revisar os envios do formulário especificado.

## Pré-requisitos {#prerequisite}

### Ativação da propriedade de grupos do revisor de envio para formulários adaptáveis usando o editor de esquema de metadados {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Para associar um grupo de revisores a um formulário, edite o esquema de metadados de formulários adaptáveis. Por padrão, não é possível adicionar um grupo de revisores a um formulário enviado.

Para editar o esquema de metadados:

1. No modo de autor, em Experience Manager, clique em **Ferramentas** > **Assets** > **Esquemas de Metadados**.
1. Na página Forms de Esquema, navegue até **Forms** > **Forms AEM Criado no.**

   O URL da página é:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Selecione **Formulário adaptável** e clique em **Editar**.
1. Na página Editar formulário, clique em **Avançado**.
1. Na guia Avançado, arraste e solte o componente **Texto de linha única**, disponível em Criar formulário.
1. Selecione o componente de texto adicionado para ver suas configurações.

   Em Configurações, digite `./jcr:content/metadata/form-submission-reviewer-group` no campo Mapear para a Propriedade.

   O campo do grupo de revisores de envio nas propriedades Avançadas do formulário adaptável é ativado com o nome especificado em Rótulo do campo.

## Associar revisores de envio a um formulário {#associating-submission-reviewers-with-a-form-1}

Para associar revisores de envio a um formulário adaptável, crie um grupo de revisores e adicione usuários a ele. Adicione o grupo de revisores criado no campo revisor de envio de formulário nas propriedades avançadas do formulário.
Os grupos de usuários permitem associar diferentes conjuntos de revisores de envio a diferentes formulários adaptáveis. Esse recurso impede que um usuário não autorizado faça uma revisão do envio.

Antes de executar as etapas a seguir, consulte [Pré-requisito](../../forms/using/adding-reviewers-form.md#prerequisite).

Para criar um grupo e adicionar membros a ele, navegue até **Ferramentas** > **Operações** > **Segurança** > **Grupos**.
Para obter mais informações, consulte [Serviços e Administração de Usuários](/help/sites-administering/security.md).
Adicione o grupo que você cria como membro do grupo de usuários predefinido: **forms-submit-reviewers**. Esse grupo de usuários é fornecido com o AEM Forms e garante que os usuários sejam adicionados como revisores de envio.

Para associar grupos de usuários a um formulário adaptável:

1. No modo de criação, navegue até **Forms** > **Forms e Documentos**.
1. Use a opção **Selecionar &#x200B;** para selecionar um formulário adaptável e clique em **Exibir propriedades**.
1. Na janela Propriedades do formulário, clique em **Editar** e em **AVANÇADO**.
1. Insira o grupo no campo de grupo de revisores de envio e clique em **Concluído**.

   O campo de grupo do revisor de envio aparece com o nome especificado no esquema de metadados editado de formulários adaptáveis.

>[!NOTE]
>
>Replicar usuários e formulários para garantir a disponibilidade dos usuários e formulários na implementação remota do AEM Forms.
>
>Certifique-se de que todos os usuários sejam replicados como membros de revisão dos grupos de usuários na implementação remota.
