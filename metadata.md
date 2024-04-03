---
product: adobe experience manager
solution: Experience Manager
description: Consultando a documentação do Experience Manager
type: Documentation
git-repo: https://github.com/AdobeDocs/adobe-consulting-services.pt-BR
index: y
source-git-commit: e2dac4b36fb94d72b72ef6f73a77e3f566539444
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 54%

---


# Metadados para uso interno

Os metadados no sistema de criação do GitHub são hierárquicos e definidos nos seguintes níveis crescentes de precedentes.

1. metadata.md
1. Índice
1. Artigo

Os metadados definidos no arquivo metadata.md se aplicam a todo o repositório, mas podem ser substituídos nos níveis de índice e artigo. Qualquer substituição dos metadados deve ser feita no nível mais baixo possível.

metadata.md

* `product`
* `git-repo`
* `index: y`

Índices

* `sub-product`
* `user-guide-title`

Artigo

* `title`
* `description`

Informações adicionais sobre os metadados podem ser encontradas no [guia de criação interno](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html).
