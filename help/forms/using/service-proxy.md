---
title: proxy do serviço de formulários HTML5
seo-title: proxy do serviço de formulários HTML5
description: O Proxy de Serviço de formulários HTML5 é uma configuração para registrar um proxy para o serviço de envio. Para configurar o Proxy de Serviço, especifique o URL do serviço de envio por meio do parâmetro de solicitação submitServiceProxy.
seo-description: O Proxy de Serviço de formulários HTML5 é uma configuração para registrar um proxy para o serviço de envio. Para configurar o Proxy de Serviço, especifique o URL do serviço de envio por meio do parâmetro de solicitação submitServiceProxy.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# proxy do serviço de formulários HTML5{#html-forms-service-proxy}

O Proxy de Serviço de formulários HTML5 é uma configuração para registrar um proxy para o serviço de envio. Para configurar o Proxy de Serviço, especifique o URL do serviço de envio por meio do parâmetro de solicitação *submitServiceProxy*.

## Benefícios do Proxy de Serviço {#benefits-of-service-proxy-br}

O proxy de serviço elimina o seguinte:

* O fluxo de trabalho de formulários HTML5 requer a abertura do serviço de envio &quot;/content/xfaforms/submit/default&quot; para os usuários de formulários HTML5. Ela expõe os servidores AEM a uma audiência não intencional mais ampla.
* O URL do serviço é incorporado no modelo de tempo de execução do formulário. Não é possível alterar o caminho do URL do serviço.
* O envio é um processo em duas etapas. Para enviar os dados do formulário, o envio requer pelo menos duas viagens ao servidor. Assim, aumenta a carga no servidor.
* Formulários HTML5 enviam dados na solicitação POST em vez da solicitação PDF. Para fluxo de trabalho que envolve formulários PDF e HTML5, são necessários dois métodos diferentes de processamento de envios.

### Topologias {#topologies-br}

Os formulários HTML5 podem usar as seguintes topologias para se conectar aos servidores AEM.

* Topologia na qual os formulários do AEM Server ou HTML5 enviam dados via POST para o servidor.
* Topologia na qual o servidor proxy envia dados POST para o servidor.

![Topologias proxy do serviço de formulários HTML5](assets/topology.png)

Topologias proxy do serviço de formulários HTML5

Formulários HTML5 conectam-se aos servidores AEM para executar scripts de servidor, serviços da Web e envios. O tempo de execução XFA dos formulários HTML5 usa chamadas Ajax no ponto final &quot;/bin/xfaforms/submitaction&quot; com vários parâmetros para se conectar aos servidores AEM. Formulários HTML5 conectam servidores AEM para executar as seguintes operações:

#### Executar scripts do lado do servidor e serviços da Web {#execute-server-sided-scripts-and-web-services}

Os scripts marcados para execução no servidor são conhecidos como scripts do lado do servidor. A tabela a seguir lista todos os parâmetros usados nos scripts do servidor e nos Serviços da Web.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>activity</p> </td>
   <td><p>A Atividade contém os eventos que acionam a solicitação. Como clicar, sair ou alterar</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom contém a expressão SOM do objeto no qual os eventos são executados.</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>O modelo contém o modelo usado para renderizar o formulário.</p> </td>
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
   <td><p>packet</p> </td>
   <td><p>o pacote é especificado como formulário.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir contém o diretório de depuração usado para renderizar o formulário.</p> </td>
  </tr>
 </tbody>
</table>

#### Enviar dados {#submit-data}

Ao clicar no botão Enviar, os formulários HTML5 enviam dados para o servidor. A tabela a seguir lista todos os parâmetros que os formulários HTML5 enviam para o servidor.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>Modelo usado para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>diretório raiz do modelo usado para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>Dados</p> </td>
   <td><p>bytes de dados usados para renderizar o formulário.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>DOM do formulário HTML5 no formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>O URL no qual o XML de dados é publicado.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>O diretório debug usado para renderizar o formulário.</p> </td>
  </tr>
 </tbody>
</table>

#### Como o proxy de envio funciona? {#how-nbsp-the-nbsp-submit-proxy-works}

O proxy de serviço de envio atua como uma passagem se o submiturl não estiver presente no parâmetro de solicitação. Funciona como uma passagem. Ele envia a solicitação para o ponto final /bin/xfaforms/submitaction e envia a resposta para o tempo de execução XFA.

O proxy de serviço de envio seleciona uma topologia se o submiturl estiver presente no parâmetro de solicitação.

* Se os servidores AEM postarem os dados, o serviço proxy atuará como uma passagem. Ele envia a solicitação para o ponto final /bin/xfaforms/submitaction e envia a resposta para o tempo de execução XFA.
* Se o proxy postar os dados, o serviço proxy passará todos os parâmetros, exceto submitUrl para o ponto final */bin/xfaforms/submitaction* , e receberá bytes xml no fluxo de resposta. Em seguida, o serviço proxy posta os bytes xml de dados no submitUrl para processamento.

* Antes de enviar dados (solicitação POST) para um servidor, os formulários HTML5 verificam a conectividade e a disponibilidade do servidor. Para verificar a conectividade e a disponibilidade, os formulários HTML enviam uma solicitação de cabeçalho vazio ao servidor. Se o servidor estiver disponível, o formulário HTML5 enviará dados (solicitação POST) ao servidor. Se o servidor não estiver disponível, uma mensagem de erro, *Não foi possível conectar-se ao servidor,* será exibida. A detecção avançada impede que os usuários sejam incomodados de repreencher o formulário. O servlet proxy lida com a solicitação de cabeçalho e não gera exceção.
