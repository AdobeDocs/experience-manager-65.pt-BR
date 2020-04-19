---
title: Configurar locais para o Forms
seo-title: Configurar locais para o Forms
description: Saiba como configurar a localização para o Forms.
seo-description: Saiba como configurar a localização para o Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Configurar locais para o Forms {#configuring-locations-for-forms}

Você pode especificar o URL, o URI e os locais de arquivos dos atributos, como a raiz da Web, o local dos formulários a serem recuperados, o arquivo PDF semente usado nas transformações do PDFForm e o local do cache.

1. No console de administração, clique em Serviços > Formulários.
1. Em Locais, especifique as opções apropriadas. As opções estão descritas abaixo.
1. Clique em Salvar.

## Configurações de locais {#locations-settings}

**URL de base:** O URL básico no qual os recursos do formulário, como imagens e scripts, estão localizados. Esse valor é necessário para transformações HTML que incluem referências HREF a dependências externas, como imagens ou scripts. Um desses scripts é xfasubset.js, que é necessário para que formulários HTML executem inteligência XFA. Esse valor deve ser o equivalente HTTP do URI raiz do conteúdo.

>[!NOTE]
>
>O URL básico suporta apenas protocolos HTTP ou de repositório. Ele não oferece suporte a protocolos como file:///. Se você precisar acessar um recurso, como um CSS personalizado ou um URI de assinatura digital, use o valor de parâmetro de API apropriado para especificar o local absoluto.

Quando um caminho de dependência é absoluto, o valor do URL básico é ignorado. Caso contrário, o caminho de dependência é combinado com o URL base.

O valor padrão é uma string vazia.

O exemplo a seguir aponta para o mesmo conteúdo (usando o URI raiz do conteúdo e o URL básico):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI raiz da Web FS:** O URL do aplicativo da Web Forms. Você pode deixar essa caixa vazia se o aplicativo da Web Forms e o aplicativo cliente estiverem implantados no mesmo servidor de aplicativos; o URL raiz da Web da API do Forms será usado.

Se o aplicativo da Web Forms e o aplicativo cliente não estiverem implantados no mesmo servidor de aplicativos, forneça o URL para o aplicativo da Web Forms nesta caixa, como mostra este exemplo:

`https://<host name>:<port>/FormServer`

Onde `host name`e `port` é o nome do servidor e o número da porta do servidor que está hospedando o aplicativo da Web Forms.

O valor padrão é uma string vazia.

**URI raiz da Web:** A raiz da Web do aplicativo. Esse valor é combinado com o parâmetro sTargetURL (quando sTargetURL é fornecido como relativo), especificado por meio do SDK de formulários AEM, para criar um URL absoluto para acessar conteúdo da Web específico do aplicativo.

O valor padrão é uma string vazia.

**URI raiz do conteúdo:** O URI ou o local absoluto do qual os formulários são recuperados. Esse valor é combinado com o parâmetro sFormQuery, especificado por meio da API, para construir o caminho absoluto para o formulário recuperado. Esse valor pode fazer referência a um diretório ou a um local da Web acessível por meio de HTTP.

O valor padrão é uma string vazia.

**URI de configuração XCI:** O local relativo ou absoluto no qual o arquivo XCI usado para renderização é encontrado. Para obter um valor relativo, presume-se que o arquivo XCI reside no arquivo AEM de formulários AEM implantáveis.

O valor padrão é `com/adobe/formServer/PA/pa.xci`.

**URI do mapa de fontes:** O local relativo ou absoluto do arquivo de mapeamento de fontes. Para um valor relativo, presume-se que esse arquivo reside no arquivo AEM de formulários AEM implantável.

O arquivo de mapeamento de fontes é usado para criar mapeamentos de fontes personalizados para transformações HTML em formulários, portanto, permite especificar qual fonte será substituída quando uma fonte não estiver disponível no computador do cliente.

O valor padrão é `com/adobe/formServer/client-font-map.properties`.

A entrada a seguir é um exemplo de uma entrada no arquivo de mapeamento de fontes:

`Arial=Arial,Helvetica,sans-serif`

**Seed PDF File:** O arquivo PDF inicial usado em uma transformação PDFForm para otimizar o delivery. O arquivo PDF semente especifica um arquivo PDF personalizado (contendo apenas recursos de fluxo XFA, imagem e fonte) que é anexado ao design de formulário e aos dados. O formulário é renderizado pelo Acrobat 7 ou posterior e se aplica à transformação PDFForm.

O valor padrão é uma string vazia.

**Localização do Cache:** Especifica o local do cache em disco do Forms. Quando você altera essa configuração, todas as informações de cache existentes no local atual são redefinidas e um novo cache é criado no novo local. Selecione uma destas opções:

**Local padrão:** Esta é a seleção padrão. Quando essa opção é selecionada, o cache é criado em um local que depende do servidor de aplicativos que você está usando:

* **JBoss:** Página inicial do [JBoss]\server\[tipo de instalação]\svcdata\FormServer\Cache
* **WebLogic:** Página inicial [do]WebLogic \user_projects\domains\[nome de domínio de formulários-AEM]\adobe\[nome do servidor de formulários]\FormServer\Cache
* **WebSphere:** [IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Diretório temporário LC:** O cache é criado em um subdiretório do diretório temporário para formulários AEM, que é especificado no console de administração em Configurações > Configurações principais do sistema > Configurações > Localização do diretório temporário. O subdiretório é nomeado adobeform_[servername].

>[!NOTE]
>
>Se você estiver usando um utilitário de limpeza temporária, lembre-se de que ao excluir esses diretórios não afeta a funcionalidade, isso pode afetar significativamente o desempenho por pouco tempo até que o novo cache seja criado. Para evitar esse problema, não exclua esses diretórios enquanto limpa o diretório temporário de formulários AEM.

