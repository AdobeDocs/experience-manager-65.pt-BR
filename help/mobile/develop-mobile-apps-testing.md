---
title: Teste de aplicativos móveis
description: Saiba como automatizar ou testar manualmente seus aplicativos móveis usando várias ferramentas.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# Teste de aplicativos móveis{#testing-mobile-apps}

{{ue-over-mobile}}

Dada a ampla variedade de dispositivos no mercado e os dispositivos que estão sendo lançados, testar seus aplicativos se tornou imperativo. Essa é uma área em que a funcionalidade e a usabilidade podem receber avaliações baixas em uma loja de aplicativos, mas um único defeito pode resultar na desinstalação do aplicativo. Deve-se prestar muita atenção em seus planos de teste e na garantia de qualidade. O link a seguir aborda muitos dos tópicos que devem ser abordados em geral, como a identificação do ambiente, a definição de casos de teste, os tipos de testes, as suposições e o envolvimento do cliente. Também são discutidas ferramentas para ajudar no esforço de teste. Ferramentas internas, como [Hobbes](/help/sites-developing/hobbes.md), podem ajudar em testes de interface do usuário baseados na Web. [Dia Difícil](/help/sites-developing/tough-day.md) pode sobrecarregar suas instâncias com uma carga simulada. Se o ambiente de testes já tiver experiência com ferramentas de terceiros, como o Selenium, elas também poderão ser usadas.

Ao desenvolver um aplicativo móvel, há muitas novas preocupações específicas para dispositivos que precisam ser abordadas juntamente com as de testes tradicionais.

* Funcional: todos os requisitos são atendidos pelo seu aplicativo?
* Usabilidade - O aplicativo é fácil de usar e entender pelo seu cliente?
* Desempenho - o que acontece durante um pico de uso? Os elementos do aplicativo, como toques e carrosséis, são rápidos e não prejudicam a experiência?
* Falha ou interrupções: o que acontece quando há uma chamada ou notificação recebida enquanto o aplicativo está em execução? O que acontece se houver uma interrupção ou desligamento da rede?
* Instalação e atualizações - Como está a experiência de instalação? Como as atualizações são enviadas?
* Técnico: seu aplicativo está consumindo muita energia de um dispositivo?
* Localização — todas as áreas do aplicativo são traduzidas?
* Certificação - Seu aplicativo foi certificado? Os clientes podem confiar que ela segue todos os requisitos legais de privacidade de dados?

Essas perguntas devem ser respondidas durante os testes automatizados e manuais.

## Teste automatizado {#automated-testing}

Deve-se realizar algum grau de teste automático para abranger a variedade de tamanhos de tela, restrições de memória, métodos de entrada e sistemas operacionais. Ele não apenas cobre muitos dos casos de teste, como também pode acelerar os testes de regressão quando novos recursos ou dispositivos são introduzidos. Idealmente, suas ferramentas de automação devem reduzir ou limitar a duplicação de esforços. Use ferramentas ou estruturas para que seu esforço de teste seja aplicável em todas as plataformas. O gráfico a seguir mostra uma estrutura simplificada de um ambiente de teste para testes de interface do usuário com base na Web e testes de aplicativos móveis. O lado esquerdo do gráfico mostra uma série de nós Selenium com navegadores. O SeleniumGrid pode criar testes comuns de interface do usuário com base na Web para qualquer um desses nós. O hub do Selenium também pode se conectar ao Appium para testes de aplicativos em várias plataformas. Somente mostrados são simuladores, mas você pode incorporar utilitários adb, para Android™ e Xcode para dispositivos iOS. Os links são fornecidos posteriormente neste documento, onde você pode encontrar detalhes específicos para as ferramentas mencionadas.

![chlimage_1](assets/chlimage_1.jpeg)

## Teste manual {#manual-testing}

Além do teste automático, seu aplicativo deve passar por um ciclo de teste manual. Os clientes que executam o aplicativo em um dispositivo real não podem ser duplicados por um script. Aqui você também tem muitas opções. Você pode usar uma plataforma, como o HockeyApp, para definir quem tem acesso e coletar feedback. Ou você pode terceirizar todo o processo para um serviço como UTest, ElusiveStars ou Testin. Se você tiver um grupo de testadores internos, mas não tiver variação de dispositivos, há serviços em nuvem nos quais você pode executar testes manuais no pool de dispositivos. Um desses serviços que fornece isso é o SauceLabs. Você também pode criar aplicativos remotamente para o PhoneGap Enterprise e instalá-los em dispositivos locais como um nível de teste de aceitação ou demonstração. Consulte o site PhoneGap (`https://phonegap.com/`) para obter os recursos e a documentação mais recentes. Qualquer que seja a abordagem, o teste manual deve fazer o seguinte:

* atingir um grande alvo de testadores,
* testar contra um grande pool de dispositivos (idealmente dispositivos reais, mas simuladores/emuladores se dispositivos reais não estiverem disponíveis),
* forneça feedback informativo:

   * relatórios de falhas,
   * analytics/tracking,
   * usabilidade,
   * áreas de atenção,
   * desempenho,
   * consumo de dados/energia etc.

## Ferramentas {#tools}

Há uma grande variedade de ferramentas disponíveis para testar aplicativos móveis. A escolha das opções a serem usadas deve ser baseada em sua situação específica: recursos, preço, suporte, cobertura e assim por diante. Veja a seguir apenas uma pequena descrição de algumas ferramentas e serviços disponíveis.

**Selenium**

* Estrutura que inclui uma API para scripts de teste para alimentar WebDriver e controlar vários navegadores.
* Você pode usar isso com o Appium para testar em dispositivos reais.
* O SeleniumGrid direciona testes entre nós para testes paralelos.
* O Selenium IDE ajuda a reduzir a gravação do caso de teste.

Para obter mais informações, consulte [https://www.selenium.dev/](https://www.selenium.dev/).

**Testdroid**

* Um serviço de testes baseado em nuvem com ganchos de integração contínua e testes de dispositivos reais.
* Está incluído um rastreador de aplicativos que verifica a compatibilidade do dispositivo, analisa registros, percorre visualizações, captura de tela e monitora o desempenho.

Para obter mais informações, consulte [https://testdroid.com/](https://testdroid.com/).

**Appium**

* O Appium é uma estrutura popular entre plataformas para automatizar testes móveis.
* Além disso, um inspetor é incluído com habilidades de registro para ajudar a codificar casos de teste.

Para obter mais informações, consulte [https://appium.io/](https://appium.io/).

**LaboratóriosMolho**

* O SauceLabs fornece testes baseados em nuvem e integra-se com integração contínua.
* Os testes são executados automaticamente no ambiente de nuvem, ou você pode iniciar um dispositivo ou plataforma específica e executar testes manuais para ajudar a depurar problemas.

Para obter mais informações, consulte [https://saucelabs.com/](https://saucelabs.com/).

<!-- **AppTestNow**

* An outsourcing service that tests your mobile apps.
* Included is a large pool of devices and offers a wide range of types of testing: performance, quality, functional, certification, localization, data consumption, and so on.

For more information, see [https://apptestnow.com/](https://apptestnow.com/). -->

**HockeyApp**

* O HockeyApp se enquadra no teste manual, em que o aplicativo móvel é enviado para uma loja de aplicativos pessoal, onde os testadores podem baixar e experimentar.

Para obter mais informações, consulte [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Embora não seja uma ferramenta de teste, o Jenkins é uma estrutura de integração contínua que fornece a espinha dorsal para testes automatizados. Vários plug-ins de terceiros estão disponíveis para estender a funcionalidade. Um exemplo, o plug-in SeleniumGrid fornece uma interface para ajudar a gerenciar o hub e os nós do Selenium.

Para obter mais informações, consulte [https://www.jenkins.io/](https://www.jenkins.io/) e [https://plugins.jenkins.io/](https://plugins.jenkins.io/).
