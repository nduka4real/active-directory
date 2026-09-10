me make it clean and well-formatted with markdown.

Active Directory Management Suite
A lightweight, GUI-based Active Directory management tool built entirely in PowerShell 5.1 using LDAP/ADSI. No dependency on the ActiveDirectory PowerShell module or ADWS – it talks directly to any domain controller over LDAP.

Developed by AKPATI NDUKA SUNDAY · github.com/nduka4real

✨ Features
🖥️ Windows Forms GUI – clean, intuitive interface with no external libraries required

👤 User Management – create, edit, delete, enable/disable, reset passwords, view details

👥 Group Management – create groups (Global / Universal / Domain Local), edit descriptions, manage members with a dual‑list interface

🏢 Organizational Unit (OU) Management – create, list, and delete OUs

📥 Bulk CSV Import – create hundreds of users from a CSV file with automatic Domain Users membership

🧪 Sample CSV Generator – one‑click creation of a template CSV file for bulk import

🛠️ AD Tools & Diagnostics – verify LDAP connectivity, open ADUC, copy domain info

📝 Automatic Logging – every action is written to AD_Management_Log.txt for auditing

🔒 LDAP/ADSI Only – no ADWS, no RSAT, no ActiveDirectory module required

📸 Screenshots
(Add your screenshots here – e.g. docs/main-screen.png, docs/bulk-import.png)

⚙️ Requirements
Component	Requirement
Operating System	Windows 10 / Windows 11 / Windows Server 2016+
PowerShell	Version 5.1 or later (built-in on modern Windows)
.NET	.NET Framework 4.5+ (built-in)
Permissions	A domain account with rights to create/modify AD objects
Network	LDAP connectivity to a domain controller (TCP 389 / 636)
🚀 Installation
Clone the repository:

bash


text
AD-Management-Suite/
├── AD_Management.ps1
├── Launch_AD_Tool.bat
└── README.md
No installation of PowerShell modules is required. The script uses only built-in .NET libraries.

🎮 Usage
Right‑click Launch_AD_Tool.bat and select Run as administrator
(or run powershell -ExecutionPolicy Bypass -File .\AD_Management.ps1 manually)

The GUI opens, showing the Main Screen with quick‑access buttons.

Use the top navigation bar to switch between:

USERS – manage domain users

GROUPS – manage groups and membership

OUs – manage organizational units

BULK IMPORT – import users from CSV

AD TOOLS – diagnostics and utilities

📥 Bulk User Import
CSV Format
csv
Username,FirstName,LastName,DisplayName,Email,Description,Password,OU
james.okoro,James,Okoro,James Okoro,james.okoro@domain.lab,Lab User,P@ssword123!,
mary.johnson,Mary,Johnson,Mary Johnson,mary.johnson@domain.lab,Lab User,P@ssword456!,OU=STAFF
Column	Required	Notes
Username	✅	SAM account name (must be unique)
Password	✅	Must meet domain complexity requirements
FirstName	❌	
LastName	❌	
DisplayName	❌	If omitted, uses FirstName LastName
Email	❌	
Description	❌	
OU	❌	Either a simple name (STAFF) or a full DN (OU=STAFF,DC=domain,DC=lab)
Steps
Open the BULK IMPORT tab.

Click Create Sample CSV to generate a template.

Edit the CSV with your users.

Click Browse… to select the file.

Click Import – progress and per‑user results are shown in the log.

Existing users are skipped, not overwritten.

🛠️ AD Tools Tab
Button	Action
Run LDAP Diagnostics	Tests RootDSE connectivity and reports domain info
Open AD Users & Computers	Launches dsa.msc (requires RSAT)
Copy Domain Info	Copies DNS name and DN to the clipboard
Clear Output	Clears the output pane
📝 Logging
All operations are logged to:

text
AD_Management_Log.txt
…in the same directory as the script. Each line is timestamped:

text
[2026-09-10 08:23:35] User created: james.okoro (CN=James Okoro,CN=Users,DC=domain,DC=lab)
[2026-09-10 08:24:02] Added CN=James Okoro,CN=Users,... to group Domain Users
[2026-09-10 08:25:11] Password reset for CN=James Okoro,CN=Users,...
Useful for auditing and troubleshooting.

🔐 Permissions
To perform most actions, the account running the script must have:

Create Child Objects on the target OU (for user/group creation)

Write permission on userAccountControl, member, description, etc.

Reset Password extended right on target users

Running the batch file as Administrator on a domain‑joined machine is usually sufficient for lab environments.

🧯 Troubleshooting
Symptom	Cause / Fix
"A device attached to the system is not functioning"	The password doesn't meet domain complexity, or the account is locked. Try a stronger password.
"Unable to determine the Active Directory naming context"	The machine cannot reach a domain controller. Check VPN / DNS.
"Group 'X' not found"	The group name must match sAMAccountName or cn exactly.
GUI does not open	Ensure PowerShell 5.1 and .NET 4.5+ are installed. Run the batch file from a console to see errors.
Buttons appear cut off	Resize the window (the UI is anchored and scales).
Check AD_Management_Log.txt for the full exception trace of any error.

🗂️ Project Structure
text
AD-Management-Suite/
├── AD_Management.ps1        # Main script (GUI + LDAP logic)
├── Launch_AD_Tool.bat       # Launcher (bypasses ExecutionPolicy)
├── AD_Management_Log.txt    # Auto-generated log file
└── README.md
🤝 Contributing
Contributions are welcome! To contribute:

Fork the repository.

Create a feature branch (git checkout -b feature/my-feature).

Commit your changes (git commit -m "Add: my feature").

Push to the branch (git push origin feature/my-feature).

Open a Pull Request.

Please keep the LDAP/ADSI‑only philosophy – no dependencies on RSAT or the ActiveDirectory module.

📜 License
This project is released under the MIT License. See LICENSE for details.

👤 Author
AKPATI NDUKA SUNDAY
GitHub: @nduka4real

⭐ Acknowledgements
Built with .NET System.DirectoryServices and System.Windows.Forms

Inspired by the need for a portable AD admin tool that works without RSAT

If you find this project useful, please ⭐ star the repository!
