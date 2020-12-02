---
title: Quais Ambientes de teste são necessários?
seo-title: Quais Ambientes de teste são necessários?
description: Vários ambientes devem ser considerados como parte dos testes
seo-description: Vários ambientes devem ser considerados como parte dos testes
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Quais Ambientes de teste serão necessários?{#which-test-environments-will-be-needed}

Para definir quais configurações serão testadas, considere o seguinte:

**Desenvolvimento**  - Para Unidade e certos testes de Integração.

**Teste**  - Para a maioria dos testes.

**Ao vivo**  - para testes finais de desempenho e de stress. Também para testes de aceitação com o cliente.

Você também precisará decidir quais instâncias serão necessárias em que local (normalmente, pelo menos uma de cada um para todos os níveis de teste):

**Autor**  - Essa instância permite que os autores insiram e publiquem conteúdo.

**Publicar**  - Essa instância apresenta o site em seu formulário publicado para acesso de visitantes.

Deve ser testado junto com o Dispatcher.

Por fim, o hardware real deve ser considerado - todos os testes de desempenho devem ser feitos em um sistema tão próximo quanto possível da configuração do ambiente final ao vivo. Por esta razão, recomenda-se também que o lançamento do projeto seja dividido em:

**Lançamento**  de software - disponibilidade reduzida; que permite tempo para testes de desempenho, ajuste e otimização em condições realistas no ambiente de produção.

**Inicialização**  forçada - disponibilidade total.
