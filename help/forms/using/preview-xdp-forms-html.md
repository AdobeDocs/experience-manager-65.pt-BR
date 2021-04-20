---
title: Gerar visualização HTML5 de um formulário XDP
seo-title: Gerar visualização HTML5 de um formulário XDP
description: A guia Visualizar HTML no LiveCycle Designer pode ser usada para visualizar formulários como eles aparecem em um navegador.
seo-description: A guia Visualizar HTML no LiveCycle Designer pode ser usada para visualizar formulários como eles aparecem em um navegador.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 14%

---


# Gerar visualização HTML5 de um formulário XDP{#generate-html-preview-of-an-xdp-form}

Ao projetar um formulário no AEM Forms Designer, além de visualizar a versão em PDF de um formulário, você também pode visualizar uma versão HTML5 dele. Você pode usar a guia **Visualizar HTML** para visualizar um formulário como ele apareceria em um navegador.

## Ativar a Visualização HTML para formulários XDP no Designer {#html-preview-of-forms-in-forms-designer}

Para permitir que o Designer gere a visualização em HTML de formulários XDP, execute as seguintes configurações:

* Configurar o serviço de autenticação do Apache Sling
* Desativar modo protegido
* Fornecer detalhes do servidor AEM Forms

### Configurar o Apache Sling Authentication Service {#configure-apache-sling-authentication-service}

1. Vá para `https://'[server]:[port]'/system/console/configMgr` no AEM Forms em execução no OSGi ou
   `https://'[server]:[port]'/lc/system/console/configMgr` no AEM Forms em execução no JEE.
1. Localize e clique em **Configuração do Apache Sling Authentication Service** para abri-lo no modo de edição.

1. Dependendo de você estar executando o AEM Forms em OSGi ou JEE, adicione o seguinte no campo **Requisitos de autenticação**:

   * AEM Forms no JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * AEM Forms no OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >Não copie e cole o valor especificado no campo Requisitos de autenticação , pois ele pode corromper os caracteres especiais no valor. Em vez disso, digite o valor especificado no campo .

1. Especifique um nome de usuário e senha nos campos **[!UICONTROL Nome de usuário anônimo]** e **[!UICONTROL Senha de usuário anônimo]**, respectivamente. As credenciais especificadas são usadas para lidar com autenticação anônima e permitir acesso a usuários anônimos.
1. Clique em **Save** para salvar a configuração.

### Desativar modo protegido {#disable-protected-mode}

O [modo protegido](../../forms/using/get-xdp-pdf-documents-aem.md) está ativado, por padrão. Mantenha-o ativado para os ambientes de produção. Você pode desativá-lo em um ambiente de desenvolvimento para visualizar o HTML5 Forms no Designer. Execute as seguintes etapas para desativá-lo:

1. Faça logon no Console da Web AEM como administrador.

   * O URL para AEM Forms no OSGi é `https://'[server]:[port]'/system/console/configMgr`
   * O URL para AEM Forms no JEE é `https://'[server]:[port]'/lc/system/console/configMgr`

1. Abra **[!UICONTROL Configurações do Forms Móvel]** para edição.
1. Desmarque a opção **[!UICONTROL Modo Protegido]** e clique em **[!UICONTROL Salvar]**.

### Fornecer detalhes do servidor AEM Forms {#provide-details-of-aem-forms-server}

1. No Designer, vá para **Ferramentas** > **Opções**.
1. Na janela Opções, selecione a página **Opções do Servidor**, forneça os detalhes a seguir e clique em **OK**.

   * **URL** do servidor: URL do servidor AEM Forms.

   * **Número** da porta HTTP: AEM porta do servidor. O valor padrão é 4502.
   * **Contexto de visualização HTML:** caminho do perfil para renderizar formulários XFA. Os perfis padrão a seguir são usados para visualizar o formulário no Designer. No entanto, também é possível especificar o caminho para um perfil personalizado.

      * `/content/xfaforms/profiles/default.html` (AEM Forms no OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms no JEE)
   * **Contexto do Forms Manager:** Caminho do contexto no qual a interface do usuário do Forms Manager é implantada. Os valores padrão são:

      * `/aem/forms` (AEM Forms no OSGi)
      * `/lc/forms` (AEM Forms no JEE)

   >[!NOTE]
   >
   >Certifique-se de que o servidor do AEM Forms esteja funcionando. A visualização HTML se conecta ao servidor CRX para *gerar* uma visualização.

   ![Opções do AEM Forms Designer  ](assets/server_options.png)

   Opções do AEM Forms Designer

1. Para visualizar um formulário em HTML, clique na guia **Preview HTML**.

   >[!NOTE]
   >
   >
   >
   >
   >    * Se a guia HTML Preview estiver fechada, pressione F4 para abrir a guia Preview HTML . Você também pode selecionar Visualizar HTML no menu Visualizar para abrir a guia Visualizar HTML .
   >    * A visualização HTML não oferece suporte a documentos PDF, a visualização HTML é apenas para documentos XDP.


   >[!CAUTION]
   >
   >Para testar a experiência real do usuário final, visualize seus formulários em navegadores externos (Google Chrome, Microsoft Edge, Mozilla Firefox e muito mais) também. Cada navegador usa um mecanismo separado para renderizar o HTML, de modo que pode haver algumas diferenças no modo como um formulário é visualizado no Designer e no navegador externo.

## Visualização de formulário usando dados de formulário {#to-preview-a-form-using-sample-data}

O Designer permite visualizar e testar o formulário usando dados XML de amostra. É recomendável testar frequentemente o formulário com dados de amostra para garantir que o formulário seja renderizado de forma correta.

Se não houver dados de amostra, o Designer poderá criá-los ou você mesmo poderá criá-los. (Consulte [Para gerar automaticamente os dados de amostra para visualizar um formulário](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) e [Para criar dados de amostra para visualizar um formulário](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

Testar seu formulário usando uma fonte de dados de amostra garante que os dados e campos sejam mapeados e que os subformulários repetitivos se repetem conforme o esperado. Você pode criar um layout equilibrado de formulário que proporciona o espaço adequado para que cada objeto apresente os dados unidos.

1. Selecione **Arquivo > Propriedades do formulário**.

1. Clique na guia **Preview** e, na caixa Arquivo de dados, digite o caminho completo para o arquivo de dados de teste. Você também pode usar o botão Procurar para navegar até o arquivo.

1. Clique em **OK**. Na próxima vez que você visualizar o formulário na guia **Visualizar HTML**, os valores de dados do arquivo XML de amostra aparecerão nos respectivos objetos.

## Visualizar formulários localizados em um repositório {#html-preview-of-forms-in-forms-manager}

No AEM Forms, é possível visualizar formulários e documentos em um repositório. A visualização ajuda a saber exatamente como os formulários se parecem e se comportam conforme serão usados pelos usuários finais.
