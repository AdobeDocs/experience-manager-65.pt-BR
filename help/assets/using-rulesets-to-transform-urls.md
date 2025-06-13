---
title: Usar conjuntos de regras para transformar URLs
description: É possível implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Usar conjuntos de regras para transformar URLs {#using-rulesets-to-transform-urls}

É possível implantar conjuntos de regras no Dynamic Media para transformar URLs. Os conjuntos de regras são conjuntos de instruções escritos em uma linguagem de script (como JavaScript) que avaliam dados XML e executam determinadas ações se esses dados atenderem a determinadas condições. Cada regra consiste em pelo menos uma condição e uma ação. Uma regra avalia os dados XML em relação às condições e, se uma condição for atendida, a ação apropriada será executada. Exemplos de conjuntos de regras incluem o seguinte:

* Adição de um sufixo de tipo MIME. Muitos serviços e sites exigem sufixos de imagem, como adicionar `.jpg` a uma URL.
* Criar um caminho de pasta para o URL para fins de SEO (Otimização do mecanismo de pesquisa).

  Consulte [Como o Adobe Dynamic Media Classic oferece suporte para SEO](/help/assets/assets/s7_seo.pdf).

* Adicionar metadados ao URL para fins de SEO (Otimização do mecanismo de pesquisa).

  Consulte [Como o Adobe Dynamic Media Classic oferece suporte para SEO](/help/assets/assets/s7_seo.pdf).

* Definir a disposição do conteúdo para acionar um download.
* Simplifique os URLs de modelo do Servidor de imagens para personalização. Por exemplo, transforme `rgb{XX,YY,ZZ}` no `\redXX\greenYY\blueZZ` pronto para RTF

* Solicite que determinados caracteres sejam codificados, como `$`, `{` e `}`, e que determinados caracteres sejam decodificados em ImageServer. Por exemplo, o Facebook não funciona bem com URLs que contêm caracteres especiais.

No contexto do Dynamic Media, os sites que usam um sistema baseado em XML para gerenciar informações de ativos podem fazer upload de arquivos XML para o Dynamic Media. Você pode designar um desses arquivos como o arquivo de conjunto de regras de pré-processamento para veicular o ativo do Dynamic Media. Esse arquivo reestrutura o formato de protocolo de URL padrão para atender à lógica de negócios dos sistemas que estão sendo integrados ao Dynamic Media. Especifique um arquivo XML para servir como o caminho do arquivo de definições do conjunto de regras.

>[!CAUTION]
>
>Tenha cuidado ao usar conjuntos de regras; eles podem impedir que o conteúdo do Dynamic Media seja exibido no seu site.

Há exemplos de conjuntos de regras disponíveis que podem ajudar você a criar seu próprio conjunto de regras.
Consulte [Referência do conjunto de regras](https://experienceleague.adobe.com/pt-br/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference).

Assim como em toda a criação de conjunto de regras, verifique se o arquivo XML é válido antes de fazer upload usando um programa de validação XML, como xmlvalid.

Além disso, primeiro teste seu conjunto de regras em um ambiente de preparo que não afete seu ambiente de produção em tempo real.
Os ambientes de produção e de preparo normalmente exigem logons diferentes.

Consulte o [aplicativo de desktop do Adobe Dynamic Media Classic para obter informações de entrada](https://experienceleague.adobe.com/pt-br/docs/dynamic-media-classic/using/getting-started/signing-out#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

**Para implantar conjuntos de regras XML:**

1. Entre no seu [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/pt-br/docs/dynamic-media-classic/using/getting-started/signing-out#sign-in-dmc-app).

   Suas credenciais e detalhes de logon foram fornecidos pela Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente da Adobe.

1. Faça upload do arquivo de conjunto de regras fazendo o seguinte:

   * Na barra Navegação global, selecione **[!UICONTROL Carregar]**.
   * Na página **[!UICONTROL Carregar]**, próximo ao canto superior esquerdo, selecione **[!UICONTROL Procurar]**.
   * Na caixa de diálogo **[!UICONTROL Abrir]**, navegue até o arquivo de conjunto de regras (XML).
   * Selecione o arquivo e, em seguida, **[!UICONTROL Abrir]**.
   * No lado direito da página **[!UICONTROL Carregar]**, selecione uma pasta de destino para o arquivo de conjunto de regras.
   * Próximo à parte inferior da página, verifique se a opção **[!UICONTROL Publicar após o carregamento]** está marcada.
   * No canto inferior direito da página, selecione **[!UICONTROL Enviar Upload]**.
   * Na barra Navegação global, selecione **[!UICONTROL Trabalhos]** para verificar o status do trabalho de carregamento. Quando a coluna **[!UICONTROL Status]** na página **[!UICONTROL Trabalho]** indicar Carregamento concluído, continue com as próximas etapas.

1. Na barra de navegação próxima à parte superior da página, selecione **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configuração de Publicação]** > **[!UICONTROL Servidor de Imagens]**.
1. Na página **[!UICONTROL Publicação do Servidor de Imagens]**, no grupo **[!UICONTROL Gerenciamento de Catálogo]**, localize o **[!UICONTROL Caminho do Arquivo de Definição de Conjunto de Regras]** e selecione **[!UICONTROL Selecionar]**.
1. Na página **[!UICONTROL Selecionar Arquivo de Definição do Conjunto de Regras (XML)]**, navegue até o arquivo de conjunto de regras e, no canto inferior direito da página, selecione **[!UICONTROL Selecionar]**.
1. No canto inferior direito da página Instalação, selecione **[!UICONTROL Fechar]**.
1. Execute um trabalho de publicação do servidor de imagens.

   As condições do conjunto de regras são aplicadas às solicitações para os Servidores de imagem ativos do Dynamic Media.

   Se você alterar o arquivo de conjunto de regras, as alterações serão aplicadas imediatamente quando você fizer upload novamente e publicar novamente o arquivo de conjunto de regras atualizado.
