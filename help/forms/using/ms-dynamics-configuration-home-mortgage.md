---
title: Configure o Microsoft Dynamics 365 para o fluxo de trabalho de hipoteca da página inicial do site de referência We.Finance
description: Saiba como usar os serviços do Microsoft&reg; Dynamics 365 por meio de formulários adaptáveis para o fluxo de trabalho de hipoteca da página de referência do We.Finance.
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Configure o Microsoft Dynamics 365 para o fluxo de trabalho de hipoteca da página inicial do site de referência We.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Saiba como usar os serviços do Microsoft® Dynamics 365 por meio de formulários adaptáveis para o fluxo de trabalho de hipoteca do site de referência We.Finance

## Visão geral {#overview}

O Microsoft® Dynamics 365 é um software de CRM (Customer Relationship Management) e ERP (Enterprise Resource Planning) que fornece soluções corporativas para criar e gerenciar contas, contatos, leads, oportunidades e casos de clientes.

A AEM Forms fornece um serviço em nuvem para integrar o Dynamics 365 com o [Integração de dados do Forms](/help/forms/using/data-integration.md) módulo. Antes de usar a apresentação do aplicativo Hipoteca residencial com o cenário do Microsoft® Dynamics, é necessário configurar o Microsoft® Dynamics 365 para ser usado com o site de referência We.Finance.

## Pré-requisitos {#prerequisites}

Antes de começar a instalar e configurar o Dynamics 365, verifique se você tem:

* AEM 6.3 Forms Service Pack 1 e posterior
* Conta do Microsoft® Dynamics 365
* Aplicativo registrado para o serviço Dynamics 365 com o Ative Diretory do Microsoft® Azure
* ID do cliente e segredo do cliente para o aplicativo registrado

## Vincule a calculadora de hipoteca do site à página inicial do site {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. Na instância do autor, vá para a seguinte página:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Role para baixo até a Calculadora de hipoteca de casa.
1. Realce o painel da coluna direita (calculadora) e selecione para exibir o menu pop-up. No menu pop-up, selecione Configurar. A caixa de diálogo Editar contêiner do AEM Forms é exibida.

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. Na caixa de diálogo Editar contêiner do AEM Forms, navegue pelo caminho do ativo e selecione home-mortgage-calculator no seguinte caminho e selecione **Confirmar o**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![seletassetpath](assets/selectassetpath.png)

1. Selecionar **Concluído**.
1. Publish a página editada.

   >[!NOTE]
   >
   >A vinculação dos campos do calculador com o FDM é pré-configurada por meio do pacote de site de referência We.Finance. Para exibir a vinculação, é possível abrir o formulário no modo de criação e ver o campo bind references.

1. Para criar uma entidade personalizada para armazenar o registro do candidato para o aplicativo de hipoteca sobre imóveis residenciais, importe o pacote da solução AEMFormsFSIRefsite_1_0.zip para sua instância do Microsoft® Dynamics:

   1. Baixe o pacote de:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importar o pacote de soluções para a instância do Microsoft® Dynamics. Na instância do Microsoft® Dynamics, acesse **Configurações** > **Soluções** e selecione **Importar**.

1. Para configurar os detalhes de contato do usuário usados no refsite, importe o pacote Sarah Rose Contact.CSV para a instância do Microsoft® Dynamics:

   1. Baixe o pacote de:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importe o pacote para sua instância do Microsoft® Dynamics. Na instância do Microsoft® Dynamics, acesse **Vendas** > **Contatos** e selecione **Importar dados**.
