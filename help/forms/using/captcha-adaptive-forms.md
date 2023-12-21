---
title: Uso de CAPTCHA em formulários adaptáveis
description: Saiba como configurar o serviço AEM CAPTCHA ou Google reCAPTCHA em formulários adaptáveis.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 5%

---

# Uso de CAPTCHA em formulários adaptáveis{#using-captcha-in-adaptive-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/captcha-adaptive-forms.html) |
| AEM 6.5 | Este artigo |


<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

O CAPTCHA (um teste de Turing público e completamente automatizado para diferenciar computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. O recurso apresenta um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. O CAPTCHA impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que bots publiquem spam ou outro conteúdo mal-intencionado.

O AEM Forms oferece suporte a CAPTCHA em formulários adaptáveis. Você pode usar o serviço reCAPTCHA pelo Google para implementar o CAPTCHA.

>[!NOTE]
>
>* O AEM Forms oferece suporte ao reCAPTCHA v2 e Enterprise. Nenhuma outra versão é compatível.
>* CAPTCHA em formulários adaptáveis não é compatível no modo offline no aplicativo AEM Forms.

## Configurar o serviço reCAPTCHA pelo Google para o Adaptive Forms {#google-reCAPTCHA}

Os usuários do AEM Forms podem usar o serviço reCAPTCHA pelo Google para implementar o CAPTCHA em formulários adaptáveis. Ele oferece recursos avançados de CAPTCHA para proteger o site. Para obter mais informações sobre como o reCAPTCHA funciona, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/). O serviço reCAPTCHA, incluindo o reCAPTCHA v2 e o reCAPTCHA Enterprise, está integrado ao AEM Forms. Com base em seu requisito, você pode configurar o serviço reCAPTCHA para habilitar:

* [reCAPTCHA Enterprise no AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 no AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### Configurar o reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Criar um [Projeto reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) habilitado com [API corporativa do reCAPTCHA](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. [Obter](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) a ID do projeto.
1. Criar um [Chave de API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e uma [chave do site para sites](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Criar contêiner de configuração para serviços em nuvem.

   1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**. Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
   1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.
      1. No Navegador de configuração, selecione a variável **[!UICONTROL global]** e selecione **[!UICONTROL Propriedades]**.
      1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações da nuvem]**.
      1. Selecionar **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

   1. No Navegador de configuração, selecione **[!UICONTROL Criar]**.
   1. Na caixa de diálogo Criar configuração, especifique um título para a pasta e habilite **[!UICONTROL Configurações da nuvem]**.
   1. Selecionar **[!UICONTROL Criar]** para criar a pasta habilitada para configurações do cloud service.
1. Configure o serviço de nuvem para o reCAPTCHA Enterprise.

   1. Na instância do autor do Experience Manager, acesse ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**.
   1. Selecionar **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o container de configuração criado na etapa anterior e selecione **[!UICONTROL Criar]**.
   1. Selecione a versão como reCAPTCHA Enterprise e especifique o Nome; ID do Projeto, Chave do Site e Chave de API (Obtido nas Etapas 2 e 3) para o serviço reCAPTCHA Enterprise.
   1. Selecione o tipo de chave. O tipo de chave deve ser o mesmo que a chave do site configurada no projeto na nuvem do Google, por exemplo, **Chave do site da caixa de seleção** ou **Chave do site com base em pontuação**.
   1. Especifique uma pontuação de limite no intervalo de 0 a 1 ([Clique para saber mais sobre pontuação](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)). Pontuações maiores ou iguais às pontuações de limite identificam a interação humana, caso contrário, são consideradas interação de bot.

      > Observação:
      >
      > * Os autores do formulário podem especificar uma pontuação no intervalo adequado para o envio ininterrupto do formulário.

   1. Selecionar **[!UICONTROL Criar]** para criar a configuração do cloud service.

   1. Na caixa de diálogo Editar componente, especifique o nome, a ID do projeto, a chave do site, a chave de API (obtida nas etapas 2 e 3), selecione o tipo de chave e insira a pontuação de limite. Selecionar **[!UICONTROL Salvar configurações]** e selecione **[!UICONTROL OK]** para concluir a configuração.

Quando o serviço reCAPTCHA Enterprise estiver ativado, ele estará disponível para uso em formulários adaptáveis. Consulte [uso de CAPTCHA em formulários adaptáveis](#using-reCAPTCHA).

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### Configurar o Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Obter [Par de chaves da API do reCAPTCHA](https://www.google.com/recaptcha/admin) do Google. Inclui uma **chave do site** e uma **chave secreta**.
1. Criar contêiner de configuração para serviços em nuvem.
   1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**. Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
   1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.

      1. No Navegador de configuração, selecione a variável **[!UICONTROL global]** e selecione **[!UICONTROL Propriedades]**.

      1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações da nuvem]**.
      1. Selecionar **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

   1. No Navegador de configuração, selecione **[!UICONTROL Criar]**.
   1. Na caixa de diálogo Criar configuração, especifique um título para a pasta e habilite **[!UICONTROL Configurações da nuvem]**.
   1. Selecionar **[!UICONTROL Criar]** para criar a pasta habilitada para configurações do cloud service.

1. Configure o serviço de nuvem para o reCAPTCHA v2.

   1. Na instância do autor do AEM, acesse ![tools-1](assets/tools-1.png) > **Cloud Service**.
   1. Selecionar **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o container de configuração criado na etapa anterior e selecione **[!UICONTROL Criar]**.
   1. Selecione versão como reCAPTCHA v2, especifique Nome; Chave do site e Chave secreta para o serviço reCAPTCHA (Obtido na Etapa 1) e selecione **[!UICONTROL Criar]** para criar a configuração do cloud service.
   1. Na caixa de diálogo Editar componente, especifique o site e as chaves secretas obtidas na etapa 1. Selecionar **[!UICONTROL Salvar configurações]** e selecione **OK** para concluir a configuração.

   Depois que o serviço reCAPTCHA é configurado, ele é disponibilizado para uso em formulários adaptáveis. Para obter mais informações, consulte [uso de CAPTCHA em formulários adaptáveis](#using-captcha).

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## Usar reCAPTCHA em formulários adaptáveis {#using-reCAPTCHA}

Para usar o reCAPTCHA em formulários adaptáveis:

1. Abra um formulário adaptável no modo de edição.

   >[!NOTE]
   >
   >Verifique se o contêiner de configuração selecionado ao criar o formulário adaptável contém o serviço de nuvem reCAPTCHA. Também é possível editar propriedades do formulário adaptável para alterar o contêiner de configuração associado ao formulário.

1. No navegador de componentes, arraste e solte a **Captcha** no formulário adaptável.

   >[!NOTE]
   >
   >Não há suporte para o uso de mais de um componente Captcha em um formulário adaptável. Além disso, não é recomendável usar CAPTCHA em um painel marcado para carregamento lento ou em um fragmento.

   >[!NOTE]
   >
   >O Captcha é sensível ao tempo e expira em cerca de um minuto. Portanto, é recomendável colocar o componente Captcha antes do botão Enviar no formulário adaptável.

1. Selecione o componente Captcha adicionado e selecione ![cmppr](assets/cmppr.png) para editar suas propriedades.
1. Especifique um título para o widget CAPTCHA. O valor padrão é **Captcha**. Selecionar **Ocultar título** se não quiser que o título seja exibido.
1. No **Serviço de captcha** selecione **reCAPTCHA** para ativar o serviço reCAPTCHA se você o tiver configurado conforme descrito em [Serviço reCAPTCHA da Google](#google-reCAPTCHA).
1. Selecione uma configuração na lista suspensa Configurações.
1. **Se a configuração selecionada tiver a versão reCAPTCHA Enterprise**:
   1. Você pode selecionar a configuração de nuvem do reCAPTCHA com **tipo de chave** as **caixa de seleção**. Na chave da caixa de seleção, digite a mensagem de erro personalizada que será exibida como uma mensagem em linha se a validação de captcha falhar. Você pode selecionar o tamanho como **[!UICONTROL Normal]** e **[!UICONTROL Compacto]**.
   1. Você pode selecionar a configuração de nuvem do reCAPTCHA com **tipo de chave** as **baseado em pontuação**. Na chave baseada em pontuação, digite a mensagem de erro personalizada que será exibida como uma mensagem pop-up se a validação de captcha falhar.
   1. Quando você seleciona um **[!UICONTROL Referência de vinculação]** os dados enviados são dados vinculados, caso contrário, são dados desvinculados. Abaixo estão exemplos XML de dados não vinculados e dados vinculados (com referência de vinculação como SSN), respectivamente, quando um formulário é enviado.

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **Se a configuração selecionada tiver a versão reCAPTCHA v2**:
   1. Selecione o tamanho como **[!UICONTROL Normal]** ou **[!UICONTROL Compacto]** para o widget reCAPTCHA. Você também pode selecionar a variável **[!UICONTROL Invisível]** opção para mostrar o desafio de CAPTCHA somente em caso de atividade suspeita. A variável **protegido pelo reCAPTCHA** exibido abaixo, é exibido nos formulários protegidos.

      ![Google protegido pelo selo reCAPTCHA](/help/forms/using/assets/google-recaptcha-v2.png)


   O serviço reCAPTCHA é ativado no formulário adaptável. Você pode visualizar o formulário e ver o CAPTCHA funcionando.

1. Salve as propriedades.

>[!NOTE]
> 
> Não selecionar **[!UICONTROL Padrão]** no menu suspenso do serviço Captcha, quando o serviço AEM CAPTCHA padrão é descontinuado.

### Mostrar ou ocultar o componente CAPTCHA com base em regras {#show-hide-captcha}

É possível optar por mostrar ou ocultar o componente CAPTCHA com base nas regras aplicadas em um componente de um Formulário adaptável. Selecione o componente e ![editar regras](assets/edit-rules-icon.svg)e selecione **[!UICONTROL Criar]** para criar uma regra. Para obter mais informações sobre como criar regras, consulte [Editor de regras](rule-editor.md).

Por exemplo, o componente CAPTCHA deve ser exibido em um formulário adaptável somente se o campo Valor da moeda no formulário tiver um valor maior que 25000.

Selecione o **[!UICONTROL Valor da moeda]** no formulário e crie as seguintes regras:

![Mostrar ou ocultar regras](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * Se você selecionar a configuração reCAPTCHA v2 com tamanho como **[!UICONTROL Invisível]** ou reCAPTCHA Enterprise score based keys, então a opção mostrar/ocultar não é aplicável.

### Validar CAPTCHA {#validate-captcha}

É possível validar CAPTCHA em um Formulário adaptável ao enviar o formulário ou basear a validação CAPTCHA em ações e condições do usuário.

#### Validar CAPTCHA no envio do formulário {#validation-form-submission}

Para validar um CAPTCHA automaticamente ao enviar um Formulário adaptável:

1. Selecione o componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para visualizar as propriedades do componente.
1. No **[!UICONTROL Validar CAPTCHA]** , selecione **[!UICONTROL Validar CAPTCHA no envio do formulário]**.
1. Selecionar ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

#### Validar CAPTCHA em ações e condições do usuário {#validate-captcha-user-action}

Para validar um CAPTCHA com base nas condições e ações do usuário:

1. Selecione o componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para visualizar as propriedades do componente.
1. No **[!UICONTROL Validar CAPTCHA]** , selecione **[!UICONTROL Validar CAPTCHA em uma ação do usuário]**.
1. Selecionar ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

   >[!NOTE]
   >
   >
   > Se você selecionar a configuração reCAPTCHA v2 com tamanho como **[!UICONTROL Invisível]** ou reCAPTCHA Enterprise score based keys, então o Captcha Válido em uma ação do usuário não é aplicável.

[!DNL Experience Manager Forms] fornece `ValidateCAPTCHA` API para validar CAPTCHA usando condições predefinidas. Você pode chamar a API usando uma Ação enviar personalizada ou definindo regras em componentes em um Formulário adaptável.

Veja a seguir um exemplo de `ValidateCAPTCHA` API para validar CAPTCHA usando condições predefinidas:

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

O exemplo significa que a variável `ValidateCAPTCHA` A API valida o CAPTCHA no formulário somente se o número de dígitos na caixa numérica especificada pelo usuário durante o preenchimento do formulário for maior que 5.

**Opção 1: uso [!DNL Experience Manager Forms] Validar a API CAPTCHA para validar CAPTCHA usando uma ação enviar personalizada**

Execute as seguintes etapas para usar o `ValidateCAPTCHA` API para validar CAPTCHA usando uma Ação enviar personalizada:

1. Adicione o script que inclui a variável `ValidateCAPTCHA` API para ação enviar personalizada. Para obter mais informações sobre ações enviar personalizadas, consulte [Criar uma ação enviar personalizada para o Forms adaptável](custom-submit-action-form.md).
1. Selecione o nome da Ação de envio personalizada na **[!UICONTROL Ação de envio]** lista suspensa no **[!UICONTROL Envio]** propriedades de um Formulário adaptável.
1. Selecionar **[!UICONTROL Enviar]**. O CAPTCHA é validado com base nas condições definidas no `ValidateCAPTCHA` API da Ação de envio personalizada.

**Opção 2: uso [!DNL Experience Manager Forms] Validar API CAPTCHA para validar CAPTCHA em uma ação do usuário antes de enviar o formulário**

Você também pode invocar `ValidateCAPTCHA` ao aplicar regras em um componente em um Formulário adaptável.

Por exemplo, você adiciona um **[!UICONTROL Validar CAPTCHA]** em um Formulário adaptável e crie uma regra para chamar um serviço com o clique de um botão.

A figura a seguir ilustra como você pode chamar um serviço com um clique de **[!UICONTROL Validar CAPTCHA]** botão:

![Validar CAPTCHA](assets/captcha-validation1.gif)

Você pode chamar o servlet personalizado que inclui `ValidateCAPTCHA` API usando o editor de regras e ativar ou desativar o botão enviar do Formulário adaptável com base no resultado da validação.

Da mesma forma, você pode usar o editor de regras para incluir um método personalizado para validar CAPTCHA em um Formulário adaptável.

<!--
### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

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

`captchaPropertyNodePath` Refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` Refers to the `g_reCAPTCHA_response` that gets generated after solving a CAPTCHA in a form. -->
