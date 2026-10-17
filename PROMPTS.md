# Desafio: pesquisa de produtos com Playwright

Registro dos prompts enviados para abrir o site, pesquisar livros e transformar o fluxo em uma skill reutilizável.

## 1. Consultar o título da página

```text
Use o MCP do Playwright pra abrir o site https://books.toscrape.com/ e me dizer o título da página.
```

## 2. Pesquisar livros no site

```text
agora quero que voce use o MCP do Playwright pra fazer uma pesquisa de livros no site https://books.toscrape.com/

o site ta em ingles, mas eu vou te passar os titulos em portugues. entao antes de buscar, traduz o titulo pro ingles (ex: "Sapiens: Uma Breve Historia da Humanidade" -> "Sapiens: A Brief History of Humankind")

livros pra buscar (4 no total):

1. "Sapiens: Uma Breve Historia da Humanidade"
2. "Garota Exemplar"
3. "O Lar da Senhora Peregrine pra Criancas Peculiares"
4. "Harry Potter e o Prisioneiro de Azkaban"

segue essa estrategia, nessa ordem, pra CADA livro:

1. se o site tiver campo de busca, usa ele primeiro
2. se nao tiver, navega pela categoria mais provavel (ex: Fantasy, Young Adult, Nonfiction, Mystery) em vez de percorrer o catalogo inteiro
3. se ainda assim nao achar, percorre no maximo 5 paginas do catalogo e entao para

regras importantes:
- NAO inventa resultado. se nao achar um livro, registra "nao encontrado" e informa onde procurou
- usa o MCP do Playwright de verdade, navegando pelo site

pra cada livro que ACHAR, registra: titulo (como aparece no site, em ingles), preco, disponibilidade, avaliacao (estrelas) e categoria

pro primeiro resultado de cada termo, adiciona tambem um resumo de 2 ou 3 linhas da descricao do livro, EM PORTUGUES

no final, salva tudo no arquivo resultado-busca.md na raiz do projeto.

formata o markdown assim:
- cabecalho "# Resultado da busca"
- secao "## Livros encontrados" com uma tabela (Titulo, Preco, Disponibilidade, Estrelas, Categoria)
- um sub-cabecalho por livro com o resumo de 2 ou 3 linhas em portugues
- secao "## Livros nao encontrados" listando cada um e onde você procurou
```

## 3. Criar uma skill reutilizável

```text
boa! agora eu quero que você transforme todo esse processo que a gente fez em uma skill genérica e reutilizável, salva ela em skills/pesquisa-produtos/SKILL.md

a skill tem que ser genérica, ou seja, não pode ser só pra livros. tem que funcionar pra qualquer site de vendas (livros, eletrônicos, roupas, o que for)

a skill precisa ter essas seções:

1. Objetivo: pesquisar produtos em um site de vendas e gerar um resumo em Markdown

2. Entradas (o que a skill precisa receber pra funcionar):
- o site (URL)
- os termos de busca
- filtros opcionais (categoria, marca, faixa de preço, etc)
- quantidade máxima de resultados

3. Passo a passo (o que o agente deve fazer):
- primeiro tenta usar o campo de busca do site, se existir
- se não tiver, navega pela categoria mais provável em vez de percorrer o catálogo inteiro
- se ainda não achar, percorre no máximo 5 páginas do catálogo e então para
- pra cada produto achado, registra: título, preço, disponibilidade, avaliação e categoria
- pro primeiro resultado de cada termo, adiciona um resumo curto em português
- se não achar, registra "não encontrado" e informa onde procurou

4. Regras:
- não inventar resultados
- não registrar dados pessoais de vendedores
- respeitar o limite de 5 páginas no catálogo

5. Formato do arquivo de saída (como o resultado-busca.md deve ficar):
- cabeçalho com título
- tabela com os produtos encontrados
- sub-cabeçalho por produto com o resumo
- seção com os produtos não encontrados

escreve tudo em português, com tom claro e direto
```

## Consumo aproximado de tokens

Cada leitura de página pelo Playwright também consome tokens, além dos prompts e das respostas. A plataforma não forneceu uma contagem exata; a estimativa geral é de alguns milhares de tokens. O total ficou dentro do esperado para uma pesquisa de quatro termos e a criação da skill.
