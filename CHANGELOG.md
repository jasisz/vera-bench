# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.0.4] - 2026-03-30

### Added

- TypeScript baseline runner (`vera-bench baselines --language typescript`)
- TypeScript LLM generation (`vera-bench run --model MODEL --language typescript`)
- TypeScript prompt builder with automatic snake_case → camelCase conversion
- TypeScript code evaluation via `npx tsx` (Node.js 22+)
- Node.js 22 added to CI test job for TypeScript support
- `_snake_to_camel()` utility for entry_point name conversion

### Changed

- `--language` flag now accepts `vera`, `python`, or `typescript`
- `--language` warning for Vera-specific flags generalised to all non-Vera languages
- `_find_baseline_file()` now uses language-specific file extensions

## [0.0.3] - 2026-03-30

### Added

- `--language python` flag on `vera-bench run` for cross-language LLM comparison
- Python prompt builder (`build_python_prompt`) — minimal prompt without SKILL.md or contracts
- Python code evaluation via subprocess with test wrapper
- `extract_code()` now handles `python` and `py` fence tags alongside `vera`
- Vera-specific metrics (verify@1, fix@1) hidden for Python runs
- Warning when Vera-only flags are used with `--language python`
- CHANGELOG.md, CODE_OF_CONDUCT.md, CONTRIBUTING.md, SECURITY.md
- CI and Codecov badges in README

### Security

- Python subprocess runs with `cwd=work_dir` and API keys stripped from env
- SyntaxError/ImportError/NameError in generated Python sets `check_pass=False`
- Guard against None VeraRunner for non-Python languages

## [0.0.2] - 2026-03-29

### Added

- `vera-bench baselines` command — runs canonical Python solutions against test cases
- `baseline_runner.py` — subprocess-based Python execution with generated test wrappers
- Cross-language comparison in `vera-bench report` (Vera results alongside Python baselines)
- Bool string normalisation for test cases (`"true"`/`"false"` → Python `True`/`False`)

### Fixed

- `run_correct` reporting: shows `-` instead of `0%` when no test cases exist (Tier 2/3)
- `check_rate` type annotation corrected to `float | None`

## [0.0.1] - 2026-03-29

### Added

- LLM runner harness — `vera-bench run --model MODEL` works end-to-end
- `models.py` — Anthropic and OpenAI API abstraction with lazy imports
- `runner.py` — generate → check → verify → run → fix pipeline with retry-on-error
- `metrics.py` — check_rate, verify_rate, fix_rate, run_correct_rate aggregation
- `report.py` — markdown report generation (summary table, tier breakdown, per-problem detail)
- `prompts.py` — full-spec and spec-from-NL prompt construction with SKILL.md context
- Incremental JSONL output (survives crashes)
- 50 benchmark problems across 5 tiers with canonical Vera, Python, and TypeScript solutions
- `vera-bench validate` — full validation pipeline (schema, vera check, vera verify, test execution)
- CI with lint, security, coverage, and dependency audit
- README with installation instructions and quick start

### First benchmark results

- Claude Sonnet 4: 96% check@1, 96% verify@1, 83% run_correct (50 problems, full-spec mode)
- Python canonical baselines: 100% run_correct (24 testable problems)

[Unreleased]: https://github.com/aallan/vera-bench/compare/v0.0.4...HEAD
[0.0.4]: https://github.com/aallan/vera-bench/compare/v0.0.3...v0.0.4
[0.0.3]: https://github.com/aallan/vera-bench/compare/v0.0.2...v0.0.3
[0.0.2]: https://github.com/aallan/vera-bench/compare/v0.0.1...v0.0.2
[0.0.1]: https://github.com/aallan/vera-bench/releases/tag/v0.0.1
