# Changelog

All notable changes to this project will be documented in this file.

## [0.1.2] - 2026-03-27

### Fixed
- **Gitignore entry now uses directory syntax**: `.folder` is added as `.folder/` (with trailing slash), matching gitignore best practices for directory entries.
- **Robust duplicate detection**: The gitignore check now normalizes both the existing entry and the new entry by stripping trailing slashes, so `.folder` and `.folder/` are recognized as the same entry.

### Changed
- **Improved gitignore file handling**: When appending to an existing `.gitignore` that doesn't end with a newline, a newline is now inserted first to prevent mangling the last existing entry.
- **Added logging to gitignore operations**: Successful `.gitignore` writes now log at `info` level; failures log at `warn` level instead of being silently ignored.

## [0.1.1] - 2026-03-25

### Added
- **Gitignore-aware indexing**: ASTRA now respects `.gitignore` files when collecting files for indexing. This prevents build artifacts like `dist/`, `target/`, and other ignored paths from being indexed.
- **Auto-gitignore for ASTRA data**: On first run, ASTRA automatically adds `.folder` to the workspace's `.gitignore` to prevent committed ASTRA data directories.
- **Watcher gitignore filtering**: Incremental updates (file watcher) now also filter out gitignore-ignored paths, preventing re-indexing of build artifacts on file changes.

### Changed
- Replaced `walkdir` crate with `ignore` crate for file traversal (provides gitignore support natively)

### Testing
- Added `test_collect_files_respects_gitignore` to verify gitignore-based exclusion behavior

## [0.1.0] - 2026-03-25

### Added
- Initial release
- Semantic RAG search over indexed symbols
- Execution-path-aware traversal through call graph (A* biased by semantic similarity)
- Support for Rust, Python, and JavaScript/TypeScript
- MCP server interface for Claude Desktop/Cursor
- Local embeddings via BAAI/bge-base-en-v1.5 (fastembed + ONNX)
- Optional OpenRouter API support for embeddings
- File watching for incremental index updates
- Persistent graph and vector store to disk