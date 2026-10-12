---
title: Especificar fontes a serem incorporadas
description: Saiba como especificar fontes a serem incorporadas em um Formulário adaptável. Você pode especificar quais fontes são incorporadas ou nunca incorporadas aos formulários gerados pelo serviço Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
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
source-wordcount: '283'
ht-degree: 0%
---
# Especificar fontes a serem incorporadas{#specify-fonts-to-embed}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Você pode especificar quais fontes são sempre incorporadas ou nunca incorporadas aos formulários usados pelo Output. A incorporação de fontes aumenta o tamanho do arquivo dos formulários. Incorpore fontes incomuns que os usuários provavelmente não terão em seus sistemas e não incorpore fontes comuns que terão instaladas.

>[!NOTE]
>
>Se você tiver especificado um arquivo XCI personalizado para Saída, a opção de fonte incorporada no arquivo XCI substituirá essas configurações. (Consulte [Especificar locais de arquivo para Saída](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. No console de administração, clique em Serviços > saída.
1. Em Configurações de Incorporação de Fonte, na caixa Incorporar Sempre Fontes, digite os nomes das fontes a serem incorporadas aos formulários, separadas por vírgulas. As fontes especificadas são incorporadas somente no formulário gerado se forem usadas no formulário. Essa configuração será ignorada se a opção de fonte incorporada tiver sido ativada no arquivo XCI passado para o serviço. Nesse caso, todas as fontes usadas no PDF são sempre incorporadas.
1. Na caixa Nunca incorporar fontes, digite os nomes das fontes que não serão incorporadas aos formulários, separados por vírgulas. As fontes especificadas não são incorporadas na PDF, mesmo se forem usadas na PDF gerada. Essa configuração será ignorada se a opção de fonte incorporada tiver sido desativada no arquivo XCI passado para o serviço. Nesse caso, nenhuma das fontes usadas no PDF é incorporada.
1. Clique em Salvar.
