

WINDOWS POWERSHELL : 
---------------------------------------------------------------------------------------------------------
**Les versions de Windows intègrent le langage PowerShell nativement.**  
Celui-ci est devenu au fil du temps bien plus qu'un "simple" langage de scripting puisque vous pouvez même développer 
des interfaces GUI en PowerShell...

Windows Management Framework 4.0 (WMF 4.0) doit être installé sur votre machine.

**PowerShell ISE -> éditeur de script intégré ( alternative à PowerGUI )**

Windows PowerShell est la nouvelle interface système de Microsoft le lancer en admin
CMD est l’un des derniers vestiges du système d’exploitation MS-DOS

### Autoriser l'exécution de scripts :

Il est possible d'indiquer à PowerShell plusieurs modes d'exécution. Chaque mode implique un certain comportement.

    Get-ExecutionPolicy -> connaitre le mode utilisé
    Set-ExecutionPolicy Unrestricted

    1. Restricted : aucun script ne peut être exécuté. PowerShell est utilisable uniquement en mode interactif.

    2. AllSigned : seuls les scripts signés peuvent être exécutés.

    3. RemoteSigned : les scripts téléchargés depuis Internet doivent être signés pour être exécutés. Les scripts présents sur votre poste de travail ne sont pas concernés et peuvent être exécutés.

    4. Unrestricted : pas de restrictions. Les scripts peuvent être exécutés. ( vous pouvez exécuter n'importe quel script .ps1 ! )
    
    
Les scripts présents sur votre poste de travail ne sont pas concernés et peuvent être exécutés.

### Importer des modules dans vos scripts :

    Get-Module # modules chargés sur la machine
    Get-Module --ListAvailable #  lister les modules disponibles
    
    Import-Module ActiveDirectory # importer via la cmdlet Import-Module
 
### Exemple Script ( ps1 ):
 
Je souhaite obtenir la liste de tous mes utilisateurs Active Directory dont la dernière connexion est supérieure à 90 jours 
afin de verrouiller leur compte pour des raisons de sécurité. Être proactif n'a jamais fait de mal à personne, 
alors nous ajouterons l'envoi d'un email automatique au help desk (assistance) pour les informer de cette désactivation.  
 
La recherche Active Directory :

Pour lister les utilisateurs concernés, vous pouvez utiliser la cmdletSearch-ADAccountsuivie de plusieurs paramètres :  
Terminez en filtrant uniquement sur les comptes actifs via la clause Where-Object

    $LockedAccount = Search-ADAccount -UsersOnly -AccountInactive -TimeSpan 90.00:00:00 -SearchBase "OU=Users,DC=Domaine,DC=Local" | Where {$_.enabled}
    $LockedAccount | Set-ADUser -Enabled $false # désactive les comptes concernés
    
1. UsersOnly : recherche uniquement des objets de type "account"
2. AccountInactive : recherche les comptes qui ne se sont pas connectés depuis une certaine période
3. TimeSpan : indique la durée d'inactivité
4. SearchBase : recherche uniquement dans cette unité d'organisation  

**Script pour automatiser la désactivation des comptes AD dont la dernière connexion > 90 jours :**


    # version 1.0
    # Auteur : Nicolas PRIGENT

    # Force le type d'execution
    Set-ExecutionPolicy Unrestricted

    # Importe le module AD
    Import-Module ActiveDirectory
    
    $LockedAccount = Search-ADAccount -UsersOnly -AccountInactive -TimeSpan 90.00:00:00 -SearchBase "OU=Users,DC=Domaine,DC=Local" | Where {$_.enabled}
    $LockedAccount | Set-ADUser -Enabled $false # désactive les comptes concernés
    
    # Envoi de l'Email
    
    $smtpServer = "smtp.xxx.fr"
    $from = "xxx@yyy"
    $to = "xxx@yyy"
    $subject = "Script"
    $body = "
    <html>
    <head></head>
         <body>
            <p>Bonjour,<br />
               Ceci est un test d'envoie d'un email par un script !!!<br />
            $LockedAccount
            </p>
        </body>
    </html>"

    Send-MailMessage -smtpserver $smtpserver -from $from -to $to -subject $subject -body $body -bodyasHTML -priority High
  
---
    
    C:\Windows\system32> Send-MailMessage -From "geo1310@hotmail.fr" -To "gbriche59@yahoo.fr" -Subject "votre objet" -SmtpServer "smtp.mail.yahoo.fr" -Body "Le corps du mail" -Attachments "le chemin d’accès à votre fichier"

### Installation Linux avec PowerShell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    curl.exe -L -o ubuntu-1604.appx https://aka.ms/wsl-ubuntu-1604
    Add-AppxPackage .\app_name.appx










