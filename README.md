Something that I use occasionally to transfer scheduling data between anki decks - e.g. you finish doing core1k and download core2k, at which point you're stuck with core2k having a lot of words that are already in core1k. You could write a script that removed the words in core1k from core2k, but that would mean that you now have to use two separate decks to study the contents of core2k. Insteaad this script here will try to match the cards from core1k to core2k, and copy the scheduling information (next due date and such) from the cards in core1k to the corresponding cards in core2k, so you can remove the core1k deck from your collection and effectively transfer the state of its material into core2k.

The script takes two arguments, a source deck (--source) and a destination deck (--destination), both as apkg files. By default the results of the transfer will be written directly onto the same apkg files, but you can specify other destinations with --output (for the destination deck) and --output-source (for the source deck). The latter is only relevant if you want to write something onto the source deck, which only happens if you want to suspend all the cards that get transferred onto the destination deck - you can do this with --missing zero-out.

Take note that both when exporting the source deck and importing the (modified) destination deck you will need to check a box re: scheduling data - otherwise anki will ignore it by default.

This should work out of the box for DoJG decks, but note that one can modify the name normalization step to work with decks in other formats - in particular there's a commented out normalization step meant to transfer data from Heisig's RTK to Migaku.
