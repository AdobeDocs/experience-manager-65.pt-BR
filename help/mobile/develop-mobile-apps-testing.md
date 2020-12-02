---
title: Testar aplicativos móveis
seo-title: Testar aplicativos móveis
description: 'null'
seo-description: nulo
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---


# Testar aplicativos móveis{#testing-mobile-apps}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Dada a grande variedade de dispositivos no mercado e dispositivos sendo lançados, testar seus aplicativos se tornou extremamente importante. Essa é uma área em que a funcionalidade e a usabilidade podem ganhar baixas revisões em uma app store, mas um único defeito pode resultar na desinstalação do aplicativo. É necessário prestar especial atenção aos seus planos de testes e à garantia da qualidade. O link a seguir aborda muitos dos tópicos que precisam ser abordados em geral, como identificar seu ambiente, definir casos de teste, tipos de testes, pressuposições, envolvimento do cliente etc. Também são discutidas ferramentas para ajudar no esforço de teste. Ferramentas internas, como [Hobbes](/help/sites-developing/hobbes.md), podem ajudar com testes de interface de usuário baseados na Web. [Duro ](/help/sites-developing/tough-day.md) Daycan enfatize suas instâncias com uma carga simulada. Se seu ambiente de teste já tiver experiência com ferramentas de terceiros, como Selenium, elas também podem ser usadas.

Ao desenvolver um aplicativo para dispositivos móveis, há muitas preocupações novas específicas aos dispositivos que precisam ser abordadas junto com os de testes tradicionais.

* Funcional - Todos os requisitos são atendidos pelo seu aplicativo?
* Usabilidade - o aplicativo é fácil de usar e entender pelo seu cliente?
* Desempenho - O que acontece durante um pico no uso? Os elementos do aplicativo, como deslizes e carrosséis, são rápidos e não diminuem a experiência?
* Falha ou interrupções - o que acontece quando há uma chamada ou notificação recebida enquanto o aplicativo está sendo executado? O que acontece se houver uma interrupção ou desligamento da rede?
* Instalação e atualizações - Como está a experiência de instalação? Como as atualizações são removidas?
* Técnica - seu aplicativo está consumindo muita energia de um dispositivo?
* Localização - Todas as áreas no aplicativo são traduzidas?
* Certificação - seu aplicativo foi certificado? Os clientes podem confiar que ele segue todos os requisitos legais de privacidade de dados?

Essas perguntas devem ser respondidas durante os testes automatizados e manuais.

## Teste automatizado {#automated-testing}

Alguns graus de teste automatizado devem ser executados para abranger a variedade de tamanhos de tela, restrições de memória, métodos de entrada e sistemas operacionais. Não só abrange grande parte dos casos de teste, como também pode acelerar o teste de regressão quando novos recursos ou dispositivos forem introduzidos. O ideal é que suas ferramentas de automação reduzam ou limitem a duplicação de esforços. Use ferramentas ou estruturas para que seu esforço de teste seja aplicável em todas as plataformas. O gráfico a seguir mostra uma estrutura simplificada de um ambiente de teste para testes de interface de usuário com base na Web e testes de aplicativo móvel. O lado esquerdo do gráfico mostra uma série de nós Selenium com navegadores. A SeleniumGrid pode gerar testes comuns de interface de usuário com base na Web para qualquer um desses nós. O hub Selenium também pode se conectar ao Appium para testes de aplicativos em várias plataformas. Somente são exibidos os simuladores, mas você pode incorporar os utilitários adb, Android e Xcode para dispositivos iOS. Os links são fornecidos posteriormente neste documento, onde você pode encontrar detalhes específicos para as ferramentas mencionadas.

![chlimage_1](assets/chlimage_1.jpeg)

## Teste manual {#manual-testing}

Além dos testes automatizados, seu aplicativo deve passar por um ciclo de testes manuais. Os clientes que executam o aplicativo em um dispositivo real não podem ser duplicados por um script. Aqui também, você tem muitas opções. Você pode usar uma plataforma, como HóqueiApp, para definir quem tem acesso e coletar feedback. Ou você pode terceirizar todo o processo para um serviço como UTest, ElusiveStars ou Testin. Se você tiver um grupo de testadores internos, mas não houver variação de dispositivos, há serviços em nuvem nos quais você pode executar testes manuais no pool de dispositivos. Um desses serviços que fornece isso é o SauceLabs. Você também pode criar aplicativos remotamente para o PhoneGap Enterprise e instalá-los em dispositivos locais como um nível de teste de aceitação ou demonstração. Consulte o site [PhoneGap](https://phonegap.com/) para obter os recursos e a documentação mais recentes. Seja qual for a abordagem, os ensaios manuais devem ser efetuados;

* atingir um grande público alvo de testadores.
* testar em relação a um grande conjunto de dispositivos (idealmente dispositivos reais, mas simuladores/emuladores se não existirem dispositivos reais),
* fornecer feedback informativo:

   * relatórios de falha,
   * análise/acompanhamento,
   * utilização,
   * áreas de atenção,
   * desempenho,
   * consumo de dados/energia, etc.

## Ferramentas {#tools}

Há uma grande variedade de ferramentas disponíveis para testar aplicativos móveis. A escolha dos que serão usados será baseada na sua situação específica: recursos, preço, suporte, cobertura etc. A seguir está apenas uma pequena descrição de algumas das ferramentas e serviços disponíveis.

**Selênio**

* Estrutura que inclui uma API para scripts de teste para alimentar WebDriver e controlar vários navegadores.
* Você pode usar isso junto com o Appium para testar em dispositivos reais.
* SeleniumGrid direciona testes em nós para testes paralelos.
* O Selenium IDE ajuda a reduzir a escrita de casos de teste.

Para obter mais informações, consulte [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Um serviço de teste baseado em nuvem com ganchos de integração contínuos e teste de dispositivo real.
* Inclui um App Crawler que verifica a compatibilidade do dispositivo, analisa registros, atravessa visualizações, captura de tela e monitora o desempenho.

Para obter mais informações, consulte [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium é uma popular estrutura entre plataformas para automação de testes móveis.
* Além disso, um inspetor está incluído com habilidades de registro para ajudar a codificar casos de teste.

Para obter mais informações, consulte [https://appium.io/](https://appium.io/).

**SauceLabs**

* O SauceLabs fornece testes baseados em nuvem e integra-se à integração contínua.
* Os testes são executados automaticamente no ambiente em nuvem ou você pode start um dispositivo ou plataforma específica e executar testes manuais para ajudar a depurar problemas.

Para obter mais informações, consulte [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Um serviço de terceirização que testará seus aplicativos móveis.
* Inclui um grande conjunto de dispositivos e oferta de uma grande variedade de tipos de testes: desempenho, qualidade, funcionalidade, certificação, localização, consumo de dados, etc.

Para obter mais informações, consulte [https://www.apptestnow.com](https://www.apptestnow.com/).

**HóqueiApp**

* O HóqueiApp se enquadra no teste manual onde o aplicativo móvel é enviado para uma loja de aplicativos pessoal onde os testadores podem baixar e experimentar.

Para obter mais informações, consulte [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Embora não seja uma ferramenta de teste, Jenkins é uma estrutura de integração contínua que fornece a espinha dorsal para testes automatizados. Vários plug-ins de terceiros estão disponíveis para estender a funcionalidade. Por exemplo, o plug-in SeleniumGrid fornece uma interface do usuário para ajudar a gerenciar o hub e os nós Selenium.

Para obter mais informações, consulte [https://jenkins-ci.org/](https://jenkins-ci.org/) e [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
