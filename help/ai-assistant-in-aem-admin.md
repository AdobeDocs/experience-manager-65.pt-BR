---
title: Configurar o assistente de IA no AEM
description: Saiba como configurar o Assistente de IA usando o Admin Console no Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
source-git-commit: c89b0dc7c544e3b81ea05bf078f33e9ab7f40880
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Configurar o assistente de IA no AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Para usar o Assistente de IA no AEM (Adobe Experience Manager), sua organização deve aceitar no nível da Admin Console. Um administrador de produto cria (ou escolhe) um grupo de usuários e concede a ele a nova permissão &quot;Assistente de IA&quot;. Qualquer pessoa adicionada a esse grupo obtém acesso instantâneo ao Assistente de IA no AEM. Se o objetivo for a disponibilidade em toda a empresa, o administrador simplesmente atribuirá todos os usuários a esse grupo.

Da perspectiva de um funcionário, o processo é simples: identifique o administrador do produto para o Adobe Experience Manager em sua organização e solicite para ser adicionado ao grupo de usuários habilitado para IA. Quando você aparece nesse grupo, o ícone Assistente é exibido automaticamente na próxima vez que você entrar.

Os administradores devem ter em mente a governança normal do Cloud Manager. Mantenha os direitos de administrador do produto no Admin Console para criar perfis, gerenciar grupos de usuários ou editar permissões. Se os usuários também precisarem do recurso **Criar Tíquete de Suporte** interno do Assistente, adicione a função padrão **Administrador de Suporte** (função padrão do Admin Console) aos mesmos indivíduos ou grupos.

O processo de configuração do Assistente de IA no AEM consiste nas seguintes etapas:

1. [Crie um novo perfil de produto no Adobe Admin Console](#create-profile).
1. [Habilitar a permissão Conhecimento de Produto do Assistente de IA](#enable-permission).
1. [Criar um novo grupo de usuários (ou usar um grupo de usuários existente)](#create-user-group).
1. [Adicionar usuários ao grupo de usuários](#add-users).
1. [Atribuir o perfil de produto ao grupo de usuários](#assign-product-profile).

**Pré-requisitos**

Antes de começar, verifique se os seguintes pré-requisitos foram atendidos:

* Você deve ter no mínimo direitos de administrador de produto no Adobe Admin Console.
* Você entende a estrutura de gerenciamento de usuários de sua organização.

**Considerações de configuração**

* Tempo de processamento: os recursos criados no Cloud Manager podem levar até 2 minutos para serem exibidos na Admin Console para configuração de permissão.
* Vários perfis: os usuários podem fazer parte de vários perfis e as permissões são combinadas de todos os perfis atribuídos.
* Escopo da organização: algumas permissões podem ser aplicadas no nível da organização em todos os programas.
* Perfis predefinidos: não exclua perfis de permissão predefinidos da Admin Console.


## 1 - Criar um novo perfil de produto no Adobe Admin Console{#create-profile}

1. Siga as instruções detalhadas em [Criar um novo perfil de produto no Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile), encontradas na documentação do Experience Platform.

1. Ao criar o novo perfil de produto, você pode usar os seguintes valores sugeridos para o Assistente de IA.

   | Campo de texto | Valor sugerido |
   | --- | --- |
   | Nome do perfil do produto | `AI Assistant in AEM` (ou seu nome descritivo preferido) |
   | Nome de exibição (opcional) | `AI Assistant` |
   | Descrição (opcional) | `Product profile for managing AI Assistant in AEM access` |
   | Notificação | Configure com base nas preferências de sua organização |


## 2 - Ativar a permissão de conhecimento do produto AI Assistant{#enable-permission}

O processo para atribuir permissões personalizadas a perfis de produtos segue o fluxo de trabalho padrão de permissões personalizadas do Adobe Cloud Manager.

Artigo de referência: [Atribuir permissões personalizadas ao novo perfil de produto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Na Admin Console, clique no nome do perfil de produto recém-criado (`AI Assistant in AEM`)

   ![Captura de tela](/help/assets/assets-ai/ai-assistant-console.png)

1. Para exibir a lista de permissões editáveis, clique na guia **Permissões**.

1. Na lista de tabelas, localize a permissão `AI Assistant Product Knowledge`.

   ![Guia Permissões do Assistente de IA no Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. À direita do nome da permissão, clique em ![Ícone de lápis ou ícone Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Na página **Editar Permissões do Assistente de IA**, ative a opção **Conhecimento de Produto do Assistente de IA**.

   ![Página Editar Permissões para a opção de alternância Conhecimento de Produto do Assistente de IA](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. No canto inferior direito da página, clique em **Salvar**.

   O perfil de produto agora tem a permissão Assistente de IA Conhecimento do produto ativada.


## 3 - Criar um novo grupo de usuários (ou usar um grupo de usuários existente){#create-user-group}

1. Siga uma das seguintes opções:

>[!BEGINTABS]

>[!TAB Criar um novo grupo de usuários]

1. Na Admin Console, clique em **Usuários** > **Grupos de usuários**.

   ![Grupos de usuários](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. Na página **Grupos de usuários**, clique em **Novo grupo de usuários**.

   ![Botão Novo grupo de usuários na página Grupos de usuários](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. Na página **Criar um novo grupo de usuários**, forneça as seguintes informações:

   | Opção | Valor sugerido |
   | --- | --- |
   | Nome do grupo de usuários | `AI Assistant in AEM` (ou seu nome preferido) |
   | Descrição (opcional) | `User group for managing AI Assistant in AEM access` |

   ![Criar uma nova página de grupo de usuários](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. No canto inferior direito da página, clique em **Salvar**.

>[!TAB Usar um grupo de usuários existente]

Você pode usar um grupo de usuários existente do AEM se ele atender aos requisitos de acesso do Assistente de IA, em vez de criar um novo grupo.

>[!ENDTABS]

## 4 - Adicionar usuários ao grupo de usuários{#add-users}

1. Siga uma das seguintes opções:

>[!BEGINTABS]

>[!TAB Adicionar usuários individuais]

1. Na página **Grupos de usuários**, na tabela **Nome do grupo**, clique no nome do grupo de usuários recém-criado ou em um nome de grupo de usuários existente.

   ![Página de grupos de usuários mostrando o Assistente de IA no nome do grupo de usuários do AEM na tabela](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. Na página **Grupos de usuários** do **Assistente de IA do AEM**, clique na guia **Usuários** e em **Adicionar usuários**.

   ![A página Assistente de IA em grupos de usuários do AEM, mostrando a guia Usuários e o botão Adicionar usuários](/help/assets/assets-ai/ai-assistant-add-users.png)

1. Na página **`Add users to this user group`**, procure e selecione os usuários que precisam de acesso ao Assistente de IA no AEM.

   ![Adicionar usuários a esta página de grupo de usuários](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. No canto inferior direito da página, clique em **Salvar**.
1. Agora, [atribua o perfil de produto ao grupo de usuários](#assign-product-profile).

>[!TAB Adicionar usuários em massa]

Você pode usar o recurso de upload em massa na Admin Console.

1. Prepare um arquivo CSV com informações do usuário.
1. Use a opção **`Add users by CSV`** para uma adição em massa eficiente.
1. Agora, [atribua o perfil de produto ao grupo de usuários](#assign-product-profile).

>[!ENDTABS]


## 5 - Atribuir o perfil de produto ao grupo de usuários{#assign-product-profile}

Esta etapa segue o fluxo de trabalho padrão do Adobe Admin Console para atribuição de perfis de produto a grupos de usuários.

Artigo de referência: [Gerenciar perfis de produto para usuários corporativos](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html)

1. Ainda no seu Assistente de IA no grupo de usuários do AEM de [4 - Adicionar usuários ao grupo de usuários](#add-users), clique na guia **Perfis de produto atribuídos**.
1. Clique em **Atribuir perfil**.

   ![Assistente de IA na página do grupo de usuários do AEM com a guia Perfis de produto atribuídos selecionada](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. Na página **Atribuir produtos e perfis**, na caixa de diálogo **Selecionar perfis de produtos**, pesquise e selecione seu perfil de produto **Assistente de IA**.

   ![A página &quot;Atribuir produtos e perfis&quot;, mostrando a caixa de diálogo &quot;Selecionar perfis de produtos&quot; e o perfil de produto &quot;Assistente de IA&quot; selecionado](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. Próximo ao canto inferior direito da caixa de diálogo, clique em **Aplicar**.
1. Próximo ao canto inferior direito da página **Atribuir produtos e perfis**, clique em **Salvar**.

   ![O perfil de produto do Assistente de IA mostrado foi atribuído ao Assistente de IA no grupo de usuários do AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Verificar a configuração

* Verifique se o perfil de produto mostra o número correto de grupos de usuários atribuídos.
* Verifique se o grupo de usuários mostra o número correto de usuários.
* Confirme se a permissão Conhecimento do produto do assistente do AI está ativada e configurada corretamente.


## Testar a configuração

Faça com que um usuário do grupo atribuído faça o seguinte:

1. Faça logon no AEM.
2. Verifique se os recursos do Assistente de IA estão acessíveis.
3. Teste a funcionalidade do Assistente de IA para garantir a ativação correta.

## Consulte também:

* [Assistente de IA no AEM](/help/ai-assistant-in-aem.md)
* [Controle de acesso do Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
