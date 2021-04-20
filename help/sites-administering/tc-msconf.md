---
title: Conexão com o Microsoft Translator
seo-title: Conexão com o Microsoft Translator
description: Saiba como se conectar AEM ao Microsoft Translator.
seo-description: Saiba como se conectar AEM ao Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---


# Conexão com o Microsoft Translator{#connecting-to-microsoft-translator}

Crie uma configuração para o serviço em nuvem do Microsoft Translator para usar sua conta de Tradução da Microsoft para traduzir AEM conteúdo da página, conteúdo da comunidade ou ativos.

| Propriedade | Descrição |
|---|---|
| Rótulo da tradução | O nome de exibição do serviço de tradução. |
| Atribuição da tradução | (Opcional) Para conteúdo gerado pelo usuário, a atribuição que aparece ao lado do texto traduzido, por exemplo `Translations by Microsoft`. |
| ID da área de trabalho | (Opcional) A ID do mecanismo personalizado do Microsoft Translator a ser usado. |
| Chave de inscrição | Sua chave de assinatura da Microsoft para o Microsoft Translator. |

Após criar a configuração, é necessário [ativá-la](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

O procedimento a seguir usa a interface otimizada para toque para criar uma configuração do Microsoft Translator.

1. No painel, clique ou toque em Ferramentas > Cloud Services.
1. Na área Microsoft Translator , clique ou toque em Mostrar configurações.
1. Clique no link + ao lado de Configurações disponíveis.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Digite um título para sua configuração. O título identifica a configuração no console Cloud Services, bem como nas listas suspensas de propriedade da página. O nome padrão é baseado no título. Opcionalmente, digite um nome a ser usado para o nó do repositório que armazena a configuração. Você deve usar o valor padrão para a propriedade Configuração pai, que é o caminho do nó do repositório.
1. Clique em Criar.
1. Na caixa de diálogo exibida, digite os valores das propriedades e clique em OK.

## Exemplos de configurações de Cloud Service do Microsoft Translator {#sample-microsoft-translator-cloud-service-configurations}

As seguintes configurações do serviço em nuvem do Microsoft Translator são instaladas com as amostras do Geometrixx. Algumas configurações de exemplo usam uma conta de avaliação do Microsoft Translation que permite no máximo 2.000.000 caracteres traduzidos gratuitos por mês.

### Licença de avaliação do Microsoft Translator {#microsoft-translator-trial-license}

A configuração da Licença de Avaliação do Microsoft Translator é uma configuração de amostra instalada com o pacote de amostra Geometrixx Outdoors. Essa configuração usa uma conta do Microsoft Translator com assinatura gratuita que permite 2.000.000 caracteres traduzidos por mês.

### Licença de Avaliação do Microsoft Translator - Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

A licença de avaliação do Microsoft Translator - configuração do Geometrixx-outdoors é uma configuração de amostra instalada com o Geometrixx Outdoors. Essa configuração usa a mesma conta gratuita do Microsoft Translator que a configuração da Licença de Avaliação do Microsoft Translator. A conta tem uma assinatura gratuita que permite 2 000 000 caracteres traduzidos por mês.

Essa configuração do Microsoft Translator é otimizada para uso com o tipo de conteúdo do site de amostra do Geometrixx Outdoors.

### Atualização Da Configuração Da Licença De Avaliação Do Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

As páginas de configuração do Microsoft Translation fornecem um link conveniente para o site da Microsoft para obter uma assinatura de conta adequada para sistemas de produção.

1. No painel, clique ou toque em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na área Microsoft Translator , clique ou toque em Mostrar configurações e, em seguida, clique ou toque em Microsoft Translator Trial License (Microsoft Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Na página de configuração, clique em Atualizar assinatura. Use a página da Web da Microsoft que é aberta para configurar sua conta do .

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalizar seu mecanismo do Microsoft Translator {#customizing-your-microsoft-translator-engine}

As páginas de configuração do Microsoft Translation fornecem um link conveniente para o site da Microsoft na Web, para personalizar seu mecanismo do Microsoft Translator. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. No painel, clique ou toque em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na área Microsoft Translator , clique ou toque em Mostrar configurações e, em seguida, clique ou toque na configuração que deseja personalizar.
1. Na página de configuração, clique em Personalizar tradutor. Use a página da Web da Microsoft que é aberta para personalizar seu serviço.

## Ativando as configurações do serviço de tradução {#activating-the-translator-service-configurations}

É necessário ativar as configurações do serviço de nuvem para suportar o conteúdo traduzido que é replicado para a instância de publicação. Use o método de [ativar uma seção completa (tree)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) para ativar os nós do repositório que armazenam as configurações do serviço em nuvem do Microsoft Translator ou de terceiros. Os nós estão localizados abaixo dos seguintes nós pai:

* Serviço de Tradução da Microsoft: /libs/settings/cloudconfigs/translation/msft-translation
* Tradução de terceiros: /etc/cloudservices/tradução automática

