---
title: Configurar o Assistente de IA no AEM
description: Saiba como configurar o Assistente de IA com o Admin Console no Adobe Experience Manager.
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
autotag-review: '2026-05-18T18:35:37.980Z'
TQID: 'https://experienceleague.adobe.com/5YTQUJbJPlJuxToS6AVhJww1KQ20tuOlRoCVquyfSng'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1202
ht-degree: 98%

---

# Configurar o Assistente de IA no AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Para usar o Assistente de IA no AEM (Adobe Experience Manager), a permissão para acessar o conhecimento do produto por meio do Assistente de IA é obrigatória. Essa permissão está ativada por padrão.

Para controlar quem pode acessar o conhecimento do produto, envie um email para [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) a partir do endereço de email associado à sua Adobe ID. A Adobe pode habilitar o controle de acesso no nível do usuário. Quando estiver habilitado, o admin poderá conceder acesso no nível de usuário seguindo as etapas descritas abaixo.

Caso tenha solicitado controle de acesso no nível do usuário, sua organização deverá aderir por meio do Adobe Admin Console. Um administrador de produto cria (ou escolhe) um grupo de usuários e concede a ele a nova permissão “Assistente de IA”. Qualquer pessoa adicionada a esse grupo obtém acesso instantâneo ao Assistente de IA no AEM. Se o objetivo for a disponibilidade em toda a empresa, o admin simplesmente atribuirá todos os usuários a esse grupo.

Da perspectiva de um(a) funcionário(a), o processo é simples: identifique o admin de produto do Adobe Experience Manager na organização e solicite a inclusão no grupo de usuários habilitado para IA. Quando aparecer nesse grupo, o ícone do Assistente será exibido automaticamente na próxima vez que fizer logon.

Os admins devem ter em mente a governança normal do Cloud Manager. Tenha direitos de admin de produto no Admin Console para criar perfis, gerenciar grupos de usuários ou editar permissões. Se os usuários também precisam do recurso integrado **Criar tíquete de suporte** do Assistente, adicione a função padrão **Admin de suporte** (função padrão do Admin Console) aos mesmos indivíduos ou grupos.

O processo de configuração do Assistente de IA no AEM consiste nas seguintes etapas:

1. [Criar um novo perfil de produto no Adobe Admin Console](#create-profile).
1. [Habilitar permissão de conhecimento sobre produtos do Assistente de IA](#enable-permission).
1. [Criar um novo grupo de usuários (ou usar um grupo de usuários existente)](#create-user-group).
1. [Adicionar usuários ao grupo de usuários](#add-users).
1. [Atribuir o perfil de produto ao grupo de usuários](#assign-product-profile).

**Pré-requisitos**

Antes de começar, verifique se os seguintes pré-requisitos foram atendidos:

* Você deve ter, no mínimo, direitos de admin de produto no Adobe Admin Console.
* Você entende a estrutura de gerenciamento de usuários da organização.

**Considerações de configuração**

* Tempo de processamento: recursos criados no Cloud Manager podem levar até dois minutos para serem exibidos no Admin Console ao configurar permissões.
* Vários perfis: os usuários podem fazer parte de vários perfis e as permissões são combinadas a partir de todos os perfis atribuídos.
* Escopo da organização: algumas permissões podem ser aplicadas no nível da organização em todos os programas.
* Perfis predefinidos: não exclua perfis de permissão predefinidos do Admin Console.


## 1 - Criar um novo perfil de produto no Adobe Admin Console{#create-profile}

1. Siga as instruções detalhadas em [Criar um novo perfil de produto no Adobe Admin Console](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/ui/create-profile), encontradas na documentação da Experience Platform.

1. Ao criar o novo perfil de produto, é possível usar os seguintes valores sugeridos para o Assistente de IA.

   | Campo de texto | Valor sugerido |
   | --- | --- |
   | Nome do perfil do produto | `AI Assistant in AEM` (ou o nome descritivo que preferir) |
   | Nome de exibição (opcional) | `AI Assistant` |
   | Descrição (opcional) | `Product profile for managing AI Assistant in AEM access` |
   | Notificação | Configure com base nas preferências da organização |


## 2 - Habilitar a permissão de conhecimento sobre produtos do Assistente de IA{#enable-permission}

O processo para atribuir permissões personalizadas a perfis de produtos segue o fluxo de trabalho padrão de permissões personalizadas do Adobe Cloud Manager.

Artigo de referência: [Atribuir permissões personalizadas ao novo perfil de produto](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. No Admin Console, clique no nome do perfil de produto recém-criado (`AI Assistant in AEM`)

   ![Captura de tela](/help/assets/assets-ai/ai-assistant-console.png)

1. Para exibir a lista de permissões editáveis, clique na guia **Permissões**.

1. Na lista de tabelas, localize a permissão `AI Assistant Product Knowledge`.

   ![Guia Permissões do Assistente de IA no Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. À direita do nome da permissão, clique no ![ícone de lápis ou no ícone editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Na página **Editar permissões do Assistente de IA**, ative o botão de alternância **Conhecimento sobre produtos do Assistente de IA**.

   ![Página Editar permissões para a opção de alternância Conhecimento sobre produtos do Assistente de IA](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. No canto inferior direito da página, clique em **Salvar**.

   Seu perfil de produto agora tem a permissão Conhecimento sobre produtos do Assistente de IA habilitada.


## 3 - Criar um novo grupo de usuários (ou usar um grupo de usuários existente){#create-user-group}

1. Siga uma das seguintes opções:

>[!BEGINTABS]

>[!TAB Criar um novo grupo de usuários]

1. No Admin Console, clique em **Usuários** > **Grupos de usuários**.

   ![Grupos de usuários](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. Na página **Grupos de usuários**, clique em **Novo grupo de usuários**.

   ![Botão Novo grupo de usuários na página Grupos de usuários](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. Na página **Criar um novo grupo de usuários**, forneça as seguintes informações:

   | Opção | Valor sugerido |
   | --- | --- |
   | Nome do grupo de usuários | `AI Assistant in AEM` (ou o nome que preferir) |
   | Descrição (opcional) | `User group for managing AI Assistant in AEM access` |

   ![Criar uma nova página grupo de usuários](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. No canto inferior direito da página, clique em **Salvar**.

>[!TAB Usar um grupo de usuários existente]

É possível usar um grupo de usuários existente do AEM se ele atender aos requisitos de acesso do Assistente de IA, em vez de criar um novo grupo.

>[!ENDTABS]

## 4 - Adicionar usuários ao grupo de usuários{#add-users}

1. Siga uma das seguintes opções:

>[!BEGINTABS]

>[!TAB Adicionar usuários individuais]

1. Na página **Grupos de usuários**, na tabela **Nome do grupo**, clique no nome do grupo de usuários recém-criado ou em um nome de grupo de usuários existente.

   ![Página grupos de usuários mostrando o nome do grupo de usuários do Assistente de IA no AEM na tabela](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. Na página **Grupos de usuários** do **Assistente de IA no AEM**, clique na guia **Usuários** e em **Adicionar usuários**.

   ![Assistente de IA na página de grupos de usuários do AEM, mostrando a guia Usuários e o botão Adicionar usuários](/help/assets/assets-ai/ai-assistant-add-users.png)

1. Na página **`Add users to this user group`**, pesquise e selecione os usuários que precisam de acesso ao Assistente de IA no AEM.

   ![Adicionar usuários a esta página de grupo de usuários](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. No canto inferior direito da página, clique em **Salvar**.
1. Agora, [atribua o perfil de produto ao grupo de usuários](#assign-product-profile).

>[!TAB Adicionar usuários em massa]

É possível usar o recurso de upload em massa no Admin Console.

1. Prepare um arquivo CSV com informações do usuário.
1. Use a opção **`Add users by CSV`** para uma adição em massa eficiente.
1. Agora, [atribua o perfil de produto ao grupo de usuários](#assign-product-profile).

>[!ENDTABS]


## 5 - Atribuir o perfil de produto ao grupo de usuários{#assign-product-profile}

Esta etapa segue o fluxo de trabalho padrão do Adobe Admin Console para atribuição de perfis de produtos a grupos de usuários.

Artigo de referência: [Gerenciar perfis de produtos para usuários empresariais](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html)

1. Ainda no grupo de usuários do Assistente de IA no AEM da etapa [4 - Adicionar usuários ao grupo de usuários](#add-users), clique na guia **Perfis de produtos atribuídos**.
1. Clique em **Atribuir perfil**.

   ![Página grupo de usuários do Assistente de IA no AEM com a guia perfis de produtos atribuídos selecionada](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. Na página **Atribuir produtos e perfis**, na caixa de diálogo **Selecionar perfis de produtos**, pesquise e selecione o perfil de produto do **Assistente de IA**.

   ![A página &quot;Atribuir produtos e perfis&quot; mostrando a caixa de diálogo &quot;Selecionar perfis de produtos&quot; e o perfil de produto &quot;Assistente de IA&quot; selecionado](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. No canto inferior direito da caixa de diálogo, clique em **Aplicar**.
1. Próximo ao canto inferior direito da página **Atribuir produtos e perfis**, clique em **Salvar**.

   ![Exibição do perfil de produto do Assistente de IA atribuído ao grupo de usuários do Assistente de IA no AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Verificar a configuração

* Verifique se o perfil de produto mostra o número correto de grupos de usuários atribuídos.
* Verifique se o grupo de usuários mostra o número correto de usuários.
* Confirme se a permissão de Conhecimento sobre produtos do Assistente de IA está habilitada e configurada corretamente.


## Teste a configuração

Indique a um usuário do grupo atribuído que faça o seguinte:

1. Faça logon no AEM.
2. Verificar se os recursos do Assistente de IA estão acessíveis.
3. Testar a funcionalidade do Assistente de IA para garantir a ativação correta.

## Consulte também:

* [Assistente de IA no AEM](/help/ai-assistant-in-aem.md)
* [Controle de acesso da Adobe Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
