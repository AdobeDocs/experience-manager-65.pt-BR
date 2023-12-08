---
title: Problemas de conexão com os serviços de saída, Forms e (documento de registro) DoR
description: Resolva os erros de conexão do AEM Forms após o SP19. Pare, instale o Microsoft Visual C++ e reinicie o servidor para obter uma solução perfeita. Solução de problemas de serviços Output, Forms, DoR.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
source-git-commit: cf5da092fabbc7834108dc54d65eb97e160984ce
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# Não é possível usar os serviços de Saída, Forms ou DoR (Documento de Registro) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problema

Após instalar o AEM Forms 6.5 Service Pack 19, tentar usar o serviço de Saída, o serviço Forms ou o serviço do Documento de registro (DoR) pode resultar em uma `Connection to failed service` erro.

## Solução

Para resolver o problema:

1. Pare sua instância do Forms do AEM 6.5.
1. Baixe e instale o [Versão de 64 bits dos pacotes redistribuíveis do Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) no computador em que o AEM 6.5 Forms está instalado.
1. Reinicie o servidor do AEM Forms.


>[!NOTE]
>
>
> Certifique-se de instalar o Redistribuível, mesmo se uma versão anterior estiver instalada.
