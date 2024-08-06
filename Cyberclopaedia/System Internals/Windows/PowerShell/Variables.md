# Variables in PowerShell
Variables in [PowerShell](PowerShell.md) are specified by putting a dollar sign (`$`) in front of their name such as `$apples, $oranges`, etc. 

>[!GUIDE]+ How-To: Create a Variable
>```powershell
>$var = val
>```
>
>![](Resources/Images/Variables/Create%20Variable.png)
>

It is important to note that all PowerShell variables are .NET objects and we can call methods on them via the `$var.method()` syntax.

## Type Casting
Variables (and literal values, too) can be converted between different types in PowerShell by prepending them with the cast operator `[<type>]`- for example, `[IPAddress]"10.10.11.29"`, `[float]$apples`.

![](Resources/Images/Variables/Cast%20Variable.png)

If the value does not represent a valid object of the type `<type>`, then PowerShell will return an error.

![](Resources/Images/Variables/Cast%20Error.png)