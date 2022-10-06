---
title: Suporte a novas localidades para localização de formulários adaptáveis
seo-title: Supporting new locales for adaptive forms localization
description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptáveis. Por padrão, as localidades compatíveis são inglês, francês, alemão e japonês.
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. The supported locales by default are English, French, German, and Japanese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: Adaptive Forms
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Suporte a novas localidades para localização de formulários adaptáveis{#supporting-new-locales-for-adaptive-forms-localization}

## Sobre dicionários de localidades {#about-locale-dictionaries}

A localização de formulários adaptáveis depende de dois tipos de dicionários de localidade:

**Dicionário específico do formulário** Contém strings usadas em formulários adaptáveis. Por exemplo, rótulos, nomes de campo, mensagens de erro, descrições de ajuda e assim por diante. Ele é gerenciado como um conjunto de arquivos XLIFF para cada localidade e você pode acessá-lo em `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Dicionários globais** Há dois dicionários globais, gerenciados como objetos JSON, em AEM biblioteca do cliente. Esses dicionários contêm mensagens de erro padrão, nomes de mês, símbolos de moeda, padrões de data e hora e assim por diante. Você pode encontrar esses dicionários no CRXDe Lite em /libs/fd/xfaforms/clientlibs/I18N. Essas localizações contêm pastas separadas para cada localidade. Como os dicionários globais geralmente não são atualizados com frequência, manter arquivos JavaScript separados para cada localidade permite que os navegadores os armazenem em cache e reduzam o uso da largura de banda da rede ao acessar diferentes formulários adaptáveis no mesmo servidor.

### Como a localização do formulário adaptável funciona {#how-localization-of-adaptive-form-works}

Há dois métodos para identificar a localidade do formulário adaptável. Quando um formulário adaptável é renderizado, ele identifica a localidade solicitada ao :

* analisar a `[local]` no URL do formulário adaptável. O formato do URL é `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Usando `[local]` O seletor permite armazenar em cache um formulário adaptável.

* observando os seguintes parâmetros na ordem especificada:

   * Parâmetro de solicitação `afAcceptLang`
Para substituir a localidade do navegador de usuários, você pode passar a variável 
`afAcceptLang` solicitar parâmetro para forçar a localidade. Por exemplo, o seguinte URL forçará a renderização do formulário no idioma japonês:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * A localidade do navegador definida para o usuário, que é especificada na solicitação usando o `Accept-Language` cabeçalho.

   * Configuração de idioma do usuário especificado em AEM.

   * Por padrão, a localidade do navegador é ativada. Para alterar a configuração de local do navegador,
      * Abra o gerenciador de configuração. O URL é `http://[server]:[port]/system/console/configMgr`
      * Localize e abra o **[!UICONTROL Canal da Web de comunicação interativa e formulário adaptável]** configuração.
      * Alterar o status do **[!UICONTROL Usar a localidade do navegador]** e  **[!UICONTROL Salvar]** a configuração.

Depois que a localidade é identificada, os formulários adaptáveis escolhem o dicionário específico do formulário. Se o dicionário específico do formulário para a localidade solicitada não for encontrado, ele usará o dicionário para o idioma em que o formulário adaptável foi criado.

Se nenhuma informação de local estiver presente, o formulário adaptável será entregue no idioma original do formulário. O idioma original é o idioma usado durante o desenvolvimento do formulário adaptável.

Se uma biblioteca do cliente para o local solicitado não existir, ela verificará se há uma biblioteca do cliente para o código de idioma presente no local. Por exemplo, se a localidade solicitada for `en_ZA` (inglês da África do Sul) e a biblioteca do cliente para `en_ZA` não existir, o formulário adaptável usará a biblioteca do cliente para `en` (Inglês), se existir. No entanto, se nenhum deles existir, o formulário adaptável usará o dicionário para `en` localidade.

## Adicionar suporte de localização para localidades não suportadas {#add-localization-support-for-non-supported-locales}

Atualmente, o AEM Forms suporta a localização de conteúdo de formulários adaptáveis em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR).

Para adicionar suporte para um novo local no tempo de execução dos formulários adaptáveis:

1. [Adicionar uma localidade ao serviço GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Adicionar biblioteca de cliente XFA para uma localidade](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Adicionar biblioteca de cliente de formulário adaptável para um local](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Adicionar suporte de local ao dicionário](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Reinicie o servidor](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Adicionar uma localidade ao serviço de localização do Guia {#add-a-locale-to-the-guide-localization-service-br}

1. Ir para `https://'[server]:[port]'/system/console/configMgr`.
1. Clique em para editar o **Serviço de localização do guia** componente.
1. Adicione a localidade que deseja adicionar à lista de localidades suportadas.

![GuideLocalizationService](assets/configservice.png)

### Adicionar biblioteca de cliente XFA para uma localidade {#add-xfa-client-library-for-a-locale-br}

Criar um nó do tipo `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, com categoria `xfaforms.I18N.<locale>`e adicione os seguintes arquivos à biblioteca do cliente:

* **I18N.js** definição `xfalib.locale.Strings` para `<locale>` conforme definido em `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** Contendo o seguinte:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Adicionar biblioteca de cliente de formulário adaptável para um local {#add-adaptive-form-client-library-for-a-locale-br}

Criar um nó do tipo `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, com categoria como `guides.I18N.<locale>` e e dependências como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`. &quot;

Adicione os seguintes arquivos à biblioteca do cliente:

* **i18n.js** definição `guidelib.i18n`, com padrões de &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para `<locale>` de acordo com as especificações XFA descritas em [Especificação do conjunto de localidades](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). Você também pode ver como ele é definido para outras localidades compatíveis em `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definição `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` para `<locale>` conforme definido em `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** Contendo o seguinte:

```text
i18n.js
LogMessages.js
```

### Adicionar suporte de local ao dicionário {#add-locale-support-for-the-dictionary-br}

Execute esta etapa somente se a variável `<locale>` você está adicionando que não está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Crie um `nt:unstructured` nó `languages` under `etc`, se ainda não estiver presente.

1. Adicionar uma propriedade de string com vários valores `languages` ao nó , se ainda não estiver presente.
1. Adicione o `<locale>` valores de localidade padrão `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se ainda não estiver presente.

1. Adicione o `<locale>` aos valores da `languages` propriedade de `/etc/languages`.

O `<locale>` aparecerá em `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Reinicie o servidor {#restart-the-server}

Reinicie o servidor de AEM para que a localidade adicionada entre em vigor.

## Exemplos de bibliotecas para adicionar suporte ao espanhol {#sample-libraries-for-adding-support-for-spanish}

Exemplos de bibliotecas de clientes para adicionar suporte ao espanhol

[Obter arquivo](assets/sample.zip)
