## Passive Recon (No Active Scanning)

(Note: Physical/Social - Go onsite, social engineering. Photos, drone footage)

- Location, images
- Job information, employee names, numbers, managers, badges

## Identifying the Target

- Public bug bounty programs (Bugcrowd)
- Rules of Engagement (ROE) - Always check in scope! ALWAYS check out of scope!

### HUNTER.IO

Gather email addresses  
Website: [www.hunter.io](https://www.hunter.io)

- Free plan = about 20 searches per month
- Putting in a domain (e.g., tesla.com) will produce names and emails @tesla.
- It will also provide the source of the email address.
- Sometimes names will be associated with job role or department.
- Can give clues as to email formats and potentially valid usernames.
- Combine with a LinkedIn search.
- Knowing the email format can enable password spraying.

### Breached Credentials

- Website: [github.com/hmaverickadams](https://github.com/hmaverickadams)
- Breach parse tool (bash script)
- Provides a 40+ GB file
- Data files containing emails and passwords collated from credential dumps
- Heath provides a tool to search through given an email domain (e.g., @tesla.com) and place into a file (tesla.txt)

Credential stuffing is when you know the password for a credential and try different formats.

Password spraying - Take known credentials and spray common passwords at them to get a hit.

## Web Info Gathering

### Hunting Subdomains

Tool - Sublist3r

- Install with `apt install sublist3r`
- Run with `sublist3r -d tesla.com`
- Use `-t` for threads to speed it up

ALT Certificate Fingerprinting

- Open browser and go to [crt.sh](https://crt.sh)
- This will find subdomains
- Enter domain and it will return listed certificates

Better tool - OWASP AMASS

- Use GitHub to install and use
- Slow, takes a long time to run

Subdomains - Important to ensure we check ALL possible domains, not just limited to a single domain.

### Identify Web Technologies

Website: [www.builtwith.com](https://www.builtwith.com)

- Enter domain and get back a list of technologies and features
- Check frameworks

Better to use Wappalyzer

- An addon for Firefox
- Built into the browser
- Requires navigation to the site and click Wappalyzer
- Knowing technology can give an indication of possible vulnerabilities
- You can enumerate version numbers on tech, looking for active vulnerabilities

Built into Kali - WHATWEB

- `whatweb <url>`
- Harder to read but can give additional info and versions

### Gathering Info with Burp Suite

- Built into Kali, free version is fine
- Burp is a web proxy, it will intercept traffic
- Steps:
  1. Temp project > Next > Start Burp
  2. Go to Firefox > Preferences > Settings
  3. Manual proxy config
  4. 127.0.0.1 port 8080 for all protocols
  5. New tab, go to [https://burp](https://burp), accept if prompted
  6. Click CA certificate, save file
  7. Go back to preferences
  8. Privacy and security
  9. New certificate
  10. Select the cert
  11. Select both checkboxes, then import
  12. Go to a website, it won't load as Burp is intercepting packets, either turn off or forward
  13. Look at responses to requests for info
  14. Note - Server names are information disclosure, low but still important

### Google Fu

- Know how to Google things
- Use Google search syntax >>> Google it
- To narrow down to just the site, use `site:`
  - Example: `site:tesla.com`
  - Remove "www" to get subdomains: `-www`
- Looking for files: `filetype:`
  - Example: `site:tesla.com filetype:pdf`

### Social Media

- OSINT (Open-source intelligence) - Use LinkedIn and Twitter
- Go to company page, images, probably badge photos
- People and positions
- Can use scrapers to get names
- Enter names into email format
- Get all the info on the people
