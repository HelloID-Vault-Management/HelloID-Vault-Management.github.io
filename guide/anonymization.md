# Anonymization

Anonymization replaces real personal and business data with realistic fake data before import.

## Enabling Anonymization

1. Check **Anonymize data before import** in the Import view
2. The data is anonymized in memory before being written to the database
3. The original vault.json file is NOT modified

## What Gets Anonymized

### Personal Data
- Names (given name, family name, display name, nickname)
- Email addresses
- Phone numbers
- Home addresses (street, house number, postal code, city, country)
- Birth dates and birth localities
- Usernames
- External IDs

### Business Data
- Department names and display names
- Location names
- Employer names
- Cost center/bearer names
- Team names
- Title names

## Advanced Options

Click **Advanced Options** to customize:

| Option | Description |
|--------|-------------|
| **Consistent business email domains** | Uses consistent domains for business emails |
| **Generate unique domains per employer** | Each employer gets its own email domain |
| **Custom email domain** | Use a specific domain (e.g., `example.com`) |
| **Duplicate last names** | Control how many people can share a surname |
| **Limit dataset for testing** | Import only N persons (managers auto-included) |
| **Seed** | Fixed seed for reproducible anonymization |

## Duplicate Last Name Modes

| Mode | Description |
|------|-------------|
| **Unlimited** | No restrictions on shared names |
| **Unique** | Every person has a unique last name |
| **Max 2 / Max 3 / Max 4** | Up to N people can share the same last name |
| **Pairs** | Consecutive persons share a name (2 per group) |
| **Triples** | Consecutive persons share a name (3 per group) |
| **Quadruples** | Consecutive persons share a name (4 per group) |

## Name Sources

The anonymizer uses European names from multiple locales:
- Dutch (nl)
- German (de)
- French (fr)
- Italian (it)
- Spanish (es)
- Polish (pl)

Names are generated using the Faker library and distributed via a NamePool that ensures the configured duplicate settings are respected.
