---
title: Como usar o Torniquete em um Formulário adaptável AEM 6.5?
description: Melhore a segurança dos formulários com o serviço de Tornição sem esforço. Guia passo a passo no interior.
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: bed93ce3-89db-477a-8316-7598275e4bca
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 11%

---

# Conecte seu ambiente do AEM Forms com o Turnstile {#connect-your-forms-environment-with-turnstile-service}

<!--
<span class="preview">This feature is based on Feature Toggle id `FT_FORMS-12407`. To enable the feature, follow the steps given in the [Enable Feature Toggle](/help/forms/using/enable-feature-toggle.md) article. </span>
-->

<span class="preview">Este recurso não está habilitado por padrão. Você pode escrever de seu endereço oficial para aem-forms-ea@adobe.com para solicitar acesso ao recurso.</span>

O CAPTCHA (um teste de Turing público e completamente automatizado para diferenciar computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. O recurso apresenta um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. O CAPTCHA impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que bots publiquem spam ou outro conteúdo mal-intencionado.

O AEM Forms 6.5 é compatível com as seguintes soluções CAPTCHA:

* [Captcha Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [Captcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Integrar o ambiente do AEM Forms com o Captcha de tartaruga

O Captcha de torniquete da Cloudflare é uma medida de segurança que visa proteger formulários e sites contra bots automatizados, ataques mal-intencionados, spams e tráfego automatizado indesejado. Ele apresenta uma caixa de seleção no envio do formulário para verificar se ele é humano, antes de permitir que ele envie o formulário.

>[!VIDEO](https://video.tv.adobe.com/v/3440945?captions=por_br)

### Pré-requisitos para integrar o ambiente do AEM Forms com o Captcha giratório {#prerequisite}

Para configurar o Turnstile para AEM Forms, você precisa obter a [Chave de site e a chave secreta](https://developers.cloudflare.com/turnstile/get-started/) do site Turnstile.

### Configurar título {#steps-to-configure-hcaptcha}

Para integrar o AEM Forms ao serviço de Borboleta, execute as seguintes etapas:

1. Crie um Contêiner de configuração em seu ambiente do AEM Forms. Um Contêiner de configuração contém as Configurações de nuvem usadas para conectar o AEM Forms a serviços externos. Para criar um Contêiner de configuração:
   1. Abra o ambiente do AEM Forms.
   1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**.
   1. No Navegador de configuração, selecione uma pasta existente ou crie uma nova pasta:
      * Para criar uma **nova pasta** e habilitar as Configurações de Nuvem:
         1. No Navegador de Configuração, clique em **[!UICONTROL Criar]**.
         1. Na caixa de diálogo Criar configuração, especifique um nome, título e verifique as **[!UICONTROL Configurações de nuvem]**.
         1. Clique em **[!UICONTROL Criar]**.
      * Para habilitar a Configuração na Nuvem para uma **pasta existente**:
         1. No Navegador de Configuração, selecione a pasta e clique em **[!UICONTROL Propriedades]**.
         1. Na caixa de diálogo Propriedades de Configuração, habilite **[!UICONTROL Configurações de Nuvem]**.
         1. Clique em **[!UICONTROL Salvar e fechar]** para salvar a configuração.

1. Configurar os Cloud Service:
   1. Na instância do autor do AEM, vá para ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e clique em **[!UICONTROL Turnstile]**.

      ![Borboleta em Cloud Service](assets/turnstile-in-ui.png)
   1. Selecione um Contêiner de configuração, criado ou atualizado, conforme descrito na seção anterior. Clique em **[!UICONTROL Criar]**.

      ![Estrutura de configuração](assets/config-hcaptcha.png)
   1. Especifique **[!UICONTROL Tipo de Widget]** como gerenciado, não interativo ou invisível.
   1. Forneça outros detalhes, como **[!UICONTROL Título]**, **[!UICONTROL Nome]**.
   1. Especifique **[!UICONTROL Chave do Site]** e **[!UICONTROL Chave Secreta]** para o serviço de Borracha [obtido no pré-requisito](#prerequisite).
   1. Clique em **[!UICONTROL Criar]**.

      ![Configure o Cloud Service para conectar seu ambiente do AEM Forms com o Turnstile](assets/config-turntstile.png)

   >[!NOTE]
   > Os usuários não precisam modificar o URL de validação do JavaScript do lado do cliente e o URL de validação do lado do servidor, pois já estão pré-preenchidos para validação do módulo de montagem.

   Depois que o serviço Captcha de tartaruga é configurado, ele é disponibilizado para uso no Formulário adaptável.

## Usar Borboleta em um Formulário Adaptável {#using-turnstile-aem-6.5}

1. Abra o ambiente do AEM Forms.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione um formulário adaptável e clique em **[!UICONTROL Propriedades]**. Em **[!UICONTROL Contêiner de Configuração]**, selecione o Contêiner de Configuração que contém a Configuração na Nuvem que conecta o AEM Forms com o Turnstile.
1. Clique em **[!UICONTROL Salvar e fechar]**.

   Se você não tiver um Contêiner de Configuração para configurar o serviço Captcha, consulte a seção [Configurar Turnstile](#configure-turnstile-steps-to-configure-hcaptcha) para saber como criar um Contêiner de Configuração.

   ![Selecionar Contêiner de Configuração](assets/captcha-properties.png)

1. Selecione um Formulário adaptável e clique em **[!UICONTROL Editar]** para abrir o formulário adaptável no editor.
1. No navegador de componentes, arraste e solte o componente **[!UICONTROL Captcha]** no Formulário adaptável.
1. Selecione o componente **[!UICONTROL Captcha]** e clique no ícone ![Propriedades](assets/configure-icon.svg). Ele abre a caixa de diálogo de propriedades. Especifique as seguintes propriedades:

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Torniquete v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL Título]:** Especifique o título para o componente Captcha. você pode identificar facilmente um componente de formulário com seu título exclusivo no formulário e no editor de regras.
   * **[!UICONTROL Configurações]:** Selecione uma Configuração na Nuvem definida para o Turnstile.
   * **[!UICONTROL Mensagem de Validação]:** Forneça uma mensagem de validação para validar o Captcha no envio do formulário ou em uma ação do usuário.
   * **[!UICONTROL Serviço de Captcha]:** Selecione o Serviço de CAPTCHA para envio de formulário e selecione Turnstile®.
   * **[!UICONTROL Configurações]:** selecione a Configuração na Nuvem definida para Turnstile®.

     >[!NOTE]
     >Você pode ter várias configurações de nuvem no seu ambiente para uma finalidade semelhante. Então, escolha o serviço com cuidado. Se nenhum serviço estiver listado, consulte [Conectar seu ambiente do AEM Forms com o Turnstile](#connect-your-forms-environment-with-turnstile-service) para saber como criar um Cloud Service que conecta seu ambiente do AEM Forms com o serviço Turnstile.

   * **[!UICONTROL Mensagem de Erro]:** Forneça a mensagem de erro a ser exibida ao usuário quando o envio do Captcha falhar.
   * **Tamanho do Captcha:** Você pode selecionar o tamanho de exibição da caixa de diálogo de desafio do hCaptcha®. Use a opção **[!UICONTROL Compactar]** para exibir um tamanho pequeno e o **[!UICONTROL Normal]** para exibir uma caixa de diálogo de desafio hCaptcha® de tamanho relativamente grande.

1. Selecione **[!UICONTROL Concluído]**.


Agora, somente formulários legítimos, em que o preenchimento de formulário apaga com êxito o desafio imposto pelo serviço de Borboleta, são permitidos para o envio do formulário.

![Desafio de tartaruga](assets/turnstile-challenge.png)


## Perguntas frequentes

* **P: Posso usar mais de um componente Captcha em um Formulário adaptável?**
* **Ans:** Não há suporte para o uso de mais de um componente Captcha em um Formulário adaptável. Além disso, não é recomendável usar um componente Captcha em um fragmento ou painel marcado para carregamento lento.

## Consulte também: {#see-also}

* [Uso de CAPTCHA em formulários adaptáveis](/help/forms/using/captcha-adaptive-forms.md)
* [Uso do hCaptcha em formulários adaptáveis](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)
