# Unreleased — Blocknil fork

- Allow zero intermediate input-key sums while still rejecting a zero final sum.
- Enforce the BIP352 limit of 2,323 recipients per scan-public-key group, including labels.
- **Breaking:** `create_silentpayment_scriptpubkeys` returns `Result`; callers must handle or
  propagate the recipient-limit error. No fork release has been published.
- Independent source-review scope and remaining integration limits: [review](../doc/blocknil-sender-review.md).

# 0.2.0

- Fix bug that allows the creation of silent payment outputs without collecting
  all the eligible input private keys. #63

# 0.1.0

- Functions for encoding and decoding Silent Payment Codes (BIP352).
- Support for deriving Silent Payment script pubkeys and shared secrets.
- Capabilities for scanning transactions to identify Silent Payment outputs.
- Implementation for signing PSBTs that spend Silent Payment outputs.
- Error handling for Silent Payment-related operations.
- Verification against BIP 352 test vectors.
