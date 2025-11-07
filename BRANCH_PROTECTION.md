# Branch protection example

This repository includes a sample payload file `branch-protection-payload.json` you can use to configure GitHub branch protection for `master`.

## Example (curl)

Uses your gh-auth token to send a proper JSON body (preserves nulls and nested objects):

```bash
curl -S -X PUT \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer $(gh auth token)" \
  https://api.github.com/repos/<OWNER>/<REPO>/branches/master/protection \
  -d @branch-protection-payload.json
```

## Example (gh cli)

Pass the payload file with --input:

```bash
gh api -X PUT repos/<OWNER>/<REPO>/branches/master/protection --input branch-protection-payload.json
```

Notes:
- Replace `<OWNER>/<REPO>` with `arnokamphuis/aiact_gdpr_documentation_help` or your repository path.
- If you want to require status checks, replace `"required_status_checks": null` in the JSON with an object such as `{"strict": true, "contexts": ["ci/test"]}`.
- These commands don't commit anything; they call the GitHub API to change protection settings. Make sure the token you use has appropriate repo-level/admin scopes and you have admin rights on the repository.
