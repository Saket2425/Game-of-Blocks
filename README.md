# README: Blockchain Voting and Auction System
## Overview
This repository contains the implementation of three decentralized applications (dApps) on Ethereum using **Solidity**:
1. **First Past the Post Voting System (FPTP)**
2. **Two-Round Voting System**
3. **Simple Auction with Withdrawal Mechanism**
4. **Meta Coin System**
Each system is designed to demonstrate key features of Solidity, including smart contract ownership, view and pure functions, mappings, and more. Below is a detailed description of each system and how they function.
---
## 1. First Past the Post (FPTP) Voting System
### How It Works:
- **Chairperson** deploys the contract and becomes the owner.
- **Voters** and **Candidates** register using `voter_registration()` and `NETA_registration()` respectively.
- The chairperson approves candidates and voters via `approve_voter()` and `NETA_approve()`.
- **Voters** view all approved candidates with `viewAll_NETA()` and cast their votes using `voteYour_NETA()`.
- The chairperson declares the winner by running `find_winner()`, and the winner's result is stored in the `winner` variable.
- Anyone can check the vote count for each candidate.
### Key Variables:
- `NETA_list`: Stores the addresses of all candidates.
- `voter_list`: Stores the addresses of all voters.
- `voters`: Mapping that tracks approval and voting status of voters.
- `Neta_approved`: Tracks if candidates are approved by the chairperson.
- `vote_cnt`: Stores vote counts for each candidate.
---
## 2. Two-Round Voting System
### How It Works:
This voting system is similar to FPTP but introduces a **runoff round**:
1. If no candidate receives more than **50%** of the votes in the first round, a second round is triggered.
2. The two candidates with the highest votes in the first round face off in the second round.
3. The candidate with the majority votes in the second round is declared the **winner**.
### Steps:
- First, voters cast their votes.
- If a candidate gets more than half the votes, they are declared the winner immediately.
- If not, the top two candidates compete in the second round, and voters vote again.
---
## 3. Simple Auction with Withdrawal Mechanism
### How It Works:
- **Owner** starts the auction by deploying the contract and calling `StartAuction(time)` where `time` specifies the auction duration.
- **Bidders** place their bids. The highest bidder is tracked in the `HighestBid` variable, and previous highest bidders' bids are stored in `pendingReturns`.
- Bidders can withdraw their funds using `withdraw()`.
  - Highest bidder can withdraw the difference between their total bid and the highest bid.
  - Other bidders can withdraw the full amount they bid.
- Once the auction ends (after the set time), the owner calls `endAuction()` to finish the auction.
### Key Concepts:
- **pendingReturns**: Holds the bids of users who are no longer the highest bidder.
- **withdraw**: Function to reclaim bids not currently the highest.
---
## 4. Meta Coin System
### Functionality:
The Meta Coin system is a simple dApp demonstrating **view** and **pure** functions in Solidity. The key purpose is to show how functions can interact with the blockchain's state variables and how some functions don't require state access.
### Function Types:
- **View Functions**: These functions can read but not modify the contract's state. For example, `ViewDues()` checks the `loans` mapping and returns the due amount.
- **Pure Functions**: These functions do not interact with any state variables. Functions like `add()` and `getCompoundInterest()` calculate values based on parameters and local variables, making them ideal for using the `pure` keyword.
---
