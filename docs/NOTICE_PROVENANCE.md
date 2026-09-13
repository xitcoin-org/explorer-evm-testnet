# Outstanding distribution notices

Review date: 13 September 2026. This record concerns the exact package versions
in the accepted frontend. It does not change the installed image or assert a
complete distribution attestation. The four published npm version records have
no license field; previous exact tarball inspections found no embedded notice.

| Package | Official provenance recovered | Remaining action |
|---|---|---|
| `@dynamic-labs-sdk/assert-package-version@1.12.1` | [Exact registry record](https://registry.npmjs.org/@dynamic-labs-sdk/assert-package-version/1.12.1) has no license, repository or gitHead. | Obtain the publisher's notice and source mapping for this exact version. A license on another Dynamic repository does not establish applicability. |
| `@dynamic-labs-sdk/client@1.12.1` | [Exact registry record](https://registry.npmjs.org/@dynamic-labs-sdk/client/1.12.1) has no license, repository or gitHead. | Obtain the publisher's notice and source mapping for this exact version. |
| `@evervault/wasm-attestation-bindings@0.3.1` | Registry gitHead `0a5a8a6660d4e33b58b6843bce1c1bbc77f72089` resolves to the official source: root [LICENSE](https://github.com/evervault/attestation-doc-validation/blob/0a5a8a6660d4e33b58b6843bce1c1bbc77f72089/LICENSE) is Apache-2.0, while the version-0.3.1 [package.json](https://github.com/evervault/attestation-doc-validation/blob/0a5a8a6660d4e33b58b6843bce1c1bbc77f72089/wasm-attestation-bindings/package.json) declares MIT. | Ask the publisher to reconcile this exact-version conflict and provide the applicable notice. Neither license is selected by inference. |
| `@metamask/eth-json-rpc-provider@1.0.1` | Tag v1.0.1 matches npm gitHead `e75769e8a507a7d76c6d4d513dfb4326932f9983`, whose tree has no license. Official correction [69d7d5d](https://github.com/MetaMask/eth-json-rpc-provider/commit/69d7d5d073de339766117658ea23293870a45e11) adds the missing ISC text and package field on 29 September 2023. | The official ISC notice is recovered, but its inclusion/applicability for the exact earlier 1.0.1 distribution still needs reconciliation. Do not describe it as embedded in that tarball. |

No package was upgraded, no installed image was rebuilt, and no license was
fabricated. Exact registry integrity values, source trees, the Evervault conflict
and the MetaMask correction are preserved in the operator handoff. Final notice
assembly and distribution attestation remain open.
