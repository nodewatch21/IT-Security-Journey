# Windows Server 2022 & Active Directory Lab Setup

## Übersicht

Dieses Lab dokumentiert die Einrichtung eines Windows Server 2022 Domain Controllers mit Active Directory in einer VMware-Umgebung. Ziel ist das praktische Verständnis von Windows-Netzwerkinfrastruktur.

**Datum:** Januar 2026  
**Umgebung:** VMware Workstation  
**OS:** Windows Server 2022 Standard Evaluation (Desktop Experience)

---

## Grundkonzepte

### Windows Server vs. Windows Desktop
Windows Server ist für Dienste optimiert, nicht für Desktop-Nutzung. Server werden über **Rollen** konfiguriert – jede Rolle ist ein Dienst (z.B. DNS, DHCP, Active Directory).

### Active Directory (AD)
Eine zentrale Datenbank die alle Objekte im Netzwerk verwaltet: Benutzer, Computer, Gruppen, Drucker, Policies.

**Wichtige Begriffe:**

| Begriff | Erklärung |
|---------|-----------|
| **Domain** | Logische Grenze – alle Objekte teilen dieselbe Datenbank und Sicherheitsrichtlinien |
| **Domain Controller (DC)** | Server der AD hostet, authentifiziert Benutzer |
| **Organizational Unit (OU)** | Container zur Strukturierung (z.B. nach Abteilungen) |
| **Gruppenrichtlinie (GPO)** | Zentrale Steuerung von Benutzer-/Computereinstellungen |
| **DNS** | Namensauflösung – eng mit AD verzahnt |

---

## Lab-Aufbau

### VM-Spezifikationen

```
CPU:        2 Kerne
RAM:        4 GB
Festplatte: 60 GB (Single File)
Netzwerk:   NAT oder Bridged
ISO:        Windows Server 2022 Evaluation
```

### Netzwerkkonfiguration

```
IP-Adresse:     192.168.178.10
Subnetzmaske:   255.255.255.0
Gateway:        192.168.178.1
DNS-Server:     127.0.0.1 (localhost - DC ist eigener DNS)
```

**Warum statische IP?** Ein Domain Controller muss immer unter derselben Adresse erreichbar sein. Alle Clients fragen ihn für Login und DNS an.

**Warum DNS auf 127.0.0.1?** Der DC wird gleichzeitig DNS-Server. AD braucht DNS um zu funktionieren.

---

## Installation Schritt für Schritt

### 1. VM erstellen

1. VMware: "Create a New Virtual Machine"
2. **Wichtig:** "I will install the operating system later" wählen (verhindert Easy Install Probleme)
3. Guest OS: Microsoft Windows → Windows Server 2022
4. Ressourcen wie oben konfigurieren
5. Nach Erstellung: VM Settings → CD/DVD → ISO einbinden
6. VM starten

### 2. Windows Server installieren

1. Sprache/Region/Tastatur einstellen (Deutsch empfohlen)
2. **"Windows Server 2022 Standard Evaluation (Desktop Experience)"** wählen
3. "Custom: Install" für Neuinstallation
4. Festplatte auswählen → Next
5. Warten, Administrator-Passwort setzen

### 3. VMware Tools installieren

1. VMware Menü → VM → Install VMware Tools
2. Im Server: Explorer öffnen → DVD-Laufwerk → setup64.exe
3. Durchklicken, Neustart
4. Ergebnis: Fullscreen, bessere Performance, Copy-Paste

### 4. Statische IP konfigurieren

1. Rechtsklick Netzwerk-Icon → "Open Network & Internet settings"
2. "Change adapter options"
3. Rechtsklick Adapter → Properties
4. Doppelklick "Internet Protocol Version 4 (TCP/IPv4)"
5. "Use the following IP address" → Werte eintragen

### 5. Active Directory Domain Services installieren

1. Server Manager → "Add roles and features"
2. Next bis "Server Roles"
3. Häkchen bei "Active Directory Domain Services"
4. "Add Features" im Popup
5. Durchklicken → Install
6. Nach Installation: "Promote this server to a domain controller"

### 6. Domain Controller konfigurieren

1. "Add a new forest"
2. Root domain name: `labor.local`
3. DSRM-Passwort setzen (Notfall-Wiederherstellung)
4. DNS-Delegation Warnung ignorieren
5. Durchklicken → Install
6. Server startet automatisch neu

---

## Active Directory Struktur aufbauen

### OU erstellen

1. Start → "Active Directory Users and Computers"
2. Linksklick auf labor.local → aufklappen
3. Rechtsklick auf labor.local → New → Organizational Unit
4. Name: `IT-Abteilung`

### Benutzer anlegen

1. Rechtsklick auf OU "IT-Abteilung" → New → User
2. Daten eingeben:
   - First name: Max
   - Last name: Mustermann
   - User logon name: mmustermann
3. Passwort setzen
4. "User must change password at next logon" deaktivieren (für Lab)

### Gruppenrichtlinie (GPO) erstellen

1. Start → "Group Policy Management"
2. Forest → Domains → labor.local aufklappen
3. Rechtsklick auf OU "IT-Abteilung"
4. "Create a GPO in this domain, and Link it here..."
5. Name: `Desktop-Test`
6. Rechtsklick auf neue GPO → Edit
7. User Configuration → Policies → Administrative Templates → Desktop → Desktop
8. "Desktop Wallpaper" → Enabled
9. Pfad: `C:\Windows\Web\Wallpaper\Windows\img0.jpg`

---

## Ergebnis

Nach diesem Lab hast du:

- [x] Windows Server 2022 in VMware installiert
- [x] Statische IP-Konfiguration verstanden und umgesetzt
- [x] Einen Domain Controller mit Active Directory aufgesetzt
- [x] Die Struktur von AD kennengelernt (Domain, OU, User)
- [x] Eine Gruppenrichtlinie erstellt und verknüpft

---

## Nächste Schritte

- [ ] Zweiten Server als Member Server zur Domain hinzufügen
- [ ] Windows 10/11 Client zur Domain joinen
- [ ] Komplexere GPOs erstellen (Software-Verteilung, Laufwerke)
- [ ] DNS und DHCP Rollen erkunden
- [ ] Backup und Recovery des Domain Controllers

---

## Troubleshooting

### VM bootet nicht von ISO
→ VM Settings → CD/DVD → "Connect at power on" aktivieren  
→ Oder Firmware von EFI auf BIOS ändern (VM Settings → Options → Advanced)

### "Windows cannot find the Microsoft Software License Terms"
→ VMware Easy Install deaktivieren: VM neu erstellen mit "I will install the operating system later"

### Kein Fullscreen
→ VMware Tools installieren

---

## Ressourcen

- [Microsoft Evaluation Center](https://www.microsoft.com/de-de/evalcenter/evaluate-windows-server-2022)
- [Active Directory Documentation](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/)

---

*Dokumentiert als Teil meiner IT-Security-Journey*
