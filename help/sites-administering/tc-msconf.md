---
title: Conectando-se ao Microsoft&reg; Tradutor
description: Saiba como se conectar AEM ao Microsoft&reg; Tradutor.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 11%

---

# Conexão com o Microsoft® Translator{#connecting-to-microsoft-translator}

Crie uma configuração para o serviço em nuvem Microsoft® Translator para usar sua conta Microsoft® Translation para traduzir AEM conteúdo de página, conteúdo de comunidade ou ativos.

| Propriedade | Descrição |
|---|---|
| Rótulo da tradução | O nome de exibição do serviço de tradução. |
| Atribuição da tradução | (Opcional) Para conteúdo gerado pelo usuário, a atribuição que aparece ao lado do texto traduzido, por exemplo `Translations by Microsoft`. |
| ID do espaço de trabalho | (Opcional) A ID do mecanismo personalizado do Microsoft® Translator a ser usado. |
| Chave de inscrição | Sua chave de assinatura Microsoft® para o Microsoft® Translator. |

Após criar a configuração, é necessário [ative-a](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

O procedimento a seguir usa a interface otimizada para toque para criar uma configuração Microsoft® Translator.

1. No painel, clique ou toque em Ferramentas > Cloud Services.
1. Na área Microsoft® Translator, selecione Mostrar configurações.
1. Clique no link + ao lado de Configurações disponíveis.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Digite um título para sua configuração. O título identifica a configuração no console Cloud Services e nas listas suspensas de propriedade da página. O nome padrão é baseado no título. Opcionalmente, digite um nome a ser usado para o nó do repositório que armazena a configuração. Use o valor padrão para a propriedade Parent Configuration que é o caminho do nó do repositório.
1. Clique em Criar.
1. Na caixa de diálogo exibida, digite os valores das propriedades e clique em OK.

## Exemplos de configurações de Cloud Service do tradutor Microsoft® {#sample-microsoft-translator-cloud-service-configurations}

As seguintes configurações do serviço em nuvem Microsoft® Translator são instaladas com as amostras de Geometrixx. Algumas configurações de exemplo usam uma conta Microsoft® Translation de avaliação que permite no máximo 2.000.000 caracteres traduzidos gratuitos por mês.

### Licença de avaliação do tradutor Microsoft® {#microsoft-translator-trial-license}

A configuração da Licença de Avaliação do Microsoft® Translator é uma configuração de amostra instalada com o pacote de amostra do Geometrixx Outdoors. Essa configuração usa uma conta do Microsoft® Translator com assinatura gratuita que permite 2.000.000 caracteres traduzidos por mês.

### Licença de avaliação do tradutor Microsoft® - Geometrixx ao ar livre {#microsoft-translator-trial-license-geometrixx-outdoors}

A licença de avaliação do Microsoft® Translator - configuração do Geometrixx-outdoors é uma configuração de amostra instalada com Geometrixx Outdoors. Essa configuração usa a mesma conta gratuita do Microsoft® Translator que a configuração da Licença de avaliação do Microsoft® Translator. A conta tem uma assinatura gratuita que permite 2 000 000 caracteres traduzidos por mês.

Esta configuração do Microsoft® Translator é otimizada para uso com o tipo de conteúdo do site de amostra Geometrixx Outdoors.

### Atualização Da Configuração Da Licença De Avaliação Do Microsoft® Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

As páginas de configuração da Microsoft® Translation fornecem um link conveniente para o site da Microsoft® na web, para obter uma assinatura de conta adequada para sistemas de produção.

1. No painel, clique ou toque em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na área Microsoft® Translator (Tradutor®), clique ou toque em Mostrar configurações e, em seguida, clique ou toque em Licença de avaliação do Microsoft® Translator (Configuração de tradução Microsoft®).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Na página de configuração, clique em Atualizar assinatura. Use a página da Web do Microsoft® que é aberta para configurar sua conta.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalização do seu mecanismo do tradutor Microsoft® {#customizing-your-microsoft-translator-engine}

As páginas de configuração da Microsoft® Translation fornecem um link conveniente para o site da Microsoft® na web, para personalizar seu mecanismo Microsoft® Translator. ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. No painel, clique ou toque em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na área Microsoft® Translator , clique ou toque em Mostrar configurações e, em seguida, clique ou toque na configuração que deseja personalizar.
1. Na página de configuração, clique em Personalizar tradutor. Use a página da Web do Microsoft® que é aberta para personalizar seu serviço.

## Ativar as configurações do serviço de tradução {#activating-the-translator-service-configurations}

Para suportar o conteúdo traduzido que é replicado para a instância de publicação, ative as configurações do serviço de nuvem. Para ativar os nós do repositório que armazenam as configurações do Microsoft® Translator ou do serviço em nuvem de terceiros, use o método de [ativação de uma seção completa (árvore)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). Os nós estão localizados abaixo dos seguintes nós principais:

* Serviço de tradução Microsoft®: /libs/settings/cloudconfigs/translation/msft-translation
* Tradução de terceiros: /etc/cloudservices/tradução automática
