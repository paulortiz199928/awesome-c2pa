# Translation Quality & Improvement Guide

## 🎯 Current Translation Status

All non-English C2PA specification translations in this repository are:
- **Method**: AI-assisted translation using DeepL
- **Status**: Beta / Community Review Phase
- **Quality**: Good for general understanding, may contain technical inaccuracies

## 📊 Known Limitations

### What AI Translation Does Well
- ✅ General meaning and document structure
- ✅ Common technical vocabulary
- ✅ Grammar and sentence flow
- ✅ Consistency in style

### Where AI Translation Struggles
- ⚠️ **Domain-specific terminology**: Terms like "manifest", "assertion", "claim" may have multiple meanings
- ⚠️ **Context sensitivity**: Same word may need different translations in different contexts
- ⚠️ **Cultural idioms**: English expressions don't always translate well
- ⚠️ **Compound technical terms**: Multi-word technical phrases
- ⚠️ **Acronyms and abbreviations**: May be translated when they shouldn't be
- ⚠️ **Code examples**: Comments in code may be mistranslated

## 🔍 Priority Areas for Review

If you're a native speaker wanting to help, focus on these high-impact areas:

### 1. Core Technical Terms (Highest Priority)
These terms appear throughout the document and must be consistent:

| English Term | Common Issues |
|--------------|---------------|
| Manifest | May be translated literally vs. kept as technical term |
| Assertion | Multiple possible translations (statement, claim, declaration) |
| Claim | Often confused with "assertion" |
| Ingredient | May be translated too literally (cooking context vs. technical) |
| Provenance | May not have direct equivalent in some languages |
| Binding | Context matters (data binding vs. legal binding) |
| Signature (cryptographic) | Often confused with handwritten signature |
| Credential | Multiple meanings (authentication vs. attestation) |

### 2. Section Titles and Headers
- Check that technical section names are accurate
- Verify cross-references are correct
- Ensure table of contents matches body

### 3. Code Comments and Examples
- Verify code comments are translated appropriately
- Check that variable names are NOT translated
- Ensure JSON keys remain in English

### 4. Diagrams and Figures
- Check figure captions
- Verify that text within diagrams is readable

### 5. Warnings and Notes
- Ensure critical warnings are clear and unambiguous
- Check that technical nuances are preserved

## 🤝 How to Report Issues

### Quick Fixes (1-2 errors)
[Open a Translation Issue](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md)

**Include**:
- Language
- Page number
- Current (incorrect) text
- Suggested correction
- Brief explanation why

**Example**:
```
Language: Japanese
Page: 42
Current: "マニフェストは主張を含む" (Manifest contains claims)
Suggested: "マニフェストはアサーションを含む" (Manifest contains assertions)
Reason: "Assertion" is the technical term, should not be translated as "claim" (主張)
```

### Multiple Issues (3+ errors)
- Open one issue per section/topic
- Or offer to review an entire chapter
- We can coordinate larger review efforts

### Systematic Review
If you want to review an entire translation:
1. Comment on [this tracking issue](../../issues) (or create one)
2. We'll coordinate with other reviewers
3. Use track changes or provide annotated PDF
4. We'll integrate your feedback

## 📈 Quality Improvement Process

### Current Workflow

```
DeepL Translation → Beta Release → Community Reports → Manual Review → Updates → Reviewed Status
     (Done)           (Current)        (Ongoing)         (Needed)      (Plan)      (Goal)
```

### Translation Status Levels

**🔄 Beta** (Current)
- AI-translated with minimal human review
- Good for understanding, not for critical implementation
- Actively seeking corrections

**✅ Community Reviewed** (Goal)
- Native speakers have reviewed technical terms
- Major issues corrected
- Suitable for most use cases
- English still recommended for implementation

**🏆 Expert Verified** (Future)
- Reviewed by C2PA experts AND native speakers
- High confidence in technical accuracy
- Can be used for implementation reference

### Version Tracking

When we update translations:
- Version number will increment (2.2.1, 2.2.2, etc.)
- Changelog will note what was corrected
- Original AI version remains available for comparison

## 🌍 Language-Specific Notes

### 简体中文 (Simplified Chinese)
**Common Issues**:
- Technical terms sometimes too literal (建议 vs. 断言 for "assertion")
- Need to decide: keep English terms or translate?
- Consider both mainland China and Taiwan usage

**Reviewers Needed**: Native speakers with software/crypto background

### 日本語 (Japanese)
**Common Issues**:
- Katakana vs. Kanji for technical terms
- Formality level (formal technical vs. accessible)
- Consistency with existing Japanese tech terminology

**Reviewers Needed**: Japanese developers familiar with security/crypto

### Deutsch (German)
**Common Issues**:
- Compound word construction
- Gender-neutral language
- Swiss vs. German vs. Austrian terminology

**Reviewers Needed**: German speakers in tech industry

### Français (French)
**Common Issues**:
- European French vs. Canadian French
- Technical terminology standardization
- Gendered nouns consistency

**Reviewers Needed**: French-speaking developers

## 💡 Translation Best Practices

### For Reviewers

1. **Keep English technical terms when appropriate**
   - Example: "JSON", "API", "hash" usually stay in English
   - Domain-specific terms (Manifest, Assertion) may stay or translate depending on language

2. **Check consistency**
   - Same English term = same translation throughout
   - Build a glossary as you review

3. **Preserve meaning over literal translation**
   - Goal: reader understands the technical concept
   - Not goal: word-for-word translation

4. **Consider your audience**
   - Target: developers with basic C2PA knowledge
   - Balance: technical accuracy vs. readability

5. **When in doubt, note it**
   - If multiple translations are valid, flag for discussion
   - Community can decide together

## 🎖️ Recognition

Contributors who significantly improve translations will be:
- Acknowledged in translation credits
- Listed as reviewers for that language
- Given recognition in project README

Quality improvements are highly valued contributions!

---

**Thank you for helping make C2PA accessible worldwide!** 🌍

Every correction, no matter how small, improves the resource for thousands of developers.
