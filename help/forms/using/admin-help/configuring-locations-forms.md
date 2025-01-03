---
title: Configuração de locais para o Forms
description: Saiba como configurar o local para o formulário AEM. Você pode especificar os locais do arquivo do atributo, o local do formulário, o arquivo de PDF de propagação e o local do cache.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Configuração de locais para o Forms {#configuring-locations-for-forms}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Você pode especificar a URL, o URI e os locais de atributos do arquivo, como a raiz da Web, o local dos formulários a serem recuperados, o arquivo de PDF de propagação usado nas transformações de PDForm e o local do cache.

1. No console de administração, clique em Serviços > Forms.
1. Em Locais, especifique as opções apropriadas. As opções são descritas abaixo.
1. Clique em Salvar.

## Configurações de locais {#locations-settings}

**URL Base:** A URL base onde os recursos de formulário, como imagens e scripts, estão localizados. Esse valor é necessário para transformações de HTML que incluem referências HREF a dependências externas, como imagens ou scripts. Um desses scripts é o xfasubset.js, que é necessário para que os formulários HTML executem inteligência XFA. Este valor deve ser o equivalente HTTP do URI da raiz de conteúdo.

>[!NOTE]
>
>O URL de base suporta apenas protocolos HTTP ou de repositório. Ele não é compatível com protocolos como file:///. Se você precisar acessar um recurso, como um CSS personalizado ou um URI de assinatura digital, use o valor do parâmetro de API apropriado para especificar o local absoluto.

Quando um caminho de dependência é absoluto, o valor do URL base é ignorado. Caso contrário, o caminho da dependência é combinado com o URL base.

O valor padrão é uma string vazia.

O exemplo a seguir aponta para o mesmo conteúdo (usando o URI da raiz do conteúdo e o URL base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI da Raiz da Web de FS:** A URL do aplicativo Web do Forms. Você pode deixar essa caixa vazia se o aplicativo Web do Forms e o aplicativo cliente forem implantados no mesmo servidor de aplicativos; o URL da raiz da Web da API do Forms é usado.

Se o aplicativo web do Forms e o aplicativo cliente não forem implantados no mesmo servidor de aplicativos, forneça o URL para o aplicativo web do Forms nesta caixa, como mostrado neste exemplo:

`https://<host name>:<port>/FormServer`

Onde `host name`e `port` são o nome e o número da porta do servidor que está hospedando o aplicativo Web do Forms.

O valor padrão é uma string vazia.

**URI da Raiz da Web:** A raiz da Web do aplicativo. Esse valor é combinado com o parâmetro sTargetURL (quando sTargetURL é fornecido como relativo), especificado por meio do AEM Forms SDK, para construir um URL absoluto para acessar o conteúdo da Web específico do aplicativo.

O valor padrão é uma string vazia.

**URI da Raiz de Conteúdo:** o URI ou o local absoluto do qual os formulários são recuperados. Esse valor é combinado com o parâmetro sFormQuery, especificado por meio da API, para construir o caminho absoluto para o formulário que é recuperado. Esse valor pode fazer referência a um diretório ou local da Web acessível por meio de HTTP.

O valor padrão é uma string vazia.

**URI de Configuração XCI:** O local relativo ou absoluto no qual o arquivo XCI usado para renderização é encontrado. Para um valor relativo, presume-se que o arquivo XCI resida no arquivo EAR de formulários AEM implantáveis.

O valor padrão é `com/adobe/formServer/PA/pa.xci`.

**URI do Mapa de Fontes:** o local relativo ou absoluto do arquivo de mapeamento de fontes. Para um valor relativo, presume-se que esse arquivo resida no arquivo EAR de formulários AEM implantáveis.

O arquivo de mapeamento de fontes é usado para criar mapeamentos de fontes personalizados para transformações de HTML em formulários, permitindo especificar qual fonte será substituída quando uma fonte não estiver disponível no computador do cliente.

O valor padrão é `com/adobe/formServer/client-font-map.properties`.

A entrada a seguir é um exemplo de uma entrada no arquivo de mapeamento de fontes:

`Arial=Arial,Helvetica,sans-serif`

**Arquivo de PDF de propagação:** o arquivo de PDF inicial usado em uma transformação PDFForm para otimizar a entrega. O arquivo de PDF de propagação especifica um arquivo de PDF personalizado (contendo apenas recursos de fluxo, imagem e fonte XFA) que é anexado com o design e os dados do formulário. O formulário é renderizado pelo Acrobat 7 ou posterior e se aplica à transformação de PDForm.

O valor padrão é uma string vazia.

**Local do Cache:** Especifica o local do cache de disco do Forms. Ao alterar essa configuração, todas as informações de cache existentes no local atual são redefinidas e um novo cache é criado no novo local. Selecione uma das seguintes opções:

**Local Padrão:** Esta é a seleção padrão. Quando essa opção é selecionada, o cache é criado em um local dependente do servidor de aplicativos que você está usando:

* **JBoss:** [JBoss Home]\server\[instalar tipo]\svcdata\FormServer\Cache
* **WebLogic:** [WebLogic Home]\user_projects\domains\[Nome de Domínio do aem-forms]\adobe\[Nome do Servidor do Forms]\FormServer\Cache
* **WebSphere:** [IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Diretório Temp da LC:** O cache é criado em um subdiretório do diretório temp de formulários AEM, que é especificado no console de administração em Configurações > Configurações do Sistema Principal > Configurações > Localização do Diretório Temp. O subdiretório é denominado adobeform_[servername].

>[!NOTE]
>
>Se você estiver usando um utilitário de limpeza temporário, embora a exclusão desses diretórios não afete a funcionalidade, ele pode afetar significativamente o desempenho por um curto período até que o novo cache seja criado. Para evitar esse problema, não exclua esses diretórios enquanto limpa o diretório temporário dos formulários AEM.
