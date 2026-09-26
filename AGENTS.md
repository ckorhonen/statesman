# Repository Guide

- Statesman is a Ruby state-machine gem; its public code is under `lib/`, adapter behavior and transition semantics are exercised by the RSpec suite, and compatibility policy lives in `docs/COMPATIBILITY.md`.
- Use Bundler to install dependencies and `bundle exec rake` for the default specification task. Preserve transactional transition/audit semantics and add focused specs for behavior changes.

Run commands from the root in a compatible Ruby/Rails environment. The gemspec pins Bundler ~>2.1.4; the checked-in CI matrix covers Ruby 2.4.9/2.6.5/2.7.0 with Rails 5.2.4/6.0.2 or master, which is historical compatibility evidence rather than a claim about current support. Native sqlite3, mysql2, and pg gems need their compiler/client-library prerequisites even when only one database adapter is exercised.

Before `bundle exec rake`, ensure `DATABASE_URL` is absent to use the default in-memory SQLite database, or points only to a disposable test database. `spec/spec_helper.rb` connects to that target and drops/recreates named tables before adapter examples; never inherit a production database URL. Use `bundle exec rspec <spec-path>` for focused checks and `bundle exec rubocop` for style. Preserve `lib/` APIs, adapter transactions, and transition/audit semantics; complete relevant specs and report which adapter/runtime was tested plus unverified matrix combinations.
