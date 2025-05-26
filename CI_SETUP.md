# CI/CD Setup for LeakedViewControllerDetector

This document describes the comprehensive CI/CD setup implemented for the LeakedViewControllerDetector Swift package.

## 🚀 GitHub Actions Workflow

The CI workflow (`.github/workflows/ci.yml`) provides comprehensive testing and quality assurance:

### **Workflow Triggers**
- Every push to `main` branch
- Every pull request to `main` branch

### **Jobs Overview**

#### 1. **Test Job** (`test`)
- **Platform**: macOS-14 with Xcode 15.2
- **Matrix Testing**: iOS 17.2 and 16.4
- **Simulators**: iPhone 15 and iPhone 14
- **Features**:
  - Swift Package Manager caching for faster builds
  - Swift package tests with code coverage
  - Xcode project generation and testing
  - iOS and tvOS simulator testing
  - Code coverage report generation
  - Codecov integration for coverage tracking

#### 2. **SwiftLint Job** (`lint`)
- **Purpose**: Code style and quality checking
- **Tool**: [SwiftLint](https://github.com/realm/SwiftLint)
- **Configuration**: Custom `.swiftlint.yml` with project-specific rules
- **Output**: GitHub Actions compatible logging

#### 3. **SwiftFormat Job** (`swiftformat`)
- **Purpose**: Code formatting verification
- **Tool**: [SwiftFormat by Nick Lockwood](https://github.com/nicklockwood/SwiftFormat)
- **Configuration**: Comprehensive `.swiftformat` config
- **Features**:
  - Lint mode checking
  - Dry run verification
  - Fails CI if formatting issues found

#### 4. **Package Validation Job** (`package-validation`)
- **Purpose**: Swift Package Manager validation
- **Features**:
  - Package.swift validation
  - Dependency resolution testing
  - Release build verification

#### 5. **Documentation Job** (`documentation`)
- **Purpose**: Documentation build verification
- **Tool**: Swift DocC
- **Features**: Ensures documentation can be generated

#### 6. **Integration Test Job** (`integration-test`)
- **Purpose**: End-to-end integration testing
- **Dependencies**: Runs after test, lint, and package-validation
- **Features**:
  - Creates a test app that imports the package
  - Verifies the package can be consumed correctly
  - Tests real-world usage scenarios

## 🛠 Code Quality Tools

### **SwiftFormat Configuration**
- **File**: `.swiftformat`
- **Swift Version**: 6.0 (specified in `.swift-version`)
- **Key Features**:
  - 120 character line length
  - 4-space indentation
  - Comprehensive formatting rules
  - Trailing closure optimization
  - Import organization
  - Redundant code removal

### **SwiftLint Configuration**
- **File**: `.swiftlint.yml`
- **Key Features**:
  - Custom rule set for the project
  - Reasonable line length limits (120/150)
  - Function and type size limits
  - Complexity analysis
  - Custom rules for best practices

## 📋 Local Development

### **Format Script**
```bash
./scripts/format.sh
```
- Checks if SwiftFormat is installed
- Runs formatting check first
- Applies formatting if needed
- Shows git diff of changes

### **Manual Commands**
```bash
# Format code
swiftformat Sources/ Tests/

# Check formatting
swiftformat --lint Sources/ Tests/

# Run SwiftLint
swiftlint lint

# Run tests (requires iOS simulator)
swift test
```

## 🎯 CI Status Badges

The README includes status badges for:
- **CI Status**: Shows overall workflow status
- **Code Coverage**: Codecov integration
- **Swift Version**: Swift 6.0 compatibility

## 📊 Code Coverage

- **Tool**: Codecov
- **Integration**: Automatic upload from CI
- **Configuration**: Fails gracefully if token not available
- **Reports**: Available at codecov.io

## 🔧 Setup Requirements

### **Repository Secrets** (Optional)
- `CODECOV_TOKEN`: For code coverage reporting

### **Branch Protection** (Recommended)
- Require status checks to pass
- Require branches to be up to date
- Include all CI jobs in required checks

## 🚦 Workflow Dependencies

```
test ──┐
lint ──┼── integration-test
package-validation ──┘

swiftformat (independent)
documentation (independent)
```

## 📝 Benefits

1. **Quality Assurance**: Multiple layers of testing and validation
2. **Consistency**: Automated formatting and linting
3. **Compatibility**: Multi-version iOS testing
4. **Documentation**: Automated doc generation verification
5. **Integration**: Real-world usage testing
6. **Performance**: Caching for faster builds
7. **Visibility**: Comprehensive status reporting

## 🔄 Maintenance

- **Xcode Version**: Update in workflow when new versions are released
- **iOS Versions**: Update matrix when supporting new iOS versions
- **Dependencies**: Keep SwiftFormat and SwiftLint updated
- **Rules**: Review and update linting/formatting rules as needed

This CI setup ensures high code quality, consistency, and reliability for the LeakedViewControllerDetector package. 