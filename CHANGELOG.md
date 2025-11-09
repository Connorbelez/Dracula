# Changelog

All notable changes to the "Dracula Enhanced" theme will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial release preparation
- GitHub Actions CI/CD pipeline
- Automated publishing workflow

## [1.0.0] - 2024-01-XX

### Added
- Initial release of Dracula Enhanced theme
- Enhanced semantic highlighting for TypeScript/JavaScript
- Improved parameter color consistency (orange #FFB86C)
- Distinct object property colors (lavender purple #BD93F9)
- Better visual separation between parameters, properties, and variables

### Changed
- Function parameters now use orange (#FFB86C) in both declarations and usage
- Object properties now use lavender purple (#BD93F9) for better distinction
- Added `variable.language.special` scope to parameter highlighting
- Modified `support.type.property-name` to use purple for object properties

### Fixed
- Parameters now maintain consistent orange color throughout function body
- Properties no longer share the same color as regular variables

## Key Features

### Enhanced Semantic Highlighting
- **Parameters**: Orange (#FFB86C) everywhere - declarations and usage
- **Properties**: Lavender purple (#BD93F9) - distinct from variables
- **Variables**: Default foreground (#F8F8F2) - clean and readable

### Based on Dracula Official
- Maintains all the beloved Dracula color palette
- Compatible with Dracula Pro workflows
- Includes both regular and soft variants

## Migration from Official Dracula

If you're coming from the official Dracula theme:
1. All your existing colors remain the same
2. You'll notice better parameter highlighting
3. Object properties are now more distinguishable
4. No breaking changes - just enhancements!

---

[Unreleased]: https://github.com/connor/dracula-enhanced/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/connor/dracula-enhanced/releases/tag/v1.0.0