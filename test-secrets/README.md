# Test Secrets for Gitleaks Action

This directory contains **fake credentials** intentionally added to test the Gitleaks action's secret detection capabilities.

## ⚠️ IMPORTANT

**All secrets in this directory are FAKE and for testing purposes only!**

- ❌ These are NOT real credentials
- ❌ Do NOT use these in production
- ✅ Safe to commit for testing secret scanning

## Test Files

### `sample-config.yml`

Contains various types of fake secrets to test detection:

1. **AWS Credentials**
   - Fake AWS Access Key ID: `AKIAIOSFODNN7EXAMPLE`
   - Fake AWS Secret Access Key: `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`

2. **GitHub Token**
   - Fake GitHub Personal Access Token: `ghp_1234567890abcdefghijklmnopqrstuvwxyz12`

3. **Slack Webhook**
   - Fake Slack webhook URL

4. **JWT Secret**
   - Fake JWT signing key

5. **Private Key**
   - Fake RSA private key

## Testing the Gitleaks Action

To test the action:

1. **Manual Trigger**:
   - Go to Actions → `action-gitleaks` workflow
   - Click "Run workflow"
   - Specify the branch/tag to test (default: `release`)

2. **Pull Request**:
   - Create a PR that modifies files in `test-secrets/` directory
   - The workflow will automatically run

3. **Expected Behavior**:
   - ✅ Gitleaks should detect multiple secrets
   - ✅ Job should fail with exit code 1
   - ✅ Summary should show all detected secrets
   - ✅ Artifacts should contain SARIF results

## Suppressing False Positives

To suppress these test secrets, add their fingerprints to `.gitleaksignore`:

```bash
# Get fingerprints from the Gitleaks output or job summary
commit:file:rule:line
```

Or create a custom `.gitleaks.toml` configuration to exclude the `test-secrets/` directory:

```toml
[allowlist]
paths = [
  '''test-secrets/.*'''
]
```
