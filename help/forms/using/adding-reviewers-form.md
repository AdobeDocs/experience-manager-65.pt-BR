---
title: Associar revisores de envio a um formulário
seo-title: Associar revisores de envio a um formulário
description: Saiba como associar revisores de envio a um formulário em AEM Forms. Os revisores associados analisam um formulário enviado por meio do portal de formulários.
seo-description: Saiba como associar revisores de envio a um formulário em AEM Forms. Os revisores associados analisam um formulário enviado por meio do portal de formulários.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Associar revisores de envio a um formulário {#associating-submission-reviewers-with-a-form}

Ao criar um formulário, você pode especificar usuários que revisam os envios do formulário por meio do portal de formulários e fornecem feedback. Sua organização pode coletar feedback e retrabalhar os formulários enviados.

AEM Forms permite associar um grupo de revisores a um formulário. Os usuários adicionados a um grupo de revisão de um formulário visualizam os envios desse formulário e fornecem feedback.

Os grupos do revisor atribuídos a um formulário só podem revisar os envios do formulário especificado.

## Pré-requisitos {#prerequisite}

### Habilitar a propriedade de grupos do revisor de envio para formulários adaptáveis usando o editor de schemas de metadados {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Para associar um grupo de revisores a um formulário, edite o schema de metadados de formulários adaptáveis. Por padrão, não é possível adicionar um grupo de revisores a um formulário enviado.

Para editar o schema de metadados:

1. No modo de autor, em Experience Manager, clique em **Ferramentas** > **Ativos** > Schemas **de** metadados.
1. Na página Formulários de Schema, navegue até **Formulários** > **Formulários criados no AEM.**

   O URL da página é:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Selecione Formulário **** adaptável e clique em **Editar**.
1. Na página Editar formulário, clique em **Avançado**.
1. Na guia Avançado, arraste e solte o componente Texto **de linha** única disponível em Formulário de compilação.
1. Selecione o componente de texto adicionado para ver suas configurações.

   Em Configurações, digite `./jcr:content/metadata/form-submission-reviewer-group` no campo Mapa para propriedade.

   O campo de grupo do revisor de envio nas propriedades Avançadas do formulário adaptável é ativado com o nome especificado em Rótulo do campo.

## Associar revisores de envio a um formulário {#associating-submission-reviewers-with-a-form-1}

Para associar revisores de envio a um formulário adaptável, crie um grupo de revisores e adicione usuários a ele. Adicione o grupo do revisor criado no campo do revisor de envio de formulário nas propriedades avançadas do formulário.
Os grupos de usuários permitem associar diferentes conjuntos de revisores de envio a diferentes formulários adaptáveis. Este recurso impede uma revisão de envio de um usuário não autorizado.

Antes de executar as etapas a seguir, consulte [Pré-requisito](../../forms/using/adding-reviewers-form.md#prerequisite).

Para criar um grupo e adicionar membros a ele, navegue até **Ferramentas** > **Operações** > **Segurança** > **Grupos**.
Para obter mais informações, consulte Administração [do usuário e Serviços](/help/sites-administering/security.md).
Certifique-se de adicionar o grupo criado como membro do grupo de usuários predefinido: **revisores** de envio de formulários. Esse grupo de usuários é enviado com AEM Forms e garante que os usuários sejam adicionados como revisores de envio.

Para associar grupos de usuários a um formulário adaptável:

1. No modo de criação, navegue até **Formulários** > **Formulários e Documentos**.
1. Use a **opção **Select **para selecionar um formulário adaptável e clique em Propriedades **da** Visualização.
1. Na janela Propriedades do formulário, clique em **Editar** e em **AVANÇADO**.
1. Insira o grupo no campo do grupo do revisor de submissão e clique em **Concluído**.

   O campo de grupo do revisor de envio é exibido com o nome especificado no schema de metadados editados dos formulários adaptáveis.

>[!NOTE]
>
>Replicar usuários e formulários para garantir a disponibilidade dos usuários e formulários na implementação remota de AEM Forms.
>
>Certifique-se de que todos os usuários sejam replicados como membros de revisão dos grupos de usuários na implementação remota.

