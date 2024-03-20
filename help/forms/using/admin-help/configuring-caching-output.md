---
title: Configuração do armazenamento em cache para saída
description: O serviço de Saída armazena em cache os designs de formulário, fragmentos e imagens. Saiba como configurar o armazenamento em cache para saída.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 0%

---

# Configuração do armazenamento em cache para saída  {#configuring-caching-for-output}

O serviço de Saída mescla dados de formulário XML com um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos.

A página Saída no console de administração contém configurações que controlam a forma como o serviço de Saída armazena itens em cache. Você pode ajustar essas configurações para otimizar o desempenho do Serviço de saída.

O Serviço de saída armazena em cache os seguintes itens:

* **designs de formulário:** O serviço de Saída armazena em cache designs de formulário que ele recupera do repositório ou de fontes HTTP. Esse armazenamento em cache melhora o desempenho porque, para solicitações de renderização subsequentes, o serviço de Saída recupera o design do formulário do cache, em vez do repositório.
* **fragmentos e imagens:** O serviço de saída pode armazenar em cache fragmentos e imagens usados em designs de formulário. Quando o serviço de saída armazena esses objetos em cache, ele melhora o desempenho, pois os fragmentos e as imagens são lidos somente no repositório na primeira solicitação.

A saída armazena o cache em dois locais:

* **na memória:** Os itens são armazenados na memória para acesso rápido. O cache de memória tem um tamanho limitado e é excluído quando você reinicia o servidor.
* **no disco:** Os itens são armazenados no sistema de arquivos do servidor. O cache de disco tem uma capacidade maior do que o cache na memória e é retido quando você reinicia o servidor. O local do cache de disco depende do servidor de aplicativos. Para obter informações sobre como alterar a localização do cache de disco, consulte [Especificar locais de arquivos para Saída](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Especificação do modo de cache {#specifying-the-cache-mode}

A saída suporta dois modos de armazenamento em cache:

* incondicional
* usando o ponto de verificação do cache

Se você alternar entre os modos de cache, reinicie o Serviço de saída para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

O tempo do ponto de verificação do cache é redefinido automaticamente quando você alterna entre os modos.

### Uso de cache incondicional {#using-unconditional-caching}

Nesse modo, quando o Serviço de saída recebe uma solicitação, ele valida os recursos (design de formulário e quaisquer ativos relacionados, como fragmentos e imagens) que são necessários. O serviço de Saída compara o carimbo de data e hora dos recursos no repositório com o carimbo de data e hora dos recursos no cache. Se o recurso no cache for mais antigo, o Serviço de saída o atualizará.

Esse modo de cache garante que os recursos mais recentes sejam usados. No entanto, o desempenho é afetado porque o Serviço de saída valida os itens em cache em relação ao repositório com cada solicitação. Esse modo de cache é adequado para ambientes de desenvolvimento e preparo em que os recursos são atualizados com frequência e o desempenho não é uma preocupação principal.

**Especificar armazenamento em cache incondicional**

1. No console de administração, clique em Serviços > saída.
1. Em Configurações do controle de cache de saída, selecione Incondicionalmente e clique em Salvar.

### Usar o ponto de verificação do cache {#use-the-cache-check-point}

Nesse modo, o Serviço de saída só verifica o repositório em busca de versões mais recentes dos recursos quando o carimbo de data e hora do recurso em cache for anterior ao horário do ponto de verificação do cache. O último tempo de ponto de verificação do cache é exibido na página Saída no Console de administração.

Use esse modo de cache em ambientes de produção de alto desempenho, nos quais o desempenho é uma preocupação e as alterações nos recursos não são frequentes. Você pode redefinir o momento do ponto de verificação do cache quando quiser implantar quaisquer alterações feitas nos recursos do repositório.

**Especificar o uso de um ponto de verificação de cache**

1. No Administration Console, clique em Serviços > saída.
1. Em Configurações do controle de cache de saída, selecione Somente se a última validação tiver sido feita antes da hora do ponto de verificação do cache e clique em Salvar.

**Redefinir o ponto de verificação do cache**

1. No console de administração, clique em Serviços > saída.
1. Em Configurações do controle de cache de saída, clique em Ponto de verificação de cache.

### Redefinir o conteúdo do cache {#reset-the-cache-contents}

Você pode limpar o conteúdo do cache a qualquer momento. Após uma redefinição de cache, a primeira solicitação para cada formulário é mais lenta porque o serviço de Saída executa uma renderização completa e cria novo conteúdo de cache.

1. No console de administração, clique em Serviços > saída.
1. Em Configurações do controle de cache de saída, clique em Redefinir cache.

## Definição das configurações de cache {#configuring-cache-settings}

Você pode especificar as configurações que o Output usa para armazenamento em cache, o que pode otimizar o desempenho do seu ambiente de formulários AEM.

Para acessar essas configurações, no console de administração, clique em Serviços > saída.

>[!NOTE]
>
>Os requisitos de disco do cache devem ser iguais ao repositório.

### Especificando configurações globais de cache {#specifying-global-cache-settings}

As configurações no **Configurações de Cache Global** afetam todos os tipos de caches. Se você alterar qualquer uma dessas configurações, reinicie o Serviço de saída para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho Máximo do Documento de Cache (KB):** O tamanho máximo, em quilobytes, de um design de formulário ou outro recurso que pode ser armazenado em qualquer cache na memória. Essa é uma configuração global que se aplica a todos os caches em memória. Se o recurso for maior que esse valor, ele não será armazenado em cache na memória. O valor padrão é 1024 quilobytes. Essa configuração não afeta o cache de disco.

**Cache de renderização do formulário habilitado:** Por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache para recuperação subsequente. Essa configuração tem pouco efeito no desempenho do Serviço de saída porque não armazena em cache documentos não interativos. Essa opção tem efeito quando você usa o Serviço de saída para documentos não interativos renderizados no cliente.

### Armazenamento em cache de designs de formulário {#caching-form-designs}

Quando o serviço de Saída recebe uma solicitação de renderização, ele recupera o design do formulário do repositório ou de uma fonte HTTP e o armazena em cache. Esse armazenamento em cache melhora o desempenho porque, para solicitações de renderização subsequentes, o serviço de Saída recupera o design do formulário do cache, em vez do repositório.

O serviço de saída sempre armazena em cache designs de formulário no disco. Se os designs de formulário forem armazenados no servidor, esses arquivos serão considerados cache de disco. O Serviço de saída também armazena em cache designs de formulário na memória, de acordo com a configuração no **Cache de Modelos na Memória** área. Se você alterar qualquer uma dessas configurações, reinicie o Serviço de saída para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do Cache de Configuração de Modelo:** O número máximo de objetos de configuração de modelo a serem mantidos na memória. O valor padrão é 100. É recomendável definir esse valor como maior ou igual ao valor Tamanho do Cache de Modelo. Essa configuração não afeta o cache de disco.

**Tamanho do Cache de Modelos:** O número máximo de objetos de conteúdo de modelo a serem mantidos na memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** Por padrão, essa caixa de seleção está marcada, o que significa que os modelos de formulário são armazenados em cache na memória. Quando essa opção não está selecionada, os modelos de formulário são armazenados em cache somente no disco.

### Armazenamento em cache de fragmentos e imagens {#caching-fragments-and-images}

O serviço de saída armazena em cache fragmentos e imagens usadas em designs de formulário no disco. Isso melhora o desempenho porque os fragmentos e as imagens são lidos somente no repositório na primeira solicitação. Em seguida, em solicitações subsequentes, o Serviço de saída lê fragmentos e imagens do cache de disco. Os fragmentos e as imagens são armazenados em cache somente no disco, e não na memória.

Você pode usar as configurações a seguir para controlar o armazenamento em cache de fragmentos e imagens no disco. Essas configurações estão no **Configurações do Cache de Recursos de Modelo** área:

**Armazenamento em cache de recursos** Selecione uma das seguintes opções na lista:

**Ativado para fragmentos e imagens:** O serviço de saída armazena fragmentos e imagens em cache. Esta é a opção padrão.

**Ativado para fragmentos:** O serviço de saída armazena fragmentos em cache, mas não imagens.

**Desabilitado:** O serviço de saída não armazena fragmentos ou imagens em cache.

**Intervalo de Limpeza (Segundos):** Especifica a frequência com que o serviço de Saída remove arquivos de cache inválidos antigos. O serviço de Saída não remove arquivos de cache válidos. Se você alterar o intervalo de limpeza, reinicie o Serviço de saída para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte Iniciar ou parar os serviços associados aos módulos de formulários AEM para obter instruções.

## Considerações de cluster para caches {#clustering-considerations-for-caches}

Em um ambiente em cluster, cada nó mantém seu próprio cache de disco e memória. O conteúdo do cache em cada nó depende de quais formulários foram renderizados nesse nó.

O local do cache deve ser idêntico (mesmo disco e caminho) em cada nó do cluster. Não coloque o cache no armazenamento compartilhado.

Se você usar a página Saída no console de administração para alterar as configurações de cache de um determinado nó, as configurações de cache de outros nós serão atualizadas quando uma solicitação for enviada para esse nó. Esse comportamento também se aplica ao botão Redefinir cache. Se você clicar no botão Redefinir cache para um nó, o cache será removido imediatamente desse nó. O cache em outros nós é limpo quando uma solicitação vai para esse nó.
