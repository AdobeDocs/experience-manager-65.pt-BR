---
title: Disponibilizar fontes
description: Verifique se as fontes usadas em um formulário estão disponíveis para uso no servidor de aplicativos J2EE que hospeda formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Disponibilizar fontes {#make-fonts-available}

Verifique se as fontes usadas em um formulário estão disponíveis para uso no servidor de aplicativos J2EE que hospeda formulários AEM. Por exemplo, considere o cenário a seguir. Um designer de formulários adiciona uma fonte ao diretório de fontes que o Designer usa e cria um formulário que usa essa fonte em um computador separado. Para que o Serviço de saída use a fonte, coloque-a no diretório de fontes do cliente. Se o diretório de fontes do cliente não existir, crie um diretório no servidor de aplicativos J2EE que hospeda formulários AEM.

Para obter informações sobre configurações de fonte adicionais, consulte [Definir configurações gerais de formulários AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Especificar o local do diretório de fontes do Cliente**

1. No console de administração, clique em Configurações > Configurações dos sistemas principais > Configurações.
1. Na caixa Localização do Diretório de fontes do sistema, digite o caminho para o diretório de fontes do cliente. É possível adicionar vários diretórios, separados por ponto e vírgula **;**
1. Clique em OK.
1. Reinicie o sistema em que o AEM Forms está instalado.

>[!NOTE]
>
>As fontes são selecionadas do cache de fontes do sistema Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do Cliente, reinicie o sistema no qual o AEM Forms está instalado.
