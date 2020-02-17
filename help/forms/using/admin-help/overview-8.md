---
title: Visão geral do serviço de saída
seo-title: Visão geral do serviço de saída
description: A Saída permite unir dados de formulário XML a um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos.
seo-description: A Saída permite unir dados de formulário XML a um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Visão geral do serviço de saída {#overview-of-output-service}

A Saída permite unir dados de formulário XML a um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos. O fluxo de saída pode ser enviado para uma impressora de rede, uma impressora local ou um arquivo de disco

Você pode usar a página Saída no console de administração para administrar o serviço de Saída. As configurações definidas são usadas em tempo de execução quando as configurações equivalentes não foram especificadas pela API de formulários do AEM. A configuração feita por meio do SDK de formulários AEM substitui as configurações definidas por meio do console de administração.

Para obter informações adicionais sobre o serviço de Saída, consulte Referência [de](https://www.adobe.com/go/learn_aemforms_services_61)serviços.

Nas páginas de saída no console de administração, é possível executar várias tarefas:

* Especifique conjuntos de caracteres para internacionalização. (Consulte [Alterar o conjunto](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)de caracteres.)
* Especifique caminhos absolutos e relativos para URLs, URIs, XCIs e locais de arquivos. (Consulte [Especificar locais de arquivo para Saída](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configure tamanhos e políticas de cache. (Consulte [Especificação do modo](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) de cache e [Definição das configurações](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)de cache.)
* Disponibilize as fontes no servidor de aplicativos. (Consulte [Disponibilizar](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)fontes.)
* Especifique as fontes a serem incorporadas. (Consulte [Especificar fontes a serem incorporadas](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Especifique as opções de configuração XCI. (Consulte [Especificar opções](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)de configuração XCI.)
* Especifique as configurações de segurança. (Consulte [Especificar configurações](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)de segurança.)

Depois de alterar as configurações, clique em Salvar para aplicá-las à Saída. Não é necessário reiniciar o servidor para que as alterações tenham efeito, mas talvez seja necessário reiniciar o serviço de Saída ao configurar as configurações de cache.
