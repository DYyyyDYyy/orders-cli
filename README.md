# orders-cli

A command-line tool for browsing and analysing online-shop orders stored in a JSON file. Node.js (ES modules) and [commander](https://github.com/tj/commander.js). The interface is in Ukrainian.

```bash
npm install
node index.js list --limit 5           # short list of orders
node index.js get 1001                 # one order in full
node index.js field 1001 customer.phone   # nested field by dot path
node index.js items 1001 --sort sum    # line items with per-line sums
node index.js total 1001               # order total
node index.js summary 1001             # delivery and payment summary
node index.js -f other.json list       # another data file
```

```text
$ node index.js items 1001
Позиції замовлення №1001 (сортування: sum, спадання: ні):
1. STM32 Black Pill Microcontroller | Кількість: 2 шт. | Ціна: 150.50 грн | Сума: 301.00 грн
2. TBS Crossfire Nano RX | Кількість: 3 шт. | Ціна: 1200.00 грн | Сума: 3600.00 грн
3. Radiomaster TX16S Transmitter | Кількість: 1 шт. | Ціна: 8500.00 грн | Сума: 8500.00 грн
```

## What it handles

- Async file reading with `fs/promises`. A missing file, invalid JSON or a root that is not an array produces a clear message and exit code 1.
- Every commander error (missing argument, unknown option or command) is rewritten into a readable message through `configureOutput`.
- Nested field access by dot path (`customer.address.city`).

Written for the Web Programming course at Ivan Franko National University of Lviv (2026).
