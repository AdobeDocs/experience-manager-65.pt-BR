---
title: Uso de CAPTCHA em formulários adaptáveis
seo-title: Uso de CAPTCHA em formulários adaptáveis
description: Saiba como configurar AEM serviço CAPTCHA ou Google reCAPTCHA em formulários adaptáveis.
seo-description: Saiba como configurar AEM serviço CAPTCHA ou Google reCAPTCHA em formulários adaptáveis.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 7a3f54d90769708344e6751756b2a12ac6c962d7
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---


# Uso de CAPTCHA em formulários adaptáveis{#using-captcha-in-adaptive-forms}

O CAPTCHA (Completamente Automated Public Turing test to tell Computers and Humans Além) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. Ele coloca um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. Impede que o usuário continue se o teste falhar e ajuda a tornar as transações online seguras, impedindo que bots postem spam ou fins mal-intencionados.

O AEM Forms suporta CAPTCHA em formulários adaptáveis. Você pode usar o serviço reCAPTCHA do Google para implementar CAPTCHA.

>[!NOTE]
>
>* O AEM Forms suporta apenas o reCaptcha v2. Nenhuma outra versão é compatível.
>* Não há suporte para CAPTCHA em formulários adaptáveis no modo offline no aplicativo AEM Forms.

>



## Configurar o serviço ReCAPTCHA pelo Google {#google-recaptcha}

Os autores de formulários podem usar o serviço reCAPTCHA do Google para implementar CAPTCHA em formulários adaptáveis. Ele oferece recursos CAPTCHA avançados para proteger seu site. Para obter mais informações sobre como o reCAPTCHA funciona, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Para implementar o serviço reCAPTCHA no AEM Forms:

1. Obtenha [o par de chaves da API reCAPTCHA](https://www.google.com/recaptcha/admin) do Google. Inclui uma chave do site e um segredo.
1. Criar contêiner de configuração para serviços em nuvem.

   1. Vá para **[!UICONTROL Tools > General > Configuration Browser]**.
      * Consulte a documentação do [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
   1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações do serviço de nuvem.

      1. No Navegador de configuração, selecione a pasta **[!UICONTROL global]** e toque em **[!UICONTROL Propriedades]**.

      1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações da nuvem]**.
      1. Toque em **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.
   1. No Navegador de configuração, toque em **[!UICONTROL Criar]**.
   1. Na caixa de diálogo Criar configuração, especifique um título para a pasta e habilite **[!UICONTROL Configurações da nuvem]**.
   1. Toque em **[!UICONTROL Criar]** para criar a pasta ativada para as configurações do serviço de nuvem.


1. Configure o serviço de nuvem para reCAPTCHA.

   1. Na instância do autor do AEM, vá para ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Toque em **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o contêiner de configuração criado na etapa anterior e toque em **[!UICONTROL Create]**.
   1. Especifique Nome, Chave do site e Chave secreta para o serviço reCAPTCHA e toque em **[!UICONTROL Criar]** para criar a configuração do serviço de nuvem.
   1. Na caixa de diálogo Editar componente , especifique o site e as chaves secretas obtidas na etapa 1. Toque em **Salvar configurações** e toque em **OK** para concluir a configuração.

   Quando o serviço reCAPTCHA é configurado, ele está disponível para uso em formulários adaptáveis. Para obter mais informações, consulte [Usando CAPTCHA em formulários adaptáveis](#using-captcha).

## Use CAPTCHA em formulários adaptáveis {#using-captcha}

Para usar CAPTCHA em formulários adaptáveis:

1. Abra um formulário adaptável no modo de edição.

   >[!NOTE]
   >
   >Verifique se o contêiner de configuração selecionado ao criar o formulário adaptável contém o serviço de nuvem reCAPTCHA. Também é possível editar as propriedades adaptáveis do formulário para alterar o contêiner de configuração associado ao formulário.

1. No navegador de componentes, arraste e solte o componente **Captcha** no formulário adaptável.

   >[!NOTE]
   >
   >Não é possível usar mais de um componente Captcha em um formulário adaptável. Além disso, não é recomendado usar CAPTCHA em um painel marcado para carregamento lento ou em um fragmento.

   >[!NOTE]
   >
   >O Captcha diferencia tempo e expira em cerca de um minuto. Portanto, é recomendável colocar o componente Captcha logo antes do botão Enviar no formulário adaptável.

1. Selecione o componente Captcha adicionado e toque em ![cmppr](assets/cmppr.png) para editar suas propriedades.
1. Especifique um título para o widget CAPTCHA. O valor padrão é **Captcha**. Selecione **Ocultar título** se não quiser que o título apareça.
1. No menu suspenso **Captcha service**, selecione **reCaptcha** para habilitar o serviço reCAPTCHA se você o tiver configurado conforme descrito em [ReCAPTCHA service by Google](#google-recaptcha). Selecione uma configuração no menu suspenso Configurações . Além disso, selecione o tamanho como **Normal** ou **Compacto** para o widget reCAPTCHA.

   >[!NOTE]
   >
   >Não selecione **[!UICONTROL Default]** no menu suspenso do serviço Captcha, pois o serviço AEM CAPTCHA padrão está obsoleto.

1. Salve as propriedades.

O serviço reCAPTCHA está ativado no formulário adaptável. Você pode visualizar o formulário e ver o CAPTCHA funcionando.

### Mostrar ou ocultar o componente CAPTCHA com base nas regras {#show-hide-captcha}

Você pode optar por mostrar ou ocultar o componente CAPTCHA com base nas regras aplicadas em um componente em um formulário adaptável. Toque no componente, selecione ![editar regras](assets/edit-rules-icon.svg) e toque em **[!UICONTROL Criar]** para criar uma regra. Para obter mais informações sobre como criar regras, consulte [Editor de regras](rule-editor.md).

Por exemplo, o componente CAPTCHA deve ser exibido em um Formulário adaptável somente se o campo Valor da moeda no formulário tiver um valor superior a 25000.

Toque no campo **[!UICONTROL Valor da moeda]** no formulário e crie as seguintes regras:

![Mostrar ou ocultar regras](assets/rules-show-hide-captcha.png)

### Validar CAPTCHA {#validate-captcha}

Você pode validar CAPTCHA em um Formulário adaptável ao enviar o formulário ou basear a validação CAPTCHA em ações e condições do usuário.

#### Validar CAPTCHA no envio do formulário {#validation-form-submission}

Para validar um CAPTCHA automaticamente ao enviar um Formulário adaptável:

1. Toque no componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para exibir as propriedades do componente.
1. Na seção **[!UICONTROL Validate CAPTCHA]**, selecione **[!UICONTROL Validate CAPTCHA no envio do formulário]**.
1. Toque em ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

#### Validar CAPTCHA em ações e condições do usuário {#validate-captcha-user-action}

Para validar um CAPTCHA com base em condições e ações do usuário:

1. Toque no componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para exibir as propriedades do componente.
1. Na seção **[!UICONTROL Validar CAPTCHA]**, selecione **[!UICONTROL Validar CAPTCHA em uma ação do usuário]**.
1. Toque em ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

[!DNL Experience Manager Forms] O fornece  `ValidateCAPTCHA` API para validar CAPTCHA usando condições predefinidas. Você pode chamar a API usando uma Ação de envio personalizada ou definindo regras em componentes em um formulário adaptável.

Veja a seguir um exemplo de uma API `ValidateCAPTCHA` para validar CAPTCHA usando condições predefinidas:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
    	GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

O exemplo significa que a API `ValidateCAPTCHA` valida o CAPTCHA no formulário somente se o número de dígitos na caixa numérica especificada pelo usuário durante o preenchimento do formulário for maior que 5.

**Opção 1: Use a API  [!DNL Experience Manager Forms] ValidateCAPTCHA para validar CAPTCHA usando uma ação de envio personalizada**

Execute as seguintes etapas para usar a API `ValidateCAPTCHA` para validar CAPTCHA usando uma Ação de envio personalizada:

1. Adicione o script que inclui a API `ValidateCAPTCHA` à Ação de envio personalizada. Para obter mais informações sobre ações de envio personalizadas, consulte [Criar uma ação de envio personalizada para o Adaptive Forms](custom-submit-action-form.md).
1. Selecione o nome da Ação de envio personalizada na lista suspensa **[!UICONTROL Enviar ação]** nas propriedades **[!UICONTROL Enviar]** de um formulário adaptável.
1. Toque em **[!UICONTROL Enviar]**. O CAPTCHA é validado com base nas condições definidas na API `ValidateCAPTCHA` da Ação de envio personalizada.

**Opção 2: Use  [!DNL Experience Manager Forms] ValidateCAPTCHA API para validar CAPTCHA em uma ação do usuário antes de enviar o formulário**

Você também pode invocar a API `ValidateCAPTCHA` aplicando regras em um componente em um Formulário adaptável.

Por exemplo, você adiciona um botão **[!UICONTROL Validar CAPTCHA]** em um Formulário adaptável e cria uma regra para invocar um serviço ao clicar em um botão.

A figura a seguir ilustra como chamar um serviço ao clicar em um botão **[!UICONTROL Validar CAPTCHA]**:

![Validar CAPTCHA](assets/captcha-validation1.gif)

Você pode chamar o servlet personalizado que inclui a API `ValidateCAPTCHA` usando o editor de regras e ativar ou desativar o botão Enviar do Formulário adaptável com base no resultado da validação.

Da mesma forma, é possível usar o editor de regras para incluir um método personalizado para validar CAPTCHA em um formulário adaptável.

### Adicionar serviços CAPTCHA personalizados {#add-custom-captcha-service}

[!DNL Experience Manager Forms] O fornece reCAPTCHA como o serviço CAPTCHA. No entanto, você pode adicionar um serviço personalizado para exibir na lista suspensa **[!UICONTROL CAPTCHA Service]**.

Veja a seguir uma amostra da implementação da interface para adicionar um serviço CAPTCHA adicional ao Formulário adaptável:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` refere-se ao caminho do recurso do componente CAPTCHA no repositório Sling. Use essa propriedade para incluir detalhes específicos do componente CAPTCHA. Por exemplo, `captchaPropertyNodePath` inclui informações para a configuração da nuvem reCAPTCHA configurada no componente CAPTCHA. As informações de configuração da nuvem fornecem **[!UICONTROL Chave do Site]** e **[!UICONTROL Chave Secreta]** definições para implementar o serviço reCAPTCHA.

`userResponseToken` refere-se ao  `g_recaptcha_response` que é gerado após solucionar um CAPTCHA em um formulário.
