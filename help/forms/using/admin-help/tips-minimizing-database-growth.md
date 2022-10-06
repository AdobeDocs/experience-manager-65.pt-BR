---
title: Dicas para minimizar o crescimento do banco de dados
seo-title: Tips for minimizing database growth
description: Processos de longa duração armazenam dados de processo no banco de dados de formulários AEM. O crescimento do banco de dados de formulários de AEM pode ser minimizado com o uso de algumas estratégias fáceis de design de processos e configuração de produtos.
seo-description: Long-lived processes store process data in the AEM forms database. The growth of the AEM forms database can be minimized using a few easy process design and product configuration strategies.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Dicas para minimizar o crescimento do banco de dados {#tips-for-minimizing-database-growth}

Processos de longa duração armazenam dados de processo no banco de dados de formulários AEM. O crescimento do banco de dados de formulários de AEM pode ser minimizado com o uso de algumas estratégias fáceis de design de processos e configuração de produtos.

## Dicas de design de processo {#process-design-tips}

Use processos de duração curta sempre que possível. Processos de duração curta não armazenam dados de processo no banco de dados. A desvantagem de utilizar processos de curta duração é que o seu estatuto e estado não são rastreados no console de administração e não há histórico do processo.

Algumas operações de serviço, como a operação Atribuir tarefa (serviço do usuário), exigem que sejam usadas em processos de longa duração. Nesse caso, é possível segmentar o processo em vários subprocessos e torná-los de duração curta quando possível. Se você usar essa estratégia, os subprocessos de duração curta deverão lidar com itens de dados grandes, como valores de documento.

Use variáveis com moderação. Ao usar processos de vida longa, para cada instância do processo, o espaço é alocado no banco de dados para cada variável no processo. O uso estratégico de variáveis pode economizar uma quantidade considerável de espaço. Por exemplo, você pode substituir valores de variáveis quando valores antigos não forem mais necessários no processo. E exclua todas as variáveis que você criou e que não estão sendo usadas. Você pode validar o processo para localizar variáveis não utilizadas.

Use tipos de variáveis simples (por exemplo, string ou int) e evite usar tipos de variáveis complexas quando possível. O espaço do banco de dados é alocado para variáveis mesmo quando elas não contêm um valor. As variáveis complexas normalmente requerem mais espaço do que as simples.

## Dicas de administração do produto {#product-administration-tips}

Use o armazenamento global de documentos (GDS) com eficácia. O diretório GDS no servidor de formulários é usado para armazenar, entre outras coisas, arquivos que são passados para serviços que fazem parte AEM formulários em processos. Para melhorar o desempenho, documentos menores são armazenados na memória e mantidos no banco de dados.

o console de administração expõe a propriedade Tamanho máximo em linha do documento padrão para configurar o tamanho máximo de documentos armazenados na memória e persistentes no banco de dados. (Consulte [Definir configurações gerais do AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) Se você definir essa propriedade como um valor baixo, a maioria dos documentos será mantida no diretório GDS em vez de no banco de dados. A vantagem é que você pode excluir mais facilmente os arquivos quando eles não são mais necessários quando eles são armazenados no diretório GDS.
