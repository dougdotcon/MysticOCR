# MysticOCR

O MysticOCR é uma ferramenta em Python projetada para reconhecer cartas de Magic: The Gathering a partir de imagens. Utilizando Reconhecimento Óptico de Caracteres (OCR), ela extrai o texto das cartas, faz a correspondência com um banco de dados utilizando *fuzzy matching* e atualiza automaticamente os preços via API da Scryfall.

## Funcionalidades

- **Reconhecimento Óptico de Caracteres (OCR)**: Extrai texto de imagens de cartas usando EasyOCR.
- **Gerenciamento de Banco de Dados**: Armazena resultados do OCR e informações das cartas usando PostgreSQL.
- **Correspondência Difusa (Fuzzy Matching)**: Correlaciona o texto reconhecido com dados reais das cartas, lidando com erros de OCR e variações.
- **Atualização de Preços**: Busca preços de mercado atuais diretamente da API da Scryfall.
- **Processamento em Lote**: Manipula múltiplas imagens automaticamente em uma única execução.
- **Sincronização Automática**: Baixa e atualiza o cache local do banco de dados de cartas.

## Pré-requisitos

- Python 3.8+
- Banco de Dados PostgreSQL
- Conexão com a internet (para API da Scryfall)

## Instalação

1. **Clonar o repositório:**
   bash
   git clone https://github.com/seuusuario/mysticocr.git
   cd mysticocr
   

2. **Instalar dependências:**
   bash
   pip install -r requirements.txt
   

   *Certifique-se de ter as dependências de sistema para o `psycopg2` instaladas.*

## Configuração

Configure a aplicação editando o arquivo `mysticocr.yml`:

yaml
mystic:
  command: scan  # Opções: scan, scan_new, match, price
  scan:
    image_dir: ./imagens
    show_image: true
  database:
    host: localhost
    port: 5432
    user: seu_usuario
    password: sua_senha
    dbname: mystic_db


**Nota de Segurança:** Nunca codifique credenciais sensíveis diretamente. Use variáveis de ambiente ou um gerenciador de segredos.

## Como Usar

Execute o script principal:

bash
python MysticOCR3.py


### Fluxo de Trabalho Recomendado

1. **Escanear Imagens (`command: scan`)**
   - Processa todas as imagens no diretório especificado.
   - Realiza OCR e salva o texto bruto no banco de dados.

2. **Correspondência de Cartas (`command: match`)**
   - Carrega dados de cartas (geralmente de um arquivo JSON bulk da Scryfall).
   - Associa o texto do OCR a cartas específicas e atualiza o banco.

3. **Atualizar Preços (`command: price`)**
   - Busca os preços mais recentes da Scryfall e atualiza o banco de dados.

## Estrutura do Projeto

- `MysticOCR3.py`: Ponto de entrada principal e gerenciador de fluxo.
- `MysticPricer.py`: Módulo para busca e atualização de preços.
- `classes/`: Módulos de lógica central.
    - `OCR.py`: Manipula a extração de texto de imagens.
    - `Matcher.py`: Lógica para correspondência difusa de texto.
    - `Database.py`: Interface com PostgreSQL.
    - `BulkData.py`: Manipulação de dados em massa da Scryfall.
    - `Card.py`: Modelo de dados de cartas.
- `mysticocr.yml`: Arquivo de configuração.
- `requirements.txt`: Dependências Python.

## Contribuindo

Pull requests são bem-vindos. Para mudanças significativas, por favor, abra uma issue primeiro para discutir o que deseja alterar.

## Licença

[MIT](https://choosealicense.com/licenses/mit/)