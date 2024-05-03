---
title: Salvar formulários como modelos
description: Saiba como criar modelos a partir de formulários com dados exigidos repetidamente.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b97175fd-cc3d-457a-af11-1f8c83192eb7
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Salvar formulários como modelos {#save-forms-as-templates}

Às vezes, quando os usuários preenchem um formulário, as entradas para alguns campos permanecem as mesmas. Para essas instâncias, é possível preencher os campos que exigem valores idênticos em cada instância e salvar o formulário ou o rascunho como um modelo. Agora, sempre que você criar uma instância do modelo, os campos especificados já estarão preenchidos com os valores especificados no modelo. Ele ajuda a economizar tempo e esforço necessários para preencher o formulário.

Execute as seguintes etapas para criar um template:

1. Abra um formulário e selecione ou preencha os campos que têm valores quase idênticos toda vez que você o usa. É possível incluir um anexo com o modelo que você normalmente adiciona ao preencher o formulário.
1. Selecione o **Salvar como modelo** ![save_as_template](assets/save_as_template.png)ícone. Uma caixa de diálogo para especificar o nome do modelo é exibida.
1. Especifique o nome do modelo e selecione **Salvar**. O modelo aparece na pasta de modelo.

   Se existir um modelo com o mesmo nome, será exibida uma caixa de diálogo para confirmar a substituição do modelo existente. Para substituir o modelo existente pelo novo modelo, selecione **Continuar** ou para salvar o modelo com um nome diferente, selecione **Cancelar**.

Agora, você pode abrir o modelo salvo. Toda vez que um modelo é aberto, um novo formulário ou tarefa é criada, e o formulário exibe os dados e opções salvos. Com modelos, é possível editar os dados pré-preenchidos, adicionar um anexo, salvar como rascunho, enviar a tarefa ou criar outro modelo usando-a. Os modelos são específicos para dispositivos móveis e não são sincronizados com o servidor do Adobe Experience Manager Forms.

Você também pode excluir um modelo se ele não for mais necessário. Para excluir um modelo, navegue até a pasta de modelos, selecione as reticências e selecione **Excluir modelo**.

>[!NOTE]
>
>Um modelo está disponível localmente e não está sincronizado com o servidor. Limpar os dados locais do aplicativo exclui o modelo.
