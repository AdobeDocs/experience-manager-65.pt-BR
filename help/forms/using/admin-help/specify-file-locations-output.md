---
title: Especificar locais de arquivos para saída
seo-title: Especificar locais de arquivos para saída
description: Saiba como especificar locais de arquivos para a Saída.
seo-description: Saiba como especificar locais de arquivos para a Saída.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---


# Especificar locais de arquivos para a Saída {#specify-file-locations-for-output}

Você pode especificar os locais onde a Saída procura por determinados tipos de arquivos necessários.

1. No console de administração, clique em Serviços > saída.
1. Em Locais, especifique as opções apropriadas.
1. Clique em Salvar.

## Configurações de localização {#locations-settings}

**URI raiz do conteúdo:** o URI ou o local absoluto do repositório a partir do qual os formulários são recuperados. Esse valor é combinado com o parâmetro sForm, especificado por meio da API, para construir o caminho absoluto para o formulário recuperado. Esse valor pode fazer referência a um diretório ou a um local da Web acessível por meio de HTTP.

O valor padrão é uma string vazia.

**Arquivo de configuração XCI:** o local relativo ou absoluto do arquivo de configuração XCI que o serviço de saída usa para renderização. Para um valor relativo, presume-se que o arquivo XCI reside no arquivo AEM formulários implantáveis EAR.

O valor padrão é `com/adobe/formServer/PA/pa_output.xci`.

**Localização do cache:** especifica o local do cache de disco de saída. Quando você altera essa configuração, todas as informações de cache existentes no local atual são redefinidas e um novo cache é criado no novo local. Selecione uma destas opções:

**Local padrão:** essa é a seleção padrão. Quando essa opção é selecionada, o cache é criado em um local que depende do servidor de aplicativos que você está usando:

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Diretório temporário LC:** o cache é criado em um subdiretório do diretório temporário para formulários AEM, que é especificado no console de administração em Configurações > Configurações principais do sistema > Configurações > Localização do diretório temporário. O subdiretório é denominado `adobeoutput_[servername]`.

>[!NOTE]
>
>Se você estiver usando um utilitário de limpeza temporária, lembre-se de que ao excluir esses diretórios não afeta a funcionalidade, isso pode afetar significativamente o desempenho por um curto período de tempo, até que o novo cache seja criado. Para evitar esse problema, não exclua esses diretórios enquanto limpa o diretório temporário dos formulários AEM.

