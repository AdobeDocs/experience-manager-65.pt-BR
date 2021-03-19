---
title: Modos de execução
seo-title: Modos de execução
description: Saiba como ajustar a instância do AEM para fins específicos usando modos de execução.
seo-description: Saiba como ajustar a instância do AEM para fins específicos usando modos de execução.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuração
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---


# Modos de execução{#run-modes}

Os modos de execução permitem ajustar a instância do AEM para uma finalidade específica; por exemplo, criar ou publicar, testar, desenvolver, intranet ou outras.

É possível:

* [Defina coleções de parâmetros de configuração para cada modo](#defining-configuration-properties-for-a-run-mode) de execução.

   Um conjunto básico de parâmetros de configuração é aplicado a todos os modos de execução. Em seguida, é possível ajustar conjuntos adicionais para a finalidade do ambiente específico. Elas são aplicadas conforme necessário.

* [Defina pacotes adicionais a serem instalados para um modo](#defining-additional-bundles-to-be-installed-for-a-run-mode) específico.

Todas as configurações e definições são armazenadas em um repositório e ativadas ao configurar o **Modo de Execução**.

## Modos de execução da instalação {#installation-run-modes}

Os modos de execução de instalação (ou fixos) são usados no momento da instalação e, em seguida, corrigidos durante todo o tempo de vida da instância, não podem ser alterados.

Os modos de execução de instalação são fornecidos prontos para uso:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Trata-se de dois pares de modos de execução mutuamente exclusivos; por exemplo, é possível:

* defina `author` ou `publish`, não ambos ao mesmo tempo

* combinar `author` com `samplecontent` ou `nosamplecontent` (mas não ambos)

>[!CAUTION]
>
>Ao usar um dos modos de execução acima (autor, publicação, conteúdo de amostra, nosamplecontent), o valor usado no tempo de instalação define o modo de execução para o *lifetime inteiro* dessa instalação.
>
>Para esses modos de execução, você *não pode* alterá-los após a instalação.

## Modos de execução personalizados {#customized-run-modes}

Você também pode criar seus próprios modos de execução personalizados. Eles podem ser combinados para cobrir cenários como:

* `author` + `development`

* `publish` +  `test`

* `publish` + `test` + `golive`

* `publish` +  `intranet`

* conforme necessário . . .

Os modos de execução personalizados também podem ser selecionados em cada inicialização.

## Uso de conteúdo de amostra e nosamplecontent {#using-samplecontent-and-nosamplecontent}

Esses modos permitem controlar o uso de conteúdo de amostra. O conteúdo da amostra é definido antes da inicialização rápida ser criada e pode incluir pacotes, configurações, etc:

* O modo de execução `samplecontent` instalará esse conteúdo (o modo padrão).

* O modo `nosamplecontent` não instalará o conteúdo da amostra.

O modo de execução nosamplecontent foi projetado para instalações de produção.

## Definição das propriedades de configuração para um modo de execução {#defining-configuration-properties-for-a-run-mode}

Uma coleção de valores para propriedades de configuração, usada para um modo de execução específico, pode ser salva no repositório.

O modo de execução é indicado por um sufixo no nome da pasta. Isso permite armazenar todas as configurações em um repositório como. Por exemplo:

* `config`

   Aplicável a todos os modos de execução

* `config.author`

   Usado para o modo de execução do autor

* `config.publish`

   Usado para publicar modo de execução

* `config.<run-mode>`

   Utilizado para o modo de execução aplicável; por exemplo, config

Consulte [Configuração do OSGi no Repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) para obter mais detalhes sobre como definir os nós de configuração individuais nessas pastas e para criar configurações para combinações de vários modos de execução.

>[!NOTE]
>
>Para [Modos de Execução de Instalação](#installation-run-modes) (por exemplo, autor), o modo de execução não pode ser alterado após a instalação. No entanto, as alterações nas propriedades de configuração individuais entrarão em vigor após a reinicialização.

## Definindo pacotes adicionais a serem instalados para um modo de execução {#defining-additional-bundles-to-be-installed-for-a-run-mode}

Pacotes adicionais que devem ser instalados para um modo de execução específico também podem ser especificados. Para essas definições, as pastas de instalação são usadas para manter os pacotes. Novamente, o modo de execução é indicado por um prefixo:

* `install.author`
* `install.publish`

Essas pastas são do tipo `nt:folder` e devem conter o pacote apropriado.

## Iniciando o CQ com um modo de execução específico {#starting-cq-with-a-specific-run-mode}

Se você tiver definido configurações para vários modos de execução, precisará definir qual deve ser usada na inicialização. Existem vários métodos para especificar qual modo de execução usar; a ordem da resolução é:

1. [ `sling.properties` arquivo](#using-the-sling-properties-file)
1. [ `-r` opção](#using-the-r-option)
1. [propriedades do sistema (`-D`)](#using-a-system-property-in-the-start-script)

1. [Detecção de nome de arquivo](#filename-detection-renaming-the-jar-file)

Ao usar um servidor de aplicativos, você também pode [definir o modo de execução em web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Uso do arquivo sling.properties {#using-the-sling-properties-file}

O arquivo `sling.properties` pode ser usado para definir o modo de execução necessário:

1. Edite o arquivo de configuração:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Adicione as seguintes propriedades: o exemplo a seguir é para o autor:

   `sling.run.modes=author`

### Uso da opção -r {#using-the-r-option}

Um modo de execução personalizado pode ser ativado usando a opção `-r` ao iniciar o início rápido. Por exemplo, use o seguinte comando para iniciar uma instância de AEM com o modo de execução definido como dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Uso de uma propriedade do sistema no script de início {#using-a-system-property-in-the-start-script}

Uma propriedade do sistema no script de início pode ser usada para especificar o modo de execução.

* Por exemplo, use o seguinte para iniciar uma instância como uma instância de publicação de produção localizada nos EUA:

   `-Dsling.run.modes=publish,prod,us`

### Detecção de nome de arquivo - renomeando o arquivo jar {#filename-detection-renaming-the-jar-file}

Os dois modos de execução de instalação a seguir podem ser ativados renomeando o arquivo jar de instalação antes da instalação:

* publicação
* author

O arquivo jar deve usar a convenção de nomenclatura:

`cq5-<run-mode>-p<port-number>`

Por exemplo, defina o modo de execução `publish` nomeando o arquivo jar:

`cq5-publish-p4503`

### Definindo o modo de execução em web.xml (com Servidor de Aplicativos) {#defining-the-run-mode-in-web-xml-with-application-server}

Ao usar um servidor de aplicativos, você também pode configurar a propriedade :

`sling.run.modes`

no arquivo :

`WEB-INF/web.xml`

Isso está no arquivo AEM `war` e deve ser atualizado antes da implantação.

Consulte [Instalando AEM com um Servidor de Aplicativos](/help/sites-deploying/application-server-install.md) para obter mais detalhes.
