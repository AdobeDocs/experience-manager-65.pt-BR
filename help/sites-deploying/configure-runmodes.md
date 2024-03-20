---
title: Modos de execução
description: Saiba como ajustar a instância do AEM para fins específicos usando modos de execução.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# Modos de execução{#run-modes}

Os modos de execução permitem ajustar a instância do AEM para um propósito específico; por exemplo, criar ou publicar, testar, desenvolver, intranet ou outros.

É possível:

* [Definir coleções de parâmetros de configuração para cada modo de execução](#defining-configuration-properties-for-a-run-mode).

  Um conjunto básico de parâmetros de configuração é aplicado a todos os modos de execução, e você pode ajustar conjuntos adicionais para a finalidade de seu ambiente específico. Elas são aplicadas conforme necessário.

* [Definir pacotes adicionais a serem instalados para um modo específico](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Todas as configurações e definições são armazenadas em um repositório e ativadas configurando o **Modo de execução**.

## Modos de execução da instalação {#installation-run-modes}

Os modos de execução de instalação (ou fixos) são usados no momento da instalação e, em seguida, corrigidos durante todo o tempo de vida da instância, eles não podem ser alterados.

Os modos de execução da instalação são fornecidos prontos para uso:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Esses são dois pares de modos de execução mutuamente exclusivos; por exemplo, você pode:

* defina `author` ou `publish`, não ambos ao mesmo tempo

* combinar `author` com um `samplecontent` ou `nosamplecontent` (mas não ambos)

>[!CAUTION]
>
>Ao usar um dos modos de execução acima (author, publish, samplecontent, nosamplecontent), o valor usado no momento da instalação define o modo de execução da *vida inteira* dessa instalação.
>
>Para esses modos de execução, você *não é possível* altere-os após a instalação.

## Modos de execução personalizados {#customized-run-modes}

Você também pode criar seus próprios modos de execução personalizados. Eles podem ser combinados para abranger cenários como:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* conforme necessário. . .

Os modos de execução personalizados também podem ser selecionados em cada inicialização.

## Uso de samplecontent e nosamplecontent {#using-samplecontent-and-nosamplecontent}

Esses modos permitem controlar o uso de conteúdo de amostra. O conteúdo de amostra é definido antes que o início rápido seja criado e pode incluir pacotes, configurações e assim por diante:

* A variável `samplecontent` modo de execução instala esse conteúdo (o modo padrão).

* A variável `nosamplecontent` não instala o conteúdo de amostra.

O modo de execução nosamplecontent foi projetado para instalações de produção.

## Definição das propriedades de configuração de um modo de execução {#defining-configuration-properties-for-a-run-mode}

Uma coleção de valores para propriedades de configuração, usada para um modo de execução específico, pode ser salva no repositório.

O modo de execução é indicado por um sufixo no nome da pasta. Isso permite armazenar todas as configurações em um repositório como. Por exemplo:

* `config`

  Aplicável a todos os modos de execução

* `config.author`

  Usado para o modo de execução do autor

* `config.publish`

  Usado para o modo de execução de publicação

* `config.<run-mode>`

  Usado para o modo de execução aplicável; por exemplo, config

Consulte [Configuração do OSGi no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) para obter mais detalhes sobre como definir os nós de configuração individuais nessas pastas e criar configurações para combinações de vários modos de execução.

>[!NOTE]
>
>Para [Modos de execução da instalação](#installation-run-modes) (por exemplo, autor) o modo de execução não pode ser alterado após a instalação. No entanto, as alterações nas propriedades de configuração individuais entrarão em vigor na reinicialização.

## Definição de pacotes adicionais a serem instalados para um modo de execução {#defining-additional-bundles-to-be-installed-for-a-run-mode}

Pacotes adicionais que devem ser instalados para um modo de execução específico também podem ser especificados. Para essas definições, as pastas de instalação são usadas para armazenar os pacotes. Novamente, o modo de execução é indicado por um prefixo:

* `install.author`
* `install.publish`

Essas pastas são do tipo `nt:folder` e devem conter o pacote apropriado.

## Início do CQ com um modo de execução específico {#starting-cq-with-a-specific-run-mode}

Se você tiver definido as configurações para vários modos de execução, será necessário definir qual será usado na inicialização. Existem vários métodos para especificar qual modo de execução usar; a ordem da resolução é:

1. [propriedades do sistema (](#using-a-system-property-in-the-start-script)
1. [](#using-the-sling-properties-file)
1. [](#using-the-r-option)
1. [Detecção de nome de arquivo](#filename-detection-renaming-the-jar-file)

Quando estiver usando um servidor de aplicativos, você também poderá [definir o modo de execução em web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Uso do arquivo sling.properties {#using-the-sling-properties-file}

A variável `sling.properties` arquivo pode ser usado para definir o modo de execução necessário:

1. Edite o arquivo de configuração:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Adicione as seguintes propriedades; o exemplo a seguir é para autor:

   `sling.run.modes=author`

### Uso da opção -r {#using-the-r-option}

Um modo de execução personalizado pode ser ativado usando o `-r` ao iniciar o início rápido. Por exemplo, use o seguinte comando para iniciar uma instância do AEM com o modo de execução definido como dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Usando uma propriedade do sistema no script de inicialização {#using-a-system-property-in-the-start-script}

Uma propriedade do sistema no script de inicialização pode ser usada para especificar o modo de execução.

* Por exemplo, use o seguinte para iniciar uma instância como uma instância de publicação de produção nos EUA:

  `-Dsling.run.modes=publish,prod,us`

### Detecção de nome de arquivo - renomeando o arquivo jar {#filename-detection-renaming-the-jar-file}

Os dois modos de execução de instalação a seguir podem ser ativados renomeando o arquivo jar de instalação antes da instalação:

* publicação
* autor

O arquivo jar deve usar a convenção de nomenclatura:

`cq5-<run-mode>-p<port-number>`

Por exemplo, defina a variável `publish` executar nomeando o arquivo jar:

`cq5-publish-p4503`

### Definindo o modo de execução em web.xml (com Servidor de Aplicações) {#defining-the-run-mode-in-web-xml-with-application-server}

Quando estiver usando um servidor de aplicativos, você também poderá configurar a propriedade:

`sling.run.modes`

no arquivo:

`WEB-INF/web.xml`

Isto é no AEM `war` arquivo e deve ser atualizado antes da implantação.

Consulte [Instalar o AEM com um servidor de aplicativos](/help/sites-deploying/application-server-install.md) para obter mais detalhes.
