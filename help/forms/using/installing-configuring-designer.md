---
title: Instalar e configurar o Designer
seo-title: Installing and configuring Designer
description: O Designer está disponível como um instalador independente e também é fornecido com o Workbench. Saiba como instalar o Designer independente.
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 1b2d743f8f2172c4e4663917d598734cb1ea1ea4
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 14%

---

# Instalar e configurar o Designer{#installing-and-configuring-designer}

## Pré-requisitos {#pre-requisites}

* Instalar versão de 32 bits do  [Visual C++ 2019 Redistribuível (x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). Verifique se os pacotes de tempo de execução redistribuíveis mencionados anteriormente estão instalados antes de iniciar a instalação.
* Um usuário com direitos de administrador para instalar ou desinstalar o AEM Forms Designer.

## Instalar o AEM Forms Designer {#install-designer}

O Designer está disponível como um instalador independente e também é fornecido com o WorkBench. Se você estiver usando um instalador independente do AEM Forms Designer, execute as seguintes etapas:

1. Desinstale a versão anterior do AEM Forms Designer, se ela já estiver instalada.
1. Baixar Designer de [Site de licenciamento do Adobe](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * O Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0) em diante versão Forms Designer também inclui a versão Service Pack. Por exemplo, para o Service Pack 15, o número da versão é 6.5.15.20221112.1.0. Neste exemplo, a 6.5.15 é a versão do service pack.


1. Inicie o instalador do AEM Forms Designer clicando duas vezes em setup.exe.
1. Continue e forneça os detalhes e o número de série na tela Personalização.
1. Se você aceitar o contrato de licença, clique em Avançar para continuar.
1. (Opcional) Altere o caminho da instalação padrão, se quiser instalar o Designer e salve-o no local desejado. Clique em Avançar.
1. Para alterar as preferências, clique em Voltar. Para instalar o Designer, clique em Instalar.
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

* **Caso 1**: quando o usuário tiver a versão do AEM Forms Designer anterior à 6.5.15.0.
* **Caso 2**: Quando o usuário tiver a versão 6.5.15.0 do AEM Forms Designer.

+++**Quando o usuário tiver a versão do AEM Forms Designer anterior à 6.5.15.0.**

Se você estiver usando um instalador independente do AEM Forms Designer, execute as seguintes etapas:

1. Antes de instalar **AEM Forms Designer 6.5.16.0**, os usuários devem desinstalar todas as versões anteriores.
1. Baixar e instalar [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) na página Versões do formulário AEM.
1. Após a instalação bem-sucedida do **AEM Forms Designer 6.5.15.0**, baixar e instalar [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) clicando duas vezes no arquivo do instalador baixado.

+++

+++**Quando o usuário tem a versão 6.5.15.0 do AEM Forms Designer**

Se você estiver usando um instalador independente do AEM Forms Designer, execute as seguintes etapas:
1. Baixe a versão mais recente do AEM Forms Designer no [Portal de distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Instale a versão mais recente do AEM Forms Designer clicando duas vezes no arquivo do instalador baixado.

+++