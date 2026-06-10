# Architecture

## Overview

stellar-react-native-wallet-kit follows a layered architecture designed to separate developer-facing APIs from protocol and transport implementation details.

```text
React Native Application
            │
            ▼
      React Hooks
            │
            ▼
   SDK Core Services
            │
            ▼
 WalletConnect Manager
            │
            ▼
     Freighter Mobile
            │
            ▼
 Stellar / Soroban Network
```

## Design Goals

* Secure by default
* Mobile-first developer experience
* Fully typed APIs
* Modular architecture
* Testability

---

## Layers

### React Hooks Layer

Provides the public interface used by application developers.

Examples:

* useWalletState()
* useStellarAccount()
* useSignTransaction()
* useSubmitTransaction()
* useContractCall()

Responsibilities:

* State management
* React lifecycle integration
* Event subscriptions

---

### Session Layer

Manages WalletConnect lifecycle.

Responsibilities:

* Pairing
* Session persistence
* Reconnection
* Deep links
* Network validation

Files:

```text
session/
├── WalletConnectManager.ts
├── reconnect.ts
└── deeplink.ts
```

---

### Stellar Layer

Contains network-specific functionality.

Responsibilities:

* Transaction building
* XDR serialization
* Soroban simulation
* Horizon submission
* Contract invocation

Files:

```text
stellar/
├── buildPaymentTransaction.ts
├── invokeContract.ts
├── simulate.ts
├── horizon.ts
└── decodeContractResult.ts
```

---

### Provider Layer

Central application state.

Responsibilities:

* Context management
* Wallet state
* Event dispatching

Files:

```text
provider/
├── StellarWalletProvider.tsx
└── context.ts
```

---

## Data Flow

Wallet Connection

```text
User
  │
  ▼
connect()
  │
  ▼
WalletConnect
  │
  ▼
Freighter
  │
  ▼
Session Established
```

Transaction Signing

```text
Application
   │
   ▼
Build Transaction
   │
   ▼
Sign Request
   │
   ▼
Freighter Approval
   │
   ▼
Signed XDR
   │
   ▼
Submission
```

---

## Future Architecture

Planned additions:

* Multi-wallet adapter system
* Hardware wallet integration
* Transaction history service
* Contract event subscriptions
* Plugin architecture
