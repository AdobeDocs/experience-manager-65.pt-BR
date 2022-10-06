---
title: Adicionar, ativar, modificar ou remover pontos de extremidade
seo-title: Adding, enabling, modifying, or removing endpoints
description: Saiba como adicionar, ativar, modificar e remover pontos de extremidade.
seo-description: Learn how to add, enable, modify and remove endpoints.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Adicionar, ativar, modificar ou remover pontos de extremidade {#adding-enabling-modifying-or-removing-endpoints}

## Adicionar um terminal a um serviço {#add-an-endpoint-to-a-service}

Os endpoints podem ser adicionados apenas a serviços. Um terminal não pode existir sozinho; deve estar associado a um serviço.

>[!NOTE]
>
>É recomendável usar nomes exclusivos ao adicionar pontos de extremidade.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Serviços.
1. Na página Gerenciamento de serviços , clique no serviço a ser configurado.
1. Na lista da guia Endpoints , selecione o tipo de endpoint a ser adicionado e clique em Add.
1. Dependendo do tipo de ponto de extremidade, defina configurações adicionais de ponto de extremidade.

[Configurações de ponto de extremidade de pasta assistida](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Configurações do ponto de extremidade de email](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configurando endpoints do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Remoção das configurações de ponto de extremidade](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Clique em Adicionar.

## Ativar ou desativar um ponto de extremidade {#enable-or-disable-an-endpoint}

Por padrão, novos endpoints são ativados automaticamente. Mas se você tiver desativado um terminal, precisará habilitá-lo para que ele fique operacional.

Se você estiver enfrentando problemas com os serviços, desative os endpoints associados para solucionar melhor o problema. Você também pode desativar os endpoints durante a manutenção regular do sistema ou ao atualizar um serviço.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Endpoint.
1. Na página Gerenciamento de ponto de extremidade, marque a caixa de seleção do ponto de extremidade a ser ativado ou desativado e clique em Ativar ou Desativar.

## Modificar um ponto de extremidade {#modify-an-endpoint}

>[!NOTE]
>
>As alterações feitas em uma configuração de endpoint usando o console de administração não são refletidas nas cópias de tempo de design dos aplicativos. Se você reimplantar um aplicativo, qualquer alteração feita em seus endpoints usando o console de administração será perdida.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Endpoint.
1. Na página Gerenciamento de ponto de extremidade , clique no ponto de extremidade para modificar.
1. Na página Atualizar ponto de extremidade , modifique o nome do ponto de extremidade, a descrição e as configurações.

   >[!NOTE]
   >
   >Não inclua um caractere &lt; no nome ou na descrição porque ele truncará o nome ou a descrição exibidos no Workspace.

1. Para salvar as alterações, clique em Atualizar.

Também é possível fazer essa tarefa na página Gerenciamento de serviços, selecionando um serviço e clicando na guia Endpoints .

## Remover um ponto de extremidade {#remove-an-endpoint}

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Endpoint.
1. Na página Gerenciamento de ponto de extremidade , marque a caixa de seleção do ponto de extremidade a ser removido e clique em Remover. O terminal não é mais exibido.
