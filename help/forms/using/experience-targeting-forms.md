---
title: Criar experiências direcionadas no AEM Forms
seo-title: Create targeted experiences in AEM Forms
description: Use o Target no AEM Forms para criar experiências personalizadas para clientes direcionados.
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Criar experiências direcionadas no AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrar o Adobe Target com o AEM Forms {#integrate-adobe-target-with-aem-forms}

O Adobe Target integrado ao AEM permite criar experiências personalizadas para um público-alvo. Com o Adobe Target, você pode criar testes A/B, medir a resposta do usuário e gerar conteúdo personalizado da Web para usuários direcionados. É possível integrar o Adobe Target com o AEM Forms para direcionar componentes de imagem de formulários adaptáveis e comunicações interativas.

Configure o Adobe Target no AEM para usá-lo com formulários adaptáveis e comunicações interativas, consulte [Criação de uma configuração do Target no AEM](/help/sites-administering/target.md) e [Adicionar uma estrutura](/help/sites-administering/target.md).

>[!NOTE]
>
>O direcionamento funciona quando o formulário adaptável ou a comunicação interativa é renderizada usando um nome de host ou endereço IP. Falha quando o formulário adaptável ou a comunicação interativa é renderizada usando o localhost.

## Criação de uma atividade do Target {#creating-a-target-activity}

1. Selecionar **Adobe Experience Manager > Personalização > Atividades**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. Na página Atividades, selecione **Criar > Criar marca**.
1. Você deverá escolher um modelo e inserir as propriedades.

   Selecione um modelo, selecione **Próximo.** Insira o título da marca na seção Propriedades e selecione **Criar.**
Sua marca agora está listada na página Atividades.

1. Selecione sua marca na página Atividades.
1. Na Área principal da sua marca, selecione **Criar** > **Criar atividade**.

   Ao criar uma atividade, especifique seus detalhes, o público-alvo e as configurações.

   A seção Detalhes inclui nome, mecanismo de direcionamento e objetivo. Ao selecionar o Adobe Target como mecanismo de direcionamento, você ativa a opção Configuração da nuvem do Target. Escolha a configuração da nuvem do Target, o tipo de atividade, forneça o objetivo da atividade e selecione **Próxima**. A comunicação interativa suporta somente o tipo de atividade de direcionamento de experiência.

   A seção Target permite adicionar a experiência de público-alvo e nomeá-la. Clique em **Adicionar experiência** para habilitar o **Selecionar público-alvo** e **Nomear experiência** opções. Selecionar **Selecionar público-alvo** para ver uma lista de públicos-alvo e sua origem. Selecione um público-alvo na lista Nome do público-alvo. Selecionar **Adicionar experiência** para nomear a experiência e selecione **Próxima**.

   A seção Metas e configurações permite agendar e priorizar sua atividade. Defina a data de início, a data de término e a prioridade da atividade, a métrica de meta, a métrica adicional e selecione **Salvar**.

   A atividade agora está listada na página da sua marca.

   >[!NOTE]
   >
   >Você pode ignorar o erro &quot;Sua atividade foi salva, mas não foi sincronizada com o Target. Motivo: a seguinte experiência não tem ofertas&quot;, se encontrada ao salvar a atividade.

1. Para ativar o destino, edite o arquivo .jsp para incluir as bibliotecas de clientes que seu modelo de formulários adaptáveis usa.

   Por exemplo, na implementação pronta para uso, clique em **Ferramentas** >  **CRXDE Lite**.

   Na barra de endereços do CRXDE Lite, digite /libs/fd/af/components/page/base/head.jsp para editar o arquivo head.jsp.

   Esta implementação usa o template simpleEnrollment. Nesta implementação, modifique o arquivo head.jsp para incluir as seguintes bibliotecas de clientes:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Para habilitar a estrutura de destino para formulários adaptáveis, navegue até o formulário ou a comunicação interativa e abra-a no modo de edição.

   Para abrir um formulário ou comunicação interativa no modo de edição, selecione **Selecionar** e selecione **Abertura**.

   Como alternativa, quatro botões são exibidos quando você move o ponteiro sobre o formulário ou o ícone de comunicação interativa sem selecioná-lo. É possível selecionar a variável **Editar** que aparece, para abrir o formulário no modo de edição.

1. Na barra de ferramentas da página, selecione **Informações da página** ![theme-options](assets/theme-options.png) > **Abrir propriedades**.
1. Na guia General, escolha uma configuração para o **Adobe Target** campo. Selecionar **Salvar e fechar**.

## Aplicação da atividade criada a uma imagem de formulário adaptável ou a uma imagem de comunicação interativa {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Abra o formulário adaptável e a comunicação interativa para edição. Se você estiver abrindo uma comunicação interativa, abra o Canal da Web.

1. No modo de criação de sua comunicação interativa ou formulário adaptável, adicione uma imagem a ser direcionada.

   >[!NOTE]
   >
   >O AEM Forms oferece suporte somente para direcionamento de componentes de imagem. Verifique se o painel que hospeda o componente de imagem não contém nenhum outro componente e se o número de colunas do painel está definido como 1.

1. Alternar de **Editar** para **Direcionamento** modo. A opção para alternar modos está próxima ao canto superior direito.
1. Selecione um **MARCA**, selecione **ATIVIDADE** e selecione **Iniciar o direcionamento**. A variável **Públicos-alvo** é exibido no lado direito do editor.

   ![menu de direcionamento](assets/targeting-menu.png)

1. Selecione um público-alvo na **Públicos-alvo** e selecione a imagem a ser direcionada. Um menu é exibido. No menu, selecione **Target**. Selecione a imagem e **Configurar**. Na janela de propriedades, selecione a imagem a ser exibida para o público-alvo selecionado. Repita a etapa para todos os públicos-alvo. O direcionamento da experiência é habilitado para a imagem na comunicação interativa ou no formulário adaptável.

## Verifique se a atividade criada é sincronizada com o servidor do Target {#check-if-the-created-activity-syncs-with-the-target-server}

Uma atividade usada para direcionar sincronizações com o servidor Target. Para verificar se a atividade está sincronizada com o servidor de destino, verifique o status da atividade na página da marca.

Verifique se o status da atividade é Sincronizado.

## Validar comportamento do Target {#validate-target-behavior}

Para validar o comportamento do Target:

* Usar o direcionamento com `wcmmode preview` no modo autor
* Usar o direcionamento com `wcmmode preview` e `wcmmode disabled` no modo de publicação

## Monitorar o direcionamento do componente de imagem {#monitor-targeting-for-the-image-component}

Para monitorar o direcionamento de componentes de imagem em seu formulário, publique imagens, atividades e formulário adaptável.

## Problemas em aberto {#open-issues}

Expressão de visibilidade, falha ao definir foco para imagens direcionadas em formulários adaptáveis.
