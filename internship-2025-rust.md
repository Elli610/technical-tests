# Internship 2025 - Rust Technical Test

## Exercise: Ethereum ERC-20 Transfer Indexer

In this exercise, you will build a Rust service that monitors and indexes ERC-20 token transfers for a specific token on the Ethereum Holesky testnet and exposes this data through a public API.

### Requirements

The solution is composed of two parts:

#### 1. ERC-20 Transfer Indexing Service

* Your service must continuously monitor ERC-20 transfer events from a specific erc20 token address on an Ethereum testnet
* For each transfer event, save the following information:
  * Sender address
  * Recipient address
  * Amount
  * Block number
  * Transaction hash
* The data aggregation must store the transfer data in a persistent store of your choice
* Bonus: Implement functionality to backfill historical transfer data

#### 2. Public API Endpoint

* Create a REST API that exposes the collected data through the endpoint: `GET /eth/transfers`
* The API must read data from your persistent store
* The response format must be:

```json
{
  "token": {
    "decimals": 18,
    "symbol": "DEMO"
  },
  "transfers": [ 
    {
        "sender": "0x1234567890123456789012345678901234567890",
        "recipient": "0xabcdefabcdefabcdefabcdefabcdefabcdefabcd",
        "amount": "1000000000000000000",
        "block_number": "123456",
        "tx_hash": "0x0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef"
    },
    {
        "sender": "0xabcdefabcdefabcdefabcdefabcdefabcdefabcd",
        "recipient": "0x9876543210987654321098765432109876543210",
        "amount": "500000000000000000",
        "block_number": "123455",
        "tx_hash": "0xfedcba9876543210fedcba9876543210fedcba9876543210fedcba9876543210"
    }
  ]
}
```

* The transfers must be listed most recent first (sorted by block number in descending order)
* Include 1 or many query parameters for filtering by sender and/or recipient

### Technical Guidelines

1. Use a Rust web framework for the HTTP API
2. Use an appropriate Rust crate for database access
3. Use web3-rs, or another Ethereum library to connect to the Holesky network and monitor events
4. Implement proper error handling (forget about handling for chain reorganizations)
5. Use async/await patterns where appropriate
6. Include a clear and simple README with:
   * Setup instructions
   * API documentation
   * Design decisions

### Project Structure Suggestions

Consider organizing your project with the following modules:

```
src/
├── main.rs            # Application entry point
├── api/               # API handlers and routes
├── models/            # Data models and database schema
├── services/          # Business logic
│   └── indexer.rs     # ERC-20 transfer indexing service
├── repositories/      # Database interactions
└── utils/             # Helper functions and Ethereum utilities
```

### Additional Notes

* Your solution should be simple while fulfilling all the requirements
* The code should be well-structured, maintainable, and follow Rust best practices
* Include a Cargo.toml file with all necessary dependencies
* Consider using configuration files for environment-specific settings and the token address

### Submission Instructions

Please share an archive (`zip`, `tar`, or equivalent) of your git project. Ensure that your submission includes:

1. Complete source code
2. Short documentation
4. Any necessary setup scripts

The archive should be runnable without excessive configuration, and the README should clearly explain how to build and run the project.

Please contact me if you have any question
