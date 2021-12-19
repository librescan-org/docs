# Introduction

The <a href="http://librescan.org/" target="_blank">LibreScan</a> team is looking for developers contributing to developing of a novel, openly accessible and truly free blockchain explorer.

## Problem

There is an eager need for a non-centralized, easily self-hostable & user friendly explorer, since while (most) blockchains are properly decentralized, 99% of users interact with them using completely centralized UIs.

The most often used type of such an evil UI is the block explorer itself.

Main issue is going 100% against blockchains' decentralization principles, as users are effectively associating all their valuable information (their wallet addresses, balances, owned token addresses etc.) with their IP addresses as soon as they make a lookup for them through such centralized explorers.

Even worse is that if any organization would ever decide to censor / ban blockchains and cryptocurrencies, they could be very effective by cutting off access to these very services.
Imagine a community highly reliant on these explorers waking up to a day where non of their points of trust is reachable.

This brings the next problem, which is trust itself. Whatever data these centralized services display, the users believe. Another important philosophy cornerstone of blockchain is the "never trust, always verify". Well, the centralized explorers go against this principle 100% as well by giving users a false comfort of exposing blockchain data that is supposedly verified. They could easily showcase false data and 99% of the users would believe it, since they have no verification tooling!

## Solution

All above issues can be solved by providing a truly free & open-source solution for this usecase. Companies have been profiteering way too long already of selling user data (blockchain data <-> personal metadata mappings) putting members of our community at risk!

The goal is to give the blockchain community an easily self hostable solution making the UI part just as much decentralized as blockchains themselves are.

As a result data meant to kept private stays private indeed.

## Quick overview of components

| Module                      | Lang / Tech | Purpose                                             |
| --------------------------- | ----------- | --------------------------------------------------- |
| [**frontend**](https://github.com/librescan-org/frontend) [[docs]](https://librescan-org.github.io/docs/tasks/frontend) | Vue3        | Responsible web frontend                            |
| [**api**](https://github.com/librescan-org/api) [[docs]](https://librescan-org.github.io/docs/tasks/api)      | NodeJS      | Retrieves and serves chain data from DB to frontend |
| [**db**](https://github.com/librescan-org/db) [[docs]](https://librescan-org.github.io/docs/tasks/db)       | PostgreSQL  | Stores restructured chain data from scraper         |
| [**scraper**](https://github.com/librescan-org/scraper) [[docs]](https://librescan-org.github.io/docs/tasks/scraper)  | Go          | Scrapes & structures blockchain data                |
| [**deploy**](https://github.com/librescan-org/deploy) [[docs]](https://librescan-org.github.io/docs/tasks/deploy)   | Various     | Orchestration platform manifests                    |
| [**infra**](https://github.com/librescan-org/infra) [[docs]](https://librescan-org.github.io/docs/tasks/infra)    | Terraform   | Infrastructure as code for popular platforms        |

# [> register <](https://forms.gle/92JWCf18ejMaaFSF6) as a contributor

The detailed roadmap of LibreScan will be laid out in January 2022.
It is highly important that the team has a ballpark overview how many contributors we can expect!

If you share the same mindset and you are willing to add value to the crypto community sign up via [this link](https://forms.gle/92JWCf18ejMaaFSF6).
