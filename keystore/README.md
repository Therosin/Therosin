# 🔐 Public Keys

This directory contains public keys that can be used to verify any signed content from me.

## 📜 What's here

- `theros-codesign.crt`  
  My self-signed X.509 certificate used to sign `.dll`, `.exe`, and other binaries.  
  Signed using `osslsigncode`, and verifiable with standard tools.

- `theros.asc`  
  My PGP public key, exported in ASCII format.  
  Used for signing packages, messages, and other plaintext content.

| Key Type   | Fingerprint                                         |
| ---------- | --------------------------------------------------- |
| X.509 Cert | `410B D31C 0378 6AE5 5BA8 6E83 F637 8A4F 0BCC BE02` |
| PGP Key    | `2EAD EB18 992E B625 3655 A961 8F2A 33B8 F0AC 9061` |

---

## ✅ Verifying signed files

### 🛠 Code-signed DLLs and executables

Use [`osslsigncode`](https://github.com/mtrojnar/osslsigncode) to verify a signed binary:

```bash
osslsigncode verify -ignore-crl -CAfile theros-codesign.crt -in path/to/target
```
You should see:
- Signature OK
- Certificate subject CN=Theros, emailAddress=theros@svaltek.xyz
- Matching SHA256 digest
  
> NOTE: `-ignore-crl` is used to skip checking CertificateAuthority, It's a self signed key (I Dont have money to burn on buying codesigning certs, maybe in future)
> Windows will NOT trust my signed files, unless you manually set them as trusted (not recommended).

### PGP signed content

- If on windows use ['Gpg4win'](https://www.gpg4win.org)
- Linux users can use OpenPGP

```bash
gpg --import theros.asc
gpg --verify file.zip.asc file.zip
```
You should see:
- Good signature from "Theros <theros@svaltek.xyz>"
- The fingerprint should match the one in this repo.
