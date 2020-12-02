---
title: Criar experiências direcionadas no AEM Forms
seo-title: Criar experiências direcionadas no AEM Forms
description: Use o Público alvo no AEM Forms para criar experiências personalizadas para clientes direcionados.
seo-description: Use o Público alvo no AEM Forms para criar experiências personalizadas para clientes direcionados.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# Criar experiências direcionadas no AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrar o Adobe Target ao AEM Forms {#integrate-adobe-target-with-aem-forms}

A Adobe Target integrada ao AEM permite criar experiências personalizadas para uma audiência de público alvo. Com a Adobe Target, você pode criar testes A/B, medir a resposta do usuário e gerar conteúdo da Web personalizado para usuários direcionados. Você pode integrar o Adobe Target com o AEM Forms aos componentes de imagem do público alvo de formulários adaptáveis e comunicações interativas.

Configure a Adobe Target no AEM para usá-la com formulários adaptativos e comunicações interativas, consulte [Criando uma Configuração de Público alvo em AEM](/help/sites-administering/target.md) e [Adicionar uma Estrutura](/help/sites-administering/target.md).

>[!NOTE]
>
>A definição de metas funciona quando o formulário adaptável ou a comunicação interativa é renderizada usando um nome de host ou endereço IP. Ele falha quando seu formulário adaptável ou comunicação interativa é renderizada usando o host local.

## Criando uma Atividade de Público alvo {#creating-a-target-activity}

1. Toque em **Adobe Experience Manager > Personalização > Atividade**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. Na página Atividade, toque em **Criar > Criar marca**.
1. Você será solicitado a escolher um modelo e inserir propriedades.

   Selecione um modelo e toque em **Próximo.** Digite o título da sua marca na seção Propriedades e toque em  **Criar.**
Sua marca agora está listada na página Atividade.

1. Toque em sua marca na página Atividade.
1. Na área Principal da sua marca, toque em **Criar** > **Criar Atividade**.

   Ao criar uma atividade, especifique seus detalhes, público alvo e configurações.

   A seção Detalhes inclui nome, mecanismo de definição de metas e objetivo. Quando você seleciona Adobe Target como o mecanismo de definição de metas, a opção de configuração da nuvem de Públicos alvos é ativada. Escolha a configuração da nuvem do Público alvo, escolha o tipo de Atividade, forneça o objetivo da atividade e toque em **Próximo**. O Interative Communication suporta apenas o tipo de Atividade de direcionamento de experiência.

   A seção Público alvo permite que você adicione experiência de audiência e nomeie-a. Clique em **Adicionar experiência** para ativar as opções **Selecionar Audiência** e **Nomear experiência**. Toque em **Selecione Audiência** para ver uma lista de audiências e sua origem. Selecione uma audiência na lista Nome da Audiência. Toque em **Adicionar experiência** para nomear a experiência e toque em **Próximo**.

   A seção Metas e configurações permite que você agende e priorize sua atividade. Defina a data do start, a data de término e a prioridade da atividade, a métrica de objetivo, a métrica adicional e toque em **Salvar**.

   A atividade agora está listada em sua página de marca.

   >[!NOTE]
   >
   >Você pode ignorar o erro &quot;Sua atividade foi salva, mas não foi sincronizada ao Público alvo. Motivo: A seguinte experiência não tem ofertas&quot;, se for encontrada ao salvar a atividade.

1. Para habilitar o público alvo, edite o arquivo .jsp para incluir bibliotecas de clientes que seu modelo de formulários adaptáveis usa.

   Por exemplo, na implementação predefinida, clique em **Ferramentas** > **CRXDE Lite**.

   Na barra de endereços CRXDE Lite, digite /libs/fd/af/components/page/base/head.jsp para editar o arquivo head.jsp.

   Essa implementação usa o modelo simpleEnrollment. Nesta implementação, modifique o arquivo head.jsp para incluir as seguintes bibliotecas de clientes:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Para ativar a estrutura de públicos alvos para formulários adaptáveis, navegue até o formulário ou comunicação interativa e abra-a no modo de edição.

   Para abrir um formulário ou uma comunicação interativa no modo de edição, toque em **Selecionar** e, em seguida, toque em **Abrir**.

   Como alternativa, quatro botões são exibidos quando você move o ponteiro sobre o formulário ou ícone de comunicação interativa sem selecioná-lo. Você pode tocar no botão **Editar** que aparece para abrir o formulário no modo de edição.

1. Na barra de ferramentas da página, toque em **Informações da página** ![opções do tema](assets/theme-options.png) > **Abrir propriedades**.
1. Na guia Geral, escolha uma configuração para o campo **Adobe Target**. Toque em **Salvar e fechar**.

## Aplicar a atividade criada a uma imagem de formulário adaptável ou a uma imagem de comunicação interativa {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Abra o formulário adaptável e a comunicação interativa para edição. Se você estiver abrindo uma comunicação interativa, abra o Canal da Web.

1. No modo de criação de sua comunicação interativa ou formulário adaptativo, adicione uma imagem para ser direcionada.

   >[!NOTE]
   >
   >A AEM Forms oferece suporte à definição de metas somente para componentes de imagem. Verifique se o painel que hospeda o componente de imagem não contém nenhum outro componente e se o número de colunas do painel está definido como 1.

1. Alterne do modo **Editar** para **Definição de metas**. A opção para alternar entre modos está próxima ao canto superior direito.
1. Selecione um **BRAND**, selecione **ATIVIDADE** e toque **Definição de metas de Start**. O menu **Audiência** é exibido no lado direito do editor.

   ![menu de definição de metas](assets/targeting-menu.png)

1. Selecione uma audiência no menu **Audiência** e toque na imagem para público alvo. Um menu é exibido. No menu, toque em **Público alvo**. Toque na imagem e toque em **Configurar**. Na janela de propriedades, selecione a imagem a ser exibida para a audiência selecionada. Repita a etapa para todas as audiências. A definição de metas de experiência está ativada para a imagem na comunicação interativa ou no formulário adaptável.

## Verifique se a atividade criada sincroniza com o servidor de Públicos alvos {#check-if-the-created-activity-syncs-with-the-target-server}

Uma atividade usada para segmentar sincronizações com o servidor do Público alvo. Para verificar se sua atividade está sincronizada com o servidor do público alvo, verifique o status da atividade na página da marca.

Verifique se o status da atividade está sincronizado.

## Validar o comportamento do Público alvo {#validate-target-behavior}

Para validar o comportamento do Público alvo:

* Usar a definição de metas com `wcmmode preview` no modo de criação
* Usar a definição de metas com `wcmmode preview` e `wcmmode disabled` no modo de publicação

## Monitore a definição de metas para o componente de imagem {#monitor-targeting-for-the-image-component}

Para monitorar o direcionamento de componentes de imagem em seu formulário, publique suas imagens, atividades e formulário adaptável.

## Problemas em aberto {#open-issues}

Expressão de visibilidade, falha ao definir foco de imagens direcionadas em formulários adaptáveis.
