---
title: Ativar a alternância de recursos para integrar os recursos de pré-lançamento e de adesão antecipada
description: O Feature Toggle é uma funcionalidade do AEM que permite aos administradores ativar novos recursos em um ambiente de tempo de execução.
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
exl-id: 08815c2b-23b3-4545-a3ab-ba47ba1c3c55
source-git-commit: 9b28ab12422743cd7849d2761aef9916ec6710f5
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 1%

---

# Alternância de recursos no Adobe Experience Manager (AEM) 6.5{#enable-feature-toggle-aem-forms-65}

O Feature Toggle é uma funcionalidade do AEM que permite aos administradores ativar ou desativar recursos específicos dinamicamente. Esse recurso é particularmente útil para gerenciar os **recursos de Primeiros usuários** e os **recursos de Pré-lançamento** sem exigir grandes implantações ou alterações na base de código. Ele garante flexibilidade e controle sobre quais recursos estão acessíveis em um ambiente AEM.

## Por que usar alternadores de recursos em uma configuração do AEM 6.5?

Ao trabalhar em uma configuração do AEM 6.5, o recurso alterna a ajuda em:

* Testando características experimentais com segurança.

* Lançando novos componentes em fases.

* Manutenção de uma única base de código em vários ambientes.

* Redução de riscos durante implantações e atualizações.

## Pré-requisitos

Antes de habilitar a alternância de recursos na configuração do AEM 6.5, verifique o seguinte:

* O usuário é membro do grupo `forms-users`.

* Navegue até `http://<author-instance-url>:portnumber/system/console/bundles` e verifique se o pacote **(com.adobe.granite.toggle.impl.dev-1.1.2.jar)** está presente ou não. Caso não esteja presente, [baixe o pacote do link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.2%20.jar).

  ![Alternância de recursos](/help/forms/using/assets/feature-toggle-6.5.png)

## Ativar alternância de recursos {#enable-feature-toggle-65}

É possível configurar as opções de recursos para usuários iniciais ou novos recursos por meio do **Console da Web do AEM** seguindo as etapas abaixo:

1. Faça logon na sua instância do AEM Forms.
2. Vá até `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Procure o **Provedor de alternância dinâmica do Adobe Granite** no Gerenciador de configurações.
4. Clique no ícone ![lápis-ícone](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. Na seção [!UICONTROL Ativar alternâncias], clique em ![ícone-lápis](assets/aem6forms_add.png).
6. Adicione a ID de alternância do recurso, como mostrado na imagem abaixo.
   ![Adicionar alternância](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >Você pode encontrar a ID de alternância de recurso no documento específica para os recursos do adotante inicial.

7. Clique em Salvar.

## Desativar alternância de recursos {#disable-feature-toggle-65}

Para desativar os recursos para os recursos cujos alternadores estão ativados, siga as etapas abaixo:

1. Faça logon na sua instância do AEM Forms.
2. Vá até `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Procure o **Provedor de alternância dinâmica do Adobe Granite** no Gerenciador de configurações.
4. Clique no ícone ![lápis-ícone](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. Na seção [!UICONTROL Alternâncias Desabilitadas], clique em ![ícone de lápis](assets/aem6forms_add.png).
6. Adicione o número de alternância para que o recurso seja desativado.
   ![Remover alternância](assets/remove_toggle_feature_forms.png)
7. Clique em Salvar.

## Consideração técnica

Os alternadores de recursos são específicos do ambiente e gerenciados no tempo de execução, de modo que não exigem uma reinicialização do servidor. No entanto, alguns recursos podem exigir a atualização das páginas relevantes ou a limpeza do cache para refletir as alterações.
Você pode acessar a lista de recursos habilitados por meio da alternância de recursos para o seu ambiente via `http://<author-instance-url>:4502/etc.clientlibs/toggles.json`.
