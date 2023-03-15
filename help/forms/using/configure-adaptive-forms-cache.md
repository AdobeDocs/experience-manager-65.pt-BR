---
title: Configurar o cache de formulários adaptáveis
seo-title: Configure adaptive forms cache
description: O cache de formulários adaptáveis foi projetado especificamente para formulários e documentos adaptáveis. Armazena em cache formulários adaptáveis e documentos adaptáveis com o objetivo de reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente.
seo-description: The adaptive forms cache is designed specifically for adaptive forms and documents. It caches adaptive forms and adaptive documents with the objective of reducing the time required to render an adaptive form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# Configurar o cache de formulários adaptáveis {#configure-adaptive-forms-cache}

Um cache é um mecanismo para reduzir o tempo de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (I/O). O cache de formulários adaptáveis armazena somente o conteúdo de HTML e a estrutura JSON de um formulário adaptável sem salvar dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável no cliente. Ele foi projetado especificamente para formulários adaptáveis.

## Configurar o cache de formulários adaptáveis nas instâncias de criação e publicação {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vá para AEM gerenciador de configuração do console da Web em `https://[server]:[port]/system/console/configMgr`.
1. Clique em **[!UICONTROL Configuração do canal Web de comunicação interativa e formulário adaptável]** para editar seus valores de configuração.
1. No [!UICONTROL editar valores de configuração] , especifique o número máximo de formulários ou documentos que uma instância do AEM [!DNL Forms] O servidor pode armazenar em cache no **[!UICONTROL Número de Forms adaptáveis]** campo. O valor padrão é 100.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Number of Adaptive Forms como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

   ![Caixa de diálogo Configuração para cache HTML de formulários adaptáveis](assets/cache-configuration-edit.png)

1. Clique em **[!UICONTROL Salvar]** para salvar a configuração.

Seu ambiente é configurado para usar formulários adaptáveis ao cache e ativos relacionados.


## (Opcional) Configurar o cache de formulário adaptável no dispatcher {#configure-the-cache}

Você também pode configurar o armazenamento de formulários adaptáveis no dispatcher para aumentar ainda mais o desempenho.

### Pré-requisitos {#pre-requisites}

* Ative o [mesclagem ou preenchimento prévio de dados no cliente](prepopulate-adaptive-form-fields.md#prefill-at-client) opção. Ajuda a unir dados exclusivos para cada instância de um formulário pré-preenchido.

### Considerações para armazenar formulários adaptáveis em cache em um dispatcher {#considerations}

* Ao usar o cache de formulários adaptáveis, use o AEM [!DNL Dispatcher] para armazenar em cache bibliotecas de clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, no servidor usado para desenvolvimento, mantenha o cache de formulários adaptáveis desativado.
* URLs sem extensão não são armazenados em cache. Por exemplo, URL com padrão`/content/forms/[folder-structure]/[form-name].html` são armazenadas em cache e o armazenamento em cache ignora URLs com padrão `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Portanto, use URLs com extensões para aproveitar os benefícios do armazenamento em cache.
* Considerações para formulários adaptáveis localizados:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Desabilitar usando a localidade do navegador](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) para URLs com formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Ao usar o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL Usar a localidade do navegador]** no gerenciador de configuração estiver desativado, a versão não localizada do formulário adaptável será fornecida. O idioma não localizado é o idioma usado durante o desenvolvimento do formulário adaptável. O local configurado para seu navegador (localidade do navegador) não é considerado e uma versão não localizada do formulário adaptável é disponibilizada.
   * Ao usar o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL Usar a localidade do navegador]** no gerenciador de configuração estiver ativado, uma versão localizada do formulário adaptável será disponibilizada, se disponível. O idioma do formulário adaptável localizado é baseado na localidade configurada para seu navegador (localidade do navegador). Pode levar a [armazenamento em cache somente da primeira instância de um formulário adaptável]. Para evitar que o problema ocorra em sua instância, consulte [solução de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Habilitar o armazenamento em cache no dispatcher

Execute as etapas listadas abaixo para habilitar e configurar o armazenamento em cache de formulários adaptáveis no dispatcher:

1. Abra o seguinte URL para cada instância de publicação do seu ambiente e [ativar o agente de limpeza para publicar instâncias do seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Adicione o seguinte ao arquivo dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

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

   * Quando uma versão mais recente do recurso referenciado em um formulário adaptável é publicada, os formulários adaptáveis afetados são automaticamente invalidados. Há algumas exceções para a invalidação automática dos recursos referenciados. Para obter uma solução alternativa para exceções, consulte [solução de problemas](#troubleshooting) seção.
1. [Adicione o arquivo de regras abaixo dispatcher.any ou personalizado](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache). Ela exclui os URLs que não oferecem suporte ao armazenamento em cache. Por exemplo, Comunicação interativa.

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

1. [Adicione os seguintes parâmetros à lista ignorar parâmetros de URL](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Seu ambiente de AEM é configurado para armazenar formulários adaptáveis em cache. Armazena em cache todos os tipos de formulários adaptáveis. Se você tiver um requisito para verificar as permissões de acesso do usuário para uma página antes de entregar a página em cache, consulte [armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR).

## Resolução de problemas {#troubleshooting}

### Alguns formulários adaptáveis contendo imagens ou vídeos não são invalidados automaticamente do cache do dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Ao selecionar e adicionar imagens ou vídeos por meio do navegador de ativos a um formulário adaptável e essas imagens e vídeos forem editados no editor de Ativos, os formulários adaptáveis contendo essas imagens não serão invalidados do cache do dispatcher automaticamente.

#### Solução {#Solution1}

Após publicar as imagens e o vídeo, desfaça a publicação e publique explicitamente os formulários adaptáveis que fazem referência a esses ativos.

### Somente a primeira instância de um formulário adaptável é armazenada em cache {#only-first-instance-of-adaptive-forms-is-cached}

#### Problema {#issue3}

Quando a URL do formulário adaptável não tiver informações de localização, e **[!UICONTROL Usar a localidade do navegador]** no gerenciador de configuração estiver ativado, uma versão localizada do formulário adaptável será disponibilizada e somente a primeira instância do formulário adaptável será armazenada em cache e entregue a cada usuário subsequente.

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
