# MysticOCR - Leitor OCR para Cartas Magic: The Gathering

Este projeto é uma ferramenta em Python para reconhecer cartas de Magic: The Gathering a partir de imagens, utilizando OCR (Reconhecimento Óptico de Caracteres), correspondência com um banco de dados e atualização automática de preços das cartas.

## Funcionalidades

- **OCR**: Reconhece texto em imagens de cartas usando EasyOCR.
- **Banco de Dados**: Armazena resultados do OCR e informações das cartas.
- **Correspondência**: Faz o pareamento dos textos reconhecidos com cartas reais usando técnicas de fuzzy matching.
- **Atualização de Preços**: Baixa preços atualizados das cartas via API Scryfall.
- **Processamento em Massa**: Suporte para escanear várias imagens automaticamente.
- **Download Automático**: Baixa o banco de dados de cartas atualizado.

## Dependências

Instale as dependências com:

```
pip install -r requirements.txt
```

Lista de pacotes:

- `easyocr`
- `opencv-python`
- `tqdm`
- `fuzzywuzzy`
- Além disso, requer `psycopg2` para integração com banco de dados PostgreSQL.
- `requests`
- `pyyaml`

## Configuração

Configure o arquivo `mysticocr.yml` com os seguintes parâmetros principais:

```yaml
mystic:
  command: scan | scan_new | match | price
  scan:
    image_dir: caminho/para/imagens
    show_image: true | false
  database:
    host: localhost
    port: 5432
    user: seu_usuario
    password: sua_senha
    dbname: nome_do_banco
```

**Nunca armazene credenciais sensíveis diretamente no código. Use variáveis de ambiente para proteger seus dados.**

## Como usar

Execute o script principal com:

```
python MysticOCR3.py
```

O comportamento depende do comando configurado:

### 1. `scan`

- Escaneia todas as imagens `.jpg` no diretório configurado.
- Realiza OCR e salva os resultados no banco de dados.
- Pode exibir as imagens com anotações do OCR.

### 2. `scan_new`

- Escaneia apenas imagens novas que ainda não estão no banco de dados.

### 3. `match`

- Carrega um arquivo JSON com cartas baixadas da Scryfall.
- Faz a correspondência dos textos OCR com as cartas reais usando fuzzy matching.
- Atualiza o banco de dados com os resultados.

### 4. `price`

- Baixa o banco de dados de cartas atualizado da Scryfall.
- Atualiza os preços das cartas no banco de dados local.

## Passos recomendados

1. Configure o arquivo `mysticocr.yml`.
2. Execute com comando `scan` para processar as imagens.
3. Execute com comando `match` para associar os textos às cartas.
4. Execute com comando `price` para atualizar os preços.

## Estrutura do Projeto

- `MysticOCR3.py`: Script principal.
- `MysticPricer.py`: Atualização de preços.
- `classes/`
  - `OCR.py`: Classe para OCR.
  - `Matcher.py`: Classe para correspondência.
  - `Database.py`: Classe para interação com banco de dados.
  - `BulkData.py` e `Card.py`: Manipulação de dados das cartas.
- `mysticocr.yml`: Configurações.
- `requirements.txt`: Dependências.

## Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## Contribuição

Contribuições são bem-vindas! Por favor, abra uma *issue* ou envie um *pull request*.

---
Documentação atualizada para refletir toda a estrutura e funcionalidades do projeto, em português brasileiro.
