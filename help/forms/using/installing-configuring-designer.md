---
title: Instalação e configuração do Designer
description: O Designer está disponível como um instalador independente e também é fornecido com o Workbench. Saiba como instalar o Designer independente.
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin, User, Developer
feature: Forms Designer,Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 8f14518117b3aff1cdb2e033fbfe40d0a903d53f
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Instalação e configuração do Designer{#installing-and-configuring-designer}

## Pré-requisitos {#pre-requisites}

+++ Para AEM Forms Designer de 64 bits (Recomendado)

* Instale a versão de 64 bits do [Visual C++ 2019 Redistributable (x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). Verifique se os pacotes de tempo de execução redistribuíveis mencionados anteriormente estão instalados antes de iniciar a instalação.
* Um usuário com direitos de administrador para instalar ou desinstalar o AEM Forms Designer.
* O sistema que executa o AEM Forms Designer de 64 bits deve ter o OpenSSL3 instalado, especificamente a biblioteca compartilhada `libcrypto-3-x64.dll`.\
  Esta biblioteca é necessária para que o AEM Designer funcione corretamente e calcule o **SHAHash**.

+++

+++ Para AEM Forms Designer de 32 bits

* Instale a versão de 32 bits do [Visual C++ 2019 Redistributable (x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). Verifique se os pacotes de tempo de execução redistribuíveis mencionados anteriormente estão instalados antes de iniciar a instalação.
* Um usuário com direitos de administrador para instalar ou desinstalar o AEM Forms Designer.

+++

>[!NOTE]
>
>* A versão de 64 bits do designer foi introduzida com o AEM 6.5 Forms Service Pack 19 (6.5.19.0).
>* A versão de 32 bits do designer está obsoleta desde o lançamento do [AEM Forms Service Pack 21 (6.5.21.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).
> * As plataformas compatíveis com o Forms Designer estão alinhadas às plataformas compatíveis com o AEM Forms. Para saber mais sobre as plataformas compatíveis com o Forms Designer, [clique aqui](/help/forms/using/aem-forms-jee-supported-platforms.md).

Para obter mais informações sobre a instalação do Forms Designer, visite [Perguntas frequentes](#fandq).

## Instalar o AEM Forms Designer {#install-designer}

O Designer está disponível como um instalador independente e também é fornecido com o WorkBench. Se você estiver usando um instalador independente do AEM Forms Designer, execute as seguintes etapas:

1. Desinstale a versão anterior do AEM Forms Designer, se ela já estiver instalada.
1. Baixe o AEM Forms Designer de 64 bits (recomendado) ou o AEM Forms Designer de 32 bits com base em seus requisitos.

   >[!NOTE]
   > 
   >* O Forms Designer de 32 bits foi agendado para ser descontinuado na versão AEM 6.5 Forms Service Packs 20 (6.5.20.0). A Adobe recomenda atualizar para o Forms Designer de 64 bits.
   >* O Forms Designer de 64 bits está disponível somente para o AEM 6.5 Forms Service Packs 19 (6.5.19.0) ou versões posteriores.
   >* A versão Adobe Experience Manager 6.5 do Forms Service Pack 15 (6.5.15.0) em diante do Forms Designer também inclui a versão do Service Pack. Por exemplo, para o Service Pack 15, o número da versão é 6.5.15.20221112.1.0. Neste exemplo, a 6.5.15 é a versão do service pack.

1. Inicie o instalador do AEM Forms Designer clicando duas vezes em setup.exe.
1. Continue e forneça seus detalhes e o número de série na tela do Personalization.

   >[!NOTE]
   >
   >* Obtenha sua chave de licença do Forms Designer no [site de licenciamento da Adobe](https://licensing.adobe.com/).

1. Se você aceitar o contrato de licença, clique em Avançar para continuar.
1. (Opcional) altere o caminho de instalação padrão, se desejar instalar o Designer no local de sua escolha. Clique em Avançar.
1. Clique em Voltar para alterar as preferências. Para instalar o Designer, clique em Instalar.
1. Quando a instalação for concluída, clique em Concluir.

Como alternativa, você pode instalar o AEM Forms Designer por meio da linha de comando, usando o modo passivo ou silencioso.

* Instalação passiva por linha de comando: o instalador exibe uma barra de progresso indicando que a instalação está em andamento, mas nenhum prompt ou mensagem de erro é exibido. Depois de iniciada, não é possível cancelar a instalação.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Instalação silenciosa da linha de comando: o instalador executa a instalação sem exibir uma interface do usuário. Nenhuma solicitação, mensagem ou caixa de diálogo é exibida. Depois de iniciada, não é possível cancelar a instalação.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## Atualizar o AEM Forms Designer {#update-forms-designer}

Há dois casos ao atualizar a versão mais recente do AEM Forms Designer 6.5.16.0:

* **Caso 1**: quando o usuário tem uma versão do AEM Forms Designer anterior à 6.5.15.0.
* **Caso 2**: quando o usuário tem a versão 6.5.15.0 do AEM Forms Designer.

+++**Quando o usuário tiver uma versão do AEM Forms Designer anterior a 6.5.15.0.**

Se você estiver usando um instalador independente do AEM Forms Designer, execute as seguintes etapas:

1. Antes de instalar o **AEM Forms Designer6.5.16.0**, os usuários devem desinstalar todas as versões anteriores.
1. Baixe e instale o [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) da Página de Versões do AEM Form.
1. Após a instalação bem-sucedida do **AEM Forms Designer6.5.15.0**, baixe e instale o [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) clicando duas vezes no arquivo do instalador baixado.

+++

+++**Quando o usuário tem 6.5.15.0 AEM Forms Designer versão**

Se você estiver usando um instalador independente do AEM Forms Designer, execute as seguintes etapas:
1. Baixe a versão mais recente do AEM Forms Designer no [Portal de distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Instale a versão mais recente do AEM Forms Designer clicando duas vezes no arquivo do instalador baixado.

+++

## Perguntas frequentes {#fandq}

* **Um usuário pode atualizar ou instalar diretamente o designer de 64 bits?**
   * Sim, os usuários podem atualizar ou instalar diretamente o designer de 64 bits. Para atualizar, instale o instalador completo do designer do [SP19](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/Designer-Patch/sp19_x64/aemforms_designer_6_5_0_wwe_win.zip) e aplique a versão subsequente do patch do designer sobre ele.

     >[!NOTE]
     > Antes de atualizar para o designer de 64 bits, desinstale primeiro o designer de 32 bits, se ele existir.

* **Os usuários podem manter tanto os de 32 bits quanto os de 64 bits instalados em seus sistemas?**
   * Não, as instalações de 32 e 64 bits não funcionarão na mesma máquina. O usuário pode ter um designer de 32 bits ou um designer de 64 bits.

* **Como verificar se um usuário está em um designer de 64 bits ou de 32 bits?**
   * Há duas maneiras de verificar a versão do Forms Designer:

      1. Abra o Designer, vá para Ajuda, clique em Sobre o designer e você verá as informações da versão do designer junto com as informações de bits. Por exemplo, você verá que 64 bits é gravado no final da versão, como mostrado aqui:
         `6.5.21.20240522.1.161 | 64 bit`
      1. Abra o Designer. No canto superior esquerdo, você verá um ícone de marca contendo informações de 64 bits com o nome do produto.

