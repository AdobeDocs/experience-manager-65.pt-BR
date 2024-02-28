---
title: Suporte a novos códigos de idiomas para localização de formulários adaptáveis
description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptáveis. Os locais suportados por padrão são inglês, francês, alemão e japonês.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
feature: Adaptive Forms
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: d195ac80ee59439bab5b1219a2c1f16e93e3d22b
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---

# Suporte a novos códigos de idiomas para localização de formulários adaptáveis{#supporting-new-locales-for-adaptive-forms-localization}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization.html) |
| AEM 6.5 | Este artigo |

## Sobre dicionários de local {#about-locale-dictionaries}

A localização de formulários adaptáveis depende de dois tipos de dicionários de localidade:

**Dicionário específico de formulário** Contém strings usadas em formulários adaptáveis. Por exemplo, rótulos, nomes de campos, mensagens de erro, descrições de ajuda e assim por diante. Ele é gerenciado como um conjunto de arquivos XLIFF para cada local e você pode acessá-lo em `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Dicionários globais** Há dois dicionários globais, gerenciados como objetos JSON, na biblioteca do cliente AEM. Esses dicionários contêm mensagens de erro padrão, nomes de meses, símbolos de moeda, padrões de data e hora e assim por diante. Você pode encontrar esses dicionários no CRXDe Lite em /libs/fd/xfaforms/clientlibs/I18N. Esses locais contêm pastas separadas para cada local. Como os dicionários globais geralmente não são atualizados com frequência, manter arquivos JavaScript separados para cada localidade permite que os navegadores os armazenem em cache e reduzam o uso da largura de banda da rede ao acessar diferentes formulários adaptáveis no mesmo servidor.

### Como funciona a localização do formulário adaptável {#how-localization-of-adaptive-form-works}

Há dois métodos para identificar o local do formulário adaptável. Quando um formulário adaptável é renderizado, ele identifica o local solicitado por:

* olhando para o `[local]` no URL do formulário adaptável. O formato do URL é `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Usar `[local]` O seletor permite armazenar em cache um formulário adaptável.

* observando os seguintes parâmetros na ordem especificada:

   * Parâmetro de solicitação `afAcceptLang`
Para substituir a localidade do navegador dos usuários, você pode transmitir a `afAcceptLang` parâmetro de solicitação para forçar a localidade. Por exemplo, a URL a seguir foi forçada a renderizar o formulário no local japonês:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * A localidade do navegador definida para o usuário, que é especificada na solicitação usando o `Accept-Language` cabeçalho.

   * Configuração de idioma do usuário especificado no AEM.

   * A localidade do navegador é ativada por padrão. Para alterar a configuração do local do navegador,
      * Abra o gerenciador de configurações. O URL é `http://[server]:[port]/system/console/configMgr`
      * Localize e abra o **[!UICONTROL Canal da Web de formulário adaptável e comunicação interativa]** configuração.
      * Alterar status da **[!UICONTROL Usar localidade do navegador]** opção e  **[!UICONTROL Salvar]** a configuração.

Depois que a localidade é identificada, os formulários adaptáveis escolhem o dicionário específico do formulário. Se o dicionário específico do formulário para a localidade solicitada não for encontrado, ele usará o dicionário do idioma no qual o formulário adaptável foi criado.

Se nenhuma informação de local estiver presente, o formulário adaptável será entregue no idioma original do formulário. O idioma original é o idioma usado ao desenvolver o formulário adaptável.

Se não existir uma biblioteca do cliente para a localidade solicitada, ela verificará se há uma biblioteca do cliente para o código de idioma presente na localidade. Por exemplo, se o local solicitado for `en_ZA` (inglês da África do Sul) e a biblioteca do cliente para `en_ZA` não existir, o formulário adaptável usará a biblioteca do cliente para `en` Idioma (inglês), se existir. No entanto, se nenhum deles existir, o formulário adaptável usará o dicionário para `en` localidade.

## Adicionar suporte de localização para localidades sem suporte {#add-localization-support-for-non-supported-locales}

Atualmente, o AEM Forms oferece suporte à localização de conteúdo de formulários adaptáveis em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR).

Para adicionar suporte para um novo local no tempo de execução dos formulários adaptáveis:

1. [Adicionar uma localidade ao serviço GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Adicionar biblioteca do cliente XFA para uma localidade](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Adicionar biblioteca de cliente de formulário adaptável para uma localidade](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Adicionar suporte de localidade para o dicionário](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Reiniciar o servidor](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Adicionar uma localidade ao serviço de Localização do Guia {#add-a-locale-to-the-guide-localization-service-br}

1. Acesse `https://'[server]:[port]'/system/console/configMgr`.
1. Clique para editar o **Serviço de localização do guia** componente.
1. Adicione a localidade que deseja adicionar à lista de localidades suportadas.

![GuiaServiçoDeLocalização](assets/configservice.png)

### Adicionar biblioteca do cliente XFA para uma localidade {#add-xfa-client-library-for-a-locale-br}

Criar um nó do tipo `cq:ClientLibraryFolder` em `etc/<folderHierarchy>`, com categoria `xfaforms.I18N.<locale>`e adicione os seguintes arquivos à biblioteca do cliente:

* **I18N.js** definindo `xfalib.locale.Strings` para o `<locale>` conforme definido em `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** contendo o seguinte:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Adicionar biblioteca de cliente de formulário adaptável para uma localidade {#add-adaptive-form-client-library-for-a-locale-br}

Criar um nó do tipo `cq:ClientLibraryFolder` em `etc/<folderHierarchy>`, com a categoria como `guides.I18N.<locale>` e dependências como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`. &quot;

Adicione os seguintes arquivos à biblioteca do cliente:

* **i18n.js** definindo `guidelib.i18n`, com padrões de &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para o `<locale>` de acordo com as especificações XFA descritas em [Especificação do conjunto de localidades](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). Você também pode ver como ele é definido para outras localidades compatíveis no `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definindo `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` para o `<locale>` conforme definido em `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** contendo o seguinte:

```text
i18n.js
LogMessages.js
```

### Adicionar suporte de localidade para o dicionário {#add-locale-support-for-the-dictionary-br}

Execute esta etapa somente se a variável `<locale>` você está adicionando não está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Criar um `nt:unstructured` nó `languages` em `etc`, se ainda não estiver presente.

1. Adicionar uma propriedade de cadeia de caracteres de vários valores `languages` ao nó, se ainda não estiver presente.
1. Adicione o `<locale>` valores de localidade padrão `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se ainda não estiver presente.

1. Adicione o `<locale>` aos valores de `languages` propriedade de `/etc/languages`.

A variável `<locale>` aparecerá em `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Reiniciar o servidor {#restart-the-server}

Reinicie o servidor AEM para que a localidade adicionada entre em vigor.

>[!NOTE]
>
> É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Bibliotecas de exemplo para adicionar suporte ao espanhol {#sample-libraries-for-adding-support-for-spanish}

Exemplos de bibliotecas de clientes para adicionar suporte para espanhol

[Obter arquivo](assets/sample.zip)
