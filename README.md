```markdown
# StackVote - Decentralized Governance Contract

A decentralized governance and voting contract built on the Stacks blockchain, enabling community-driven decision-making through deposit-based voting power.

## Overview

StackVote is a Clarity smart contract that implements a democratic voting system where STX holders can:
- Deposit STX to gain voting power
- Create proposals for community governance
- Vote on proposals with weighted voting (based on deposit amount)
- Execute approved proposals after voting deadlines
- Claim rewards for participation

## Features

### Core Functionality

- **Deposit System**: Users deposit STX to acquire voting power (1 STX = 1 vote weight)
- **Proposal Creation**: Any user can create governance proposals with title, description, and voting duration
- **Weighted Voting**: Voting power is proportional to STX deposited
- **Voting Rewards**: Voters earn 2% rewards on their voting weight for participating
- **Proposal Execution**: Automated execution after deadline based on vote tally

### Key Constants

| Error Code | Description |
|-----------|-------------|
| ERR_NOT_ADMIN (100) | Only owner can perform this action |
| ERR_NOT_FOUND (101) | Proposal or vote not found |
| ERR_ALREADY_VOTED (102) | User has already voted on this proposal |
| ERR_VOTING_CLOSED (103) | Voting period has ended |
| ERR_NO_FUNDS (104) | User has insufficient voting power |
| ERR_INVALID_AMOUNT (105) | Invalid amount provided |

## Public Functions

### `deposit(amount: uint) -> Response`
Deposits STX to gain voting power.
```
stackvote::deposit u1000
```

### `create-proposal(title: string, description: string, duration: uint) -> Response`
Creates a new governance proposal.
```
stackvote::create-proposal "Increase Block Size" "Proposal to increase Stacks block size to 2MB" u1000
```

### `vote(proposal-id: uint, support: bool) -> Response`
Votes on an active proposal (true = for, false = against).
```
stackvote::vote u1 true
```

### `execute-proposal(proposal-id: uint) -> Response`
Executes a proposal after its voting deadline expires.
```
stackvote::execute-proposal u1
```

### `claim-reward(proposal-id: uint) -> Response`
Claims voting participation rewards after a proposal execution.
```
stackvote::claim-reward u1
```

## Read-Only Functions

- **`get-proposal(id: uint)`**: Retrieve proposal details
- **`get-vote(proposal-id: uint, voter: principal)`**: Get voter's vote details
- **`get-total-proposals()`**: Total number of proposals created
- **`get-weight-of(voter: principal)`**: Get user's voting power

## Data Structures

### Proposal
```
{
  creator: principal,
  title: string-ascii(128),
  description: string-ascii(256),
  for-votes: uint,
  against-votes: uint,
  total-staked: uint,
  deadline: uint,
  executed: bool
}
```

### Vote
```
{
  support: bool,
  weight: uint,
  timestamp: uint,
  rewarded: bool
}
```

## Usage Example

1. **Deposit STX for voting power**:
   ```
   deposit 1000
   ```

2. **Create a proposal**:
   ```
   create-proposal "Fee Reduction" "Reduce transaction fees by 10%" 1000
   ```

3. **Vote on the proposal**:
   ```
   vote 1 true
   ```

4. **Claim voting rewards after execution**:
   ```
   claim-reward 1
   ```

## Reward Mechanism

Voters earn **2% of their voting weight** as rewards for participating. For example:
- Deposit: 1000 STX
- Voting reward: 20 STX (2% of 1000)

## Security Features

- Owner-based access control for administrative functions
- Vote weight validation to prevent voting without deposits
- Duplicate vote prevention (one vote per user per proposal)
- Voting deadline enforcement
- Single reward claim per vote

## Installation

1. Clone the repository
2. Install Clarinet: https://github.com/hirosystems/clarinet
3. Run tests:
   ```bash
   clarinet test
   ```
4. Deploy:
   ```bash
   clarinet deployment mainnet
   ```

## Technical Stack

- **Blockchain**: Stacks (Layer 2 Bitcoin)
- **Language**: Clarity
- **Framework**: Clarinet


## Contributing

Contributions are welcome! Please submit pull requests or open issues for bugs and feature requests.

---

**Version**: 1.0.0  
**Status**: Production Ready
```
