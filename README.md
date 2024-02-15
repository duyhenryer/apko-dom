# apko-done

[![Build](https://github.com/duyhenryer/apko-done/actions/workflows/release.yaml/badge.svg?branch=main)](https://github.com/duyhenryer/apko-done/actions/workflows/release.yaml)

Wolfi-based image configured using [melange](https://github.com/chainguard-dev/melange) and [apko](https://github.com/chainguard-dev/apko).

It comes with a [dummy melange package](hello.melange.yaml) and a default [apko image config](latest.apko.yaml). 
Edit `latest.apko.yaml` to add or remove whatever packages you need.

## Usage

```bash
$ docker run --rm -it ghcr.io/duyhenryer/apko-dom
```

## Signing

This image is signed with [cosign](https://github.com/sigstore/cosign). To verify, download `cosign` and run

```sh
cosign verify ghcr.io/duyhenryer/apko-dom:latest \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  --certificate-identity https://github.com/duyhenryer/apko-dom/.github/workflows/release.yaml@refs/heads/main | jq
```

Expected output

<details>

```
Verification for ghcr.io/duyhenryer/apko-dom:latest --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The code-signing certificate was verified using trusted certificate authority certificates
[
  {
    "critical": {
      "identity": {
        "docker-reference": "ghcr.io/duyhenryer/apko-dom"
      },
      "image": {
        "docker-manifest-digest": "sha256:20b93dde6a36933a286c52a85c5f8b36da0f5fa1ec28c9f9fac7ee529093276f"
      },
      "type": "cosign container image signature"
    },
    "optional": {
      "1.3.6.1.4.1.57264.1.1": "https://token.actions.githubusercontent.com",
      "1.3.6.1.4.1.57264.1.2": "push",
      "1.3.6.1.4.1.57264.1.3": "32065f21a8cf583cccab02d47d8591ffcda988e1",
      "1.3.6.1.4.1.57264.1.4": "Build action",
      "1.3.6.1.4.1.57264.1.5": "duyhenryer/apko-dom",
      "1.3.6.1.4.1.57264.1.6": "refs/heads/main",
      "Bundle": {
        "SignedEntryTimestamp": "MEQCIH+X2vzzEbHAlPjk/unoTgxlLAXHd5UQJHi58gMyvRxvAiB4JI7Dmqi/tNka6ON+GFM6CaWgBRIbQnaFS0kbd75iwA==",
        "Payload": {
          "body": "eyJhcGlWZXJzaW9uIjoiMC4wLjEiLCJraW5kIjoiaGFzaGVkcmVrb3JkIiwic3BlYyI6eyJkYXRhIjp7Imhhc2giOnsiYWxnb3JpdGhtIjoic2hhMjU2IiwidmFsdWUiOiJmZTQ2NjI3ZDUxMGYwYzA5YWRmOWU5ZjcwNmFjYTQxNzUxMDE4YmYyMmI3N2I3MWE3NmM1NDY4NzI3NTM0MTFmIn19LCJzaWduYXR1cmUiOnsiY29udGVudCI6Ik1FUUNJRFdZOUpVSzJtUVZ4Q0lHWE9yeHZHUWNTcmgzZTBYSWptekY1NkxMRjQ5QUFpQUt0OU1hc3lIY2oza3IvZlRrdjJMLzUxK0Z5MWFsM1JmU0tkanhmeWtGSGc9PSIsInB1YmxpY0tleSI6eyJjb250ZW50IjoiTFMwdExTMUNSVWRKVGlCRFJWSlVTVVpKUTBGVVJTMHRMUzB0Q2sxSlNVZDBla05EUW1vMlowRjNTVUpCWjBsVll6SktVMGxTWVZwQ1lVSnJaR3R0TmxSYVJFczJNa0poYkd4amQwTm5XVWxMYjFwSmVtb3dSVUYzVFhjS1RucEZWazFDVFVkQk1WVkZRMmhOVFdNeWJHNWpNMUoyWTIxVmRWcEhWakpOVWpSM1NFRlpSRlpSVVVSRmVGWjZZVmRrZW1SSE9YbGFVekZ3WW01U2JBcGpiVEZzV2tkc2FHUkhWWGRJYUdOT1RXcE5kMDlVUVROTlJFMTNUa1JCTkZkb1kwNU5hazEzVDFSQk0wMUVUWGhPUkVFMFYycEJRVTFHYTNkRmQxbElDa3R2V2tsNmFqQkRRVkZaU1V0dldrbDZhakJFUVZGalJGRm5RVVYyTURaMFVEaEJhMjAwZW5Cd1VUZE1hRFpzZEN0dU5FWkJjbGRPTWxCcGN6WmFMMFFLY1ZGblVsWXJSV2hITDBkTVp6ZFlkVWhCZUd0bVVqRmtNSGxZY0hWWFptdGtTSHBXVGxGaWVteHhRek5OYmtKcE5tRlBRMEpXTUhkbloxWmFUVUUwUndwQk1WVmtSSGRGUWk5M1VVVkJkMGxJWjBSQlZFSm5UbFpJVTFWRlJFUkJTMEpuWjNKQ1owVkdRbEZqUkVGNlFXUkNaMDVXU0ZFMFJVWm5VVlZvTVRWTUNtMXVablZoYzI5Q2RrVTVibEpXUzFaV2VFNUpNVTVaZDBoM1dVUldVakJxUWtKbmQwWnZRVlV6T1ZCd2VqRlphMFZhWWpWeFRtcHdTMFpYYVhocE5Ga0tXa1E0ZDFsM1dVUldVakJTUVZGSUwwSkdhM2RXTkZwV1lVaFNNR05JVFRaTWVUbHVZVmhTYjJSWFNYVlpNamwwVERKU01XVlhhR3hpYmtvMVdsaEpkZ3BaV0VKeVlua3hhMkl5TUhaTWJXUndaRWRvTVZscE9UTmlNMHB5V20xNGRtUXpUWFpqYlZaeldsZEdlbHBUTlRWWlZ6RnpVVWhLYkZwdVRYWmhSMVpvQ2xwSVRYWmlWMFp3WW1wQk5VSm5iM0pDWjBWRlFWbFBMMDFCUlVKQ1EzUnZaRWhTZDJONmIzWk1NMUoyWVRKV2RVeHRSbXBrUjJ4MlltNU5kVm95YkRBS1lVaFdhV1JZVG14amJVNTJZbTVTYkdKdVVYVlpNamwwVFVKSlIwTnBjMGRCVVZGQ1p6YzRkMEZSU1VWQ1NFSXhZekpuZDA1bldVdExkMWxDUWtGSFJBcDJla0ZDUVhkUmIwMTZTWGRPYWxadFRXcEdhRTlIVG0xT1ZHZDZXVEpPYWxsWFNYZE5iVkV3VGpKUk5FNVVhM2hhYlZwcVdrZEZOVTlFYUd4TlZFRmhDa0puYjNKQ1owVkZRVmxQTDAxQlJVVkNRWGhEWkZkc2MxcERRbWhaTTFKd1lqSTBkMGxSV1V0TGQxbENRa0ZIUkhaNlFVSkNVVkZVV2toV05XRkhWblVLWTI1c2JHTnBPV2hqUjNSMlRGZFNkbUpVUVdSQ1oyOXlRbWRGUlVGWlR5OU5RVVZIUWtFNWVWcFhXbnBNTW1oc1dWZFNla3d5TVdoaFZ6UjNUM2RaU3dwTGQxbENRa0ZIUkhaNlFVSkRRVkYwUkVOMGIyUklVbmRqZW05MlRETlNkbUV5Vm5WTWJVWnFaRWRzZG1KdVRYVmFNbXd3WVVoV2FXUllUbXhqYlU1MkNtSnVVbXhpYmxGMVdUSTVkRTFIVlVkRGFYTkhRVkZSUW1jM09IZEJVV3RGVm5kNFZtRklVakJqU0UwMlRIazVibUZZVW05a1YwbDFXVEk1ZEV3eVVqRUtaVmRvYkdKdVNqVmFXRWwyV1ZoQ2NtSjVNV3RpTWpCMlRHMWtjR1JIYURGWmFUa3pZak5LY2xwdGVIWmtNMDEyWTIxV2MxcFhSbnBhVXpVMVdWY3hjd3BSU0Vwc1dtNU5kbUZIVm1oYVNFMTJZbGRHY0dKcVFUUkNaMjl5UW1kRlJVRlpUeTlOUVVWTFFrTnZUVXRFVFhsTlJGa3hXbXBKZUZsVWFHcGFhbFUwQ2sweVRtcFpNa1pwVFVSS2EwNUVaR3RQUkZVMVRWZGFiVmt5VW1oUFZHYzBXbFJGZDBoUldVdExkMWxDUWtGSFJIWjZRVUpEZDFGUVJFRXhibUZZVW04S1pGZEpkR0ZIT1hwa1IxWnJUVVJaUjBOcGMwZEJVVkZDWnpjNGQwRlJkMFZMUVhkdFlVaFNNR05JVFRaTWVUbHVZVmhTYjJSWFNYVlpNamwwVERKU01RcGxWMmhzWW01S05WcFlTWFpaV0VKeVlua3hhMkl5TUhkUFFWbExTM2RaUWtKQlIwUjJla0ZDUkZGUmNVUkRaM3BOYWtFeVRsZFplVTFYUlRSWk1sa3hDazlFVG1wWk1rNW9XV3BCZVZwRVVUTmFSR2N4VDFSR2JWcHRUbXRaVkdzMFQwZFZlRTFDT0VkRGFYTkhRVkZSUW1jM09IZEJVVFJGUlZGM1VHTnRWbTBLWTNrNWIxcFhSbXRqZVRsMFdWZHNkVTFDYTBkRGFYTkhRVkZSUW1jM09IZEJVVGhGUTNkM1NrNXFTVE5OZWxFeFRYcHJORTFETUVkRGFYTkhRVkZSUWdwbk56aDNRVkpCUlVoM2QyUmhTRkl3WTBoTk5reDVPVzVoV0ZKdlpGZEpkVmt5T1hSTU1sSXhaVmRvYkdKdVNqVmFXRWwzUjBGWlMwdDNXVUpDUVVkRUNuWjZRVUpGVVZGTFJFRm5lVTFVUlRGTlZHTXpUMFJDYkVKbmIzSkNaMFZGUVZsUEwwMUJSVk5DUm1OTlZsZG9NR1JJUW5wUGFUaDJXakpzTUdGSVZta0tURzFPZG1KVE9XdGtXR3h2V2xjMWVXVlhWbmxNTWtaM1lUSTRkRnBIT1hSTWVUVnVZVmhTYjJSWFNYWmtNamw1WVRKYWMySXpaSHBNTTBwc1lrZFdhQXBqTWxWMVpWZEdkR0pGUW5sYVYxcDZUREpvYkZsWFVucE1NakZvWVZjMGQwOUJXVXRMZDFsQ1FrRkhSSFo2UVVKRmQxRnhSRU5uZWsxcVFUSk9WMWw1Q2sxWFJUUlpNbGt4VDBST2Fsa3lUbWhaYWtGNVdrUlJNMXBFWnpGUFZFWnRXbTFPYTFsVWF6UlBSMVY0VFVKUlIwTnBjMGRCVVZGQ1p6YzRkMEZTVVVVS1FtZDNSV05JVm5waFJFSmFRbWR2Y2tKblJVVkJXVTh2VFVGRlZrSkZjMDFUVjJnd1pFaENlazlwT0haYU1td3dZVWhXYVV4dFRuWmlVemxyWkZoc2J3cGFWelY1WlZkV2VVd3lSbmRoTWpoMFdrYzVkRXd5Um1wa1IyeDJZbTVOZG1OdVZuVmplVGd5VFZSQk1FOUVXVE5OUkZrd1RESkdNR1JIVm5SalNGSjZDa3g2UlhkR1oxbExTM2RaUWtKQlIwUjJla0ZDUm1kUlNVUkJXbmRrVjBwellWZE5kMmRaYTBkRGFYTkhRVkZSUWpGdWEwTkNRVWxGWlhkU05VRklZMEVLWkZGRVpGQlVRbkY0YzJOU1RXMU5Xa2hvZVZwYWVtTkRiMnR3WlhWT05EaHlaaXRJYVc1TFFVeDViblZxWjBGQlFWbHdkRzFPZFU5QlFVRkZRWGRDUndwTlJWRkRTVVp1TWpkYWFWRkRjM1pHV0hoeGNpdHZOWEJFVVdsRVlYZ3ZOR0ZFWm1sTGFtOXFhVGRCWTFKQmVteEJhVUZNY0V4Q2VYTXhMMFp6VVZobkNsRlpWQzlFV0hSMmJFbDFlWFZEVFZSdWVVSjFXWEJCZW01amRtMHZWRUZMUW1kbmNXaHJhazlRVVZGRVFYZE9ia0ZFUW10QmFrRktRa0ZUYm10MlRpOEtOVFVyTUZjeVVrZFViVzB5TjFadFpYZ3dObmhTZUZseFNYQmpiWFJIYTI1NmQzYzVjMFY2V1Zabk0xbG9iMkpoTnpacmVGVlZVVU5OUWtoc1dWcHhaZ3BzZEVJM1ZDOWxMMEpMWm5Bd1kwNXZXRU01Y0ZKaVVETnVTa3hHT1cwcmJYWjJlRlZEUm1ZeGFXOTVhbkJFWWsxWWVVUmtZbVJ1UmtSblBUMEtMUzB0TFMxRlRrUWdRMFZTVkVsR1NVTkJWRVV0TFMwdExRbz0ifX19fQ==",
          "integratedTime": 1694055849,
          "logIndex": 34877926,
          "logID": "c0d23d6ad406973f9559f3ba2d1ca01f84147d8ffc5b8445c224f98b9591801d"
        }
      },
      "Issuer": "https://token.actions.githubusercontent.com",
      "Subject": "https://github.com/duyhenryer/apko-dom/.github/workflows/release.yaml@refs/heads/main",
      "githubWorkflowName": "Build action",
      "githubWorkflowRef": "refs/heads/main",
      "githubWorkflowRepository": "duyhenryer/apko-dom",
      "githubWorkflowSha": "32065f21a8cf583cccab02d47d8591ffcda988e1",
      "githubWorkflowTrigger": "push"
    }
  }
] 
```
</details>



