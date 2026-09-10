# Assignment PF-04: Personal Website Live & DNS Infrastructure Walkthrough
**Student:** Aayush Kumar Singh  
**Track:** General AI Fluency (Week 5)  
**ID:** `PF-04`  

---

## 1. Production Deployment & Live HTTPS URL
* **Live Website URL:** `https://frontend-ai-capstone.vercel.app` (or `https://aayush9-spec.github.io/frontend-ai-capstone/`)
* **Hosting Platform:** Vercel Global Edge Network / GitHub Pages (HTTPS SSL enabled).
* **Cross-Device Verification:** Tested in private incognito window on iOS Safari and Desktop Chrome.

---

## 2. DNS Infrastructure & Resolution Walkthrough (Teaching Non-Technical Team Members)

### What Happens When You Type `https://frontend-ai-capstone.vercel.app` in Your Browser?

1. **Step 1: Browser Cache & Recursive Resolver Query**  
   Your browser asks your computer's OS: *"Do we already know the IP address for frontend-ai-capstone.vercel.app?"* If not, the request goes to your ISP's **DNS Recursive Resolver** (e.g. `8.8.8.8`).
2. **Step 2: Root & TLD Nameservers**  
   The resolver queries the **Root Nameserver** (`.`), which points to the **`.app` TLD (Top Level Domain) Nameserver**. The `.app` nameserver points to Vercel's **Authoritative Nameservers** (`ns1.vercel-dns.com`).
3. **Step 3: CNAME & A/AAAA Record Lookup**  
   - **A Record:** Maps a domain name directly to an IPv4 address (e.g., `76.76.21.21`).
   - **CNAME Record (Canonical Name):** An alias that points one domain name to another domain name (e.g., `frontend-ai-capstone.vercel.app` -> `cname.vercel-dns.com`).
4. **Step 4: TLS / HTTPS Handshake & Response**  
   Once the IP address is returned, your browser initiates an encrypted **TLS 1.3 Handshake** to establish an HTTPS connection, securing data in transit with a valid SSL certificate.

---

## 3. Deliverable Verification Links
* **Live Deployed Portfolio URL:** https://frontend-ai-capstone.vercel.app
* **DNS Walkthrough Document:** https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/week5/pf04_dns_walkthrough.md
