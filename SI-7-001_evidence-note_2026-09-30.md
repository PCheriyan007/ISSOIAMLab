# Evidence Note: SI-7-001

- **Evidence ID:** SI-7-001
- **Control:** SI-7, Software, Firmware, and Information Integrity
- **Date performed:** 2026-09-30
- **Performed by:** Preston Cheriyan
- **Artifact:** SI-7-001_ISO-hash-verification_2026-09-30.png

## Objective

Verify the integrity of all operating system installation media before use in the lab environment.

## Method

Published checksum values were retrieved live from each source using `curl.exe` (Rocky Linux, Ubuntu, Windows Server 2025) or captured via browser (Windows 11 Enterprise 26H2). SHA-256 hashes of the local ISO files were computed using PowerShell `Get-FileHash` and compared against the published values. The terminal session was bracketed with `Get-Date` timestamps (3:15:08 AM to 3:16:06 AM). The Windows 11 source was captured by browser screenshot shortly after (3:18 AM per the system taskbar clock). Verification was performed from a standard (non-elevated) PowerShell session.

## Results

| ISO | Expected hash source | Source type | Result |
|---|---|---|---|
| Rocky Linux 9.8 DVD | https://download.rockylinux.org/pub/rocky/9/isos/x86_64/CHECKSUM | Vendor (official) | Match |
| Ubuntu Server 24.04.5 | https://releases.ubuntu.com/24.04.5/SHA256SUMS | Vendor (official) | Match |
| Windows Server 2025 Eval | https://github.com/rgl/windows-vagrant/blob/c5ccbced198e51dd1bcd4bf58bc8ea34c686eaf3/windows-evaluation-isos.json | Third-party (community), pinned commit | Match |
| Windows 11 Enterprise 26H2 Eval | https://files.rg-adguard.net/file/16d63494-c659-0519-f94f-3ce1cd561b94 | Third-party (community) | Match |

## Limitations

- No Microsoft-published checksum was located for either evaluation ISO, so the Windows hashes were corroborated against community-maintained sources.
- Both Windows ISOs were downloaded directly from Microsoft's official download servers over HTTPS:
  - Windows Server 2025: https://software-static.download.prss.microsoft.com/dbazure/998969d5-f34g-4e03-ac9d-1f9786c66749/26100.32230.260111-0550.lt_release_svc_refresh_SERVER_EVAL_x64FRE_en-us.iso
    - This download URL is identical to the URL listed in the pinned rgl/windows-vagrant source, further corroborating that the published checksum describes the same file.
  - Windows 11 Enterprise 26H2: https://software-static.download.prss.microsoft.com/dbazure/26300.9457.260913-1737.26h2_ge_release_svc_refresh_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en-us.iso
- The Rocky Linux checksum was retrieved from the Rocky 9 "latest" directory; the verified entry explicitly names `Rocky-9.8-x86_64-dvd.iso`.
- Hash matching verifies integrity against the published values but not publisher authenticity. GPG signature verification of the Rocky and Ubuntu checksum files was not performed.

## Conclusion

All four ISOs verified as intact and matching published values. Approved for use in lab builds.