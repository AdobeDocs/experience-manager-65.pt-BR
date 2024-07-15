---
title: Adicionar, ativar, modificar ou remover pontos de extremidade
description: Saiba como adicionar, habilitar, modificar e remover pontos de extremidade.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Adicionar, ativar, modificar ou remover pontos de extremidade {#adding-enabling-modifying-or-removing-endpoints}

## Adicionar um terminal a um serviço {#add-an-endpoint-to-a-service}

Os pontos de extremidade podem ser adicionados somente a serviços. Um ponto de extremidade não pode existir sozinho; ele deve estar associado a um serviço.

>[!NOTE]
>
>É recomendável usar nomes exclusivos ao adicionar pontos de extremidade.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de Serviços, clique no serviço a ser configurado.
1. Na lista da guia Pontos de extremidade, selecione o tipo de ponto de extremidade a ser adicionado e clique em Adicionar.
1. Dependendo do tipo de endpoint, defina configurações adicionais de endpoint.

[Configurações de ponto de extremidade da pasta monitoradas](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Configurações de ponto de extremidade de email](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configurar pontos de extremidade do Gerenciador de tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Configurações de ponto de extremidade de comunicação remota](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Clique em Adicionar.

## Ativar ou desativar um ponto de extremidade {#enable-or-disable-an-endpoint}

Por padrão, novos endpoints são habilitados automaticamente. Mas se você desativou um endpoint, é necessário ativá-lo para que ele fique operacional.

Se você estiver tendo problemas com os serviços do, desative os endpoints associados para solucionar melhor o problema. Você também pode desativar os pontos de extremidade durante a manutenção regular do sistema ou ao atualizar um serviço.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Endpoint Management.
1. Na página Gerenciamento de Ponto de Extremidade, marque a caixa de seleção do ponto de extremidade a ser ativado ou desativado e clique em Ativar ou Desativar.

## Modificar um ponto de extremidade {#modify-an-endpoint}

>[!NOTE]
>
>As alterações feitas em uma configuração de endpoint usando o console de administração não são refletidas nas cópias em tempo de design dos aplicativos. Se você reimplantar um aplicativo, qualquer alteração feita em seus endpoints usando o console de administração será perdida.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Endpoint Management.
1. Na página Gerenciamento de ponto de extremidade, clique no ponto de extremidade a ser modificado.
1. Na página Atualizar endpoint, modifique o nome, a descrição e as configurações do endpoint.

   >[!NOTE]
   >
   >Não inclua um caractere &lt; no nome ou na descrição porque ele truncará o nome ou a descrição exibida no Workspace.

1. Para salvar as alterações, clique em Atualizar.

Você também pode fazer essa tarefa na página Gerenciamento de serviço selecionando um serviço e clicando na guia Pontos finais.

## Remover um ponto de extremidade {#remove-an-endpoint}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Endpoint Management.
1. Na página Gerenciamento de Ponto de Extremidade, marque a caixa de seleção do ponto de extremidade a ser removido e clique em Remover. O endpoint não é mais exibido.
