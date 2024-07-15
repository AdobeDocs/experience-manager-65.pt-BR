---
title: Criar uma tela de logon
description: Como modificar a página de logon dos módulos do LiveCycle, por exemplo, do AEM Forms workspace ou do Forms Manager.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 3%

---

# Criar uma tela de logon{#creating-a-new-login-screen}

Você pode modificar a tela de logon de todos os módulos do AEM Forms que usam a tela de logon do AEM Forms. Por exemplo, as modificações afetam a tela de logon do Forms Manager e da área de trabalho do AEM Forms.

## Pré-requisitos {#prerequisite}

1. Fazer logon em `/lc/crx/de` com permissões de Administrador.
1. Execute as seguintes ações:

   1. Replicar a estrutura hierárquica: de `/libs/livecycle/core/content` em `/apps/livecycle/core/content`.

      Mantenha as mesmas propriedades (nó/pasta) e controle de acesso.

   1. Copie a pasta de conteúdo:

      de: `/libs/livecycle/core`

      para: `/apps/livecycle/core`.

   1. Excluir o conteúdo da pasta `/apps/livecycle/core`.

1. Execute estas ações:

   1. Replicar a estrutura hierárquica: de `/libs/livecycle/core/components/login` em `/apps/livecycle/core/components/login`. Mantenha as mesmas propriedades (nó/pasta) e controle de acesso.

   1. Copiar a pasta de componentes: de `/libs/livecycle/core` para `/apps/livecycle/core`.

   1. Exclua o conteúdo da pasta: `/apps/livecycle/core/components/login`.

### Adicionar um novo local {#adding-a-new-locale}

1. Copiar a pasta `i18n`:

   * de `/libs/livecycle/core/components/login`
   * para `/apps/livecycle/core/components/login`

1. Exclua todas as pastas dentro de `i18n` exceto uma, digamos `en`.

1. Na pasta `en`, execute estas ações:

   1. Renomeie a pasta com o nome do local que você deseja que seja compatível. Por exemplo, `ar`.

   1. Altere o valor da propriedade `jcr:language` para `ar`(para a pasta `ar`).

   >[!NOTE]
   >
   >Se a localidade for uma combinação de código idioma-país, digamos, `ar-DZ`, altere o nome da pasta e o valor da propriedade para `ar-DZ`.

1. Copiar `login.jsp`:

   * de `/libs/livecycle/core/components/login`
   * para `/apps/livecycle/core/components/login`

1. Modifique o seguinte trecho de código para `/apps/livecycle/core/components/login/login.jsp`:

***A localidade é o código de idioma***

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
```

Para

```jsp
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
```

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
```

Para

```jsp
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
```

***Para alterar a localidade padrão***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### Adição de novo texto ou modificação de texto existente {#adding-new-text-or-modifying-existing-text}

1. Copiar pasta `i18n`:

   * de `/libs/livecycle/core/components/login`
   * para `/apps/livecycle/core/components/login`

1. Agora modifique o valor da propriedade `sling:message` do nó (na pasta de código de localidade desejada) para o qual você deseja alterar o texto. A tradução é feita através da chave mencionada no valor da propriedade `sling:key` do nó.

1. Para adicionar um novo par de valor-chave, execute as seguintes ações. Verifique um exemplo na captura de tela a seguir.

   1. Crie um nó do tipo `sling:MessageEntry`, ou copie um nó existente e renomeie-o, em todas as pastas de localidade.
   1. Copiar `login.jsp` :

      * de `/libs/livecycle/core/components/login`

      * para `/apps/livecycle/core/components/login`

   1. Modifique `/apps/livecycle/core/components/login/login.jsp` para incorporar o texto recém-adicionado.

   ![Adicionar novo par de valor-chave](assets/capture_new.png)

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

### Adicionar novo estilo ou modificar estilo existente {#adding-new-style-or-modifying-existing-style}

1. Copiar nó `login`:

   * de `/libs/livecycle/core/content`
   * para `/apps/livecycle/core/content`

1. Excluir os arquivos `login.js` e `jquery-1.8.0.min.js` do nó `/apps/livecycle/core/content/login.`
1. Modifique os estilos no arquivo CSS.
1. Para adicionar novos estilos:

   1. Adicionar novos estilos a `/apps/livecycle/core/content/login/login.css`
   1. Copiar `login.jsp`

      * de `/libs/livecycle/core/components/login`

      * para `/apps/livecycle/core/components/login`

   1. Modifique `/apps/livecycle/core/components/login/login.jsp` para incorporar os estilos adicionados recentemente.


Por exemplo:

* Adicionar o seguinte a `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* Modificar o seguinte em `/apps/livecycle/core/components/login.jsp`.


  ```jsp
  <div class="loginContentArea">
  ```

  Para

  ```jsp
  <div class="newLoginContentArea">
  ```

>[!NOTE]
>
>Se as imagens existentes em `/apps/livecycle/core/content/login` (copiadas de `/libs/livecycle/core/content/login`) forem removidas, remova as referências correspondentes no CSS.

### Adicionar novas imagens {#add-new-images}

1. Siga as etapas de Adicionar novo estilo ou modificar estilo existente (documentado acima).
1. Adicionar novas imagens em `/apps/livecycle/core/content/login`. Para adicionar uma imagem:

   1. Instale o cliente WebDAV.
   1. Navegue até a pasta `/apps/livecycle/core/content/login`, usando o cliente webDAV. Para obter mais informações, consulte [Acesso ao WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en).

   1. Adicione novas imagens.

1. Adicione novos estilos em `/apps/livecycle/core/content/login/login.css,` correspondentes às novas imagens adicionadas em `/apps/livecycle/core/content/login`.
1. Use os novos estilos em `login.jsp` às `/apps/livecycle/core/components`.

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
