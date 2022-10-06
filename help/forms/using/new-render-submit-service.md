---
title: Novo serviço de renderização e envio
seo-title: New render and submit service
description: Defina os serviços de renderização e envio no Workbench para renderizar o formulário XDP como HTML ou PDF, dependendo do dispositivo do qual ele é acessado.
seo-description: Define render and submit services in Workbench to render XDP form as HTML or PDF depending on the device it is accessed from.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Novo serviço de renderização e envio{#new-render-and-submit-service}

## Introdução {#introduction}

No Workbench, ao definir uma variável `AssignTask` , especifique um formulário específico (formulário XDP ou PDF). Além disso, especifique um conjunto de serviços de Renderização e Envio, por meio do perfil de ação.

Um XDP pode ser renderizado como um formulário PDF ou HTML. Os novos recursos incluem a capacidade de:

* Renderizar e enviar um formulário XDP como HTML
* Renderizar e enviar um formulário XDP como PDF no desktop e como HTML em dispositivos móveis (por exemplo, um iPad)

### Novo serviço HTML Forms {#new-html-forms-service}

O novo serviço HTML Forms aproveita o novo recurso no Forms para suportar a renderização do formulário XDP como HTML. O novo serviço HTML Forms expõe os seguintes métodos:

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

Mais informações sobre perfis de formulário móvel podem ser encontradas em [Criação de um perfil personalizado](/help/forms/using/custom-profile.md).

## Novos processos de renderização e envio de formulário HTML {#new-html-form-render-amp-submit-processes}

Para cada operação &#39;AssignTask&#39;, especifique um Renderizador e um processo Enviar com o formulário. Esses processos são chamados pelo TaskManager `renderForm`e `submitForm`APIs para permitir manuseio personalizado. Semântica desses processos para o Novo formulário de HTML:

### Renderizar um novo formulário HTML {#render-a-new-html-form}

O novo processo para renderizar o HTML, como todo processo de renderização, tem os seguintes parâmetros de E/S -

Entrada - `taskContext`

Saída - `runtimeMap`

Saída - `outFormDoc`

Esse método simula o comportamento exato de `renderHTMLForm` API de NewHTMLFormsService. Ele chama o `generateFormURL` API para obter o URL para a representação de HTML do formulário. Em seguida, ele preenche o runtimeMap com a seguinte chave ou valores:

novo formulário html = true

newHTMLFormURL = o URL retornado após chamar `generateFormURL` API.

### Enviar um novo formulário HTML {#submit-a-new-html-form}

Esse processo para enviar um novo formulário HTML funciona com os seguintes parâmetros de E/S -

Entrada - `taskContext`

Saída - `runtimeMap`

Saída - `outputDocument`

O processo define o `outputDocument`para `inputDocument`recuperada de `taskContext`.

## Renderizar ou enviar processos padrão e perfis de ação {#default-render-or-submit-processes-and-action-profiles}

Os serviços padrão Renderizar e Enviar permitem que o suporte renderize PDF em um desktop e HTML em dispositivos móveis (iPad).

### Formulário de renderização padrão {#default-render-form}

Esse processo renderiza um formulário XDP em várias plataformas, perfeitamente. O processo recupera o agente do usuário do `taskContext`e usa os dados para chamar o processo para renderizar o HTML ou o PDF.

![formulário de renderização padrão](assets/default-render-form.png)

### Formulário de envio padrão {#default-submit-form}

Esse processo envia um formulário XDP em várias plataformas de maneira simples. Ele recupera o agente do usuário do `taskContext`e usa os dados para chamar o processo para enviar HTML ou PDF.

![padrão-enviar-formulário](assets/default-submit-form.png)

## Mudar a renderização de formulários móveis do PDF para o HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

Os navegadores estão removendo gradualmente o suporte para plug-ins com base NPAPI, incluindo plug-ins para Adobe Acrobat e Adobe Acrobat Reader. Você pode alterar a renderização de formulários móveis de PDF para HTML usando as seguintes etapas:

1. Faça logon no Workbench como um usuário válido.
1. Selecionar **Arquivo** > **Obter aplicativos**.

   A caixa de diálogo Obter aplicativos é exibida.

1. Selecione os aplicativos para os quais deseja alterar a renderização do formulário móvel e clique em **OK**.
1. Abra o processo para o qual deseja alterar a renderização.
1. Abra o ponto de partida/tarefa direcionado, navegue até a seção Apresentação e dados e clique em **Gerenciar perfis de ação**.

   A caixa de diálogo Gerenciar perfis de ação é exibida.
1. Altere as configurações de perfil de renderização padrão de PDF para HTML e clique em **OK**.
1. Verifique o processo.
1. Repita as etapas para alterar a renderização para outros processos.
1. Implante o aplicativo relevante para os processos que você alterou.

### Perfil de ação padrão {#default-action-profile}

O Perfil de ação padrão renderizou o Formulário XDP como PDF. Esse comportamento foi alterado para usar os processos Formulário de renderização padrão e Formulário de envio padrão .

Algumas perguntas frequentes sobre perfis de ação são as seguintes:

![gen_question_b_20](assets/gen_question_b_20.png) **Quais processos de Renderização/Envio estarão disponíveis para uso imediato?**

* Guia de renderização (as guias estão obsoletas)
* Guia de formulário de renderização
* Renderizar formulário PDF
* Renderizar formulário HTML
* Renderizar novo formulário de HTML (novo)
* Formulário de renderização padrão (novo)

E processos de Envio equivalentes.

![gen_question_b_20](assets/gen_question_b_20.png) **Quais perfis de ação estarão disponíveis para uso imediato?**

Para XDP Forms:

* Padrão (renderizar/enviar usando os novos processos &quot;Renderizar/Enviar Padrão&quot;)

![gen_question_b_20](assets/gen_question_b_20.png) **O que precisa ser feito pelo designer de processos para permitir que o formulário seja renderizado no HTML em um dispositivo e no PDF em um desktop?**

Nada. O Perfil de ação padrão é escolhido automaticamente e o modo de renderização também é atendido automaticamente.

![gen_question_b_20](assets/gen_question_b_20.png) **O que precisa ser feito para habilitar a renderização do formulário no HTML em um desktop?**

O usuário deve selecionar o botão de opção HTML para o perfil padrão.

![gen_question_b_20](assets/gen_question_b_20.png) **Haverá algum impacto de atualização na alteração do comportamento do perfil de ação padrão?**

Sim, como os serviços de renderização e envio anteriores associados ao perfil de ação padrão eram diferentes, eles são tratados como uma personalização dos formulários existentes. Ao clicar **Restaurar padrões**, os serviços padrão de renderização e envio são definidos.

Se você modificou os serviços Renderizar ou Enviar formulário PDF ou criou serviços personalizados (digamos, personalizado1) e agora deseja usar a mesma funcionalidade para renderização de HTML. Você precisa replicar o novo renderizador ou enviar serviço (como o custom2) e aplicar personalizações semelhantes a eles. Agora, modifique o perfil de ação do seu XDP para começar a usar serviços personalizados2, em vez do custom1 para renderização ou envio.

O que precisa ser feito pelo designer de processos para permitir que o formulário seja renderizado no HTML em um dispositivo e no PDF em um desktop?
O que precisa ser feito pelo designer de processos para permitir que o formulário seja renderizado no HTML em um dispositivo e no PDF em um desktop?
