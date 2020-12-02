---
title: Especificação de fontes a serem incorporadas
seo-title: Especificação de fontes a serem incorporadas
description: Saiba como especificar fontes a serem incorporadas.
seo-description: Saiba como especificar fontes a serem incorporadas.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Especificação de fontes para incorporar {#specifying-fonts-to-embed}

Você pode especificar quais fontes são sempre incorporadas ou nunca incorporadas aos formulários gerados pelo serviço Forms. A incorporação de fontes aumenta o tamanho do arquivo dos formulários. Incorpore fontes incomuns que os usuários raramente têm em seus sistemas. Não incorpore fontes comuns que elas normalmente têm instalado.

>[!NOTE]
>
>Se você tiver especificado um arquivo XCI personalizado para Forms, a opção de fonte incorporada no arquivo XCI substituirá essas configurações. (Consulte [Configuração de locais para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. No console de administração, clique em **[!UICONTROL Serviços > Forms]**.
1. Em **[!UICONTROL Configurações de incorporação de fonte]**, na caixa **[!UICONTROL Sempre incorporar fontes]**, digite os nomes das fontes a serem incorporadas aos formulários, separados por vírgulas. As fontes especificadas são incorporadas somente no formulário gerado se forem usadas no formulário. Essa configuração será ignorada se a opção de fonte incorporada tiver sido ativada no arquivo XCI passado para o serviço porque, nesse caso, todas as fontes usadas no PDF sempre serão incorporadas.
1. Na caixa **[!UICONTROL Nunca incorporar fontes]**, digite os nomes das fontes que não serão incorporadas aos formulários, separados por vírgulas. As fontes especificadas não são incorporadas no PDF, mesmo se forem usadas no PDF gerado. Essa configuração será ignorada se a opção de fonte incorporada tiver sido desativada no arquivo XCI passado ao serviço porque, nesse caso, nenhuma das fontes usadas no PDF é incorporada.
1. Clique em **[!UICONTROL Salvar]**.

