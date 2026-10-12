---
title: Salvar formulários como modelos
description: Saiba como criar modelos a partir de formulários com dados exigidos repetidamente.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b97175fd-cc3d-457a-af11-1f8c83192eb7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%
---
# Salvar formulários como modelos {#save-forms-as-templates}

>[!NOTE]
>
>O aplicativo AEM Forms está obsoleto no momento. Para perguntas ou ajuda, contate [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Às vezes, quando os usuários preenchem um formulário, as entradas para alguns campos permanecem as mesmas. Para essas instâncias, é possível preencher os campos que exigem valores idênticos em cada instância e salvar o formulário ou o rascunho como um modelo. Agora, sempre que você criar uma instância do modelo, os campos especificados já estarão preenchidos com os valores especificados no modelo. Ele ajuda a economizar tempo e esforço necessários para preencher o formulário.

Execute as seguintes etapas para criar um template:

1. Abra um formulário e selecione ou preencha os campos que têm valores quase idênticos toda vez que você o usa. É possível incluir um anexo com o modelo que você normalmente adiciona ao preencher o formulário.
1. Selecione o ícone **Salvar como Modelo** ![save_as_template](assets/save_as_template.png). Uma caixa de diálogo para especificar o nome do modelo é exibida.
1. Especifique o nome do modelo e selecione **Salvar**. O modelo aparece na pasta de modelo.

   Se existir um modelo com o mesmo nome, será exibida uma caixa de diálogo para confirmar a substituição do modelo existente. Para substituir o modelo existente por um novo modelo, selecione **Continuar** ou para salvar o modelo com um nome diferente, selecione **Cancelar**.

Agora, você pode abrir o modelo salvo. Toda vez que um modelo é aberto, um novo formulário ou tarefa é criada, e o formulário exibe os dados e opções salvos. Com modelos, é possível editar os dados pré-preenchidos, adicionar um anexo, salvar como rascunho, enviar a tarefa ou criar outro modelo usando-a. Os modelos são específicos para dispositivos móveis e não são sincronizados com o servidor do Adobe Experience Manager Forms.

Você também pode excluir um modelo se ele não for mais necessário. Para excluir um modelo, navegue até a pasta de modelos, selecione as reticências e **Excluir modelo**.

>[!NOTE]
>
>Um modelo está disponível localmente e não está sincronizado com o servidor. Limpar os dados locais do aplicativo exclui o modelo.
