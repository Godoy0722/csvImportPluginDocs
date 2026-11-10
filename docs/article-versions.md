# Article Versions

[← Prev: Multi-Locale Support](multi-locale.md) | [README](../README.md) | [Next: Supplementary Files Descriptions →](supplementary-files.md)

The CSV import plugin supports creating multiple versions of the same article in a single import operation. This feature allows you to track revisions, corrections, and updates to published articles while maintaining a complete version history

## How It Works

The multiversion system uses two key fields to manage article versions:

- **versionIdentifier**: A unique string that links multiple versions of the same article together
- **version**: A positive integer indicating the version number (1, 2, 3, etc.)

When you provide these fields in your CSV:
1. Articles with the same `versionIdentifier` are treated as different versions of the same submission
2. Each version can have updated content, metadata, or files
3. Readers see the latest published version. When no version is published, the editorial workflow opens the latest version
4. All versions remain accessible in the system's version history

## Version Management Rules

1. **Version Identifiers**:
   - Can be any unique string (e.g., "article-001", "ml-paper-2024", "climate-study")
   - Leave empty for single-version articles
   - Must be unique across different articles (don't reuse identifiers)

2. **Version Numbers**:
   - Must be positive integers (1, 2, 3, ...)
   - Required when `versionIdentifier` is provided
   - Must be unique for each version of the same article
   - Version 1 is always the initial/base version

3. **Required Fields**:
   - **Version 1** must include the required fields: `articleTitle`, `authors`, and `datePublished`. `datePublished` is the publication date when that version is published, and the submission date when that version is queued or scheduled
   - **Versions > 1** can include only the fields you want to update (partial updates)
   - Fields not provided in higher versions inherit values from the previous version. A queued or scheduled version does not inherit a publication date. The date on the first row is the date the article was submitted

4. **Automatic Current Version**:
   - Readers see the latest published version. When no version is published, the editorial workflow opens the latest version
   - All other versions remain in the system as historical versions

## Practical Examples

### Example 1: Single Article Without Versions

For articles that don't need version tracking, simply leave `versionIdentifier` and `version` empty. Single-version examples: [OJS 3.3](../examples/3.3/issues/single_locale_single_version.csv), [OJS 3.4](../examples/3.4/issues/single_version_issues.csv), [OJS 3.5](../examples/3.5/issues/single_locale_single_version.csv).


### Example 2: Multi Version Articles

For article with multiple versions, you'll need to set the `versionIdentifier` and `version` fields. The `versionIdentifier` tracks the same article and the `version` handles with the article different versions. Multi-version examples: [OJS 3.3](../examples/3.3/issues/single_locale_multi_version.csv), [OJS 3.4](../examples/3.4/issues/multi_version_issues.csv), [OJS 3.5](../examples/3.5/issues/single_locale_multi_version.csv).

### Example 3: Mixed Articles

You can mix single-version and multi-version articles in the same CSV file. Mixed examples: [OJS 3.3](../examples/3.3/issues/mixed.csv), [OJS 3.4](../examples/3.4/issues/issues_example.csv), [OJS 3.5](../examples/3.5/issues/mixed.csv).

## Important Notes

- All versions of an article share the same submission ID but have different publication IDs
- Each version can have its own DOI if needed
- Readers can access previous versions through the article's version history
- The import process validates that no duplicate versions exist (same identifier + version number)
- Versions must be imported in sequence within a single CSV file (version 1 before version 2, etc.)

[← Prev: Multi-Locale Support](multi-locale.md) | [README](../README.md) | [Next: Supplementary Files Descriptions →](supplementary-files.md)
