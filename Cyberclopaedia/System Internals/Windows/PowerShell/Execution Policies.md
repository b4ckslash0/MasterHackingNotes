# Execution Policy
A [PowerShell](PowerShell.md) **execution policy** is a safety measure which determines the conditions under which PowerShell scripts are allowed to be run. Its main purpose is to prevent unintentional execution of unwanted scripts.

There are seven different types of execution policies in PowerShell.

`Undefined`:
- The current [scope](Execution%20Policies.md#Execution%20Policy%20Scope) does not have an execution policy set.
- If all scopes have an `Undefined` execution policy, the effective execution policy is `Restricted` for Windows clients and `RemoteSigned` for Windows Servers.

`Default`:
- A placeholder for the default execution policy - `Restricted` on Windows clients and `RemoteSigned` on Windows servers.

`Restricted`:
- Execution of individual commands is allowed, but execution of scripts is prohibited.
- Prevents running of all script files, as well as formatting and configuration files (`.ps1xml`), module script files (`.psm1`) and profiles (`.ps1`).
- The default execution policy for Windows clients.

`AllSigned`:
- All scripts (including local ones) and configuration files are allowed to run if they are signed by a trusted publisher.
- Running scripts from untrusted publishers invokes a prompt for confirmation.
- There is a risk of running signed, yet malicious scripts.

`RemoteSigned`:
- Scripts and configuration files downloaded "from the Internet" must be signed by a trusted publisher in order to execute. Nevertheless, external scripts and configuration files can still run if they are unblocked, for example through the `Unblock-File` [commandlet](Commands/Commandlets.md).
>[!NOTE]
>"From the internet" means that the files were downloaded via Microsoft Edge or Internet Explorer. If the file was obtained through another browser or method, then there is no way for Windows to know if it is "from the Internet" or not.
- Local scripts and configuration files require no signature to run.
- The default execution policy for Windows servers.
- There is a risk of running scripts which do not come "from the Internet" and also running signed, yet malicious scripts.

`Unrestricted`:
- Unsigned scripts are allowed to execute.
- There is a risk of running malicious scripts.
- This is the only possible execution policy on non-Windows.

`Bypass`:
- All scripts are allowed to run without warnings or prompts.

## Execution Policy Scope 
Execution policies can be set at five different levels called **Scopes**.

# Managing Execution Policies
> [!GUIDE] How-To:
> Hill