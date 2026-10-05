---
title: Habilitar conversões de arquivos com vários threads
description: Saiba como habilitar conversões de arquivos com vários threads.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%
---
# Habilitar conversões de arquivos com vários threads {#enabling-multi-threaded-file-conversions}

O PDF Generator pode executar várias conversões de arquivos simultaneamente para melhorar a taxa de transferência da conversão. Escolha o modo de conversão aplicável:

| Modo de conversão | Aplicativos que oferecem suporte a conversões simultâneas | Modelo de conta de usuário |
|---|---|---|
| Modo multiusuário | OpenOffice | Uma conta de usuário separada executa cada instância do OpenOffice. |
| Modo de usuário único | Microsoft® Word e Microsoft® Excel | Uma conta de usuário executa várias instâncias do Word e Excel. As conversões do PowerPoint permanecem serializadas. |

Antes de habilitar qualquer um dos modos, conclua a [configuração de pré-instalação do PDF Generator](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations) para os aplicativos e o sistema operacional que você usa. Para obter as versões do aplicativo com suporte, consulte [Suporte de software para PDF Generator](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator).

## Modo multiusuário {#multi-user-mode}

No modo multiusuário, o PDF Generator inicia cada instância do OpenOffice em uma conta de usuário separada. Configure contas de usuário administrativo válidas o suficiente para o número de conversões simultâneas de que você precisa. Em um cluster, configure as mesmas contas em cada nó.

No Windows, verifique se os usuários do PDF Generator têm o [privilégio Substituir um token de nível de processo](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege) e conclua a configuração de Controle de Conta de Usuário aplicável descrita em [Configurar Serviços de Documento](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac).

### Conversões do OpenOffice {#openoffice-conversions}

Configure uma conta de usuário do PDF Generator para cada instância do OpenOffice que possa ser executada simultaneamente. Instale o OpenOffice em um local que cada usuário configurado possa acessar e descarte as caixas de diálogo de ativação iniciais do OpenOffice para cada usuário.

Para sistemas baseados em UNIX, conclua a instalação do OpenOffice e os requisitos de permissão do usuário em [Configurar Serviços de Documento](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations).

## Modo de usuário único no Windows {#single-user-mode-on-windows}

O modo de usuário único permite que o PDF Generator execute conversões simultâneas em uma conta de usuário configurada.

Nesse modo, várias instâncias do Microsoft® Word (DOC e DOCX) e do Excel (XLS e XLSX) são executadas no mesmo usuário. O Microsoft® PowerPoint (PPT e PPTX) não suporta o modo de usuário único. O PDF Generator inicia somente uma instância do PowerPoint por vez, portanto, as conversões do PowerPoint são serializadas.

Para ativar o modo de usuário único para conversões do Word e Excel:

1. No console de administração, navegue até **Início > Serviços > Aplicativos e Serviços > Gerenciamento de Serviços**.
1. Filtre por **PDF Generator** e selecione **GeneratePDFService**.
1. Na guia **Configuração**, configure as seguintes opções:

   * Defina **Habilitar Modo de Usuário Único para PDFMaker** como **true**.
   * Defina **Tamanho do Pool do PDFMaker** para o número máximo de instâncias do Word que podem executar conversões simultaneamente.
   * Defina **Habilitar Modo de Usuário Único para Native2PDF** como **true**.
   * Defina **Tamanho do Pool do Native2PDF** para o número máximo de instâncias do Excel que podem executar conversões simultaneamente.

1. Reinicie o servidor do AEM Forms.
