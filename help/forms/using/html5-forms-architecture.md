---
title: Arquitetura de formulários HTML5
description: Os formulários HTML5 são implantados como um pacote na instância AEM incorporada e expõem a funcionalidade como ponto final REST sobre HTTP/S usando a arquitetura RESTful Apache Sling.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 0%

---

# Arquitetura de formulários HTML5{#architecture-of-html-forms}

## Arquitetura {#architecture}

A funcionalidade de formulários HTML5 é implantada como um pacote na instância AEM incorporada e é exposta como um ponto final REST sobre HTTP/S usando RESTful [Apache Sling Architecture](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Uso da estrutura Sling {#using-sling-framework}

O [Apache Sling](https://sling.apache.org/) é centrado em recursos. Ele usa um URL de solicitação para resolver primeiro o recurso. Cada recurso tem uma propriedade **sling:resourceType** (ou **sling:resourceSuperType**). Com base nessa propriedade, no método de solicitação e nas propriedades do URL de solicitação, um script sling é selecionado para lidar com a solicitação. Esse script sling pode ser um JSP ou um servlet. Para formulários HTML5, os nós **Perfil** atuam como recursos de sling e o **Renderizador de Perfil** atua como o script de sling que lida com a solicitação para renderizar o formulário para dispositivos móveis com um perfil específico. O **Renderizador de Perfil** é um JSP que lê parâmetros de uma solicitação e chama o Serviço OSGi do Forms.

Para obter detalhes sobre o ponto de extremidade REST e os parâmetros de solicitação com suporte, consulte [Renderizando Modelo de Formulário](/help/forms/using/rendering-form-template.md).

Quando um usuário faz uma solicitação de um dispositivo cliente, como um navegador iOS ou Android™, o Sling primeiro resolve o nó de perfil com base no URL da solicitação. Deste Nó de Perfil, ele lê **sling:resourceSuperType** e **sling:resourceType** para determinar todos os scripts disponíveis que podem lidar com essa solicitação de Renderização de Formulário. Em seguida, ele usa seletores de solicitação Sling juntamente com o método de solicitação para identificar o script mais adequado para lidar com essa solicitação. Quando a solicitação atinge uma JSP de renderizador de perfil, a JSP chama o serviço OSGi do Forms.

Para obter mais detalhes sobre a resolução do script sling, consulte [Folha de características do AEM Sling](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR) ou [Decomposição do URL do Apache Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### Fluxo de chamadas de processamento de formulário típico {#typical-form-processing-call-flow}

Os forms HTML5 armazenam em cache todos os objetos intermediários necessários para processar (representação ou envio) um form na primeira solicitação. Ele não armazena em cache os objetos dependentes dos dados, pois esses objetos provavelmente serão alterados.

O Formulário para publicação de conteúdo para dispositivos móveis mantém dois níveis diferentes de cache, Cache de pré-renderização e Cache de renderização. O cache preRender contém todos os fragmentos e imagens de um modelo resolvido e o cache Render contém conteúdo renderizado, como HTML.

![fluxo de trabalho de formulários HTML5](assets/cacheworkflow.png)

fluxo de trabalho de formulários HTML5

Os formulários do HTML5 não armazenam em cache modelos que têm referências ausentes de fragmentos e imagens. Se os formulários HTML5 demorarem mais do que o tempo normal, verifique os registros do servidor em busca de referências e avisos ausentes. Além disso, verifique se o tamanho máximo do objeto não foi atingido.

O serviço OSGi do Forms processa uma solicitação em duas etapas:

* **Geração de layout e estado inicial do formulário**: o serviço de renderização OSGi do Forms chama o componente de cache do Forms para determinar se o formulário já foi armazenado em cache e não foi invalidado. Se o formulário for armazenado em cache e válido, ele fornecerá o HTML gerado do cache. Se o formulário for invalidado, o serviço de renderização OSGi do Forms gerará o Layout de formulário inicial e o Estado de formulário no formato XML. Esse XML é transformado em layout de HTML e estado de formulário JSON inicial pelo serviço OSGi do Forms e, em seguida, armazenado em cache para solicitações subsequentes.
* **Forms pré-preenchido**: durante a renderização, se um usuário solicitar formulários com dados pré-preenchidos, o serviço de renderização OSGi do Forms chamará o contêiner de serviço do Forms e gerará um novo estado de Formulário com dados mesclados. No entanto, como o layout já foi gerado na etapa acima, essa chamada é mais rápida do que a primeira chamada. Essa chamada só executa a mesclagem de dados e executa os scripts nos dados.

Se houver qualquer atualização no formulário ou qualquer um dos ativos usados dentro do formulário, o componente de cache de formulários a detectará e o cache desse formulário específico será invalidado. Depois que o serviço OSGi do Forms conclui o processamento, a jsp do Renderizador de perfil adiciona referências e estilos da biblioteca do JavaScript a este formulário e retorna a resposta ao cliente. Um servidor Web típico como [Apache](https://httpd.apache.org/) pode ser usado aqui com a compactação HTML ativada. Um servidor Web reduziria significativamente o tamanho da resposta, o tráfego de rede e o tempo necessário para transmitir os dados entre o servidor e a máquina cliente.

Quando um usuário envia o formulário, o navegador envia o estado do formulário em formato JSON para o [proxy de serviço de envio](../../forms/using/service-proxy.md); em seguida, o proxy de serviço de envio gera um XML de dados usando dados JSON e envia esse XML de dados para o ponto de extremidade de envio.

## Componentes {#components}

Você precisa de um pacote complementar do AEM Forms para ativar os formulários HTML5. Para obter informações sobre como instalar o pacote complementar do AEM Forms, consulte [Instalação e configuração do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componentes OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

O **Renderizador de Forms do Adobe XFA (com.adobe.livecycle.adobe-lc-forms-core)** é o nome de exibição do pacote OSGi do HTML5 forms quando visualizado na Exibição de pacote do console de administração Felix (https://[host]:[port]/system/console/bundles).

Este componente contém componentes OSGi para renderização, gerenciamento de cache e definições de configuração.

#### Serviço OSGi do Forms {#forms-osgi-service}

Esse serviço OSGi contém a lógica para renderizar um XDP como HTML e lida com o envio de um formulário para gerar dados XML. Este serviço usa o contêiner de serviço do Forms. O contêiner de serviço do Forms chama internamente o componente nativo `XMLFormService.exe` que executa o processamento.

Se uma solicitação de renderização for recebida, esse componente chamará o contêiner de serviço Forms para gerar informações de layout e estado que são processadas para gerar estados DOM de formulário HTML e JSON.

Esse componente também é responsável por gerar dados XML a partir do JSON de estado de formulário enviado.

#### Componente de cache {#cache-component}

O HTML5 forms usa o cache para otimizar a taxa de transferência e o tempo de resposta. Você pode configurar o nível do serviço de cache para ajustar o equilíbrio entre o desempenho e a utilização do espaço.

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
   <td>Armazenar em cache somente artefatos intermediários gerados antes do renderizador do formulário, como modelo contendo fragmentos e imagens embutidas</td>
  </tr>
  <tr>
   <td>Agressivo</td>
   <td>Armazenar em cache conteúdo de HTML renderizado <br /> Armazenar em cache todos os artefatos no nível Conservador.<br /> <strong>Observação</strong>: essa estratégia resulta em melhor desempenho, mas consome mais memória para armazenar os artefatos em cache.</td>
  </tr>
 </tbody>
</table>

Os formulários HTML5 executam cache na memória usando a estratégia LRU. Se a estratégia de cache estiver definida como Nenhum, o cache não será criado e os dados existentes do cache, se houver, serão apagados. Além da estratégia de armazenamento em cache, você também pode configurar o tamanho total do cache na memória, o que pode ajudar a ter o máximo vinculado ao tamanho do cache e, se ele for além disso, usará o modo LRU para liberar recursos do cache.

>[!NOTE]
>
>O cache na memória não é compartilhado entre nós de cluster.

#### Serviço de configuração {#configuration-service}

O Serviço de Configuração habilita o ajuste dos parâmetros de configuração e das definições de cache para formulários HTML5.

Para atualizar essas configurações, vá para o CQ Felix Admin Console (disponível em https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr), pesquise e selecione Mobile Forms Configuration.

Você pode configurar o tamanho do cache ou desabilitá-lo usando o serviço de configuração. Você também pode ativar a depuração usando o parâmetro Opções de depuração. Mais informações sobre a depuração de formulários podem ser encontradas em [Depurando formulários HTML5](/help/forms/using/debug.md).

### Componentes de tempo de execução (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

O Pacote de tempo de execução contém as bibliotecas do lado do cliente usadas para renderizar formulários de HTML.

**Componentes importantes disponíveis como parte do pacote de Tempo de Execução:**

#### Mecanismo de script {#scripting-engine}

A implementação do Adobe XFA é compatível com dois tipos de linguagens de script para permitir a execução lógica definida pelo usuário nos formulários: JavaScript e FormCalc.

O mecanismo de script do HTML Forms foi criado no JavaScript para oferecer suporte à API de script XFA em ambos os idiomas.

No momento da renderização, o script FormCalc é traduzido (e armazenado em cache) no JavaScript no servidor transparente para o usuário ou designer.

Esse mecanismo de script usa alguns dos recursos do ECMAScript5 como Object.defineProperty. O mecanismo/biblioteca é fornecido como uma biblioteca do cliente CQ com o nome de categoria **xfaforms.profile**. Também fornece a **API FormBridge** para habilitar portais ou aplicativos externos para interagir com o formulário. Usando o FormBridge, um aplicativo externo pode ocultar programaticamente determinados elementos, obter ou definir seus valores ou alterar seus atributos.

Para obter mais detalhes, consulte o artigo [Formulário Bridge](/help/forms/using/form-bridge-apis.md).

#### Mecanismo de layout {#layout-engine}

O layout e o aspecto visual dos formulários HTML5 são baseados nos recursos SVG 1.1, jQuery, BackBone e CSS3. A aparência inicial de um formulário é gerada e armazenada em cache no servidor. O ajuste desse layout inicial e quaisquer outras alterações incrementais no layout do formulário são gerenciados no cliente. Para isso, o pacote de Tempo de execução contém um mecanismo de layout escrito no JavaScript e baseado em jQuery/Backbone. Esse mecanismo lida com todo o comportamento dinâmico, como Adicionar/Remover instâncias repetíveis e o layout de objetos expansíveis. Este mecanismo de layout renderiza um formulário uma página por vez. Inicialmente, um usuário visualiza apenas uma página e a barra de rolagem horizontal é responsável apenas pela primeira página. No entanto, quando um usuário rola para baixo, a próxima página inicia a renderização. Essa representação página por página reduz a quantidade de tempo necessária para renderizar a primeira página em um navegador e melhora o desempenho percebido do formulário. Este mecanismo/biblioteca faz parte da Biblioteca de Cliente CQ com o nome de categoria **xfaforms.profile**.

O Mecanismo de layout também contém um conjunto de widgets usados para capturar o valor de campos de formulário de um usuário. Esses widgets são modelados como [Widgets da interface do usuário do jQuery](https://api.jqueryui.com/jQuery.widget/) que implementam determinado contrato adicional para funcionar perfeitamente com o mecanismo de Layout.

Para obter mais detalhes sobre widgets e contratos correspondentes, consulte [Widgets personalizados para formulários HTML5](/help/forms/using/introduction-widgets.md).

#### Estilo {#styling}

O estilo associado aos elementos HTML é adicionado em linha ou com base no bloco CSS incorporado. Alguns estilos comuns que não dependem do formulário fazem parte da Biblioteca do cliente CQ com o nome de categoria xfaforms.profile.

Além das propriedades de estilo padrão, cada elemento de formulário também contém determinadas classes CSS com base no tipo de elemento, nome e outras propriedades. Usando essas classes, é possível reestilizar elementos especificando seu próprio CSS.

Para obter mais detalhes sobre estilos e classes padrão, consulte [Introdução a estilos](/help/forms/using/css-styles.md).

#### Script do lado do servidor e serviços da Web {#server-side-script-and-web-services}

Qualquer script que esteja marcado para execução no servidor ou marcado para chamar um Serviço da Web (independentemente de onde esteja marcado para execução) sempre é executado no servidor.

O mecanismo de script do cliente:

1. Faz uma chamada síncrona para o servidor que passa o estado de Formulário atual na forma de JSON
1. Executa o script ou o Serviço da Web no servidor
1. Gera um novo estado JSON
1. Mescla o novo estado JSON no cliente quando a resposta é retornada.

#### Pacotes de recursos de localização {#localization-resource-bundles}

Os formulários HTML5 são compatíveis com os idiomas italiano (it), espanhol (es), português do Brasil (pt_BR), chinês simplificado (zh_CN), chinês tradicional (suporte limitado apenas) (zh_TW), coreano (ko_KR), inglês (en_US), francês (fr_FR), alemão (de_DE) e japonês (ja). Com base na localidade recebida no cabeçalho da solicitação, o Conjunto de recursos correspondente é enviado ao cliente. Este conjunto de recursos foi adicionado ao Perfil JSP como uma Biblioteca de Cliente CQ com o nome de categoria **xfaforms.I18N**. Você pode substituir a lógica de coleta do pacote de localidade no perfil.

### Componentes do Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

O pacote do Sling tem conteúdo relacionado a Perfis e Renderizador de perfil.

#### Perfis {#profiles}

Perfis são os nós de Recurso no sling que representam um formulário ou uma Família do Forms. No Nível do CQ, esses perfis são nós JCR. Os nós residem na pasta **/content** no repositório JCR e podem estar dentro de qualquer subpasta na pasta **/content**.

#### Renderizadores de perfis {#profile-renderers}

O nó de Perfil tem uma propriedade **sling:resourceSuperType** com valor **xfaforms/profile**. Esta propriedade envia internamente solicitações de encaminhamento ao script sling para nós Profile na pasta **/libs/xfaforms/profile**. Esses scripts são páginas JSP, que são containers para reunir os formulários de HTML e os artefatos JS/CSS necessários. As páginas incluem referências a:

* **xfaforms.I18N.&lt;locale>**: esta biblioteca contém dados localizados.
* **xfaforms.profile**: esta biblioteca contém a implementação do mecanismo de Layout e Script XFA.

Essas bibliotecas são modeladas como Bibliotecas de clientes do CQ que tiram vantagens dos recursos de concatenação automática, minificação e compactação das bibliotecas JavaScript da estrutura do CQ.
Para obter mais informações sobre as Bibliotecas de Clientes CQ, consulte a [Documentação da Biblioteca de Clientes CQ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR).

Conforme descrito acima, o renderizador de perfil JSP chama o serviço do Forms por meio de uma inclusão de sling. Este JSP também define várias opções de depuração baseadas na configuração administrativa ou parâmetros de solicitação.

Os formulários HTML5 permitem que os desenvolvedores criem Perfil e Renderizador de perfil para personalizar a aparência dos formulários. Por exemplo, os formulários de HTML permitem que os desenvolvedores integrem formulários em um painel ou seção &lt;div> de um portal de HTML existente.
Para obter mais detalhes sobre como criar perfis personalizados, consulte [Criando um Perfil Personalizado](/help/forms/using/custom-profile.md).
