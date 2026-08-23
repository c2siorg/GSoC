# Project Name

**LensMint Web3 Camera** (`lensmint-camera`)

**Contributor:** Guansan Qin (Tenerife)  
**GitHub:** [Tenerife-Q](https://github.com/Tenerife-Q)  
**Email:** tenerifesea189@gmail.com  
**Organization:** C2SI  
**Mentor:** Mohit Bhat  
**GSoC:** 2026 · ~350h track

---

# Project Abstract

LensMint is a camera built on a Raspberry Pi. It takes a photo, signs a small provenance record with a key that never leaves the board, and can mint that photo on Sepolia or Solana devnet. Everything on the device runs as one Rust program.

The starting problem is simple to state. A photo that travels through IPFS, Filecoin, or any gateway usually gets re-encoded, and its SHA-256 changes completely. The picture still looks the same to a person, but the digest no longer matches what the camera recorded. A perceptual hash survives that. So the season's ZK work proves a statement about the perceptual hash instead of the file bytes.

The RISC Zero guest checks one statement with two conditions:

1. an Ed25519 signature, made at shutter time, over the message `uuid|sha256|phash`
2. `Hamming(pHash0, pHash1) <= 5`

The JPEG bytes never enter the circuit. So the proof says this camera key signed this record when the shutter fired, and a later perceptual hash is still close to the one signed at capture. It doesn't say the photo is real, and it is not an AI or deepfake detector.

Three machines are involved, and keeping them separate is the main architectural decision of the season. The Pi captures, signs, gates, and mints. Groth16 proving takes minutes and heats the board, so it runs on a PC. Public verification of the seal is a second Sepolia transaction that has nothing to do with the mint transaction.

The work came in two phases, which follows how my mentor wanted the summer split:

1. **Phase 1** — the camera itself: an `egui` UI on the Pi, an Ed25519 keystore, dual-track storage, and minting on EVM and Solana from the same daemon.
2. **Phase 2** — the proof path: a signed HashRecord at capture, off-device proving, a local mint gate that refuses to mint without proof files, and a Sepolia verifier contract.

One correction is worth recording here, because it shaped the second half. My mentor asked for a Rust-only runtime. I read that as the GUI, so the mid-term mint path still went through a TypeScript relayer. He pointed at it during a review, and minting moved into the daemon in [Issue 87](https://github.com/c2siorg/lensmint-camera/issues/87) and [PR 88](https://github.com/c2siorg/lensmint-camera/pull/88).

A longer written guide, with the starting guide for the next contributor, is linked at the end of this report.

---

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/OOjxLTXb)

## [GSoC Project Proposal](https://drive.google.com/file/d/1j6C9l34ljod8-WMcQ_kfm05lISQixnAk/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/lensmint-camera)

## [GitHub Personal Repo](https://github.com/Tenerife-Q/lensmint-camera)

## [Commits during GSoC 2026](https://github.com/c2siorg/lensmint-camera/commits/gsoc2026-tenerife?author=Tenerife-Q)

## [Project Demo Video](https://drive.google.com/file/d/1sC3sLav34UYtZb6b2B4belUimy_x9D1Z/view?usp=sharing)

- **Full walkthrough:** [Drive](https://drive.google.com/file/d/1sC3sLav34UYtZb6b2B4belUimy_x9D1Z/view?usp=sharing) — shutter on the Pi, prove on a laptop, mint, then verify on Sepolia (capture `ecc4527c-b550-4695-ac62-5f2bd8f0f759`)
- **Short overview:** [Drive](https://drive.google.com/file/d/1TnQTV4MagZ2YkhhMRzhxviGnm3gM2znn/view?usp=sharing)

## [Project Wiki](https://www.notion.so/GSoC-2026-LensMint-Board-Tenerife-35428e1a4d678059b2e5e52874e1f920)

Task board I kept during the season. The issues and pull requests themselves are listed in Work Summary.

## [GSoC Blog](https://medium.com/@tenerifesea189)

- [DevLog 1: Native Rust GUI on a Bare-Metal Raspberry Pi](https://medium.com/@tenerifesea189/lensmint-devlog-1-running-a-native-rust-gui-on-a-bare-metal-raspberry-pi-bf24c5d0067b)
- [DevLog 2: Hitting the Hardware Bottom](https://medium.com/@tenerifesea189/lensmint-devlog-2-hitting-the-hardware-bottom-week-1-2-61bb8a5bfccc)
- [DevLog 3: You Can't Software-Update Physics](https://medium.com/@tenerifesea189/lensmint-devlog-3-you-cant-software-update-physics-week-3-4-9212cdd9f0ec)
- [DevLog 4: From Shutter to Blockchain](https://medium.com/@tenerifesea189/lensmint-devlog-4-from-shutter-to-blockchain-week-5-6-mid-term-c75a1fab6edc)
- [DevLog 5: Edge Cases, One Daemon](https://medium.com/@tenerifesea189/lensmint-devlog-5-edge-cases-one-daemon-post-mid-term-aab4c2c45829)
- [DevLog 6: Making Authenticity Public](https://blog.c2si.org/lensmint-devlog-6-making-authenticity-public-phase-2-zk-4f2673c01d8c)

---

# Work Summary

Phase 1 delivered the camera and the mint path. Phase 2 delivered the proof path on top of it. The tables below list the issues and pull requests.

### Phase 2 — ZK authenticity

| Description | Issue | PR |
|---|---|---|
| Signed HashRecord written next to the JPEG at capture time | [#89](https://github.com/c2siorg/lensmint-camera/issues/89) | [#90](https://github.com/c2siorg/lensmint-camera/pull/90) |
| RISC Zero guest: Ed25519 signature and Hamming distance, with the JPEG kept out of the circuit | [#91](https://github.com/c2siorg/lensmint-camera/issues/91) | [#92](https://github.com/c2siorg/lensmint-camera/pull/92) |
| Host prove command, receipt and journal output, and timing benchmarks | [#93](https://github.com/c2siorg/lensmint-camera/issues/93) | [#94](https://github.com/c2siorg/lensmint-camera/pull/94) |
| Mint gate that refuses to mint without matching proof files, on both chains | [#95](https://github.com/c2siorg/lensmint-camera/issues/95) | [#96](https://github.com/c2siorg/lensmint-camera/pull/96) |
| `AuthenticityVerifier` on Sepolia, verified through the RISC Zero Router | [#97](https://github.com/c2siorg/lensmint-camera/issues/97) | [#98](https://github.com/c2siorg/lensmint-camera/pull/98) |

### Phase 1 — camera, keys, and minting

| Issue | PR | What it covers |
|---|---|---|
| [#54](https://github.com/c2siorg/lensmint-camera/issues/54) | [#55](https://github.com/c2siorg/lensmint-camera/pull/55) | AArch64 build so `eframe` links on the Pi |
| [#56](https://github.com/c2siorg/lensmint-camera/issues/56) | [#57](https://github.com/c2siorg/lensmint-camera/pull/57) | Event-driven `egui` spike |
| [#58](https://github.com/c2siorg/lensmint-camera/issues/58) | [#60](https://github.com/c2siorg/lensmint-camera/pull/60) | Viewfinder, gallery, and a bounded command channel |
| [#59](https://github.com/c2siorg/lensmint-camera/issues/59) | [#61](https://github.com/c2siorg/lensmint-camera/pull/61) | Ed25519 `keystore.pem` created with mode `0400` |
| [#62](https://github.com/c2siorg/lensmint-camera/issues/62) | [#64](https://github.com/c2siorg/lensmint-camera/pull/64) | V4L2 `mmap` capture into `egui` textures |
| [#63](https://github.com/c2siorg/lensmint-camera/issues/63) | [#65](https://github.com/c2siorg/lensmint-camera/pull/65) | Zoom and focus `ioctl` controls with UI rollback when the hardware refuses |
| [#66](https://github.com/c2siorg/lensmint-camera/issues/66) | [#68](https://github.com/c2siorg/lensmint-camera/pull/68) | Dual-track storage: full JPEG on disk, thumbnails in `sled` |
| [#67](https://github.com/c2siorg/lensmint-camera/issues/67) | [#69](https://github.com/c2siorg/lensmint-camera/pull/69) | Gallery grid and cascade delete |
| [#70](https://github.com/c2siorg/lensmint-camera/issues/70) | [#71](https://github.com/c2siorg/lensmint-camera/pull/71) | Video recording through `ffmpeg`, and on-screen zoom buttons |
| [#72](https://github.com/c2siorg/lensmint-camera/issues/72) | [#73](https://github.com/c2siorg/lensmint-camera/pull/73) | Gradient pHash computed alongside SHA-256 |
| [#74](https://github.com/c2siorg/lensmint-camera/issues/74) | [#75](https://github.com/c2siorg/lensmint-camera/pull/75) | Metadata JSON and local envelope signing |
| [#77](https://github.com/c2siorg/lensmint-camera/issues/77) | [#78](https://github.com/c2siorg/lensmint-camera/pull/78) | Chain selection and mint status in the UI |
| [#79](https://github.com/c2siorg/lensmint-camera/issues/79) | [#81](https://github.com/c2siorg/lensmint-camera/pull/81) | Retry and backoff against the mint API of that stage |
| [#80](https://github.com/c2siorg/lensmint-camera/issues/80) | [#82](https://github.com/c2siorg/lensmint-camera/pull/82) | Camera overlay, gallery, and settings screens |
| [#83](https://github.com/c2siorg/lensmint-camera/issues/83) | [#84](https://github.com/c2siorg/lensmint-camera/pull/84) | TypeScript relayer backend. This was the mid-term path and is no longer part of the runtime. |
| [#85](https://github.com/c2siorg/lensmint-camera/issues/85) | [#86](https://github.com/c2siorg/lensmint-camera/pull/86) | ERC-721 contract and Anchor program, still called through the relayer that week |
| [#87](https://github.com/c2siorg/lensmint-camera/issues/87) | [#88](https://github.com/c2siorg/lensmint-camera/pull/88) | Minting moved into the Rust daemon: in-process EVM and Solana adapters, a mint queue, nonce and gas limits, and an idempotency key |

### Documentation and tests

| Description | PR |
|---|---|
| Technical documentation and contributor starting guide | [#99](https://github.com/c2siorg/lensmint-camera/pull/99) |
| Tests for the mint gate, config loading, journal encoding, and verifier bounds | [#100](https://github.com/c2siorg/lensmint-camera/pull/100) |

The early measurements behind the pHash choice are in [Issue #38](https://github.com/c2siorg/lensmint-camera/issues/38) and [PR #45](https://github.com/c2siorg/lensmint-camera/pull/45), with the scripts in [lensmint-research-lab](https://github.com/Tenerife-Q/lensmint-research-lab). After a 95% JPEG re-encode the SHA-256 changed completely while the Gradient pHash distance stayed at 2, which is where the threshold of 5 comes from.

---

# What Covered

## The camera daemon

<img width="1786" height="837" alt="main" src="https://github.com/user-attachments/assets/5c573c4f-98f9-4cff-a1fa-00760b4b6cc1" />

One Rust process on the Pi owns the UI, the camera, storage, the device key, and minting.

The UI thread only draws. It sends commands over a bounded channel with `try_send`, so an SD-card write or a slow RPC call can't freeze the viewfinder. Frames come from V4L2 through `mmap` into an `egui` texture. When the lens refuses a focus request with `ENOTTY` or `EBUSY`, the slider returns to the last real hardware value rather than showing a state the camera isn't in. Preview zoom is a texture crop, and the signed JPEG stays the uncropped frame.

Storage is split in two, because writing and reading full JPEGs on an SD card is slow enough to be visible in the UI. Full images go to disk, and small thumbnails live in a `sled` database that backs the gallery. Deleting a photo removes the image, its thumbnail, and any sidecar files that belong to it.

Identity is deliberately separate from money. `keystore.pem` holds the Ed25519 camera key and is created with mode `0400`. The EVM and Solana gas wallets are different files. The contracts record the camera public key as the device identity, not the address that paid for the transaction.

Minting runs in the daemon itself. `MintQueue` serializes requests, the key `{chain}-{sha256}` stops the same photo from being broadcast twice on the same chain, the EVM adapter pins the nonce and caps replacement gas bumps, and the RPC pool moves to another endpoint when one fails. Sepolia goes through `LensMint.mintFromHardware`, and Solana devnet through the Anchor `mint_from_hardware` instruction with Metaplex Core. [DevLog 5](https://medium.com/@tenerifesea189/lensmint-devlog-5-edge-cases-one-daemon-post-mid-term-aab4c2c45829) covers this part.

## The authenticity path

<img width="1536" height="1024" alt="blog-zk-architecture-final" src="https://github.com/user-attachments/assets/f56b9233-7b8a-4f1a-836f-5b5d977f35e4" />

When the shutter fires, the daemon writes `{uuid}.hash.json` next to the JPEG. It holds the UUID, the SHA-256, the capture pHash, the device public key, and a signature over `uuid|sha256|phash`. This happens off the preview loop.

Proving happens on another machine. The host recompresses the image, computes the later perceptual hash, and runs the guest. On the demo laptop a proof took about 5.7 minutes (`prove_wall_ms=344084`) and produced a 945-byte receipt at distance 1. The host writes the receipt, a JSON journal for the Pi, and a packed ABI journal for the contract.

Back on the Pi, the mint gate reads local files only. It checks the signature on the record, requires a non-empty receipt, and compares the journal fields against the record. It does not run Groth16, and it is not a substitute for the on-chain check. Both chains use this same gate. If the files are missing or don't match, the mint is refused.

Public verification is a separate Sepolia transaction. `AuthenticityVerifier` takes the seal and the ABI journal and asks the RISC Zero Router to verify them against the guest `IMAGE_ID`. `IMAGE_ID` identifies the compiled guest program, which is the same for every proof from that build. The photo's own digest is the SHA-256 inside the HashRecord. [DevLog 6](https://blog.c2si.org/lensmint-devlog-6-making-authenticity-public-phase-2-zk-4f2673c01d8c) walks through the encodings.

### End-to-end run on real hardware

Shutter on the Pi, prove on a laptop, mint, then verify. This used the camera's own keystore, not a host fixture.

| Item | Value |
|---|---|
| Capture UUID | `ecc4527c-b550-4695-ac62-5f2bd8f0f759` |
| Guest `IMAGE_ID` (program id, not the photo digest) | `0xce0407dc8cd448f4c56f285dd5faa6eeb2bb715c95644ebaec7e46ea5b35f163` |
| Mint transaction | [Sepolia](https://sepolia.etherscan.io/tx/0x83482970433a1f1b1aca6b1b694e6c63da35a242f8d74a4e8269e37a64a8d0ee) |
| Verification transaction | [Sepolia](https://sepolia.etherscan.io/tx/0x699bf0c0c784890cb34f8aada498f810f472c11297f88f6e2704be9d63118606) |
| Verifier contract | [`0xD2f3E1AB4d685956461F342EbeABEaE585D76927`](https://sepolia.etherscan.io/address/0xD2f3E1AB4d685956461F342EbeABEaE585D76927) |

Two transactions, two different meanings. A successful mint means the local gate passed. The seal is only verified by the second one.

---

# What left

**No service to request a proof.** Today the JPEG and the HashRecord are copied from the Pi to the proving machine by hand, and the receipt is copied back. A small web service could take a HashRecord, run the guest, and return the receipt. The trust split would not change: the Pi signs, a host proves, and Sepolia checks the seal.

**No Solana verifier.** Solana uses the same local gate before minting, but this phase deployed no on-chain Groth16 verifier there, so public seal verification is Sepolia only. A follow-up can reuse the same guest statement.

**Limits inside the current proof.** The host does not check that the JPEG it was given matches the SHA-256 in the record before proving, and it has a fallback that produces a synthetic distance when no tested recompression quality lands under the threshold. So the guest proves the signature and the relationship between two hashes it was handed. Tightening that binding is the next real piece of work on the circuit.

**Product gaps I would fix first.** The UI has no recipient field, so an EVM mint goes to the gas wallet. The checked-in config only carries Sepolia and Solana devnet addresses, so another network needs a deployment and a config entry rather than just a menu choice. Videos are recorded and shown in the gallery but have no HashRecord, so the gate refuses to mint them.

**Out of scope this season.** Proving on the Pi, IPFS or Filecoin as a required path, and the fuzz tests and device registry from the original proposal.

---

# Challenges and lessons

The first V4L2 frames came out torn on a diagonal, in green and purple. I spent a while on stride settings before finding that the Rust `v4l2_format` struct was missing a 4-byte pad that the kernel C layout has on AArch64. That was the moment the project stopped being ordinary application work.

Proving forced an architectural choice rather than an optimization. Groth16 on the Pi is minutes and heat, and no camera can freeze that long, so the proof had to leave the board and the mint gate had to work on files instead.

The on-chain side had its own encoding surprises. The verifier wants a 260-byte Router seal, not the raw Groth16 bytes, and the guest commits a fixed ABI journal for the contract while the Pi reads the same fields as JSON. Same statement, two encodings, and changing what the guest commits changes `IMAGE_ID`.

---

# Technical documentation

The written guide for the next contributor covers the features, how the modules connect, the architecture diagrams, the hardware notes, and how to run the daemon and the proof flow:

**[LensMint GSoC 2026 documentation](https://github.com/Tenerife-Q/lensmint-camera/blob/916c34314b8d2229a3b69cc6fce151e0eef5d22e/docs/gsoc-2026/README.md)**
