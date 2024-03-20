---
title: Configurar uma conta de alias da empresa no Dynamic Media
description: Saiba como configurar uma conta alias de empresa no Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Sobre a configuração de uma conta empresarial alternativa do Dynamic Media {#about-dm-alias-acct}

Os URLs do Dynamic Media e o código de inserção do visualizador contêm o nome da conta da empresa. Esse nome de conta foi criado no momento do provisionamento do Dynamic Media. Pode haver cenários em que sua empresa tenha passado por uma aquisição ou reformulação da marca, ou em que você deseje simplesmente usar um nome mais fácil de memorizar. Nesses cenários, não é fácil atualizar manualmente o nome da conta da empresa em todos os URLs e o código de inserção do visualizador que aparece imediatamente. Além disso, há a possibilidade de que você afete seu repositório existente do Dynamic Media ou o conteúdo ativo. Para resolver esse problema, você pode configurar uma conta alias de empresa da Dynamic Media.

Uma conta alias de empresa da Dynamic Media garante que todos os URLs do Dynamic Media prontos para uso e o código de inserção do visualizador na interface do usuário reflitam todas as atualizações feitas no contexto comercial, como a reformulação da marca. Uma conta alias também tem um impacto positivo na SEO (Otimização do mecanismo de pesquisa), pois os URLs do Dynamic Media e o código de inserção do visualizador refletem o novo nome de conta da empresa.

Ao configurar um alias de conta de empresa da Dynamic Media, esteja ciente do seguinte:

* Qualquer URL ou código incorporado existente do visualizador do Dynamic Media na *live* as propriedades digitais devem ser atualizadas manualmente para refletir o novo nome de alias. No entanto, todos os URLs ou visualizadores incorporados ao código com o nome original da empresa do Dynamic Media continuam a funcionar para ativos existentes ou novos.
* O recurso de conta alias da empresa do Dynamic Media é limitado ao modo de criação e entrega do Experience Manager Assets. O alias da empresa não funciona com o Experience Manager Sites. Os componentes do WCM (Web Content Management, gerenciamento de conteúdo da Web) não são atualizados para essa alteração. Esses componentes continuam a funcionar com o nome original da empresa da Dynamic Media para buscar ativos da Dynamic Media.
* Você pode configurar apenas uma conta de alias da empresa no **[!UICONTROL Editar configuração do Dynamic Media]** página. No entanto, você pode criar quantas contas de alias de empresa desejar por meio de um caso de suporte e refletir manualmente o nome do alias necessário nos URLs do Dynamic Media ou no código de inserção do visualizador.
* O pacote pronto para uso [Invalidação de cache](/help/assets/invalidate-cdn-cache-dynamic-media.md) O recurso do Dynamic Media invalida os URLs com contas de Alias de empresa e de empresa configuradas na página Configuração do Dynamic Media no Cloud Service.
* Ao configurar um alias de conta de empresa no **[!UICONTROL Editar configuração do Dynamic Media]** página, para que a invalidação do cache seja bem-sucedida, você deve invalidar URLs para *ambos* o **[!UICONTROL Empresa]** e a **[!UICONTROL Alias da empresa]** conta, simultaneamente.

Consulte também [Criar uma configuração do Dynamic Media no Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configurar uma conta de alias da empresa no Dynamic Media {#configure-dm-alias-account}

Você começa a configurar uma conta alias da empresa do Dynamic Media enviando primeiro um caso de suporte. Esta etapa é obrigatória.

1. [Use o Admin Console para criar um caso de suporte](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html?lang=pt-BR).
1. Forneça as seguintes informações no seu caso de suporte:

   * O alias da empresa do Dynamic Media que você deseja usar. O nome deve conter *somente* letras (maiúsculas e minúsculas mistas permitidas), números, hifens e sublinhados.
   * Sua região.
   * Se algum [conjuntos de regras](/help/assets/using-rulesets-to-transform-urls.md) estão sendo usados anteriormente para veicular conteúdo do Dynamic Media por meio de um nome de conta de empresa alternativo da Dynamic Media.

1. Depois que a conta alias do Dynamic Media for criada pelo suporte, na instância do autor as a Cloud Service do Experience Manager, selecione o logotipo as a Cloud Service do Experience Manager para acessar o console de navegação global.
1. À esquerda do console, selecione o ícone Ferramentas e vá para **[!UICONTROL Cloud Service > Configuração do Dynamic Media]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]** (não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**). Em seguida, selecione **[!UICONTROL Editar]**.

   ![Campo de texto Alias da empresa do Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. No **[!UICONTROL Editar configuração do Dynamic Media]** página, no campo **[!UICONTROL Alias da empresa]** campo de texto, digite o nome da conta alias Dynamic Media que você especificou anteriormente no caso de suporte.
1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.
A conta alias da empresa do Dynamic Media agora é salva e ativada; todos os URLs e códigos incorporados do visualizador para ativos existentes e novos agora refletem o novo nome alias da empresa.
