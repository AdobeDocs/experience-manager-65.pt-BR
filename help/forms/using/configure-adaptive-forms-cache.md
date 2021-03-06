---
title: Configurar o cache de formulários adaptáveis
seo-title: Configurar o cache de formulários adaptáveis
description: 'O cache de formulários adaptáveis foi projetado especificamente para formulários e documentos adaptáveis. Armazena em cache formulários adaptáveis e documentos adaptáveis com o objetivo de reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente. '
seo-description: 'O cache de formulários adaptáveis foi projetado especificamente para formulários e documentos adaptáveis. Armazena em cache formulários adaptáveis e documentos adaptáveis com o objetivo de reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 1%

---

# Configurar o cache de formulários adaptáveis {#configure-adaptive-forms-cache}

Um cache é um mecanismo para reduzir o tempo de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (I/O). O cache de formulários adaptáveis armazena somente o conteúdo HTML e a estrutura JSON de um formulário adaptável sem salvar dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável no cliente. Ele foi projetado especificamente para formulários adaptáveis.

## Configurar o cache de formulários adaptáveis nas instâncias de criação e publicação {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vá para AEM gerenciador de configuração do console da Web em `https://[server]:[port]/system/console/configMgr`.
1. Clique em **[!UICONTROL Adaptive Form e Interative Communication Web Channel Configuration]** para editar seus valores de configuração.
1. Na caixa de diálogo [!UICONTROL editar valores de configuração], especifique o número máximo de formulários ou documentos que uma instância do servidor AEM [!DNL Forms] pode armazenar em cache no campo **[!UICONTROL Número do Adaptive Forms]**. O valor padrão é 100.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Number of Adaptive Forms como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

   ![Caixa de diálogo Configuração para formulários adaptáveis cache HTML](assets/cache-configuration-edit.png)

1. Clique em **[!UICONTROL Save]** para salvar a configuração.

Seu ambiente é configurado para usar formulários adaptáveis ao cache e ativos relacionados.


## (Opcional) Configurar o cache de formulário adaptável no dispatcher {#configure-the-cache}

Você também pode configurar o armazenamento de formulários adaptáveis no dispatcher para aumentar ainda mais o desempenho.

### Pré-requisitos {#pre-requisites}

* Habilite a opção [mesclar ou preencher previamente dados no cliente](prepopulate-adaptive-form-fields.md#prefill-at-client). Ajuda a unir dados exclusivos para cada instância de um formulário pré-preenchido.

### Considerações para armazenar formulários adaptáveis em cache em um dispatcher {#considerations}

* Ao usar o cache de formulários adaptáveis, use o AEM [!DNL Dispatcher] para armazenar em cache as bibliotecas de clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, no servidor usado para desenvolvimento, mantenha o cache de formulários adaptáveis desativado.
* URLs sem extensão não são armazenados em cache. Por exemplo, URL com padrão`/content/forms/[folder-structure]/[form-name].html` são armazenadas em cache e o armazenamento em cache ignora URLs com padrão `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Portanto, use URLs com extensões para aproveitar os benefícios do armazenamento em cache.
* Considerações para formulários adaptáveis localizados:
   * Use o formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Desative o uso de ](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) localidade do navegador para URLs com formato  `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Quando você usa o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html` e **[!UICONTROL Usar Localidade do Navegador]** no gerenciador de configuração estiver desativado, a versão não localizada do formulário adaptável será exibida. O idioma não localizado é o idioma usado durante o desenvolvimento do formulário adaptável. O local configurado para seu navegador (localidade do navegador) não é considerado e uma versão não localizada do formulário adaptável é disponibilizada.
   * Quando você usa o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html` e **[!UICONTROL Usar Localidade do Navegador]** no gerenciador de configuração estiver ativado, uma versão localizada do formulário adaptável será disponibilizada, se disponível. O idioma do formulário adaptável localizado é baseado na localidade configurada para seu navegador (localidade do navegador). Isso pode levar a [armazenar em cache somente a primeira instância de um formulário adaptável]. Para evitar que o problema ocorra em sua instância, consulte [solução de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Habilitar o armazenamento em cache no dispatcher

Execute as etapas listadas abaixo para habilitar e configurar o armazenamento em cache de formulários adaptáveis no dispatcher:

1. Abra o seguinte URL para cada instância de publicação de seu ambiente e [habilite o agente de limpeza para instâncias de publicação de seu ambiente](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Adicione o seguinte ao arquivo](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files) dispatcher.any:

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   Ao adicionar o acima:

   * Um formulário adaptável permanece em cache até que uma versão atualizada do formulário não seja publicada.

   * Quando uma versão mais recente do recurso referenciado em um formulário adaptável é publicada, os formulários adaptáveis afetados são automaticamente invalidados. Há algumas exceções para a invalidação automática dos recursos referenciados. Para obter uma solução alternativa para exceções, consulte a seção [solução de problemas](#troubleshooting).
1. [Adicione o arquivo](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache) de regras abaixo dispatcher.any ou custom rules. Ela exclui os URLs que não oferecem suporte ao armazenamento em cache. Por exemplo, Comunicação interativa.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Adicione os seguintes parâmetros à lista](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters) Ignorar parâmetros de URL :

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Seu ambiente de AEM é configurado para armazenar formulários adaptáveis em cache. Armazena em cache todos os tipos de formulários adaptáveis. Se você tiver um requisito para verificar as permissões de acesso do usuário para uma página antes de entregar a página em cache, consulte [armazenamento em cache de conteúdo protegido](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Resolução de problemas {#troubleshooting}

### Alguns formulários adaptáveis contendo imagens ou vídeos não são invalidados automaticamente do cache do dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Ao selecionar e adicionar imagens ou vídeos por meio do navegador de ativos a um formulário adaptável e essas imagens e vídeos forem editados no editor de Ativos, os formulários adaptáveis contendo essas imagens não serão invalidados do cache do dispatcher automaticamente.

#### Solução {#Solution1}

Após publicar as imagens e o vídeo, desfaça a publicação e publique explicitamente os formulários adaptáveis que fazem referência a esses ativos.

### Somente a primeira instância de um formulário adaptável é armazenada em cache {#only-first-instance-of-adaptive-forms-is-cached}

#### Problema {#issue3}

Quando a URL do formulário adaptável não tiver informações de localização e **[!UICONTROL Usar Localidade do Navegador]** no gerenciador de configuração estiver ativado, uma versão localizada do formulário adaptável será fornecida e somente a primeira instância do formulário adaptável será armazenada em cache e entregue a cada usuário subsequente.

#### Solução {#Solution3}

Execute as seguintes etapas para resolver o problema:

1. Abra o conf.d/httpd-dispatcher.conf ou qualquer outro arquivo de configuração configurado para carregar no tempo de execução.

1. Adicione o seguinte código ao arquivo e salve-o. É um código de amostra para modificá-lo de acordo com seu ambiente.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
