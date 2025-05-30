---
title: Suporte a novos códigos de idiomas para localização de formulários adaptáveis
description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptáveis. Os locais suportados por padrão são inglês, francês, alemão e japonês.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
feature: Adaptive Forms,Foundation Components
role: Admin,User
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 2%

---

# Suporte a novos códigos de idiomas para localização de formulários adaptáveis{#supporting-new-locales-for-adaptive-forms-localization}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

## Sobre dicionários de local {#about-locale-dictionaries}

A localização de formulários adaptáveis depende de dois tipos de dicionários de localidade:

**Dicionário específico de formulário** Contém cadeias de caracteres usadas em formulários adaptáveis. Por exemplo, rótulos, nomes de campos, mensagens de erro, descrições de ajuda e assim por diante. Ele é gerenciado como um conjunto de arquivos XLIFF para cada localidade e você pode acessá-lo em `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Dicionários globais** Há dois dicionários globais, gerenciados como objetos JSON, na biblioteca do cliente AEM. Esses dicionários contêm mensagens de erro padrão, nomes de meses, símbolos de moeda, padrões de data e hora e assim por diante. Você pode encontrar esses dicionários no CRXDe Lite em /libs/fd/xfaforms/clientlibs/I18N. Esses locais contêm pastas separadas para cada local. Como os dicionários globais geralmente não são atualizados com frequência, manter arquivos JavaScript separados para cada localidade permite que os navegadores os armazenem em cache e reduzam o uso da largura de banda da rede ao acessar diferentes formulários adaptáveis no mesmo servidor.

### Como funciona a localização do formulário adaptável {#how-localization-of-adaptive-form-works}

Há dois métodos para identificar o local do formulário adaptável. Quando um formulário adaptável é renderizado, ele identifica o local solicitado por:

* observando o seletor `[local]` na URL do formulário adaptável. O formato da URL é `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Usar o seletor `[local]` permite armazenar em cache um formulário adaptável.

* observando os seguintes parâmetros na ordem especificada:

   * Parâmetro de solicitação `afAcceptLang`
Para substituir a localidade do navegador dos usuários, você pode passar o parâmetro de solicitação `afAcceptLang` para forçar a localidade. Por exemplo, a URL a seguir foi forçada a renderizar o formulário no local japonês:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * A localidade do navegador definida para o usuário, que é especificada na solicitação usando o cabeçalho `Accept-Language`.

   * Configuração de idioma do usuário especificado no AEM.

   * A localidade do navegador é ativada por padrão. Para alterar a configuração do local do navegador,
      * Abra o gerenciador de configurações. A URL é `http://[server]:[port]/system/console/configMgr`
      * Localize e abra a configuração **[!UICONTROL Canal da Web do Formulário adaptável e da Comunicação Interativa]**.
      * Altere o status da opção **[!UICONTROL Usar localidade do navegador]** e **[!UICONTROL Salve]** a configuração.

Depois que a localidade é identificada, os formulários adaptáveis escolhem o dicionário específico do formulário. Se o dicionário específico do formulário para a localidade solicitada não for encontrado, ele usará o dicionário do idioma no qual o formulário adaptável foi criado.

Se nenhuma informação de local estiver presente, o formulário adaptável será entregue no idioma original do formulário. O idioma original é o idioma usado ao desenvolver o formulário adaptável.

Se não existir uma biblioteca do cliente para a localidade solicitada, ela verificará se há uma biblioteca do cliente para o código de idioma presente na localidade. Por exemplo, se a localidade solicitada for `en_ZA` (inglês da África do Sul) e a biblioteca do cliente para `en_ZA` não existir, o formulário adaptável usará a biblioteca do cliente para `en` (inglês), se existir. No entanto, se nenhum deles existir, o formulário adaptável usará o dicionário para a localidade `en`.

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
1. Clique para editar o componente **Serviço de Localização do Guia**.
1. Adicione a localidade que deseja adicionar à lista de localidades suportadas.

![GuideLocalizationService](assets/configservice.png)

### Adicionar biblioteca do cliente XFA para uma localidade {#add-xfa-client-library-for-a-locale-br}

Crie um nó do tipo `cq:ClientLibraryFolder` em `etc/<folderHierarchy>`, com a categoria `xfaforms.I18N.<locale>`, e adicione os seguintes arquivos à biblioteca do cliente:

* **I18N.js** definindo `xfalib.locale.Strings` para o `<locale>` conforme definido em `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** contendo o seguinte:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Adicionar biblioteca de cliente de formulário adaptável para uma localidade {#add-adaptive-form-client-library-for-a-locale-br}

Crie um nó do tipo `cq:ClientLibraryFolder` em `etc/<folderHierarchy>`, com a categoria `guides.I18N.<locale>` e as dependências `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`. &quot;

Adicione os seguintes arquivos à biblioteca do cliente:

* **i18n.js** definindo `guidelib.i18n`, com padrões de &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para o `<locale>` de acordo com as especificações do XFA descritas em [Especificação do Conjunto de Localidades](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). Você também pode ver como ele é definido para outras localidades com suporte no `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definindo `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` para `<locale>` conforme definido em `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** contendo o seguinte:

```text
i18n.js
LogMessages.js
```

### Adicionar suporte de localidade para o dicionário {#add-locale-support-for-the-dictionary-br}

Execute esta etapa somente se o `<locale>` que você está adicionando não estiver entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Crie um nó `nt:unstructured` `languages` em `etc`, se ainda não estiver presente.

1. Adicione uma propriedade de cadeia de caracteres de vários valores `languages` ao nó, se ainda não estiver presente.
1. Adicione os `<locale>` valores de localidade padrão `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se ainda não estiverem presentes.

1. Adicione `<locale>` aos valores da propriedade `languages` de `/etc/languages`.

O `<locale>` aparecerá em `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Reiniciar o servidor {#restart-the-server}

Reinicie o servidor AEM para que a localidade adicionada entre em vigor.

>[!NOTE]
>
> É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Bibliotecas de exemplo para adicionar suporte ao espanhol {#sample-libraries-for-adding-support-for-spanish}

Exemplos de bibliotecas de clientes para adicionar suporte para espanhol

[Obter arquivo](assets/sample.zip)
