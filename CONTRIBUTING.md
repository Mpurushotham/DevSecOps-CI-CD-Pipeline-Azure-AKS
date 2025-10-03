# Contributing to Azure DevSecOps Pipeline

First off, thank you for considering contributing to this project! It's people like you that make this pipeline better for everyone.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Security](#security)

## 📜 Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

## 🤝 How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the existing issues to avoid duplicates. When you create a bug report, include as many details as possible:

**Bug Report Template:**

```markdown
**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '...'
3. See error

**Expected behavior**
What you expected to happen.

**Screenshots**
If applicable, add screenshots.

**Environment:**
 - OS: [e.g. Ubuntu 22.04]
 - Azure CLI Version: [e.g. 2.50.0]
 - Kubernetes Version: [e.g. 1.28.3]
 - Pipeline Version: [e.g. 2.0]

**Additional context**
Add any other context about the problem.
```

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:

- **Use a clear and descriptive title**
- **Provide a detailed description** of the suggested enhancement
- **Explain why this enhancement would be useful**
- **List any alternatives** you've considered

### Your First Code Contribution

Unsure where to begin? Look for issues tagged with:
- `good-first-issue` - Good for newcomers
- `help-wanted` - Issues that need assistance
- `documentation` - Documentation improvements

## 🔧 Development Setup

### Prerequisites

- Azure subscription
- Azure CLI installed
- kubectl installed
- Docker Desktop
- Node.js 18 LTS
- Terraform 1.6+
- Git

### Local Development Environment

1. **Fork and clone the repository**

```bash
git clone https://github.com/your-username/azure-devsecops-pipeline.git
cd azure-devsecops-pipeline
```

2. **Install dependencies**

```bash
# Frontend
cd src/frontend
npm install

# Backend
cd ../backend
npm install
```

3. **Set up environment variables**

```bash
# Frontend
cp src/frontend/.env.example src/frontend/.env

# Backend
cp src/backend/.env.example src/backend/.env
```

4. **Start local development**

```bash
# Frontend
cd src/frontend
npm start

# Backend (separate terminal)
cd src/backend
npm run dev
```

5. **Run tests**

```bash
# Frontend tests
cd src/frontend
npm test

# Backend tests
cd src/backend
npm test
```

### Docker Development

```bash
# Build images locally
docker build -t ecommerce-frontend:dev src/frontend
docker build -t ecommerce-backend:dev src/backend

# Run with docker-compose
docker-compose -f docker-compose.dev.yml up
```

## 🔀 Pull Request Process

### 1. Create a Branch

```bash
# Update main branch
git checkout main
git pull origin main

# Create feature branch
git checkout -b feature/your-feature-name
# or
git checkout -b fix/your-bug-fix
```

### Branch Naming Convention

- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation changes
- `refactor/` - Code refactoring
- `test/` - Adding or updating tests
- `chore/` - Maintenance tasks

### 2. Make Your Changes

- Write clean, readable code
- Follow the existing code style
- Add tests for new functionality
- Update documentation as needed

### 3. Commit Your Changes

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```bash
# Format: <type>(<scope>): <subject>

git commit -m "feat(backend): add user authentication endpoint"
git commit -m "fix(frontend): resolve navigation bug"
git commit -m "docs(readme): update installation instructions"
```

**Commit Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks
- `perf`: Performance improvements
- `ci`: CI/CD changes
- `build`: Build system changes

### 4. Push Your Changes

```bash
git push origin feature/your-feature-name
```

### 5. Create Pull Request

1. Go to the repository on GitHub
2. Click "Pull Request"
3. Select your branch
4. Fill out the PR template
5. Link any related issues

**PR Title Format:**
```
<type>(<scope>): <description>

Example:
feat(security): add Trivy container scanning
fix(pipeline): resolve database migration issue
```

**PR Description Template:**

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update

## Testing
- [ ] Unit tests pass locally
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review of my code
- [ ] I have commented my code where necessary
- [ ] I have updated the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally
- [ ] Any dependent changes have been merged

## Screenshots (if applicable)
Add screenshots to help explain your changes

## Related Issues
Closes #(issue number)
```

### 6. Code Review Process

- At least one approval required
- All CI checks must pass
- No merge conflicts
- Documentation updated
- Tests passing

### 7. After Merge

```bash
# Update your local main branch
git checkout main
git pull origin main

# Delete feature branch
git branch -d feature/your-feature-name
git push origin --delete feature/your-feature-name
```

## 📝 Coding Standards

### General Guidelines

- **Keep it simple** - Simple code is easier to maintain
- **DRY principle** - Don't Repeat Yourself
- **SOLID principles** - Follow object-oriented design principles
- **Comments** - Comment complex logic, not obvious code
- **Naming** - Use descriptive names for variables and functions

### JavaScript/Node.js Standards

```javascript
// Use const/let, never var
const apiUrl = 'https://api.example.com';
let counter = 0;

// Use arrow functions for callbacks
const users = data.map(user => user.name);

// Use async/await instead of callbacks
async function fetchData() {
  try {
    const response = await fetch(apiUrl);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching data:', error);
    throw error;
  }
}

// Use template literals
const message = `Hello, ${username}!`;

// Use destructuring
const { id, name, email } = user;
```

### React Standards

```javascript
// Use functional components with hooks
import React, { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetchUser(userId).then(data => {
      setUser(data);
      setLoading(false);
    });
  }, [userId]);

  if (loading) return <Loading />;
  if (!user) return <NotFound />;

  return <div>{user.name}</div>;
}

export default UserProfile;
```

### YAML/Pipeline Standards

```yaml
# Use meaningful names
- stage: SecurityScanning
  displayName: 'Security Scanning and Analysis'
  
# Group related tasks
- job: ContainerSecurity
  steps:
  - task: Docker@2
    displayName: 'Build Container Image'
  - task: CmdLine@2
    displayName: 'Scan with Trivy'

# Use variables for reusability
variables:
  imageName: 'ecommerce-backend'
  imageTag: '$(Build.BuildId)'
  
# Comment complex logic
# This task scans the container for vulnerabilities
# and fails the build if critical issues are found
```

### Kubernetes Manifests

```yaml
# Always specify resource limits
resources:
  requests:
    memory: "256Mi"
    cpu: "250m"
  limits:
    memory: "512Mi"
    cpu: "1000m"

# Use labels consistently
metadata:
  labels:
    app: backend
    tier: application
    version: blue
    environment: production

# Security context should be explicit
securityContext:
  runAsNonRoot: true
  runAsUser: 1001
  allowPrivilegeEscalation: false
  readOnlyRootFilesystem: true
```

### Terraform Standards

```hcl
# Use meaningful resource names
resource "azurerm_kubernetes_cluster" "main" {
  name                = "aks-${var.project}-${var.environment}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  
  # Use variables for configurability
  kubernetes_version  = var.kubernetes_version
  
  # Always add tags
  tags = {
    Environment = var.environment
    ManagedBy   = "Terraform"
    Project     = var.project
  }
}

# Use modules for reusability
module "networking" {
  source = "./modules/networking"
  
  resource_group_name = azurerm_resource_group.main.name
  location            = var.location
  address_space       = var.vnet_address_space
}

# Document complex resources
# This creates the AKS cluster with:
# - System node pool for system workloads
# - User node pool for application workloads
# - Azure CNI networking
# - Calico network policies
```

## 🧪 Testing Guidelines

### Unit Tests

- Write tests for all new functions
- Aim for >80% code coverage
- Test edge cases and error scenarios

```javascript
// Example: Jest test
describe('UserService', () => {
  describe('createUser', () => {
    it('should create a user with valid data', async () => {
      const userData = {
        name: 'John Doe',
        email: 'john@example.com'
      };
      
      const user = await UserService.createUser(userData);
      
      expect(user).toBeDefined();
      expect(user.email).toBe(userData.email);
    });
    
    it('should throw error with invalid email', async () => {
      const userData = {
        name: 'John Doe',
        email: 'invalid-email'
      };
      
      await expect(UserService.createUser(userData))
        .rejects.toThrow('Invalid email format');
    });
  });
});
```

### Integration Tests

- Test API endpoints
- Test database interactions
- Use test databases, not production

### E2E Tests

- Test critical user flows
- Use Playwright or Cypress
- Keep tests maintainable

### Running Tests

```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Run specific test file
npm test -- UserService.test.js

# Run in watch mode
npm test -- --watch
```

## 📚 Documentation

### Code Documentation

- Document complex algorithms
- Explain "why", not just "what"
- Keep documentation up to date

### README Updates

When adding new features, update:
- Feature list
- Installation instructions
- Usage examples
- Configuration options

### API Documentation

Document all API endpoints:

```javascript
/**
 * Get user by ID
 * 
 * @route GET /api/users/:id
 * @param {string} id - User ID
 * @returns {Object} User object
 * @throws {404} User not found
 * @throws {500} Server error
 * 
 * @example
 * GET /api/users/123
 * Response: { id: "123", name: "John Doe", email: "john@example.com" }
 */
router.get('/users/:id', async (req, res) => {
  // Implementation
});
```

### Architecture Decisions

Document significant decisions in `docs/decisions/`:

```markdown
# ADR-001: Use Blue-Green Deployment Strategy

## Status
Accepted

## Context
We need a deployment strategy that allows zero-downtime deployments with fast rollback capability.

## Decision
We will use blue-green deployment strategy for production deployments.

## Consequences
### Positive
- Zero downtime during deployments
- Instant rollback capability
- Full testing before traffic switch

### Negative
- Requires double resources during deployment
- More complex than rolling updates
```

## 🔒 Security

### Security Considerations

- **Never commit secrets** - Use Azure Key Vault
- **Validate inputs** - Prevent injection attacks
- **Use parameterized queries** - Prevent SQL injection
- **Implement rate limiting** - Prevent DoS attacks
- **Keep dependencies updated** - Patch vulnerabilities

### Security Checklist

Before submitting a PR:

- [ ] No secrets in code or config
- [ ] Dependencies are up to date
- [ ] Security scans pass
- [ ] Input validation implemented
- [ ] Authentication/authorization tested
- [ ] Error messages don't expose sensitive info

### Reporting Security Vulnerabilities

**DO NOT** create a public issue for security vulnerabilities.

Instead, email: security@company.com

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)

## 🎯 Review Process

### What Reviewers Look For

1. **Functionality** - Does it work as expected?
2. **Code Quality** - Is it clean and maintainable?
3. **Tests** - Are there adequate tests?
4. **Documentation** - Is it documented?
5. **Security** - Are there security concerns?
6. **Performance** - Is it performant?

### Reviewer Guidelines

- Be respectful and constructive
- Explain your suggestions
- Approve when ready, request changes if needed
- Don't approve your own PRs

## 🏆 Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Invited to join the community

## 📞 Questions?

- Check existing [Issues](https://github.com/your-org/azure-devsecops-pipeline/issues)
- Join our [Discussions](https://github.com/your-org/azure-devsecops-pipeline/discussions)
- Email: devops@company.com

---

Thank you for contributing! 🎉
