# CVE-2022-29072

>   7-Zip through 21.07 on Windows allows privilege escalation and command
>   execution when a file with the .7z extension is dragged to the
>   Help\>Contents area.

# Uncertainty

There is quite a bit of uncertainty regarding this CVE in the public. The NIST vuln details has placed a status of "awaiting analysis" for this CVE.

The mitigation of this "potential" vulnerability calls for removing the 7-Zip help file ("7-zip.chm") from the installation directory of 7-Zip. If we err on the side of caution here, at worst, the file is removed, the few users who use the help file will not be able to, and the help file will be re-installed in the next application update cycle.

> ** DISPUTED ** 7-Zip through 21.07 on Windows allows privilege escalation and command execution when a file with the .7z extension is dragged to the Help>Contents area. This is caused by misconfiguration of 7z.dll and a heap overflow. The command runs in a child process under the 7zFM.exe process, NOTE: multiple third parties have reported that no privilege escalation can occur.

# Overview

While the POC for privilege escalation at the GitHub repository below has not
been released (thankfully; and it appears the author isn't keen on releasing it for reasons that are their own). We recommend you perform the current recommended
mitigation in place which is to remove the “7zip.chm” (compressed HTML help
file) from the installation directory in the meantime.

As well, utilize your SIEM (Microsoft Sentinel) to setup alerting of interactions between the
“7zip.chm” file with other utilities such as “cmd.exe”, “powershell.exe”, or
“pwsh.exe” to be alerted of any activity. We chose to replicate the CVE author's [sigma rule](https://github.com/kagancapar/CVE-2022-29072/blob/main/7z_CVE-2022-29072.yml) to generate alerts via Sentinel.

Visit the "[scripts](https://github.com/sentinelblue/CVE-2022-29072/tree/main/scripts)" and "[Microsoft Sentinel](https://github.com/sentinelblue/CVE-2022-29072/tree/main/Sentinel)" directories for more information.

## References

<https://github.com/kagancapar/CVE-2022-29072>

<https://nvd.nist.gov/vuln/detail/CVE-2022-29072>
