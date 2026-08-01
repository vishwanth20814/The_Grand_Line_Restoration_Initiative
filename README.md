# Task 03 – The Grand Line Restoration Initiative

## Overview

This task involved restoring and validating a recovered Rust codebase representing the **Grand Line Navigation Network**. The repository contained multiple engineering archives recovered from different stages of development. The objective was not to redesign the project, but to investigate its behavior, identify engineering issues, restore the intended functionality, and preserve the historical implementation.

---

# Repository Structure

```
ghost-in-the-machine/
├── archives/
│   ├── alabasta/
│   ├── east-blue/
│   ├── reverse-mountain/
│   └── whiskey-peak/
├── docs/
├── src/
├── tools/
└── Cargo.toml
```

---

# Objective

The primary objectives of this task were to:

- Restore recovered engineering archives.
- Build and test each Rust project.
- Investigate compiler, runtime, and integration issues.
- Preserve historical behavior rather than rewriting the implementation.
- Document the engineering investigation and restoration process.

---

# Investigation Process

I investigated each recovered archive independently by reading its documentation and verifying its behavior.

For every archive I performed:

```bash
cargo build
cargo run
cargo test
```

This allowed me to verify compilation, runtime behavior, and integration tests before making any modifications.

---

# Archive Investigation
itly referenced the directory. - The runtime resolved the directory correctly. - The integration test required its existence. - Restoring the directory allowed all tests to pass without modifying application logic.  Therefore, the historical implementation was preserved while restoring the expected project structure.  ---  # Final Result  | Archive | Build | Run | Tests | |----------|------|-----|-------| | Alabasta | ✅ | ✅ | ✅ | | East Blue | ✅ | ✅ | ✅ | | Reverse Mountain | ✅ | ✅ | ✅ (after restoration) | | Whiskey Peak | ✅ | ✅ | ✅ |  ---  # Screenshots  ## Reverse Mountain Test Failure  ![Reverse Mountain Failure](screenshots/reverse-mountain-failure.png)  ---  ## Reverse Mountain Test Success  ![Reverse Mountain Success](screenshots/reverse-mountain-success.png)  ---  ## Final Successful Test Execution  ![All Tests Passed](screenshots/all-tests-passed.png)  ---  # Conclusion  This task emphasized investigating an inherited Rust codebase, understanding existing engineering decisions, and restoring expected behavior with minimal changes. Instead of modifying application logic unnecessarily, the solu
## 1. Alabasta

### Investigation

- Read the project documentation.
- Built the project.
- Executed the application.
- Ran all tests.

### Results
itly referenced the directory. - The runtime resolved the directory correctly. - The integration test required its existence. - Restoring the directory allowed all tests to pass without modifying application logic.  Therefore, the historical implementation was preserved while restoring the expected project structure.  ---  # Final Result  | Archive | Build | Run | Tests | |----------|------|-----|-------| | Alabasta | ✅ | ✅ | ✅ | | East Blue | ✅ | ✅ | ✅ | | Reverse Mountain | ✅ | ✅ | ✅ (after restoration) | | Whiskey Peak | ✅ | ✅ | ✅ |  ---  # Screenshots  ## Reverse Mountain Test Failure  ![Reverse Mountain Failure](screenshots/reverse-mountain-failure.png)  ---  ## Reverse Mountain Test Success  ![Reverse Mountain Success](screenshots/reverse-mountain-success.png)  ---  ## Final Successful Test Execution  ![All Tests Passed](screenshots/all-tests-passed.png)  ---  # Conclusion  This task emphasized investigating an inherited Rust codebase, understanding existing engineering decisions, and restoring expected behavior with minimal changes. Instead of modifying application logic unnecessarily, the solu
- Build successful.
- Runtime successful.
- All integration tests passed.
- Only compiler warnings (`dead_code` and `unused_import`) were present.
- No functional issues required restoration.

---

## 2. East Blue

### Investigation

- Built the project.
- Executed the application.
- Ran all tests.

### Results

- Build successful.
- Runtime successful.
- All tests passed.
- No engineering issues were detected.

---

## 3. Reverse Mountain

### Investigation

The build and runtime completed successfully, but one integration test failed.

Failed test:

```
asset_directory_is_expected_in_config_tree
```

Error:

```
expected configured asset directory to exist
```

To determine the cause, I inspected:

- `tests/integration.rs`
- `config/application.toml`
- `src/runtime.rs`

The configuration contained:

```toml
assets_dir = "assets"
```

The runtime resolved the asset directory as:

```rust
let assets_dir = config_dir.join(&config.runtime.assets_dir);
```

This indicated that the application expected the following directory:

```
config/assets
```

However, the directory did not exist in the recovered archive.

---

## Root Cause

The configuration referenced an asset directory that was missing from the repository structure.

Although the runtime could continue with fallback behavior, the integration test explicitly required the configured asset directory to exist.

---

## Fix Applied

Created the missing directory:

```bash
mkdir -p config/assets
touch config/assets/.gitkeep
```

---

## Verification

After restoring the directory:

```bash
cargo test
```

Result:

```
running 3 tests

test runtime_initializes_with_missing_asset_dir ... ok
test load_default_config ... ok
test asset_directory_is_expected_in_config_tree ... ok
```

All tests passed successfully.

---

## 4. Whiskey Peak

### Investigation

- Built the project.
- Executed the application.
- Ran all tests.

### Results

- Build successful.
- Runtime successful.
- All unit and integration tests passed.
- No modifications were required.

---

# Engineering Issue Identified

Only one engineering issue was discovered during the investigation.

| Archive | Issue | Status |
|----------|------|--------|
| Alabasta | None | Passed |
| East Blue | None | Passed |
| Reverse Mountain | Missing configured asset directory | Fixed |
| Whiskey Peak | None | Passed |

---

# Commands Used

Repository setup:

```bash
git clone https://github.com/Rufine777/ghost-in-the-machine.git
```

Rust installation:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
```

Project verification:

```bash
cargo build
cargo run
cargo test
```

Repository investigation:

```bash
cat README.md
cat config/application.toml
cat src/runtime.rs
```

Restoration:

```bash
mkdir -p config/assets
touch config/assets/.gitkeep
```

Git:

```bash
git status
git add .
git commit
git push
```

---

# Rust Concepts Used

- Cargo package management
- Project structure
- Configuration loading
- Integration testing
- Runtime initialization
- Modules
- Structs
- Error handling
- Path resolution

---

# Git Concepts Used

- Repository cloning
- Remote management
- Repository status
- Staging changes
- Commits
- Remote repositories
- Push operations

---

# Linux Concepts Used

- Directory navigation
- File inspection
- Directory creation
- Hidden files
- Terminal-based debugging

Commands used include:

- `cd`
- `cat`
- `mkdir`
- `touch`
- `find`
- `git`
- `cargo`

---

# Assumptions

The missing asset directory was considered an accidental omission from the recovered engineering archive rather than an intended code change because:

- The configuration explicitly referenced the directory.
- The runtime resolved the directory correctly.
- The integration test required its existence.
- Restoring the directory allowed all tests to pass without modifying application logic.

Therefore, the historical implementation was preserved while restoring the expected project structure.

---

# Final Result

| Archive | Build | Run | Tests |
|----------|------|-----|-------|
| Alabasta | ✅ | ✅ | ✅ |
| East Blue | ✅ | ✅ | ✅ |
| Reverse Mountain | ✅ | ✅ | ✅ (after restoration) |
| Whiskey Peak | ✅ | ✅ | ✅ |

---

# Screenshots

## Reverse Mountain Test Failure

![Reverse Mountain Failure](screenshots/reverse-mountain-failure.png)

---

## Reverse Mountain Test Success

![Reverse Mountain Success](screenshots/reverse-mountain-success.png)

---

## Final Successful Test Execution

![All Tests Passed](screenshots/all-tests-passed.png)

---

# Conclusion

This task emphasized investigating an inherited Rust codebase, understanding existing engineering decisions, and restoring expected behavior with minimal changes. Instead of modifying application logic unnecessarily, the solution preserved the intended design by restoring the missing project structure, resulting in successful builds, execution, and test completion across all recovered engineering archives.
