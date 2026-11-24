# TOFIX

Findings from a code scan on 2026-10-04.

## High

- Repo contents - a "Demos for the V programming language" repo with no V code at all: no `*.v` file exists now or anywhere in git history (`git log --all -- '*.v'` is empty). Add the demos (e.g. `src/hello_world.v`) plus a V checker processor in `rsconstruct.toml` (`v fmt -verify` / `v vet`), or retire the repo.

## Medium

- `rsconstruct.toml` - `tera.templates/.github/dependabot.yml.tera` exists but there is no `[processor.tera]` / `[analyzer.tera]` section, so the template is never rendered or checked and `.github/dependabot.yml` can drift from it silently; add the tera processor like the sibling demos repos (`demos-lang-lua/rsconstruct.toml:9-21`), which also needs `config/personal.lua` and `config/version.lua`.
- `README.md:1` - hand-written two-line README, while the rest of the fleet renders `README.md` from the shared `tera.templates/README.md.tera`; add the shared template (plus `config/personal.lua`, `config/version.lua`) so the README is generated and carries the usual license/build badges.

## Low

- `README.md:2` - no description of what is demonstrated or how to run it (`v run <file>.v`); once demos exist, put this in `tera.snippets/main.md.tera`.
- `links.txt` - two reference links at the repo root that nothing references; move them into the README snippet (or `doc/LINKS.txt` as in `demos-lang-lua`).
