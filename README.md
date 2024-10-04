# Repository Documentation for Metasploit Subdomain Backup File Brute Force Scanner
This repository contains a Metasploit auxiliary module that attempts to find backup files on a list of subdomains via brute force. It includes improved detection mechanisms to minimize false positives, making it a valuable tool for penetration testers and security researchers.

# Features
Scans a list of subdomains for backup files.
Allows for custom user agents.
Implements checks for file size and MIME types to reduce false positives.
Supports both HTTP and HTTPS protocols.

# Installation
To use this module, clone the repository and place the module in the appropriate Metasploit directory. Here’s how you can do it:

Clone the Repository:

git clone https://github.com/yourusername/metasploit-backup-scanner.git

Move the Module: Place the Ruby file into the Metasploit auxiliary directory:

mv metasploit-backup-scanner/backup_scanner.rb /usr/share/metasploit-framework/modules/auxiliary/scanner/http/

msfconsole

# Usage

Load the Module

To use the module, start Metasploit and load the module as follows:

msf6 > use auxiliary/scanner/http/backup_scanner

Set Required Options

You need to set various options to configure the module:


msf6 auxiliary(scanner/http/backup_scanner) > set RHOSTS <target_subdomain_or_ip>

msf6 auxiliary(scanner/http/backup_scanner) > set RPORT <target_port>  # Default is 80

msf6 auxiliary(scanner/http/backup_scanner) > set DOMAIN_LIST <path_to_subdomain_file>

msf6 auxiliary(scanner/http/backup_scanner) > set WORDLIST <path_to_backup_file_names>

msf6 auxiliary(scanner/http/backup_scanner) > set USER_AGENT "<your_custom_user_agent>"  # Optional

msf6 auxiliary(scanner/http/backup_scanner) > set SSL <true|false>  # Optional

msf6 auxiliary(scanner/http/backup_scanner) > set THREADS <number_of_threads>  # Default is 10

msf6 auxiliary(scanner/http/backup_scanner) > set MIN_SIZE <minimum_file_size_in_bytes>  # Default is 5000

'''

### Run the Scanner
Once you have configured the options, run the module:

msf6 auxiliary(scanner/http/backup_scanner) > run

### Example Usage
Here is an example of how to configure and run the module:


msf6 > use auxiliary/scanner/http/backup_scanner

msf6 auxiliary(scanner/http/backup_scanner) > set RHOSTS localhost

msf6 auxiliary(scanner/http/backup_scanner) > set RPORT 70

msf6 auxiliary(scanner/http/backup_scanner) > set DOMAIN_LIST /home/parag/responsible/sublist.txt

msf6 auxiliary(scanner/http/backup_scanner) > set WORDLIST /home/parag/responsible/wordlist.txt

msf6 auxiliary(scanner/http/backup_scanner) > set USER_AGENT "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"

msf6 auxiliary(scanner/http/backup_scanner) > run


Output

Upon running the module, it will check each specified backup file on the given subdomains, outputting results for each request. Here are some example outputs:

[*] Checking http://example.com:70/backup.zip ...

[-] No Response: http://example.com:70/backup.zip

[*] Checking http://example.com:70/backup.sql ...

[+] Found valid backup file: http://example.com:70/backup.sql (Status: 200, Size: 37453 bytes, MIME: application/sql)





