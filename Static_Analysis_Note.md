# Check the sample

## Command

`file sample.exe`

### Fingerprinting

- `sha256sum sample.exe` (`Get-FileHash -Algorithm SHA256` in PowerShell);

- `md5sum sample.exe` (`Get-FileHash -Algorithm MD5` in Powershell);

- Check imphash (import hash) in pestudio for finding DLL imports similarities.
---

# Signature

## Tool(s)

[Capa](https://github.com/mandiant/capa)

---

# String search

## Command

`strings`

## Tools

[pestudio](https://www.winitor.com/download)

[FLOSS](https://github.com/mandiant/flare-floss)

## What to look for

- Windows API's appearance

`rg -i 'VirtualAlloc|WriteProcessMemory|CreateRemoteThread|OpenProcess|WinHttp|InternetOpen|URLDownload|CreateService|RegSetValue'`

- IP Addresses, URLs, domain names

`rg -i 'https?://|ftp://|www\.|[a-z0-9-]+\.(com|net|org|io|ru|cn|top|xyz)'`

`rg '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b'`

- Paths and file names

`rg -i '([a-z]:\\|\\\\|%appdata%|%temp%|system32|users\\|programdata)'`

- Shell commands or system tools

`rg -i 'powershell|cmd\.exe|rundll32|regsvr32|schtasks|wscript|cscript|certutil|bitsadmin'`

- Anti-analysis signs

`rg -i 'vmware|virtualbox|vbox|wireshark|procmon|x64dbg|ollydbg|ida|sandbox'`

- Registry

`rg -i 'HKEY_|HKLM|HKCU|CurrentVersion\\Run|Services\\'`

- Miscellaneous strings such as Bitcoin addresses and Message Box texts.

## Tricks

### `strings -a -e l -n 6 -t x sample.exe`

- `-a`: Scan the whole file;

- `-n 6`: Only return 6-char strings;

- `-t x`: Print offset of the strings under hex format;

- `-e l`: Read 16-bit little endian letters (Useful with Windows Malware).

Run the command twice: one with and one without `-e l`.

### `rg -C 5`

Print 5 strings before and 5 strings after the indicated string.

### `sort -u`

Eliminate duplicated strings.

---

# Assembly analysis

- Ghidra

- IDA Pro
