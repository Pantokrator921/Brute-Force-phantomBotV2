![PhantomBotV2](https://github.com/user-attachments/assets/73aa24e5-49c6-46e5-b5f5-e7ba447393d2)
# Phantom Bot V2 - Missing Word & Position Finder

This Python script is an advanced version designed to recover a 12-word seed phrase for a Phantom Wallet when **one of the 12 words is missing and its original position is unknown**.

You provide the 11 words you know, and the script will systematically test every possible word from the BIP-39 list in every possible position (1-12) to find your complete phrase.

**IMPORTANT: USE AT YOUR OWN RISK.** Automating wallet recovery is risky. Review the code carefully to ensure it does not perform any malicious actions. The author of this script assumes no liability for any loss of funds.

## How It Works

Unlike the first version which only searched for the 12th word, this script is far more comprehensive:

1.  **Systematic Testing:** The script takes your 11 known words. It then inserts each of the 2048 words from the BIP-39 list into each of the 12 possible positions (i.e., it tests for `word_1`, `word_2`, ..., `word_12`).
2.  **Checksum Validation:** Every single attempt (a 12-word combination) is first checked for a valid BIP-39 checksum before being entered. This is crucial for speeding up the process by immediately discarding thousands of invalid combinations.
3.  **Browser Automation:** The script launches Google Chrome with the Phantom extension, navigates to the recovery page, and inputs the potentially valid phrases.
4.  **Balance Check:** After each successful import, the script checks if the wallet has a balance greater than $0.00.
5.  **Success Report:** If a wallet with a balance is found, the script stops immediately and prints the complete, correct seed phrase to the console.

### **Important Note on Runtime**
This script performs a very large number of checks (up to 12 * 2048 attempts). **Therefore, the process can take a very long time (several hours or more)**, depending on the speed of your computer and internet connection.

## Prerequisites

* Python 3.x
* Google Chrome Browser
* ChromeDriver (must match your Chrome version)
* The `.crx` file of the Phantom Wallet extension

## Installation Guide

1.  **Clone or Download the Repository:**
    ```bash
    git clone [https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git](https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git)
    cd YOUR-REPOSITORY
    ```

2.  **Install Dependencies:**
    Install the required Python library.
    ```bash
    pip install selenium
    ```

3.  **Set up ChromeDriver:**
    * Download the [ChromeDriver](https://googlechromelabs.github.io/chrome-for-testing/) that exactly matches your installed version of Google Chrome.
    * Unzip the file and place `chromedriver` in the same folder as the script or in a directory included in your system's `PATH` variable.

4.  **Create Project Structure:**
    * Create a folder named `phantomBot` in the root directory.
    * Download the [English BIP-39 wordlist](https://github.com/bitcoin/bips/blob/master/bip-0039/english.txt).
    * Save it as `english.txt` inside the `phantomBot` folder.

5.  **Configure the Script:**
    Open the `phantomBotV2.py` file and edit the following lines:

    * **`EXTENSION_PATH`**: Replace the example path with the **absolute path** to your Phantom `.crx` file.
    * **`seed_words`**: Enter the **11 words that you know**. The relative order of these 11 words should be correct.
        ```python
        seed_words = [
            'moral', 'pioneer', 'identify', 'grid', 'cinnamon', 'arrest',
            'invite', 'salmon', 'crumble', 'toddler', 'expose'
        ]
        ```

## Execution

Run the script from your terminal. Be prepared for a long runtime.

```bash
python phantomBotV2.py
```
