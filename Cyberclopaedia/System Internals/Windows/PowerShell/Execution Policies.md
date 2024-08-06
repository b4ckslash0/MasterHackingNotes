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
Execution policies can be set at five different levels called **Scopes**. There are five of them - `MachinePolicy`, `UserPolicy`, `Process`, `CurrentUser` and `LocalMachine`, listed in decreasing precedence order.

|Policy|Meaning|
|:--:|:--:|
|`MachinePolicy`|The execution policy is set by a Group Policy for all users of the computer.|
|`UserPolicy`|The execution policy is set by a Group Policy for the current user on the computer.|
|`Process`|The execution policy affects only the current PowerShell session. It is stored in the `$env:PSExecutionPolicyPreference$` environment variable.|
|`CurrentUser`|The execution policy only affects only the current user. It is stored in the `HKEY_CURRENT_USER` registry subkey.|
|`LocalMachine`|The execution policy affects all users on the current computer. It is stored in the `HKEY_LOCAL_MACHINE` registry subkey.|

The effective execution policy the one set at the scope with the highest precedence. For example, a policy set at the `UserPolicy` level will override a policy set at the `Process` scope, no matter if the latter is more restrictive.

# Managing Execution Policies
> [!GUIDE]- How-To: View Execution Policies
> To view the effective execution policy:
> 
> ```powershell
> Get-ExecutionPolicy
> ```
> 
> To view the execution policy set for a specific scope:
> ```powershell
> Get-ExecutionPolicy -Scope <Scope>
> ```
> 
> To view the execution policy set for each scopes:
> 
> ```powershell
> Get-ExecutionPolicy -List
> ```

>[!GUIDE]- How-To: Set Execution Policies
>To change the execution policy in a given scope:
>
>```powershell
>Set-ExecutionPolicy -ExecutionPolicy <Policy> -Scope <Scope>
>```
>
>>[!NOTE]
>>Whilst this does alter the execution policy for the current scope, the policy will still be overridden by another policy set at a scope with higher precedence.