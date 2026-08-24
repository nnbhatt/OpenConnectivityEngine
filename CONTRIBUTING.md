
# Contributing to Open Integration Engine

Thank you for your interest in contributing to the **Open Integration Engine** project. Contributions are vital to the continued growth and success of the project, and we welcome all forms of participation, whether you are a developer, a documentation contributor, or a user providing feedback.

The contribution process is straightforward and can be completed in a few simple steps:

## How to Contribute

### 1. Open an Issue
Before making any changes, please open an issue in the [GitHub Issues Tracker](https://github.com/OpenIntegrationEngine/engine/issues). This step helps us discuss the problem or feature before work begins, ensuring alignment and reducing redundant efforts.

### 2. Fork the Repository
Start by forking the [Open Integration Engine GitHub repository](https://github.com/OpenIntegrationEngine/engine) to your own GitHub account.

### 3. Clone Your Fork
Clone your fork locally to your development environment:
```bash
git clone git@github.com:your-github/engine.git
```

### 4. Make Changes
Create a new branch for your feature or bug fix:
```bash
git checkout -b feature/your-feature-name
```

### 5. Install Tooling
OIE specifies the working Java version in [.sdkmanrc](./.sdkmanrc). To take advantage of this, install [SDKMAN](https://sdkman.io/) and run `sdk env install`
in the project's root directory. No other tooling is required.

### 5a. Build
The build is driven by Gradle through the included wrapper; no separate Gradle install is needed:
```bash
./gradlew build                         # full unsigned build and unit tests
./gradlew test                          # run unit tests (-Pcoverage=true for JaCoCo)
./gradlew cyclonedxBom                  # aggregate CycloneDX SBOM
./gradlew dependencyCheckAggregate      # dependency vulnerability reports
./gradlew dist                          # build distribution extension zips
```
On Windows use `gradlew.bat` instead of `./gradlew`. The assembled distribution lands in `server/setup`, the same location the previous Ant build used. Normal and CI builds are unsigned. For unsigned release candidates, run a clean build: `./gradlew clean build dist`. Windows with SDKMan may generate an error about the file path being too long in the javadoc step, skip this by adding `-x :server:userApiJavadoc` to your Gradle command.

The default test gate runs all self-contained suites using Gradle's standard `*Test`, `*Tests`, and `*TestCase` patterns. A documented set of legacy and external-infrastructure suites, including three historical `Test*` classes with nonstandard names, remains excluded because it currently needs database services, a running server, private fixtures, or portability repairs. Run `./gradlew test -PincludeLegacyTests=true` to audit that backlog; it is not expected to pass until those prerequisites and failures are resolved.

Jar signing is a privileged release operation and is disabled unless `-PenableSigning=true` is supplied. Never use the historical repository signing key; it has been publicly exposed. Generate a new signing identity, keep its keystore and passwords outside the checkout in an approved secrets manager, and inject these environment variables only in a protected release environment:

- `OIE_SIGNING_KEYSTORE`
- `OIE_SIGNING_STORE_TYPE`
- `OIE_SIGNING_STORE_PASSWORD`
- `OIE_SIGNING_ALIAS`
- `OIE_SIGNING_KEY_PASSWORD`
- `OIE_SIGNING_TSA_URL` (an explicitly approved timestamp authority endpoint)

With those values injected, run `./gradlew --no-daemon clean build dist -PenableSigning=true`. Hardware-token/CA workflows may additionally use `OIE_SIGNING_CERT_MODE=ca`, `OIE_SIGNING_PROVIDER_CLASS`, `OIE_SIGNING_PROVIDER_ARG`, and `OIE_SIGNING_CERT_CHAIN`. An explicit `-Pkeystore_property_file=/absolute/path` remains available for local release tooling, but that file must stay outside the repository with restrictive permissions. Do not pass passwords as Gradle command-line properties.

Dependencies are pinned and checksum-verified. To change a dependency version: edit `gradle/libs.versions.toml`, then refresh the checksum metadata **with a cold dependency cache and CI's flags**:
```bash
GRADLE_USER_HOME=$(mktemp -d) ./gradlew --write-verification-metadata sha256 build dist cyclonedxBom -Pcoverage=true
```
The cold cache matters: a warm cache skips re-resolving already-cached parent POMs, so they never get recorded, and the build then fails verification only in CI (this bit us once during the migration). The run downloads everything once and takes a few minutes. Only when adding a **new** artifact that ships in the distribution does `gradle/vendored-layout.json` need a one-line placement entry, and the build fails with a message telling you so.

### Changing build logic

The build's correctness is guarded by output comparison, not by unit
tests of the build scripts. When you change build logic (staging,
packaging, jar definitions), confirm the change does not alter the
product: build `server/setup` before and after, and compare the two
trees. The [oie-build-parity](https://github.com/pacmano1/oie-build-parity)
tooling does this at the archive-entry level (and can reproduce the
original byte-identical comparison against the pre-Gradle Ant baseline).
Only the changes you intended should appear.

### Run and debug

```bash
./gradlew :server:createDerbyDb     # one-time: create the embedded database
./gradlew :server:devRun            # run the server from the development tree
./gradlew :server:devLauncher       # run the server the way production starts it (from server/setup)
./gradlew :client:devClient         # run the administrator client against https://localhost:8443
```

Add `--debug-jvm` to any of these to suspend on JVM start and attach a debugger on port 5005. The JDK module flags come from `server/conf/default_modules.vmoptions`, the same file the production launcher uses. For IDEs, import the repository as a Gradle project (IntelliJ does this natively; Eclipse via Buildship); the old `.classpath`/`.project` files are gone on purpose.

### 6. Implement your changes

Implement the necessary changes, ensuring they align with the project’s coding standards and practices.

### 7. Test Your Changes
Before submitting your changes, please ensure that all tests pass and that your changes work as expected in your local environment.

### 8. Submit a Pull Request
Once your changes are ready, push them to your fork and create a **draft pull request (PR)** from your branch to the `main` branch of the project. Draft PRs help indicate that the work is in progress.  
Mark the PR as **"Ready for review"** only when it is actually complete and ready for feedback. Include a brief description of the changes and reference the related issue.

## Reporting Bugs

If you encounter a bug, please report it using the **GitHub Issues Tracker**:
1. **Search for existing issues** to check if the problem has already been reported.
2. If the issue is not listed, create a new issue with the following information:
   - A clear and descriptive title.
   - Steps to reproduce the issue.
   - The expected vs. actual behavior.
   - Any relevant logs, error messages, or screenshots to help diagnose the issue.

## Suggesting Features

If you would like to suggest a new feature or enhancement:
1. Open a new issue in the **GitHub Issues Tracker**.
2. Label the issue as a **feature request**.
3. Provide a detailed description of the feature and the problem it aims to solve.
4. If applicable, include examples or use cases to demonstrate the value of the feature.

## Community Guidelines

- Be respectful and professional in all interactions.
- Provide constructive feedback and suggestions.
- Engage in discussions around pull requests and issues with an open and collaborative mindset.

## License

By contributing to **Open Integration Engine**, you agree that your contributions will be licensed under the [Mozilla Public License (MPL) 2.0](./LICENSE).

Thank you for your interest in improving **Open Integration Engine**.
