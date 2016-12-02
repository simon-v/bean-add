# bean-add
## A beancount transaction entry assistant

Bean-add is a relatively simple tool designed to ease adding transactions to your beancount (http://furius.ca/beancount/) journal. While both vi and EMACS have extensions for dealing with ledger and beancount files, some people prefer to edit their text with Nano.

To begin, run `bean-add` with your journal file name as the argument. The journal file will be parsed, and you will be presented with a command prompt, not unlike that of fdisk or parted.

Type `h` for a list of available commands.

To add a new transaction, type `n`. Enter the transaction's details: date, description, and the participating accounts and their amounts. You can press `tab` during entry to trigger completion. If there was a transaction with matching description in the past (and there almost always is), you will be presented with an option to reuse the accounts for the new transaction.

If, during transaction entry, you enter an amount of zero for any of the accounts, that account will be removed from the transaction, allowing you to correct any mistakes on the fly. For more elaborate corrections, use the `e` command. If you plan on using this feature, make sure `$EDITOR` is set to your preferred editor.

Once you are done with the transaction entry, it will be inserted chronologically into your file and you will be returned to the command prompt. Note that this assumes that your beancount file is sorted by date; If it isn't, the results will be unpredictable. Fortunately, this sorting method can be disabled through the options (see below).

Certain special directives, such as `balance` and `pad` can also be entered using `bean-add`. The commands for those are usually an uppercase letter.

Type `f` to flag the transaction. Type `t` to add or remove transaction tags.

You can navigate to another record in the journal file with `s`. This is useful if you suddenly remember you forgot some minor detail in a previous transaction. There are also shortcuts available for seeking one record forward and backwards, as well as to the beginning and end of the journal file. To find the record number you want, you can either type `l` to search for records that contain a certain string, or `j` to examine the transaction's immediate context. You can also type `b` to attempt to calculate the final balance of an account on the fly.

To remove a record from the journal file, type `r`. To undo a recent removal, type `u`. You can also use these two commands in a succession to reinsert a transaction in an appropriate place after editing it, if so desired.

When you are done entering your transactions, type `w` to write the journal file to disk and `q` to quit.

Type `c` at any point to validate the journal file with `bean-check`. If you plan on using this feature, make sure `bean-check` is in your `$PATH`.

Type `o` to view a list of option commands that modify the way bean-add works and their current settings.

Some degree of scripting is possible by piping input into `bean-add`. For example, if you know that your bank charges you $1.95 every month for holding a checking account (and most banks do), then you could write a script, replicating your keystrokes, similar to:

    #!/bin/sh
    echo 'n
    
    Bank service charge
    y
    1.95 USD
    
    
    wq' | bean-add journal.bnct

And then have `cron` or another scheduler execute it every month, on the 1st, thus saving you the effort.

Another use for scripting has been proposed in the comments on the issue regarding [split-file beancount journals](https://github.com/simon-v/bean-add/issues/3#issuecomment-250917599).

`bean-add` provides a basic capability to perform credit card statement verification. To begin, type `v`, then feed in the name of the account which contains the transactions on the statement (likely, something like `Liabilities:CreditCard`), the name of the account from which the statement is paid (likely, something like `Assets:Bank:Checking`) and the statement's grand total. Select the records that appear on the statement by typing their numbers. Typing a record number that is already in the statement will remove it. For this to work as expected, be sure to `f`lag every record that hasn't yet appeared on a statement; Only flagged records are considered for addition. In addition, if the record contains multiple legs that are not paid out at the same time, make sure to also flag each of those legs (the `ff` command is helpful here); The flags will be used to track the legs' "paid" status.

To make things easier for you, the `of` option exists, which automatically flags new transactions that contain any of the specified accounts.

If, at some point during statement verification, you discover an error in one of the records, you can interrupt the process by pressing `Control-C`. When you next press `v`, you will be offered to continue from where you left off.

Once the sum of balances of all transactions in the statement matches the statement's target, you will be prompted for the statement's date and description. `bean-add` will then unset the flags of all records on the statement to prevent them from being used on another statement and add the statement's own record.

This program is free software, released under the Apache License, Version 2.0. See the LICENSE file for more information.

The program's canonical project page resides at http://github.com/simon-v/bean-add/
