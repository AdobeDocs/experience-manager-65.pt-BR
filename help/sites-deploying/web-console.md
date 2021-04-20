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
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---


# Console da Web{#web-console}

O console da Web no AEM é baseado no [Apache Felix Web Management Console](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). O Apache Felix é um esforço da comunidade para implementar a Plataforma de Serviço OSGi R4, que inclui a estrutura OSGi e os serviços padrão.

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

A guia **Configuration** é usada para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar AEM parâmetros do sistema.

>[!NOTE]
>
>Consulte [Configuração OSGi com o Console da Web](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes.

A guia **Configuration** pode ser acessada por:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/configMgr`

Uma lista de configurações será exibida:

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Há dois tipos de configurações disponíveis nas listas suspensas nesta tela:

* ****
ConfiguraçõesPermite atualizar as configurações existentes. Eles têm uma Identidade Persistente (PID) e podem ser:

   * Norma e integral em AEM; são obrigatórios, se excluídos, os valores retornam às configurações padrão.
   * instâncias criadas a partir de configurações de fábrica; essas instâncias são criadas pelo usuário, a exclusão remove a instância .

* **Fatory**
ConfigurationsPermite criar uma instância do objeto de funcionalidade necessário.

   Isso receberá uma Identidade Persistente, listada na lista suspensa Configurações .

Selecionar qualquer entrada nas listas exibirá os parâmetros relacionados a essa configuração:

![chlimage_1-21](assets/chlimage_1-21a.png)

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

A guia **Bundles** é o mecanismo para instalar os pacotes OSGi necessários para o AEM. A guia pode ser acessada por um dos métodos a seguir:

* O menu suspenso:

   **OSGi >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/bundles`

Uma lista de pacotes será mostrada:

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

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
>Após **Atualizar**, é recomendável executar **Atualizar Pacotes**.

## Componentes {#components}

A guia **Components** permite habilitar e/ou desabilitar os vários componentes. Ele pode ser acessado por:

* O menu suspenso:

   **Principal >**

* O URL; por exemplo:

   `http://localhost:4502/system/console/components`

Uma lista de componentes será exibida. Vários ícones estão disponíveis para habilitar, desabilitar ou (quando apropriado) abrir detalhes de configuração de um componente específico.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Clicar no nome de um componente específico exibirá mais informações sobre seu status. Aqui você também pode ativar, desativar ou recarregar o componente.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>Habilitar ou desabilitar um componente só será aplicado até que AEM/CRX seja reiniciado.
>
>O estado inicial é definido no descritor do componente, que é gerado durante o desenvolvimento e armazenado no pacote no momento da criação do pacote.

