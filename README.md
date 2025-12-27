# MysticOCR

MysticOCR is an intelligent Python tool designed to recognize Magic: The Gathering cards from images. It leverages Optical Character Recognition (OCR) to extract text, matches it against a database of real cards using fuzzy matching, and automatically updates prices via the Scryfall API.

## Features

- **Optical Character Recognition (OCR)**: Extracts text from card images using EasyOCR.
- **Database Management**: Stores OCR results and card information using PostgreSQL.
- **Fuzzy Matching**: Correlates recognized text with actual card data, handling OCR errors and variations.
- **Price Updates**: Fetches current market prices directly from the Scryfall API.
- **Batch Processing**: Handles multiple images automatically in a single run.
- **Automatic Data Sync**: Downloads and updates the local card database cache.

## Prerequisites

- Python 3.8+
- PostgreSQL Database
- Internet connection (for Scryfall API)

## Installation

1. **Clone the repository:**
   bash
   git clone https://github.com/yourusername/mysticocr.git
   cd mysticocr
   

2. **Install dependencies:**
   bash
   pip install -r requirements.txt
   

   *Ensure you have the system dependencies for `psycopg2` installed.*

## Configuration

Configure the application by editing the `mysticocr.yml` file:

yaml
mystic:
  command: scan  # Options: scan, scan_new, match, price
  scan:
    image_dir: ./images
    show_image: true
  database:
    host: localhost
    port: 5432
    user: your_username
    password: your_password
    dbname: mystic_db


**Security Note:** Never hardcode sensitive credentials. Use environment variables or a secure vault.

## Usage

Run the main script:

bash
python MysticOCR3.py


### Workflow

1. **Scan Images (`command: scan`)**
   - Processes all images in the specified directory.
   - Performs OCR and saves raw text to the database.

2. **Match Cards (`command: match`)**
   - Loads card data (usually from a Scryfall bulk JSON).
   - Matches OCR text to specific cards and updates the database.

3. **Update Prices (`command: price`)**
   - Fetches the latest prices from Scryfall and updates the database.

## Project Structure

- `MysticOCR3.py`: Main entry point and workflow manager.
- `MysticPricer.py`: Module for price fetching and updates.
- `classes/`: Core logic modules.
    - `OCR.py`: Handles image text extraction.
    - `Matcher.py`: Logic for fuzzy matching text to cards.
    - `Database.py`: PostgreSQL interface.
    - `BulkData.py`: Handles Scryfall bulk data operations.
    - `Card.py`: Card data model.
- `mysticocr.yml`: Configuration file.
- `requirements.txt`: Python dependencies.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)