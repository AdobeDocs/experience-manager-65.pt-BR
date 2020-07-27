---
title: Criação de um perfil personalizado para formulários HTML5
seo-title: Criação de um perfil personalizado para formulários HTML5
description: Um perfil de formulários HTML5 é um nó de recurso no Apache Sling. Representa uma versão personalizada do serviço de renderização de formulários HTML5.
seo-description: Um perfil de formulários HTML5 é um nó de recurso no Apache Sling. Representa uma versão personalizada do serviço de renderização de formulários HTML5.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Criação de um perfil personalizado para formulários HTML5 {#creating-a-custom-profile-for-html-forms}

Um perfil é um nó de recurso no [Apache Sling](https://sling.apache.org/). Representa a versão personalizada do serviço de execução de formulários HTML5. Você pode usar o serviço de representação de formulários HTML5 para personalizar a aparência, o comportamento e as interações dos formulários HTML5. Existe um nó de perfil na `/content` pasta no repositório JCR. Você pode colocar o nó diretamente sob a `/content` pasta ou qualquer subpasta da `/content` pasta.

O nó do perfil tem a propriedade **sling:resourceSuperType** e o valor padrão é **xfaforms/perfil**. O script de renderização para o nó está em /libs/xfaforms/perfil.

Os scripts Sling são scripts JSP. Esses scripts JSP servem como container para reunir o HTML para o formulário solicitado e os artefatos JS / CSS necessários. Esses scripts Sling também são chamados de scripts **do Renderizador de** Perfis. O renderizador de perfis chama o serviço OSGi do Forms para renderizar o formulário solicitado.

O script de perfil está em html.jsp e html.POST.jsp para solicitações GET e POST. Você pode copiar e modificar um ou mais arquivos para substituir e adicionar suas personalizações. Não faça alterações no local, a atualização de patch substitui essas alterações.

Um perfil contém vários módulos. Os módulos são formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp e footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Os módulos formRuntime.jsp contêm referências das bibliotecas clientes. Ele também descreve métodos para extrair informações de localidade da solicitação e incluir as mensagens localizadas na solicitação. Você pode incluir libs ou estilos personalizados JavaScript no formRuntime.jsp.

## config.jsp {#config-jsp}

O módulo config.jsp contém várias configurações, como registro em log, serviços proxy e versão de comportamento. Você pode adicionar sua própria configuração e personalização do widget ao módulo config.jsp. Você também pode adicionar configurações como registro de widget personalizado ao módulo config.jsp.

## toolbar.jsp {#toolbar-jsp}

O toolbar.jsp contém o código para criar uma barra de ferramentas colorida. Para remover a barra de ferramentas, remova toolbar.jsp do arquivo HTML.jsp

## formBody.jsp {#formbody-jsp}

O módulo formBody.jsp é para a representação HTML do formulário XFA.

## nav_footer.jsp {#nav-footer-jsp}

No início, o formulário HTML5 renderiza apenas a primeira página do formulário. Quando um usuário rola o formulário, o restante dos formulários é carregado. Isso agiliza a experiência de carregamento. O componente nav_footer.jsp contém todos os estilos e os elementos necessários para facilitar o carregamento das páginas na rolagem.

## footer.jsp {#footer-jsp}

O módulo footer.jsp está vazio. Isso permite que você adicione scripts usados apenas para interação do usuário.

## Criação de Perfis personalizados {#creating-custom-profiles}

Para criar um perfil personalizado, execute as seguintes etapas:

### Criar nó de Perfil {#create-profile-node}

1. Navegue até a interface CRX DE no URL: `https://'[server]:[port]'/crx/de` e faça logon na interface com credenciais de administrador.

1. No painel esquerdo, navegue até o local */content/xfaforms/perfis*.

1. Copie o nó padrão e cole o nó em outra pasta (*/content/perfis*) com o nome *hrform*.

1. Selecione o novo nó, *forma* e adicione uma propriedade de string: *sling:resourceType* com valor: *forma/demonstração*.

1. Clique em Salvar tudo no menu da barra de ferramentas para salvar as alterações.

### Criar o script do renderizador de perfis {#create-the-profile-renderer-script}

Depois de criar um perfil personalizado, adicione informações de renderização a esse perfil. Ao receber uma solicitação para o novo perfil, o CRX verifica a existência da pasta /apps para a página JSP a ser renderizada. Crie a página JSP na pasta /apps.

1. No painel esquerdo, navegue até a `/apps` pasta.
1. Clique com o botão direito do mouse na `/apps` pasta e escolha criar uma pasta com o nome **hrform**.
1. Considere que a pasta **hrform** crie uma pasta chamada **demo**.
1. Clique no botão **Salvar tudo** .
1. Navegue até `/libs/xfaforms/profile/html.jsp` o nó **html.jsp** e copie-o.
1. Cole o nó **html.jsp** na `/apps/hrform/demo` pasta criada acima com o mesmo nome **html.jsp** e clique em **Salvar**.
1. Se você tiver outros componentes do script de perfil, siga as etapas de 1 a 6 para copiar os componentes na pasta /apps/hrform/demo.

1. Para verificar se o perfil foi criado, abra o URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Para verificar seus formulários, [importe seus formulários](/help/forms/using/get-xdp-pdf-documents-aem.md) do sistema de arquivos local para o AEM Forms e [pré-visualização o formulário](/help/forms/using/previewing-forms.md) na instância do autor do servidor AEM.
