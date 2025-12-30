---
layout: default
title: Organization & Enterprise Best Practices
---

Best practices for managing GitHub at organizational and enterprise scale, covering governance, security, compliance, and operational excellence.

---

## Organization-Level Best Practices

### Organization Setup & Governance

#### Organization Structure

```
Enterprise
├── Organization 1 (Product Team)
│   ├── Team: Frontend
│   ├── Team: Backend
│   ├── Team: DevOps
│   └── Repositories (50+)
├── Organization 2 (Platform Team)
│   ├── Team: Infrastructure
│   ├── Team: Security
│   └── Repositories (30+)
└── Organization 3 (Data Team)
    ├── Team: Analytics
    ├── Team: ML Engineering
    └── Repositories (20+)
```

#### Organization Settings

**Essential configurations:**
- Enable two-factor authentication requirement
- Set base repository permissions (read/write/admin)
- Configure default branch protection rules
- Enable Dependabot alerts and security updates
- Set up organization-wide webhooks
- Configure OAuth app access restrictions

### Team Management

#### Team Structure Best Practices

**Team hierarchy:**
```
@company/engineering
├── @company/frontend-team
│   ├── @company/react-specialists
│   └── @company/vue-specialists
├── @company/backend-team
│   ├── @company/api-team
│   └── @company/database-team
└── @company/platform-team
    ├── @company/devops
    └── @company/security
```

**Team permissions:**
- **Read**: View and clone repositories
- **Triage**: Manage issues and PRs without write access
- **Write**: Push to repositories and manage issues/PRs
- **Maintain**: Manage repositories without destructive actions
- **Admin**: Full administrative access

#### CODEOWNERS Strategy

Implement organization-wide code ownership:

```
# Global organizational rules
* @company/engineering

# Platform and infrastructure
/.github/ @company/platform-team @company/security
/infrastructure/ @company/devops
/terraform/ @company/devops
/kubernetes/ @company/devops

# Application code
/frontend/ @company/frontend-team
/backend/ @company/backend-team
/api/ @company/api-team

# Security-sensitive files
/security/ @company/security
*.pem @company/security
*.key @company/security
/secrets/ @company/security

# Documentation
/docs/ @company/docs-team
*.md @company/docs-team

# Database schemas
/migrations/ @company/database-team
/schema/ @company/database-team
```

### Repository Standards

#### Repository Naming Conventions

```
# Microservices
service-user-management
service-payment-processing
service-notification

# Libraries
lib-authentication
lib-logging
lib-utilities

# Infrastructure
infra-terraform-aws
infra-kubernetes-configs
infra-monitoring

# Applications
app-customer-portal
app-admin-dashboard
app-mobile-ios
```

#### Required Repository Files

All repositories must include:
- `README.md` - Project overview and setup
- `LICENSE` - License information
- `CONTRIBUTING.md` - Contribution guidelines
- `CODE_OF_CONDUCT.md` - Community standards
- `SECURITY.md` - Security policy
- `.github/CODEOWNERS` - Code ownership
- `.github/pull_request_template.md` - PR template
- `.github/ISSUE_TEMPLATE/` - Issue templates

#### Repository Templates

Create organization templates for:
- Microservice projects
- Library/package projects
- Infrastructure projects
- Documentation sites
- Mobile applications

### Branch Protection & Policies

#### Standard Branch Protection Rules

**For `main` branch:**
```
✓ Require pull request reviews (minimum 2)
✓ Dismiss stale reviews when new commits are pushed
✓ Require review from code owners
✓ Require status checks to pass before merging
  - Build/CI
  - Unit tests
  - Integration tests
  - Security scan
  - Code coverage (minimum 80%)
✓ Require branches to be up to date before merging
✓ Require conversation resolution before merging
✓ Require signed commits
✓ Require linear history
✓ Include administrators in restrictions
✓ Restrict who can push to matching branches
✓ Allow force pushes: Never
✓ Allow deletions: Never
```

**For `develop` branch:**
```
✓ Require pull request reviews (minimum 1)
✓ Require status checks to pass
✓ Require branches to be up to date
```

**For `release/*` branches:**
```
✓ Require pull request reviews (minimum 2)
✓ Require review from release managers
✓ Lock branch after release
✓ Require signed commits
```

### Security & Compliance

#### Security Policies

**Organization-wide security requirements:**
1. **Dependency Management**
   - Enable Dependabot security updates
   - Require approval for dependency updates
   - Regular security audits (weekly)
   - No known vulnerabilities in production

2. **Secret Management**
   - Never commit secrets to repositories
   - Use GitHub Secrets for CI/CD
   - Rotate secrets quarterly
   - Enable secret scanning
   - Use tools like GitGuardian or TruffleHog

3. **Access Control**
   - Enforce 2FA for all organization members
   - Regular access reviews (quarterly)
   - Remove inactive users (90 days)
   - Use teams for permissions, not individuals
   - Principle of least privilege

4. **Code Scanning**
   - Enable CodeQL or similar SAST tools
   - Require security scans in CI/CD
   - Address critical/high findings before merge
   - Regular penetration testing

#### Compliance Standards

**Audit trails:**
```yaml
# Required audit logging
- Repository access changes
- Team membership changes
- Branch protection modifications
- Secret access
- Deploy events
- Admin actions
```

**Data retention policies:**
- Retain git history: Indefinite
- Retain audit logs: 2 years minimum
- Retain CI/CD logs: 90 days
- Retain security scan results: 1 year

### CI/CD Standards

#### Organization-Wide CI/CD Pipeline

**Standard pipeline stages:**
```yaml
name: Organization CI/CD Pipeline

on:
  pull_request:
  push:
    branches: [main, develop]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run linting
        run: npm run lint

  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run security scan
        uses: securego/gosec@master
      - name: Dependency check
        run: npm audit

  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: npm test
      - name: Upload coverage
        uses: codecov/codecov-action@v3

  build:
    needs: [lint, security-scan, test]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build application
        run: npm run build
      
  deploy-staging:
    if: github.ref == 'refs/heads/develop'
    needs: build
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - name: Deploy to staging
        run: ./deploy-staging.sh

  deploy-production:
    if: github.ref == 'refs/heads/main'
    needs: build
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Deploy to production
        run: ./deploy-production.sh
```

---

## Enterprise-Level Best Practices

### Enterprise Architecture

#### Multi-Organization Strategy

**Organization segmentation:**
- **By product line**: Separate orgs for different products
- **By business unit**: Marketing, Engineering, Data, etc.
- **By environment**: Production, Staging, Development
- **By compliance**: SOC2, HIPAA, PCI-DSS specific orgs

#### Enterprise Management Console

**Centralized management of:**
- Organization policies
- User provisioning and de-provisioning
- License management
- Security and compliance monitoring
- Billing and cost allocation
- Audit logging

### Identity & Access Management

#### SSO Integration

```yaml
# SAML Configuration
Enterprise SSO Setup:
  Identity Provider: Okta/Azure AD/Google Workspace
  Attributes Mapping:
    - email → email
    - displayName → full_name
    - department → team
    - role → github_role
  
  Just-in-Time Provisioning: Enabled
  SCIM Provisioning: Enabled
  Session Timeout: 8 hours
  Require Re-authentication: For sensitive operations
```

#### Role-Based Access Control (RBAC)

**Enterprise roles:**
```
Enterprise Owner
├── Organization Owner
│   ├── Repository Admin
│   ├── Team Maintainer
│   └── Member
└── Billing Manager

Security Manager (Across all orgs)
└── Security Analyst (Read-only)

Compliance Officer (Audit access)
└── Compliance Analyst (Read-only)
```

### Enterprise Security

#### Security Policies Enforcement

**Mandatory enterprise policies:**
1. **Repository Security**
   - Private by default
   - Required branch protection on all repos
   - Mandatory code review (2+ reviewers)
   - Signed commits required
   - No force push to protected branches

2. **Secrets Management**
   - Enterprise-wide secret scanning
   - Integration with HashiCorp Vault/AWS Secrets Manager
   - Automatic secret rotation
   - Secret access auditing

3. **Vulnerability Management**
   - Automated dependency scanning
   - CVE monitoring and alerting
   - SLA for vulnerability remediation:
     - Critical: 24 hours
     - High: 7 days
     - Medium: 30 days
     - Low: 90 days

4. **Third-party Access**
   - Whitelist approved OAuth apps
   - Regular review of external collaborators
   - Time-limited access for contractors
   - Separate organizations for third-party development

#### Compliance & Governance

**Regulatory compliance:**
```
SOC 2 Compliance:
  - Access control auditing
  - Change management tracking
  - Incident response procedures
  - Data encryption in transit and at rest

GDPR Compliance:
  - Data retention policies
  - Right to be forgotten procedures
  - Data export capabilities
  - Privacy impact assessments

HIPAA Compliance (if applicable):
  - PHI data handling procedures
  - Audit logging requirements
  - Access controls for PHI
  - Business associate agreements
```

### Enterprise Workflows

#### Inner Source Programs

**Encourage collaboration across the enterprise:**
```
Inner Source Best Practices:
  - Discoverable repositories (internal marketplace)
  - Clear contribution guidelines
  - Designated maintainer teams
  - Recognition programs for contributors
  - Regular inner source events/hackathons
  - Metrics tracking (contributions, adoption)
```

#### Release Management

**Enterprise release strategy:**
```
Release Process:
  1. Feature Development (feature/* branches)
  2. Integration Testing (develop branch)
  3. Release Candidate (release/* branch)
  4. UAT/Staging Deployment
  5. Production Deployment (main branch)
  6. Post-deployment Monitoring
  
Release Cadence:
  - Major releases: Quarterly
  - Minor releases: Monthly
  - Patch releases: As needed
  - Emergency hotfixes: < 2 hours

Change Advisory Board (CAB):
  - Review all production changes
  - Assess risk and impact
  - Approve/reject deployments
  - Schedule maintenance windows
```

### Enterprise Monitoring & Analytics

#### Metrics & KPIs

**Track organization health:**
```
Code Quality Metrics:
  - Code coverage: >80%
  - Technical debt ratio: <5%
  - Code duplication: <3%
  - Cyclomatic complexity: <10

Collaboration Metrics:
  - PR merge time: <24 hours
  - Review response time: <4 hours
  - Code review participation: >70%
  - Cross-team contributions: Monitor trends

Security Metrics:
  - Time to patch vulnerabilities
  - Number of exposed secrets (target: 0)
  - Security scan coverage: 100%
  - Incident response time

Productivity Metrics:
  - Deployment frequency
  - Lead time for changes
  - Mean time to recovery (MTTR)
  - Change failure rate
```

#### Centralized Logging & Monitoring

**Enterprise observability:**
```yaml
Logging Strategy:
  Audit Logs:
    - Retention: 7 years
    - Export to SIEM: Real-time
    - Monitoring: 24/7
  
  Application Logs:
    - Centralized: ELK Stack/Splunk
    - Retention: 90 days
    - Search and analysis capabilities
  
  Security Events:
    - Real-time alerting
    - Automated response workflows
    - Integration with SOAR platforms
```

### Cost Management

#### License Optimization

**Manage enterprise licenses efficiently:**
- Regular audits of active users
- Reclaim licenses from inactive users (30-day threshold)
- Right-size teams (convert members to outside collaborators)
- Use organization insights for usage analytics

#### Resource Allocation

```
Cost Allocation:
  - Tag repositories by project/team
  - Track Actions minutes by team
  - Monitor storage usage
  - Allocate costs via chargeback model
  - Set budgets and alerts
```

### Disaster Recovery & Business Continuity

#### Backup Strategy

**Enterprise backup requirements:**
```bash
# Repository backups
Frequency: Daily
Retention: 30 days (incremental), 1 year (full)
Storage: Geographic redundancy
Testing: Quarterly restore tests

# Organization settings backup
Frequency: Weekly
Includes:
  - Team structure
  - Permissions
  - Branch protection rules
  - Webhooks and integrations
  - Organization policies
```

#### Disaster Recovery Plan

**Recovery time objectives (RTO):**
- Critical repositories: < 1 hour
- Standard repositories: < 4 hours
- Documentation: < 24 hours

**Recovery point objectives (RPO):**
- Critical data: < 15 minutes
- Standard data: < 1 hour

### Training & Onboarding

#### Enterprise Training Program

**Required training for all developers:**
1. Git and GitHub fundamentals (4 hours)
2. Security best practices (2 hours)
3. Compliance requirements (2 hours)
4. Organization-specific workflows (2 hours)
5. Tool and automation training (4 hours)

**Continuous learning:**
- Monthly tech talks
- Quarterly security awareness training
- Annual compliance recertification
- Access to GitHub Learning Lab
- Conference sponsorships

#### Onboarding Checklist

```markdown
New Developer Onboarding:
- [ ] GitHub Enterprise account created
- [ ] SSO/2FA configured
- [ ] Added to appropriate teams
- [ ] Access to required repositories granted
- [ ] Training modules completed
- [ ] Development environment setup verified
- [ ] First PR submitted and reviewed
- [ ] Security and compliance attestation signed
```

### Next Steps

- Review [Repository Best Practices]({{ '/docs/repository-best-practices' | relative_url }})
- Explore [Collaboration]({{ '/docs/collaboration' | relative_url }})
- Implement [Branch Protection Strategies]({{ '/docs/branching-merging' | relative_url }})
