---
title: Configurar pontos de extremidade do Gerenciador de tarefas
description: Saiba como configurar os pontos de extremidade do Gerenciador de tarefas para chamar o serviço. Configurações diferentes são necessárias para configurar os pontos de extremidade do Gerenciador de tarefas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Configurar pontos de extremidade do Gerenciador de tarefas {#configuring-task-manager-endpoints}

Os pontos de extremidade do Gerenciador de tarefas permitem que os usuários do Workspace chamem o serviço.

**Configurações de ponto de extremidade do Gerenciador de tarefas**

Use as seguintes configurações para configurar um ponto de extremidade do Gerenciador de tarefas.

**Nome:** (Obrigatório) Identifica o endpoint. O nome é exibido na visualização de cartão no Espaço de trabalho. Não inclua um caractere &lt; porque ele truncará o nome exibido no Workspace. Se você estiver inserindo um URL como o nome do endpoint, verifique se ele está em conformidade com as regras de sintaxe especificadas no RFC1738.

**Descrição:** Uma descrição do endpoint. Não inclua um caractere &lt; porque ele truncará a descrição exibida no Workspace.

**Instruções da tarefa:** Instruções para o usuário que inicia esse workflow.

**Proprietário do processo:** O nome da pessoa responsável pelo processo.

**O Usuário Pode Encaminhar Tarefas:** Permite ao usuário encaminhar a tarefa inicial.

**Mostrar janela de anexo:** Permite que o usuário veja a janela do anexo.

**Permitir Anexo Adicionando:** Permite que o usuário adicione anexos e notas.

**Tarefa inicialmente bloqueada:** Bloqueia a tarefa inicial.

**Adicionar ACLs para Filas Compartilhadas:** A tarefa inicial é criada com ACLs para usuários compartilhados da fila.

**Categorização:** (Obrigatório) A categoria em que o usuário verá o formulário no Espaço de trabalho. Selecione uma categoria na lista ou selecione Nova categoria para adicionar uma categoria.

**Nome da operação:** (Obrigatório) Uma lista de operações que podem ser atribuídas ao endpoint.
