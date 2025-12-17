# Dependency Security Audit

1. Analyze project dependencies:
   - Check package.json and requirements.txt files
   - List all dependencies with versions
   - Identify outdated packages

2. Security check:
   - Run npm audit (for JavaScript packages)
   - Check for known vulnerabilities in Python packages
   - Identify dependencies with critical security issues

3. Create an upgrade plan:
   - List packages requiring immediate updates
   - Note breaking changes in latest versions
   - Estimate impact of required updates

Save findings in 'security_audit.md' with severity levels highlighted.