---
title: Configurar cache de formulários adaptáveis
description: O cache de formulários adaptáveis foi projetado especificamente para formulários e documentos adaptáveis. Ele armazena em cache formulários adaptáveis e documentos adaptáveis com o objetivo de reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---

# Configurar cache de formulários adaptáveis {#configure-adaptive-forms-cache}

Um cache é um mecanismo para reduzir os tempos de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (E/S). O cache de formulários adaptáveis armazena somente o conteúdo de HTML e a estrutura JSON de um formulário adaptável sem salvar os dados preenchidos previamente. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável no cliente. Ele foi projetado especificamente para formulários adaptáveis.

## Configurar o cache de formulários adaptáveis nas instâncias de criação e publicação {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vá para o gerenciador de configuração do console da Web AEM em `https://[server]:[port]/system/console/configMgr`.
1. Clique em **[!UICONTROL Configuração do canal da Web do formulário adaptável e da comunicação interativa]** para editar seus valores de configuração.
1. Na caixa de diálogo [!UICONTROL editar valores de configuração], especifique o número máximo de formulários ou documentos que uma instância do servidor AEM [!DNL Forms] pode armazenar em cache no campo **[!UICONTROL Número de Forms Adaptável]**. O valor padrão é 100.

   >[!NOTE]
   >
   >Para desabilitar o cache, defina o valor no campo Número de Forms Adaptáveis como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

   ![Caixa de diálogo de configuração para cache de HTML de formulários adaptáveis](assets/cache-configuration-edit.png)

1. Clique em **[!UICONTROL Salvar]** para salvar a configuração.

Seu ambiente está configurado para usar formulários adaptáveis em cache e ativos relacionados.


## (Opcional) Configurar o cache de formulários adaptáveis no Dispatcher {#configure-the-cache}

Você também pode configurar o cache de formulários adaptáveis no Dispatcher para aumentar ainda mais o desempenho.

### Pré-requisitos {#pre-requisites}

* Habilite a opção [mesclar ou preencher dados previamente no cliente](prepopulate-adaptive-form-fields.md#prefill-at-client). Ele ajuda a mesclar dados exclusivos para cada instância de um formulário pré-preenchido.

### Considerações para o armazenamento em cache de formulários adaptáveis em uma Dispatcher {#considerations}

* Ao usar o cache de formulários adaptáveis, use o AEM [!DNL Dispatcher] para armazenar em cache bibliotecas de clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, no servidor usado para desenvolvimento, mantenha o cache de formulários adaptáveis desativado.
* Os URLs sem extensão não são armazenados em cache. Por exemplo, a URL com padrão `/content/forms/[folder-structure]/[form-name].html` é armazenada em cache e o armazenamento em cache ignora URLs com padrão `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Portanto, use URLs com extensões para aproveitar os benefícios do armazenamento em cache.
* Considerações para formulários adaptáveis localizados:
   * Use o formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Desabilitar usando localidade do navegador](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) para URLs com formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Quando você usa o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html` e **[!UICONTROL Usar Localidade do Navegador]** no gerenciador de configurações está desabilitado, a versão não localizada do formulário adaptável é fornecida. O idioma não localizado é o idioma usado no desenvolvimento do formulário adaptável. A localidade configurada para seu navegador (localidade do navegador) não é considerada e uma versão não localizada do formulário adaptável é fornecida.
   * Quando você usa o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html` e **[!UICONTROL Usar Localidade do Navegador]** no gerenciador de configurações está habilitado, uma versão localizada do formulário adaptável é fornecida, se disponível. O idioma do formulário adaptável localizado se baseia no local configurado para seu navegador (local do navegador). Isso pode levar ao [armazenamento em cache somente a primeira instância de um formulário adaptável]. Para evitar que o problema ocorra em sua instância, consulte [solução de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Ativar o armazenamento em cache no Dispatcher

Para ativar e configurar o armazenamento em cache de formulários adaptáveis no Dispatcher, execute as seguintes etapas:

1. Abra a seguinte URL para cada instância de publicação do seu ambiente e [habilite o agente de limpeza para instâncias de publicação do seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=pt-BR#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Adicione o seguinte ao arquivo dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#automatically-invalidating-cached-files):

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

   * Um formulário adaptável permanece no cache até que uma versão atualizada do formulário não seja publicada.

   * Quando uma versão mais recente de um recurso referenciado em um formulário adaptável é publicada, os formulários adaptáveis afetados são invalidados automaticamente. Há algumas exceções à invalidação automática de recursos referenciados. Para obter uma solução alternativa para as exceções, consulte a seção [solução de problemas](#troubleshooting).
1. [Adicione o arquivo de regras dispatcher.any abaixo ou o arquivo de regras personalizado](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#specifying-the-documents-to-cache). Ela exclui os URLs que não oferecem suporte ao armazenamento em cache. Por exemplo, Comunicação interativa.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Do not cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Do not cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Do not cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Adicionar os seguintes parâmetros à lista de parâmetros de URL ignorados](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Seu ambiente AEM está configurado para armazenar formulários adaptáveis em cache. Armazena em cache todos os tipos de formulários adaptáveis. Se você precisar verificar as permissões de acesso do usuário para uma página antes de entregar a página em cache, consulte [armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR).

## Resolução de problemas {#troubleshooting}

### Alguns formulários adaptáveis contendo imagens ou vídeos não são invalidados automaticamente do cache do Dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Ao selecionar e adicionar imagens ou vídeos por meio do navegador de ativos a um formulário adaptável e essas imagens e vídeos forem editados no editor do Assets, os formulários adaptáveis que contêm essas imagens não são invalidados do cache do Dispatcher automaticamente.

#### Solução {#Solution1}

Após a publicação das imagens e do vídeo, cancele explicitamente a publicação e publique os formulários adaptáveis que fazem referência a esses ativos.

### Somente a primeira instância de um formulário adaptável é armazenada em cache {#only-first-instance-of-adaptive-forms-is-cached}

#### Problema {#issue3}

Quando a URL do formulário adaptável não tiver informações de localização e a **[!UICONTROL Localidade do Navegador de Uso]** estiver habilitada no gerenciador de configurações, uma versão localizada do formulário adaptável será fornecida. Somente a primeira instância do formulário adaptável é armazenada em cache e entregue a cada usuário subsequente.

#### Solução {#Solution3}

Resolva o problema executando as seguintes etapas:

1. Abra o arquivo conf.d/httpd-dispatcher.conf ou qualquer outro arquivo de configuração configurado para ser carregado no tempo de execução.

1. Adicione o código a seguir ao arquivo e salve-o. É uma amostra de código, modifique-a para atender ao seu ambiente.

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
