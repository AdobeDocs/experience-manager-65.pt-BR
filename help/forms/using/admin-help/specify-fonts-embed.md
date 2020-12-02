---
title: Especificar fontes a serem incorporadas
seo-title: Especificar fontes a serem incorporadas
description: Saiba como especificar fontes a serem incorporadas.
seo-description: Saiba como especificar fontes a serem incorporadas.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Especificar fontes a serem incorporadas{#specify-fonts-to-embed}

Você pode especificar quais fontes são sempre incorporadas ou nunca incorporadas aos formulários usados pelo Output. A incorporação de fontes aumenta o tamanho do arquivo dos formulários. Incorpore fontes incomuns que os usuários provavelmente não terão em seus sistemas e não incorpore fontes comuns que eles terão instalado.

>[!NOTE]
>
>Se você tiver especificado um arquivo XCI personalizado para Saída, a opção de fonte incorporada no arquivo XCI substituirá essas configurações. (Consulte [Especificar locais de arquivos para Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. No console de administração, clique em Serviços > saída.
1. Em Configurações de incorporação de fonte, na caixa Sempre incorporar fontes, digite os nomes das fontes a serem incorporadas aos formulários, separados por vírgulas. As fontes especificadas são incorporadas somente no formulário gerado se forem usadas no formulário. Essa configuração será ignorada se a opção de fonte incorporada tiver sido ativada no arquivo XCI passado ao serviço. Nesse caso, todas as fontes usadas no PDF são sempre incorporadas.
1. Na caixa Nunca incorporar fontes, digite os nomes das fontes que não serão incorporadas aos formulários, separados por vírgulas. As fontes especificadas não são incorporadas no PDF, mesmo se forem usadas no PDF gerado. Essa configuração será ignorada se a opção de fonte incorporada tiver sido desativada no arquivo XCI passado para o serviço. Nesse caso, nenhuma das fontes usadas no PDF é incorporada.
1. Clique em Salvar.

