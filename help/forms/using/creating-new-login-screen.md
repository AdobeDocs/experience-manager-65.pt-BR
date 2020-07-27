---
title: Criar uma nova tela de login
seo-title: Criar uma nova tela de login
description: Como modificar a página de logon dos módulos do LiveCycle, por exemplo, da área de trabalho do AEM Forms ou do Gerenciador de Formulários.
seo-description: Como modificar a página de logon dos módulos do LiveCycle, por exemplo, da área de trabalho do AEM Forms ou do Gerenciador de Formulários.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
translation-type: tm+mt
source-git-commit: b4c1bc5f09491a8843a82c3589604f6717a76ea8
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 5%

---


# Criar uma nova tela de login{#creating-a-new-login-screen}

Você pode modificar a tela de login de todos os módulos de AEM Forms que usam a tela de login de AEM Forms. Por exemplo, as modificações afetam a tela de logon da área de trabalho do Forms Manager e do AEM Forms.

## Pré-requisitos {#prerequisite}

1. Faça logon com permissões `/lc/crx/de` de administrador.
1. Execute as seguintes ações:

   1. Replicar a estrutura hierárquica: de `/libs/livecycle/core/content` na `/apps/livecycle/core/content`.

      Mantenha as mesmas propriedades (nó/pasta) e controle de acesso.

   1. Copie a pasta de conteúdo:

      de: `/libs/livecycle/core`

      para: `/apps/livecycle/core`.

   1. Exclua o conteúdo da `/apps/livecycle/core` pasta.

1. Execute estas ações:

   1. Replicar a estrutura hierárquica: de `/libs/livecycle/core/components/login` na `/apps/livecycle/core/components/login`. Mantenha as mesmas propriedades (nó/pasta) e controle de acesso.

   1. Copie a pasta de componentes: de `/libs/livecycle/core` a `/apps/livecycle/core`.

   1. Exclua o conteúdo da pasta: `/apps/livecycle/core/components/login`.

### Adicionar uma nova localidade {#adding-a-new-locale}

1. Copie a `i18n` pasta:

   * de `/libs/livecycle/core/components/login`
   * para `/apps/livecycle/core/components/login`

1. Exclua todas as pastas dentro `i18n` exceto uma, digamos `en`.

1. Na pasta `en`, execute estas ações:

   1. Renomeie a pasta para o nome da localidade que deseja suportar. Por exemplo, `ar`.

   1. Altere o `jcr:language` valor da propriedade para `ar`(para a `ar` pasta).
   >[!NOTE]
   >
   >Se locale for uma combinação de código de país de idioma, digamos, `ar-DZ`altere o nome da pasta e o valor da propriedade para `ar-DZ`.

1. Copiar `login.jsp`:

   * de `/libs/livecycle/core/components/login`
   * para `/apps/livecycle/core/components/login`

1. Modifique o seguinte trecho de código para `/apps/livecycle/core/components/login/login.jsp`:

***Localidade é código de idioma***

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }

To

String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("ar")) {
            browserLocale = "ar";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```jsp

String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }

To

String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
            browserLocale = "ar-DZ";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
***To change Default locale***

```jsp

String browserLocale = "en";
for(int i=0; i<locales.length; i++)

To

String browserLocale = "ar";
for(int i=0; i<locales.length; i++)
```



### Adicionar novo texto ou modificar um texto existente {#adding-new-text-or-modifying-existing-text}

1. Copiar `i18n` pasta:

   * de `/libs/livecycle/core/components/login`
   * para `/apps/livecycle/core/components/login`

1. Agora, modifique o valor da propriedade `sling:message` do nó (sob a pasta de código de localidade desejada) para o qual você deseja alterar o texto. A tradução é feita por meio da chave mencionada no valor da `sling:key` propriedade do nó.

1. Para adicionar um novo par de valores chave, execute as seguintes ações. Verifique um exemplo na captura de tela a seguir.

   1. Crie um nó do tipo `sling:MessageEntry`, ou copie um nó existente e renomeie-o em todas as pastas de localidade.
   1. Copiar `login.jsp` :

      * de `/libs/livecycle/core/components/login`

      * para `/apps/livecycle/core/components/login`
   1. Modificar `/apps/livecycle/core/components/login/login.jsp` para incorporar o texto recém-adicionado.

   ![Adicionar novo par de valores chave](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   Para

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```



### Adicionar novo estilo ou modificar um estilo existente {#adding-new-style-or-modifying-existing-style}

1. Copy `login` node:

   * de `/libs/livecycle/core/content`
   * para `/apps/livecycle/core/content`

1. Excluir arquivos `login.js` e `jquery-1.8.0.min.js`, do nó `/apps/livecycle/core/content/login.`
1. Modifique os estilos no arquivo CSS.
1. Para adicionar novos estilos:

   1. Adicionar novos estilos a `/apps/livecycle/core/content/login/login.css`
   1. Copiar `login.jsp`

      * de `/libs/livecycle/core/components/login`

      * para `/apps/livecycle/core/components/login`
   1. Modifique `/apps/livecycle/core/components/login/login.jsp` para incorporar os estilos recém-adicionados.



Por exemplo:

* Adicione o seguinte a `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* Modifique o seguinte em `/apps/livecycle/core/components/login.jsp`.


   ```jsp
   <div class="loginContentArea">
   ```

   Para

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>Se as imagens existentes em `/apps/livecycle/core/content/login` (copiadas de `/libs/livecycle/core/content/login`) forem removidas, remova as referências correspondentes em CSS.


### Adicionar novas imagens {#add-new-images}

1. Siga as etapas de Adicionar novo estilo ou modificar o estilo existente (documentado acima).
1. Adicione novas imagens em `/apps/livecycle/core/content/login`. Para adicionar imagem:

   1. Instale o cliente WebDAV.
   1. Navegue até a `/apps/livecycle/core/content/login` pasta, usando o cliente webDAV. Para obter mais informações, consulte: [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   1. Adicione novas imagens.

1. Adicione novos estilos `/apps/livecycle/core/content/login/login.css,` correspondentes a novas imagens adicionadas em `/apps/livecycle/core/content/login`.
1. Use os novos estilos em `login.jsp` em `/apps/livecycle/core/components`.

Por exemplo:


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    * Modifique o seguinte em /apps/livecycle/core/components/login.jsp.

```jsp
<div class="loginContainerBkg">
```

Para

```jsp
<div class="newLginContainerBkg">
```

