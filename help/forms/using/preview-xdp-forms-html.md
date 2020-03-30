---
title: Gerar pré-visualização HTML5 de um formulário XDP
seo-title: Gerar pré-visualização HTML5 de um formulário XDP
description: A guia HTML de Pré-visualização no LiveCycle Designer pode ser usada para pré-visualização de formulários conforme eles aparecem em um navegador.
seo-description: A guia HTML de Pré-visualização no LiveCycle Designer pode ser usada para pré-visualização de formulários conforme eles aparecem em um navegador.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Gerar pré-visualização HTML5 de um formulário XDP{#generate-html-preview-of-an-xdp-form}

Ao projetar um formulário no AEM Forms Designer, além de visualizar a execução em PDF de um formulário, também é possível pré-visualização uma execução HTML5 dele. Você pode usar a guia HTML **de** Pré-visualização para pré-visualização de um formulário como ele apareceria em um navegador.

## Ativar Pré-visualização HTML para formulários XDP no Designer {#html-preview-of-forms-in-forms-designer}

Para permitir que o Designer gere pré-visualizações HTML de formulários XDP, execute as seguintes configurações:

* Configurar o serviço de autenticação Apache Sling
* Desativar modo protegido
* Fornecer detalhes do servidor do AEM Forms

### Configurar o serviço de autenticação Apache Sling {#configure-apache-sling-authentication-service}

1. Ir para `https://'[server]:[port]'/system/console/configMgr` o AEM Forms em execução no OSGi ou
   `https://'[server]:[port]'/lc/system/console/configMgr` em AEM Forms em execução em JEE.
1. Localize e clique em **Apache Sling Authentication Service** configuration para abri-la no modo de edição.

1. Dependendo de você estar executando o AEM Forms em OSGi ou JEE, adicione o seguinte no campo Requisitos **de** autenticação:

   * AEM Forms em JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * Formulários AEM no OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms
   >[!NOTE]
   >
   >Não copie e cole o valor especificado no campo Requisitos de autenticação, pois ele pode corromper os caracteres especiais no valor. Em vez disso, digite o valor especificado no campo.

1. Especifique um nome de usuário e senha nos campos Nome **[!UICONTROL de usuário]** anônimo e Senha **[!UICONTROL de usuário]** anônimo, respectivamente. As credenciais especificadas são usadas para lidar com autenticação anônima e permitir acesso a usuários anônimos.
1. Click **Save** to save the configuration.

### Desativar modo protegido {#disable-protected-mode}

Por padrão, o modo [](../../forms/using/get-xdp-pdf-documents-aem.md) protegido está ativado. Mantenha-o ativado para os ambientes de produção. Você pode desativá-lo para um ambiente de desenvolvimento para pré-visualização de formulários HTML5 no Designer. Execute as seguintes etapas para desativá-la:

1. Faça logon no console da Web do AEM como administrador.

   * O URL para AEM Forms no OSGi é `https://'[server]:[port]'/system/console/configMgr`
   * O URL para AEM Forms no JEE é `https://'[server]:[port]'/lc/system/console/configMgr`

1. Abra Configurações **[!UICONTROL de formulários]** móveis para edição.
1. Desmarque a opção Modo **** protegido e clique em **[!UICONTROL Salvar]**.

### Fornecer detalhes do servidor do AEM Forms {#provide-details-of-aem-forms-server}

1. No Designer, vá para **Ferramentas** > **Opções**.
1. Na janela Opções, selecione a página Opções **do** servidor, forneça os detalhes a seguir e clique em **OK**.

   * **URL** do servidor: URL do servidor do AEM Forms.

   * **Número** da porta HTTP: Porta do servidor AEM. O valor padrão é 4502.
   * **Contexto de Pré-visualização HTML:** Caminho do perfil para renderizar formulários XFA. Os perfis padrão a seguir são usados para pré-visualização do formulário no Designer. No entanto, também é possível especificar um caminho para um perfil personalizado.

      * `/content/xfaforms/profiles/default.html` (Formulários AEM no OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (Formulários AEM em JEE)
   * **Contexto do Gerenciador de Formulários:** Caminho de contexto no qual a interface do usuário do Forms Manager é implantada. Os valores padrão são:

      * `/aem/forms` (Formulários AEM no OSGi)
      * `/lc/forms` (Formulários AEM em JEE)
   **Observação:** Verifique se o servidor do AEM Forms está ativo e em execução. The HTML preview connects to the CRX server to *generate* a preview.

   ![Opções do AEM Forms Designer ](assets/server_options.png)

   Opções do AEM Forms Designer

1. Para pré-visualização um formulário em HTML, clique na guia HTML **da** Pré-visualização.

   >[!NOTE]
   >
   >
   >
   >
   >    * Se a guia Pré-visualização HTML estiver fechada, pressione F4 para abrir a guia HTML Pré-visualização. Você também pode selecionar HTML de Pré-visualização no menu Visualização para abrir a guia HTML de Pré-visualização.
   >    * A pré-visualização HTML não suporta documentos PDF, a pré-visualização HTML é somente para documentos XDP.


   >[!CAUTION]
   >
   >Para testar a experiência real do usuário final, pré-visualização seus formulários em navegadores externos (Google Chrome, Microsoft Edge, Mozilla Firefox e muito mais) também. Cada navegador usa um mecanismo separado para renderizar HTML, portanto, pode haver algumas diferenças na forma como um formulário pré-visualização no Designer e no navegador externo.

## Visualização de formulário usando dados de formulário {#to-preview-a-form-using-sample-data}

O Designer permite visualizar e testar o formulário usando dados XML de amostra. É recomendável testar frequentemente o formulário com dados de amostra para garantir que o formulário seja renderizado de forma correta.

Se não houver dados de amostra, o Designer poderá criá-los ou você mesmo poderá criá-los. (Consulte [Para gerar automaticamente os dados de amostra para visualizar um formulário](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) e [Para criar dados de amostra para visualizar um formulário](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

Testar seu formulário usando uma fonte de dados de amostra garante que os dados e campos sejam mapeados e que os subformulários repetitivos se repetem conforme o esperado. Você pode criar um layout equilibrado de formulário que proporciona o espaço adequado para que cada objeto apresente os dados unidos.

1. Select **File > Form Properties**.

1. Click the **Preview** tab and, in the Data File box, type the full path to your test data file. Você também pode usar o botão Procurar para navegar até o arquivo.

1. Clique em **OK**. The next time you preview the form in the **Preview HTML** tab, the data values from the sample XML file will appear in the respective objects.

## Formulários de Pré-visualização localizados em um repositório {#html-preview-of-forms-in-forms-manager}

No AEM Forms, é possível pré-visualização de formulários e documentos em um repositório. A Pré-visualização ajuda a saber exatamente como os formulários se parecem e se comportam conforme serão usados pelos usuários finais.

[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
