# StorageHub Grant Application

> This document will be part of the terms and conditions of your agreement and therefore needs to contain all the required information about the project. Don't remove any of the mandatory parts presented in bold letters or as headlines (except for the title)! Lines starting with a `>` (such as this one) should be removed. Please use markdown instead of HTML (e.g. `![](image.png)` instead of `<img>`). 
>
> See the [Grants Program Process](https://github.com/w3f/Grants-Program/#pencil-process) on how to submit a proposal.
- **Team Name:** Moonsong Labs
- **Payment Address:** USD Wire Preferred
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 2

> :exclamation: *The combination of your GitHub account submitting the application and the payment address above will be your unique identifier during the program. Please keep them safe.*
## Project Overview :page_facing_up:

If this application is in response to an RFP, please indicate this on the first line of this section.

If this is an application for a follow-up grant (the continuation of an earlier, successful W3F grant), please provide the name and/or pull request of the said grant on the first line of this section.

### Overview

* Tagline Describer
    * StorageHub is a decentralized storage public good parachain optimized for file based storage and larger data sets that are not suitable to be stored directly in standard parachain storage. The proposed parachain will provide developers in the Polkadot ecosystem with an alternate decentralized and substrate-based storage solution and functionality.

* Purpose	
    * The goal of this project is to provide storage for web3 applications and protocols within the Polkadot & Kusama ecosystems. Unlike other storage protocols that focus on end user or enterprise storage scenarios, StorageHub’s feature set optimizes for web3 application storage use cases. StorageHub aims to provide a decentralized storage option that allows web3 applications to store large files and large data sets in a cost efficient way without sacrificing decentralization properties.

* Problem 
    * Storage oriented chains, like Filecoin and Arweave, have emerged to provide more efficient and decentralized storage capabilities. However, these chains are standalone chains, and are not designed to interoperate with other chains. The problem is that web3 apps need smart contract logic and compute to be combined with storage to make a complete solution, but smart contracts and compute generally reside on different chains (e.g. Ethereum Mainnet, L2 rollups, Parachains) vs. on the storage optimized chains (Filecoin, Arweave). In response, these storage chains have tried to bolster their smart contract capabilities (e.g. Filecoin’s FVM, Arweave’s Smartweave), but they have and will continue to be hard pressed to convince all compute and smart contract activity to migrate to their chains.

    * The ideal scenario would be to combine smart contract execution from e.g. a Substrate based Polkadot parachain such as Moonbeam or Astar with storage from a storage optimized chain like Arweave.  If we look at NFT scenarios as an example, this is happening. The scenario is that you have an NFT contract on Mainnet, that has a pointer to a JPEG via an Arweave URL.  The problem is that this is a one-way pointer between 2 independent systems. It is up to the application to mediate interactions between the 2 chains in the client.  There is no awareness or connection between the contract and the JPEG other than the URL pointer in the contract. What if the contract could update access to and ownership of the actual data itself? What if the contract could read and act on the data stored? Simple functionality like this would open up a large number of new scenarios. End user UX could be substantially improved by removing the need for the user to understand and interact directly with both the contract and the storage blockchains, using potentially different accounts, keys, etc.

* Vision
    * StorageHub is a storage optimized parachain that is designed to work with other Polkadot & Kusama parachains. It focuses on storing data in an efficient and decentralized way, while allowing that storage to be accessed, used, and managed by other parachains. It will be possible for users to directly interact with the storage on the chain, but StorageHub also seeks to natively interoperate with existing parachains via XCM.

* Inspiration 
    * Amazon S3
        * (https://en.wikipedia.org/wiki/Amazon_S3) was a key building block of web2 cloud infrastructure that greatly eased and improved data storage in web2 applications.  With S3 devs could store arbitrarily large amounts of data in their apps without needing to get bogged down with storage infrastructure or scaling concerns.  StorageHub seeks to do something similar for web3 devs building on Polkadot.

    * Filecoin
        * (https://filecoin.io/) is a storage optimized chain that creates a 2 sided marketplace of storage providers and storage consumers.  The project is responsible for key innovations such as ipfs and libp2p, among other things.  In many ways filecoin sets the standard for decentralized storage in the web3 space.  Although the protocol seems focused on trying to compete with cloud and other centralized storage providers.

    * Arweave
        * (https://www.arweave.org/) is a storage optimized chain like filecoin, but that emphasizes permanent storage vs creating a time based storage marketplace.  Users pay once to store data on arweave forever.  It is popular to use for metadata associated with NFTs, among other things.

    * Project Greenfield
        * (https://github.com/bnb-chain/greenfield-whitepaper/blob/main/README.md) is a storage optimized chain designed to work with the BNB chain.  It was born out of practical needs that the state of BNB chain is already many terabytes large and there is a need to offload unnecessary storage from the main BNB chain.  There are lots of good cross chain ideas in Greenfield including having storage on Greenfield represented as NFTs on BNB chain which can be managed and whose ownership can be changed.

### Project Details

* Design and Implementation Principles
    * StorageHub will be a Substrate-native implementation deployed to both Kusama and Polkadot.
    * It will be a public good chain that uses DOT for fees, governance, and other utilities.
    * It will offer native XCM support such that parachains can interact with stored data and metadata in a trustless way..
    * End users and Dapps should be able to store and retrieve stored data from the chain.
    * The chain will create a 2 sided marketplace of storage providers and storage consumers.
    * A minimum of N copies of any given piece of data should be stored such that the system can survive the loss of some copies without losing the original dataset.  Erasure encoding or similar technique could be optionally used to achieve this.
    * On the tradeoff spectrum between decentralization vs performance, we opt to always maintain good decentralization properties even if that means less performance is possible.
    * There will need to be a network of storage providers that supply storage to the blockchain. 
    * The parachain will track metadata about the data being stored, and facilitate payments between the data owner and the storage provider. 
    * A set of metadata associated with any stored data will be managed by StorageHub. This will allow the data owner to control access, and to transfer ownership of the data to other parties.
    * StorageHub doesn’t aim to have smart contract functionality itself. Rather it strives to integrate, work with, and complement other smart contract or native parachains.
    * In creating the design for StorageHub, we will leverage previous research into polkadot and substrate based filestorage solutions such as:
        * https://github.com/w3f/Grants-Program/pull/1888
        * https://github.com/common-good-storage/report/blob/master/src/first.md

* Key Questions and Anticipated Challenges
    * Existing storage networks focus more on storage but less on user accessibility to that data.  But storage without accessibility isn’t that useful to users.  Can we incorporate outside accessibility guarantees into the protocol?
    * What type of storage will it provide? Only immutable hash/value type or will it support mutable references (like a filesystem, useful to store/manage a web service or page)
    * What kind of XCM interaction (API) do we want to support?
        * XCM (mostly HRMP) costs may make some scenarios prohibitive.
        * Given the costs of XCM, to what degree does it make sense to store metadata on StorageHub vs on the controlling chain?
    * What do sustainable economics look like for storage providers, especially given that a public good chain won’t have a token to help bootstrap this side of the market?
    * How is data provided and stored without increasing PoV?  This will most likely need to be a combination of offchain workers and a separate storage system.  Regular substrate state can’t be used for larger data storage, it would be used to keep tracking information about where and what data is stored.
    * What does this new data provider node look like and how does it work with other node types supporting the system?
    * How will the system ensure that enough copies of a given piece of data are present and available, given that storage provider nodes can go offline at any time.
    * How is it checked that data providers have the data they are being paid to store?  What are the consequences of failing this check?
    * How do you manage censorship of data?
        * Different kinds of data that could be subject to take down requests.  Data that e.g. a political party doesn’t like.  Data that is illegal in a given jurisdiction due to copyright or similar.  Data that is both illegal and morally offensive. 
        * Perhaps OpenGov tracks could be used for censorship takedowns.
        * Or data storage providers could be given censorship controls, and a permissionless staking design would make it so token holders could vote out providers that are out of line with community censorship standards.


### Ecosystem Fit
* Where and How Does StorageHub Fit In
    * There are currently no native Polkadot decentralized storage solutions and StorageHub aims to fill that gap.
    * Crust provides an incentive layer on top of existing storage protocols like ipfs.  Whereas StorageHub seeks to be a storage provider itself.
    * StorageHub will be natively accessible by other parachains via XCM.

* Target Audience
    * StorageHub is targeted for chains, contracts, teams and individuals that require data storage of larger datasets, and who value that storage being decentralized, censorship resistant, and permanent as long as storage fees are paid.
    * StorageHub will prioritize web3 developers that want to incorporate decentralized storage into their applications.  This means a focus on APIs, SDKs, developer docs and education.
    * StorageHub will secondarily provide a reference application which allows users to directly interact with the system, storing data and managing data storage.

* Use Cases
    * NFT, NFT marketplace, and Metaverse metadata storage
    * Dapps that require data storage
    * Personal and enterprise data storage - same as other storage chains.
    * DAO owned data assets - DAOs operating on existing parachains can manage access to and ownership of data assets on StorageHub.
    * “True” NFTs that can have the entirety of their associated data assets on-chain via a combination of an e.g. NFT contract and StorageHub stored assets.
    * Markets for data sets using NFT marketplaces.
    * New types of smart contracts that can act on StorageHub stored data on an one off or continuous basis


## Team :busts_in_silhouette:

### Team members
* Team Leader: Derek Yoo
* Team:
    * Alan Sapède
    * Chase Williams
    * Olivia Smith
    * Engineers to be hired

### Contact

- **Contact Name:** Chase Williams
- **Contact Email:** Chase@moonsonglabs.com
- **Website:** https://moonsonglabs.com/

### Legal Structure

- **Registered Address:** 1500 District Ave Burlington, MA 01803
- **Registered Legal Entity:** Delaware C Corp

### Team's experience

* The Moonsong Labs protocol engineering team has deep expertise in Substrate, EVM, cross chain technologies, and launching parachains on Kusama and Polkadot. Our team is the core engineering team for the Moonbeam Network and have made significant contributions to the ecosystem, such as contributions to Frontier, the Moonwall testing framework, parachain-staking pallet, and xcm tools. The engineering team is made up of 13+ engineers and is rapidly growing. 

* Team Example Code Repos:
    * https://github.com/Moonsong-Labs
    * https://github.com/moonbeam-foundation/moonbeam

* Team LinkedIn Profiles:
    * [Alan Sapede](https://www.linkedin.com/in/alansapede/)
    * [Derek Yoo](https://www.linkedin.com/in/derek-yoo-8a050/)
    * [Olivia Smith](https://www.linkedin.com/in/olivia-smith-69966616a/)
    * [Chase Williams](https://www.linkedin.com/in/chase-williams-442712b1/)
    * Engineering Team TBD

### Team Code Repos

- https://github.com/<your_organisation>/<project_1>
- https://github.com/<your_organisation>/<project_2>

Please also provide the GitHub accounts of all team members. If they contain no activity, references to projects hosted elsewhere or live are also fine.

- https://github.com/<team_member_1>
- https://github.com/<team_member_2>

### Team LinkedIn Profiles (if available)

- https://www.linkedin.com/<person_1>
- https://www.linkedin.com/<person_2>

### Google Scholar Profiles (Or other research indexer profile, ex. Researchgate)
- https://scholar.google.com/citations?user=<person_1>
- https://scholar.google.com/citations?user=<person_2>

## Development Status :open_book:

If you've already started working on your project or it is part of a larger project, please provide a link and a description of the research here. In any case, please provide some documentation on the research and other work you have conducted before applying. This could be:

- links to improvement proposals or [RFPs](https://github.com/w3f/Grants-Program/tree/master/docs/RFPs) (requests for proposal),
- academic publications relevant to the problem,
- links to your research diary, blog posts, articles, forum discussions or open GitHub issues,
- references to conversations you might have had related to this project with anyone from the Web3 Foundation.

## Development Roadmap :nut_and_bolt:

This section should break the research development roadmap down into milestones and deliverables. To assist you in defining it, we have created a document with examples for some grant categories, including research [here](../docs/Support%20Docs/grant_guidelines_per_category.md). Since these will be part of the agreement, it helps to describe _the deliverable we should expect in as much detail as possible_, plus how we can verify that deliverable. Whenever milestones are delivered, we refer to this document to ensure that everything has been delivered as expected.

Below we provide an **example roadmap**. In the descriptions, it should be clear how your project is related to Substrate, Kusama or Polkadot. We _recommend_ that teams structure their roadmap as 1 milestone ≈ 1 month.

> :exclamation: If any of your deliverables is based on somebody else's work, make sure you cite it. If your research contains software artifacts in the same situation, make sure you work and publish _under the terms of the license_ of the respective project and that you **highlight this fact in your milestone documentation** and in the source code if applicable! **Teams that submit others' work without attributing it will be immediately terminated.**

### Overview

- **Total Estimated Duration:** Duration of the whole project (e.g. 2 months)
- **Full-Time Equivalent (FTE):**  Average number of full-time employees working on the project throughout its duration (see [Wikipedia](https://en.wikipedia.org/wiki/Full-time_equivalent), e.g. 2 FTE)
- **Total Costs:** Requested amount in USD for the whole project (e.g. 12,000 USD). Note that the acceptance criteria and additional benefits vary depending on the [level](../README.md#level_slider-levels) of funding requested. This and the costs for each milestone need to be provided in USD; if the grant is paid out in Bitcoin, the amount will be calculated according to the exchange rate at the time of payment.

### Milestone 1 Example — Literature Review and Data Collection

- **Estimated duration:** 1 month
- **FTE:**  1,5
- **Costs:** 8,000 USD

> :exclamation: **The default deliverables 0a-0e below are mandatory for all milestones**.

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | Copyright and Licenses | CC0 / CC BY 4.0 / Apache 2.0 / GPLv3 / MIT / Unlicense |
| **0b.** | Documentation/Tutorial | We will provide both **artifacts documentation** of the deliverables and a basic **tutorial** that explains how a user can (for example) execute the code included or can visualize data or use any artifacts included. |
| **0c.** | Methodology | Detailed explanation of how the results were achieved and how to reproduce/verify the results. |
| **0d.** | Infrastructure | We will provide the list of all infrastructure requirements (text editors with proper versions, software packages, data packages, etc) that can be used to verify the deliveries with this milestone. Ideally, we recommend the usage of LaTeX/Overleaf for article production and Docker files for software execution. |
| **0e.** | Article | We will send an **article** or part of it (with source code) that explains in the English language [...] (what was done/achieved as part of the grant). (Content, language and medium should reflect your target audience described above.). For level 2 and 3 grants, the article must contain the following statement in an acknowledgments section:  This work was supported by a research grant from the Web3 Foundation.  |
| 1. | List of academic papers regarding X | We will systematically search the literature about X and deliver a list of papers to read with web links to them |
| 2. | Data to be extracted from the papers | Data fields with the explanation of each that will be extracted from the papers ... |
| 3. | Analysis procedures | We gonna describe all the procedures planned for the analysis that will be conducted in the next milestone ... |


### Milestone 2 Example — Data Analysis

- **Estimated Duration:** 1 month
- **FTE:**  1,5
- **Costs:** 8,000 USD

...


## Future Plans

Please include here

- how you intend to use, enhance, promote and support your project in the short term, and
- the team's long-term plans and intentions in relation to it.

## Referral Program (optional) :moneybag: 

You can find more information about the program [here](../README.md#moneybag-referral-program).
- **Referrer:** Name of the Polkadot Ambassador or GitHub account of the Web3 Foundation grantee
- **Payment Address:** BTC, Ethereum (USDC/DAI) or Polkadot/Kusama (USDT) payment address. Please also specify the currency. (e.g. 0x8920... (DAI))

## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?** Web3 Foundation Website / Medium / Twitter / Element / Announcement by another team / personal recommendation / etc.

Here you can also add any additional information that you think is relevant to this application but isn't part of it already, such as:

- Work you have already done.
- If there are any other teams who have already contributed (financially) to the project.
- Previous grants you may have applied for.
