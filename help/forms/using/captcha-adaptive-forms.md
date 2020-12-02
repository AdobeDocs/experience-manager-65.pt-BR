---
title: Uso do CAPTCHA em formulários adaptáveis
seo-title: Uso do CAPTCHA em formulários adaptáveis
description: Saiba como configurar AEM CAPTCHA ou o serviço Google reCAPTCHA em formulários adaptáveis.
seo-description: Saiba como configurar AEM CAPTCHA ou o serviço Google reCAPTCHA em formulários adaptáveis.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# Uso de CAPTCHA em formulários adaptáveis{#using-captcha-in-adaptive-forms}

O CAPTCHA (Completamente Automated Public Turing test para distinguir computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. Ela representa um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. Impede que o usuário continue se o teste falhar e ajuda a tornar as transações on-line seguras, impedindo que bots postem spam ou fins mal-intencionados.

A AEM Forms suporta CAPTCHA em formulários adaptáveis. Você pode usar o serviço reCAPTCHA do Google para implementar CAPTCHA.

>[!NOTE]
>
>* O AEM Forms suporta apenas reCaptcha v2. Nenhuma outra versão é suportada.
>* O CAPTCHA em formulários adaptáveis não é suportado no modo offline no aplicativo AEM Forms.

>



## Configurar o serviço ReCAPTCHA pelo Google {#google-recaptcha}

Os autores de formulários podem usar o serviço reCAPTCHA do Google para implementar CAPTCHA em formulários adaptáveis. Ele oferta recursos CAPTCHA avançados para proteger seu site. Para obter mais informações sobre como o reCAPTCHA funciona, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Para implementar o serviço reCAPTCHA no AEM Forms:

1. Obtenha [o par de chaves da API reCAPTCHA](https://www.google.com/recaptcha/admin) do Google. Inclui uma chave do site e um segredo.
1. Criar container de configuração para serviços em nuvem.

   1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
      * Consulte a documentação [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
   1. Faça o seguinte para ativar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.

      1. No Navegador de configuração, selecione a pasta **[!UICONTROL global]** e toque em **[!UICONTROL Propriedades]**.

      1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações de nuvem]**.
      1. Toque em **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.
   1. No Navegador de configuração, toque em **[!UICONTROL Criar]**.
   1. Na caixa de diálogo Criar configuração, especifique um título para a pasta e ative **[!UICONTROL Configurações de nuvem]**.
   1. Toque em **[!UICONTROL Criar]** para criar a pasta ativada para configurações de serviço em nuvem.


1. Configure o serviço de nuvem para reCAPTCHA.

   1. Na instância do autor AEM, vá para ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Toque em **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o container de configuração criado na etapa anterior e toque em **[!UICONTROL Criar]**.
   1. Especifique Nome, Chave do site e Chave secreta para o serviço reCAPTCHA e toque em **[!UICONTROL Criar]** para criar a configuração do serviço de nuvem.
   1. Na caixa de diálogo Editar componente, especifique o site e as chaves secretas obtidas na etapa 1. Toque em **Salvar configurações** e toque em **OK** para concluir a configuração.

   Quando o serviço reCAPTCHA estiver configurado, ele estará disponível para uso em formulários adaptáveis. Para obter mais informações, consulte [Usando CAPTCHA em formulários adaptáveis](#using-captcha).

## Use CAPTCHA em formulários adaptáveis {#using-captcha}

Para usar CAPTCHA em formulários adaptáveis:

1. Abra um formulário adaptável no modo de edição.

   >[!NOTE]
   >
   >Certifique-se de que o container de configuração selecionado ao criar o formulário adaptável contenha o serviço em nuvem reCAPTCHA. Também é possível editar as propriedades do formulário adaptável para alterar o container de configuração associado ao formulário.

1. No navegador de componentes, arraste e solte o componente **Captcha** no formulário adaptável.

   >[!NOTE]
   >
   >Não há suporte para o uso de mais de um componente Captcha em um formulário adaptável. Além disso, não é recomendado usar CAPTCHA em um painel marcado para carregamento lento ou em um fragmento.

   >[!NOTE]
   >
   >O Captcha faz distinção de tempo e expira em cerca de um minuto. Portanto, é recomendável colocar o componente Captcha logo antes do botão Enviar no formulário adaptável.

1. Selecione o componente Captcha adicionado e toque em ![cmppr](assets/cmppr.png) para editar suas propriedades.
1. Especifique um título para o widget CAPTCHA. O valor padrão é **Captcha**. Selecione **Ocultar título** se não quiser que o título apareça.
1. No menu suspenso **Captcha service**, selecione **reCaptcha** para ativar o serviço reCAPTCHA se você o configurou conforme descrito em [ReCAPTCHA service do Google](#google-recaptcha). Selecione uma configuração no menu suspenso Configurações. Além disso, selecione o tamanho como **Normal** ou **Compacto** para o widget reCAPTCHA.

   >[!NOTE]
   >
   >Não selecione **[!UICONTROL Padrão]** no menu suspenso do serviço Captcha, pois o serviço AEM CAPTCHA padrão está obsoleto.

1. Salve as propriedades.

O serviço reCAPTCHA está ativado no formulário adaptável. Você pode pré-visualização o formulário e ver o CAPTCHA funcionando.
