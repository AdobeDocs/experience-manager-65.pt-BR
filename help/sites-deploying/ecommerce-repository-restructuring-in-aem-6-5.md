---
title: Reestruturação do repositório de comércio eletrônico no AEM 6.5
seo-title: Reestruturação do repositório de comércio eletrônico no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 for E-Commerce.
seo-description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 for E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Atualização
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# Reestruturação do repositório de comércio eletrônico no AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Conforme descrito na página principal [Reestruturação do Repositório AEM 6.5](/help/sites-deploying/repository-restructuring.md), os clientes que atualizam para AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações do repositório que afetam a solução AEM de comércio eletrônico. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

## Com a atualização 6.5 {#with-upgrade}

### Dados de Produtos, Pedidos, Coleções, Classificações, Métodos de Entrega e Métodos de Pagamento {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Você pode usar uma tarefa <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Lazy Migration</a> para migrar dados de E-Commerce.</p> <p>Ele executa as seguintes etapas:</p>
    <ul>
     <li>ajusta referências à localização antiga para apontar para a nova localização</li>
     <li>move o conteúdo do local antigo para o novo local</li>
     <li>remove a localização antiga para ativar eventualmente a utilização da nova localização em todo o sistema</li>
    </ul> <p>Os locais cobertos pela tarefa são:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/Shipping-methods<br /> </li>
    </ul> <p>Para catálogos maiores, é recomendável executar a tarefa de migração de comércio individualmente, passando a seguinte propriedade do sistema Java para AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Depois da migração, o AEM precisa ser reiniciado.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

