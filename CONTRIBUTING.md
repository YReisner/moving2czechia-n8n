# Contributing

Thanks for your interest in contributing! Whether it's a bug fix, a new workflow, or an improvement to an existing one — all contributions are welcome.

## How to contribute a new workflow

1. **Fork** this repository
2. **Export** your workflow from n8n as JSON (**Workflow** > **Download**)
3. **Clean up** the export:
   - Remove any hardcoded API keys, emails, or personal data
   - Set sensitive parameter values to `null` or empty strings
   - Give your nodes clear, descriptive names
4. **Add the file** to the `workflows/` directory with a descriptive, lowercase, hyphenated name and a `.json` extension (e.g. `workflows/bus-schedule-checker.json`)
5. **Update the README** with a section describing your workflow, its prerequisites, and setup instructions
6. **Open a pull request** with a clear description of what the workflow does

## How to report a bug or suggest a feature

- Open an [issue](https://github.com/YReisner/moving2czechia-n8n/issues) using the provided templates
- Be as specific as possible — include your n8n version, error messages, and steps to reproduce

## Guidelines

- Keep workflows focused on a single purpose
- Use the **"Set Parameters"** pattern (a single node with all user-configurable values) so users only need to edit one place
- Don't commit API keys, tokens, or personal information
- Test your workflow before submitting

## Questions?

Open an issue and we'll be happy to help.
