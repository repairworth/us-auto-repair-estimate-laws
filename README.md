# U.S. State Auto Repair Estimate Laws

State-by-state dataset (50 states and the District of Columbia) of the laws and regulations that govern written auto repair estimates in the United States. Compiled and published by RepairWorth (https://repairworth.com/car-repair-estimate/). Release 2026-10-02.

**Not legal advice. Verify the official text.** This dataset summarizes public legal texts for research and consumer information. Laws change, and a short summary can miss exceptions. Read the official text, or ask a lawyer, before relying on any row.

## What it covers

For each jurisdiction: whether a dedicated statute or rule exists and its citation, whether an estimate must be given and above what dollar amount, how far the final bill may exceed the estimate before the customer must consent again, the form of consent, the return of replaced parts, shop registration, and the disclosure of estimate, diagnostic or teardown charges.

Only state-level law is covered. Municipal ordinances are out of scope.

The same table is published, with a checker for written estimates, at https://repairworth.com/car-repair-estimate/

## Files

| File | Content |
|---|---|
| `us-state-auto-repair-estimate-laws.csv` | One row per jurisdiction (51 rows, 18 columns) |
| `evidence.csv` | 270 quotes from official sources, one row per supported field, with the source URL and the retrieval date |
| `LICENSE` | Creative Commons Attribution 4.0 International, full legal text |

Both CSV files are UTF-8 with a header row and LF line endings.

## Method

1. Candidate citations were located with search tools and legal mirrors. Several widely repeated claims turned out to be false: wrong section numbers, bills that were never enacted, a generic "10% or $50" pattern.
2. The rows were then checked against official state websites only: the legislature, the official code publisher, or the state agency that administers the rule. A row is `verified` only when that official text was read. A failed retrieval counts as not conclusive, never as evidence that a law does not exist.
3. Each quote in `evidence.csv` was taken from the official page named in `source_url`. Mirror text is never used as evidence.
4. Nothing is inferred. A row is `lead` when the official text was not read; any citation or reference kept in the record is a pointer to follow up, and the rule fields are empty; the `note` column gives the reference examined and the reason. A row is `no_statute_found` only when an official source was read on the date given and no dedicated statute was found; a search that was not repeated on the official source is a `lead`.

The sources behind RepairWorth data are listed at https://repairworth.com/data-sources/

## Statuses (`status`)

| Status | Meaning | Rows |
|---|---|---|
| `verified` | The official text was read and the row names a statute or rule. Rule values come from that text. | 40 |
| `no_statute_found` | An official source was read on the date given and no dedicated statute was found (`official_url`, `checked_on`). This is a negative finding: it cannot be proven by quotation. Rule cells are empty. | 4 |
| `lead` | The official text was not read; any citation or reference kept in the record is a pointer to follow up, and the rule fields are empty. | 7 |

An empty cell means "not established from the source read". It does not mean "no rule".

## Columns of `us-state-auto-repair-estimate-laws.csv`

| Column | Description |
|---|---|
| `state` | Jurisdiction name (50 states and the District of Columbia). |
| `state_code` | Two-letter USPS code. Primary key. |
| `status` | `verified`, `no_statute_found` or `lead`. See the status table. |
| `has_statute` | `yes` or `partial` on `verified` rows (partial = the rule covers only some shops or some repairs), `no` on `no_statute_found` rows, empty on `lead` rows. |
| `statute_citation` | Citation of the statute or rule. Empty on `no_statute_found` rows; on a `lead` row, a pointer to follow up, or empty. |
| `official_url` | Page of the official state source (legislature, official code publisher or administering agency). Always present on `verified` and `no_statute_found` rows. |
| `secondary_url` | Legal mirror, given for convenience only. Never used as evidence. |
| `written_estimate_required` | Whether the shop must give an estimate, and on what condition. |
| `written_estimate_threshold_usd` | Dollar amount above which the estimate duty applies (integer, USD). |
| `overrun_without_new_consent` | How far the final bill may exceed the estimate before the customer must consent again. |
| `consent_form` | Form of the customer's consent (written, oral, either). |
| `return_of_replaced_parts` | Rule on returning replaced parts to the customer. |
| `shop_registration_required` | Whether repair shops must register with the state. |
| `diagnostic_or_teardown_fee_disclosure` | Rule on disclosing estimate, diagnostic or teardown charges. |
| `verified_quote` | Short verbatim quote from the official source. Empty unless status is verified. |
| `checked_on` | Date (ISO 8601) the official text was read, or the search was run for rows that are not `verified`. |
| `effective_version` | Version or effective date of the text read, when the source states it. |
| `note` | Scope limits, exceptions, the reason a row is not `verified`, and any rule value that has no field-level quote. |

## Columns of `evidence.csv`

| Column | Description |
|---|---|
| `state`, `state_code` | Jurisdiction. |
| `field` | Column of the main file that the quote supports. |
| `quote` | Verbatim text from the official source. |
| `source_url` | Official page the quote was read on. |
| `retrieved_on` | Retrieval date (ISO 8601). |

## Limitations

- Laws change. `checked_on` is the date the text was read, not a guarantee that the text is still current.
- Summaries can omit exceptions (waivers, towing, after-hours drop-off, insurance claims). Read `note` and the source.
- `no_statute_found` covers only the official pages that were read (see `note`) and cannot be proven by quotation. Another chapter, a regulation or a general consumer-protection law may still apply.
- On `verified` rows, every rule cell has at least one quote filed under its own field in `evidence.csv`.
- `evidence.csv` also holds quotes for rows that are not `verified` (for example an enacting session law whose current codified text was not read). They document the search, not a published rule value.
- Some official sites could not be read by an automated tool (JavaScript-only pages, bot blocks, codes published only by a commercial publisher). Those rows are .

## License

The compilation (selection, structure, summaries and annotations) is released under Creative Commons Attribution 4.0 International (CC BY 4.0): https://creativecommons.org/licenses/by/4.0/ . The statutes and regulations themselves are government edicts in the public domain.

## How to cite

RepairWorth (2026). U.S. State Auto Repair Estimate Laws (release 2026-10-02) [Data set]. https://repairworth.com/car-repair-estimate/
