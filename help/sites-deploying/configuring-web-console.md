---
title: Console da Web
seo-title: Web Console
description: Saiba como usar o console da Web no AEM.
seo-description: Learn how to use the web console in AEM.
uuid: 047274ff-4d7d-4c7d-95be-06f363beae2e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: f934eb02-1f84-44f2-9f14-3f17250c9a90
exl-id: bdfeaf85-e832-40c1-8769-7d027cdb021e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 2%

---

# Console da Web{#web-console}

O console da Web no AEM é baseado no [Console de Gerenciamento da Web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). O Apache Felix é um esforço da comunidade para implementar a Plataforma de Serviço OSGi R4, que inclui a estrutura OSGi e os serviços padrão.

>[!NOTE]
>
>No console da Web, qualquer descrição que mencione as configurações padrão está relacionada aos padrões do Sling.
>
>AEM tem seus próprios padrões e, portanto, os padrões definidos podem ser diferentes daqueles documentados no console.

O console da Web oferece uma seleção de guias para manter os pacotes OSGi, incluindo:

* [Configuração](#configuration): usado para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar AEM parâmetros do sistema
* [Pacotes](#bundles): usado para instalar pacotes
* [Componentes](#components): usado para controlar o status dos componentes necessários para o AEM

Todas as alterações feitas são aplicadas imediatamente ao sistema em execução. Não é necessário reiniciar.

O console pode ser acessado de `../system/console`; por exemplo:

`http://localhost:4502/system/console/components`

## Configuração {#configuration}

O **Configuração** A guia é usada para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar AEM parâmetros do sistema.

>[!NOTE]
>
>Consulte [Configuração do OSGi com o console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) para obter mais detalhes.

O **Configuração** Essa guia pode ser acessada por:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/configMgr`

Uma lista de configurações será exibida:

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

Há dois tipos de configurações disponíveis nas listas suspensas nesta tela:

* **Configurações**

   Permite atualizar as configurações existentes. Eles têm uma Identidade Persistente (PID) e podem ser:

   * Norma e integral em AEM; são obrigatórios, se excluídos, os valores retornam às configurações padrão.
   * instâncias criadas a partir de configurações de fábrica; essas instâncias são criadas pelo usuário, a exclusão remove a instância .

* **Configurações de fábrica**

   Permite criar uma instância do objeto de funcionalidade necessário.

   Isso receberá uma Identidade Persistente, listada na lista suspensa Configurações .

Selecionar qualquer entrada nas listas exibirá os parâmetros relacionados a essa configuração:

![chlimage_1-61](assets/chlimage_1-61.png)

Em seguida, você pode atualizar os parâmetros conforme necessário e:

* **Salvar**

   Salve as alterações feitas.

   Para uma Configuração de fábrica, isso criará uma nova instância com uma Identidade Persistente. A nova instância será listada em Configurações.

* **Redefinir**

   Redefina os parâmetros mostrados na tela para os que foram salvos por último.

* **Excluir**

   Exclua a configuração atual. Se padrão, os parâmetros são retornados às configurações padrão. Se criada a partir de uma configuração de fábrica, a instância específica será excluída.

* **Desvincular**

   Desvincule a configuração atual do pacote.

* **Cancelar**

   Cancelar quaisquer alterações atuais.

## Pacotes {#bundles}

O **Pacotes** é o mecanismo para instalar os pacotes OSGi necessários para o AEM. A guia pode ser acessada por um dos métodos a seguir:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/bundles`

Uma lista de pacotes será mostrada:

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

Com essa guia, é possível:

* **Instalar ou atualizar**

   Você pode **Procurar** para localizar o arquivo que contém seu pacote e especificar se ele deve **Iniciar** imediatamente e em que **Nível inicial**.

* **Recarregar**

   Atualiza a lista exibida.

* **Atualizar pacotes**

   Isso verificará as referências de todos os pacotes e atualizará conforme necessário.

   Por exemplo, após uma atualização, a versão antiga e a nova ainda podem estar em execução devido a referências anteriores. Essa opção marcará e moverá todas as referências para a nova versão, permitindo que a versão antiga pare.

* **Início**

   Inicia um pacote de acordo com o nível inicial especificado.

* **Parar**

   Interrompe o pacote.

* **Desinstalar**

   Desinstala o pacote do sistema.

* **consulte o status**

   A lista especifica o status atual do pacote; clicar no nome de um pacote específico com mostrar mais informações.

>[!NOTE]
>
>Depois **Atualizar** é recomendável executar uma **Atualizar pacotes**.

## Componentes {#components}

O **Componentes** permite ativar e/ou desativar os vários componentes. Ele pode ser acessado por:

* O menu suspenso:

   **Principal >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/components`

Uma lista de componentes será exibida. Vários ícones estão disponíveis para habilitar, desabilitar ou (quando apropriado) abrir detalhes de configuração de um componente específico.

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

Clicar no nome de um componente específico exibirá mais informações sobre seu status. Aqui você também pode ativar, desativar ou recarregar o componente.

![chlimage_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>Habilitar ou desabilitar um componente só será aplicado até que AEM/CRX seja reiniciado.
>
>O estado inicial é definido no descritor do componente, que é gerado durante o desenvolvimento e armazenado no pacote no momento da criação do pacote.
