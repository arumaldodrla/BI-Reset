# Contributing to BI Reset

Thank you for your interest in contributing to BI Reset! This document provides guidelines for both AI development agents and human contributors.

## Development Model

BI Reset is developed **100% by AI agents** using frameworks like Google Antigravity, supervised by human project managers. All development tasks are assigned through GitHub Issues and completed via Pull Requests.

## For AI Development Agents

### Workflow

1. **Receive Assignment**: A human supervisor will assign you a task by creating a GitHub Issue with detailed specifications.
2. **Review Documentation**: Read the relevant specification documents in the `6_ai_agent_development/` directory.
3. **Implement**: Write clean, well-documented code that strictly follows the specifications.
4. **Test**: Ensure all unit tests and integration tests pass before submitting.
5. **Submit PR**: Create a Pull Request with a clear description linking to the original issue.
6. **Iterate**: Address any feedback from human reviewers.

### Code Standards

- **Language**: TypeScript for backend and frontend
- **Testing**: Minimum 80% code coverage
- **Documentation**: All functions must have JSDoc comments
- **Commits**: Use conventional commit messages (e.g., `feat:`, `fix:`, `docs:`)

### Required Checks

Before submitting a PR, ensure:

- [ ] All tests pass (`npm test`)
- [ ] Code is formatted (`npm run format`)
- [ ] Linting passes (`npm run lint`)
- [ ] Build succeeds (`npm run build`)

## For Human Supervisors

### Reviewing PRs

1. Verify that the implementation matches the specification
2. Check test coverage and quality
3. Run the code locally to verify functionality
4. Provide clear, actionable feedback if changes are needed
5. Approve and merge when all criteria are met

### Creating Issues for AI Agents

When creating a task for an AI agent, include:

- **Clear Objective**: What needs to be built
- **Specification Link**: Reference to the relevant doc in `6_ai_agent_development/`
- **Acceptance Criteria**: Specific, testable requirements
- **Context**: Any additional information the agent needs

## Branch Strategy

- `main`: Production-ready code
- `develop`: Integration branch for completed features
- `feature/*`: Individual feature branches created by AI agents

## Questions?

If you have questions about contributing, please create a GitHub Issue with the `question` label.
