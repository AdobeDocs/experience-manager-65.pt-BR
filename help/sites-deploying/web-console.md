---
title: Console da Web
seo-title: Console da Web
description: Saiba como usar o console da Web AEM.
seo-description: Saiba como usar o console da Web AEM.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 2%

---


# Console da Web{#web-console}

O console da Web no AEM é baseado no [Console de gerenciamento da Web do Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). O Apache Felix é um esforço comunitário para implementar a Plataforma de serviço OSGi R4, que inclui a estrutura OSGi e os serviços padrão.

>[!NOTE]
>
>No console da Web, qualquer descrição que mencione as configurações padrão está relacionada aos padrões do Sling.
>
>AEM tem seus próprios padrões e, portanto, os padrões definidos podem ser diferentes dos documentados no console.

O console da Web oferta uma seleção de guias para manter os pacotes OSGi, incluindo:

* [Configuração](#configuration): usado para configurar os pacotes OSGi, sendo, portanto, o mecanismo subjacente para configurar AEM parâmetros do sistema
* [Pacotes](#bundles): usado para instalar pacotes
* [Componentes](#components): usado para controlar o status dos componentes necessários para AEM

Quaisquer alterações feitas são aplicadas imediatamente ao sistema em execução. Não é necessário reiniciar.

O console pode ser acessado de `../system/console`; por exemplo:

`http://localhost:4502/system/console/components`

## Configuração {#configuration}

A guia **Configuration** é usada para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar AEM parâmetros do sistema.

>[!NOTE]
>
>Consulte [Configuração OSGi com o Console Web](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes.

A guia **Configuração** pode ser acessada por:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/configMgr`

Uma lista de configurações será mostrada:

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Há dois tipos de configurações disponíveis nas listas suspensas nesta tela:

* ****
ConfiguraçõesPermite atualizar as configurações existentes. Eles têm uma Identidade Persistente (PID) e podem ser:

   * Norma e integral para AEM; esses valores são obrigatórios, se excluídos, retornam às configurações padrão.
   * instâncias criadas a partir de Configurações de fábrica; essas instâncias são criadas pelo usuário, a exclusão remove a instância.

* **Configurações de fábrica**
Permite criar uma instância do objeto de funcionalidade necessário.

   Isso receberá uma Identidade persistente, listada na lista suspensa Configurações.

Selecionar qualquer entrada do lista exibirá os parâmetros relacionados a essa configuração:

![chlimage_1-29](assets/chlimage_1-21a.png)

Em seguida, você pode atualizar os parâmetros conforme necessário e:

* **Salvar**

   Salve as alterações feitas.

   Para uma configuração de fábrica, isso criará uma nova instância com uma identidade persistente. A nova instância será listada em Configurações.

* **Redefinir**

   Redefina os parâmetros mostrados na tela para os salvos por último.

* **Excluir**

   Exclua a configuração atual. Se padrão, os parâmetros são retornados para as configurações padrão. Se for criada a partir de uma configuração de fábrica, a instância específica será excluída.

* **Desvincular**

   Desvincule a configuração atual do pacote.

* **Cancelar**

   Cancele quaisquer alterações atuais.

## Pacotes {#bundles}

A guia **Pacotes** é o mecanismo de instalação dos pacotes OSGi necessários para AEM. A guia pode ser acessada por um dos seguintes métodos:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/bundles`

Uma lista de pacotes será mostrada:

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

Usando essa guia, é possível:

* **Instalar ou atualizar**

   Você pode **Procurar** para localizar o arquivo que contém seu pacote e especificar se ele deve **Start** imediatamente e em que **Nível de Start**.

* **Recarregar**

   Atualiza a lista exibida.

* **Atualizar pacotes**

   Isso verificará as referências de todos os pacotes e atualizará conforme necessário.

   Por exemplo, após uma atualização, a versão antiga e a nova ainda podem estar em execução devido a referências anteriores. Essa opção verificará e moverá todas as referências para a nova versão, permitindo que a versão antiga pare.

* **Início**

   Start um pacote de acordo com o nível de start especificado.

* **Parar**

   Pára o pacote.

* **Desinstalar**

   Desinstala o pacote do sistema.

* **ver o status**

   A lista especifica o status atual do pacote; clique no nome de um pacote específico para mostrar mais informações.

>[!NOTE]
>
>Depois de **Atualizar**, é recomendável executar **Atualizar Pacotes**.

## Componentes {#components}

A guia **Components** permite ativar e/ou desativar os vários componentes. Ele pode ser acessado por:

* O menu suspenso:

   **Principal >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/components`

Uma lista de componentes será exibida. Vários ícones estão disponíveis para permitir que você ative, desative ou (quando apropriado) abra os detalhes de configuração de um componente específico.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Clicar no nome de um componente específico exibirá mais informações sobre seu status. Aqui você também pode ativar, desativar ou recarregar o componente.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>Habilitar ou desabilitar um componente só será aplicado até que o AEM/CRX seja reiniciado.
>
>O estado do start é definido no descritor do componente, que é gerado durante o desenvolvimento e armazenado no pacote no momento da criação do pacote.

