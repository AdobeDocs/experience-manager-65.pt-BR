---
title: Depuração de formulários HTML5
seo-title: Debugging HTML5 forms
description: As etapas da lista de documentos para solucionar vários problemas conhecidos.
seo-description: The document list steps to troubleshoot various known issues.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# Depuração de formulários HTML5 {#debugging-html-forms}

Este documento inclui vários cenários de solução de problemas. Para cada cenário, algumas etapas são fornecidas para solucionar o problema. Siga estas etapas e, se o problema persistir, configure o Logger para obter e revisar os logs quanto a erros/avisos. Para obter mais detalhes sobre o registro em log de formulários do HTML5, consulte [Geração de logs para formulários HTML5](/help/forms/using/enable-logs.md).

## Problema: Ao renderizar o formulário, vejo a página de exceção org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

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
   <td>template</td>
   <td>O nome do arquivo do modelo</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>O caminho onde o modelo e os recursos associados residem</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Caminho absoluto do arquivo de dados que é unido ao modelo.<br /> Observação: Path define o caminho absoluto do arquivo de dados.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de dados codificados UTF-8 que são mesclados com o modelo.</td>
  </tr>
 </tbody>
</table>

## Problema: Não é possível renderizar um formulário (uma mensagem de erro é exibida) {#problem-unable-to-render-form}

1. Verifique se os parâmetros especificados estão corretos. Para obter informações detalhadas sobre parâmetros, consulte [Parâmetros de renderização](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Faça logon no Gerenciador de pacotes do CRX (em https://&lt;server>:&lt;port>/crx/packmgr/index.jsp) e verifique se os seguintes pacotes estão instalados corretamente:

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. Faça logon no Console da Web do CQ (Felix Console) em https://&lt;server>:&lt;port>/system/console/bundles.

   Certifique-se de que o status dos seguintes pacotes esteja &quot;ativo&quot;:

   * escala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * Renderizador Forms do Adobe XFA

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Conector LC do Adobe XFA Forms

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problema: Renderizações de formulário sem estilos {#problem-form-renders-without-styles}

1. No seu navegador, abra **Ferramentas do desenvolvedor**. Certifique-se de que profile.css esteja disponível.
1. Se o arquivo profile.css não estiver disponível, faça logon no CRX DE em https://&lt;server>:&lt;port>/crx/de.
1. Na hierarquia de pastas à esquerda, navegue até /etc/clientlibs/fd/xfaforms/. Abra os arquivos css.txt listados nas pastas.

   * o perfil do visitante
   * tempo de execução
   * scrollnav
   * toolbar
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

1. Se os arquivos mencionados não estiverem disponíveis, instale o adobe-lc-forms-runtime-pkg-&lt;version>pacote .zip novamente.

### Problema: Erro inesperado encontrado {#problem-unexpected-error-encountered}

1. No URL do formulário, adicione um parâmetro de consulta debugClientLibs e defina seu valor como true (Por exemplo: https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path=&quot;&quot;>&amp;template=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. No navegador de desktop como o chrome, acesse Ferramentas do desenvolvedor -> Console.
1. Abra os logs para identificar o tipo de erro. Para obter informações detalhadas sobre logs, consulte [registros para formulários HTML5](/help/forms/using/enable-logs.md).
1. Acesse Ferramentas do desenvolvedor -> Console. Use o rastreamento de pilha para localizar o código que está causando o erro. Depurar o erro para resolver o problema.

   >[!NOTE]
   >
   >Se houver falha no script, verifique se o mesmo problema ocorre durante a renderização do PDF do formulário. Em caso afirmativo, há um problema na lógica de script de formulário.

## Problema: Não é possível enviar o formulário {#problem-unable-to-submit-the-form}

1. Certifique-se de ter direitos para acessar o servidor AEM e estar conectado ao servidor.
1. Verifique se o parâmetro submitUrl está correto.
1. Habilite os logs do lado do cliente, conforme mencionado em [Registros para os formulários HTML5](/help/forms/using/enable-logs.md) usando a opção de depuração como **1-a5-b5-c5**. Em seguida, renderize o formulário e clique em enviar. Abra o console de depuração do navegador e verifique se há um erro.
1. Localize os logs do servidor, como mencionado em [Registros para os formulários HTML5](/help/forms/using/enable-logs.md). Verifique se houve algum erro nos logs do servidor durante o envio.

## Problema: Mensagens de erro localizadas não são exibidas {#problem-localized-error-messages-do-not-display}

1. Renderizar o formulário com um parâmetro de consulta adicional **debugClientLibs=true** no navegador do desktop, acesse Ferramentas do desenvolvedor -> Recursos e verifique o arquivo I18N.css.
1. Se o arquivo não estiver disponível, faça logon no CRX DE em https://&lt;server>:&lt;port>/crx/de.
1. Na hierarquia de pastas à esquerda, navegue até /libs/fd/xfaforms/clientlibs/I18N e verifique se os seguintes arquivos e pastas existem:

   * Namespace.js
   * LogMessages.js
   * Pastas para idiomas

1. Se algum dos arquivos ou pastas acima não existir, instale o **adobe-lc-forms-runtime-pkg-&lt;version>.zip** pacote novamente.
1. Navegue até a pasta que tem o mesmo nome do local e verifique seu conteúdo. A pasta deve conter os seguintes arquivos:

   * I18N.js
   * js.txt

1. Verifique o conteúdo de js.txt e verifique se ele tem as seguintes entradas.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: Imagem não exibida {#problem-image-not-showing-up}

1. Certifique-se de que o URL da imagem esteja correto.
1. Verifique se o navegador aceita esse tipo de imagem.
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
   <td>template</td>
   <td>O nome do arquivo do modelo</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>O caminho onde o modelo e os recursos associados residem</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Caminho absoluto do arquivo de dados que é unido ao modelo.<br /> Observação: Path define o caminho absoluto do arquivo de dados.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de dados codificados UTF-8 que são mesclados com o modelo.</td>
  </tr>
 </tbody>
</table>

1. No navegador do desktop, acesse Ferramentas do desenvolvedor -> Recursos.

   Verifique o lado esquerdo em Quadros se essa imagem for exibida.
