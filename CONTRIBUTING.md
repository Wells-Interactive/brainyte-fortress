# 🤝 Contributing

**Brainyte Fortress** welcomes contributions that help improve the platform's **security, reliability, privacy, maintainability, and overall user experience**.

Brainyte Fortress includes **AfOS (Android Fortress OS)** and is built around an AOSP-based, multi-repository development structure. Contributors should understand the repository structure and follow the contribution process before making changes.

---

## 📋 Before Contributing

Before making a contribution:

* **Keep changes small and focused.**
* **Understand the existing architecture and repository structure.**
* **Test your changes** before submitting them.
* **Document** new features, configuration changes, or important behavior.
* **Think security-first** — avoid unnecessary attack surfaces, insecure defaults, or exposed secrets.
* **Follow the existing project structure and coding conventions.**
* **Do not commit passwords, private keys, API keys, credentials, signing keys, or other sensitive information.**
* **Do not modify unrelated components** as part of a contribution.
* For changes affecting **security, architecture, licensing, boot, kernel, system frameworks, signing, or other sensitive areas**, ask for permission before proceeding where necessary.

---

## 🏗️ AfOS / AOSP Contributions

AfOS is developed within an **AOSP-based multi-repository workspace** managed seperately.

The AOSP workspace may contain multiple independent Git repositories.

Do **not** assume that the entire `aosp/` directory is a single Git repository.

Before changing code, identify the repository and component that owns the files you intend to modify.

Use the appropriate `repo` and Git commands to inspect the workspace and repository status.

### AfOS contributions may require additional review

Changes involving areas such as:

```text
🔐 Security
🛡️ SELinux / security policy
🔑 Signing / keys
🚀 Boot process
⚙️ System frameworks
🧩 Device configuration
📱 Android platform components
🧠 Kernel or low-level system components
📦 Vendor components
```

may require additional technical or security review.

If you want to work directly on **AfOS Android**, explain what you intend to work on and why before beginning where prior approval is required.

---

## 🌿 Branching

**Do not work directly on `main`.**

Create a dedicated branch for your contribution.

For example:

```bash
git checkout -b feature/my-change
```

Examples:

```text
feature/afos-security
feature/secure-settings
fix/build-configuration
docs/contributing
security/selinux-policy
```

Keep the branch focused on one logical change whenever possible.

---

## 🔒 Protected `main` Branch

The `main` branch is protected.

Contributors **must not directly push changes to `main`**.

Changes must go through a **Pull Request (PR)** and satisfy the repository's protection requirements.

The protected `main` branch requires:

* **Pull Request before merging**
* **At least 1 required approval**
* **Stale approvals dismissed when new commits are pushed**
* **Required status checks to pass**
* **Branch to be up to date before merging**
* **All review conversations resolved**
* **Force pushes blocked**
* **Branch deletion blocked**

These protections exist to prevent accidental or unreviewed changes from entering the main development branch.

---

## 🔍 Pull Request Requirements

Before submitting a Pull Request:

1. Make sure your branch contains only the intended changes.
2. Test the changes.
3. Review the changes yourself.
4. Check for accidental secrets or sensitive information.
5. Update relevant documentation.
6. Explain what changed and why.
7. Explain how the changes were tested.
8. Identify any security, compatibility, or architectural implications.

A Pull Request should clearly communicate:

```text
What changed?
      ↓
Why was it changed?
      ↓
What was tested?
      ↓
What could be affected?
      ↓
Are there security implications?
```

---

## 🧪 Testing

Contributors are responsible for testing their changes before submitting a Pull Request.

Where applicable, include:

* Build results
* Unit-test results
* Integration-test results
* Device testing
* Security testing
* Relevant logs or test information

Do not claim that something was tested if it was not actually tested.

For large AOSP/AfOS changes, perform the most appropriate targeted tests available rather than unnecessarily rebuilding the entire platform for every change.

---

## 🔐 Security

Security-sensitive information must never be committed to the repository.

Never commit:

```text
❌ Passwords
❌ Private keys
❌ API keys
❌ Authentication tokens
❌ Signing keys
❌ Credentials
❌ Secrets
❌ Private certificates
```

If you discover a potential security vulnerability, **do not disclose sensitive vulnerability details through a public issue or Pull Request**.

Follow the project's security-reporting process instead.

---

## 🔐 Permission

Some contributions require prior approval, particularly changes affecting security, architecture, licensing, or other sensitive parts of Brainyte Fortress or AfOS.

Where approval is required, contact:

**Email:** [wellsintltd@gmail.com](mailto:wellsintltd@gmail.com)
**Phone:** +234-806 751 9239

Please briefly explain:

1. What you want to change.
2. Why the change is needed.
3. Which part of Brainyte Fortress or AfOS it affects.
4. Any security, compatibility, or maintenance considerations.
5. If you want to work on **AfOS Android** and why.
6. How you intend to test the change.

Permission should be obtained **before beginning work** when the change falls into an area requiring prior approval.

---

## 📝 Documentation

Contributions that introduce new functionality, configuration, architecture, or security behavior should include appropriate documentation.

Documentation should allow another contributor to understand:
What is it?
    ↓
Why does it exist?
    ↓
How does it work?
    ↓
How is it configured?
    ↓
How is it tested?

---



