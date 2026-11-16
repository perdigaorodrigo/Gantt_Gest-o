# HydroUAI — Gestão de Projetos

Protótipo funcional de Gantt interativo, sem backend e sem dependências externas. Compatível com GitHub Pages.

## Publicar no GitHub Pages

1. Crie um repositório, por exemplo `hydrouai-gestao`.
2. Envie `index.html`, `styles.css`, `app.js` e a pasta `data` para a raiz da branch `main`.
3. No repositório, acesse **Settings → Pages → Build and deployment** e selecione **Deploy from a branch**, `main`, `/ (root)`.
4. Abra `https://SEU-USUARIO.github.io/hydrouai-gestao/` após o GitHub publicar.
5. Para atualizar o Gantt de todos os visitantes, edite e faça commit de `data/projetos.csv`. Recarregue a página.

Também é possível inserir os arquivos dentro de um site HydroUAI já existente (em uma pasta `gestao/`) e acessar a rota correspondente; preserve os caminhos relativos.

## Editar o arquivo CSV no Excel

Abra `data/projetos.csv` no Excel e mantenha estes cabeçalhos (nomes exatos):

`id,categoria,projeto,atividade,responsaveis,inicio,fim,progresso,status,atuacao`

| Campo | Exemplo / regra |
| --- | --- |
| id | Identificador único; não repetir |
| categoria | Ensino, P&D, Fundações, Consultorias ou Prospecção; outras também são aceitas |
| projeto | Nome que aparece na lista e na barra |
| atividade | Descrição breve do trabalho |
| responsaveis | Nomes separados por `;`, como `André;Rodrigo` |
| inicio, fim | Datas ISO `AAAA-MM-DD`; `fim` deve ser igual ou posterior ao início |
| progresso | Número de 0 a 100, sem o símbolo `%`; vazio significa não informado |
| status | `Planejado`, `Em andamento`, `Concluído` etc. |
| atuacao | Tipo de participação: `Supervisão` ou `Execução` (novos valores também são aceitos) |

**Importante:** no Excel, exporte como **CSV UTF-8 delimitado por vírgulas**. Se seu Excel gerar CSV com `;` como separador entre colunas, use a opção de exportação com vírgulas ou converta antes de fazer commit. Os pontos e vírgulas dentro de `responsaveis` devem ficar dentro de uma coluna e são intencionais.

## Funcionalidades

- Gantt interativo com agrupamento por categoria e barras proporcionais à duração e ao progresso.
- Filtros por integrante, categoria, atuação e status; pesquisa por texto.
- Alternância entre visualização mensal e semanal; linha indicando a data atual.
- Painel de indicadores e contagem de prazos vencidos.
- Clique nas barras ou nos itens para exibir detalhes.
- Importação **temporária** de CSV local no navegador para testar uma atualização.
- Exportação de CSV com o resultado filtrado.
- Estrutura 100% estática, sem API e sem custos de hospedagem em repositórios públicos elegíveis.

## Limitações e evolução

Este protótipo é de consulta, não de edição colaborativa: fazer upload de CSV na página NÃO altera o GitHub nem atualiza o arquivo dos outros membros. Para colaboração com login, edição online, autenticação e gravação automática seria necessário adicionar uma camada de dados/autenticação (por exemplo Supabase + GitHub Pages, ou um fluxo baseado na API do GitHub com login seguro). **Não armazene dados confidenciais em CSV de repositório público.**

As linhas do CSV inicial servem apenas como **dados ilustrativos**, inclusive responsáveis, prazos e avanços. Substitua pelos valores oficiais antes de compartilhar o site.

## Teste local

Na pasta do site, execute `python -m http.server 8000` e acesse `http://localhost:8000/`. Abrir `index.html` diretamente como `file://` não permite carregar o CSV por fetch na maioria dos navegadores.

## Atualização de novembro de 2026

CSV recebido do usuário com 20 projetos. Codificação convertida de Windows-1252 e grafias como `MissÃ£o` corrigidas. Datas originalmente em formato americano M/D/AAAA foram convertidas para ISO. Adicionada coluna `atuacao` com os valores Supervisão e Execução, exibidos na lista, nos detalhes e como filtro. Progresso em branco permanece sem informação em vez de ser convertido em 0%.

## Atualização de novembro de 2026

CSV recebido do usuário com 20 projetos. Codificação convertida de Windows-1252 e grafias como `MissÃ£o` corrigidas. Datas originalmente em formato americano M/D/AAAA foram convertidas para ISO. Adicionada coluna `atuacao` com os valores Supervisão e Execução, exibidos na lista, nos detalhes e como filtro. Progresso em branco permanece sem informação em vez de ser convertido em 0%.

## Formatos de data aceitos (v3)

O CSV publicado em `data/projetos.csv` usa datas ISO `AAAA-MM-DD`. Na importação manual, a interface também aceita datas exportadas por Excel em padrão americano `MM/DD/AAAA` (mês/dia/ano), por exemplo `12/1/2026` → `2026-12-01`. Datas impossíveis são rejeitadas e os valores importados são normalizados para ISO ao exportar. A interface contém um único filtro **Atuação**.
