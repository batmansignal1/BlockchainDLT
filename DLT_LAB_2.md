# Question 1: Blockchain Growth Analysis Using Geth Development Mode

## Aim
To start Geth in Development Mode, create and execute Ether transfer transactions, observe blockchain growth by monitoring block numbers after each transaction, and retrieve the details of a specific transaction.

---

## Requirements

- Geth installed
- Terminal (Ubuntu/Linux)
- JavaScript Console (`geth attach`)
- Development mode (`--dev`)

---

## Step 1: Start Geth in Development Mode

Open a terminal and run:

```bash
geth --dev --http --http.api eth,net,web3,personal,miner --allow-insecure-unlock console
```

Wait until the Geth JavaScript console (`>`) appears.

---

## Step 2: Display Available Ethereum Account

```javascript
eth.accounts
```

Example Output

```javascript
["0x8F2C5dD9f7F0b7D7f53D2C4A7D2E2E7B4A45AB12"]
```

---

## Step 3: Display Current Block Number

```javascript
eth.blockNumber
```

Example Output

```javascript
0
```

Record this as the **Initial Block Number**.

---

## Step 4: Unlock the Account

```javascript
personal.unlockAccount(eth.accounts[0], "", 0)
```

Output

```javascript
true
```

---

## Step 5: Execute Four Ether Transfer Transactions

Since only one account exists in development mode, send Ether from the account to itself.

### Transaction 1 (0.5 ETH)

```javascript
tx1 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(0.5, "ether")
})
```

Display the block number:

```javascript
eth.blockNumber
```

Record the block number.

---

### Transaction 2 (1 ETH)

```javascript
tx2 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1, "ether")
})
```

Display the block number:

```javascript
eth.blockNumber
```

Record the block number.

---

### Transaction 3 (1.5 ETH)

```javascript
tx3 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1.5, "ether")
})
```

Display the block number:

```javascript
eth.blockNumber
```

Record the block number.

---

### Transaction 4 (2 ETH)

```javascript
tx4 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(2, "ether")
})
```

Display the block number:

```javascript
eth.blockNumber
```

Record the block number.

---

## Step 6: Display the Latest Block

```javascript
eth.getBlock("latest")
```

Example Output

```javascript
{
  number: 4,
  hash: "...",
  parentHash: "...",
  miner: "...",
  transactions: [
      "0x..."
  ]
}
```

---

## Step 7: Retrieve Details of the Second Transaction

Use the transaction hash stored in `tx2`.

```javascript
eth.getTransaction(tx2)
```

Example Output

```javascript
{
  hash: "0x...",
  from: "0x...",
  to: "0x...",
  value: 1000000000000000000,
  gas: 21000,
  gasPrice: 1000000000,
  blockNumber: 2,
  transactionIndex: 0
}
```

---

# Sample Observation Table

| Step | Ether Sent | Transaction Variable | Block Number |
|------|-----------:|----------------------|-------------:|
| Initial | - | - | 0 |
| Transaction 1 | 0.5 ETH | `tx1` | 1 |
| Transaction 2 | 1 ETH | `tx2` | 2 |
| Transaction 3 | 1.5 ETH | `tx3` | 3 |
| Transaction 4 | 2 ETH | `tx4` | 4 |

> **Note:** In Geth Development Mode, each transaction is automatically mined, so the block number typically increases by one after every successful transaction.

---

# Result

The Geth blockchain was successfully started in Development Mode. Four Ether transfer transactions of **0.5 ETH**, **1 ETH**, **1.5 ETH**, and **2 ETH** were executed successfully without restarting Geth. The block number increased after each transaction, demonstrating blockchain growth. The latest block was displayed, and the details of the second transaction were successfully retrieved using its transaction hash.

---

# Screenshots to Include in the Record

1. Initial block number (`eth.blockNumber` before transactions).
2. Available Ethereum account (`eth.accounts`).
3. Block number after each transaction.
4. Latest block (`eth.getBlock("latest")`).
5. Transaction details of the second transaction (`eth.getTransaction(tx2)`).
6. Final block number after the fourth transaction.

## Complete Code (Copy & Paste)

```javascript
// Display available accounts
eth.accounts

// Display initial block number
eth.blockNumber

// Unlock the account
personal.unlockAccount(eth.accounts[0], "", 0)

// Transaction 1: Send 0.5 ETH
tx1 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(0.5, "ether")
})

// Display block number
eth.blockNumber

// Transaction 2: Send 1 ETH
tx2 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1, "ether")
})

// Display block number
eth.blockNumber

// Transaction 3: Send 1.5 ETH
tx3 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1.5, "ether")
})

// Display block number
eth.blockNumber

// Transaction 4: Send 2 ETH
tx4 = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(2, "ether")
})

// Display block number
eth.blockNumber

// Display the latest block
eth.getBlock("latest")

// Retrieve details of the second transaction
eth.getTransaction(tx2)
```

# Question 2: Transaction Verification Using Gas Limit

## Aim
To verify the minimum gas requirement for an Ether transfer by executing a transaction with an insufficient gas limit, observing the resulting error, and then repeating the transaction with the required gas limit of 21,000. Finally, retrieve the transaction receipt to confirm that the transaction has been successfully included in the blockchain.

---

## Requirements

- Geth installed
- Terminal (Ubuntu/Linux)
- JavaScript Console (`geth attach`)
- Development mode (`--dev`)

---

## Step 1: Start Geth in Development Mode

Open a terminal and run:

```bash
geth --dev --http --http.api eth,net,web3,personal,miner --allow-insecure-unlock console
```

Wait until the Geth JavaScript console (`>`) appears.

---

## Step 2: Display Available Account

```javascript
eth.accounts
```

---

## Step 3: Unlock the Account

```javascript
personal.unlockAccount(eth.accounts[0], "", 0)
```

Output

```javascript
true
```

---

## Step 4: Attempt Transaction with Gas Less Than 21,000

Execute the following transaction using a gas limit of **20,000**.

```javascript
txFail = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1, "ether"),
    gas: 20000
})
```

Observe and record the error message generated by Geth.

Example Error

```text
intrinsic gas too low
```

---

## Step 5: Repeat the Same Transaction Using Gas Limit = 21,000

```javascript
txSuccess = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1, "ether"),
    gas: 21000
})
```

The transaction hash will be returned.

---

## Step 6: Retrieve the Transaction Receipt

```javascript
eth.getTransactionReceipt(txSuccess)
```

Example Output

```javascript
{
  blockHash: "...",
  blockNumber: 1,
  transactionHash: "...",
  gasUsed: 21000,
  status: "0x1",
  transactionIndex: 0
}
```

---

## Step 7: Verify the Transaction is Included in the Blockchain

Retrieve the transaction details.

```javascript
eth.getTransaction(txSuccess)
```

The output should contain a valid `blockNumber`, confirming that the transaction has been mined and included in the blockchain.

---

# Expected Observation

| Transaction | Gas Limit | Result |
|------------|----------:|--------|
| First | 20,000 | Failed – "intrinsic gas too low" |
| Second | 21,000 | Successful and included in blockchain |

---

# Result

The transaction executed with a gas limit below **21,000** failed with an **"intrinsic gas too low"** error. After increasing only the gas limit to **21,000**, the transaction executed successfully. The transaction receipt confirmed successful execution, and the transaction details verified that it had been included in the blockchain.

---

# Screenshots to Include in the Record

1. Account details (`eth.accounts`).
2. Error message for the transaction with gas limit **20,000**.
3. Successful transaction hash using gas limit **21,000**.
4. Transaction receipt (`eth.getTransactionReceipt(txSuccess)`).
5. Transaction details (`eth.getTransaction(txSuccess)`).

// Display available accounts
eth.accounts

// Unlock the account
personal.unlockAccount(eth.accounts[0], "", 0)

// Attempt transaction with insufficient gas
txFail = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1, "ether"),
    gas: 20000
})

// Repeat transaction with correct gas limit
txSuccess = eth.sendTransaction({
    from: eth.accounts[0],
    to: eth.accounts[0],
    value: web3.toWei(1, "ether"),
    gas: 21000
})

// Retrieve the transaction receipt
eth.getTransactionReceipt(txSuccess)

// Verify the transaction details
eth.getTransaction(txSuccess)