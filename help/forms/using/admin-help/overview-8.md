---
title: Visão geral do serviço de saída
description: Output permite mesclar dados de formulário XML com um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%
---
# Visão geral do serviço de saída {#overview-of-output-service}

Output permite mesclar dados de formulário XML com um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos. O fluxo de saída pode ser enviado para uma impressora de rede, uma impressora local ou um arquivo de disco

Você pode usar a página Saída no console de administração para administrar o Serviço de saída. As configurações definidas são usadas em tempo de execução quando as configurações equivalentes não foram especificadas por meio da API de formulários do AEM. A configuração feita por meio do AEM Forms SDK substitui as configurações definidas usando o console de administração.

Para obter informações adicionais sobre o Serviço de saída, consulte [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_61).

Nas páginas de Saída do console de administração, é possível executar várias tarefas:

* Especifique conjuntos de caracteres para internacionalização. (Consulte [Alterar o conjunto de caracteres](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Especifique caminhos absolutos e relativos para URLs, URIs, XCIs e locais de arquivos. (Consulte [Especificar locais de arquivo para Saída](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configurar políticas e tamanhos de cache. (Consulte [Especificação do modo de cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) e [Definição das configurações de cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Disponibilizar fontes no servidor de aplicativos. (Consulte [Disponibilizar fontes](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Especificar fontes a serem incorporadas. (Consulte [Especificar fontes a serem inseridas](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Especifique as opções de configuração XCI. (Consulte [Especificar opções de configuração XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Especifique as configurações de segurança. (Consulte [Especificar configurações de segurança](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Depois de alterar as configurações, clique em Salvar para aplicá-las à Saída. Não é necessário reiniciar o servidor para que as alterações entrem em vigor, mas talvez seja necessário reiniciar o serviço de Saída ao definir as configurações de cache.
