---
title: Conectar ao Microsoft Translator
description: Saiba como conectar o AEM ao Microsoft Translator pronto para uso para automatizar seu fluxo de trabalho de tradução.
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
solution: Experience Manager, Experience Manager Sites
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 64%
---
# Conectar ao Microsoft Translator {#connecting-to-microsoft-translator}

O AEM fornece um conector integrado para o [Microsoft Translator](https://www.microsoft.com/pt-br/translator/business/) para traduzir conteúdo ou ativos da página. Após obter uma licença do Microsoft para usar o Microsoft Translator, configure o conector seguindo as instruções nesta página.

| Propriedade | Descrição |
|---|---|
| Rótulo da tradução | O nome de exibição do serviço de tradução |
| Atribuição da tradução | (Opcional) Para conteúdo gerado pelo usuário, a atribuição que aparece ao lado do texto traduzido, por exemplo, `Translations by Microsoft` |
| ID do espaço de trabalho | (Opcional) A ID do mecanismo personalizado do Microsoft Translator a ser usado |
| Chave de inscrição | Sua chave de assinatura Microsoft para o Microsoft Translator |

O procedimento a seguir cria uma configuração do Microsoft Translator.

1. No [painel de navegação,](/help/sites-authoring/basic-handling.md#first-steps) clique em **Ferramentas** > **Serviços em Nuvem** > **Serviços de Tradução em Nuvem**.
1. Navegue até o local em que deseja criar a configuração. Normalmente, isso fica na raiz do site ou pode ser uma configuração global padrão.
1. Clique no botão **Criar**.
1. Defina sua configuração.
   1. Selecione **Microsoft Translator** no menu suspenso.
   1. Digite um título para sua configuração. O título identifica a configuração no console do Cloud Services bem como nas listas suspensas de propriedades da página.
   1. Opcionalmente, digite um nome a ser usado para o nó do repositório que armazena a configuração.

   ![Criar configuração de tradução](assets/create-translation-config.png)

1. Clique em **Criar**.
1. Na janela **Editar configuração**, forneça os valores para o serviço de tradução descrito na tabela anterior.

   ![Editar configuração de tradução](assets/msft-config-ui.png)

1. Clique em **Conectar** para verificar a conexão.
1. Clique em **Salvar e fechar**.

## Publicar as configurações do serviço de tradução {#publishing-the-translator-service-configurations}

Como etapa final, publique as configurações do Microsoft Translator para oferecer suporte ao conteúdo traduzido publicado, usando a ação [publicar uma árvore](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree).
