MTG Instant Draft Machine

The MTG Instant Draft Machine is a Python-based tool that generates highly customized Magic: The Gathering draft packs (Play Boosters, Draft Boosters, Jumpstart, Chaos, and Cube) using the Scryfall API, and prints them instantly to an 80mm thermal receipt printer.
This repository includes a dynamic draft generator (instantdraft.py) and a dedicated print spooler for existing local images (print_spooler.py).

Features
* Multiple Draft Formats: Supports Standard/Draft Boosters, Play Boosters (MKM onwards), Jumpstart packets, full Chaos Drafts, and custom CubeCobra lists.
* Real-time Scryfall Integration: Fetches accurate card text, mana costs, stats, and art directly from Scryfall. Automatically hunts down and prints associated tokens/helpers!
* Dynamic Layout Engine: Automatically scales text, wraps abilities, formats double-faced cards (DFCs) and split cards, and proportionally crops art to fit the receipt paper.
* Thermal Printer Optimization: Utilizes Atkinson Dithering, contrast enhancement, and LANCZOS scaling to convert continuous-tone card art into crisp, readable 1-bit pixel art optimized for thermal printing.
* Mac Silicon Support: Built-in dynamic library fallbacks for Mac M-Series (Apple Silicon) users struggling with USB printer connections.

Prerequisites & Hardware
Hardware:
* An ESC/POS compatible thermal receipt printer (Tested extensively with 80mm Vretti printers, most 80mm POS systems with USB will work).
* 80mm thermal paper.
Software:
* Python 3.7+
* python-escpos
* Pillow (PIL)
* requests

Installation
1. Clone this repository: git clone [https://github.com/yourusername/mtg-instant-draft.git](https://github.com/yourusername/mtg-instant-draft.git) cd mtg-instant-draft 
2. Install the required Python dependencies: pip install "python-escpos[usb]" Pillow requests  Note: On Windows, you may need to set up Zadig USB drivers for python-escpos to communicate with your printer.
3. Configure your Printer (Optional): Open the Python scripts and verify the VENDOR_ID and PRODUCT_ID. The default is 0x1fc9 and 0x2016 (Common for Vretti and Xprinter models). You can find your printer's IDs by looking at your system's USB device tree.

Usage
1. Instant Draft Machine (instantdraft.py)
Run the interactive script to start generating packs:
python3 instantdraft.py 
You will be prompted to enter:
* Set Code: Enter a 3-letter Scryfall set code (e.g., blb, otj, mkm).
* Special Modes: Type CHAOS for a random pack from MTG history, JUMPSTART for an algorithmic Jumpstart packet, or paste a CubeCobra URL to draft from your custom cube!
* Pack Count: How many packs to generate.
* Tokens: Whether or not to fetch and print the associated tokens at the end.
2. Thermal Print Spooler (print_spooler.py)
If you already have a folder of exported proxy images (PNG/JPG) and just want to print them with the high-quality dithering and scaling:
python3 print_spooler.py 
* You will be prompted to provide the path to your image directory.
* The script auto-crops white space, forces landscape orientation, applies Atkinson dithering, and queues them seamlessly to the printer.

Notes on Rate Limiting
This tool strictly adheres to Scryfall's API guidelines by enforcing a 100ms delay between requests. Large sets or cubes may take a few moments to cache.

Contributing
Pull requests are welcome! If you find a bug with a specific card layout or have an idea for a new booster draft algorithm, feel free to open an issue.
