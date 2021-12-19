# Scraper developers

After the DB has been constructed and the API is ready to serve data from it to the frontend, we need to start filling the DB with real world data scraped off a real blockchain.

The simple hierarchy is that each block contains N transactions. Transactions can be of various kinds, respectively:

## Regular ETH transaction

This is the simplest form of a transaction, where the particular chain's native currency (ETH on Ethereum, BNB on Binance Smart Chain, etc.) gets transferred from address 0xA to address 0xB.

They can be easily recognized by the scraper as all these transactions have an empty data field (0x).

## Contract deployment transaction

Contract deployment transactions can be also detected without much effort, since these are the only transactions where there is no recipient defined.

Any transaction where there is no recipient and the data field is not empty is definitely a contract deployment transaction.

We need to further differentiate token contract and other custom contract deployments:

- ERC20 Token contract

Such a contract implements the [EIP-20 Token Standard Inferface](https://eips.ethereum.org/EIPS/eip-20) and has the specified method IDs present in the contract bytecode.

- Other custom contract
    
Anything which is not an ERC20 token contract falls into this category, meaning if at least ONE of the method signatures present in EIP20 is not defined in the contract then it falls into this category.

## Token transfer transaction

These kind of transactions contain information about a token transaction in their either their data field or emit a Transfer(address, address, uint256) type of event during execution

- Direct transfers

These kinds of transfers are easily recognizable from the data field's first four bytes being ```0xa9059cbb``` indicating the transfer(address, uint256) function signature.

Two 32byte parameters will follow, the first being trimmed to 20bytes which indicates the recipient of the transfer, and the other value meaning the amount of tokens transferred in a HEX encoded form.

- Internal transfers

When some other kind of transaction (e.g. DEX trade) moves tokens, they will event a single or multiple Transfer(address, address, uint256) signature events. These events should be parsed if they are emitted and inserted into the DB.

---

## Choice of language

The scraper module of LibreScan is implemented in [Go](https://go.dev).

### Ecosystem

Go is a quite popular programming language in the blockchain & crypto ecosystem, as major players build their official engines with it.
Just to name a few:

- [Ethereum](https://github.com/ethereum/go-ethereum)
- [Binance](https://github.com/binance-chain/bsc)
- [Coinbase](https://github.com/coinbase/kryptology)

### Language purpose

While it is true that Rust is more performant than Go, but the Go language was especially designed for concurrent network based applications

### Learning curve

Again, the learning curve (=entry barrier) was an important factor as well when making the decision.
Rust has a way steeper learning curve and has unquestionably harder to understand sources. Same philosophy applies that the more people are able to read how stuff works, the better.

### Considering benefits & tradeoffs

Comparing all the above benefits of Go with the performance tradeoff against Rust, the choice was a no-brainer.
If you love Go & crypto you should really join the development to build something truly magnificent for this space!

# [> register <](https://forms.gle/92JWCf18ejMaaFSF6) as a contributor

The detailed roadmap of LibreScan will be laid out in January 2022.
It is highly important that the team has a ballpark overview how many contributors we can expect!

If you share the same mindset and you are willing to add value to the crypto community sign up via [this link](https://forms.gle/92JWCf18ejMaaFSF6).
