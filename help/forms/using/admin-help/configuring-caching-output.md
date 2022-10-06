---
title: Configuração do armazenamento em cache para saída
seo-title: Configuring caching for Output
description: O serviço de saída armazena em cache os designs de formulário, fragmentos e imagens. Saiba como configurar o armazenamento em cache para saída.
seo-description: The Output service caches the form designs, fragments and images. Learn how to configure the caching for output.
uuid: 00bffeb5-c9c4-4a46-98b5-e14ec9f4514e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5398abd-f62c-485d-9f4b-a316c0de2b6b
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---

# Configuração do armazenamento em cache para saída  {#configuring-caching-for-output}

O serviço de saída mescla dados de formulário XML com um design de formulário criado no Designer para criar um fluxo de saída de documento em vários formatos.

A página Saída no console de administração contém configurações que controlam a maneira como o serviço de Saída armazena itens em cache. Você pode ajustar essas configurações para otimizar o desempenho do serviço de Saída.

O serviço de saída armazena em cache os seguintes itens:

* **designs de formulário:** O serviço de saída armazena em cache designs de formulário que ele recupera do repositório ou de fontes HTTP. Esse armazenamento em cache melhora o desempenho, pois para solicitações de renderização subsequentes, o serviço de Saída recupera o design de formulário do cache em vez de do repositório.
* **fragmentos e imagens:** O serviço de saída pode armazenar em cache fragmentos e imagens usados em designs de formulário. Quando o serviço de saída armazena esses objetos em cache, ele melhora o desempenho, pois os fragmentos e imagens são lidos somente do repositório na primeira solicitação.

A saída armazena o cache em dois locais:

* **na memória:** Os itens são armazenados na memória para acesso rápido. O cache na memória tem um tamanho limitado e é excluído ao reiniciar o servidor.
* **no disco:** Os itens são armazenados no sistema de arquivos do servidor. O cache de disco tem uma capacidade maior do que o cache na memória e ele é retido quando você reinicia o servidor. A localização do cache de disco depende do servidor de aplicativos. Para obter informações sobre como alterar o local do cache de disco, consulte [Especificar locais de arquivo para saída](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Especificação do modo de cache {#specifying-the-cache-mode}

A saída suporta dois modos de armazenamento em cache:

* incondicional
* uso do ponto de verificação do cache

Se você alternar entre os modos de cache, reinicie o serviço de Saída para que a alteração entre em vigor. Para reiniciar este serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

A hora do ponto de verificação do cache é redefinida automaticamente quando você alternar entre modos.

### Uso do armazenamento em cache incondicional {#using-unconditional-caching}

Nesse modo, quando o serviço de Saída recebe uma solicitação, ele valida os recursos (design de formulário e quaisquer ativos relacionados, como fragmentos e imagens) necessários. O serviço de saída compara o carimbo de data e hora dos recursos no repositório ao carimbo de data e hora dos recursos no cache. Se o recurso no cache for mais antigo, o serviço de saída o atualizará.

Esse modo de cache garante que os recursos mais recentes sejam usados. No entanto, o desempenho é afetado porque o serviço de saída valida os itens em cache em relação ao repositório com cada solicitação. Esse modo de cache é adequado para ambientes de desenvolvimento e de preparo, onde os recursos são atualizados com frequência e o desempenho não é uma preocupação principal.

**Especificar cache incondicional**

1. No console de administração, clique em Serviços > saída.
1. Em Configurações de Controle de Cache de Saída, selecione Incondicionalmente e clique em Salvar.

### Usar o ponto de verificação do cache {#use-the-cache-check-point}

Nesse modo, o serviço de Saída só verifica o repositório por versões mais recentes dos recursos quando o carimbo de data e hora do recurso em cache for mais antigo que o tempo do ponto de verificação do cache. O último tempo do ponto de verificação do cache é exibido na página Saída no Console de Administração.

Use esse modo de cache em ambientes de produção de alto desempenho, onde o desempenho é uma preocupação e as alterações nos recursos são pouco frequentes. Você pode redefinir o tempo do ponto de verificação do cache quando quiser implantar qualquer alteração feita nos recursos do repositório.

**Especificar o uso de um ponto de verificação de cache**

1. No Console de administração, clique em Serviços > na saída.
1. Em Configurações de Controle do Cache de Saída, selecione Somente se a última validação foi feita antes do tempo do ponto de verificação do cache e clique em Salvar.

**Redefinir o ponto de verificação do cache**

1. No console de administração, clique em Serviços > saída.
1. Em Configurações de Controle de Cache de Saída, clique em Ponto de Verificação de Cache.

### Redefinir o conteúdo do cache {#reset-the-cache-contents}

Você pode limpar o conteúdo do cache a qualquer momento. Após uma redefinição de cache, a primeira solicitação para cada formulário é mais lenta porque o serviço de saída executa uma renderização completa e cria novo conteúdo de cache.

1. No console de administração, clique em Serviços > saída.
1. Em Configurações de Controle de Cache de Saída, clique em Redefinir Cache.

## Definição das configurações de cache {#configuring-cache-settings}

Você pode especificar as configurações que o Output usa para armazenamento em cache, o que pode otimizar o desempenho do seu ambiente de formulários AEM.

Para acessar essas configurações, no console de administração, clique em Services > output.

>[!NOTE]
>
>Os requisitos de disco para o cache devem ser iguais ao repositório.

### Especificação das configurações de cache global {#specifying-global-cache-settings}

As configurações no **Configurações de Cache Global** afetam todos os tipos de caches. Se você alterar qualquer uma dessas configurações, reinicie o Serviço de saída para que a alteração entre em vigor. Para reiniciar este serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho máximo do documento do cache (KB):** O tamanho máximo, em quilobytes, de um design de formulário ou de outro recurso que pode ser armazenado em qualquer cache na memória. Esta é uma configuração global que se aplica a todos os caches em memória. Se o recurso for maior que esse valor, ele não será armazenado em cache na memória. O valor padrão é 1024 kilobytes. Essa configuração não afeta o cache de disco.

**Cache de renderização de formulário ativado:** Por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache para recuperação subsequente. Essa configuração tem pouco efeito no desempenho do serviço de saída, pois não armazena em cache documentos não interativos. Essa opção tem efeito quando você usa o serviço Saída para documentos não interativos renderizados no cliente.

### Armazenamento de designs de formulário em cache {#caching-form-designs}

Quando o serviço de saída recebe uma solicitação de renderização, ele recupera o design de formulário do repositório ou de uma fonte HTTP e o armazena em cache. Esse armazenamento em cache melhora o desempenho, pois para solicitações de renderização subsequentes, o serviço de Saída recupera o design de formulário do cache em vez de do repositório.

O serviço de saída sempre armazena em cache designs de formulário em disco. Se os designs de formulário forem armazenados no servidor, esses arquivos serão considerados o cache de disco. O serviço de saída também armazena em cache designs de formulário na memória, de acordo com a configuração no **No Cache do Modelo de Memória** área. Se você alterar qualquer uma dessas configurações, reinicie o Serviço de saída para que a alteração entre em vigor. Para reiniciar este serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do Cache de Configuração do Modelo:** O número máximo de objetos de configuração de modelo a serem mantidos na memória. O valor padrão é 100. É recomendável definir esse valor maior ou igual ao valor Tamanho do Cache do Modelo. Essa configuração não afeta o cache de disco.

**Tamanho do Cache do Modelo:** O número máximo de objetos de conteúdo de modelo a serem mantidos na memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** Por padrão, essa caixa de seleção é selecionada, o que significa que os modelos de formulário são armazenados em cache na memória. Quando essa opção não está selecionada, os modelos de formulário são armazenados em cache somente no disco.

### Armazenamento em cache de fragmentos e imagens {#caching-fragments-and-images}

O serviço de saída armazena em cache fragmentos e imagens usados em designs de formulário no disco. Isso melhora o desempenho, pois os fragmentos e imagens são lidos somente do repositório na primeira solicitação. Em seguida, nas solicitações subsequentes, o serviço de Saída lê fragmentos e imagens do cache de disco. Fragmentos e imagens são armazenados em cache somente em disco, e não na memória.

Você pode usar as seguintes configurações para controlar o armazenamento em cache de fragmentos e imagens no disco. Essas configurações estão localizadas na variável **Configurações do Cache de Recursos do Modelo** Área:

**Cache de recursos** Selecione uma das seguintes opções na lista:

**Ativado para fragmentos e imagens:** O serviço de saída armazena em cache fragmentos e imagens. Esta é a opção padrão.

**Ativado para fragmentos:** O serviço de saída armazena em cache fragmentos, mas não imagens.

**Desativado:** O serviço de saída não armazena em cache fragmentos ou imagens.

**Intervalo de Limpeza (Segundos):** Especifica a frequência com que o serviço de Saída remove arquivos de cache inválidos antigos. O serviço de saída não remove arquivos de cache válidos. Se você alterar o intervalo de limpeza, reinicie o Serviço de saída para que a alteração entre em vigor. Para reiniciar esse serviço, use o Workbench ou consulte Iniciar ou parar os serviços associados aos módulos de formulários AEM para obter instruções.

## Considerações de cluster para caches {#clustering-considerations-for-caches}

Em um ambiente em cluster, cada nó mantém seu próprio cache na memória e no disco. O conteúdo do cache em cada nó depende de quais formulários foram renderizados nesse nó.

O local do cache deve ser idêntico (mesmo disco e caminho) em cada nó do cluster. Não coloque o cache no armazenamento compartilhado.

Se você usar a página Saída no console de administração para alterar as configurações de cache de um determinado nó, as configurações de cache em outros nós serão atualizadas quando uma solicitação for para esse nó. Esse comportamento também se aplica ao botão Redefinir Cache. Se você clicar no botão Redefinir cache de um nó, o cache será imediatamente removido desse nó. O cache em outros nós é limpo quando uma solicitação vai para esse nó.
