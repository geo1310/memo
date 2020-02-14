
# README.MD


WINDOWS POWERSHELL : 
---------------------------------------------------------------------------------------------------------

PowerShell ISE -> éditeur de script intégré ( alternative à PowerGUI )

Windows PowerShell est la nouvelle interface système de Microsoft
le lancer en admin
CMD est l’un des derniers vestiges du système d’exploitation MS-DOS

Get-ExecutionPolicy -> connaitre le mode utilisé
Set-ExecutionPolicy Unrestricted

Restricted : aucun script ne peut être exécuté. PowerShell est utilisable uniquement en mode interactif.

AllSigned : seuls les scripts signés peuvent être exécutés.

RemoteSigned : les scripts téléchargés depuis Internet doivent être signés pour être exécutés.
Les scripts présents sur votre poste de travail ne sont pas concernés et peuvent être exécutés.

Unrestricted : pas de restrictions. Les scripts peuvent être exécutés.

C:\Windows\system32> Send-MailMessage -From "geo1310@hotmail.fr" -To "gbriche59@yahoo.fr" -Subject "votre objet" -SmtpServer "smtp.mail.yahoo.fr" -Body "Le corps du mail" -Attachments "le chemin d’accès à votre fichier"

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
curl.exe -L -o ubuntu-1604.appx https://aka.ms/wsl-ubuntu-1604
Add-AppxPackage .\app_name.appx



GIT :
-------------------------------------------------------------------------------------------------------

    git config --global user.name "name"
    git config --global user.email "email"

    git clone lienFourniParGitHub

### create a new repository on the command line

    echo "# crepes_bretonnes" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/geo1310/crepes_bretonnes.git
    git push -u origin master



VIRTUAL BOX :
-----------------------------------------------------------------------------------------------------

### Additions invitees

 Open your terminal
 
    sudo apt-get install build-essential gcc make perl dkms
 reboot  
 Open your terminal  
 Go to the installation disk
 
    sudo sh VBoxLinuxAdditions.run
    
 reboot












