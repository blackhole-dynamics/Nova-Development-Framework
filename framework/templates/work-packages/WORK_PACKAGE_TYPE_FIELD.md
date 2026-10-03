# Template Snippet – Work Package Type Field

```yaml
work_package:
  id: ""
  title: ""
  type: ""
  tags: []
  risk_level: ""
  allowed_files: []
  forbidden_files: []
  tests_required: ""
  requires_nova_review: true
  requires_human_maintainer_commit: true
```

## Allowed Types

- review-only
- docs-only
- code-fix
- feature
- test-only
- security-baseline
- security-code-fix
- health-score-update
- ci-diagnostic
- release-prep
- destructive-blueprint
- destructive-implementation
- project-adapter
