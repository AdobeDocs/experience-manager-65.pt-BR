---
title: Trabalhar com um formulário
description: Exibir e atualizar o formulário associado a uma tarefa ou Ponto inicial no aplicativo AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Trabalhar com um formulário {#working-with-a-form}

Se um formulário estiver ativado para sincronização no aplicativo de formulários, ele será baixado e você poderá trabalhar diretamente com ele.

Os formulários são baixados no aplicativo e estão disponíveis offline. Por exemplo, você está executando uma empresa bancária e um cliente preenche um aplicativo em seu site. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena para revisão. O administrador revisa o formulário e cria um formulário de verificação na instância de autor do AEM. O administrador habilita a sincronização do formulário com o aplicativo AEM Forms. Se o formulário de verificação estiver disponível no aplicativo AEM Forms, seu agente de campo poderá usar um dispositivo móvel para verificar os detalhes do cliente. O dispositivo móvel é sincronizado com o servidor e o formulário de verificação é carregado no aplicativo. O agente de campo pode visitar o cliente, verificar os detalhes, salvar dados como rascunho ou enviar o formulário de verificação. O formulário é sincronizado com o servidor sempre que o aplicativo está online.

Para sincronizar o formulário no aplicativo AEM Forms:

1. Na instância do autor, selecione um formulário e clique em **Exibir Propriedades**.
1. Na página de propriedades, clique em **Avançado.**
1. Em Avançado, habilite a opção: **Sincronizar com o aplicativo AEM Forms** e selecione **Salvar**.

Para sincronizar vários formulários, na instância do autor, selecione vários formulários no gerenciador de formulários e selecione **Sincronizar com o aplicativo AEM Forms**. Quando o formulário é publicado, o aplicativo AEM Forms pode se conectar ao servidor de publicação e buscar os formulários.

Se o aplicativo Android AFA (AEM Form Application) falhar na sincronização, execute as seguintes etapas para corrigir o problema de sincronização:

1. Vá para o **https://[server]:[port]/system/console/configMgr**.
1. Procure o **[!UICONTROL Manipulador de autenticação de token do Adobe Granite]** e clique em **[!UICONTROL Editar]**.
1. Selecione a opção **[!UICONTROL Nenhum]** no menu suspenso para o atributo **[!UICONTROL SameSite do atributo cookie de token de logon]**.
1. Clique em **[!UICONTROL Salvar]**.

![Sincronizar imagem com o aplicativo Android AFA](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>Formulários suportados:
>
>* Formulários adaptáveis (sem carregamento lento)
>* Formulários móveis
>
>Os anexos no nível do formulário não são compatíveis com os formulários adaptáveis obtidos no aplicativo AEM Forms sincronizado com o servidor OSGi do AEM Forms. Os usuários podem anexar arquivos em um campo se o autor tiver ativado anexos no nível do campo no momento da criação do formulário.


**Para abrir e atualizar um formulário**

1. Para abrir um formulário, selecione o **[!UICONTROL Formulário]** na tela inicial.
1. Você pode atualizar os campos do formulário, adicionar anexos, salvar como rascunho e enviá-lo.
