# DAO Share Distro Proposal

This workflow builds Participation Steward cycle distribution evidence and a reviewed DAO proposal payload.

Use `rg-dao-ops` for CookieJar evidence, Moloch/DAOhaus inspection, proposal payload preparation, and operator verification. Use `rg-publishing-ops` for Discord review summaries.

The onchain submit step has `autoRun: false`; the operator continues it after reviewing exact DAO, proposal text, recipients, amounts/shares, token/payment fields, and transaction target.
