---
title: Disponibilizar fontes
seo-title: Disponibilizar fontes
description: Verifique se as fontes usadas em um formulário estão disponíveis para uso no servidor de aplicativos J2EE que hospeda formulários AEM.
seo-description: Verifique se as fontes usadas em um formulário estão disponíveis para uso no servidor de aplicativos J2EE que hospeda formulários AEM.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Disponibilizar fontes {#make-fonts-available}

Verifique se as fontes usadas em um formulário estão disponíveis para uso no servidor de aplicativos J2EE que hospeda formulários AEM. Por exemplo, considere o seguinte cenário. Um designer de formulário adiciona uma fonte ao diretório de fontes que o Designer usa e cria um formulário que usa essa fonte em um computador separado. Para que o serviço de Saída use a fonte, coloque-a no diretório Fontes do cliente. Se o diretório Fontes do cliente não existir, crie um diretório no servidor de aplicativos J2EE que hospeda formulários AEM.

Para obter informações sobre configurações de fonte adicionais, consulte [Definir configurações gerais de formulários AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Especificar o local do diretório de fontes do Cliente**

1. No console de administração, clique em Configurações > Principais configurações de sistemas > Configurações.
1. Na caixa Local do diretório Fontes do sistema, digite o caminho para o diretório de fontes do cliente. Vários diretórios podem ser adicionados, separados por ponto-e-vírgula **;**
1. Clique em OK.
1. Reinicie o sistema no qual os formulários AEM estão instalados.

>[!NOTE]
>
>As fontes são escolhidas do cache de fontes do sistema do Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do Cliente, reinicie o sistema no qual os formulários AEM estão instalados.

