---
title: Submissão assíncrona de formulários adaptativos
seo-title: Submissão assíncrona de formulários adaptativos
description: Saiba como configurar o envio assíncrono para formulários adaptáveis.
seo-description: Saiba como configurar o envio assíncrono para formulários adaptáveis.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# Submissão assíncrona de formulários adaptativos{#asynchronous-submission-of-adaptive-forms}

Tradicionalmente, formulários da Web são configurados para envio sincronizado. No envio síncrono, quando os usuários enviam um formulário, eles são redirecionados para uma página de confirmação, uma página de agradecimento ou, em caso de falha no envio, uma página de erro. Entretanto, experiências modernas da Web, como aplicativos de página única, estão ganhando popularidade, onde a página da Web permanece estática, enquanto a interação cliente-servidor acontece em segundo plano. Agora você pode fornecer essa experiência com formulários adaptáveis configurando o envio assíncrono.

No envio assíncrono, quando um usuário envia um formulário, o desenvolvedor do formulário conecta uma experiência separada, como redirecionar para outro formulário ou uma seção separada do site. O autor também pode fazer plug-in em serviços separados como enviar dados para um armazenamento de dados diferente ou adicionar um mecanismo de análise personalizado. No caso de envio assíncrono, um formulário adaptável se comporta como um aplicativo de página única, pois o formulário não é recarregado ou seu URL não é alterado quando os dados do formulário submetido são validados no servidor.

Leia para obter detalhes sobre o envio assíncrono em formulários adaptáveis.

## Configurar submissão assíncrona {#configure}

Para configurar o envio assíncrono para um formulário adaptável:

1. No modo de criação de formulário adaptável, selecione o objeto Container de formulário e toque em ![cmppr1](assets/cmppr1.png) para abrir suas propriedades.
1. Na seção Propriedades de **[!UICONTROL envio]** , ative **[!UICONTROL Usar envio]** assíncrono.
1. Na seção **[!UICONTROL Ao enviar]** , selecione uma das opções a seguir para executar no envio bem-sucedido do formulário.

   * **[!UICONTROL Redirecionar para URL]**: Redireciona para o URL ou página especificada no envio do formulário. Você pode especificar um URL ou navegar para escolher o caminho para uma página no campo URL/Caminho **[!UICONTROL de]** redirecionamento.
   * **[!UICONTROL Mostrar mensagem]**: Exibe uma mensagem no envio do formulário. Você pode gravar uma mensagem no campo de texto abaixo da opção Mostrar mensagem. O campo de texto oferece suporte à formatação Rich Text.

1. Toque em ![check-button1](assets/check-button1.png) para salvar as propriedades.

## Como o envio assíncrono funciona {#how-asynchronous-submission-works}

O AEM Forms fornece controladores de erros e sucesso prontos para uso para envios de formulário. Os manipuladores são funções do lado do cliente que são executadas com base na resposta do servidor. Quando um formulário é submetido, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o evento bem-sucedido ou erro para o envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função.

Além disso, autores e desenvolvedores de formulários podem gravar regras no nível de formulário para substituir manipuladores padrão. Para obter mais informações, consulte [Substituir manipuladores padrão usando regras](#custom).

Analisemos primeiro a resposta do servidor para eventos bem-sucedidos e com erros.

### Resposta do servidor para o evento bem-sucedido de envio {#server-response-for-submission-success-event}

A estrutura para a resposta do servidor para o evento bem-sucedido de envio é a seguinte:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

A resposta do servidor em caso de envio de formulário bem-sucedido inclui:

* Tipo de formato de dados do formulário: XML ou JSON
* Dados de formulário no formato XML ou JSON
* Opção selecionada para redirecionar para uma página ou exibir uma mensagem conforme configurado no formulário
* URL da página ou conteúdo da mensagem conforme configurado no formulário

O manipulador de sucesso lê a resposta do servidor e, consequentemente, redireciona para o URL da página configurada ou exibe uma mensagem.

### Resposta do servidor para o evento de erro de envio {#server-response-for-submission-error-event}

A estrutura para a resposta do servidor para o evento de erro de envio é a seguinte:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

A resposta do servidor em caso de erro no envio do formulário inclui:

* Motivo do erro, falha na validação CAPTCHA ou no servidor
* Lista de objetos de erro, que inclui a expressão SOM do campo que falhou na validação e a mensagem de erro correspondente

O manipulador de erros lê a resposta do servidor e, consequentemente, exibe a mensagem de erro no formulário.

## Substituir manipuladores padrão usando regras {#custom}

Os desenvolvedores e autores de formulários podem gravar regras, no nível de formulário, no editor de código para substituir manipuladores padrão. A resposta do servidor para eventos de erro e sucesso é exposta no nível do formulário, que os desenvolvedores podem acessar usando `$event.data` as regras.

Execute as seguintes etapas para gravar regras no editor de código para lidar com eventos bem-sucedidos e de erro.

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em ![edit-rules1](assets/edit-rules1.png) para abrir o editor de regras.
1. Selecione **[!UICONTROL Formulário]** na árvore Objetos de formulário e toque em **[!UICONTROL Criar]**.
1. Selecione Editor **[!UICONTROL de]** código no menu suspenso de seleção de modo.
1. No editor de código, toque em **[!UICONTROL Editar código]**. Toque em **[!UICONTROL Editar]** na caixa de diálogo de confirmação.
1. Escolha Envio **** bem-sucedido ou **[!UICONTROL Erro no Envio]** no menu suspenso **[!UICONTROL Evento]** .
1. Escreva uma regra para o evento selecionado e toque em **[!UICONTROL Concluído]** para salvar a regra.

