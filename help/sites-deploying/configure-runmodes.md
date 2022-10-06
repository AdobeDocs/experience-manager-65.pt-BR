---
title: Modos de execução
seo-title: Run Modes
description: Saiba como ajustar a instância do AEM para fins específicos usando modos de execução.
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# Modos de execução{#run-modes}

Os modos de execução permitem ajustar a instância do AEM para uma finalidade específica; por exemplo, criar ou publicar, testar, desenvolver, intranet ou outras.

É possível:

* [Definir coleções de parâmetros de configuração para cada modo de execução](#defining-configuration-properties-for-a-run-mode).

   Um conjunto básico de parâmetros de configuração é aplicado a todos os modos de execução. Em seguida, é possível ajustar conjuntos adicionais para a finalidade do ambiente específico. Elas são aplicadas conforme necessário.

* [Definir pacotes adicionais a serem instalados para um modo específico](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Todas as configurações e definições são armazenadas em um repositório e ativadas pela configuração da variável **Modo de execução**.

## Modos de Execução de Instalação {#installation-run-modes}

Os modos de execução de instalação (ou fixos) são usados no momento da instalação e, em seguida, corrigidos durante todo o tempo de vida da instância, não podem ser alterados.

Os modos de execução de instalação são fornecidos prontos para uso:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Trata-se de dois pares de modos de execução mutuamente exclusivos; por exemplo, é possível:

* defina uma `author` ou `publish`, não ambos ao mesmo tempo

* combinar `author` com `samplecontent` ou `nosamplecontent` (mas não ambos)

>[!CAUTION]
>
>Ao usar um dos modos de execução acima (autor, publicação, conteúdo de amostra, nosamplecontent), o valor usado no momento da instalação define o modo de execução para o *vida inteira* dessa instalação.
>
>Para esses modos de execução, você *cannot* altere-as após a instalação.

## Modos de execução personalizados {#customized-run-modes}

Você também pode criar seus próprios modos de execução personalizados. Eles podem ser combinados para cobrir cenários como:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* conforme necessário . . .

Os modos de execução personalizados também podem ser selecionados em cada inicialização.

## Uso de conteúdo de amostra e nosamplecontent {#using-samplecontent-and-nosamplecontent}

Esses modos permitem controlar o uso de conteúdo de amostra. O conteúdo da amostra é definido antes da inicialização rápida ser criada e pode incluir pacotes, configurações, etc:

* O `samplecontent` o modo de execução instalará esse conteúdo (o modo padrão).

* O `nosamplecontent` não instalará o conteúdo de amostra.

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

Consulte [Configuração do OSGi no Repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) para obter mais detalhes sobre como definir os nós de configuração individuais nessas pastas e criar configurações para combinações de vários modos de execução.

>[!NOTE]
>
>Para [Modos de Execução de Instalação](#installation-run-modes) (por exemplo, autor) o modo de execução não pode ser alterado após a instalação. No entanto, as alterações nas propriedades de configuração individuais entrarão em vigor após a reinicialização.

## Definindo pacotes adicionais a serem instalados para um modo de execução {#defining-additional-bundles-to-be-installed-for-a-run-mode}

Pacotes adicionais que devem ser instalados para um modo de execução específico também podem ser especificados. Para essas definições, as pastas de instalação são usadas para manter os pacotes. Novamente, o modo de execução é indicado por um prefixo:

* `install.author`
* `install.publish`

Essas pastas são do tipo `nt:folder` e devem conter o pacote apropriado.

## Iniciando o CQ com um modo de execução específico {#starting-cq-with-a-specific-run-mode}

Se você tiver definido configurações para vários modos de execução, precisará definir qual deve ser usada na inicialização. Existem vários métodos para especificar qual modo de execução usar; a ordem da resolução é:

1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [propriedades do sistema (](#using-a-system-property-in-the-start-script)

1. [Detecção de nome de arquivo](#filename-detection-renaming-the-jar-file)

Ao usar um servidor de aplicativos, você também pode [definir o modo de execução em web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Uso do arquivo sling.properties {#using-the-sling-properties-file}

O `sling.properties` pode ser usado para definir o modo de execução necessário:

1. Edite o arquivo de configuração:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Adicione as seguintes propriedades: o exemplo a seguir é para o autor:

   `sling.run.modes=author`

### Uso da opção -r {#using-the-r-option}

Um modo de execução personalizado pode ser ativado usando o `-r` ao iniciar o início rápido. Por exemplo, use o seguinte comando para iniciar uma instância de AEM com o modo de execução definido como dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Uso de uma propriedade do sistema no script de início {#using-a-system-property-in-the-start-script}

Uma propriedade do sistema no script de início pode ser usada para especificar o modo de execução.

* Por exemplo, use o seguinte para iniciar uma instância como uma instância de publicação de produção localizada nos EUA:

   `-Dsling.run.modes=publish,prod,us`

### Detecção de nome de arquivo - renomeação do arquivo jar {#filename-detection-renaming-the-jar-file}

Os dois modos de execução de instalação a seguir podem ser ativados renomeando o arquivo jar de instalação antes da instalação:

* publicação
* author

O arquivo jar deve usar a convenção de nomenclatura:

`cq5-<run-mode>-p<port-number>`

Por exemplo, defina a variável `publish` execute o modo nomeando o arquivo jar:

`cq5-publish-p4503`

### Definindo o modo de execução em web.xml (com o Servidor de Aplicativos) {#defining-the-run-mode-in-web-xml-with-application-server}

Ao usar um servidor de aplicativos, você também pode configurar a propriedade :

`sling.run.modes`

no arquivo :

`WEB-INF/web.xml`

Isso está no AEM `war` e deve ser atualizado antes da implantação.

Consulte [Instalar AEM com um servidor de aplicativos](/help/sites-deploying/application-server-install.md) para obter mais detalhes.
