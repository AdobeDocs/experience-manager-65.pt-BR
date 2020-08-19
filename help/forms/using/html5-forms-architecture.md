---
title: Arquitetura de formulários HTML5
seo-title: Arquitetura de formulários HTML5
description: Os formulários HTML5 são implantados como um pacote dentro da instância AEM incorporada e expõe a funcionalidade como ponto final REST sobre HTTP/S usando a arquitetura RESTful Apache Sling.
seo-description: Os formulários HTML5 são implantados como um pacote dentro da instância AEM incorporada e expõe a funcionalidade como ponto final REST sobre HTTP/S usando a arquitetura RESTful Apache Sling.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
translation-type: tm+mt
source-git-commit: 84dd0d551431169239f63cff62a015e15f998e7d
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 0%

---


# Arquitetura de formulários HTML5{#architecture-of-html-forms}

## Arquitetura {#architecture}

A funcionalidade de formulários HTML5 é implantada como um pacote dentro da instância de AEM incorporada e é exposta como um ponto final REST sobre HTTP/S usando a arquitetura RESTful [Apache Sling](https://sling.apache.org/).

![02-aem-forms-Architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Uso da estrutura Sling {#using-sling-framework}

[O Apache Sling](https://sling.apache.org/) é centrado em recursos. Ele usa um URL de solicitação para resolver o recurso primeiro. Cada recurso tem uma propriedade **sling:resourceType** (ou **sling:resourceSuperType**). Com base nessa propriedade, no método de solicitação e nas propriedades do URL de solicitação, um script sling é selecionado para lidar com a solicitação. Este script sling pode ser um JSP ou um servlet. Para formulários HTML5, os nós de **Perfil** atuam como recursos de sling e o **Perfil Renderer** atua como o script sling que lida com a solicitação para renderizar o formulário móvel com um perfil específico. Um renderizador de **Perfil** é um JSP que lê parâmetros de uma solicitação e chama o Forms OSGi Service.

Para obter detalhes sobre o terminal REST e os parâmetros de solicitação suportados, consulte [Renderizando modelo](/help/forms/using/rendering-form-template.md)de formulário.

Quando um usuário faz uma solicitação de um dispositivo cliente, como um navegador iOS ou Android, o Sling primeiro resolve o Nó de Perfil com base no URL da solicitação. A partir deste Nó de Perfil, é exibido **sling:resourceSuperType** e **sling:resourceType** para determinar todos os scripts disponíveis que podem lidar com essa solicitação de renderização de formulário. Em seguida, ele usa seletores de solicitação Sling junto com o método de solicitação para identificar o script mais adequado para lidar com essa solicitação. Quando a solicitação chegar a um JSP do renderizador de Perfis, o JSP chamará o serviço Forms OSGi.

Para obter mais detalhes sobre a resolução de scripts de sling, consulte [AEM Folha](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) de Bate-Papo ou decomposição [do Url de Sling do](https://sling.apache.org/site/url-decomposition.html)Apache.

#### Fluxo típico de chamada de processamento de formulário {#typical-form-processing-call-flow}

Os formulários HTML5 armazenam em cache todos os objetos intermediários necessários para processar (execução ou envio) um formulário na primeira solicitação. Ele não armazena em cache os objetos dependentes dos dados, pois é provável que esses objetos sejam alterados.

O Formulário móvel mantém dois níveis diferentes de cache, cache PreRender e Cache de renderização. O cache preRender contém todos os fragmentos e imagens de um modelo resolvido e o cache Render contém conteúdo renderizado, como HTML.

![Fluxo de trabalho de formulários HTML5](assets/cacheworkflow.png)

Fluxo de trabalho de formulários HTML5

Os formulários HTML5 não armazenam em cache modelos que têm referências ausentes de fragmentos e imagens. Se os formulários HTML5 levarem mais do que o tempo normal, verifique nos registros do servidor se há referências e avisos ausentes. Além disso, verifique se o tamanho máximo do objeto não foi atingido.

O serviço OSGi da Forms processa uma solicitação em duas etapas:

* **Geração** de layout e estado inicial do formulário: O serviço de renderização OSGi da Forms chama o componente Cache da Forms para determinar se o formulário já foi armazenado em cache e não foi invalidado. Se o formulário for armazenado em cache e válido, ele servirá o HTML gerado do cache. Se o formulário for invalidado, o serviço de renderização OSGi da Forms gerará o Layout inicial do formulário e o Estado do formulário no formato XML. Esse XML é transformado em layout HTML e Estado de formulário JSON inicial pelo serviço OSGi da Forms e armazenado em cache para solicitações subsequentes.
* **Forms** pré-preenchido: Durante a renderização, se um usuário solicitar formulários com dados pré-preenchidos, o serviço de renderização OSGi da Forms chamará o container de serviço da Forms e gerará um novo estado de Formulário com dados unidos. No entanto, como o layout já é gerado na etapa acima, essa chamada é mais rápida do que a primeira chamada. Essa chamada só executa a união de dados e os scripts são executados nos dados.

Se houver alguma atualização no formulário ou qualquer um dos ativos usados dentro do formulário, o componente de cache de formulário a detectará e o cache desse formulário específico será invalidado. Quando o serviço Forms OSGi concluir o processamento, o Perfil Renderer jsp adicionará referências e estilos da biblioteca JavaScript a esse formulário e retornará a resposta ao cliente. Um servidor Web típico como o [Apache](https://httpd.apache.org/) pode ser usado aqui com a compactação HTML ativada. Um servidor Web reduziria significativamente o tamanho da resposta, o tráfego de rede e o tempo necessário para transmitir os dados entre o servidor e o computador cliente.

Quando um usuário envia o formulário, o navegador envia o estado do formulário no formato JSON para o proxy [do serviço de](../../forms/using/service-proxy.md)envio; em seguida, o proxy de serviço de envio gera um XML de dados usando dados JSON e envia esse XML de dados para o terminal de envio.

## Componentes {#components}

Você precisa de um pacote complementar do AEM Forms para ativar formulários HTML5. Para obter informações sobre como instalar o pacote suplementar do AEM Forms, consulte [Instalação e configuração do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componentes do OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)** é o nome de exibição do pacote HTML5 formulários OSGi quando exibido da Visualização do pacote do console de administração Felix (https://[host]:[port]/system/console/bundles).

Este componente contém componentes OSGi para renderização, gerenciamento de cache e configurações.

#### Forms OSGi Service {#forms-osgi-service}

Este serviço OSGi contém a lógica para renderizar um XDP como HTML e manipula a submissão de um formulário para gerar XML de dados. Este serviço usa o container de serviço Forms. O container de serviço Forms chama internamente o componente nativo `XMLFormService.exe` que executa o processamento.

Se uma solicitação de renderização for recebida, esse componente chamará o container de serviço da Forms para gerar informações de layout e estado que são processadas posteriormente para gerar estados DOM de formulário HTML e JSON.

Esse componente também é responsável pela geração de dados XML a partir do JSON de estado de formulário enviado.

#### Componente de cache {#cache-component}

Os formulários HTML5 usam o cache para otimizar o throughput e o tempo de resposta. Você pode configurar o nível do serviço de cache para ajustar a compensação entre o desempenho e a utilização do espaço.

<table>
 <tbody>
  <tr>
   <th>Estratégia de cache</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Nenhum</td>
   <td>Não armazenar artefatos em cache<br /> </td>
  </tr>
  <tr>
   <td>Conservador</td>
   <td>Armazenar em cache somente artefatos intermediários que são gerados antes da renderização do modelo como o formulário que contém fragmentos e imagens em linha</td>
  </tr>
  <tr>
   <td>Agressivo</td>
   <td>Armazenar em cache conteúdo<br /> HTML renderizado Armazena em cache todos os artefatos em cache no nível Conservador.<br /> <strong>Observação</strong>: Essa estratégia resulta em melhor desempenho, mas consome mais memória para armazenar os artefatos em cache.</td>
  </tr>
 </tbody>
</table>

Os formulários HTML5 executam o cache na memória usando a estratégia LRU. Se a estratégia de cache estiver definida como Nenhum cache não será criado e os dados existentes do cache, se houver, serão apagados. Além da estratégia de cache, você também pode configurar o tamanho total do cache na memória, o que pode ajudar a ter o limite máximo no tamanho do cache e, se ele for além disso, usará o modo LRU para liberar os recursos do cache.

>[!NOTE]
>
>O cache na memória não é compartilhado entre nós do cluster.

#### Serviço de configuração {#configuration-service}

O Serviço de configuração permite o ajuste dos parâmetros de configuração e das configurações de cache para formulários HTML5.

Para atualizar essas configurações, vá para o Admin Console CQ Felix (disponível em https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr), procure e selecione Configuração do Forms móvel.

É possível configurar o tamanho do cache ou desativá-lo usando o serviço de configuração. Você também pode ativar a depuração usando o parâmetro Opções de depuração. Para obter mais informações sobre como depurar formulários, consulte [Depuração de formulários](/help/forms/using/debug.md)HTML5.

### Componentes de tempo de execução (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

O Pacote de tempo de execução contém as bibliotecas do lado do cliente usadas para renderizar formulários HTML.

**Componentes importantes disponíveis como parte do pacote de tempo de execução:**

#### Mecanismo de script {#scripting-engine}

A implementação do Adobe XFA suporta dois tipos de linguagens de script para permitir a execução lógica definida pelo usuário nos formulários: JavaScript e FormCalc.

O mecanismo de script do HTML Forms é gravado em JavaScript para suportar a API de scripts XFA em ambas as línguas.

No tempo de renderização, o script FormCalc é convertido (e armazenado em cache) em JavaScript no servidor transparente para o usuário ou designer.

Este mecanismo de script usa alguns dos recursos do ECMAScript5, como Object.defineProperty. O mecanismo/biblioteca é entregue como o CQ Client Lib com o nome da categoria **xfaforms.perfil**. Também fornece API **** FormBridge para permitir que portais ou aplicativos externos interajam com formulários. Usando o FormBridge, um aplicativo externo pode ocultar programaticamente certos elementos, obter ou definir seus valores ou alterar seus atributos.

Para obter mais detalhes, consulte o artigo [Form Bridge](/help/forms/using/form-bridge-apis.md) .

#### Mecanismo de layout {#layout-engine}

O layout e o aspecto visual dos formulários HTML5 são baseados nos recursos SVG 1.1, jQuery, BackBone e CSS3. A aparência inicial de um formulário é gerada e armazenada em cache no servidor. O ajuste desse layout inicial e quaisquer outras alterações incrementais no layout do formulário são gerenciados no cliente. Para isso, o pacote de tempo de execução contém um mecanismo de layout escrito em JavaScript e baseado em jQuery/Backbone. Esse mecanismo lida com todos os comportamentos dinâmicos, como Adicionar/Remover instâncias repetíveis, Layout de objeto expansível. Esse mecanismo de layout renderiza um formulário uma página de cada vez. Inicialmente, um usuário visualização somente uma página e a barra de rolagem horizontal é responsável apenas pela primeira página. No entanto, quando um usuário rola para baixo, a próxima página start a renderização. Essa execução página por página reduz a quantidade de tempo necessário para renderizar a primeira página em um navegador e melhora o desempenho percebido do formulário. Este mecanismo/biblioteca faz parte do CQ Client Lib com o nome da categoria **xfaforms.perfil**.

O Mecanismo de layout também contém um conjunto de widgets usados para capturar o valor dos campos de formulário de um usuário. Esses widgets são modelados como Widgets [da interface do](https://api.jqueryui.com/jQuery.widget/) jQuery que implementam certos contratos adicionais para funcionar perfeitamente com o mecanismo de layout.

Para obter mais detalhes sobre widgets e contratos correspondentes, consulte Widgets [personalizados para formulários](/help/forms/using/introduction-widgets.md)HTML5.

#### Estilo {#styling}

O estilo associado aos elementos HTML é adicionado em linha ou com base no bloco CSS incorporado. Alguns estilos comuns que não dependem do formulário fazem parte do CQ Client Lib com o nome da categoria xfaforms.perfil.

Além das propriedades de estilo padrão, cada elemento de formulário também contém certas classes CSS com base no tipo de elemento, nome e outras propriedades. Usando essas classes, é possível redefinir os elementos especificando seu próprio CSS.

Para obter mais detalhes sobre estilos e classes padrão, consulte [Introdução aos estilos](/help/forms/using/css-styles.md).

#### Script do lado do servidor e serviços da Web {#server-side-script-and-web-services}

Todos os scripts marcados para executar no servidor ou para chamar um serviço da Web (independentemente de onde estejam marcados para execução) sempre são executados no servidor.

O mecanismo de script do cliente:

1. Faz uma chamada síncrona para o servidor que transmite o estado atual do Formulário na forma de JSON
1. Executa o script ou o serviço Web no servidor
1. Gera um novo estado JSON
1. Une o novo estado JSON no cliente quando a resposta for retornada.

#### Pacotes de recursos de localização {#localization-resource-bundles}

Os formulários HTML5 suportam italiano (it), espanhol (es), português brasileiro (pt_BR), chinês simplificado (zh_CN), chinês tradicional (zh_TW), coreano (ko_KR), inglês (pt_BR), francês (fr_FR), alemão (de_DE) e japonês (ja). Com base na localidade recebida no cabeçalho da solicitação, o Pacote de recursos correspondente é enviado para o cliente. Este pacote de recursos é adicionado ao JSP do Perfil como um Client Lib do CQ com o nome da categoria **xfaforms.I18N**. Você pode substituir a lógica de escolher o pacote de localidade no perfil.

### Componentes Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

O pacote Sling contém conteúdo relacionado a Perfis e Perfil Renderer.

#### Perfis {#profiles}

Perfis são os nós de Recursos no sling que representam um formulário ou uma Família do Forms. No nível do CQ, esses perfis são nós JCR. Os nós residem na pasta **/conteúdo** no repositório JCR e podem estar dentro de qualquer subpasta na pasta **/conteúdo** .

#### Renderizadores de perfis {#profile-renderers}

O nó Perfil tem uma propriedade **sling:resourceSuperType** com valor **xfaforms/perfil**. Essa propriedade envia internamente solicitações para o script sling para nós de Perfil localizados na pasta **/libs/xfaforms/perfil** . Esses scripts são páginas JSP, que são container para reunir os formulários HTML e os artefatos JS/CSS necessários. As páginas incluem referências a:

* **xfaforms.I18N.&lt;locale>**: Esta biblioteca contém dados localizados.
* **xfaforms.perfil**: Esta biblioteca contém implementação para o mecanismo de script e layout XFA.

Essas bibliotecas são modeladas como Bibliotecas do cliente CQ, que aproveitam as vantagens dos recursos de concatenação automática, miniificação e compactação das bibliotecas JavaScript da estrutura do CQ.
Para obter mais informações sobre a CQ Client Libs, consulte Documentação do [CQ Clientlib](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html).

Como descrito acima, o renderizador de perfil JSP chama o Forms Service por meio de uma inclusão sling. Esse JSP também define várias opções de depuração com base na configuração do administrador ou nos parâmetros de solicitação.

Os formulários HTML5 permitem que os desenvolvedores criem o Perfil e o Perfil Renderer para personalizar a aparência dos formulários. Por exemplo, formulários HTML permitem que desenvolvedores integrem formulários em um painel ou seção &lt;div> de um portal HTML existente.
Para obter mais detalhes sobre como criar perfis personalizados, consulte [Criação de um Perfil](/help/forms/using/custom-profile.md)personalizado.
