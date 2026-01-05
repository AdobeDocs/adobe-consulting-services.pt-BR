---
title: Perguntas frequentes sobre integração com o Veeva Vault
description: Perguntas frequentes sobre integração com o Veeva Vault
exl-id: c308ebb3-7881-4094-9f35-c67a96fb5ab1
source-git-commit: b024e4295b5b37030c1524342832400c279c650a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# Perguntas frequentes

**Quais metadados devem ser sincronizados com o Veeva?**

É importante entender os metadados com base no tipo de conteúdo (por exemplo, promoções) no Veeva Portal. Depois de revisar o Veeva Portal, crie o esquema de metadados de conteúdo no AEM para manter todos os metadados relevantes para cada ativo/página e configure a integração para mapear os metadados entre os dois sistemas.

**A integração oferece suporte aos documentos vinculados da Veeva? Caso contrário, quais tipos de relação são suportados?**

Não. Consulte a [documentação do Veeva](https://vaulthelp2.vod309.com/wordpress/admin-user-help/documents-admin-user-help/about-document-relationships/). O Documento vinculado (tipo de relacionamento de referência) é um dos tipos de relacionamento padrão que não pode ser criado ou excluído por meio da API devido a um comportamento especial do Vault. Componente, documentos de suporte e qualquer outro que não esteja nesta lista devem poder ser configurados por meio da configuração do AEM Veeva Cloud.

**A integração oferece suporte ao conteúdo modular do AEM?**

Sim, a integração é compatível com Fragmentos de conteúdo e Fragmentos de experiência do AEM.

**A integração suporta o conteúdo modular Veeva?**

Não, não neste momento.

**A integração sincroniza anotações visuais do Veeva com o AEM?**

Não, não neste momento. As anotações visuais só podem ser acessadas por meio da API as a PDF.

**Como definimos permissões em documentos VPM sincronizados pela integração?**

A integração usa um usuário de serviço para carregar documentos por meio da API.  As regras de padronização e substituição de documentos (padronização de funções em documentos) são compatíveis somente com a interface de usuário do VPM e não são aplicadas quando a API é usada. A recomendação é usar o DAC (Dynamic Access Control) para atribuições de funções. O DAC é aplicado por todos os pontos de contato, incluindo a API. [Consulte a documentação aqui.](http://vaulthelp2.vod309.com/wordpress/admin-user-help/ah-user-permissions-access-control/about-dynamic-access-control-for-documents/)

**A integração dá suporte a várias instâncias do VPM?**

A integração usa uma abordagem de configuração de nuvem que permite que vários endpoints do Veeva sejam configurados de uma instância do AEM.

**A integração oferece suporte à publicação do AEM?**

Não, essa integração funciona somente com o autor do AEM. Tem como objetivo facilitar os ciclos de revisão da MLR antes que o conteúdo seja publicado.
