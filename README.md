# The Penguins Club Accounting

A simple, [plain-text accounting](https://plaintextaccounting.org/) setup for [The Penguins Club](https://thepenguins.club/) using [hledger](https://hledger.org/).

## Repository Structure

```bash
fishcounting/
├── .env
├── .env.example
├── .gitignore
├── README.md
└── the-penguins-club-accounting.journal
```

## Requirements

- [hledger](https://hledger.org/install.html)
- Bash or a compatible shell

## Setup

Copy the example environment file:

```bash
cp .env.example .env
```

The `.env` file should contain:

```env
LEDGER_FILE=./the-penguins-club-accounting.journal
```

Load the environment variables:

```bash
set -a; source .env; set +a
```

## Verify the Journal

Display all accounts, including zero-balance accounts:

```bash
hledger accounts
hledger bal --empty
```

Display the balance sheet:

```bash
hledger bs
```

Check journal consistency:

```bash
hledger check
```

## Record Transactions

Example: receiving a donation of 1,000 BDT into the organization's bank account.

Add the following transaction to `the-penguins-club-accounting.journal`:

```journal
2026-10-15 Donation received
    assets:bank       1000 BDT
    income:donations -1000 BDT
```

Review the resulting balances:

```bash
hledger bal
hledger register
hledger is
```

## GUI

### hledger-web

A browser-based interface for viewing accounts, balances, and transactions.

```bash
hledger web
```

Open the local URL printed by hledger-web, typically `http://localhost:5000`.

Documentation: https://hledger.org/1.52/hledger-web.html

### hledger-ui

An interactive terminal interface for browsing accounts and entering transactions.

```bash
hledger ui
```

Documentation: https://hledger.org/1.52/hledger-ui.html

**Security:** Keep the web interface on a trusted local environment. Do not expose it publicly without appropriate access controls.

## Environment Configuration

`.env.example`:

```dotenv
LEDGER_FILE=./the-penguins-club-accounting.journal
```

`.gitignore`:

```gitignore
.env
.DS_Store
```

The `.env` file is not loaded automatically by hledger. Load it in your shell before running commands, or use a tool such as `direnv`.

## Accounting Principles

- The journal starts with zero balances.
- Every transaction must balance.
- Use consistent account names and currency conventions.
- Keep the journal under version control.
- Never commit secrets or private configuration.
- Back up the journal regularly.

## Resources

- hledger documentation: https://hledger.org/doc.html
- hledger installation: https://hledger.org/install.html
- hledger-web: https://hledger.org/1.52/hledger-web.html
- hledger-ui: https://hledger.org/1.52/hledger-ui.html
