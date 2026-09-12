# AVWT Reference Catalog feed

This public repository distributes immutable, signed AV Workstation Toolkit Reference Catalog release artifacts. It contains no AVWT application source, package authority, credentials, signing private keys, or development manifests.

Production feed root: <https://11anthonym.github.io/AVWT-Catalog/>

## Published layout

```text
stable/
  catalog-channel.json
  catalog-channel.sig
catalogs/
  <revision>/
    AVWT-Catalog-<version>.avwtcatalog
    catalog-changes.json
```

Every `.avwtcatalog` is a complete signed snapshot produced and verified by the private AVWT publisher. `catalog-channel.json` is also signed. Consumers must verify signatures, hashes, schemas, revision monotonicity, and catalog cross-references; repository visibility and HTTPS are transport properties, not catalog trust.

## Publication contract

1. Produce and approve the exact feed output outside this repository. Never generate, rebuild, or resign it here.
2. Add a new `catalogs/<revision>/` directory. Existing revision files are immutable and must never be replaced or deleted.
3. Verify the anonymously served catalog URL and its SHA-256 digest.
4. Update `stable/catalog-channel.json` and `stable/catalog-channel.sig` last, as an inseparable signed pair.
5. Verify the two stable URLs and the immutable bundle URL without authentication or redirects.

The validation workflow rejects unexpected files, private-key markers, incomplete revision directories, and changes to previously committed immutable revision files. Production signing private keys and publisher credentials must remain outside all Git repositories.

