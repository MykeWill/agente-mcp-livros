---
name: pesquisa-produtos
description: "Pesquisa produtos em sites de vendas com Playwright e salva resultados verificados em Markdown. Use para buscar livros, eletrônicos, roupas ou outros produtos por termos e filtros."
---

# Pesquisa de produtos em sites de vendas

## Objetivo

Pesquisar produtos em um site de vendas e gerar um resumo dos resultados em Markdown, sem inventar informações.

## Entradas

Receba do usuário:

- **Site:** URL da loja.
- **Termos de busca:** nomes ou descrições dos produtos a procurar.
- **Filtros opcionais:** categoria, marca, faixa de preço, tamanho, cor ou outros critérios relevantes.
- **Quantidade máxima de resultados:** limite total ou por termo, conforme indicado pelo usuário. Se não estiver claro, peça esclarecimento antes da pesquisa.

## Passo a passo

1. Abra o site informado usando o MCP do Playwright e inspecione a página. Reutilize uma página já disponível quando possível.
2. Identifique se o site oferece um campo de busca. Quando houver, pesquise cada termo nele primeiro. Se o termo estiver em outro idioma, traduza-o para o idioma do site antes de pesquisar, preservando nomes próprios e marcas.
3. Aplique os filtros fornecidos pelo usuário e confira se os resultados correspondem ao termo e aos filtros. Considere correspondência de título e descrição; não trate um produto apenas relacionado como resultado exato.
4. Se não houver campo de busca, navegue pela categoria mais provável para o produto. Evite percorrer o catálogo inteiro.
5. Se ainda não encontrar o produto, consulte no máximo **cinco páginas do catálogo** e pare. Conte as páginas efetivamente abertas nessa busca; não continue além desse limite. Caso a navegação por categoria não seja possível ou suficiente, registre as categorias e páginas consultadas.
6. Respeite a quantidade máxima de resultados informada. Para cada produto encontrado, confira a página do produto e registre:
   - título como aparece no site;
   - preço e moeda;
   - disponibilidade;
   - avaliação, mantendo a escala ou formato apresentado pelo site;
   - categoria.
7. Para o primeiro produto encontrado de cada termo, leia a descrição e escreva um resumo curto, em português, sem adicionar fatos que não estejam descritos na página.
8. Se um dado solicitado não estiver visível ou disponível, registre **“não informado”** em vez de deduzi-lo.
9. Se não encontrar produto correspondente, registre **“não encontrado”** e informe onde procurou, incluindo termos usados, categorias e páginas consultadas, quando aplicável.
10. Salve o resultado no arquivo `resultado-busca.md` na raiz do projeto. Se o usuário indicar outro local, use o local indicado.

## Regras

- Use o MCP do Playwright para navegar e ler o site; não apresente resultados baseados apenas em suposições ou conhecimento prévio.
- Não invente produtos, títulos, preços, disponibilidade, avaliações, categorias ou descrições.
- Não registre dados pessoais de vendedores, como nome, telefone, e-mail ou endereço.
- Respeite o limite de no máximo cinco páginas do catálogo quando a busca exigir percorrê-lo.
- Não percorra o catálogo inteiro; prefira a busca do site e, na ausência dela, categorias pertinentes.
- Mantenha preços, moedas, disponibilidade e avaliações de acordo com o que o site exibe.
- Se a página não carregar ou os dados não puderem ser verificados, informe a limitação no arquivo em vez de apresentar informação incerta como fato.

## Formato do arquivo de saída

Use este formato e preencha somente com informações verificadas:

```markdown
# Resultado da busca

## Produtos encontrados

| Título | Preço | Disponibilidade | Avaliação | Categoria |
|---|---:|---|---|---|
| Título como aparece no site | Preço e moeda | Disponibilidade | Avaliação apresentada | Categoria |

### Título do primeiro produto encontrado para o termo

Resumo curto em português, baseado na descrição do produto.

## Produtos não encontrados

- **Termo pesquisado:** não encontrado. Procurei em [busca/categorias/páginas consultadas].
```

Inclua um subtítulo e resumo para o primeiro produto encontrado de **cada termo**. Se não houver produtos encontrados ou não houver termos sem correspondência, mantenha as seções com uma nota clara, por exemplo: “Nenhum produto encontrado” ou “Todos os termos tiveram resultados”.
