---
title: Atualizar o tipo de licença para a implantação
description: Atualize o tipo de licença para a implantação usando a página Alterar licença no console de administração.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Atualizar o tipo de licença para a implantação {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Como parte do processo de instalação do AEM Forms, você usou o Configuration Manager para configurar e implantar os módulos AEM Forms necessários. Por padrão, esses módulos são configurados com uma licença de avaliação de 60 dias. Use a página Alterar Licença no console de administração para alterar o tipo de licença da implantação. Os módulos implantados no momento são exibidos na página Alterar licença.

A página Alterar licença exibe informações sobre sua licença:

* O tipo de licença atual
* A data e a hora em que a licença foi atualizada pela última vez
* Quem executou a última atualização
* O status atual da licença
* A data em que os formulários AEM foram instalados
* A data em que a licença atual expirará

>[!NOTE]
>
>A alteração de licença se aplica a todos os módulos implantados. Antes de alterar o tipo de licença, cancele a implantação de módulos que não estejam licenciados. Não selecione o tipo de licença de Produção se a lista de módulos implantados contiver módulos diferentes daqueles que você adquiriu do Adobe.

## Atualizar o tipo de licença {#update-the-license-type}

1. No console de administração, clique em Licenciamento.
1. Leia o contrato de licença do usuário final dos formulários AEM, selecione Aceito se concordar com os termos do contrato e clique em Avançar.
1. Na página Alterar licença, selecione um tipo de licença:

   * **EVAL:** licença de avaliação de 60 dias
   * **DEV:** licença de desenvolvimento permanente
   * **NFR:** licença de avaliação de 2 anos
   * **IDEV:** assinatura de 1 ano do Programa Adobe Developer
   * **Produção:** licença perpétua

1. Selecione Sim, a alteração de licença é válida para todos os módulos implantados.
1. Clique em Confirmar alteração da licença. Será exibida uma mensagem informando que a licença foi atualizada com êxito.
