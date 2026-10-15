# Database Baseline & Migration Strategy

The Version 1 database has been consolidated into a frozen canonical PostgreSQL baseline.

The baseline was validated by rebuilding the database from an empty PostgreSQL instance and confirming that the current application could connect to and read the reconstructed schema.

## Fresh Deployments

A fresh environment is created from the canonical Version 1 baseline.

Historical development migrations are not replayed because their final state has already been incorporated into the baseline.

## Future Changes

After the Version 1 freeze, database changes are introduced through ordered forward migrations.

The workflow is:

Canonical Version 1 Baseline
→ New Migration
→ Local Validation
→ Deployment

The frozen baseline is not rewritten for ordinary feature changes.

## Public Repository Scope

The public repository documents the database architecture, migration strategy, and operational model.

Canonical SQL scripts, migration implementation files, application modules, credentials, and other internal implementation details are maintained privately.
