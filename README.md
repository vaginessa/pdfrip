<div align="center">
  <h1><code>PDFRip</code></h1>
  <p><strong>A multi-threaded PDF password cracking utility equipped with commonly encountered password format builders and dictionary attacks.</strong></p>
</div>

## 📖 Table of Contents

- [Introduction](#%E2%84%B9%EF%B8%8F-introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Contribution](#contribution)
- [License](#license)

## ℹ️ Introduction

**pdfrip** is a fast multithreaded PDF password cracking utility written in Rust with support for wordlist based dictionary attacks, date and number range bruteforcing, and a custom query builder for password formats.

<div align="center">
  <table>
    <tr>
      <td><img height="300" width="400" src="https://user-images.githubusercontent.com/26198477/153601211-e3be5dcb-17c4-425d-9259-65fe4b679290.png"></td>
    </tr>
  </table>
</div>

## Features

- **Fast:** Performs about 50k-100k+ passwords per second utilising full CPU cores.
- **Custom Query Builder:** You can write your own queries like `STRING{69-420}` with the `-q` option which would generate a wordlist with the full number range.
- **Date Bruteforce:** You can pass in an year as the input with the `-d` option which would bruteforce all 365 days of the year in `DDMMYYYY` format which is a pretty commonly used password format for PDFs.
- **Number Bruteforce:** Just give a number range like `5000-100000` with the `-n` option and it would bruteforce with the whole range.

## Installation

```
$ curl -L https://github.com/mufeedvh/pdfrip/releases/download/v1.0.0/pdfrip_amd64 -o pdfrip
```

(`Linux AMD x86-64`)

**OR**

Download the executable from [**Releases**](https://github.com/mufeedvh/pdfrip/releases) for your OS.

**OR**

Install with `cargo`:

    $ cargo install --git https://github.com/mufeedvh/pdfrip.git
    
[Install Rust/Cargo](https://rust-lang.org/tools/install)

## Build From Source

**Prerequisites:**

* [Git](https://git-scm.org/downloads)
* [Rust](https://rust-lang.org/tools/install)
* Cargo (Automatically installed when installing Rust)
* A C linker (Only for Linux, generally comes pre-installed)

```
$ git clone https://github.com/mufeedvh/pdfrip.git
$ cd pdfrip/
$ cargo build --release
```

The first command clones this repository into your local machine and the last two commands enters the directory and builds the source in release mode.

## Usage

Get a list of all the arguments:

    $ pdfrip --help
    
Start a dictionary attack with a wordlist **(-w/--wordlist)**:

    $ pdfrip encrypted.pdf -w rockyou.txt
    
Bruteforce number ranges for the password **(-n/--num-bruteforce)**:

    $ pdfrip encrypted.pdf -n 1000-9999
    
Bruteforce all dates in a year for the password in `DDMMYYYY` format **(-d/--date-bruteforce)**:

    $ pdfrip encrypted.pdf -d 1999
    
Build a custom query to generate a wordlist **(-q/--custom-query)**: (useful when you know the password format)

    $ pdfrip encrypted.pdf -q ALICE{1000-9999}
    
    $ pdfrip encrypted.pdf -q DOC-ID{0-99}-FILE
    
Enable preceding zeros for custom queries **(-z/--add-preceding-zeros)**: (which would make `{10-5000}` to `{0010-5000}` matching the end range's digits)

    $ pdfrip encrypted.pdf -q ALICE{10-9999} --add-preceding-zeros

## Contribution

Ways to contribute:

- Suggest a feature
- Report a bug
- Fix something and open a pull request
- Help me document the code
- Spread the word

## License

Licensed under the MIT License, see <a href="https://github.com/mufeedvh/pdfrip/blob/master/LICENSE">LICENSE</a> for more information.
