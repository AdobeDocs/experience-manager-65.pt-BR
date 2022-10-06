---
title: Adição de domínios
seo-title: Adding domains
description: Saiba como adicionar um domínio corporativo, local ou híbrido usando configurações de Gerenciamento de domínio e considerações gerais para nomes de domínio e IDs.
seo-description: Learn how to add an enterprise, local, or hybrid domain using Domain Management settings and general considerations for domain names and IDs.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# Adição de domínios {#adding-domains}

## Adicionar um domínio empresarial {#add-an-enterprise-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em Novo domínio empresarial.
1. Na caixa ID, digite um identificador exclusivo para o domínio e, na caixa Nome, digite um nome descritivo para o domínio. (Consulte [Considerações importantes para nomes de domínio e IDs](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique se deseja ativar o bloqueio de conta. (Consulte [Definir configurações de bloqueio de conta](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Por padrão, a opção Habilitar bloqueio de conta está selecionada.
1. Clique em Adicionar autenticação e, na lista Provedor de autenticação , selecione um provedor, dependendo do mecanismo de autenticação que sua organização usa. Os valores possíveis são LDAP, Kerberos, SAML ou um provedor de autenticação personalizado.

   Se você selecionar LDAP, poderá usar o servidor LDAP especificado na configuração do diretório, ou poderá escolher um servidor LDAP diferente para usar na autenticação. Se você escolher um servidor diferente, seus usuários deverão existir em ambos os servidores LDAP.

1. Forneça quaisquer informações adicionais necessárias na página. (Consulte [Configurações de autenticação](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Adicione um diretório ou uma Interface de Provedor de Serviços personalizada (SPI). (Consulte [Adicionar diretórios ou SPIs personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Clique em Finish e em OK.

Depois de criar um domínio corporativo, sincronize manualmente o diretório ou crie um acionador para executar uma sincronização antes que o Gerenciamento de usuários possa usá-lo. Em seguida, você pode configurar um agendamento de sincronização de diretório e executar a sincronização manual, conforme necessário. (Consulte [Sincronização de diretórios](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Adicionar um domínio local {#add-a-local-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em Novo domínio local.
1. Na caixa ID, digite um identificador exclusivo para o domínio e, na caixa Nome, digite um nome descritivo para o domínio. (Consulte [Considerações importantes para nomes de domínio e IDs](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique se deseja ativar o bloqueio de conta e clique em OK. (Consulte [Definir configurações de bloqueio de conta](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Por padrão, a opção Habilitar bloqueio de conta está selecionada.

## Adicionar um domínio híbrido {#add-a-hybrid-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em Novo domínio híbrido.
1. Na caixa ID, digite um identificador exclusivo para o domínio e, na caixa Nome, digite um nome descritivo para o domínio. (Consulte [Considerações importantes para nomes de domínio e IDs](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Clique em Adicionar autenticação e, na lista Provedor de autenticação , selecione um provedor, dependendo do mecanismo de autenticação que sua organização usa. Os valores possíveis são LDAP, Kerberos, SAML ou um provedor de autenticação personalizado.
1. Forneça quaisquer informações adicionais necessárias na página. (Consulte [Configurações de autenticação](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Clique em OK e em OK novamente.

## Considerações importantes para nomes de domínio e IDs {#important-considerations-for-domain-names-and-ids}

Lembre-se das seguintes considerações ao escolher um nome de domínio e ID:

### Considerações gerais {#general-considerations}

* Quando você estiver usando um provedor de banco de dados diferente de DB2, a ID de domínio poderá conter até 50 bytes. Se você estiver usando caracteres ASCII de byte único, o limite será de 50 caracteres. Se o identificador de domínio contiver caracteres multibyte, esse limite será reduzido. Por exemplo, se você criar um domínio cujo identificador contém caracteres de 3 bytes, o limite será de 16 caracteres. Além disso, não é possível criar domínios que contenham caracteres de 4 bytes. Se você criar uma ID de domínio que excede esse limite, AEM formulários estará em um estado instável. Para se recuperar desse estado instável, consulte o &quot; [Remova um domínio que contenha caracteres estendidos ou de vários bytes](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; nesta página.
* O número de domínios corporativos e domínios locais que podem ser criados em AEM formulários depende da duração de cada uma das IDs de domínio. Quando você adiciona um domínio corporativo ou híbrido, o Gerenciamento de usuários atualiza a string configInstance no nó AuthProviders do arquivo de configuração dos formulários AEM (config.xml). A cadeia de caracteres configInstance contém uma lista separada por dois pontos dos caminhos absolutos de todos os domínios associados ao provedor de autorização. Essa string tem um limite de tamanho de 8192 caracteres. Quando esse limite é atingido, não é possível criar domínios adicionais.

### Considerações ao usar o DB2 {#considerations-when-using-db2}

Ao usar o DB2 para o banco de dados de formulários AEM, o comprimento máximo permitido da ID de domínio depende do tipo de caracteres usados:

* 100 bytes únicos (ASCII) (por exemplo, caracteres usados em inglês, francês ou alemão)
* 50 bytes duplos (por exemplo, caracteres usados em idiomas chinês, japonês ou coreano)
* 25 quatro bytes (por exemplo, caracteres usados no idioma chinês tradicional)

### Considerações ao usar o MySQL {#considerations-when-using-mysql}

Ao usar o MySQL como o banco de dados de formulários de AEM, as seguintes limitações se aplicam:

* Use somente caracteres de byte único (ASCII) para a ID de domínio e o nome de domínio. Se você usar caracteres ASCII estendidos, AEM formulários estará em um estado instável e poderá lançar uma exceção se tentar excluir o domínio. Para se recuperar desse estado instável, consulte o &quot; [Remova um domínio que contenha caracteres estendidos ou de vários bytes](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; nesta página.
* Não é possível criar dois domínios que tenham o mesmo nome, mas que sejam diferentes no caso de . Por exemplo, tentar criar um domínio chamado *Adobe* quando um domínio chamado *adobe* já existe resulta em um erro.
* O Gerenciamento de usuários não pode diferenciar dois nomes de domínio que diferem apenas no uso de caracteres estendidos. Por exemplo, se você criar um domínio chamado *abcde* e um domínio chamado *âbcdè*, são consideradas iguais.

### Remova um domínio que contenha caracteres estendidos ou de vários bytes {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Exporte o arquivo de configuração, conforme descrito em [Importação e exportação do arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Abra o arquivo de configuração e, no nó Domains , localize o nó cujo atributo de nome corresponde ao nome do domínio criado com caracteres estendidos ou de vários bytes. Exclua o nó inteiro relacionado a esse domínio.
1. No banco de dados, procure o domínio na tabela edcprincipaldomainentity :

   * Selecionar `*` de edcprincipaldomainentity.
   * Encontre o nome de domínio que contém caracteres estendidos ou de vários bytes e defina seu status como OBSOLETE.

1. Importe o arquivo de configuração atualizado, conforme descrito em [Importação e exportação do arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
