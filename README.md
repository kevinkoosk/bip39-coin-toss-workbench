# BIP-39 Coin-Toss Workbench

An offline, educational Tkinter application that converts 256 manually generated binary outcomes into a 24-word BIP-39 mnemonic.

The application is designed around a simple physical exercise:

> Toss 16 numbered coins or tokens over 16 rounds to generate 256 entropy bits.

It validates the recorded outcomes, calculates the BIP-39 SHA-256 checksum and displays the corresponding BIP-39 word-list positions and English words.

## Purpose

This project was created to make BIP-39 entropy and checksum generation easier to understand.

Instead of treating a recovery phrase as something mysteriously generated inside a wallet, the application shows how:

1. Physical coin outcomes produce 256 random bits.
2. SHA-256 produces an eight-bit checksum.
3. The resulting 264 bits are divided into 24 groups of 11 bits.
4. Each 11-bit group identifies one of the 2,048 words in the BIP-39 English word list.

The application deliberately exposes the final three entropy bits, eight checksum bits and complete final 11-bit word group.

## Features

* Accepts 16 rounds of 16 outcomes.
* Supports `0` or `O` for zero.
* Supports `1` or `X` for one.
* Allows spaces between recorded outcomes.
* Checks every round for missing, excessive or invalid input.
* Highlights fields containing errors.
* Refuses to process incomplete or malformed input.
* Calculates the eight-bit checksum using SHA-256.
* Separately displays the final three random bits.
* Displays all 24 11-bit groups.
* Displays each internal BIP-39 index.
* Displays the corresponding printed word-list position.
* Displays the corresponding English BIP-39 word.
* Includes the official 2,048-word English list.
* Requires no network connection or third-party Python packages.
* Provides vertically and horizontally scrollable content.
* Supports resizable windows and smaller displays.
* Performs an internal BIP-39 self-test before opening.

## Requirements

* Python 3.9 or later
* Tkinter

Tkinter is normally included with standard Python installations on Windows and macOS.

Some Linux distributions require it to be installed separately. On Debian or Ubuntu:

```bash
sudo apt install python3-tk
```

## Running the application

Download `bip39_coin_tkinter.py`.

On Windows:

```powershell
py bip39_coin_tkinter.py
```

Alternatively:

```powershell
python bip39_coin_tkinter.py
```

On Linux or macOS:

```bash
python3 bip39_coin_tkinter.py
```

## Recording the coin outcomes

Number 16 identical coins or tokens from 1 to 16.

Give each token two distinguishable faces:

* `O` represents `0`.
* `X` represents `1`.

For every round:

1. Toss all 16 tokens.
2. Arrange them in numerical order.
3. Record their outcomes from token 1 through token 16.
4. Enter the resulting 16-character sequence into the corresponding field.

Repeat this process for all 16 rounds.

The ordering is:

```text
Round 1, tokens 1–16
Round 2, tokens 1–16
...
Round 16, tokens 1–16
```

This produces:

```text
16 tokens × 16 rounds = 256 entropy bits
```

## How the checksum works

The complete 256-bit sequence is converted into 32 bytes and processed using SHA-256.

For a 24-word BIP-39 mnemonic, the first eight bits of the SHA-256 result become the checksum:

```text
256 entropy bits + 8 checksum bits = 264 bits
```

The 264 bits are then divided into 24 groups:

```text
264 ÷ 11 = 24 groups
```

Each 11-bit group has a value between 0 and 2047 and therefore identifies one of the 2,048 BIP-39 words.

The first 23 word groups use 253 entropy bits. The final word group consists of:

```text
3 remaining entropy bits + 8 checksum bits
```

## Built-in verification

The application tests itself against the established all-zero BIP-39 example before opening.

For 256 zero bits, the correct result is:

* Checksum: `01100110`
* First 23 words: `abandon`
* Final word: `art`

If this internal test fails, the interface will not open.

## Security warning

This project is an educational prototype. It has not undergone an independent security audit.

A recovery phrase can provide complete control over the associated cryptocurrency wallet. Anyone who obtains the phrase—or the original entropy used to generate it—may be able to control the wallet and its assets.

If experimenting with real wallet generation:

* Use a genuinely offline and trusted computer.
* Do not photograph the coin outcomes.
* Do not upload the outcomes or generated words.
* Do not enter them into cloud-based tools.
* Do not copy them through an internet-connected clipboard.
* Independently review the source code.
* Verify the result using a separate trusted implementation.
* Perform a complete wallet recovery test before transferring assets.
* Never rely on this software as the sole source of security advice.

The author and contributors make no representation that this application is suitable for securing assets of real value.

## Privacy

The application:

* Does not require an internet connection.
* Does not transmit the entered data.
* Does not automatically save the entropy or mnemonic.
* Does not contain analytics or telemetry.
* Does not automatically copy the result to the clipboard.

These properties do not protect against a compromised operating system, malicious software, screen recording, clipboard monitoring or physical observation.

## Project origin

This project began as a learning exercise by Malaysian lawyer and trainer Kevin Koo, exploring whether numbered physical coins or tokens could provide understandable, auditable entropy for BIP-39 mnemonic generation.

The concept, security model and interface were developed through an extended dialogue about physical randomness, binary representation, SHA-256 checksums, human error and offline wallet generation.

## Creation and attribution

Created by **Kevin Koo**, in collaboration with **ChatGPT and Codex by OpenAI**.

Kevin conceived the numbered-token method, directed the design, tested the explanations and made the substantive project decisions. ChatGPT and Codex assisted with cryptographic explanation, design review, Python implementation, validation logic, interface structure and documentation.

Kevin reviewed the generated work and takes responsibility for the decision to publish and maintain this repository.

OpenAI does not sponsor, endorse or maintain this project.

## Word-list attribution

The embedded English word list comes from the official BIP-39 repository:

https://github.com/bitcoin/bips/blob/master/bip-0039/english.txt

BIP-39 was authored by Marek Palatinus, Pavol Rusnak, Aaron Voisine and Sean Bowe.

## Contributing

Corrections, security observations, usability improvements and educational suggestions are welcome.

Please do not submit real recovery phrases, wallet secrets or entropy records in issues, discussions, screenshots, examples or test cases.

Security-sensitive observations should be disclosed privately to the repository maintainer before public discussion.

## Licence

This project is released under the MIT License.

Copyright © 2026 Kevin Koo
