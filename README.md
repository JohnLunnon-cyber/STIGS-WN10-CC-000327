# Remediate WN10-CC-000327 - Enable PowerShell Transcription

## Description

**Control ID:** WN10-CC-000327  
**Requirement:** PowerShell Transcription must be enabled on Windows 10 systems.

PowerShell is a powerful administrative tool, but it can be exploited by threat actors to run malicious commands without leaving clear traces. Enabling transcription ensures that all PowerShell input and output are captured and saved to disk for auditing and incident response.
<img width="1171" alt="Screenshot 2025-07-06 at 08 52 57" src="https://github.com/user-attachments/assets/3fac1b00-5725-482c-a241-0350cc539491" />




This remediation configures the required registry settings to enable transcription, sets a secure output directory for the transcript logs, and includes invocation headers for better forensic context.

**Why it’s important:**
- Creates an auditable trail of PowerShell activity.
- Supports incident response and forensic investigations.
- Helps detect misuse of administrative privileges.
- Meets compliance requirements defined by security frameworks such as DISA STIGs.

- After running remediation script:

---
<img width="1128" alt="Screenshot 2025-07-05 at 16 48 38" src="https://github.com/user-attachments/assets/47887c64-1bfa-49c5-b916-6cdb2de1f03c" />

https://github.com/JohnLunnon-cyber/STIGS-WN10-CC-000327/blob/main/Screenshot%202025-07-05%20at%2016.48.38.png

---

## Remediation Script

```powershell
# Remediate WN10-CC-00032


markdown
Copy
Edit
# Remediate WN10-CC-000327 - Enable PowerShell Transcription

## Description

**Control ID:** WN10-CC-000327  
**Requirement:** PowerShell Transcription must be enabled on Windows 10 systems.

PowerShell is a powerful administrative tool, but it can be exploited by threat actors to run malicious commands without leaving clear traces. Enabling transcription ensures that all PowerShell input and output are captured and saved to disk for auditing and incident response.

This remediation configures the required registry settings to enable transcription, sets a secure output directory for the transcript logs, and includes invocation headers for better forensic context.

**Why it’s important:**
- Creates an auditable trail of PowerShell activity.
- Supports incident response and forensic investigations.
- Helps detect misuse of administrative privileges.
- Meets compliance requirements defined by security frameworks such as DISA STIGs.

---

## Remediation Script

```powershell
# Remediate WN10-CC-000327 - Enable PowerShell Transcription

# Define registry path
$transcriptionPath = "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\Transcription"

# Create the key if it doesn't exist
If (-Not (Test-Path $transcriptionPath)) {
    New-Item -Path $transcriptionPath -Force
}

# Enable Transcription (1 = enabled)
Set-ItemProperty -Path $transcriptionPath -Name "EnableTranscripting" -Value 1 -Type DWord

# (Optional) Set Output Directory for transcripts
# Adjust this path as needed
$outputDirectory = "C:\Transcripts"
If (-Not (Test-Path $outputDirectory)) {
    New-Item -Path $outputDirectory -ItemType Directory -Force
}
Set-ItemProperty -Path $transcriptionPath -Name "OutputDirectory" -Value $outputDirectory -Type String

# (Optional) Include Invocation Header (1 = include)
Set-ItemProperty -Path $transcriptionPath -Name "IncludeInvocationHeader" -Value 1 -Type DWord

Write-Host "PowerShell Transcription has been enabled and configured."







