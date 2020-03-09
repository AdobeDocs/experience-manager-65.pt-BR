---
title: Suporte a novas localidades para a localização de formulários adaptáveis
seo-title: Suporte a novas localidades para a localização de formulários adaptáveis
description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptativos. Por padrão, as localidades compatíveis são inglês, francês, alemão e japonês.
seo-description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptativos. Por padrão, as localidades compatíveis são inglês, francês, alemão e japonês.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: dbfadb0b49c83c38aa2cb55c32517ad70bbd79d0

---


# Suporte a novas localidades para a localização de formulários adaptáveis{#supporting-new-locales-for-adaptive-forms-localization}

## Sobre dicionários de localidades {#about-locale-dictionaries}

A localização de formulários adaptáveis depende de dois tipos de dicionários de localidade:

**Dicionário** específico do formulário Contém strings usadas em formulários adaptáveis. Por exemplo, rótulos, nomes de campos, mensagens de erro, descrições de ajuda e assim por diante. Ele é gerenciado como um conjunto de arquivos XLIFF para cada localidade e você pode acessá-lo em `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Dicionários** globais Existem dois dicionários globais, gerenciados como objetos JSON, na biblioteca do cliente AEM. Esses dicionários contêm mensagens de erro padrão, nomes de mês, símbolos de moeda, padrões de data e hora e assim por diante. Você pode encontrar esses dicionários no CRXDe Lite em /libs/fd/xfaforms/clientlibs/I18N. Esses locais contêm pastas separadas para cada localidade. Como os dicionários globais geralmente não são atualizados com frequência, a manutenção de arquivos JavaScript separados para cada localidade permite que os navegadores os armazenem em cache e reduzam o uso da largura de banda da rede ao acessar formulários adaptáveis diferentes no mesmo servidor.

### Como funciona a localização do formulário adaptável {#how-localization-of-adaptive-form-works}

Quando um formulário adaptável é renderizado, ele identifica a localidade solicitada, observando os seguintes parâmetros na ordem especificada:

* Parâmetro de solicitação `afAcceptLang`Para substituir a localidade do navegador de usuários, é possível passar o parâmetro de `afAcceptLang` solicitação para forçar a localidade. Por exemplo, o URL a seguir forçará a renderização do formulário na localidade japonesa:
   `https://[server]:[port]/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* A localidade do navegador definida para o usuário, que é especificada na solicitação usando o `Accept-Language` cabeçalho.

* Configuração de idioma do usuário especificado no AEM.

Depois que a localidade é identificada, os formulários adaptativos escolhem o dicionário específico do formulário. Se o dicionário específico do formulário para a localidade solicitada não for encontrado, ele usará o dicionário inglês (en).

Se uma biblioteca do cliente para a localidade solicitada não existir, ela verificará se há uma biblioteca do cliente para o código de idioma presente na localidade. Por exemplo, se a localidade solicitada for `en_ZA` (inglês sul-africano) e a biblioteca do cliente para `en_ZA` não existir, o formulário adaptável usará a biblioteca do cliente para o idioma `en` (inglês), se existir. No entanto, se nenhum deles existir, o formulário adaptativo usará o dicionário para a `en` localidade.

## Adicionar suporte de localização para localidades não suportadas {#add-localization-support-for-non-supported-locales}

Atualmente, o AEM Forms suporta a localização de conteúdo de formulários adaptáveis em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR).

Para adicionar suporte para uma nova localidade em tempo de execução de formulários adaptáveis:

1. [Adicionar uma localidade ao serviço GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Adicionar biblioteca de cliente XFA para uma localidade](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Adicionar biblioteca de cliente de formulário adaptável para uma localidade](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Adicionar suporte de localidade para o dicionário](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Reinicie o servidor](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Adicionar uma localidade ao serviço de localização do guia {#add-a-locale-to-the-guide-localization-service-br}

1. Ir para `https://[server]:[port]/system/console/configMgr`.
1. Clique para editar o componente Serviço **de localização do** Guia.
1. Adicione a localidade que deseja adicionar à lista de localidades compatíveis.

![GuideLocalizationService](assets/configservice.png)

### Adicionar biblioteca de cliente XFA para uma localidade {#add-xfa-client-library-for-a-locale-br}

Crie um nó do tipo `cq:ClientLibraryFolder` em `etc/<folderHierarchy>`, com categoria `xfaforms.I18N.<locale>`, e adicione os seguintes arquivos à biblioteca do cliente:

* **I18N.js** definindo `xfalib.locale.Strings` para o `<locale>` conforme definido em `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** contendo o seguinte:

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Adicionar biblioteca de cliente de formulário adaptável para uma localidade {#add-adaptive-form-client-library-for-a-locale-br}

Crie um nó do tipo `cq:ClientLibraryFolder` em `etc/<folderHierarchy>`, com categoria como `guides.I18N.<locale>` e e dependências como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`. &quot;

Adicione os seguintes arquivos à biblioteca do cliente:

* **i18n.js** definindo `guidelib.i18n`, tendo padrões de &quot;calendáriosSímbolos&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para as especificações XFA `<locale>` [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)conforme as especificações deEspecificação deLocale Set. Você também pode ver como ele é definido para outras localidades compatíveis em `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definindo `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` para o `<locale>` conforme definido em `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** contendo o seguinte:

```
i18n.js
LogMessages.js
```

### Adicionar suporte de localidade para o dicionário {#add-locale-support-for-the-dictionary-br}

Execute essa etapa somente se o item `<locale>` que você está adicionando não estiver entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja``ko-kr`, .

1. Crie um `nt:unstructured` nó `languages` em `etc`, se ainda não estiver presente.

1. Adicione uma propriedade de string com vários valores `languages` ao nó, se ainda não estiver presente.
1. Adicione os valores de localidade `<locale>` padrão `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se ainda não estiver presente.

1. Adicione os valores `<locale>` da `languages` propriedade de `/etc/languages`.

O `<locale>` será exibido em `https://[server]:[port]/libs/cq/i18n/translator.html`.

### Restart the server {#restart-the-server}

Reinicie o servidor AEM para que a localidade adicionada entre em vigor.

## Amostra de bibliotecas para adicionar suporte ao espanhol {#sample-libraries-for-adding-support-for-spanish}

Amostra de bibliotecas de clientes para adicionar suporte para espanhol

[Obter arquivo](assets/sample.zip)
