# Easy Track
## Problem

Lido DAO governance currently relies on Aragon voting model. This means DAO approves or rejects proposals via direct governance token voting. Though transparent and reliable, it is not a convenient way to make decisions only affecting small groups of Lido DAO members. Besides, direct token voting doesn't exactly reflect all the decision making processes within the Lido DAO and is often used only to rubberstamp an existing consensus.
There are a few natural sub-governance groups within the DAO, e.g. validators commitee, financial operations team and LEGO commitee. Every day they need to take routine actions only related to their field of expertise. The decisions they make hardly ever spark any debate in the comunity, and votings on such decisions often struggle to attract wider DAO attention and thus, to pass.

## Solution

Easy Track frictionless motions are solution to this problem. 
Easy Track motion is a lightweight voting considered to have passed if the minimum objections threshold hasn’t been exceeded. As opposed to traditional Aragon votings, Easy Track motions are cheaper (no need to vote ‘pro’, token holders only have to vote ‘contra’ if they have objections) and easier to manage (no need to ask broad DAO community vote on proposals sparking no debate). 

## Use cases for Easy Track motions

There are three types of votings run periodically by the Lido DAO that are proposed to be wrapped into the new Easy Track motions.
- Node Operators increasing staking limits
- Funds being allocated into reward programs
- Funds being allocated to LEGO program

See [specification.md](https://github.com/lidofinance/easy-track/blob/master/specification.md) for full specification.

## Project Setup
To use the tools that this project provides, please pull the repository from GitHub and install its dependencies as follows. It is recommended to use a Python virtual environment.

```bash
git clone https://github.com/lidofinance/easy-track
cd easy-track
npm install
```
Compile the Smart Contracts:

```bash
brownie compile # add `--size` to see contract compiled sizes
```

## Scripts

### `deploy.py`
Contains script to deploy main Easy Track contracts with EVM Script factories.
Script requires next ENV variables to be set:
- `DEPLOYER` - id of brownie's account which will deploy contracts. Might be skipped if run on `development` network.
- `LEGO_PROGRAM_VAULT` - address of Lido's LEGO program
- `LEGO_COMMITTEE_MULTISIG` - address allowed to create motions to top up LEGO program
- `REWARD_PROGRAMS_MULTISIG` - address allowed to create motions to add, remove or top up reward program

Next optional variables can be set:
- `PAUSE_ADDRESS` - address to grant PAUSE_ROLE
- `UNPAUSE_ADDRESS` - address to grant UNPAUSE_ROLE
- `CANCEL_ADDRESS` - address to grant CANCEL_ROLE


### `grant_executor_permissions.py`
Creates Aragon's Voting to grants permissions to EVMScriptExecutor required to execute EVMScripts generated by EVMScript factories. After voting creation checks that after execution all permissions will be granted correctly.

Script requires next ENV variables to be set:
- `DEPLOYER` - id of brownie's account which will deploy contracts. To create a voting account must have LDO Tokens. Might be skipped if run on a `development` network.
- `EVM_SCRIPT_EXECUTOR` - address to grant permissions.

### `revoke_all_permissions.py`
Creates Aragon's Voting to revoke all granted permissions from EVMScriptExecutor. After voting creation checks that after execution EVMScriptExecutor will has no any permissions.

Script requires next ENV variables to be set:
- `DEPLOYER` - id of brownie's account which will deploy contracts. To create a voting account must have LDO Tokens. Might be skipped if run on a `development` network.
- `EVM_SCRIPT_EXECUTOR` - address to grant permissions.