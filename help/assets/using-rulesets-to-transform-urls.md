---
title: Uso de conjuntos de regras para transformar URLs
description: Você pode implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritas em uma linguagem de script (como JavaScript) que avalia dados XML e executa determinadas ações se esses dados atenderem a determinadas condições.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: Business Practitioner, Administrator,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 5%

---

# Uso de conjuntos de regras para transformar URLs {#using-rulesets-to-transform-urls}

Você pode implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritas em uma linguagem de script (como JavaScript) que avalia dados XML e executa determinadas ações se esses dados atenderem a determinadas condições. Cada regra consiste em pelo menos uma condição e pelo menos uma ação. Uma regra avalia os dados XML em relação às condições e, se uma condição for atendida, tomará a ação apropriada. Exemplos de conjuntos de regras incluem:

* Adicionar um sufixo do tipo MIME. Muitos serviços e sites exigem sufixos de imagem, como adicionar `.jpg` a um URL.
* Criação de um caminho de pasta para o URL para fins de SEO (Otimização de Mecanismo de Pesquisa).

   Consulte [Como o Adobe Dynamic Media Classic suporta SEO](/help/assets/assets/s7_seo.pdf).

* Adicionar metadados ao URL para fins de SEO (Otimização de mecanismo de pesquisa).

   Consulte [Como o Adobe Dynamic Media Classic suporta SEO](/help/assets/assets/s7_seo.pdf).

* Definir a disposição do conteúdo para acionar um download.
* Simplifique os URLs de modelos do Image Serving para personalização. Por exemplo, transformar `rgb{XX,YY,ZZ}` em RTF-ready `\redXX\greenYY\blueZZ`

* Solicite determinados caracteres a serem codificados, como `$`, `{` e `}`, e determinados caracteres a serem decodificados para o ImageServer. Por exemplo, o Facebook não funciona bem com URLs contendo caracteres especiais.

   Consulte [Removendo caracteres especiais de URLs](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

No contexto do Dynamic Media, os sites que usam um sistema baseado em XML para gerenciar informações de ativos podem fazer upload de arquivos XML para o Dynamic Media. Você pode designar um desses arquivos como o arquivo de conjunto de regras de pré-processamento para servir ativos do Dynamic Media. Esse arquivo reestrutura o formato de protocolo URL padrão para atender à lógica comercial dos sistemas que estão sendo integrados ao Dynamic Media. Você especifica um arquivo XML a ser exibido como o caminho de arquivo das definições do conjunto de regras.

>[!CAUTION]
>
>Tenha cuidado ao usar conjuntos de regras; elas podem impedir que o conteúdo do Dynamic Media seja exibido no seu site.

Existem conjuntos de regras de amostra disponíveis que podem ajudar você a criar seu próprio conjunto de regras.
Consulte [Referência do conjunto de regras](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Como em toda a criação do conjunto de regras, certifique-se de que o arquivo XML seja válido antes de fazer upload usando um programa de validação XML, como xmlvalid.
Consulte também [Resolução de problemas de conjuntos de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Além disso, certifique-se de testar primeiro seu conjunto de regras em um ambiente de preparo que não afete seu ambiente de produção ativo.
Ambientes de produção e ambientes de preparo normalmente exigem logons diferentes.

Consulte o [aplicativo de desktop Adobe Dynamic Media Classic para obter informações de logon](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consulte também [Usar a imagem &#39;asset&#39; em vez de &#39;is&#39; em um conjunto de regras](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Para implantar conjuntos de regras XML:**

1. Faça logon no [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte Técnico.

1. Faça upload do arquivo de conjunto de regras fazendo o seguinte:

   * Na barra Navegação global, clique em **[!UICONTROL Fazer upload]**.
   * Na página **[!UICONTROL Upload]**, próximo ao canto superior esquerdo, clique em **[!UICONTROL Procurar]**.
   * Na caixa de diálogo **[!UICONTROL Abrir]**, navegue até o arquivo do conjunto de regras (XML).
   * Selecione o arquivo e clique em **[!UICONTROL Abrir]**.
   * No lado direito da página **[!UICONTROL Upload]**, selecione uma pasta de destino para o arquivo de conjunto de regras.
   * Próximo à parte inferior da página, verifique se **[!UICONTROL Publicar após o upload]** está marcado.
   * No canto inferior direito da página, clique em **[!UICONTROL Enviar upload]**.
   * Na barra Navegação global, clique em **[!UICONTROL Trabalhos]** para verificar o status do trabalho de upload. Quando a coluna **[!UICONTROL Status]** na página **[!UICONTROL Trabalho]** exibir Carregar concluído, continue para as próximas etapas.

1. Na barra de navegação próxima à parte superior da página, clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configuração de publicação > Servidor de imagem]**.
1. Na página **[!UICONTROL Publicação do servidor de imagens]**, no grupo **[!UICONTROL Gerenciamento de catálogo]**, localize o **[!UICONTROL Caminho do arquivo de definição de conjunto de regras]** e clique em **[!UICONTROL Selecionar]**.
1. Na página **[!UICONTROL Selecionar arquivo de definição do conjunto de regras (XML)]**, navegue até o arquivo de conjunto de regras e, no canto inferior direito da página, clique em **[!UICONTROL Selecionar]**.
1. No canto inferior direito da página Configurar, clique em **[!UICONTROL Fechar]**.
1. Execute um trabalho de publicação do servidor de imagens.

   As condições do conjunto de regras são aplicadas nas solicitações dos Servidores de Imagem Dynamic Media ao vivo.

   Se você fizer alterações no arquivo de conjunto de regras, as alterações serão aplicadas imediatamente quando você fizer upload novamente e publicar novamente o arquivo de conjunto de regras atualizado.
