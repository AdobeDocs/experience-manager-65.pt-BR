---
title: Console da Web no AEM
description: Saiba como usar o console da Web no AEM.
uuid: 047274ff-4d7d-4c7d-95be-06f363beae2e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: f934eb02-1f84-44f2-9f14-3f17250c9a90
exl-id: bdfeaf85-e832-40c1-8769-7d027cdb021e
source-git-commit: a17b25e55a0bf16a0df42a7ba4768503618a19e2
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# Console da Web{#web-console}

O console da Web no AEM (Adobe Experience Manager) é baseado na variável [Console de gerenciamento Web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). O Apache Felix é um esforço da comunidade para implementar a Plataforma de serviço OSGi R4, que inclui a estrutura OSGi e os serviços padrão.

>[!NOTE]
>
>No console da Web, todas as descrições que mencionam as configurações padrão estão relacionadas aos padrões do Sling.
>
>O AEM tem seus próprios padrões, portanto, os padrões definidos podem ser diferentes daqueles documentados no console.

O console da Web oferece uma seleção de guias para manter os pacotes OSGi, incluindo:

* [Configuração](#configuration): usado para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar parâmetros do sistema AEM
* [Pacotes](#bundles): usado para instalar pacotes
* [Componentes](#components): usado para controlar o status dos componentes necessários para o AEM

Quaisquer alterações feitas são aplicadas imediatamente ao sistema em execução. Não é necessário reiniciar.

O console pode ser acessado de `../system/console`; por exemplo:

`http://localhost:4502/system/console/components`

## Configuração {#configuration}

A variável **Configuração** é usada para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar os parâmetros do sistema AEM.

>[!NOTE]
>
>Consulte [Configuração do OSGi com o console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) para obter mais detalhes.

A variável **Configuração** A guia pode ser acessada das seguintes maneiras:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/configMgr`

Uma lista de configurações será exibida:

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

Há dois tipos de configurações disponíveis nas listas suspensas desta tela:

* **Configurações**

   Permite atualizar as configurações existentes. Eles têm uma Identidade persistente (PID) e podem ser:

   * padrão e integral para AEM; são necessários, se excluídos, os valores retornam às configurações padrão.
   * instâncias criadas em Configurações de fábrica; essas instâncias são criadas pelo usuário, a exclusão remove a instância.

* **Configurações de fábrica**

   Permite criar uma instância do objeto de funcionalidade necessário.

   Isso receberá uma Identidade persistente e será listado na lista suspensa Configurações.

Selecionar qualquer entrada nas listas exibirá os parâmetros relacionados a essa configuração:

![chlimage_1-61](assets/chlimage_1-61.png)

Em seguida, você pode atualizar os parâmetros conforme necessário e:

* **Salvar**

   Salve as alterações feitas.

   Para uma Configuração de fábrica, isso criará uma nova instância com uma Identidade persistente. A nova instância será listada em Configurações.

* **Redefinir**

   Reinicializa os parâmetros mostrados na tela para os que foram salvos por último.

* **Excluir**

   Exclua a configuração atual. Se for padrão, os parâmetros são retornados às configurações padrão. Se criada a partir de uma Configuração de fábrica, a instância específica é excluída.

* **Desvincular**

   Desvincular a configuração atual do pacote.

* **Cancelar**

   Cancelar as alterações atuais.

## Pacotes {#bundles}

A variável **Pacotes** é o mecanismo para instalar os pacotes OSGi necessários para o AEM. A guia pode ser acessada por um dos seguintes métodos:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/bundles`

Uma lista de pacotes será exibida:

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

Usando essa guia, você pode:

* **Instalar ou atualizar**

   Você pode **Procurar** para localizar o arquivo que contém o pacote e especificar se ele deve **Início** imediatamente e em que **Nível inicial**.

* **Recarregar**

   Atualiza a lista exibida.

* **Atualizar pacotes**

   Isso verificará as referências de todos os pacotes e atualizará conforme necessário.

   Por exemplo, após uma atualização, a versão antiga e a nova ainda podem estar em execução devido a referências anteriores. Essa opção verificará e moverá todas as referências para a nova versão, permitindo que a versão antiga seja interrompida.

* **Início**

   Inicia um pacote de acordo com o nível inicial especificado.

* **Parar**

   Para o pacote.

* **Desinstalar**

   Desinstala o pacote do sistema.

* **ver o status**

   A lista especifica o status atual do pacote; clicando no nome de um pacote específico com informações adicionais.

>[!NOTE]
>
>Depois **Atualizar** é recomendável executar um **Atualizar pacotes**.

## Componentes {#components}

A variável **Componentes** permite Ativar e/ou Desativar os vários componentes. Ele pode ser acessado das seguintes maneiras:

* O menu suspenso:

   **Principal >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/components`

Uma lista de componentes será exibida. Vários ícones estão disponíveis para permitir que você ative, desative ou (quando apropriado) abra os detalhes de configuração de um componente específico.

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

Clicar no nome de um componente específico exibirá mais informações sobre o status. Aqui você também pode ativar, desativar ou recarregar o componente.

![chlimage_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>Ativar ou desativar um componente só será aplicado até que o AEM/CRX seja reiniciado.
>
>O estado inicial é definido no descritor do componente, que é gerado durante o desenvolvimento e armazenado no pacote no momento da criação do pacote.
