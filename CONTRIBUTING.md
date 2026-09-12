# Diretrizes de Organização e Fluxo de Trabalho

Este documento estabelece a arquitetura do site, o fluxo de versionamento com Git, os padrões de publicação em Markdown/Jekyll e as convenções editoriais adotadas neste repositório.

---

## 1. Visão Geral e Propósito

Este repositório contém a página pessoal e o blog de **Tito Spadini**, construído com **Jekyll** e hospedado no **GitHub Pages**.
- **Autor:** Tito Spadini.
- **Idioma principal:** Português do Brasil (`pt-BR`).
- **Filosofia de organização:** Simplicidade, consistência visual, controle de versão limpo, semântica web e preservação integral dos textos autorais.

---

## 2. Diretriz Editorial Primordial (Intocabilidade do Teor)

- **Obras Estritamente Autorais:** Todos os ensaios, artigos e publicações reunidos neste repositório são de autoria exclusiva de Tito Spadini.
- **Intocabilidade do Conteúdo:** O teor, estilo, argumentação, ritmo, escolhas de vocabulário e conteúdo dos textos **nunca devem ser modificados, parafraseados, resumidos, ampliados ou suprimidos**, a menos que expressamente determinado pelo autor.
- **Escopo de Suporte e Manutenção:** Quaisquer contribuições, automações ou ferramentas de suporte (incluindo assistentes de IA) devem ater-se exclusivamente a:
  - Conversão mecânica de formatos (por exemplo, de LaTeX para Markdown) preservando rigorosamente o texto;
  - Adequação aos metadados do Jekyll (frontmatter YAML);
  - Organização de arquivos, imagens e integridade de diretórios;
  - Manutenção de layouts HTML, estilos SASS/CSS e configuração do Jekyll (`_config.yml`);
  - Infraestrutura, scripts e comandos do Git;
  - Correções pontuais e estritamente mecânicas/ortográficas quando solicitadas pelo autor.

---

## 3. Estrutura de Diretórios e Arquivos

```text
.
├── _config.yml                        <-- Configurações globais do Jekyll
├── _layouts/                          <-- Modelos de layout HTML (default, post, etc.)
├── _posts/                            <-- Ensaios e publicações em Markdown
│   └── AAAA-MM-DD-titulo-do-post.md   <-- Post com padrão de data e slug
├── _sass/                             <-- Estilos e folhas de estilo SASS/SCSS
├── assets/                            <-- Arquivos estáticos (CSS, fontes, ícones)
├── images/                            <-- Imagens utilizadas nas postagens e páginas
├── docs/                              <-- Documentos e anexos auxiliares (PDFs, etc.)
├── index.md                           <-- Página inicial sobre o autor
├── ensaios.html                       <-- Listagem de ensaios publicados
├── publicacoes.md                     <-- Lista de publicações acadêmicas
├── livros.md                          <-- Recomendações e referências bibliográficas
├── contato.md                         <-- Informações de contato
└── CONTRIBUTING.md                    <-- Este guia de diretrizes e fluxo de trabalho
```

---

## 4. Padrões de Publicação de Ensaios (`_posts/`)

### 4.1. Nomenclatura dos Arquivos
Os arquivos dentro da pasta `_posts/` devem seguir rigorosamente o padrão exigido pelo Jekyll:
```text
AAAA-MM-DD-<slug-em-kebab-case>.md
```
- **Data (`AAAA-MM-DD`):** Data oficial de publicação ou data de conclusão da escrita.
- **Slug:** Em caixa baixa (*kebab-case*), sem acentos ou caracteres especiais, sintetizando o tema do ensaio (ex.: `2025-11-19-propostas-e-projetos-para-ufabc.md`).

### 4.2. Cabeçalho Frontmatter (YAML)
Todo arquivo de post deve iniciar obrigatoriamente com o frontmatter delimitado por `---`:

```yaml
---
layout: post
title:  "Título Completo do Ensaio"
date:   AAAA-MM-DD 00:00:00 -0300
author: Tito Spadini
published: true
---
```

### 4.3. Estrutura Interna do Texto
1. **Título Principal (H1):** Logo após o frontmatter, iniciar o corpo do documento com o título principal:
   ```markdown
   # Título Completo do Ensaio
   ```
2. **Subseções (H2, H3):**
   - As divisões principais do ensaio utilizam cabeçalhos de nível 2 (`## Nome da Seção`).
   - Subdivisões internas utilizam nível 3 (`### Nome da Subseção`).
3. **Tipografia e Caracteres:**
   - Usar aspas curvas/tipográficas (“ e ”) ou aspas regulares de forma consistente.
   - Usar travessões (`—`) para orações intercaladas e quebras de pensamento.
   - Em caso de conversão a partir de LaTeX, desescapar símbolos que não exigem escape em Markdown (como cifras `R$` em vez de `R\$`).

---

## 5. Fluxo de Trabalho com Git

### Estrutura de Branches:
- **`master`:** Branch principal do repositório (refletida diretamente no GitHub Pages). Contém apenas posts prontos para publicação e a versão estável do site.
- **`<nome-do-ensaio>` ou `<feature>`:** Branches temporárias para redação de novos ensaios extensos ou alterações estruturais de layout.

### Ciclo de Vida para Novo Post:

#### 1. Criação do Post
```bash
# Garantir que a branch principal está atualizada
git checkout master
git pull

# (Opcional) Criar branch temática se for uma edição longa
git checkout -b novo-ensaio

# Criar o arquivo em _posts
touch _posts/AAAA-MM-DD-titulo-do-ensaio.md
```

#### 2. Edição e Pré-visualização Local
- Escrever ou importar o conteúdo com o frontmatter apropriado.
- Se necessário, testar localmente com Jekyll:
  ```bash
  bundle exec jekyll serve
  ```

#### 3. Publicação
```bash
git add _posts/AAAA-MM-DD-titulo-do-ensaio.md
git commit -m "[ENSAIO] Adiciona post: Título do Ensaio"
git checkout master
git merge novo-ensaio    # se usada branch temática
git push origin master
```

---

## 6. Padrão de Mensagens de Commit

Para manter o histórico do Git limpo, rastreável e informativo, adota-se um padrão com tags semânticas:

### 1. Título com Tag Semântica:
Breve e objetivo (até ~60-72 caracteres), precedido pela tag entre colchetes:
- `[ENSAIO]` — Adição ou revisão de ensaios em `_posts/`.
- `[LAYOUT]` — Modificações em `_layouts/`, `_sass/` ou CSS.
- `[PAGE]` — Alterações em páginas estáticas (`index.md`, `contato.md`, `livros.md`, etc.).
- `[DOCS]` — Documentação do repositório (`CONTRIBUTING.md`, `README.md`).
- `[CONFIG]` — Mudanças no `_config.yml` ou dependências do Jekyll/Gemfile.

### 2. Padrão Específico para a Tag `[ENSAIO]`:
Para publicações e ensaios, a mensagem do commit não deve focar em etapas mecânicas de edição ou conversão de arquivos, mas sim no **conteúdo e na temática do próprio ensaio**:
- **Título:** `[ENSAIO] Adiciona post: Título do Ensaio` (ou `[ENSAIO] Atualiza post: Título do Ensaio`).
- **Lista de tópicos (Bullets):** Os títulos das seções/propostas principais que compõem o ensaio ou os eixos temáticos centrais abordados.
- **Corpo do texto:** Uma síntese ou resumo conceitual do ensaio, contextualizando as motivações, reflexões e objetivos da obra.

### 3. Modelo Geral de Estrutura de Commit:
```text
[TAG] Título conciso da alteração

- Ponto ou tópico principal
- Segundo detalhe ou eixo temático relevante

Descrição textual contextualizada explicando a alteração (ou, no caso de [ENSAIO], uma síntese do teor da obra publicada).
```
