---
title: Quais ambientes de teste são necessários?
description: Vários ambientes devem ser considerados como parte do teste
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%
---
# Quais ambientes de teste são necessários?{#which-test-environments-will-be-needed}

Para definir quais configurações para teste, você deve considerar o seguinte:

**Desenvolvimento** - Para a Unidade e determinados testes de Integração.

**Testando** - Para a maioria dos testes.

**Ao vivo** - Para desempenho final e testes de stress. Também para testes de aceitação com o cliente.

Decida quais instâncias são necessárias e onde (geralmente, pelo menos uma de cada para todos os níveis de teste):

**Autor** - Esta instância permite que os autores insiram e publiquem conteúdo.

**Publicar** - Esta instância apresenta o site em seu formulário publicado para acesso dos visitantes.

Testado com a Dispatcher.

Por fim, o hardware real deve ser considerado - todos os testes de desempenho devem ser feitos em um sistema com a configuração o mais próxima possível do ambiente ativo final. Por esse motivo, também é recomendável que o Lançamento do projeto seja dividido em:

**Soft Launch** - disponibilidade reduzida; o que permite tempo para testes de desempenho, ajuste e otimização em condições realistas no ambiente de produção.

**Inicialização rígida** - Disponibilidade total.
