---
title: Especificar fontes a serem incorporadas
description: Saiba como especificar fontes a serem incorporadas em um Formulário adaptável. Você pode especificar quais fontes são incorporadas ou nunca incorporadas aos formulários gerados pelo serviço Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Especificar fontes a serem incorporadas{#specify-fonts-to-embed}

Você pode especificar quais fontes são sempre incorporadas ou nunca incorporadas aos formulários usados pelo Output. A incorporação de fontes aumenta o tamanho do arquivo dos formulários. Incorpore fontes incomuns que os usuários provavelmente não terão em seus sistemas e não incorpore fontes comuns que terão instaladas.

>[!NOTE]
>
>Se você tiver especificado um arquivo XCI personalizado para Saída, a opção de fonte incorporada no arquivo XCI substituirá essas configurações. (Consulte [Especificar locais de arquivos para Saída](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. No console de administração, clique em Serviços > saída.
1. Em Configurações de Incorporação de Fonte, na caixa Incorporar Sempre Fontes, digite os nomes das fontes a serem incorporadas aos formulários, separadas por vírgulas. As fontes especificadas são incorporadas somente no formulário gerado se forem usadas no formulário. Essa configuração será ignorada se a opção de fonte incorporada tiver sido ativada no arquivo XCI passado para o serviço. Nesse caso, todas as fontes usadas no PDF são sempre incorporadas.
1. Na caixa Nunca incorporar fontes, digite os nomes das fontes que não serão incorporadas aos formulários, separados por vírgulas. As fontes especificadas não são incorporadas ao PDF, mesmo se forem usadas no PDF gerado. Essa configuração será ignorada se a opção de fonte incorporada tiver sido desativada no arquivo XCI passado para o serviço. Nesse caso, nenhuma das fontes usadas no PDF é incorporada.
1. Clique em Salvar.
