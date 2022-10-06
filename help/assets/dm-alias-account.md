---
title: Configurar uma conta de alias de empresa do Dynamic Media
description: Saiba como configurar uma conta de alias da empresa no Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Sobre a configuração de uma conta de alias de empresa do Dynamic Media {#about-dm-alias-acct}

Os URLs do Dynamic Media e o código de inserção do visualizador contêm o nome da conta da empresa. Esse nome de conta foi criado no momento do provisionamento da Dynamic Media. Pode haver cenários em que sua empresa tenha sido submetida a uma aquisição ou a uma reformulação da marca, ou você queira simplesmente usar um nome mais memorável. Nesses cenários, não é fácil atualizar manualmente o nome da conta da empresa em todos os URLs e código incorporado do visualizador que sai da caixa. Além disso, há a possibilidade de que você possa afetar seu repositório Dynamic Media existente ou afetar o conteúdo ao vivo. Para resolver esse problema, você pode configurar uma conta de alias de empresa do Dynamic Media.

Uma conta de alias de empresa do Dynamic Media garante que todos os URLs do Dynamic Media e código de inserção do visualizador prontos para uso na interface do usuário reflitam as atualizações feitas no contexto comercial, como a reformulação da marca. Uma conta de alias também tem um impacto positivo em sua SEO (Otimização do mecanismo de pesquisa) porque os URLs do Dynamic Media e o código de incorporação do visualizador refletem o novo nome da conta da empresa.

Ao configurar uma conta de alias de empresa do Dynamic Media, esteja ciente do seguinte:

* Quaisquer URLs do Dynamic Media ou código incorporado do visualizador em seu *live* as propriedades digitais devem ser atualizadas manualmente para refletir o novo nome do alias. No entanto, quaisquer URLs ou códigos de inserção de visualizadores com o nome original da empresa Dynamic Media continuam a funcionar para ativos existentes ou novos.
* O recurso de conta de alias da empresa do Dynamic Media está limitado ao modo de criação e ao delivery do Experience Manager Assets. O nome do alias da empresa não funciona com o Experience Manager Sites. Os componentes do WCM (Gerenciamento de conteúdo da Web) não são atualizados para essa alteração. Esses componentes continuam a funcionar com o nome original da empresa da Dynamic Media para buscar ativos da Dynamic Media.
* Você pode configurar apenas uma conta de alias da empresa no **[!UICONTROL Editar configuração do Dynamic Media]** página. No entanto, é possível criar quantas contas de alias da empresa por meio de um caso de suporte e refletir manualmente o nome do alias necessário nos URLs do Dynamic Media ou no código incorporado do visualizador.
* O pronto para uso [Invalidação de cache](/help/assets/invalidate-cdn-cache-dynamic-media.md) O recurso do Dynamic Media invalida os URLs com as contas Alias da empresa e da empresa configuradas na página Configuração do Dynamic Media no Cloud Services.
* Ao configurar uma conta de alias da empresa no **[!UICONTROL Editar configuração do Dynamic Media]** para que a invalidação do cache seja bem-sucedida, você deve invalidar URLs para *both* o **[!UICONTROL Empresa]** e a **[!UICONTROL Alias da Empresa]** , simultaneamente.

Consulte também [Criar uma configuração do Dynamic Media no Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configurar uma conta de alias de empresa do Dynamic Media {#configure-dm-alias-account}

Você começa a configurar uma conta de alias de empresa do Dynamic Media enviando primeiro um caso de suporte. Esta etapa é necessária.

1. [Use o Admin Console para criar um caso de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
1. Forneça as seguintes informações no caso de suporte:

   * O nome do alias da empresa do Dynamic Media que você deseja usar. O nome deve conter *only* letras (mistura de maiúsculas e minúsculas permitida), números, hifens e sublinhados.
   * Sua região.
   * Se houver [conjuntos de regras](/help/assets/using-rulesets-to-transform-urls.md) estão sendo usados anteriormente para obter a veiculação de conteúdo do Dynamic Media por meio de um nome de conta de empresa alternativo do Dynamic Media.

1. Depois que a conta de alias do Dynamic Media for criada pelo Suporte, na instância do autor as a Cloud Service do Experience Manager, selecione o logotipo do Experience Manager as a Cloud Service para acessar o console de navegação global.
1. À esquerda do console, selecione o ícone Ferramentas e vá para **[!UICONTROL Cloud Services > Configuração do Dynamic Media]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]** (não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**). Em seguida, selecione **[!UICONTROL Editar]**.

   ![Campo de texto Alias da empresa do Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. No **[!UICONTROL Editar configuração do Dynamic Media]** na página **[!UICONTROL Alias da Empresa]** digite o nome da conta do alias do Dynamic Media que você especificou no caso de suporte anterior.
1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.
A conta de alias da empresa do Dynamic Media agora é salva e ativada; todos os URLs e o código incorporado do visualizador para ativos novos e existentes agora refletem o novo nome do alias da empresa.
