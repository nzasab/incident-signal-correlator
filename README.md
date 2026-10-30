# Incident Signal Correlator

Analyze structured service event logs, group repeated failures into short incident windows, and summarize impact.

## Quick start

Requires Python 3.10+; standard library only. Run from this repository's root.

```bash
python -m app.cli examples/events.jsonl --window-minutes 10 --min-errors 3
```

## Tests

```bash
python -m unittest discover -s tests -v
```

## Architecture

- `app/`: CLI and core analysis logic.
- `examples/`: safe, synthetic example inputs.
- `tests/`: repeatable unit tests.
- `.github/workflows/tests.yml`: CI tests on push and pull requests.

## Engineering decisions

- Read-only analysis: the tool does not modify its input files.
- Machine-readable JSON output facilitates automation and regression testing.
- No third-party dependencies; quick to run and review.

## Current scope and limitations

Processes ISO-8601 UTC JSONL events with service, severity, and message. Aggregation uses a fixed gap from the first error in each window, not a sliding-window incident model. Limited to ERROR and CRITICAL severities. Intended for retrospective analysis of structured data, not a live alerting service.

## Good Claude Code evaluation tasks

1. Ask Claude Code to inspect the implementation and report specific risks without making changes.
2. Add one regression test for a realistic edge case, then request a minimal fix.
3. Review its diff, run the test suite, check failure behavior, and document what you accepted or rejected.

## Attribution

This repository was initially created with AI assistance. Describe subsequent changes and test results accurately when presenting it as a portfolio project.

## License

MIT. See [LICENSE](LICENSE).
