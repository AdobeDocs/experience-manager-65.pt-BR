---
title: Visão geral do serviço de saída
description: Output permite mesclar dados de formulário XML com um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Visão geral do serviço de saída {#overview-of-output-service}

Output permite mesclar dados de formulário XML com um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos. O fluxo de saída pode ser enviado para uma impressora de rede, uma impressora local ou um arquivo de disco

Você pode usar a página Saída no console de administração para administrar o Serviço de saída. As configurações definidas são usadas em tempo de execução quando as configurações equivalentes não foram especificadas por meio da API de formulários AEM. A configuração feita por meio do SDK de formulários AEM substitui as configurações definidas usando o console de administração.

Para obter informações adicionais sobre o Serviço de saída, consulte [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_61).

Nas páginas de Saída do console de administração, é possível executar várias tarefas:

* Especifique conjuntos de caracteres para internacionalização. (Consulte [Alterar o conjunto de caracteres](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Especifique caminhos absolutos e relativos para URLs, URIs, XCIs e locais de arquivos. (Consulte [Especificar locais de arquivos para Saída](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configurar políticas e tamanhos de cache. (Consulte [Especificação do modo de cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) e [Definição das configurações de cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Disponibilizar fontes no servidor de aplicativos. (Consulte [Disponibilizar fontes](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Especificar fontes a serem incorporadas. (Consulte [Especificar fontes a serem incorporadas](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Especifique as opções de configuração XCI. (Consulte [Especificar opções de configuração XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Especifique as configurações de segurança. (Consulte [Especificar configurações de segurança](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Depois de alterar as configurações, clique em Salvar para aplicá-las à Saída. Não é necessário reiniciar o servidor para que as alterações entrem em vigor, mas talvez seja necessário reiniciar o serviço de Saída ao definir as configurações de cache.
