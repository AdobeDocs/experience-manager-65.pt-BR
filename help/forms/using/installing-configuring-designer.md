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
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 30%

---

# Instalar e configurar o Designer{#installing-and-configuring-designer}

## Pré-requisitos {#pre-requisites}

O instalador do AEM Forms Designer requer a versão de 32 bits do [Pacote de tempo de execução redistribuível do Visual C++ 2012](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) e [Pacote de tempo de execução redistribuível do Visual C++ 2013](https://support.microsoft.com/pt-br/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Verifique se os pacotes de tempo de execução redistribuíveis mencionados anteriormente estão instalados antes de iniciar a instalação.

Você precisa de direitos de administrador para instalar ou desinstalar o Designer.

## Instalar o Designer {#install-designer}

O Designer está disponível como um instalador independente e também é fornecido com o WorkBench. Se você estiver usando um instalador independente para o Designer, execute as seguintes etapas:

1. Baixar o Designer no Adobe [Site de licenciamento](https://licensing.adobe.com/).

   >[!NOTE]
   >
   >Se você tiver uma versão anterior do Designer instalada, desinstale a versão anterior antes de continuar.

1. Inicie o instalador do Designer, clicando duas vezes em setup.exe.
1. Continue e forneça os detalhes e o número de série na tela Personalização.
1. Se você aceitar o contrato de licença, clique em Avançar para continuar.
1. (Opcional) Altere o caminho da instalação padrão, se quiser instalar o Designer e salve-o no local desejado. Clique em Avançar.
1. Para alterar as preferências, clique em Voltar. Para instalar o Designer, clique em Instalar.
1. Quando a instalação for concluída, clique em Concluir.

Como alternativa, você pode instalar o Designer por meio da linha de comando usando o modo passivo ou silencioso.

* Instalação passiva da linha de comando: O instalador exibe uma barra de progresso que indica que a instalação está em andamento, mas nenhum prompt ou mensagem de erro é exibida. Depois de iniciado, não é possível cancelar a instalação.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Instalação silenciosa da linha de comando: O instalador executa a instalação sem exibir uma interface de usuário. Não são exibidos prompts, mensagens ou caixas de diálogo. Depois de iniciado, não é possível cancelar a instalação.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```


