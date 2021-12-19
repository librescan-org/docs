# API scaffolders

After inspecting data retrievable on the most popular block explorer's endpoints, a Mock API should be designed to return static data for frontend integration

## Endpoints to be inspected:

- Listing entities
    - [List transactions](https://etherscan.io/txs)
    - [List blocks](https://etherscan.io/blocks)
    - [List all token transfers](https://etherscan.io/tokentxns)
    - [List specific token transfers](https://etherscan.io/token/0xaaa7a10a8ee237ea61e8ac46c50a8db8bcc1baaa) - **Note individual tabs: Transactions & Holders**

- Inspecting a particular entity
    - [Inspect transaction](https://etherscan.io/tx/0xb90286759db02d31da762da627c6b38eb0f1e6259b7cb12c5bd8361d9e8b8fd9)
    - [Inspect block](https://etherscan.io/block/13608386)
    - [Inspect token transfer](https://etherscan.io/tx/0xe3a869af682a06a8546fa8385b28672706aeffe233dcb49325e54a0bded7c37a)
    - [Inspect EOA](https://etherscan.io/address/0x4dac65c769ce98d48795facbc871745ada9e49e3) - **Note individual tabs: Transactions & ERC-20 Token Txns**
    - [Inspect contract](https://etherscan.io/address/0xaaa7a10a8ee237ea61e8ac46c50a8db8bcc1baaa) - **Note individual tab: Contract**

---

## Choice of language

LibreScan goes with JavaScript for its API component.
The reasons are as follows:

### JavaScript is still the most popular language

Since the API component reads from the Database and can restructure it in endless possible ways to be consumed by the frontend, it was crucial to pick a widely used language so we can have many contributors.

### Performance

Python was another option considered here for above reasons, but it is still less popular and WAY less performant than NodeJS.
If you want to see the actual numbers, check the popular [Benchmark game](https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/python.html) by Debian.

While there are way more performant solutions than NodeJS (Go, Rust, C ...) they have way smaller communities (in descending order).

Since the heavy lifting will be done by the scraper module anyway, NodeJS is a sane choice for the API component as it has to handle a very limited workflow.
