---
title: Depuração de formulários HTML5
description: As etapas da lista de documentos para solucionar vários problemas conhecidos.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: HTML5 Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Depuração de formulários HTML5 {#debugging-html-forms}

Este documento inclui vários cenários de solução de problemas. Para cada cenário, algumas etapas são fornecidas para solucionar o problema. Siga estas etapas e, se o problema persistir, configure o Logger para obter e revisar logs para erros/avisos. Para obter mais detalhes sobre o registro de formulários HTML5, consulte [Geração de logs para formulários HTML5](/help/forms/using/enable-logs.md).

## Problema: ao renderizar o formulário, vejo a página de exceção org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

Nos detalhes da exceção, pesquise por palavra **causado por**.

O motivo provável é que um ou mais parâmetros no URL estão incorretos.

Verifique os seguintes parâmetros:

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>modelo</td>
   <td>O nome do arquivo do modelo</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>O caminho onde o modelo e os recursos associados residem</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Caminho absoluto do arquivo de dados que é mesclado com o modelo.<br /> Observação: O caminho define o caminho absoluto do arquivo de dados.</td>
  </tr>
  <tr>
   <td>dados</td>
   <td>Bytes de dados codificados por UTF-8 que são mesclados com o modelo.</td>
  </tr>
 </tbody>
</table>

## Problema: Não é possível renderizar um formulário (uma mensagem de erro é exibida) {#problem-unable-to-render-form}

1. Verifique se os parâmetros especificados estão corretos. Para obter informações detalhadas sobre parâmetros, consulte [Parâmetros de renderização](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Faça logon no Gerenciador de pacotes do CRX (em https://)&lt;server>:&lt;port>/crx/packmgr/index.jsp) e verifique se os seguintes pacotes estão instalados corretamente:

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. Faça logon no Console da Web do CQ (Felix Console) em https://&lt;server>:&lt;port>/system/console/bundles.

   Verifique se o status dos seguintes pacotes é &quot;ativo&quot;:

   * scala-lang.bundle [osgi]

   (com.adobe.livecyescala-lang.bundle)

   * Renderizador de Forms do Adobe XFA

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Conector Adobe XFA Forms LC

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problema: formulário é renderizado sem estilos {#problem-form-renders-without-styles}

1. No navegador, abra **Ferramentas do desenvolvedor**. Certifique-se de que profile.css esteja disponível.
1. Se o arquivo profile.css não estiver disponível, faça logon no CRX DE em https://&lt;server>:&lt;port>/crx/de.
1. Na hierarquia de pastas à esquerda, navegue até /etc/clientlibs/fd/xfaforms/. Abra os arquivos css.txt listados nas pastas.

   * perfil
   * tempo de execução
   * scrollnav
   * barra de ferramentas
   * xfalib

1. Verifique se os arquivos mencionados no css.txt estão presentes no CRX DE lite em /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Se os arquivos mencionados não estiverem disponíveis, instale o arquivo adobe-lc-forms-runtime-pkg-&lt;version>pacote .zip novamente.

### Problema: erro inesperado encontrado {#problem-unexpected-error-encountered}

1. No URL do formulário, adicione um parâmetro de consulta debugClientLibs e defina seu valor como true (Por exemplo: https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path=&quot;&quot;>&amp;modelo=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. No navegador do desktop, como o chrome, acesse Ferramentas do desenvolvedor > Console.
1. Abra os logs para identificar o tipo de erro. Para obter informações detalhadas sobre logs, consulte [registros para formulários HTML5](/help/forms/using/enable-logs.md).
1. Acesse Ferramentas do desenvolvedor > Console. Use o rastreamento de pilha para localizar o código que está causando o erro. Depurar o erro para resolver o problema.

   >[!NOTE]
   >
   >Se for uma falha de script, verifique se o mesmo problema ocorre durante a representação PDF do formulário também. Se sim, então há um problema na lógica do script de formulário.

## Problema: não é possível enviar o formulário {#problem-unable-to-submit-the-form}

1. Verifique se você tem direitos de acesso ao servidor AEM e se está conectado ao servidor.
1. Verifique se o parâmetro submitUrl está correto.
1. Ative os registros do lado do cliente conforme mencionado em [Logs para os formulários HTML5](/help/forms/using/enable-logs.md) usando a opção de depuração como **1-a5-b5-c5**. Em seguida, renderize o formulário e clique em submit. Abra o console de depuração do navegador e verifique se há um erro.
1. Localize os registros do servidor conforme mencionado em [Logs para os formulários HTML5](/help/forms/using/enable-logs.md). Verifique se houve algum erro nos logs do servidor durante o envio.

## Problema: as mensagens de erro localizadas não são exibidas {#problem-localized-error-messages-do-not-display}

1. Renderizar o formulário com parâmetro de consulta adicional **debugClientLibs=true** no navegador do desktop, acesse Ferramentas do desenvolvedor > Recursos e verifique o arquivo I18N.css.
1. Se o arquivo não estiver disponível, faça logon no CRX DE em https://&lt;server>:&lt;port>/crx/de.
1. Na hierarquia de pastas à esquerda, navegue até /libs/fd/xfaforms/clientlibs/I18N e verifique se os seguintes arquivos e pastas existem:

   * Namespace.js
   * LogMessages.js
   * Pastas para idiomas

1. Se algum dos arquivos ou pastas acima não existir, instale o **adobe-lc-forms-runtime-pkg-&lt;version>.zip** pacote novamente.
1. Navegue até a pasta que tem o mesmo nome da localidade e verifique seu conteúdo. A pasta deve conter os seguintes arquivos:

   * I18N.js
   * js.txt

1. Verifique o conteúdo do js.txt e certifique-se de que ele tenha as entradas a seguir.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: a imagem não é exibida {#problem-image-not-showing-up}

1. Verifique se o URL da imagem está correto.
1. Verifique se o navegador é compatível com esse tipo de imagem.
1. Nos detalhes da exceção, pesquise por palavra **causado por**.

   O motivo provável é que um ou mais parâmetros no URL estão incorretos.

   Verifique os seguintes parâmetros: Texto da etapa

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>modelo</td>
   <td>O nome do arquivo do modelo</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>O caminho onde o modelo e os recursos associados residem</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Caminho absoluto do arquivo de dados que é mesclado com o modelo.<br /> Observação: O caminho define o caminho absoluto do arquivo de dados.</td>
  </tr>
  <tr>
   <td>dados</td>
   <td>Bytes de dados codificados por UTF-8 que são mesclados com o modelo.</td>
  </tr>
 </tbody>
</table>

1. No navegador do desktop, acesse Ferramentas do desenvolvedor > Recursos.

   Verifique no lado esquerdo em Quadros se essa imagem é exibida.
