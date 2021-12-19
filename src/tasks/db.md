# DB designers

Librescan stack will utilize a PostgreSQL database to store blockchain data in the most storage efficient way without compromising on lookup speeds.

It must be able to perform well even on a Raspberry Pi 4 with two attached SSD drives.

The goal is to turn the following YAML draft into PostgreSQL table creation statements:

```yaml
ids:
  id: bigserial
  idx: bytea # 16 bytes, indexed, used for lookup
  remainder: bytea # remainder of binary data
  type: smallint # 0=eoa 1=contract 2=txhash 3=blockhash

nicks:
  id: bigint # foreign key id@ids
  nick: string # nickname of the particular id 
  type: smallint # indicates nickname type

erc20tokens:
  id: bigint # foreign key id@ids
  name: string # token name
  symbol: string # token symbol
  decimals: smallint # how many decimals the token has
  supply: bigint # divided by decimals

blocks:
  id: bigint # foreign key id@ids, the blockhash
  height: int # block height in the chain
  created_at: int # unix ts

txs:
  txhash: bigint # foreign key id@ids, the txhash
  block: int # block height, foreign key height@blocks
  value: bigint # in gwei
  from_id: bigint # foreign key id@ids
  to_id: bigint # foreign key id@ids
  gas_limit: bigint
  gas_price: bigint
  method_id: int? # 4 bytes
  params: bytea? # not contract deployment, not erc20 tx

ethtxs: # if data == 0x tx gets inserted
  txhash: bigint # foreign key id@ids
  from_id: bigint # foreign key id@ids
  to_id: bigint # foreign key id@ids
  value: bigint # in gwei
  
erc20txs: # if first four bytes indicate transfer signature tx gets inserted
  txhash: bigint # foreign key id@ids
  token_id: bigint # foreign key id@ids
  from_id: bigint # foreign key id@ids
  to_id: bigint # foreign key id@ids
  value: bigint # divided by decimals

contracts:
  txhash: bigint # foreign key id@ids
  address_id: bigint # contract address, foreign key id@ids
  deployer_id: bigint # deployer address, foreign key id@ids
  bytecode: bytea # contract bytecode

stats:
  address_id: bigint # foreign key id@ids
  token_id: bigint # foreign key id@ids, or 0 for eth transfers
  balance: bigint # divided by decimals / gwei
  first_in: int # unix ts
  first_out: int # unix ts
  last_in: int # unix ts
  last_out: int # unix ts

```

Constructive comments to the structure are welcome as well.

---

## Choice of engine

PostgreSQL was chosen for several reasons as follows:

### Performance & Scaling

PostgreSQL is usually the choice for open-source projects of this magnitude.
The community around it is also preferable in our humble opinion.

> If you’re developing an application with a database back end, which of the two should you use? Consider PostgreSQL for any application that might grow to enterprise scope, with complex queries and frequent write operations. If you’re new to the world of databases and don’t expect your application to scale up, or you’re looking for a quick tool for prototyping, then consider MySQL.

### Philosopy

Again, the Philisophy of the technologies used is another important factor as we've seen when we described the previous modules. Consider the following:

> One of the original developers of Ingres returned to Berkeley in 1985 (after founding a company that commercialized Ingres) to develop a successor to Ingres that he named Postgres. The name was officially changed to PostgreSQL to take advantage of the reference to Structured Query Language, but the project uses both names. The first production release, PostgreSQL 6.0, came out in 1997. Now at version 14 (beta), Postgres is developed by an “unincorporated association of volunteers and companies who share code under the PostgreSQL Licence,” according to a project FAQ.

> Unlike PostgreSQL, MySQL has always been under corporate control. Original developer MySQL AB was acquired by Sun Microsystems in 2008, shortly before Sun was itself acquired by Oracle in 2010.

*Source from [fivetran.com](https://www.fivetran.com/blog/postgresql-vs-mysql)*

# [> register <](https://forms.gle/92JWCf18ejMaaFSF6) as a contributor

The detailed roadmap of LibreScan will be laid out in January 2022.
It is highly important that the team has a ballpark overview how many contributors we can expect!

If you share the same mindset and you are willing to add value to the crypto community sign up via [this link](https://forms.gle/92JWCf18ejMaaFSF6).
