---
title: Gerar visualização de HTML5 de um formulário XDP
description: A guia HTML de visualização no LiveCycle Designer pode ser usada para visualizar formulários conforme eles aparecem em um navegador.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Gerar visualização de HTML5 de um formulário XDP{#generate-html-preview-of-an-xdp-form}

Ao criar um formulário no AEM Forms Designer, além de visualizar a representação em PDF de um formulário, também é possível visualizar uma representação em HTML. Você pode usar a guia **Preview HTML** para visualizar um formulário da maneira que ele aparece em um navegador.

## Ativar a Visualização de HTML para formulários XDP no Designer {#html-preview-of-forms-in-forms-designer}

Para permitir que o Designer gere a pré-visualização de HTML de formulários XDP, execute as seguintes configurações:

* Configurar o serviço de autenticação do Apache Sling
* Desativar modo protegido
* Fornecer detalhes do servidor do AEM Forms

### Configurar o serviço de autenticação do Apache Sling {#configure-apache-sling-authentication-service}

1. Vá para `https://'[server]:[port]'/system/console/configMgr` no AEM Forms executando no OSGi ou
   `https://'[server]:[port]'/lc/system/console/configMgr` no AEM Forms em execução no JEE.
1. Localize e clique na configuração do **Apache Sling Authentication Service** para abri-lo no modo de edição.

1. Dependendo de você estar executando o AEM Forms no OSGi ou no JEE, adicione o seguinte no campo **Requisitos de autenticação**:

   * AEM Forms no JEE

      * -/content/xfaforms
      * -/etc/clientlibs

   * AEM Forms no OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >Não copie e cole o valor especificado no campo Requisitos de autenticação, pois ele pode corromper os caracteres especiais no valor. Em vez disso, digite o valor especificado no campo.

1. Especifique um nome de usuário e uma senha nos campos **[!UICONTROL Nome de Usuário Anônimo]** e **[!UICONTROL Senha de Usuário Anônimo]**, respectivamente. As credenciais especificadas são usadas para manipular a autenticação anônima e permitir acesso a usuários anônimos.
1. Clique em **Salvar** para salvar a configuração.

### Desativar modo protegido {#disable-protected-mode}

O [modo protegido](../../forms/using/get-xdp-pdf-documents-aem.md) está ativado, por padrão. Mantenha-o ativado para os ambientes de produção. Você pode desativá-lo para que um ambiente de desenvolvimento pré-visualize o HTML5 Forms no designer. Execute as seguintes etapas para desativá-la:

1. Faça logon no AEM Web Console como administrador.

   * A URL para o AEM Forms no OSGi é `https://'[server]:[port]'/system/console/configMgr`
   * A URL para o AEM Forms no JEE é `https://'[server]:[port]'/lc/system/console/configMgr`

1. Abra as **[!UICONTROL Configurações do Mobile Forms]** para edição.
1. Desmarque a opção **[!UICONTROL Modo protegido]** e clique em **[!UICONTROL Salvar]**.

### Fornecer detalhes do servidor do AEM Forms {#provide-details-of-aem-forms-server}

1. No Designer, vá para **Ferramentas** > **Opções**.
1. Na janela Opções, selecione a página **Opções de Servidor**, forneça os detalhes a seguir e clique em **OK**.

   * **URL do servidor**: URL do servidor do AEM Forms.

   * **Número da porta HTTP**: porta do servidor AEM. O valor padrão é 4502.
   * **Contexto de Visualização de HTML:** Caminho do perfil para renderização de formulários XFA. Os perfis padrão a seguir são usados para visualizar o formulário no Designer. Entretanto, também é possível especificar o caminho para um perfil personalizado.

      * `/content/xfaforms/profiles/default.html` (AEM Forms no OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms no JEE)

   * **Contexto do Forms Manager:** Caminho de contexto no qual a interface do usuário do Forms Manager é implantada. Os valores padrão são:

      * `/aem/forms` (AEM Forms no OSGi)
      * `/lc/forms` (AEM Forms no JEE)

   >[!NOTE]
   >
   >Verifique se o servidor do AEM Forms está ativo e em execução. A visualização do HTML se conecta ao servidor do CRX para *gerar* uma visualização.

   ![Opções do AEM Forms Designer &#x200B;](assets/server_options.png)

   Opções do AEM Forms Designer

1. Para visualizar um formulário no HTML, clique na guia **Preview HTML**.

   >[!NOTE]
   >
   >
   >
   >
   >    * Se a guia HTML Preview for fechada, pressione F4 para abrir a guia Preview HTML. Você também pode selecionar Visualizar HTML no menu Exibir para abrir a guia Visualizar HTML.
   >    * A visualização de HTML não é compatível com documentos de PDF, a visualização de HTML é somente para documentos XDP.
   >
   >

   >[!CAUTION]
   >
   >Para testar a experiência real do usuário final, visualize seus formulários em navegadores externos (Google Chrome, Microsoft Edge, Mozilla Firefox e muito mais) também. Cada navegador usa um mecanismo separado para renderizar o HTML, de modo que pode haver algumas diferenças na maneira como um formulário é visualizado no Designer e no navegador externo.

## Para visualizar um formulário usando dados de amostra {#to-preview-a-form-using-sample-data}

O Designer permite visualizar e testar o formulário usando dados XML de amostra. É recomendável testar frequentemente seu formulário com dados de amostra para garantir que ele seja renderizado corretamente.

Se você não tiver dados de amostra, o Designer poderá criá-los ou você mesmo poderá criá-los. (Consulte [Gerar automaticamente dados de exemplo para visualizar o formulário](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) e [Criar dados de exemplo para visualizar o formulário](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

Testar o formulário usando uma fonte de dados de amostra garante que os dados e campos sejam mapeados e que os subformulários de repetição sejam repetidos conforme esperado. Você pode criar um layout de formulário equilibrado que forneça o espaço apropriado para cada objeto exibir os dados mesclados.

1. Selecione **Arquivo > Propriedades do formulário**.

1. Clique na guia **Visualizar** e, na caixa Arquivo de dados, digite o caminho completo para o arquivo de dados de teste. Você também pode usar o botão Procurar para navegar até o arquivo.

1. Clique em **OK**. Na próxima vez que você visualizar o formulário na guia **Visualizar HTML**, os valores de dados do arquivo XML de amostra aparecerão nos respectivos objetos.

## Visualizar formulários em um repositório {#html-preview-of-forms-in-forms-manager}

No AEM Forms, é possível visualizar formulários e documentos em um repositório. A Pré-visualização ajuda a saber exatamente como os formulários aparecem e se comportam são usados pelos usuários finais.
