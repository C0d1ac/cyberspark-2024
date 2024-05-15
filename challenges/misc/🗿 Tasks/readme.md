# Cybermaze 2023-2024 MISC Writeups

> Author: Stylish 🗿
> 
> 
> <aside>
> 💡 Linkedin: [https://www.linkedin.com/in/dhia-labiedh/](https://www.linkedin.com/in/dhia-labiedh/)
> 
> </aside>
> 

# **1. Mail is Pain 🗿**

![Untitled](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/9a07a720-fb0b-4bdb-9627-f1be2d802f63)



In this task, we are given a ".eml" file, which is an email that caused malware to be installed on Quiiper’s workstation. Our objective is to analyze this email, extract all Indicators of Compromise (IOCs), and investigate these IOCs to gather more information about the malware.

## Initial Look

we can use an external tool to analyze the provided email file (optional)

PhishTool is a good example: 

[](https://app.phishtool.com/submit)

![Untitled 1](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/2dd34640-0524-407e-96e3-7be4a33ed2af)



there are a couple of things that stand out in this email. First we have the Email Subject 

***“Urgent Security Update”***

This sense of urgency is usually used by Threat Actors to conduct a [phishing](https://www.imperva.com/learn/application-security/phishing-attack-scam/) attack.

![Untitled 2](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/cdb9dcb1-3292-4f82-adeb-5d689bdf60d1)


The email urgent the user Quiiper to click on the blue “**Update Settings”** Button. but after a quick lookup, we can see that the button redirects the user to a strange ip address **`130.185.238.251`**

![Untitled 3](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/634f8787-5790-4580-a40b-438f557c5e29)


This is our First IOC that must be investigated using our Cyber Threat Intelligence (CTI) & Open Source Intelligence (OSINT) Skills.

Let’s analyze this suspicious ip address using any online investigation tool such as [VIRUSTOTAL](https://www.virustotal.com/gui/home/upload)

![Untitled 4](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/e0a2605b-db7c-41a6-9873-c49993f8eb2f)


we can see that this is ip has been flagged as malicious by multiple security vendors. [Threatfox](https://threatfox.abuse.ch/browse/) basically gives us the first part of the flag which is the name of the malware. **SparkRat.**

So let’s continue our investigation in Threatfox’s official website and there we will find the second part of the flag which is the **UUID** of the malware.

![Untitled 5](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/744c58e7-6c5b-4065-81f0-38f62093cb4b)


![Untitled 6](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/79d5ee76-c739-49c5-bcb3-43aa083ddee6)


This is our final flag:

<aside>
💡 Spark{**SparkRat_**d7885d46-ed9a-11ed-9e9b-42010aa4000a}

---

</aside>

---

---

---

---

# **2. From the RockBottom 🗿**

The hint to solving this task relies on another IOC found in the email  which is this strange username `ENGIN33R5PARK`

![Untitled 7](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/61b27e20-8758-4fec-a717-97f44ff335d6)


Let’s use any username OSINT tool such as “**[instantusername.com](https://instantusername.com/?q=ENGIN33R5PARK)**”

![Untitled 8](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/ec3898c1-008c-4e9f-9e08-d71bb01870a8)


we have a few hits, after investigating some of the social media accounts, we find this interesting twitter account:

![Untitled 9](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/ebf1c916-0f7b-47e5-8472-e712e0d4a1b2)


It seems that the hacker has successfully exfiltrated some of our company’s data and he’s selling it in some strange platform:

[](http://engin33r5park.anonblogd4pcarck2ff6qlseyawjljaatp6wjq6rqpet2wfuoom42kyd.onion/p/selling-to-the-highest-bidder)

→ we can see that this link ends with a `.onion` which indicates that it leads to a **TOR site, aka the Darkweb.**

we need a special browser (TOR Browser) to be able to access this .onion website:

![Untitled 10](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/397de9bb-356b-412d-8db4-c2c716e25ed7)


![Untitled 11](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/dd29f763-a312-4d93-a56b-2768ba2f6782)


the .onion link leads us to a blog that leads us to another one drive link tha has a zip file with “important-data” to download.

![Untitled 12](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/96ac9ec3-5d81-43e7-8991-a536d246956e)


However, it seems that this zip file is password-protected!

![Untitled 13](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/36fa6441-aba3-464c-b403-f6fa2fe60a4f)


So, let’s try cracking this password using any crack tool such as **[John The Ripper](https://github.com/openwall/john)**

![Untitled 14](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/39fb6097-4112-48c1-9649-7b9319180a93)


That’s it! with 2 simple commands, and the right wordlist `rockyou`.txt you can easily crack it!

( yeah the task name was a hint about the wordlist. From the `Rock`BOTTOM.)

![Untitled 15](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/d320d5d1-bcf2-496b-8497-ba70cb5fa694)


<aside>
💡 Spark{D4mn_Y0u_Qu!!per}

</aside>

---

---

---

---

# **3. Tactics, Techniques, and Procedures 🗿**

![b67fc944-3d25-43c4-b6fc-907a61154b22](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/ce8cc5f3-e87b-4a30-90f4-bd4331d7a553)


Following the tasks scenario, the threat actor is trying to maintain **Persistence** on the compromised machine, we are asked to determine the identity of this threat actor, the **[MTRE ATT&CK](https://attack.mitre.org)** technique he used, and finally the procedure associated with it. 

→ The provided wallpaper is a huge hint for the first part of our flag. A quick reverse image search gives us the name of this threat actor group which is **`APT3`** 

![Untitled 16](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/30726403-647d-4a0e-af24-29ebaedb9e70)


[APT3, Gothic Panda, Pirpi, UPS Team, Buckeye, Threat Group-0110, TG-0110, Group G0022 | MITRE ATT&CK®](https://attack.mitre.org/groups/G0022/)

![Untitled 17](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/2eca3db5-667b-47a8-9f37-f78792ffc288)


Now all thats left is to find **The Technique and the Procedure:**

[Account Manipulation, Technique T1098 - Enterprise | MITRE ATT&CK®](https://attack.mitre.org/techniques/T1098/)

![Untitled 18](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/b6280be7-f450-43ae-be2c-f71c57e71309)


—> `T1087` 

[APT3, Gothic Panda, Pirpi, UPS Team, Buckeye, Threat Group-0110, TG-0110, Group G0022 | MITRE ATT&CK®](https://attack.mitre.org/groups/G0022/)

![Untitled 19](https://github.com/C0d1ac/cyberspark-2024/assets/120717514/862761cd-301e-4858-b818-211bbb56acfb)

<aside>
💡 Spark{apt3_T1098_G0022}

</aside>




> Thank you to all the participants for your enthusiasm and dedication. Your efforts and skills made this year **Cyberspark** CTF a great success. We look forward to seeing you in future events!
> 

```powershell
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣼⡇⣸⡿⠟⠁⠀⢀⣶⣶⠄⠀⠀⠀⠈⠉⠻⣿⠿⣦⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣾⣿⠇⡿⠁⠀⣀⣴⠟⠉⠁⠀⠀⠀⠀⠀⠀⠀⠈⢢⡈⢻⣷⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣼⣿⣋⠀⠀⢀⡾⠟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠁⠈⠙⠷⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣸⣿⣿⠇⠀⠀⠈⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣿⣿⠇⠀⠀⠀⠀⠀⠀⠀⣀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢶⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣿⡿⠁⠀⠀⠀⠀⠀⣀⣤⣤⣤⣤⣤⣤⣤⣤⣤⣤⣄⣀⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣸⣿⠁⠀⠀⠀⠀⠀⠐⠛⠛⠿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣶⣶⣶⣴⣶⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢰⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠿⠟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣿⠃⣀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢹⣿⣿⣿⠿⠿⣿⣿⣿⣿⣿⣿⠇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣾⡟⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢡⡀⠀⠀⠙⢿⣿⣿⡃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣿⡏⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢹⣦⠀⠀⠀⠉⠈⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣾⡿⠃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢻⣷⡄⠀⠳⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣼⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠹⣷⡄⠀⠹⣧⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣰⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣇⠘⢿⣦⠀⢹⡆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣿⡟⠀⠀⠀⠀⠀⠀⠀⠀⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠙⣷⣄⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣾⣿⣷⣀⠀⠀⠀⠀⣀⣠⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠉⠁⠀⠀⠀⠈⠻⠿⢷⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢰⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠛⠀⠀⠀⠀⠀⠀⠀⠀⣀⣠⣄⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣰⣆⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣾⣿⣿⣿⣿⣿⣿⣿⠿⠛⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠙⢿⣿⣿⣿⣿⣷⣶⣶⣶⣶⣶⣶⣶⣷⣾⣿⣿⣿⣦⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣿⣿⣿⣿⣿⡿⠛⠋⠀⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠟⠛⠉⠉⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣸⣿⣿⠟⠃⠉⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠙⠛⠻⠿⣿⣿⣿⣿⣿⣿⣷⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣀⣀⣠⣿⣿⠿⠓⠂⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠉⠛⠻⠿⣿⣿⡆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣠⣤⣤⣤⣤⣶⣶⣶⣦⣤⣤⣴⣶⣾⣿⣿⣿⣿⣿⣿⠟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠙⢿⣿⣿⣿⣿⣿⣿⣿⣷⣶⣶⣶⣤⣤⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣴⣾⣿⣿⠟⣭⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣟⣹⣍⢰⣿⣆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠁⠀⣹⣿⣿⣿⣿⣯⣿⣿⣿⣿⣿⣿⣿⡟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⢀⣠⣾⣿⣿⣿⠋⣴⣿⣿⠿⠛⣀⣼⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣄⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢹⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⡟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⣰⣿⣿⣿⣿⠛⣡⣾⣿⣫⣴⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡟⠻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣶⣤⣀⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠩⣿⣿⣿⣿⣿⣿⣿⣿⣿⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⣴⣿⣿⣿⣿⣇⣴⡿⢛⣿⣿⠿⠻⠛⠛⠛⣹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣇⠀⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣶⣤⣄⣀⠀⠀⠀⠀⠀⠀⠀⠀⠈⣿⡇⢿⠿⣿⢿⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⢰⣿⣿⣿⣿⣿⣿⠏⣠⣿⣿⠏⠀⢀⣤⣴⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡆⢀⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣶⣦⣤⣤⣤⣴⣿⣦⣤⣤⣶⣿⡟⢦⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢀⣿⠏⣸⣿⣿⣿⠇⣰⣿⡿⠁⢠⡀⢸⣿⣿⣿⣿⡿⠿⠛⢿⣿⣿⣿⣿⣿⣿⣿⣾⡏⠙⢿⣿⣿⣿⣿⣿⡉⢙⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣋⠀⠀⠻⣦⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⢀⣴⣾⠏⠀⣿⣿⣾⣿⠀⣿⡿⠁⢀⣿⣧⣿⣿⣿⠟⠋⠀⢠⣴⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣶⣼⣿⣿⣿⣿⣿⣷⣼⣿⣿⣿⣿⣿⣿⣿⣿⣿⠿⠛⠉⠉⢿⡿⠿⢿⡛⢻⣿⣿⣿⠿⠛⠃⣀⣀⠈⢻⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⣰⣿⣿⠃⠀⠀⢿⣿⣿⣿⣾⣿⠇⠀⣿⣿⣿⡿⣫⣅⠀⠀⠀⢸⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠿⢿⣿⣷⣿⣿⣿⣿⡿⠟⠁⣹⣷⣤⣤⣤⣤⣤⠀⠀⢸⣿⣾⣿⣏⠀⠀⠀⠀⠈⠻⡀⠀⠙⢷⣤⣀⠀⠀⠀⠀⠀⠀⠀
⣾⣿⢻⣿⣧⡄⠀⠈⣿⣿⣿⣿⣿⣶⣾⣿⢟⣽⣿⡿⠿⠀⠀⠀⢼⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠟⠀⠀⠻⣿⣿⣿⣿⣿⣷⣶⣾⣿⣿⣿⣿⣿⠛⠋⠀⢠⣾⣿⣿⡋⠙⣻⠒⢤⣤⣀⠀⠁⠲⢦⡀⠀⠙⢷⣄⠀⠀⠀⠀⠀
⠛⠁⣾⣿⣿⣇⣰⣸⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣧⣄⡀⠀⠀⠀⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣤⡆⠀⢀⣿⣿⣿⠀⠉⠙⢿⣿⣿⣿⡛⠉⠉⠀⠀⣠⣾⣿⡟⠋⠀⠀⠋⠀⠀⠀⠹⣿⡿⠆⢀⠛⠀⠀⠀⠙⢷⡄⠀⠀⠀
⠄⢀⣿⣿⣿⣿⠋⠀⢙⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡟⢸⣿⡄⢀⣤⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣧⣤⣾⣿⣿⣿⣷⣶⣄⠀⠙⣿⣿⣿⣶⣶⣄⡘⠛⣿⣿⠀⠀⢰⣿⣦⡄⠀⠀⠀⠁⠀⠀⢸⣷⡀⠀⠀⠀⠈⢻⡄⠀⠀
⣡⣿⣿⣿⣿⠏⢀⣴⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠈⣿⣿⢸⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠃⢻⣿⣿⣿⣿⣷⣀⣿⢿⣿⣿⣿⣿⡇⢸⣿⣿⠀⠀⢀⡘⢿⣷⠀⠀⢰⣄⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⢿⡀⠀
⣿⣿⣿⠟⠁⣠⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠀⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠏⠀⠘⣿⣿⣿⣿⣿⣿⣇⠘⠟⠻⣿⣿⡇⣼⣿⣿⠀⠀⣼⣿⡄⠉⠱⣷⣌⢿⣦⡀⢀⣿⣷⠀⠀⠀⠀⠀⢸⣇⠀
⣿⡿⢁⣴⣿⣿⡟⣹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⠀⠈⢻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠀⠀⣿⣿⣿⣿⣿⣿⣿⣿⣧⠀⠀⣿⣿⣿⣿⣿⣿⠀⢸⣿⣿⣷⠀⢠⣼⣿⣷⣿⣿⣿⣿⣿⠀⠀⠀⠀⠀⠘⣿⠀
⣿⣣⣾⣿⢿⣿⣿⣿⣿⣿⣿⣿⣿⠏⠉⢿⣿⣿⣿⣿⡄⠀⣼⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠀⠀⢠⣿⣿⣿⣿⣿⣿⣿⡏⢻⣷⣾⣿⣿⣿⣿⣿⣿⠀⢸⡟⢿⣿⣦⢸⣿⣿⣿⣿⣿⣿⠟⠁⠘⠀⠀⠀⠀⢀⣿⠀
⣿⣿⣿⢧⣾⣿⣿⣿⣿⣿⣿⠟⠁⠀⠀⠘⣿⣿⣿⣿⣧⣰⣿⣿⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠀⢠⣿⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⣿⣿⣿⣿⣿⣿⣿⣇⣼⡇⠸⣿⣿⡏⢻⣿⣿⣿⣿⣿⡀⣴⣦⠀⠀⠀⠀⣸⡿⠀
⣿⣿⣿⣾⣿⣿⣿⣿⣿⠟⠁⠀⠀⠀⠀⠀⠘⢿⣿⣿⣿⣏⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⢠⣾⣿⣿⣛⣻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠃⠀⢸⣿⣧⣸⣿⣿⣿⣿⣿⣿⡏⢹⠁⠓⠀⣤⡿⠀⠀
⣿⣿⣿⣿⣿⡿⠟⠋⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢻⣿⣿⣿⠿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠁⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⡻⣿⡏⢸⣿⣿⣿⣿⣇⣀⠀⠀⢀⣿⠁⠀⠀
⣿⣿⡿⠉⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠹⣿⣿⡆⠹⣿⣿⣿⣻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠙⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⣹⣧⢸⣿⣿⣿⣟⣉⠉⠀⡴⠃⠘⣧⠀⠀
⣿⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣆⠈⠻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣰⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠿⣿⢉⣿⣿⣯⣿⣿⣿⣿⣿⡟⠛⠛⠛⠀⠀⠀⢹⣇⠀
⣿⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠘⣿⣿⣿⠀⠀⣬⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡟⢀⡈⢨⣿⣿⡟⠛⠛⠙⠛⠛⠇⠀⠀⠀⢠⡀⠀⠀⣿⡄
⣿⣿⣷⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣶⣶⣶⡀⠀⣿⣿⣿⣷⣾⣿⣿⢠⣦⡀⠀⠈⠉⣙⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⢃⣾⣿⠇⠈⠁⠀⣿⣿⣷⡀⠀⠀⠀⢀⣤⡀⠀⠀⠘⣧⠀⠀⢸⡇
⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣿⣿⣿⠇⠀⢻⣿⣿⣅⣿⣿⣿⠈⠉⣁⣤⣶⣾⣿⣿⣿⣿⡿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⣿⠀⠀⢠⠀⢿⣿⢿⣷⣤⣀⠀⠀⠻⣿⣄⠀⠀⢹⡄⠀⠘⣷
⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣿⣿⣶⣿⣿⣿⣿⣿⣿⢁⣠⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⢨⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠿⣻⣿⣿⣿⣿⠀⠀⠘⡇⢸⣿⣿⣿⣿⣿⡆⠀⠀⢈⠻⢷⣄⠀⣇⠀⠀⣿
⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣼⣿⣿⣿⣿⣿⡟⣿⣿⣿⣿⣿⢸⣿⠿⠿⢿⣿⣿⣿⣿⣿⣿⣧⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡏⠻⣿⣿⣿⣿⠏⣱⡿⠁⢀⣼⣿⣿⡇⠀⠀⢃⠈⣿⣿⣿⣿⣾⣿⡄⠀⠸⣷⣄⢻⣧⠈⠀⢠⣿
⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⣿⣿⣿⣿⣷⢹⣿⣿⣿⣿⠀⠀⠀⢰⣿⣿⣿⣿⣿⣿⣿⡟⢿⣿⣿⣿⣿⣿⡿⣿⣿⣿⣿⠿⠿⣿⣟⣡⣾⠛⠁⢀⣼⣿⣿⣿⣇⠦⠠⢼⡆⠸⣿⣿⣿⣿⣷⣥⠀⠀⠘⣿⣾⡟⠃⠀⢸⡇
⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⢰⣧⡈⣿⣿⣿⣿⣿⣿⣏⡅⢨⣿⣿⣿⣿⣿⣷⣿⣿⣷⡆⠀⢠⣿⣿⠟⠁⠀⠀⠘⣿⣿⣿⣿⣿⣿⡷⠄⢹⣶⣿⣿⣿⣿⣿⣿⡀⠀⠀⢨⣿⡇⠳⠀⠸⠇
⣿⣿⣿⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣿⠛⠛⣿⣿⣿⠋⣿⣿⣿⣷⣾⣿⣾⣿⣿⣿⣿⣿⣿⣿⣛⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣧⣴⣿⣿⣷⣶⠆⠀⠀⠀⠛⠛⠋⠉⠉⣿⣷⠀⣸⣿⣿⣿⣿⣿⣽⣿⣿⣆⣀⢿⣿⣷⡀⠀⠀⠀
⣿⣿⣿⣿⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣾⣿⣿⡿⠀⠀⣿⡇⢸⢰⣿⣿⣿⡿⢹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠿⠛⠁⢹⣿⡟⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⢰⣿⣿⣿⡿⢿⣿⣿⣿⡟⠘⠛⠀⣿⣿⠉⠀⠀⠀
⣿⣿⣿⣿⣷⠀⠀⠀⠀⠀⠀⠀⠀⢀⣿⣿⣿⡇⠀⠀⣿⣧⡀⣸⣿⣿⣿⡇⢸⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠃⠀⠀⢠⣿⣿⣿⣿⡿⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⣾⣿⣿⡏⠶⣾⣿⠟⠋⠀⠀⠀⠀⢿⣿⡆⠀⠀⠀
⣿⡟⣿⣿⣿⣧⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣿⡇⠀⠀⢻⣿⣿⣿⣿⣿⣿⣇⣼⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠀⠀⠀⢸⣿⣿⣿⡟⠁⠀⠀⠀⠀⠀⣀⣠⣾⣿⣿⠋⠉⣿⣄⠀⠈⠁⠀⠀⠀⠀⠀⠀⢸⣿⡏⠀⠀⠀
⠿⣿⣿⣿⣿⣿⣷⡀⠀⠀⣀⣀⠀⣸⣿⣿⣿⡀⠀⠀⠈⣿⣿⣿⣿⣿⣿⡿⢿⡛⢻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡟⠋⠀⠀⠀⠀⣾⣿⣿⣿⣄⣀⣀⣠⣤⣶⣿⣿⢿⣿⣟⣋⣀⡀⢨⠻⣷⣄⡀⠀⠀⠀⠀⠀⠀⣼⣿⣷⡄⠀⠀
⣿⣿⣿⣿⣿⡿⠿⣿⣾⣿⣿⣿⣿⡿⢿⣿⣿⡇⠀⢀⣾⣿⣿⣿⣿⣿⣿⣷⣤⠀⢹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡄⠀⠀⠀⢀⢋⣿⣿⡿⢋⣭⣿⠿⠿⠏⠉⢹⣿⣿⢿⣿⣿⣿⣿⣿⣮⣿⣿⣦⣄⡀⣀⣀⣴⣿⣟⣻⠀⠀⠀
⣿⡿⠛⣫⣤⣴⣾⣿⣿⣿⣗⡿⣿⣿⣷⣿⣿⣿⣤⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣶⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣶⣦⣶⣿⣿⣿⣿⣾⡿⠟⢁⣶⠀⢀⣴⣀⣻⣯⣤⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⢋⣟⠛⠀⠀⠀
⣿⣦⣼⣿⢿⣿⣿⣿⣿⣟⢻⣿⣿⣿⣍⡛⠻⢿⣿⡿⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠿⠿⠿⠿⠟⠋⢁⣀⣀⣀⣠⣴⣿⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡽⡿⣿⣿⡿⢿⣿⠇⠀⠀⠀
⣤⣿⣿⣿⣷⣙⢿⣿⣿⣿⣷⣿⣿⣯⣿⣿⣶⣤⣤⣀⣻⣿⣿⣿⡿⠋⠀⠀⠉⠉⠙⣻⡿⢿⣿⠿⠿⠟⠛⠉⢻⣿⣁⣨⣿⠀⣀⣀⡀⠀⠀⢈⣩⣿⣿⡿⠿⠛⣛⣻⣿⣯⣽⣿⣿⣿⣿⣿⣿⣿⣿⣿⣯⣿⠿⣷⣶⣿⣇⣰⣿⠀⠀⠀⠀
⠟⠛⠛⠿⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣍⠙⢿⣿⣿⡿⠋⠙⠶⠶⠀⠀⠀⢀⠀⠘⠛⠷⢶⣦⣤⣤⣤⣴⣦⣤⣽⣿⣿⣏⣀⣉⣉⣩⣵⣾⣿⣿⣿⣶⣶⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣦⣼⣿⣷⣿⣿⣿⣿⣿⣿⡀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠉⠉⠻⣿⣿⣿⣿⣿⣿⣿⣿⣾⣿⣿⣷⣦⣀⣄⠀⠀⠀⠀⠘⠻⠿⠶⣶⣦⣭⣛⠛⢛⣋⣈⣙⣿⣷⣾⣿⣿⣿⣿⣿⣿⣿⣿⡟⠻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠟⠛⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠉⠻⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⢿⠇⠀⠀⠀⠀⠀⠀⠀⠈⠙⢿⣿⣷⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣏⣹⣿⣿⣿⣿⡆⠈⠛⢻⣿⣿⣻⣿⣿⣿⣿⣿⡟⠋⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⡀
⣀⡀⠀⠀⠀⠀⠀⠀⠀⠠⣴⣶⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣤⣄⠀⠀⠖⠀⠀⢀⣀⣤⣦⣼⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠛⠉⠉⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠙
⣋⠁⢀⣀⣤⡀⣤⣄⣠⣤⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣶⣿⣿⠿⠻⣿⡁⣠⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⣀⠀⢠⣤⣦⣽⣯⣬⣹⠉⣭⣭⢉⡉⠀⢈⢉⣿⡏⣿⣧⣶⣾⣿⣵⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣤⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢷⣤⣤⣶⣶⣄⢤⣄⠤⣤⣀⡀
```
