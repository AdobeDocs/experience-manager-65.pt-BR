---
title: Teste de aplicativos móveis
seo-title: Testing Mobile Apps
description: Teste de aplicativos móveis
seo-description: null
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: 17d13e9b201629d9d1519fde4740cf651fe89d2c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Teste de aplicativos móveis{#testing-mobile-apps}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Dada a ampla variedade de dispositivos no mercado e os dispositivos que estão sendo lançados, testar seus aplicativos se tornou extremamente importante. Essa é uma área em que a funcionalidade e a usabilidade podem receber avaliações baixas em uma loja de aplicativos, mas um único defeito pode resultar na desinstalação do aplicativo. Deve-se prestar muita atenção em seus planos de teste e no controle de qualidade. O link a seguir aborda muitos dos tópicos que precisam ser abordados em geral, como identificar seu ambiente, definir casos de teste, tipos de testes, suposições, envolvimento do cliente etc. Também são discutidas ferramentas para ajudar no esforço de teste. Ferramentas internas, como [Hobbes](/help/sites-developing/hobbes.md)O pode ajudar com testes de interface do usuário baseados na Web. [Dia difícil](/help/sites-developing/tough-day.md) O pode sobrecarregar suas instâncias com uma carga simulada. Se o ambiente de testes já tiver experiência com ferramentas de terceiros, como o Selenium, elas também poderão ser usadas.

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

Deve-se realizar algum grau de teste automático para abranger a variedade de tamanhos de tela, restrições de memória, métodos de entrada e sistemas operacionais. Ele não apenas cobre grande parte dos casos de teste, como também pode acelerar os testes de regressão quando novos recursos ou dispositivos são introduzidos. Idealmente, suas ferramentas de automação devem reduzir ou limitar a duplicação de esforços. Use ferramentas ou estruturas para que seu esforço de teste seja aplicável em todas as plataformas. O gráfico a seguir mostra uma estrutura simplificada de um ambiente de teste para testes de interface do usuário com base na Web e testes de aplicativos móveis. O lado esquerdo do gráfico mostra uma série de nós Selenium com navegadores. O SeleniumGrid pode criar testes comuns de interface do usuário com base na Web para qualquer um desses nós. O hub do Selenium também pode se conectar ao Appium para testes de aplicativos em várias plataformas. Somente mostrados são simuladores, mas você pode incorporar utilitários adb, para Android e Xcode para dispositivos iOS. Os links são fornecidos posteriormente neste documento, onde você pode encontrar detalhes específicos para as ferramentas mencionadas.

![chlimage_1](assets/chlimage_1.jpeg)

## Teste manual {#manual-testing}

Além do teste automático, seu aplicativo deve passar por um ciclo de teste manual. Os clientes que executam o aplicativo em um dispositivo real não podem ser duplicados por um script. Aqui você também tem muitas opções. Você pode usar uma plataforma, como o HockeyApp, para definir quem tem acesso e coletar feedback. Ou você pode terceirizar todo o processo para um serviço como UTest, ElusiveStars ou Testin. Se você tiver um grupo de testadores internos, mas não tiver variação de dispositivos, há serviços em nuvem nos quais você pode executar testes manuais no pool de dispositivos. Um desses serviços que fornece isso é o SauceLabs. Você também pode criar aplicativos remotamente para o PhoneGap Enterprise e instalá-los em dispositivos locais como um nível de teste de aceitação ou demonstração. Consulte o PhoneGap (`https://phonegap.com/`) para obter os recursos e a documentação mais recentes. Qualquer que seja a abordagem, os testes manuais devem ser realizados;

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

Há uma grande variedade de ferramentas disponíveis para testar aplicativos móveis. A escolha de opções a serem usadas será baseada em sua situação específica: recursos, preço, suporte, cobertura etc. Veja a seguir apenas uma pequena descrição de algumas ferramentas e serviços disponíveis.

**Selênio**

* Estrutura que inclui uma API para scripts de teste para alimentar WebDriver e controlar vários navegadores.
* Você pode usar isso em conjunto com o Appium para testar em dispositivos reais.
* O SeleniumGrid direciona testes entre nós para testes paralelos.
* O Selenium IDE ajuda a reduzir a gravação do caso de teste.

Para obter mais informações, consulte [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Um serviço de testes baseado em nuvem com ganchos de integração contínua e testes de dispositivos reais.
* Inclui um rastreador de aplicativos que verifica a compatibilidade do dispositivo, analisa logs, percorre visualizações, captura de tela e monitora o desempenho.

Para obter mais informações, consulte [https://testdroid.com/](https://testdroid.com/).

**Appium**

* O Appium é uma estrutura popular entre plataformas para automatizar testes móveis.
* Além disso, um inspetor é incluído com habilidades de registro para ajudar a codificar casos de teste.

Para obter mais informações, consulte [https://appium.io/](https://appium.io/).

**MolhoLabs**

* O SauceLabs fornece testes baseados em nuvem e integra-se com integração contínua.
* Os testes são executados automaticamente no ambiente de nuvem, ou você pode iniciar um dispositivo ou plataforma específica e executar testes manuais para ajudar a depurar problemas.

Para obter mais informações, consulte [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Um serviço de terceirização que testará seus aplicativos móveis.
* Inclui um grande pool de dispositivos e oferece uma ampla variedade de tipos de testes: desempenho, qualidade, funcional, certificação, localização, consumo de dados etc.

Para obter mais informações, consulte [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeyApp**

* O HockeyApp se enquadra no teste manual, em que o aplicativo móvel é enviado para uma loja de aplicativos pessoal, onde os testadores podem baixar e experimentar.

Para obter mais informações, consulte [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Embora não seja uma ferramenta de teste, o Jenkins é uma estrutura de integração contínua que fornece a espinha dorsal para testes automatizados. Vários plug-ins de terceiros estão disponíveis para estender a funcionalidade. Um exemplo, o plug-in SeleniumGrid fornece uma interface para ajudar a gerenciar o hub e os nós do Selenium.

Para obter mais informações, consulte [https://jenkins-ci.org/](https://jenkins-ci.org/) e [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
