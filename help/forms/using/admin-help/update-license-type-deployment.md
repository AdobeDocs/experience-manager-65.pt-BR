---
title: Atualizar o tipo de licença para a implantação
seo-title: Update the license type for the deployment
description: Atualize o tipo de licença da implantação usando a página Alterar licença no console de administração.
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Atualizar o tipo de licença para a implantação {#update-the-license-type-for-the-deployment}

Como parte do processo de instalação dos formulários AEM, você usou o Configuration Manager para configurar e implantar os módulos de formulários AEM necessários. Por padrão, esses módulos são configurados com uma licença de avaliação de 60 dias. Use a página Alterar licença no console de administração para alterar o tipo de licença da implantação. Os módulos implantados no momento são exibidos na página Alterar licença .

A página Alterar licença exibe informações sobre sua licença:

* O tipo de licença atual
* A data e a hora em que a licença foi atualizada pela última vez
* Quem executou a última atualização
* O status atual da licença
* A data em que AEM formulários foi instalado
* A data de expiração da licença atual

>[!NOTE]
>
>A alteração de licença se aplica a todos os módulos implantados. Antes de alterar o tipo de licença, desimplante todos os módulos que não estejam licenciados. Não selecione o tipo de licença Production (Produção) se a lista de módulos implantados contiver módulos diferentes daqueles que você comprou no Adobe.

## Atualizar o tipo de licença {#update-the-license-type}

1. No console de administração, clique em Licenciamento.
1. Leia o contrato de licença do usuário final dos formulários de AEM, selecione Aceito se concordar com os termos do contrato e clique em Avançar.
1. Na página Alterar licença , selecione um tipo de licença:

   * **EVAL:** Licença de avaliação de 60 dias
   * **DEV:** Licença de desenvolvimento pessoal
   * **NFR:** Licença de avaliação de 2 anos
   * **IDEV:** Assinatura de um ano do Programa Adobe Developer
   * **Produção:** Licença perpétua

1. Selecione Sim, a alteração de licença é válida para todos os módulos implantados.
1. Clique em Confirmar alteração da licença. Será exibida uma mensagem informando que a licença foi atualizada com êxito.
