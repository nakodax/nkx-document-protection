<p align="center">
  <a href="https://nakodax.com/documents">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://nakodax.com/branding/nakodax-lockup.svg">
      <img alt="NakodaX" src="https://nakodax.com/branding/nakodax-lockup-on-light.svg" width="260">
    </picture>
  </a>
</p>

# NakodaX Document Protection: an encrypted codebase, left in public

![Encryption: AES-256-GCM](https://img.shields.io/badge/encryption-AES--256--GCM-00B26D) ![Protected files: 559](https://img.shields.io/badge/protected%20files-559-00B26D) ![Licence: proprietary](https://img.shields.io/badge/licence-proprietary-555) ![Works with Google Drive, SharePoint, OneDrive and Dropbox](https://img.shields.io/badge/works%20with-Drive%20%7C%20SharePoint%20%7C%20OneDrive%20%7C%20Dropbox-555)

**We protect our own code with NakodaX. This repository is what that looks like from the outside.**

NakodaX Document Protection keeps control of a file after you send it: revoke access, set an expiry or limit opens, even once it has been downloaded or forwarded. This repository holds the Document Protection codebase, encrypted with NakodaX Source Protection. Clone it, open any file, and see what someone without a licence sees.

<p align="center">
  <img src="https://nakodax.com/illustrations/documents-hero.webp" width="100%" alt="A protected document lifting out of an open box of files on a glowing green thread, still connected to the box: NakodaX Document Protection keeps control of a file after it is shared.">
</p>

[Product page](https://nakodax.com/documents) · [Security at NakodaX](https://nakodax.com/security) · [Request review access](ACCESS.md) · [Unlock a protected app yourself: nkx-sample-app](https://github.com/nakodax/nkx-sample-app) · [Report a security issue](SECURITY.md)

## What is NakodaX Document Protection?

NakodaX Document Protection is document DRM for the files you share outside your company. Files are encrypted in the browser before upload and shared through links you control. You can set an expiry, limit how many times a file opens, share only selected pages, slides, rows or columns, and revoke access after the file has been sent. Recipients do not need an account.

## What can you do with NakodaX Document Protection?

- **Revoke access after a file has been sent**, downloaded or forwarded.
- **Set an expiry date**, and **limit how many times** a document can be opened.
- **Share selected pages, slides, rows or columns**, not the whole file.
- **Encrypt files in the browser before upload**, so the readable file never reaches NakodaX servers.
- **Let recipients open protected files without creating an account.**
- **See document-level analytics** for opens and usage.
- **Protect email attachments, photos and video** the same way, with access you can end at any time.
- **Work from Google Drive, Microsoft SharePoint, OneDrive, Google Photos and Dropbox.**

## This repository at a glance

| | |
|---|---|
| **Product** | NakodaX Document Protection, by NakodaX |
| **What this repository holds** | The Document Protection codebase: API, web app, browser extension and tools |
| **What is protected** | 559 files: TypeScript, TSX, Python and SQL source, plus tests, docs, scripts and config |
| **What stays readable** | Folder and file names, this README, `LICENSE`, `ACCESS.md`, `SECURITY.md`, `.gitignore`, the four browser extension icons, and the `.nkx/manifest.json` files |
| **Protected with** | [NakodaX Source Protection](https://github.com/nakodax/nkx-source-protection) |
| **Encryption** | AES-256-GCM, with a separate random key for every file |
| **Key protection** | Each file key is wrapped with a key derived by scrypt (N = 2^17, r = 8, p = 1) and then bound to this build with HKDF-SHA256 |
| **Tamper resistance** | Every ciphertext is bound to its own file path, so renaming or swapping files makes decryption fail |
| **Encrypted files on disk** | `.nkxc`, one per protected file, plus companion stubs used by NakodaX tooling |
| **Licence** | Proprietary, public to inspect, not open source. See [`LICENSE`](LICENSE) |
| **Contact** | support@nakodax.com |

## How does NakodaX Document Protection work?

1. **Protect at the source.** The file is encrypted in your browser before it is uploaded.
2. **Share as needed.** Send a protected link by email, from cloud storage, or from NakodaX.
3. **Check permission at every open.** Each time the file is opened, NakodaX confirms that access is still allowed.
4. **Change access at any time.** Revoke, limit, extend or expire access, even after the file has been shared, downloaded or forwarded.

## What can someone see in this repository without a key?

- **The layout.** Folder and file names are readable, as in any NakodaX protected repository.
- **Ciphertext.** Every `.nkxc` file is random-looking bytes. There is no code, comment or string to read.
- **The manifest.** `.nkx/manifest.json` lists each protected file with its wrapped key, its hashes and its language. Every file key in it is wrapped, and is useless without a valid NakodaX licence.
- **These documents:** this README, [`LICENSE`](LICENSE), [`ACCESS.md`](ACCESS.md), [`SECURITY.md`](SECURITY.md) and `.gitignore`, plus the four icon images of the browser extension.

## Check it yourself in one minute

```bash
git clone https://github.com/nakodax/nkx-document-protection.git
cd nkx-document-protection

# Count the encrypted files
git ls-files '*.nkxc' | wc -l

# Look inside one: random bytes, no source code
head -c 96 apps/api/src/app.ts.nkxc | xxd

# Search every encrypted file for code keywords: no matches
grep -l -a -E '^(import|export|def|class|function) ' -r --include='*.nkxc' . | wc -l
```

**About this snapshot.** This repository is published as a single squashed commit of a protected release (November 2026). Development history and individual commits are not included in public snapshots.

## Who is NakodaX Document Protection for?

- **Teams that send contracts, board packs, pricing or due-diligence files** outside the company.
- **Anyone who has needed to un-send a file.**
- **People sharing from Google Drive, SharePoint, OneDrive or Dropbox** who want control after the share.
- **Founders and deal teams running a data room**, who need to know who opened what and to end access when the deal closes.

## How is this different from other ways to share files?

| Approach | Revoke after download? | Expiry or open limits? | Recipient needs an account? |
|---|---|---|---|
| **NakodaX Document Protection** | Yes | Yes | No |
| Email attachment | No | No | No |
| Password-protected file | No, once the password is shared | No | No |
| Cloud storage share link | The link can be turned off, but downloaded copies stay | Depends on the service | Depends on the service |

## Frequently asked questions

### What is NakodaX Document Protection?

NakodaX Document Protection is a NakodaX product that protects files before you share them. You can revoke access, set an expiry or limit opens after the file is out, and recipients do not need an account.

### Can I revoke access to a file after I have sent it?

Yes. Every open checks that access is still allowed, so you can end access after the file has been shared, downloaded or forwarded.

### Do recipients need a NakodaX account?

No. Recipients open protected files without creating an account.

### Can NakodaX read my documents?

No. Files are encrypted in your browser before upload, so the readable file never reaches NakodaX servers.

### How is this different from password-protecting a file?

A password protects a file only until someone shares the password or the file. NakodaX checks permission every time the content is opened, so you can revoke access after it has been sent, forwarded or downloaded.

### Which storage services does it work with?

Google Drive, Microsoft SharePoint, OneDrive, Google Photos and Dropbox. See [nakodax.com/documents](https://nakodax.com/documents) for the current list.

### Is this repository open source?

No. It is public, not open source. You can clone it and read the five documents and the manifest. You may not decrypt, copy or redistribute the protected files, or use them to train AI models. See [`LICENSE`](LICENSE).

### Can an AI model or LLM read this repository?

No. Without a licence key, the protected files are ciphertext. An AI model, a code search index or a scraper learns nothing from them beyond file names.

### How do I get access to review the code?

Email **support@nakodax.com** with the subject `Source review: nkx-document-protection`. Customers, prospective customers, investors, auditors and security researchers with a specific question are reviewed case by case. [`ACCESS.md`](ACCESS.md) has the details.

## Key terms

- **Document DRM:** controls that stay with a file after it is shared, such as revoking access, expiry and open limits.
- **Protected link:** the link a recipient uses to open a NakodaX protected file. Access is checked at every open.
- **`.nkxc` file:** one source file's ciphertext. Useless without the manifest and a valid licence.
- **Manifest (`.nkx/manifest.json`):** the list of protected files, with each file's wrapped key and hashes.

## Related

- [nkx-upload](https://github.com/nakodax/nkx-upload): encrypt and upload large video and audio from the command line
- [nkx-source-protection](https://github.com/nakodax/nkx-source-protection): NakodaX Source Protection, the product that encrypts this repository, protected the same way
- [nkx-data-protection](https://github.com/nakodax/nkx-data-protection): NakodaX Data Pipelines, protected the same way
- [nkx-sample-app](https://github.com/nakodax/nkx-sample-app): see protection run, with a public trial key
- Website: [nakodax.com](https://nakodax.com) · Platform: [box.nakodax.com](https://box.nakodax.com) · Support: [nakodax.com/support](https://nakodax.com/support)

## Security and compliance

- **CSA STAR Level 1:** [listed on the CSA STAR Registry](https://cloudsecurityalliance.org/star/registry/nakodax-technologies-private-limited/services/nakodax), with our CAIQ answers public.
- **ISO/IEC 5230 and ISO/IEC 18974:** open source licence compliance and open source security assurance, [listed by OpenChain](https://openchainproject.org/community-of-conformance) ([announcement](https://openchainproject.org/news/2026/11/05/nakodax-announces-an-openchain-conformant-program)).
- **NIST CSF 2.0:** self-assessed alignment across all 22 categories, updated every quarter.
- **NIST SSDF (SP 800-218):** our software development practices are self-assessed against the Secure Software Development Framework.

Full details are on [nakodax.com/security](https://nakodax.com/security). For security documentation or a questionnaire, email security@nakodax.com.

## Security and licence

Found a problem? See [`SECURITY.md`](SECURITY.md). Proprietary, all rights reserved: [`LICENSE`](LICENSE).

*Last updated: November 2026.*
