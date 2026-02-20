# Refactor Playbook

## Incremental approach
1. Introduce interfaces around current external dependencies.
2. Extract one use case at a time to application layer.
3. Move data mapping out of business logic.
4. Collapse shared utils into explicit domain/application services.
5. Add tests after each extraction to prevent regressions.

## Risk controls
- Avoid big-bang rewrites.
- Keep old and new paths behind feature flags where needed.
- Track latency and error-rate regressions during migration.
