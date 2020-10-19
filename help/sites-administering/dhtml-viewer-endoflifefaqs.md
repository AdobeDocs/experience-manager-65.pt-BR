---
title: 'Perguntas frequentes sobre fim de vida útil de visualizadores DHTML '
seo-title: 'Perguntas frequentes sobre fim de vida útil de visualizadores DHTML '
description: A partir de 31 de janeiro de 2014, a plataforma do visualizador DHTML da Scene7 será oficialmente encerrada. Esta notificação fornece respostas para perguntas frequentes para que você possa se preparar para essa transição para a nova plataforma do visualizador HTML5.
seo-description: A partir de 31 de janeiro de 2014, a plataforma do visualizador DHTML da Scene7 será oficialmente encerrada. Esta notificação fornece respostas para perguntas frequentes para que você possa se preparar para essa transição para a nova plataforma do visualizador HTML5.
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: 283802809d665cd979e2f1a4fa969b6ddc491ed6
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---


# Perguntas frequentes sobre fim de vida útil de visualizadores DHTML {#dhtml-viewer-end-of-life-faqs}

A partir de 31 de janeiro de 2014, a plataforma do visualizador DHTML da Scene7 será oficialmente encerrada. Esta notificação fornece respostas para perguntas frequentes para que você possa se preparar para essa transição para a nova plataforma do visualizador HTML5.

**Qual é a mudança?**

A partir de 31 de janeiro de 2014, a Scene7 oferecerá suporte oficial ao fim da vida útil da plataforma do visualizador DHTML.

**O que significa o fim da vida?**

Fim da vida útil significa que a Scene7 (1) não adicionará mais nenhum aprimoramento de recursos à plataforma do visualizador DHTML (2) não mais endereçará nem lançará nenhuma correção de erros na plataforma do visualizador DHTML e (3) o atendimento ao cliente não estará mais solucionando problemas ou fornecendo suporte para quaisquer problemas ou perguntas do visualizador relacionados ao DHTML.

**Por que a Scene7 está fazendo essa mudança?**

Os padrões da Web estão em constante evolução e o DHTML é uma tecnologia de desenvolvimento da Web mais antiga que está sendo rapidamente substituída pelo HTML5. A maior limitação para o DHTML como plataforma é que ele não é capaz de criar a riqueza da experiência que o HTML5 agora pode suportar de forma consistente e mais fácil entre navegadores. Por exemplo, essas limitações incluem falta de suporte entre navegadores para:

* Cursores personalizados
* Cantos arredondados
* Animações (como girar a página, diminuir o zoom)
* Efeitos (como sombras, brilho)
* Suporte completo para fontes
* Reprodução de vídeo sem plug-in

Específico à plataforma do visualizador Scene7 DHTML, a solução baseada em JSP e as APIs do Javascript não foram otimizadas para dispositivos móveis para aproveitar os recursos de multitoque e gesto. E mesmo que os visualizadores DHTML lançados em 2011/início de 2012 fossem otimizados para dispositivos móveis, eles eram difíceis de personalizar e manter devido à falta de uma estrutura de desenvolvimento flexível baseada em componentes do SDK.

Orientada por essas limitações no DHTML e pela rápida tração do setor com o HTML5 como um padrão emergente em desktops e dispositivos móveis, a Scene7 decidiu investir em uma plataforma de visualizador baseada em HTML5. Esse investimento irá oferta para nossos clientes uma plataforma robusta contra a qual eles podem criar visualizadores interativos mais ricos e envolventes, que podem atingir os usuários em várias telas, incluindo dispositivos desktop, iOS e Android.

**Como faço para saber se meu visualizador está usando a plataforma DHTML?**

Para determinar se o visualizador que sua empresa está usando é DHTML e, portanto, é afetado por essa alteração, verifique se:

1. Sua empresa está usando um visualizador Scene7 pronto para uso listado nesta tabela onde a &quot;Tecnologia do visualizador&quot; é designada como &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Sua empresa está usando um visualizador que foi criado como uma nova predefinição com base em um visualizador Scene7 pronto para uso nesta tabela, onde a &quot;Tecnologia de visualizador&quot; é designada como &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Sua empresa está usando um visualizador personalizado criado a partir da solução DHTML baseada em JSP:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. Sua empresa está usando um visualizador personalizado criado a partir da API do Javascript:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. Sua empresa está usando um visualizador personalizado criado com a API de flyout multitela DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. Sua empresa está usando um visualizador personalizado criado com a API de flyout da área de trabalho DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. Sua empresa está usando uma biblioteca de detecção de dispositivo que faz parte do pacote de visualizadores DHTML:

   Procure por JS incluindo &quot;sj_deviceDetect.js&quot; no código.

   Este foi substituído pelo novo código de detecção de dispositivo JS aqui: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**O que é a plataforma de visualização substituta?**

A substituição para DHTML é a plataforma do visualizador Scene7 HTML5, que consiste em:

* Visualizadores HTML5 prontos para uso com interações móveis otimizadas em vários tipos de visualizadores, incluindo zoom básico, zoom de deslocamento, conjuntos de imagens, conjuntos de amostras, rotação multidimensional e mídia mista. Para obter exemplos atualizados desses visualizadores, consulte: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* O SDK do visualizador HTML5, que permite a personalização abrangente de visualizadores Adobe Scene7 para sites e dispositivos compatíveis com HTML5 (como iOS e Android), proporcionando o máximo de flexibilidade e criatividade para marcar a aparência e interatividade do visualizador. A vantagem dos componentes reutilizáveis otimizados para desempenho reduz o custo geral do desenvolvimento do visualizador e acelera o desenvolvimento personalizado.

**Quando a plataforma do visualizador HTML5 terá os recursos de que preciso para transição da plataforma do visualizador DHTML?**

A Scene7 lançou o primeiro SDK do visualizador HTML5 no último trimestre de 2011 com o lançamento da versão 5.5. Desde então, adicionamos vários recursos à plataforma e estendemos o suporte para mais e mais tipos de visualizadores. Para os requisitos mais comuns do visualizador, a plataforma do visualizador HTML5 provavelmente já tem os recursos que você precisa migrar agora. E continuamos a investir agressivamente nesta plataforma de espectadores com lançamentos a cada trimestre.

Para determinar se os requisitos do visualizador podem ser atendidos hoje com a plataforma do visualizador HTML5, consulte a seguinte documentação:

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (para recursos e recursos de personalização de visualizadores prontos para uso)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (para acessar a documentação da API do SDK)

Se ainda não tiver certeza se o SDK do visualizador HTML5 atende aos seus requisitos, consulte nossa equipe de serviços profissionais.

**Como faço para transição meus visualizadores para a plataforma HTML5?**

Para transição dos visualizadores para a plataforma HTML5, a Scene7 oferta as seguintes opções:

1. Use um dos visualizadores HTML5 predefinidos da Scene7, que podem ser encontrados aqui: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. Configure um dos visualizadores HTML5 predefinidos da Scene7 na configuração do aplicativo SPS. Isso permitirá que você personalize determinados comportamentos, como tamanho do visualizador, transições, comportamento de zoom etc.: [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. Personalize a aparência dos visualizadores HTML5 predefinidos da Scene7 modificando o CSS para alterar o design visual, como arte-final de botão, posicionamento, transparência, cores de fundo, etc: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. Crie um visualizador HTML5 personalizado do zero usando o SDK que pode ser baixado aqui: [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). Você pode se envolver com serviços profissionais para criar o visualizador personalizado ou ter sua própria equipe de desenvolvimento da Web para criá-lo.

**E os navegadores que não suportam HTML5?**

O HTML5 é compatível com vários dispositivos móveis e navegadores da Web e continua a ganhar força. Atualmente, mesmo que o HTML5 não seja compatível com o Internet Explorer 8 ou posterior, a Scene7 inovou nossa plataforma de visualizador HTML5 para estender o suporte até mesmo para o IE 7 e o IE 8. Com a plataforma do visualizador Scene7 HTML5, você pode alcançar a grande maioria dos usuários de desktop e de dispositivos móveis com uma única plataforma de desenvolvimento.

Os requisitos de sistema atuais a partir do SDK HTML5 versão 2.2.1 são:

* Microsoft® Windows® XP ou posterior, Macintosh® OS X 10.6 ou posterior
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 ou posterior
* iOS 3.2.2 ou posterior
* Certificado no iPhone3 ou posterior e no iPad1 ou posterior (navegadores nativos)
* Android OS 2.2 ou posterior

Para verificar se o navegador é compatível com a plataforma do visualizador HTML5, inicie o visualizador de exemplo a seguir:

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

Se você vir a imagem ampliada passando o mouse ou arrastando o dedo sobre a imagem principal, então é um navegador/dispositivo suportado.

**Quais opções tenho se eu quiser permanecer em produção com meu visualizador DHTML existente?**

Embora você ainda possa estar em produção com visualizadores baseados em DHTML, é importante observar que não haverá aprimoramentos, correções de bugs nem atendimento ao cliente após 31 de janeiro de 2014. Dessa forma, recomendamos que todos os clientes migrem para nossa plataforma de visualizador HTML5 mais robusta. . No entanto, se sua situação comercial impedir essa migração até a data final de vida útil, você terá a opção de contrair com serviços profissionais para estender o período de tempo de manutenção suportado. Para obter mais informações, entre em contato com seu gerente de conta.

**Com quem posso entrar em contato para obter mais informações?**

Se essas Perguntas frequentes não responderem a todas as suas perguntas, [use a Admin Console para criar um caso](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) de suporte ou entre em contato com o gerente da conta do Adobe.
