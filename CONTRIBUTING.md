# Contributing to Awesome C2PA

Thank you for your interest in contributing to Awesome C2PA! This document provides guidelines for contributing to this project.

## 🌟 Ways to Contribute

There are several ways you can contribute:

1. **Add new resources** (tools, libraries, articles, tutorials)
2. **Translate specifications** to new languages
3. **Improve translations** (fix errors, improve clarity)
4. **Fix broken links** or update outdated information
5. **Enhance descriptions** of existing resources
6. **Report issues** or suggest improvements
7. **Share your C2PA use cases** or demos

## 📋 Before You Contribute

### Check Existing Content

Before submitting a new resource:
- Search the README to ensure it's not already listed
- Check open [pull requests](../../pulls) and [issues](../../issues) to avoid duplicates
- Review our [quality standards](#quality-standards) below

### Quality Standards

We only accept resources that meet these criteria:

#### For Tools & Libraries
- ✅ **Active maintenance**: Updated within the last 12 months
- ✅ **Documentation**: Has clear README and usage instructions
- ✅ **Relevance**: Directly related to C2PA implementation or usage
- ✅ **Open source or freely accessible**: Preference for open source projects
- ✅ **Working**: Actually functional and tested

#### For Articles & Tutorials
- ✅ **Accuracy**: Technically accurate information about C2PA
- ✅ **Quality**: Well-written and clear
- ✅ **Relevance**: Provides value to C2PA developers or users
- ✅ **Accessible**: Publicly available (not behind a paywall)

#### For Translations
- ✅ **Completeness**: Entire document translated, not partial
- ✅ **Accuracy**: Technically correct terminology
- ✅ **Native speaker**: Reviewed by at least one native speaker
- ✅ **Formatting**: Preserves original document structure

## 🔧 How to Contribute

### Adding a New Resource

1. **Fork the repository**
   ```bash
   # Click the "Fork" button on GitHub, then:
   git clone https://github.com/paulortiz199928/awesome-c2pa.git
   cd awesome-c2pa
   ```

2. **Create a new branch**
   ```bash
   git checkout -b add-resource-name
   ```

3. **Add your resource**
   - Find the appropriate section in `README.md`
   - Add your resource in alphabetical order within that section
   - Follow this format:
     ```markdown
     - [Resource Name](https://url.com) - Brief description (1-2 sentences) highlighting what makes it useful
     ```

4. **Commit your changes**
   ```bash
   git add README.md
   git commit -m "Add [Resource Name] to [Section Name]"
   ```

5. **Push and create a Pull Request**
   ```bash
   git push origin add-resource-name
   ```
   Then open a Pull Request on GitHub with:
   - Clear title: "Add [Resource Name]"
   - Description explaining why this resource is valuable

### Translating Specifications

We welcome translations of the C2PA specification to new languages!

#### Before Starting

1. **Check for existing work**
   - Look at [issues](../../issues) with the `translation` label
   - Someone may already be working on your target language

2. **Announce your intent**
   - Open an issue titled: "Translation: [Language] specification"
   - This prevents duplicate work

#### Translation Process

1. **Download the original**
   - Get the [official English PDF](doc/C2PA_Specification.pdf)

2. **Create your translation**
   - Maintain technical accuracy
   - Use consistent terminology (create a glossary if needed)
   - Preserve all diagrams, tables, and code examples
   - Keep the document structure identical
   - Add a translation note on the title page

3. **Quality assurance**
   - Have at least one other native speaker review it
   - Check for technical accuracy with someone familiar with C2PA
   - Verify all terms are consistently translated

4. **Submit your translation**
   - Name the file: `C2PA_Specification [language-code].pdf`
     - Examples: `C2PA_Specification fr.pdf`, `C2PA_Specification ko.pdf`
   - Place it in the `doc/` directory
   - Update `README.md` and `doc/README.md` with the new language
   - Create a Pull Request with:
     - Title: "Add [Language] translation of C2PA specification"
     - Description: Translation method, reviewers, any notes

#### Language Codes

Use ISO 639-1 codes (or ISO 639-3 if needed):
- `fr` - French
- `es` - Spanish
- `ko` - Korean
- `pt` - Portuguese
- `zh-Hans` - Simplified Chinese (already done ✅)
- `zh-Hant` - Traditional Chinese
- `ja` - Japanese (already done ✅)
- `de` - German (already done ✅)

### Fixing Translation Errors

**Note**: All current translations are AI-assisted (DeepL) and in beta status. We actively welcome corrections!

Found an error in an existing translation?

1. **Document the error**
   - Open an issue with:
     - Language and page number
     - Current (incorrect) text
     - Suggested correction
     - Explanation of why it's incorrect

2. **Or submit a fix directly**
   - Fork, fix, and submit a PR
   - Include justification for the change

3. **Review priorities**
   - See [Translation Quality Guide](TRANSLATION_QUALITY.md) for high-priority areas
   - Focus on technical terminology consistency
   - Even small corrections are valuable!

### Improving Existing Content

To improve descriptions or fix broken links:

1. Fork and create a branch
2. Make your improvements
3. Commit with a descriptive message
4. Submit a Pull Request explaining the improvements

## ✍️ Style Guidelines

### Writing Descriptions

When adding resources, write clear, concise descriptions:

**Good:**
```markdown
- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - Official Rust SDK for creating and validating C2PA manifests. The reference implementation.
```

**Not ideal:**
```markdown
- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - A Rust library
```

### Guidelines:
- Start with what the resource **is** (library, tool, tutorial, etc.)
- Explain what makes it **useful** or **unique**
- Keep it to 1-2 sentences
- Use proper grammar and punctuation
- Don't use marketing language or excessive praise

### Markdown Formatting

- Use consistent heading levels
- Maintain alphabetical order within sections (unless there's a clear hierarchy)
- Use proper link formatting: `[Text](URL)`
- Don't use trailing punctuation in list items (no periods at the end)

## 🚫 What NOT to Include

Please don't submit:
- **Unrelated content**: Must be directly related to C2PA
- **Spam or low-quality links**: Obvious link farms or SEO spam
- **Inactive projects**: Not updated in over 2 years without explicit notice
- **Duplicates**: Already listed resources
- **Self-promotion without value**: Your project must meet quality standards

## 🔍 Review Process

After you submit a Pull Request:

1. **Automated checks**: Links will be validated automatically
2. **Maintainer review**: A maintainer will review within 1-7 days
3. **Feedback**: You may receive requests for changes
4. **Merge**: Once approved, your contribution will be merged

### What We Look For

- Does it meet our quality standards?
- Is it in the right section?
- Is the description clear and helpful?
- Is the formatting consistent?
- Does it add value to the list?

## 📬 Questions?

If you have questions about contributing:

- **Open an issue**: Use the [question template](../../issues/new)
- **Start a discussion**: Use [GitHub Discussions](../../discussions)
- **Check existing issues**: Your question may already be answered

## 🙏 Recognition

All contributors are valued! Your contributions will be:
- Listed in the Git history
- Recognized in [pull requests](../../pulls?q=is%3Apr+is%3Aclosed)
- Appreciated by the C2PA community

For significant contributions (translations, major additions), we may add you to an acknowledgments section.

## 📜 License

By contributing, you agree that your contributions will be licensed under the CC0 1.0 Universal license (same as the project).

---

**Thank you for helping make C2PA accessible to everyone!** 🌍

**[← Back to README](README.md)**
