---
title: Configurar o Microsoft Dynamics 365 para o fluxo de trabalho hipotecário residencial do site de referência We.Finance
seo-title: Configurar o Microsoft Dynamics 365 para o fluxo de trabalho hipotecário residencial do site de referência We.Finance
description: Saiba como aproveitar os serviços do Microsoft® Dynamics 365 através de formulários adaptáveis para o fluxo de trabalho hipotecário residencial do site de Referência do We.Finance
seo-description: Saiba como aproveitar os serviços do Microsoft® Dynamics 365 através de formulários adaptáveis para o fluxo de trabalho hipotecário residencial do site de Referência do We.Finance
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# Configurar o Microsoft Dynamics 365 para o fluxo de trabalho hipotecário residencial do site de referência We.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Saiba como aproveitar os serviços do Microsoft® Dynamics 365 através de formulários adaptáveis para o fluxo de trabalho hipotecário residencial do site de Referência do We.Finance

## Visão geral {#overview}

O Microsoft® Dynamics 365 é um software CRM (Customer Relationship Management) e ERP (Enterprise Resource Planning, gerenciamento de relacionamento com o cliente) que fornece soluções corporativas para criar e gerenciar contas, contatos, clientes potenciais, oportunidades e casos de clientes.

O AEM Forms fornece um serviço em nuvem para integrar o Dynamics 365 com o módulo [Forms Data Integration](/help/forms/using/data-integration.md) . A explicação passo a passo do aplicativo [Home Mortgage com o Microsoft® Dynamics](/help/forms/using/finance-reference-site-walkthrough.md#home-mortgage-application-walkthrough-with-microsoft-dynamics) mostra como um cliente usa o site de referência We.Finance para solicitar um empréstimo quando o site está usando o Microsoft® Dynamics for Forms Data Integration. Antes de poder usar a apresentação do aplicativo Home Mortgage com o cenário Microsoft® Dynamics, é necessário configurar o Microsoft® Dynamics 365 para ser usado com o site de referência We.Finance.

## Pré-requisitos {#prerequisites}

Antes de começar a configurar o Dynamics 365, verifique se você:

* [Configure e configure os sites](/help/forms/using/setup-reference-sites.md)de referência do AEM Forms.

* AEM 6.3 Forms Service Pack 1 e posterior
* Conta do Microsoft® Dynamics 365
* Aplicativo registrado para o serviço do Dynamics 365 com o Microsoft® Azure Ative Diretory
* ID do cliente e segredo do cliente para o aplicativo registrado

## Vincule a calculadora de hipotecas residenciais ao home page do site {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. Na instância do autor, vá para a seguinte página:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Role para baixo até a Calculadora Hipoteca Inicial.
1. Realce o painel da coluna direita (da calculadora) e toque para exibir o menu pop-up. No menu pop-up, toque em Configurar. A caixa de diálogo Editar Container de formulários AEM é exibida.

   ![calculadora configurepanel](assets/calculatorconfigurepanel.png)

1. Na caixa de diálogo Editar o Container de formulários AEM, navegue pelo caminho do ativo e selecione a calculadora de hipoteca inicial no seguinte caminho e toque em **Confirmar**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![seltassetpath](assets/selectassetpath.png)

1. Toque em **Concluído**.
1. Publique a página editada.

   >[!NOTE]
   >
   >O vínculo dos campos da calculadora com o FDM é pré-configurado pelo pacote do site de referência We.Finance. Para visualização do vínculo, abra o formulário no modo de criação e veja as referências de vínculo de campo.

1. Para criar uma entidade personalizada para armazenar o registro do candidato para o aplicativo de hipoteca residencial, importe o pacote da solução AEMFormsFSIRefsite_1_0.zip para a instância do Microsoft® Dynamics:

   1. Baixe o pacote de:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importe o pacote da solução para a instância do Microsoft® Dynamics. Em sua instância do Microsoft® Dynamics, vá até **Configurações** > **Soluções** e toque em **Importar**.

1. Para configurar os detalhes de contato do usuário usados no refsite, importe o pacote Sarah Rose Contact.CSV para sua instância do Microsoft® Dynamics:

   1. Baixe o pacote de:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importe o pacote para sua instância do Microsoft® Dynamics. Em sua instância do Microsoft® Dynamics, vá até **Vendas** > **Contatos** e toque em **Importar dados**.

