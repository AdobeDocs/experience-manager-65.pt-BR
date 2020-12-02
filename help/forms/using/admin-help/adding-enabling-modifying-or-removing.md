---
title: Adicionar, ativar, modificar ou remover pontos de extremidade
seo-title: Adicionar, ativar, modificar ou remover pontos de extremidade
description: Saiba como adicionar, ativar, modificar e remover pontos de extremidade.
seo-description: Saiba como adicionar, ativar, modificar e remover pontos de extremidade.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Adicionar, ativar, modificar ou remover pontos finais {#adding-enabling-modifying-or-removing-endpoints}

## Adicionar um terminal a um serviço {#add-an-endpoint-to-a-service}

Os pontos de extremidade podem ser adicionados somente a serviços. Um terminal não pode existir sozinho; deve estar associado a um serviço.

>[!NOTE]
>
>É recomendável usar nomes exclusivos ao adicionar pontos de extremidade.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique no serviço a ser configurado.
1. Na lista da guia Pontos de extremidade, selecione o tipo de ponto de extremidade a ser adicionado e clique em Adicionar.
1. Dependendo do tipo de endpoint, defina configurações adicionais de endpoint.

   [Configurações de ponto de extremidade de pasta monitorada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

   [Configurações de ponto de extremidade de email](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

   [Configuração dos pontos finais do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

   [Configurações de ponto de extremidade remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Clique em Adicionar.

## Ativar ou desativar um terminal {#enable-or-disable-an-endpoint}

Por padrão, novos pontos de extremidade são ativados automaticamente. Mas se você tiver desabilitado um terminal, precisará habilitá-lo para que ele esteja operacional.

Se você estiver enfrentando problemas com os serviços, desative os pontos de extremidade associados para melhor solucionar o problema. Você também pode desativar os pontos de extremidade durante a manutenção regular do sistema ou durante a atualização de um serviço.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de ponto de extremidade.
1. Na página Gerenciamento de pontos de extremidade, marque a caixa de seleção do ponto de extremidade a ser ativado ou desativado e clique em Ativar ou Desativar.

## Modificar um ponto de extremidade {#modify-an-endpoint}

>[!NOTE]
>
>As alterações feitas na configuração de um terminal usando o console de administração não são refletidas nas cópias em tempo de design dos aplicativos. Se você reimplantar um aplicativo, qualquer alteração feita em seus pontos finais usando o console de administração será perdida.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de ponto de extremidade.
1. Na página Gerenciamento de ponto de extremidade, clique no ponto de extremidade para modificá-lo.
1. Na página Atualizar ponto de extremidade, modifique o nome do ponto de extremidade, a descrição e as configurações.

   >[!NOTE]
   >
   >Não inclua um caractere &lt; no nome ou na descrição porque ele truncará o nome ou a descrição exibidos no Workspace.

1. Para salvar as alterações, clique em Atualizar.

Você também pode fazer essa tarefa na página Gerenciamento de serviços selecionando um serviço e, em seguida, clicando na guia Pontos de extremidade.

## Remover um ponto de extremidade {#remove-an-endpoint}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de ponto de extremidade.
1. Na página Gerenciamento de ponto de extremidade, marque a caixa de seleção do ponto de extremidade a ser removido e clique em Remover. O terminal não é mais exibido.

