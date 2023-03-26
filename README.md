# EVM Multibase
Library and instanced smart contracts for doing encoding and decoding in different bases and the multibase format, on top of the EVM.

## Motivations

Projects that I'm working with either need on-chain or in EVM string encoding in different bases. Such as: on-chain functions and off-chain view of functions, strict validation of base encoded/decoded strings, content ID based URIs [such as IPFS](https://proto.school/anatomy-of-a-cid), or human typable or speakable identifiers. Combining the bases and multibase code into the same repo made sense to me to do as a library. This library suports both directly using the bases, multibase prefixes, ignoring validity checks and checking encoding validity.

## CS Philosophy, Methods, Design Choice and Patterns

- Lower level code is used. Soldity would use to much gas for my design goals.
- Minimize gas, I consider resource costs to be part of the security threat modelling. But don't comprimise security just for gas.
- (e)Wasm and eBPF will probably made in a different repo, but share code/work with this one.
- Push for secure code. (Use this code at your own risk, its not audited, and this is early code.)
- Allows by-passing some checks. In some cases some validations have no security risk.
- Default to checks being on. You should know what your doing and the impacts of turning on and off checks.
- Allow for use from solidity
- Initally prefer external calls. This reduces the attack surface of being the same EVM context and I would think make the stack depth more friendly.
- Prefer off-chain use. You probably should not even be using this library on-chain, except for exposing external views. Generating strings on chain can often be a bad idea. Except when doing so is needed for validation/ verifiability / security, gives better user experience (including economics such as cost), or frees the amount of work done on chain for other uses.
- The follwing solidity style ABI custom errors are used BaseNotImplemented(), BaseUnknown(), InvalidCharacters().
- FATD..D - This is something I have not published publicly yet. Leverages TDD in part. Acceptance is coverage mapped to the tests. Data and Test first when it makes sane sense to do so.

## [Multibases](https://github.com/multiformats/multibase) / Bases For MVP
| Left-aligned | Notes | Prefix |
| :---         |     :---:      |          ---: |
| base16upper | Both standard case insand non-star case senstive | F | 
| base16(lower) | hexadecimal | f |
| base16mixed | Not standard case-in-sensitive decoder | |
|base32| | b |
| base58btc| Bitcoin style base 58 | z |
| base64pad|| M |
| wordbase 2048 | Propsed [BIP-39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) like encoding  | wordbase2048 |
|||WORDBASE2048|
|||WordBase2048.|
| base256emoji | 256 Emoji Base | 🚀 |

## Basic Technology Stack
| Category | What | Use |
| :---         |     :---:      |          ---: |
| language   | Javascript | |
|| Bun | |
| language | Yul | |
| language | Huff | |
| language | Trim | |
| language | Solidity | |
| language | Fe | |
| language | Vyper | |
| language | Python | |
|| Jupyter Lab
|| Docker | |
|| VS Code Dev Containers | |
||Git | |
|| Github | |

## Installation

There is no installation steps yet. Still prototyping this. If you want to use it at your own peril, you may clone this repo or reference it in your imports.

## Use

## Repository Structure

### In Source Code. (Only the top/root folder. See more)
```
.
├── 📁 .devcontainer      # VS Code Development Container
├── 📁 .github/workflows  # Github Actions workflows (part of CI/CD) 
├── 📁 acceptance         # Acceptance criteria and more information about this repository.
├── 📁 analysis           # Jupyter Lab notebooks for data driven development and metaprogramming.
├── 📁 contracts          # Smart contract code is placed here.
├── 📁 examples           # Examples of how to use this code.
├── 📁 fractal            # Not for humans. Coverage map metadata source is sent to / updated from here 
├── 📁 test               # Tests that drive the development.
├── 🗒️ .env.example       # Example enviroment fil.e
├── 🗒️ .gitattributes     # Specifies the files and paths attributes that must be used by git.
├── 🗒️ .gitignore         # Intentionally untracked files and folder that Git must ignore.
├── 🗒️ .gitmodules        # Helps with inclusion of other repos.
├── 🗒️ CODE_OF_CONDUCT.md # Rules for the communtiy.
├── 🗒️ LICENSE            # MIT License.
├── 🗒️ README.md          # This file.
├── 🗒️ RICARDIAN.sigs     # Ricardian contract signatures of authors or contributors.
├── 🗒️ bun.lockb          # Bun's lock file.
├── 🗒️ bunfig.toml        # Bun's configuration file.
├── 🗒️ foundry.toml       # Configuration file for foundry / forge.
└── 🗒️ package.json       # Javascript and NPM repo metadata.
```

### In Builds (and CI/CD)
```
└── 📁 dist               # The builds ready for distribution go in this folder.
```

### File Extensions
| What is it? | Notes | File Extension |
| :---         |     :---:      |          ---: |
| fractal metadata and coverage map | git status     | \*.f.yml |
| fractal metadata and coverage map | git diff       | \*.f.\* |

## Contributions and Acknowledgements
### Authors
- Will Richards 2

## License
This software is available under the following licenses:

- MIT

## Disclaimer
