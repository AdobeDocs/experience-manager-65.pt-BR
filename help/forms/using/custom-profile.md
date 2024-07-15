---
title: Criação de um perfil personalizado para formulários HTML5
description: Um perfil de formulários HTML5 é um nó de recurso no Apache Sling. Ele representa uma versão personalizada do serviço de renderização do HTML5 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms,Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Criação de um perfil personalizado para formulários HTML5 {#creating-a-custom-profile-for-html-forms}

Um perfil é um nó de recurso em [Apache Sling](https://sling.apache.org/). Ele representa a versão personalizada do serviço de representação de formulários HTML5. Você pode usar o serviço de representação de formulários HTML5 para personalizar a aparência, o comportamento e as interações dos formulários HTML5. Existe um nó de perfil na pasta `/content` no repositório JCR. Você pode colocar o nó diretamente na pasta `/content` ou em qualquer subpasta da pasta `/content`.

O nó de perfil tem a propriedade **sling:resourceSuperType** e o valor padrão é **xfaforms/profile**. O script de renderização do nó está em /libs/xfaforms/profile.

Os scripts Sling são scripts JSP. Esses scripts JSP servem como contêineres para reunir o HTML do formulário solicitado e os artefatos JS/CSS necessários. Esses scripts Sling também são chamados de **scripts de Renderizador de perfil**. O renderizador de perfil chama o serviço OSGi do Forms para renderizar o formulário solicitado.

O script de perfil está em html.jsp e html.POST.jsp para solicitações GET e POST. Você pode copiar e modificar um ou mais arquivos para substituir e adicionar suas personalizações. Não faça nenhuma alteração no local, a atualização do patch substituirá essas alterações.

Um perfil contém vários módulos. Os módulos são formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp e footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Os módulos formRuntime.jsp contêm referências das bibliotecas de clientes. Ele também descreve métodos para extrair informações de local da solicitação e incluir as mensagens localizadas na solicitação. Você pode incluir suas próprias bibliotecas ou estilos personalizados de JavaScript no formRuntime.jsp.

## config.jsp {#config-jsp}

O módulo config.jsp contém várias configurações, como registro, serviços proxy e versão de comportamento. Você pode adicionar sua própria configuração e personalização de widget ao módulo config.jsp. Você também pode adicionar configurações, como registro de widget personalizado, ao módulo config.jsp.

## toolbar.jsp {#toolbar-jsp}

O toolbar.jsp contém o código para criar uma barra de ferramentas colorida. Para remover a barra de ferramentas, remova toolbar.jsp do HTML.jsp

## formBody.jsp {#formbody-jsp}

O módulo formBody.jsp é para a representação HTML do formulário XFA.

## nav_footer.jsp {#nav-footer-jsp}

No início, o formulário HTML5 renderiza apenas a primeira página do formulário. Quando um usuário rola o formulário, o restante dos formulários é carregado. Isso agiliza a experiência de carregamento. O componente nav_footer.jsp contém todos os estilos e elementos necessários para facilitar o carregamento das páginas na rolagem.

## footer.jsp {#footer-jsp}

O módulo footer.jsp é um vazio. Ela permite adicionar scripts que são usados apenas para interação do usuário.

## Criação de perfis personalizados {#creating-custom-profiles}

Para criar um perfil personalizado, execute as seguintes etapas:

### Criar nó de perfil {#create-profile-node}

1. Navegue até a interface do CRX DE na URL: `https://'[server]:[port]'/crx/de` e faça logon na interface com credenciais de administrador.

1. No painel esquerdo, navegue até o local */content/xfaforms/profiles*.

1. Copie o padrão do nó e cole-o em uma pasta diferente (*/content/profiles*) com o nome *hrform*.

1. Selecione o novo nó, *hrform*, e adicione uma propriedade de cadeia de caracteres: *sling:resourceType* com o valor: *hrform/demo*.

1. Clique em Salvar tudo no menu da barra de ferramentas para salvar as alterações.

### Criar o script renderizador de perfil {#create-the-profile-renderer-script}

Depois de criar um perfil personalizado, adicione informações de renderização a esse perfil. Ao receber uma solicitação para o novo perfil, o CRX verifica a existência da pasta /apps para que a página JSP seja renderizada. Crie a página JSP na pasta /apps.

1. No painel esquerdo, navegue até a pasta `/apps`.
1. Clique com o botão direito do mouse na pasta `/apps` e escolha criar uma pasta com o nome **hrform**.
1. Dentro da pasta **hrform**, crie uma pasta chamada **demo**.
1. Clique no botão **Salvar tudo**.
1. Navegue até `/libs/xfaforms/profile/html.jsp` e copie o nó **html.jsp**.
1. Cole o nó **html.jsp** na pasta `/apps/hrform/demo` criada acima com o mesmo nome **html.jsp** e clique em **Salvar**.
1. Se você tiver outros componentes do script de perfil, siga as etapas 1 a 6 para copiar os componentes na pasta /apps/hrform/demo.

1. Para verificar se o perfil foi criado, abra a URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Para verificar seus formulários, [Importe seus formulários](/help/forms/using/get-xdp-pdf-documents-aem.md) do sistema de arquivos local para o AEM Forms e [visualize o formulário](/help/forms/using/previewing-forms.md) na instância de autor do servidor AEM.
