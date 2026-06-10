# Security

## Security Principles

The SDK is designed around one core principle:

**Private keys must never leave wallet software.**

Applications using this SDK should never have access to user secret keys.

---

## Trust Model

### Trusted Components

* Freighter Mobile
* Stellar Network
* Soroban RPC
* Horizon

### Untrusted Components

* Connected applications
* Third-party APIs
* External user input

---

## Transaction Flow

1. Application builds transaction
2. SDK serializes transaction
3. Freighter receives request
4. User reviews request
5. Freighter signs transaction
6. Signed XDR returned

At no point is secret key material exposed.

---

## Session Security

WalletConnect sessions are persisted locally.

Recommendations:

* Use encrypted storage
* Clear sessions on logout
* Validate active network
* Rotate sessions periodically

---

## Network Validation

The SDK validates:

* Testnet vs Mainnet
* Account ownership
* Session state

If a mismatch is detected:

```text
W004: NetworkMismatch
```

is thrown before signing occurs.

---

## Smart Contract Security

Before submission:

* Simulate transaction
* Validate authorization
* Estimate resources
* Detect execution errors

This reduces failed signing requests.

---

## Contributor Guidelines

Security-sensitive changes require:

* Maintainer review
* Additional testing
* Threat assessment

Examples:

* Signing logic
* Session handling
* Wallet integration
* Transaction serialization

---

## Reporting Vulnerabilities

Please do not create public issues.

Instead:

[security@project-domain.com](mailto:security@project-domain.com)

Include:

* Vulnerability description
* Impact assessment
* Reproduction steps
* Suggested mitigation
