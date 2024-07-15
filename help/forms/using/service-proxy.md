---
title: proxy do serviço de formulários HTML5
description: O Proxy do Serviço de Formulários HTML5 é uma configuração para registrar um proxy para o serviço de envio. Para configurar o Proxy de Serviço, especifique a URL do serviço de envio por meio do parâmetro de solicitação submitServiceProxy.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# proxy do serviço de formulários HTML5{#html-forms-service-proxy}

O Proxy do Serviço de Formulários HTML5 é uma configuração para registrar um proxy para o serviço de envio. Para configurar o Proxy de Serviço, especifique a URL do serviço de envio por meio do parâmetro de solicitação *submitServiceProxy*.

## Benefícios do proxy de serviço {#benefits-of-service-proxy-br}

O proxy de serviço elimina o seguinte:

* o fluxo de trabalho de formulários HTML5 requer a abertura do serviço de envio &quot;/content/xfaforms/submit/default&quot; para os usuários de formulários HTML5. Ele expõe os servidores AEM a um público-alvo não-intencional mais amplo.
* A URL do serviço está incorporada no modelo de tempo de execução do formulário. Não é possível alterar o caminho da URL de serviço.
* O envio é um processo de duas etapas. Para enviar os dados do formulário, o envio requer pelo menos duas jornadas para o servidor. Assim, aumenta a carga no servidor.
* Os formulários HTML5 enviam dados na solicitação POST em vez da solicitação PDF. Para fluxos de trabalho envolvendo formulários PDF e HTML5, são necessários dois métodos diferentes de processamento dos envios.

### Topologias {#topologies-br}

Os formulários HTML5 podem usar as seguintes topologias para se conectar aos servidores AEM.

* Uma topologia em que o Servidor AEM ou o HTML 5 envia dados via POST para o servidor.
* Uma topologia em que o servidor proxy envia dados de POST para o servidor.

![topologias de proxy do serviço de formulários HTML5](assets/topology.png)

Topologias de proxy de serviço de formulários HTML5

Os formulários HTML5 se conectam aos servidores AEM para executar scripts do lado do servidor, serviços da Web e envios. O tempo de execução XFA dos formulários HTML5 usa chamadas Ajax no ponto final &quot;/bin/xfaforms/submitaction&quot; com vários parâmetros para se conectar aos servidores AEM. Os formulários HTML5 conectam servidores AEM para executar as seguintes operações:

#### Executar scripts de servidor e serviços da Web {#execute-server-sided-scripts-and-web-services}

Os scripts marcados para serem executados no servidor são conhecidos como scripts do lado do servidor. A tabela a seguir lista todos os parâmetros usados em scripts do lado do servidor e Serviços da Web.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>atividade</p> </td>
   <td><p>A atividade contém os eventos que acionam a solicitação. Como clicar, sair ou alterar</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom contém a expressão SOM do objeto onde os eventos são executados.</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>Template contém o template usado para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot contém o diretório raiz do modelo usado para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>Dados</p> </td>
   <td><p>Os dados contêm bytes de dados usados para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom contém DOM do formulário HTML5 no formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>pacote</p> </td>
   <td><p>o pacote é especificado como formulário.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir contém o diretório de depuração usado para processar o formulário.</p> </td>
  </tr>
 </tbody>
</table>

#### Enviar dados {#submit-data}

Ao clicar no botão enviar, os formulários HTML5 enviam dados para o servidor. A tabela a seguir lista todos os parâmetros que os formulários HTML5 enviam para o servidor.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>Modelo usado para processar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>diretório raiz do modelo usado para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>Dados</p> </td>
   <td><p>bytes bata usados para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>DOM do formulário HTML5 no formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>O URL onde o XML de dados é publicado.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>O diretório de depuração usado para processar o formulário.</p> </td>
  </tr>
 </tbody>
</table>

#### Como funciona o proxy de envio? {#how-nbsp-the-nbsp-submit-proxy-works}

O proxy de serviço de envio atua como uma passagem se o URL de envio não estiver presente no parâmetro de solicitação. Ela age como uma passagem. Ele envia a solicitação para o ponto de acesso /bin/xfaforms/submitaction e envia a resposta para o tempo de execução do XFA.

O proxy de serviço de envio seleciona uma topologia se o URL de envio estiver presente no parâmetro de solicitação.

* Se os servidores AEM publicarem os dados, o serviço de proxy atuará como uma passagem. Ele envia a solicitação para o ponto de acesso /bin/xfaforms/submitaction e envia a resposta para o tempo de execução do XFA.
* Se o proxy postar os dados, o serviço proxy transmitirá todos os parâmetros, exceto submitUrl, para o ponto de extremidade */bin/xfaforms/submitaction* e receberá bytes xml no fluxo de resposta. Em seguida, o serviço proxy publica os bytes xml de dados no submitUrl para processamento.

* Antes de enviar dados (solicitação de POST) para um servidor, os formulários HTML5 verificam a conectividade e a disponibilidade do servidor. Para verificar a conectividade e a disponibilidade, os formulários HTML enviam uma solicitação head vazia para o servidor. Se o servidor estiver disponível, o formulário HTML5 enviará dados (solicitação POST) para o servidor. Se o servidor não estiver disponível, uma mensagem de erro, *Não foi possível se conectar ao servidor,* será exibida. A detecção avançada evita que os usuários tenham dificuldade em preencher o formulário novamente. O servlet proxy manipula a solicitação head e não gera exceção.
