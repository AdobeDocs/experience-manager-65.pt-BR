---
title: Disponibilizar fontes
description: Verifique se as fontes usadas em um formulário estão disponíveis para uso no servidor de aplicativos J2EE que hospeda o AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
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
source-wordcount: '228'
ht-degree: 2%
---
# Disponibilizar fontes {#make-fonts-available}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Verifique se as fontes usadas em um formulário estão disponíveis para uso no servidor de aplicativos J2EE que hospeda o AEM Forms. Por exemplo, considere o cenário a seguir. Um designer de formulários adiciona uma fonte ao diretório de fontes que o Designer usa e cria um formulário que usa essa fonte em um computador separado. Para que o Serviço de saída use a fonte, coloque-a no diretório de fontes do cliente. Se o diretório de fontes do cliente não existir, crie um diretório no servidor de aplicativos J2EE que hospeda o AEM Forms.

Para obter informações sobre configurações de fonte adicionais, consulte [Definir configurações gerais de formulários do AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Especificar o local do diretório de fontes do Cliente**

1. No console de administração, clique em Configurações > Configurações dos sistemas principais > Configurações.
1. Na caixa Localização do Diretório de fontes do sistema, digite o caminho para o diretório de fontes do cliente. É possível adicionar vários diretórios, separados por ponto-e-vírgula **;**
1. Clique em OK.
1. Reinicie o sistema em que o AEM Forms está instalado.

>[!NOTE]
>
>As fontes são selecionadas do cache de fontes do sistema Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do Cliente, reinicie o sistema no qual o AEM Forms está instalado.
