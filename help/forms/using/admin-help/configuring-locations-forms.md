---
title: Configuração de localizações para Forms
seo-title: Configuring locations for Forms
description: Saiba como configurar a localização do Forms.
seo-description: Learn how to configure location for Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# Configuração de localizações para Forms {#configuring-locations-for-forms}

Você pode especificar o URL, o URI e os locais dos atributos do arquivo, como a raiz da Web, o local dos formulários a serem recuperados, o arquivo de PDF de propagação usado nas transformações do PDFForm e o local do cache.

1. No console de administração, clique em Serviços > Forms.
1. Em Locais, especifique as opções apropriadas. As opções estão descritas abaixo.
1. Clique em Salvar.

## Configurações de localizações {#locations-settings}

**URL base:** O URL base onde os recursos do formulário, como imagens e scripts, estão localizados. Esse valor é necessário para transformações de HTML que incluem referências HREF a dependências externas, como imagens ou scripts. Um desses scripts é xfasubset.js, que é necessário para que formulários HTML executem inteligência XFA. Esse valor deve ser o equivalente HTTP do URI da raiz do conteúdo.

>[!NOTE]
>
>O URL base suporta apenas protocolos HTTP ou de repositório. Ele não é compatível com protocolos como file:///. Se você precisar acessar um recurso, como um CSS personalizado ou um URI de assinatura digital, use o valor de parâmetro de API apropriado para especificar o local absoluto.

Quando um caminho de dependência é absoluto, o valor do URL básico é ignorado. Caso contrário, o caminho de dependência será combinado com o URL base.

O valor padrão é uma string vazia.

O exemplo a seguir aponta para o mesmo conteúdo (usando o URL de raiz de conteúdo e o URL de base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI raiz da Web FS:** O URL do aplicativo Web do Forms. Você pode deixar essa caixa vazia se o aplicativo Web Forms e o aplicativo cliente estiverem implantados no mesmo servidor de aplicativos; o URL raiz da Web da API do Forms será usado.

Se o aplicativo Web do Forms e o aplicativo cliente não forem implantados no mesmo servidor de aplicativos, forneça o URL do aplicativo Web do Forms nesta caixa, como mostrado neste exemplo:

`https://<host name>:<port>/FormServer`

Onde `host name`e `port` são o nome do servidor e o número da porta do servidor que está hospedando o aplicativo web Forms.

O valor padrão é uma string vazia.

**URI raiz da Web:** A raiz da Web do aplicativo. Esse valor é combinado com o parâmetro sTargetURL (quando sTargetURL é fornecido como relativo), especificado por meio do SDK dos formulários AEM, para construir um URL absoluto para acessar o conteúdo da Web específico do aplicativo.

O valor padrão é uma string vazia.

**URI raiz do conteúdo:** O URI ou local absoluto do qual os formulários são recuperados. Esse valor é combinado com o parâmetro sFormQuery, especificado por meio da API, para construir o caminho absoluto para o formulário que é recuperado. Esse valor pode referenciar um diretório ou um local da Web acessível por meio de HTTP.

O valor padrão é uma string vazia.

**URI de configuração XCI:** O local relativo ou absoluto no qual o arquivo XCI usado para renderização é encontrado. Para um valor relativo, presume-se que o arquivo XCI reside no arquivo EAR de formulários AEM implantáveis.

O valor padrão é `com/adobe/formServer/PA/pa.xci`.

**URI do mapa de fontes:** O local relativo ou absoluto do arquivo de mapeamento de fonte. Para um valor relativo, presume-se que esse arquivo reside no arquivo EAR de formulários AEM implantáveis.

O arquivo de mapeamento de fonte é usado para criar mapeamentos de fonte personalizados para transformações de HTML nos formulários, permitindo, portanto, especificar qual fonte será substituída quando uma fonte não estiver disponível no computador do cliente.

O valor padrão é `com/adobe/formServer/client-font-map.properties`.

A entrada a seguir é um exemplo de uma entrada no arquivo de mapeamento de fonte:

`Arial=Arial,Helvetica,sans-serif`

**Arquivo PDF Seed:** O arquivo PDF inicial usado em uma transformação PDFForm para otimizar a entrega. O arquivo seed PDF especifica um arquivo PDF personalizado (contendo somente fluxo XFA, imagem e recursos de fonte) que é anexado ao design de formulário e aos dados. O formulário é renderizado pelo Acrobat 7 ou por uma versão posterior e se aplica à transformação PDFForm.

O valor padrão é uma string vazia.

**Localização do Cache:** Especifica o local do cache de disco do Forms. Quando você altera essa configuração, todas as informações de cache existentes no local atual são redefinidas e um novo cache é criado no novo local. Selecione uma destas opções:

**Localização padrão:** Esta é a seleção padrão. Quando essa opção é selecionada, o cache é criado em um local que depende do servidor de aplicativos que você está usando:

* **JBoss:** [Página inicial do JBoss]\server\[tipo de instalação]\svcdata\FormServer\Cache
* **WebLogic:** [Página inicial do WebLogic]\user_projects\domains\[nome de domínio do aem-forms]\adobe\[nome do servidor do forms]\FormServer\Cache
* **WebSphere:** [Página inicial do IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Diretório Temp LC:** O cache é criado em um subdiretório do diretório temporário AEM forms, que é especificado no console de administração em Configurações > Configurações do sistema principal > Configurações > Localização do diretório Temp. O subdiretório é denominado adobeform_[servername].

>[!NOTE]
>
>Se você estiver usando um utilitário de limpeza temporária, tenha em mente que, ao excluir esses diretórios, não afeta a funcionalidade, isso pode afetar significativamente o desempenho por um curto período de tempo até que o novo cache seja criado. Para evitar esse problema, não exclua esses diretórios enquanto limpa o diretório temporário dos formulários AEM.
