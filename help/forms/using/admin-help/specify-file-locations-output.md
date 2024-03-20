---
title: Especificar locais de arquivos para Saída
description: Saiba como especificar locais de arquivos para Saída para determinados tipos de arquivos, por exemplo, URI da raiz do conteúdo, Arquivo de configuração XCI, Cache e Padrão.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Especificar locais de arquivos para Saída {#specify-file-locations-for-output}

Você pode especificar os locais onde a Saída procura determinados tipos de arquivos que ela requer.

1. No console de administração, clique em Serviços > saída.
1. Em Locais, especifique as opções apropriadas.
1. Clique em Salvar.

## Configurações de locais {#locations-settings}

**URI da raiz do conteúdo:** O URI ou local absoluto do repositório do qual os formulários são recuperados. Esse valor é combinado com o parâmetro sForm, especificado por meio da API, para construir o caminho absoluto para o formulário recuperado. Esse valor pode fazer referência a um diretório ou local da Web acessível por meio de HTTP.

O valor padrão é uma string vazia.

**Arquivo de configuração XCI:** O local relativo ou absoluto do arquivo de configuração XCI que o serviço de Saída usa para renderização. Para um valor relativo, presume-se que o arquivo XCI resida no arquivo EAR implantável dos formulários AEM.

O valor padrão é `com/adobe/formServer/PA/pa_output.xci`.

**Local do Cache:** Especifica o local do cache do disco de Saída. Ao alterar essa configuração, todas as informações de cache existentes no local atual são redefinidas e um novo cache é criado no novo local. Selecione uma das seguintes opções:

**Local padrão:** Esta é a seleção padrão. Quando essa opção é selecionada, o cache é criado em um local dependente do servidor de aplicativos que você está usando:

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Diretório Temp LC:** O cache é criado em um subdiretório do diretório temporário dos formulários AEM, que é especificado no console de administração em Settings > Core System Settings > Configurations > Location of Temp Diretory. O subdiretório é nomeado como `adobeoutput_[servername]`.

>[!NOTE]
>
>Se você estiver usando um utilitário de limpeza temporário, embora a exclusão desses diretórios não afete a funcionalidade, isso pode afetar significativamente o desempenho por um curto período, até que o novo cache seja criado. Para evitar esse problema, não exclua esses diretórios enquanto limpa o diretório temporário dos formulários AEM.
