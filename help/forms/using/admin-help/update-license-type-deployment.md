---
title: Atualizar o tipo de licença para a implantação
seo-title: Atualizar o tipo de licença para a implantação
description: Atualize o tipo de licença para a implantação usando a página Alterar licença no console de administração.
seo-description: Atualize o tipo de licença para a implantação usando a página Alterar licença no console de administração.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Atualize o tipo de licença para a implantação {#update-the-license-type-for-the-deployment}

Como parte do processo de instalação de formulários AEM, você usou o Configuration Manager para configurar e implantar os módulos de formulários AEM necessários. Por padrão, esses módulos são configurados com uma licença de avaliação de 60 dias. Use a página Alterar licença no console de administração para alterar o tipo de licença da implantação. Os módulos implantados no momento são exibidos na página Alterar licença.

A página Alterar Licença exibe informações sobre sua licença:

* O tipo de licença atual
* A data e a hora em que a licença foi atualizada pela última vez
* Quem realizou a última atualização
* O status atual da licença
* A data em que os formulários AEM foram instalados
* A data em que a licença atual expirará

>[!NOTE]
>
>A alteração de licença se aplica a todos os módulos implantados. Antes de alterar o tipo de licença, desimplante todos os módulos que não estejam licenciados. Não selecione o tipo de licença de produção se a lista dos módulos implantados contiver módulos diferentes daqueles que você comprou da Adobe.

## Atualizar o tipo de licença {#update-the-license-type}

1. No console de administração, clique em Licenciamento.
1. Leia o contrato de licença de usuário final para formulários AEM, selecione Aceito se concordar com os termos do contrato e clique em Avançar.
1. Na página Alterar licença, selecione um tipo de licença:

   * **EVAL:licença de avaliação de** 60 dias
   * **DEV:Licença de desenvolvimento** perpétua
   * **NFR:licença de avaliação de** 2 anos
   * **IDEV:subscrição de** 1 ano para o Programa de desenvolvedor do Adobe
   * **Produção:Licença** Perpétua

1. Selecione Sim, a alteração de licença é válida para todos os módulos implantados.
1. Clique em Confirmar alteração de licença. Será exibida uma mensagem informando que a licença foi atualizada com êxito.

