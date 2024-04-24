---
title: Reestruturação do repositório do E-Commerce no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura do repositório no AEM 6.5 para E-Commerce.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---

# Reestruturação do repositório do E-Commerce no AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Conforme descrito no pai [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md) , os clientes que estiverem atualizando para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam a solução AEM E-Commerce. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

## Com atualização para 6.5 {#with-upgrade}

### Produto, Pedido, Coletas, Classificações, Métodos de Entrega e Dados de Métodos de Pagamento {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Você pode usar um <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migração lenta</a> tarefa para migrar dados do E-Commerce.</p> <p>Ele executa as seguintes etapas:</p>
    <ul>
     <li>ajusta as referências ao local antigo para apontar para o novo local</li>
     <li>move o conteúdo do local antigo para o novo local</li>
     <li>remove o local antigo para eventualmente ativar o uso do novo local em todo o sistema</li>
    </ul> <p>Os locais abrangidos pela tarefa são:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Para catálogos maiores, a Adobe recomenda que você execute a tarefa de migração de comércio individualmente, transmitindo a seguinte propriedade do sistema Java™ para AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Após a migração, reinicie o AEM.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
