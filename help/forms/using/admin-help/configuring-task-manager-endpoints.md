---
title: Configuração dos pontos finais do Gerenciador de Tarefas
seo-title: Configuração dos pontos finais do Gerenciador de Tarefas
description: Saiba como configurar os pontos de extremidade do Tarefa Manager.
seo-description: Saiba como configurar os pontos de extremidade do Tarefa Manager.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Configurando pontos finais do Gerenciador de Tarefas {#configuring-task-manager-endpoints}

Os pontos de extremidade do Gerenciador de tarefas permitem que os usuários do Workspace chamem o serviço.

**Configurações de ponto de extremidade do Gerenciador de tarefas**

Use as seguintes configurações para configurar um terminal do Gerenciador de Tarefas.

**Nome:** (Obrigatório) Identifica o endpoint. O nome é exibido na visualização do cartão no Workspace. Não inclua um caractere &lt; porque ele truncará o nome exibido no Workspace. Se você estiver inserindo um URL como o nome do ponto de extremidade, verifique se ele está em conformidade com as regras de sintaxe especificadas em RFC1738.

**Descrição:** uma descrição do ponto final. Não inclua um caractere &lt; porque ele truncará a descrição exibida no Workspace.

**Instruções de tarefa:** Instruções para o usuário que start esse fluxo de trabalho.

**Proprietário do Processo:** O nome da pessoa responsável pelo processo.

**O usuário pode encaminhar a Tarefa:** permite que o usuário encaminhe a tarefa inicial.

**Mostrar janela de anexo:** permite que o usuário veja a janela de anexo.

**Permitir adição de anexo:** permite que o usuário adicione anexos e observações.

**Tarefa inicialmente travada:** trava a tarefa inicial.

**Adicionar ACLs para filas compartilhadas:** a tarefa inicial é criada com ACLs para usuários de filas compartilhadas.

**Categorização:** (Obrigatória) A categoria na qual o usuário visualizará o formulário no Workspace. Selecione uma categoria na lista ou selecione Nova Categoria para adicionar uma categoria.

**Nome da Operação:**  (Obrigatório) Uma lista de operações que podem ser atribuídas ao ponto final.
