---
title: Envio assíncrono de formulários adaptáveis
description: Saiba como configurar o envio assíncrono para formulários adaptáveis.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Envio assíncrono de formulários adaptáveis{#asynchronous-submission-of-adaptive-forms}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html) |
| AEM 6.5 | Este artigo |

Tradicionalmente, os formulários web são configurados para enviar de forma síncrona. No envio síncrono, quando os usuários enviam um formulário, eles são redirecionados para uma página de confirmação, uma página de agradecimento ou, se houver falha de envio, uma página de erro. No entanto, experiências da Web modernas, como aplicativos de página única, estão ganhando popularidade, onde a página da Web permanece estática enquanto a interação cliente-servidor acontece em segundo plano. Agora você pode fornecer essa experiência com formulários adaptáveis configurando o envio assíncrono.

No envio assíncrono, quando um usuário envia um formulário, o desenvolvedor do formulário conecta uma experiência separada, como redirecionar para outro formulário ou uma seção separada do site. O autor também pode conectar serviços separados, como enviar dados para um armazenamento de dados diferente ou adicionar um mecanismo de análise personalizado. Se houver envio assíncrono, um formulário adaptável se comporta como um aplicativo de página única, pois o formulário não é recarregado ou sua URL não é alterada quando os dados do formulário enviado são validados no servidor.

Leia para obter detalhes sobre envio assíncrono em formulários adaptáveis.

## Configurar envio assíncrono {#configure}

Para configurar o envio assíncrono para um formulário adaptável:

1. No modo de criação do formulário adaptável, selecione o objeto Contêiner de formulário e selecione ![cmppr1](assets/cmppr1.png) para abrir suas propriedades.
1. No **[!UICONTROL Envio]** seção de propriedades, ativar **[!UICONTROL Usar envio assíncrono]**.
1. No **[!UICONTROL Ao enviar]** selecione uma das seguintes opções a serem executadas no envio bem-sucedido do formulário.

   * **[!UICONTROL Redirecionar para URL]**: redireciona para a URL ou página especificada no envio do formulário. Você pode especificar um URL ou procurar para escolher o caminho para uma página no **[!UICONTROL URL/caminho de redirecionamento]** campo.
   * **[!UICONTROL Mostrar mensagem]**: exibe uma mensagem no envio do formulário. Você pode escrever uma mensagem no campo de texto abaixo da opção Mostrar mensagem. O campo de texto é compatível com a formatação de rich text.

1. Selecionar ![botão de seleção1](assets/check-button1.png) para salvar as propriedades.

## Como o envio assíncrono funciona {#how-asynchronous-submission-works}

O AEM Forms fornece manipuladores de sucesso e erro prontos para uso para envios de formulários. Os manipuladores são funções do lado do cliente executadas com base na resposta do servidor. Quando um formulário é enviado, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o evento bem-sucedido ou com erro para o envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função.

Além disso, os autores e desenvolvedores de formulários podem escrever regras no nível do formulário para substituir os manipuladores padrão. Para obter mais informações, consulte [Substituir manipuladores padrão usando regras](#custom).

Primeiro, vamos analisar a resposta do servidor em busca de eventos de sucesso e erro.

### Resposta do servidor para evento de sucesso de envio {#server-response-for-submission-success-event}

A estrutura da resposta do servidor para o evento de sucesso de envio é a seguinte:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

A resposta do servidor se o envio de um formulário for bem-sucedido inclui:

* Tipo de formato de dados de formulário: XML ou JSON
* Dados de formulário em formato XML ou JSON
* Opção selecionada para redirecionar para uma página ou exibir uma mensagem conforme configurado no formulário
* URL da página ou conteúdo da mensagem conforme configurado no formulário

O manipulador de sucesso lê a resposta do servidor e redireciona adequadamente para o URL da página configurada ou exibe uma mensagem.

### Resposta do servidor para evento de erro de envio {#server-response-for-submission-error-event}

A estrutura da resposta do servidor para o evento de erro de envio é a seguinte:

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

A resposta do servidor se houver um erro no envio do formulário inclui:

* Motivo do erro, falha no CAPTCHA ou validação no lado do servidor
* Lista de objetos de erro, que inclui a expressão SOM do campo cuja validação falhou e a mensagem de erro correspondente

O manipulador de erros lê a resposta do servidor e exibe a mensagem de erro no formulário.

## Substituir manipuladores padrão usando regras {#custom}

Desenvolvedores de formulários e autores podem escrever regras, no nível do formulário, no editor de código para substituir manipuladores padrão. A resposta do servidor para eventos de sucesso e erro é exposta no nível do formulário, que os desenvolvedores podem acessar usando `$event.data` nas regras.

Execute as seguintes etapas para escrever regras no editor de código para lidar com eventos de sucesso e erro.

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e ![edit-rules1](assets/edit-rules1.png) para abrir o editor de regras.
1. Selecionar **[!UICONTROL Formulário]** na árvore Objetos de formulário e selecione **[!UICONTROL Criar]**.
1. Selecionar **[!UICONTROL Editor de código]** no menu suspenso de seleção de modo.
1. No editor de código, selecione **[!UICONTROL Editar código]**. Selecionar **[!UICONTROL Editar]** no diálogo de confirmação.
1. Escolher **[!UICONTROL Envio bem-sucedido]** ou **[!UICONTROL Erro no envio]** do **[!UICONTROL Evento]** menu suspenso.
1. Escreva uma regra para o evento selecionado e selecione **[!UICONTROL Concluído]** para salvar a regra.
