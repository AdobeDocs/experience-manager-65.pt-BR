---
title: Como trabalhar com um formulário
seo-title: Como trabalhar com um formulário
description: Visualização e atualize o formulário associado a uma tarefa ou ponto de partida no aplicativo AEM Forms
seo-description: Visualização e atualize o formulário associado a uma tarefa ou ponto de partida no aplicativo AEM Forms
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Como trabalhar com um formulário {#working-with-a-form}

Se um formulário estiver habilitado para sincronização no aplicativo de formulários, ele será baixado e você poderá trabalhar diretamente com ele.

Os formulários são baixados no aplicativo e estão disponíveis offline. Por exemplo, você está executando uma empresa bancária e um cliente preenche um aplicativo em seu site. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena para revisão. O administrador revisa o formulário e cria um formulário de verificação na instância do autor de AEM. O administrador permite a sincronização do formulário com o aplicativo AEM Forms. Se o formulário de verificação estiver disponível no aplicativo AEM Forms, seu agente de campo poderá usar um dispositivo móvel para verificar os detalhes do cliente. O dispositivo móvel é sincronizado com o servidor e o formulário de verificação é carregado no aplicativo. Seu agente de campo pode visitar seu cliente, verificar os detalhes, salvar dados como rascunho ou enviar o formulário de verificação. O formulário é sincronizado com o servidor sempre que seu aplicativo estiver online.

Para sincronizar seu formulário no aplicativo AEM Forms:

1. Na instância do autor, selecione um formulário e clique em Propriedades **da** Visualização.
1. Na página de propriedades, clique em **Avançado.**
1. Em Avançado, ative a opção: Sincronize **com o aplicativo** AEM Forms e toque em **Salvar**.

Para sincronizar vários formulários, na instância do autor, selecione vários formulários no gerenciador de formulários e toque em **Sincronizar com o aplicativo** AEM Forms. Quando o formulário é publicado, o aplicativo AEM Forms pode se conectar ao servidor de publicação e buscar os formulários.

>[!NOTE]
>
>Formulários suportados:
>
>* Formulários adaptáveis (sem carregamento lento)
>* Formulários móveis
>
>
Os anexos de nível de formulário não são suportados nos formulários adaptáveis obtidos no aplicativo AEM Forms sincronizado com o servidor AEM Forms OSGi. Os usuários podem anexar arquivos em um campo se o autor tiver ativado anexos de nível de campo no momento da criação do formulário.

**Para abrir e atualizar um formulário**

1. Para abrir um formulário, toque no formulário na tela inicial.
1. É possível atualizar os campos do formulário, adicionar anexos, salvar como rascunho e enviá-lo.
