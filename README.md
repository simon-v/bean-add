# bean-add
## A beancount transaction entry assistant

Bean-add is a relatively simple tool designed to ease adding transactions to your beancount [http://furius.ca/beancount/] journal. While both vi and EMACS have extensions for dealing with ledger and beancount files, some people prefer to edit their text with Nano.

To begin, run `bean-add` with your journal file name as the argument. The journal file will be parsed, and you will be presented with a command prompt, not unlike that of fdisk or parted.

Type `h` for a list of available commands.

To add a new transaction, type `n`. Enter the transaction's details: date, description, and the participating accounts and their amounts. You can press `tab` during entry to trigger completion. If there was a transaction with matching description in the past (and there almost always is), you will be presented with an option to reuse the accounts for the new transaction.

If, during transaction entry, you enter an amount of zero for any of the accounts, that account will be removed from the transaction, allowing you to correct any mistakes on the fly.

Once you are done with the transaction entry, it will be inserted chronologically into your file and you will be returned to the command prompt. Note that this assumes that your beancount file is sorted by date; If it isn't, the results will be unpredictable. Fortunately, this sorting method can be disabled through the options (see below).

Certain special directives, such as `balance` and `pad` can also be entered using `bean-add`. The commands for those are usually an uppercase letter.

Type `f` to flag the transaction. Type `t` to add or remove transaction tags.

You can navigate to other record in the journal file with `s`. This is useful if you suddenly remember you forgot some minor detail in a previous transaction.

To remove a record from the journal file, type `r`. To undo a recent removal, type `u`.

When you are done entering your transactions, type `w` to write the journal file to disk and `q` to quit.

Type `c` at any point to validate the journal file with `bean-check`. If you plan on using this feature, make sure `bean-check` is in your `$PATH`.

Type `o` to view a list of option commands that modify the way bean-add works and their current settings.

The program is released under the "Do what you feel is right, but don't be a jerk" public license, and it comes without any kind of warranty.
