# Contributing to AWS CLI Guide

First off, thank you for considering contributing to this project! 🎉

## How Can I Contribute?

### 🐛 Reporting Bugs

If you find an error in any command:

1. Check if the issue already exists in [Issues](https://github.com/your-username/aws-cli-guide/issues)
2. If not, create a new issue with:
   - The command that has the error
   - Expected behavior
   - Actual behavior
   - AWS CLI version (`aws --version`)

### 💡 Suggesting New Commands

Have a useful command that's not in the guide?

1. Open an issue with the label `enhancement`
2. Include:
   - The command
   - What service it belongs to
   - A brief description of what it does
   - Why it's useful

### 📝 Improving Documentation

- Fix typos
- Improve descriptions
- Add examples
- Translate to other languages

### 🔀 Pull Requests

1. Fork the repository
2. Create a new branch (`git checkout -b feature/new-command`)
3. Make your changes
4. Commit with a descriptive message (`git commit -m 'Add: EKS commands section'`)
5. Push to your branch (`git push origin feature/new-command`)
6. Open a Pull Request

## Style Guide

### Commands Format

When adding new commands, follow this format:

```markdown
### Service Name

```bash
# Description of what the command does
aws service-name action --parameter value
```
```

### Commit Messages

Use these prefixes:
- `Add:` for new content
- `Fix:` for bug fixes
- `Update:` for updates to existing content
- `Docs:` for documentation changes
- `Translate:` for translations

## Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Help others learn

## Questions?

Feel free to open an issue with the label `question`.

---

Thank you for contributing! 🚀
