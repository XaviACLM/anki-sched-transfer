Something that I use occasionally to transfer scheduling data between anki decks - e.g. you finish doing core1k and download core2k, at which point you're stuck with core2k having a lot of words that are already in core1k. You could write a script that removed the words in core1k from core2k, but that would mean that you now have to use two separate decks to study the contents of core2k. Insteaad this script here will try to match the cards from core1k to core2k, and copy the scheduling information (next due date and such) from the cards in core1k to the corresponding cards in core2k, so you can remove the core1k deck from your collection and effectively transfer the state of its material into core2k.

The script takes two arguments, a source deck (--source) and a destination deck (--destination), both as apkg files. By default the results of the transfer will be written directly onto the same apkg files, but you can specify other destinations with --output (for the destination deck) and --output-source (for the source deck). The latter is only relevant if you want to write something onto the source deck, which only happens if you want to suspend all the cards that get transferred onto the destination deck - you can do this with --missing zero-out.

Take note that both when exporting the source deck and importing the (modified) destination deck you will need to check a box re: scheduling data - otherwise anki will ignore it by default.

This should work out of the box for DoJG decks, but note that one can modify the name normalization step to work with decks in other formats - in particular there's a commented out normalization step meant to transfer data from Heisig's RTK to Migaku.

## Using this to transfer data between DoJG decks

- Clone this directory somewhere on your computer.
- Put the .apkg files for both decks in the same folder as `main.py`
  - Download the DoJG deck you want to transfer *to* from [here](https://github.com/XaviACLM/dojg-furigana/tree/master/finished_decks).
  - From Anki, export the DoJG deck you're currently using. Make sure to tick the option to include scheduling information.
- Back up the .apkg file you exported (even if it's still in anki - we'll be deleting that later)
- Open some kind of shell in your working directory (easiest way to do this in windows is shift+right click on the empty space in the folder -> open powershell window here)
- Run the command `main.py --source <your-exported-deck> --destination <your-downloaded-deck> --output output.apkg`, replacing the parts in brackets for the corresponding *file*names, with or without extensions.
- If the program throws an exception telling you to include a `--missing` argument:
  - This is because some of the cards in your original deck don't have an equivalent in the deck you downloaded - this is probably because there's a few different versions of the DoJG floating around, some with a bit more cards, some with a bit less. The message right before the exception will have printed out exactly which cards these are, so if they aren't very many you're safe to run the same command with  as before `--missing ignore`.
  - If there *are* very many then something's gone wrong with the script - debug it yourself or feel free to contact me.
- The program will have created an `output.apkg` file in your working directory.
- Open Anki again, select your DoJG deck and click `delete`. Again, make sure you've backed it up before doing this.
- Drag the `output.apkg` file into Anki. In the menu that pops up, make sure to check the option to import scheduling information.
- Done!
