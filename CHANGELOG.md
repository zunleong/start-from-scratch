# Changelog

All notable changes to this skill are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versioning follows [Semantic Versioning](https://semver.org/).

## [1.0.0] - 2026-07-02

Initial release.

### Added
- Live interview flow: project type, framework (React/Vue/Vanilla/Other), language, exact framework version, exact language version, build approach (SPA vs SSR for React/Vue), styling approach, target folder, git init
- Best-practice advisory notes generated from the picked stack (framework + project type, language, styling), shown as informational text only
- Mandatory plan summary + explicit confirmation step before any file/command execution
- Execution guidance for Vite, Next.js, and Nuxt scaffolding, versioned package installs, ESLint + Prettier setup, and project-type-scaled folder structures
- Fixed defaults: npm as package manager, ESLint + Prettier always on, no test framework, no pre-installed extra libraries
