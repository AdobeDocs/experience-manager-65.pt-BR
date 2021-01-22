---
title: Uso de conjuntos de regras para transformar URLs
description: Você pode implantar conjuntos de regras no Dynamic Media para transformar URLs. Conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: f786b35e77c6b862f7fc6e45d3d0af56a51e3e95
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 5%

---


# Uso de conjuntos de regras para transformar URLs {#using-rulesets-to-transform-urls}

Você pode implantar conjuntos de regras no Dynamic Media para transformar URLs. Conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições. Cada regra consiste em pelo menos uma condição e pelo menos uma ação. Uma regra avalia os dados XML em relação às condições e, se uma condição for atendida, ela executará a ação apropriada. Exemplos de conjuntos de regras incluem:

* Adicionando um sufixo de tipo MIME. Muitos serviços e sites exigem sufixos de imagem, como adicionar `.jpg` a um URL.
* Criando um caminho de pasta para o URL para fins de SEO (Search Engine Otimization).

   Consulte [Como o Adobe Dynamic Media Classic suporta SEO](/help/assets/assets/s7_seo.pdf).

* Adicionar metadados ao URL para fins de SEO (Search Engine Otimization).

   Consulte [Como o Adobe Dynamic Media Classic suporta SEO](/help/assets/assets/s7_seo.pdf).

* Definir a disposição do conteúdo para acionar um download.
* Simplificar o serviço de imagens modelando URLs para personalização. Por exemplo, transforme `rgb{XX,YY,ZZ}` em RTF-ready `\redXX\greenYY\blueZZ`

* Solicite que determinados caracteres sejam codificados, como `$`, `{` e `}`, e que determinados caracteres sejam decodificados em direção ao ImageServer. Por exemplo, o Facebook não funciona bem com URLs que contêm caracteres especiais.

   Consulte [Remoção de caracteres especiais de URLs](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

No contexto da Dynamic Media, os sites que usam um sistema baseado em XML para gerenciar informações de ativos podem carregar arquivos XML para a Dynamic Media. Você pode designar um desses arquivos como o arquivo de conjunto de regras de pré-processamento para servir ativos Dynamic Media. Esse arquivo reestrutura o formato padrão do protocolo URL para atender à lógica comercial dos sistemas que estão sendo integrados à Dynamic Media. Especifique um arquivo XML para servir como o caminho de arquivo de definições de conjuntos de regras.

>[!CAUTION]
>
>Tenha cuidado ao usar conjuntos de regras; eles podem impedir que o conteúdo do Dynamic Media seja exibido em seu site.

Existem conjuntos de regras de amostra disponíveis que podem ajudar a criar seu próprio conjunto de regras.
Consulte [Referência do conjunto de regras](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Como ocorre com a criação de todo o conjunto de regras, verifique se o arquivo XML é válido antes de carregá-lo usando um programa validador XML, como xmlvalid.
Consulte também [Resolução de problemas de conjuntos de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Além disso, primeiro teste seu conjunto de regras em um ambiente temporário que não afete seu ambiente de produção em tempo real.
Ambientes de produção e ambientes de preparo geralmente exigem logons diferentes.

Consulte o aplicativo de desktop Dynamic Media Classic [Adobe para obter informações de logon](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consulte também [Usar a imagem &#39;asset&#39; em vez de &#39;is&#39; em um conjunto de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Para implantar conjuntos de regras XML:**

1. Faça logon no [aplicativo de desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.

1. Carregue seu arquivo de conjunto de regras fazendo o seguinte:

   * Na barra Navegação global, clique em **[!UICONTROL Carregar]**.
   * Na página **[!UICONTROL Carregar]**, próximo ao canto superior esquerdo, clique em **[!UICONTROL Procurar]**.
   * Na caixa de diálogo **[!UICONTROL Abrir]**, navegue até o arquivo de conjunto de regras (XML).
   * Selecione o arquivo e clique em **[!UICONTROL Abrir]**.
   * No lado direito da página **[!UICONTROL Carregar]**, selecione uma pasta de destino para o arquivo de conjunto de regras.
   * Próximo à parte inferior da página, verifique se **[!UICONTROL Publicar após carregar]** está marcada.
   * No canto inferior direito da página, clique em **[!UICONTROL Enviar upload]**.
   * Na barra Navegação global, clique em **[!UICONTROL Tarefas]** para verificar o status do trabalho de upload. Quando a coluna **[!UICONTROL Status]** na página **[!UICONTROL Job]** exibir Carregar concluído, vá para as próximas etapas.

1. Na barra de navegação próxima à parte superior da página, clique em **[!UICONTROL Configuração > Configuração de aplicativo > Configuração de publicação > Servidor de imagem]**.
1. Na página **[!UICONTROL Publicação do servidor de imagens]**, no grupo **[!UICONTROL Gerenciamento de catálogo]**, localize o **[!UICONTROL Caminho do arquivo de definição de conjunto de regras]** e clique em **[!UICONTROL Selecionar]**.
1. Na página **[!UICONTROL Selecionar arquivo de definição do conjunto de regras (XML)]**, navegue até o arquivo de conjunto de regras e, no canto inferior direito da página, clique em **[!UICONTROL Selecionar]**.
1. No canto inferior direito da página Configuração, clique em **[!UICONTROL Fechar]**.
1. Execute um trabalho de publicação do Image Server.

   As condições do conjunto de regras são aplicadas às solicitações dos Dynamic Media Image Servers ativos.

   Se você fizer alterações no arquivo do conjunto de regras, as alterações serão aplicadas imediatamente quando você fizer upload e publicar novamente o arquivo atualizado do conjunto de regras.

