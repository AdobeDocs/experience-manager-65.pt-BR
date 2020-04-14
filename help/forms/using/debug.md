---
title: Depuração de formulários HTML5
seo-title: Depuração de formulários HTML5
description: As etapas da lista do documento para solucionar vários problemas conhecidos.
seo-description: As etapas da lista do documento para solucionar vários problemas conhecidos.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: 21efe30c6a69d04c737bc523aeaab504db8f605b

---


# Depuração de formulários HTML5 {#debugging-html-forms}

Este documento inclui vários cenários de solução de problemas. Para cada cenário, algumas etapas são fornecidas para solucionar o problema. Siga estas etapas e, se o problema persistir, configure o Logger para obter e revisar os registros em busca de erros/avisos. Para obter mais detalhes sobre o registro de formulários em HTML5, consulte [Geração de registros para formulários](/help/forms/using/enable-logs.md)em HTML5.

## Problema: Ao renderizar o formulário, vejo a página de exceção org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

Nos detalhes da exceção, pesquise por palavra **causada por**.

O motivo provável é que um ou mais parâmetros no URL estejam incorretos.

Verifique os seguintes parâmetros:

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>O nome de arquivo do modelo</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>O caminho onde o modelo e os recursos associados residem</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Caminho absoluto do arquivo de dados que é unido ao modelo.<br /> Observação: O caminho define o caminho absoluto do arquivo de dados.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de dados codificados UTF-8 que são mesclados com o modelo.</td>
  </tr>
 </tbody>
</table>

## Problema: Não é possível renderizar um formulário (uma mensagem de erro é exibida) {#problem-unable-to-render-form}

1. Verifique se os parâmetros especificados estão corretos. Para obter informações detalhadas sobre parâmetros, consulte [Renderizar parâmetros](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Faça logon no CRX Package Manager (em https://&lt;server>:&lt;port>/crx/packmgr/index.jsp) e verifique se os seguintes pacotes estão instalados corretamente:

   * adobe-lc-forms-content-pkg-&lt;versão>.zip
   * adobe-lc-forms-runtime-pkg-&lt;versão>.zip

1. Faça logon no CQ Web Console (Console do Felix) em https://&lt;servidor>:&lt;porta>/system/console/bundles.

   Verifique se o status dos seguintes pacotes está &quot;ativo&quot;:

   * escala-lang.bundle [osgi]
   (com.adobe.livecyclescala-lang.bundle)

   * Renderizador de formulários do Adobe XFA
   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC Connector
   (com.adobe.livecycle.adobe-lc-forms-lc-Connector)

## Problema: Renderizações de formulário sem estilos {#problem-form-renders-without-styles}

1. No seu navegador, abra Ferramentas **do** desenvolvedor. Verifique se perfil.css está disponível.
1. Se o arquivo perfil.css não estiver disponível, faça logon no CRX DE em https://&lt;servidor>:&lt;porta>/crx/de.
1. Na hierarquia de pastas à esquerda, navegue até /etc/clientlibs/fd/xfaforms/. Abra os arquivos css.txt listados nas pastas.

   * o perfil do visitante
   * tempo de execução
   * scrollnav
   * toolbar
   * xfalib

1. Verifique se os arquivos mencionados dentro do css.txt estão presentes no CRX DE lite em /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Se os arquivos mencionados não estiverem disponíveis, instale novamente o pacote adobe-lc-forms-runtime-pkg-&lt;versão>.zip.

### Problema: Erro inesperado encontrado {#problem-unexpected-error-encountered}

1. No URL do formulário, adicione um parâmetro de query debugClientLibs e defina seu valor como true (por exemplo: https://&lt;servidor>:&lt;porta>/content/xfaforms/profiles/test.html?contentRoot=&lt;algum caminho>&amp;template=&lt;nome do arquivo xdp>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. No navegador de desktop como o chrome, vá até Developer Tools -> Console.
1. Abra os registros para identificar o tipo de erro. Para obter informações detalhadas sobre registros, consulte [logs para formulários](/help/forms/using/enable-logs.md)HTML5.
1. Vá para Ferramentas do desenvolvedor -> Console. Use o rastreamento de pilha para localizar o código que está causando o erro. Depurar o erro para resolver o problema.

   >[!NOTE]
   >
   >Se houver falha de script, verifique se o mesmo problema ocorre durante a execução do formulário em PDF. Em caso afirmativo, há um problema na lógica de script de formulário.

## Problema: Não é possível enviar o formulário {#problem-unable-to-submit-the-form}

1. Verifique se você tem direitos de acesso ao servidor AEM e se está conectado ao servidor.
1. Verifique se o parâmetro submitUrl está correto.
1. Ative os registros do lado do cliente como mencionado em [Logs para os formulários](/help/forms/using/enable-logs.md) HTML5 usando a opção debug como **1-a5-b5-c5**. Em seguida, renderize o formulário e clique em Enviar. Abra o console de depuração do navegador e verifique se há um erro.
1. Localize os logs do servidor, conforme mencionado em [Logs, para os formulários](/help/forms/using/enable-logs.md)HTML5. Verifique se ocorreu algum erro nos registros do servidor durante o envio.

## Problema: Mensagens de erro localizadas não são exibidas {#problem-localized-error-messages-do-not-display}

1. Renderize o formulário com o parâmetro de query adicional **debugClientLibs=true** no navegador de desktop e vá para Ferramentas do desenvolvedor -> Recursos e verifique o arquivo I18N.css.
1. Se o arquivo não estiver disponível, faça logon no CRX DE em https://&lt;servidor>:&lt;porta>/crx/de.
1. Na hierarquia de pastas à esquerda, navegue até /libs/fd/xfaforms/clientlibs/I18N e verifique se os seguintes arquivos e pastas existem:

   * Namespace.js
   * LogMessages.js
   * Pastas para idiomas

1. Se algum dos arquivos ou pastas acima não existir, instale o pacote **adobe-lc-forms-runtime-pkg-&lt;versão>.zip** novamente.
1. Navegue até a pasta que tem o mesmo nome que o nome da localidade e verifique seu conteúdo. A pasta deve conter os seguintes arquivos:

   * I18N.js
   * js.txt

1. Verifique o conteúdo de js.txt e verifique se ele tem as seguintes entradas.

   ```
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: Imagem não aparecendo {#problem-image-not-showing-up}

1. Verifique se o URL da imagem está correto.
1. Verifique se o navegador suporta esse tipo de imagem.
1. Nos detalhes da exceção, pesquise por palavra **causada por**.

   O motivo provável é que um ou mais parâmetros no URL estejam incorretos.

   Verifique os seguintes parâmetros:
Texto da etapa

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>O nome de arquivo do modelo</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>O caminho onde o modelo e os recursos associados residem</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Caminho absoluto do arquivo de dados que é unido ao modelo.<br /> Observação: O caminho define o caminho absoluto do arquivo de dados.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de dados codificados UTF-8 que são mesclados com o modelo.</td>
  </tr>
 </tbody>
</table>

1. No navegador do desktop, vá para Ferramentas do desenvolvedor -> Recursos.

   Verifique no lado esquerdo em Quadros se essa imagem é exibida.
