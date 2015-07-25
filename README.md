# bean-add
## A beancount transaction entry assistant

Bean-add is a relatively simple tool designed to ease adding transactions to your beancount [http://furius.ca/beancount/] journal.

To begin, run `bean-add` with your journal file name as the argument. The journal file will be parsed, and you will be presented with a command prompt, not unlike that of fdisk or parted.

Type `h` for a list of available commands.

To add a new transaction, type `n`. Enter the transaction's details: date, description, and the participating accounts and their amounts. You can press `tab` during entry to trigger completion. If there was a transaction with matching description in the past (and there almost always is), you will be presented with an option to reuse the accounts for the new transaction.

Once you are done with the transaction entry, it will be inserted chronologically into your file and you will be returned to the command prompt.

Certain special directives, such as `balance` and `pad` can also be entered using `bean-add`. The commands for those are usually an uppercase letter.

Type `f` to flag the transaction and `t` to tag it with `#bean-add` so you can find it more easily when you later open the journal file with your favorite text editor.

You can navigate to other record in the journal file with `s`. This is useful if you suddenly remember you forgot some minor detail in a previous transaction.

To remove a record from the journal file, type `r`. To undo a recent removal, type `u`.

When you are done entering your transactions, type `w` to write the journal file to disk and `q` to quit.

Type `c` at any point to validate the journal file with `bean-check`. If you plan on using this feature, make sure `bean-check` is in your `$PATH`.

The program is released under the "Do what you feel is right, but don't be a jerk" public license.
