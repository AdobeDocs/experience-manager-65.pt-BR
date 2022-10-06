---
title: Configurando endpoints do Gerenciador de Tarefas
seo-title: Configuring Task Manager endpoints
description: Saiba como configurar endpoints do Gerenciador de tarefas.
seo-description: Learn how to configure Task Manager endpoints.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Configurando endpoints do Gerenciador de Tarefas {#configuring-task-manager-endpoints}

Os endpoints do Gerenciador de tarefas permitem que os usuários do Workspace chamem o serviço.

**Configurações de ponto de extremidade do Gerenciador de Tarefas**

Use as seguintes configurações para configurar um ponto de extremidade do Gerenciador de Tarefas.

**Nome:** (Obrigatório) Identifica o ponto de extremidade. O nome é exibido na exibição de cartão no Workspace. Não inclua um caractere &lt; porque ele truncará o nome exibido no Workspace. Se estiver inserindo um URL como o nome do ponto de extremidade, verifique se ele está em conformidade com as regras de sintaxe especificadas na RFC1738.

**Descrição:** Uma descrição do ponto de extremidade. Não inclua um caractere &lt; porque ele truncará a descrição exibida no Workspace.

**Instruções da tarefa:** Instruções para o usuário que inicia esse fluxo de trabalho.

**Proprietário do Processo:** O nome da pessoa responsável pelo processo.

**O Usuário Pode Encaminhar A Tarefa:** Permite que o usuário encaminhe a tarefa inicial.

**Mostrar janela do anexo:** Permite que o usuário veja a janela de anexo.

**Permitir adição de anexo:** Permite que o usuário adicione anexos e notas.

**Tarefa Inicialmente Bloqueada:** Bloqueia a tarefa inicial.

**Adicionar ACLs para filas compartilhadas:** A tarefa inicial é criada com ACLs para usuários de fila compartilhada.

**Categorização:** (Obrigatório) A categoria na qual o usuário verá o formulário no Workspace. Selecione uma categoria na lista ou selecione Nova categoria para adicionar uma categoria.

**Nome da Operação:** (Obrigatório) Uma lista de operações que podem ser atribuídas ao endpoint.
