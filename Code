<# This form was created by Empilon
.NAME
    password manager
.SYNOPSIS
    Save up to one password! encrypted!
.DESCRIPTION
    here i learned how to encrypt a string
#>

Add-Type -AssemblyName System.Windows.Forms
[System.Windows.Forms.Application]::EnableVisualStyles()

$Form                            = New-Object system.Windows.Forms.Form
$Form.ClientSize                 = New-Object System.Drawing.Point(468,188)
$Form.text                       = "Password manager"
$Form.TopMost                    = $false

$randompswd                      = New-Object system.Windows.Forms.TextBox
$randompswd.multiline            = $false
$randompswd.width                = 272
$randompswd.height               = 20
$randompswd.location             = New-Object System.Drawing.Point(130,25)
$randompswd.Font                 = New-Object System.Drawing.Font('Microsoft Sans Serif',10)

$Button1                         = New-Object system.Windows.Forms.Button
$Button1.text                    = "Generate!"
$Button1.width                   = 76
$Button1.height                  = 30
$Button1.location                = New-Object System.Drawing.Point(130,54)
$Button1.Font                    = New-Object System.Drawing.Font('Microsoft Sans Serif',10)

$Label1                          = New-Object system.Windows.Forms.Label
$Label1.text                     = "random password:"
$Label1.AutoSize                 = $true
$Label1.width                    = 25
$Label1.height                   = 10
$Label1.location                 = New-Object System.Drawing.Point(12,28)
$Label1.Font                     = New-Object System.Drawing.Font('Microsoft Sans Serif',10)

$Button2                         = New-Object system.Windows.Forms.Button
$Button2.text                    = "Save"
$Button2.width                   = 60
$Button2.height                  = 30
$Button2.location                = New-Object System.Drawing.Point(249,54)
$Button2.Font                    = New-Object System.Drawing.Font('Microsoft Sans Serif',10)

$Button3                         = New-Object system.Windows.Forms.Button
$Button3.text                    = "Decrypt!"
$Button3.width                   = 71
$Button3.height                  = 30
$Button3.location                = New-Object System.Drawing.Point(119,100)
$Button3.Font                    = New-Object System.Drawing.Font('Microsoft Sans Serif',10)

$TextBox1                        = New-Object system.Windows.Forms.TextBox
$TextBox1.multiline              = $false
$TextBox1.width                  = 100
$TextBox1.height                 = 20
$TextBox1.enabled                = $false
$TextBox1.location               = New-Object System.Drawing.Point(199,107)
$TextBox1.Font                   = New-Object System.Drawing.Font('Microsoft Sans Serif',10)

$Form.controls.AddRange(@($randompswd,$Button1,$Label1,$Button2,$Button3,$TextBox1))

$Button1.Add_Click({ Generate })
$Button2.Add_Click({ save })
$Button3.Add_Click({ decrypt })

function Generate {
$randompswd.text = -join ((65..90) + (97..122) | Get-Random -Count 10 | % {[char]$_})
}

function save {
if (Test-Path C:\TEMP\Password) {
    [System.Windows.MessageBox]::Show("You can only save one password! `n You can remove the last saved password by going to the file C:\TEMP\ and delete the file \Password")
}
else{
$SecretFile = "C:\TEMP\Password"
$SecretContent = $randompswd.text

ConvertTo-SecureString -String $SecretContent -AsPlainText -Force | 
  ConvertFrom-SecureString | 
  Out-File $SecretFile -Encoding UTF8
  
notepad $SecretFile
}}
function decrypt {
    # File used to store the encrypted string
$SecretFile = "C:\TEMP\Password"

# Secret string
$SecretContent = $randompswd.text

$SecureString = ConvertTo-SecureString -String (Get-Content $SecretFile)
$Pointer = [Runtime.InteropServices.Marshal]::SecureStringToBSTR($SecureString)
$SecretContent = [Runtime.InteropServices.Marshal]::PtrToStringAuto($Pointer)

$TextBox1.text = $SecretContent
}
[void]$Form.ShowDialog()
