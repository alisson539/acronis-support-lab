# How to Troubleshoot Acronis Service Startup Failure (Error 1067)

## Summary
Certain Acronis services (e.g., *Acronis Scheduler2 Service*, *Managed Machine Service*, *Acronis Agent Core Service*) may fail to start and immediately stop with **Error 1067: The process terminated unexpectedly**.  
This article provides a structured approach to diagnose and resolve the issue.

---

## Problem

When attempting to start an Acronis service, the system returns:

Error 1067: The process terminated unexpectedly.

============


The service remains in **Stopped** state, causing agent malfunction, backup failure, or loss of communication with the Acronis cloud.

---

## Symptoms

- Service starts and stops immediately  
- `sc query <service>` shows `STATE: STOPPED`  
- Event Viewer logs show crashes or module load failures  
- Acronis Agent appears **offline** in the Cyber Protect Console  
- Protection plans fail to execute  

---

## Evidence Collection

Gather the following before changing anything:

### 1. Service state  
```powershell
sc query <serviceName>

===============

2. Windows Event Viewer logs

Check:

Application

System

Filter by:

Acronis*

Application Error

.NET Runtime

Faulting module (common ones: msvcr100.dll, vcruntime140.dll, mms.exe)

3. Dependency services
sc qc <serviceName>


Check for:

missing DLLs

corrupted paths

disabled dependencies

Root Causes (Most Common)

Missing or corrupted Visual C++ runtime

Acronis components rely heavily on VC++ 2010/2015/2019

Port conflict on required services

Especially port 443 (TLS communication)

Binding failures will trigger 1067

Corrupted service executable or configuration

Caused by forced shutdowns or incomplete updates

File system permission issues

Missing rights for SYSTEM or Acronis services

Third-party interference

Antivirus

EDR tools

SSL inspection

Agent upgrade failure

Partial updates leave binaries inconsistent

Resolution Steps
1. Restart the affected service
Restart-Service <serviceName> -Force


If it immediately stops → continue.

2. Reinstall Visual C++ Redistributables

Install these packages (ALL of them):

VC++ 2010 (x64 + x86)

VC++ 2015–2019 combined package

Download: https://aka.ms/vs/17/release/vc_redist.x64.exe
 (if available)

3. Check for port conflicts

Required by Acronis Agent:

netstat -ano | findstr :443


If another process is listening (not acronis):

stop the conflicting service

or change its port

4. Repair the Acronis Agent installation

Run:

Open Control Panel → Programs

Select Acronis Cyber Protect Agent

Choose Repair

5. Re-register agent (if corrupted)
"C:\Program Files\Acronis\Agent\registration_tool.exe" register

6. Review Event Viewer for the exact faulting module

If the same DLL appears repeatedly:

delete cache

reinstall component

clear %ProgramData%\Acronis (with care)

7. If unresolved → escalate with evidence

Include:

Impact

Repro steps

Scope (one device or tenant?)

Logs (Acronis + Event Viewer)

Hypothesis

This is mandatory for Tier 1 → Tier 2 escalation quality.

Validation

After applying a fix:

Start the service

Confirm STATE = RUNNING

Check Cyber Protect Console: Agent should be online

Trigger a protection plan task

Confirm clean job execution