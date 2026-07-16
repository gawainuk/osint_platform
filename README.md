# White Hawk Labs OSINT Platform
## User Guide

**Version: July 2026**

---

## Table of Contents

1. [What is the Platform?](#1-what-is-the-platform)
2. [Getting Access](#2-getting-access)
3. [Your Dashboard at a Glance](#3-your-dashboard-at-a-glance)
4. [Running Your First Scan](#4-running-your-first-scan)
5. [Understanding Your Results](#5-understanding-your-results)
6. [Working with Findings](#6-working-with-findings)
7. [Annotating and Triaging Findings](#7-annotating-and-triaging-findings)
8. [Targets and Monitoring](#8-targets-and-monitoring)
9. [Domain Groups](#9-domain-groups)
10. [Username Enumeration](#10-username-enumeration)
11. [Threat Intelligence](#11-threat-intelligence)
12. [Quarterly Reports](#12-quarterly-reports)
13. [Exporting Data](#13-exporting-data)
14. [Account and Team Management](#14-account-and-team-management)
15. [Third-Party Integrations](#15-third-party-integrations)
16. [User Roles and Permissions](#16-user-roles-and-permissions)
17. [Frequently Asked Questions](#17-frequently-asked-questions)

---

## 1. What is the Platform?

White Hawk Labs OSINT Platform is a professional threat intelligence
and open-source intelligence (OSINT) tool designed for security teams,
analysts, and investigators.

You provide a target — a company domain, organisation name, or person
of interest — and the platform automatically gathers intelligence from
hundreds of public sources in parallel:

**Infrastructure** — open ports, exposed services, cloud storage
buckets, TLS certificates, JARM fingerprints for C2 infrastructure
detection

**Domain threats** — typosquatting domains designed to impersonate
your brand, IDN homograph attacks, newly registered lookalike domains

**Technology exposure** — what software is running on the target's
web presence and whether it has known CVEs (from the NIST NVD
catalogue)

**Company intelligence** — company registration data from UK Companies
House, US SEC EDGAR (for listed companies), and OpenCorporates (global
coverage), including directors, officers, and persons of significant
control

**People** — company directors and officers, LinkedIn profiles, GitHub
employees, username enumeration across 600+ social platforms

**Email** — harvested email addresses, predicted email patterns for
known directors, breach exposure via Have I Been Pwned

**Reputation** — VirusTotal checks, Spamhaus ASN listings, AbuseIPDB
scores, ThreatFox C2 intelligence

**Threat actor attribution** — whether findings match known threat
actor tactics, techniques, and infrastructure from the MITRE ATT&CK
database

All findings are scored, risk-weighted, and presented in a structured
report that an analyst can review, annotate, and export.

---

## 2. Getting Access

### Accepting your invitation

Your administrator will send you an invitation email from
`noreply@whitehawklabs.com`. The email contains an
**Accept Invitation** button and a backup URL.

1. Click **Accept Invitation**
2. You will be taken to the platform registration page
3. Set your password (minimum 12 characters, must include uppercase,
   lowercase, and a number or symbol)
4. Click **Create Account**
5. You will be logged in automatically

> **Invitation links expire after 7 days.** If yours has expired,
> ask your administrator to resend it from the Users panel.

### Logging in

Navigate to `https://osint.whitehawklabs.com` and enter your email
address and password. Your session lasts 60 minutes of inactivity,
after which you will need to log in again.

### Forgotten password

Click **Forgot password** on the login page, enter your email address,
and follow the link in the reset email. Password reset links expire
after 1 hour.

---

## 3. Your Dashboard at a Glance

After logging in you will see the main navigation on the left side and
the dashboard in the centre. The navigation includes:

| Nav item | What it is |
|----------|-----------|
| **Jobs** | All scan jobs — running, complete, and historical |
| **Targets** | Saved targets with monitoring, history, and domain groups |
| **Threat Intelligence** | IOC feed, threat actors, sector reports, quarterly reports |
| **Admin** | Organisation settings, users, API keys, and third-party integrations |

The bell icon in the top right shows your notifications — alerts from
monitoring rescans, IOC cross-matches, and digest activity.

---

## 4. Running Your First Scan

### Step 1 — Go to Jobs

Click **Jobs** in the navigation. Click the **+ New Scan** button.

### Step 2 — Fill in the target profile

The scan form asks for:

**Domain** *(required)*
The primary web domain of the target organisation.
Example: `acmecorp.com`

**Organisation name** *(required)*
The full legal or trading name of the organisation.
Example: `Acme Corporation`

**Director names** *(optional but recommended)*
Full names of company directors, separated by commas. These are used
for email pattern discovery, LinkedIn lookup, and username enumeration.
Example: `Jane Smith, John Doe`

**VIP names** *(optional)*
Additional key personnel — executives, senior managers, technical leads.
Example: `Sarah Jones, Mike Williams`

> **Tip:** If you are scanning a UK-registered company, the platform
> automatically retrieves director names from Companies House. For
> US-listed companies, SEC EDGAR data is retrieved automatically.
> For other jurisdictions, provide director names manually or configure
> an OpenCorporates integration key.

### Step 3 — Submit and wait

Click **Run Scan**. The platform will:

1. Accept your job and show it as **Pending**
2. Dispatch parallel intelligence modules (typically 8–10 modules
   running simultaneously)
3. Merge all results and calculate risk scores
4. Enrich findings with threat intelligence
5. Mark the job **Complete** — typically within 2–5 minutes

You can watch the progress in real time. The state indicator cycles
through: `Pending → Routing → Running → Merging → Enriching → Complete`

---

## 5. Understanding Your Results

### The Overview tab

When a scan completes, click on it to open the results. The **Overview**
tab shows:

**Risk score** — a number from 0 to 100

This is the headline measure of threat exposure. It is calculated from
all findings weighted by severity and adjusted by active threat
intelligence signals.

| Score range | Label | Meaning |
|------------|-------|---------|
| 75–100 | Critical | Significant active threats requiring immediate attention |
| 50–74 | High | Serious exposure — prioritise remediation |
| 25–49 | Medium | Notable findings worth addressing |
| 0–24 | Low | Minimal exposure detected |

**Threat Climate Indicator**
A multiplier applied when threat actors attributed to findings in this
scan have recently appeared in live intelligence feeds. A lightning bolt
(⚡) on a finding means its risk score has been elevated because the
attributed threat actor is currently active in real-world attacks.

**Finding summary**
A breakdown of findings by category — Infrastructure, Domain Threats,
Technology, Company Intelligence, People, Email, Reputation — with
counts and risk contribution per category.

**Risk score timeline**
If this target has been scanned before, a sparkline shows how the risk
score has changed across scans.

### The Findings tab

All individual findings are listed here, sorted by risk weight
(highest first by default). Each finding shows:

- **Type** — what kind of finding it is (e.g. `typosquat_domain`,
  `technology_cve_exposure`, `jarm_c2_match`, `company_officer`)
- **Value** — the discovered data (a domain, IP, CVE ID, person name, etc.)
- **Confidence** — how certain the platform is about this finding
- **Risk weight** — contribution to the overall risk score
- **Status** — whether an analyst has reviewed it

### The Changes tab

If this is not the first scan of this target, the Changes tab shows
what is **new**, what has **disappeared**, and what has **changed**
compared to the previous scan. This is the most important tab for
monitoring workflows — it tells you exactly what changed in the
target's exposure profile since you last looked.

### The Graph tab

An interactive visualisation of all findings grouped by category.
Nodes represent finding types; edges show relationships between them.
Click any node to highlight related findings.

---

## 6. Working with Findings

### Filtering findings

Above the findings list, use the filter bar to narrow results:

- **Category** — filter by Infrastructure, Domain Threats, Technology,
  Company Intelligence, People, Email, or Reputation
- **Status** — show only unreviewed, under review, or reviewed findings
- **Priority** — filter by analyst priority
- **Search** — search by finding value (domain, IP, CVE ID, person name)

### Opening a finding

Click any finding row to open the **Annotation Panel** on the right.
This shows:

- The full finding value and metadata
- Confidence score and risk weight
- IOC enrichment results (ThreatFox, AbuseIPDB) where applicable
- ATT&CK attribution badges if threat actors were identified
- For email findings — a **Check HIBP** button to check breach exposure
- Analyst annotation fields (see section 7)
- Full annotation history — every change ever made, by whom, and when

### IOC Enrichment

For findings that represent potential indicators of compromise (IP
addresses, suspicious domains, file hashes), you will see an
**Enrich IOC** button. Clicking this queries:

- **ThreatFox** — checks whether this IOC is a known malware C2
  indicator, including the malware family and confidence score
- **AbuseIPDB** — for IP addresses, checks the abuse confidence
  percentage and community report count

Enrichment results are cached for 24 hours. If you enrich an IOC
today and open the finding tomorrow, the cached result is shown with
a timestamp.

### JARM C2 matches

If the platform detects that a service's TLS fingerprint (JARM hash)
matches known command-and-control infrastructure, a `jarm_c2_match`
finding appears with a red badge. These are automatically enriched
and ATT&CK-attributed where possible. A JARM C2 match is one of the
highest-confidence finding types the platform produces.

### CVE exposure

The `technology_cve_exposure` finding type appears when a detected
technology has a known CVE with a CVSS score of 4.0 or above. Each
finding links to the NVD advisory and includes the CVSS score and
severity rating. If the CVE also appears in the CISA Known Exploited
Vulnerabilities catalogue, the risk weight is further elevated.

### Company intelligence findings

For UK companies, US-listed companies, and companies found via
OpenCorporates, the platform creates:

- `company_registration` — registered name, address, incorporation
  details, and a link to the source registry
- `company_officer` — directors and officers (with role and
  appointment date where available)
- `person_significant_control` — beneficial owners holding >25% of
  shares or voting rights (UK Companies House)

Officer names discovered through any registry are automatically fed
into username enumeration and email pattern discovery.

### Typosquat deep dive

When you confirm a `typosquat_domain` finding as a true positive
(see section 7), the platform automatically runs a deep-dive
investigation on that domain — WHOIS registration, DNS resolution,
ThreatFox and AbuseIPDB checks, and technology fingerprinting of
the typosquat domain itself. Results appear in the annotation panel
within 30–60 seconds.

---

## 7. Annotating and Triaging Findings

Annotation is how analysts record their assessment of each finding.
All annotation changes are permanently recorded in the audit history
and cannot be deleted or altered.

### Review status

Tracks where a finding is in the analyst workflow:

| Status | Meaning |
|--------|---------|
| **Unreviewed** | Default — not yet looked at |
| **Under Review** | Being actively investigated |
| **Reviewed** | Assessment complete |
| **Escalated** | Needs senior analyst or incident response attention |
| **Closed** | No further action required |

### Assessment status

Your verdict on whether the finding represents a real threat:

| Assessment | Meaning |
|-----------|---------|
| **Needs Verification** | Uncertain — more investigation needed |
| **Confirmed True Positive** | Real threat — take action |
| **Likely True Positive** | Probably real — treat with caution |
| **Likely False Positive** | Probably not a real threat |
| **Confirmed False Positive** | Definitively not a real threat |
| **Duplicate Finding** | Already captured elsewhere |
| **Known Infrastructure** | This is your own or a known-good asset |

> **Important:** Setting a finding to **Confirmed True Positive**
> triggers automatic follow-up actions. For typosquat domains, this
> launches the deep-dive investigation automatically.

### Analyst priority

| Priority | Meaning |
|----------|---------|
| **Critical** | Immediate action required |
| **High** | Address within 24 hours |
| **Medium** | Address within the week |
| **Low** | Monitor — no immediate action |
| **Accepted** | Risk accepted — will not be addressed |

### Action tags

36 pre-defined tags organised into 8 categories let you label findings
with specific actions or observations:

- `block_ip`, `block_domain`, `sinkhole_domain`
- `notify_registrar`, `submit_takedown`
- `patch_immediately`, `update_software`
- `monitor_closely`, `watchlist_added`
- `ioc_found_threatfox`, `tor_exit_node`, `malware_infrastructure`

Some tags are applied automatically based on finding type and
enrichment results. All tags are included in PDF and STIX exports.

### Analyst notes

A free-text field for any observations, investigation notes, or
context you want to record. Notes are included in the annotation
history and in PDF report exports.

---

## 8. Targets and Monitoring

### What is a Target?

A Target is a saved scan profile for an organisation you want to
track over time. Instead of manually submitting a new scan job each
time, you save the target once and the platform rescans it
automatically on your chosen schedule.

### Creating a Target

From the **Targets** tab, click **+ New Target**. Fill in the same
fields as a scan job (domain, organisation name, optional directors
and VIPs). The target is saved and you can scan it on demand or
enable monitoring.

### Enabling monitoring

On any target card, toggle **Monitoring**. You will be asked to choose
a scan interval:

| Interval | Availability |
|----------|-------------|
| Daily | Professional and Enterprise plans |
| Weekly | All plans |
| Fortnightly | All plans |
| Monthly | All plans |

The schedule block on the target card shows next scheduled scan date,
last scan date, and last risk score (colour-coded).

### Monitoring notifications

When an automated rescan completes and finds new or disappeared
findings, you receive a notification linking directly to the
**Changes** tab of that scan. Rescans with no changes produce no
notification — you are only interrupted when something actually
changed.

### Target History Dashboard

Click the **📈** button in the Targets header to open the Target
History Dashboard. This shows all your targets as cards with:

- A sparkline of risk score across the last 10 scans
- Trend arrow (↑ rising, ↓ falling, → stable)
- Delta badges showing new findings (+N) or resolved findings (-N)
  from the most recent scan
- Next scan date for monitored targets

Click any target card to expand its full scan timeline.

---

## 9. Domain Groups

Domain Groups let you manage multiple domains belonging to the same
organisation as a single named entity. For example, `acmecorp.com`,
`acmecorp.co.uk`, and `acme-holdings.com` can all be grouped under
"Acme Corporation".

### Creating a group

In the Targets sidebar, click **📁 New Group** (alongside the
**+ New Target** button). Enter a group name and optional description.

### Adding targets to a group

On each target card in the sidebar, a **Group:** dropdown lets you
assign or reassign that target to any of your groups. Select a group
from the dropdown — the target is assigned immediately. Select
"— Ungrouped —" to remove it from a group.

### What groups show you

In the **Target History Dashboard** (📈 view), groups appear as
expandable cards above ungrouped targets. Each group card shows:

- The **highest risk score** across all member domains (worst-case)
- Combined **new findings count** from the most recent scans
- Whether any members have monitoring active

Expand a group card to see individual member domain rows, each with
their own sparkline and risk score.

### Group monitoring

Inside an expanded group card, click **Enable monitoring** to turn on
monitoring for all member domains at once, with the same interval.
Each domain is then monitored individually — the scheduler picks them
up automatically.

### Deleting a group

The **Delete group** button (inside an expanded group card) removes
the group but does not delete the member targets — they simply become
ungrouped and continue to appear as individual target cards.

---

## 10. Username Enumeration

Username enumeration searches for a given username across 600+ social
media platforms and websites to build a picture of where a person
has a presence.

### Running a standalone search

On any target card in the **Targets** sidebar, click the **🔍** button.
A search modal opens, pre-populated with a username suggestion derived
from the target's domain.

Enter one or more usernames (up to 5 at once, separated by commas or
new lines) and click **Search** or press Ctrl+Enter.

Progress is shown in real time as platforms are checked. When complete:
- Found profiles appear as a grid of clickable links
- Each link opens the discovered profile in a new tab
- Download a CSV of all results with the **Download CSV** button

### Automatic enumeration during scans

When a full scan discovers director or officer names from Companies
House, SEC EDGAR, or OpenCorporates, those names are automatically
used for username enumeration as part of the scan. Results appear as
`social_handle` findings in the job results.

### Limits

- Maximum 5 usernames per batch search
- One search per username per organisation per 24 hours
- Maximum 5 concurrent searches per organisation

---

## 11. Threat Intelligence

The **Threat Intelligence** section has five tabs.

### Threat Actors tab

A searchable database of 174+ threat actors from the MITRE ATT&CK
Enterprise framework. Each actor profile shows:

- ATT&CK ID, aliases, and suspected country of origin
- Known techniques (TTPs) with MITRE ATT&CK links
- Associated malware and tools
- Sector targeting — which industries this group is known to target
- Confidence level based on available evidence

Click any actor to open their full profile. The database is
automatically synchronised with MITRE ATT&CK every Sunday at 02:00
UTC.

### Sector Reports tab

Threat intelligence organised by industry sector. Expand any sector
to see which threat actors are known to target it, with:

- **Confidence badge** — Confirmed (red, real report within 18 months),
  High Confidence (amber, older real report), Low Confidence (blue,
  ATT&CK profile only), or Suspected (grey, minimal evidence)
- **Last reported date** — when the most recent report citing this
  actor in this sector was published
- **Source link** — click to open the original advisory or report

Click any ATT&CK ID or actor name to jump to their full profile.

### IOC Feed tab

A live feed of indicators of compromise (IOCs) gathered from 20+
intelligence sources every 6 hours. Sources include:

- CISA KEV (Known Exploited Vulnerabilities) via NVD API
- CISA CSAF advisories (IT, ICS/OT, and VA categories)
- ThreatFox (abuse.ch) — malware C2 IOCs
- Cisco Talos, Securelist/Kaspersky, Kaspersky ICS CERT
- NCSC UK, FBI IC3, BleepingComputer, The Record, Krebs on Security
- And 10+ additional sources

A **cross-match** badge appears on any IOC that matches a finding in
one of your organisation's scans — a direct link between a live threat
intelligence signal and your specific exposure.

### Quarterly Reports tab

Downloadable threat intelligence reports covering confirmed incidents,
active threat groups, key TTPs, and recommended actions for specific
sectors. See section 12 for full details.

### Status tab

System status for the intelligence pipeline including IOC digest
schedule and last run statistics, MITRE ATT&CK sync status, and email
delivery configuration. Visible to all users; the **Send test email**
button is available to super admins only.

---

## 12. Quarterly Reports

The Quarterly Reports panel shows two types of reports.

### Curated Platform Reports

Reports uploaded by the White Hawk Labs team — human-curated PDFs
covering confirmed incidents, active threat groups, and recommended
actions for specific sectors and quarters. These appear at the top of
the panel with a blue **PLATFORM** badge and are available to all
organisations.

Click **👁 View** to open the report in your browser, or
**📥 Download** to save the PDF.

### AI-Generated Reports

Reports generated on demand by Claude AI, synthesising your platform's
accumulated intelligence for a specific sector and quarter. To
generate one:

1. Select a **Sector** (Finance, Healthcare, Energy, Government, etc.)
2. Select the **Quarter** (Q1–Q4) and **Year**
3. Click **Generate Report**
4. Wait 30–90 seconds
5. The PDF downloads automatically when complete

**What the report contains:**
- Executive Summary
- Confirmed Incidents — sourced from uploaded advisories and incident
  reports (if available for this sector and period)
- Active Threat Groups — actors known to target this sector, clearly
  labelled as either confirmed active or ATT&CK historical profiling
- Key Vulnerabilities and Attack Techniques
- Recommended Actions
- Intelligence Sources — every report and advisory cited, with URLs

**Confidence transparency:** The report always distinguishes between
confirmed intelligence (from uploaded incident reports) and ATT&CK
profile data (historical targeting patterns). If no confirmed incident
reports exist for the chosen sector and period, the report explicitly
says so rather than presenting historical data as current activity.

**Report quality improves with uploaded incident data.** The confirmed
incidents section is only as good as the data uploaded by your
administrator. Ask your admin to upload relevant CISA advisories, NCSC
alerts, and incident reports via the Platform Admin panel.

---

## 13. Exporting Data

### PDF Report

From any completed scan job, click **Export → PDF**. The PDF includes
the risk score, finding summary by category, and all findings with
their metadata and analyst annotations. Suitable for sharing with
management or including in incident reports.

### CSV Export

Click **Export → CSV** to download all findings as a spreadsheet.
Useful for importing into ticketing systems or further analysis in
Excel or similar tools.

### STIX 2.1 Bundle

Click **Export → STIX** to download a STIX 2.1 JSON bundle — a
machine-readable threat intelligence format compatible with SIEMs,
threat intelligence platforms (TIPs), and security orchestration tools
including Splunk, Microsoft Sentinel, IBM QRadar, and MISP.

The bundle includes:
- **Indicator** objects for network and domain findings
- **Vulnerability** objects for CVE findings with NVD external
  references
- **Software** objects for detected technologies
- **Identity** objects for people and organisations discovered
- **Threat-actor / Intrusion-set** objects when ATT&CK attribution
  exists
- **Relationship** objects linking indicators to attributed actors
- Your organisation's identity as the bundle creator (`created_by_ref`
  on all objects)
- Assessment status reflected as STIX labels (`benign` for known
  infrastructure, `malicious-activity` for confirmed true positives)

---

## 14. Account and Team Management

### Accessing settings

Click **Admin** in the navigation. This is your organisation's
settings panel, with tabs for Users, API Keys, and Integrations.

### Inviting team members

Go to **Admin → Users → Invite User**. Enter their email address and
select their role. They will receive an invitation email with a button
to create their account. The invitation link expires after 7 days.

If an invitation expires, use **Resend Invite** on that user's row
to send a fresh link.

### Managing users

The Users panel shows all members with their role, last login date,
and status. Org admins can invite new users, resend invitations, and
send password reset emails to locked-out users.

### API keys

Go to **Admin → API Keys** to create a machine-readable API key for
programmatic access to the platform. Treat API keys like passwords —
do not share them or commit them to source code.

---

## 15. Third-Party Integrations

The **Integrations** tab in the Admin panel lets org admins configure
their own API keys for external services the platform calls on your
behalf. Your keys are encrypted at rest and used only for your
organisation's scans.

If you do not configure an integration key, the platform uses its own
shared key where available, or skips the service if no platform key
is configured.

### Available integrations

| Service | What it enables | Key required |
|---------|----------------|-------------|
| **Have I Been Pwned** | Email breach checking — identifies whether staff email addresses appear in known data breaches | Paid ($3.50/month at haveibeenpwned.com) |
| **AbuseIPDB** | IP reputation checking — community abuse reports for suspicious IPs | Free (1,000 checks/day) |
| **ThreatFox** | Malware C2 IOC enrichment — identifies known malware infrastructure | Free (register at auth.abuse.ch) |
| **Companies House** | UK company director and registration data | Free (developer.company-information.service.gov.uk) |
| **NVD** | CVE vulnerability data — higher rate limit with a key | Free (nvd.nist.gov) |
| **OpenCorporates** | Global company registry — US, EU, and 100+ jurisdictions | Commercial (opencorporates.com) |
| **Anthropic (Claude AI)** | Quarterly report AI generation — use your own key to control costs | Paid (console.anthropic.com) |

### Adding an integration key

1. Go to **Admin → 🔌 Integrations**
2. Find the service you want to configure
3. Click **Add key**
4. Paste your API key and click **Save**
5. Click **Test** to verify the key works before running a scan

The key is stored encrypted and only shown as a masked hint (****last4
characters) after saving. You can update or remove a key at any time.

---

## 16. User Roles and Permissions

| Role | Who it is for | What they can do |
|------|--------------|-----------------|
| **Viewer** | Stakeholders, read-only access | View jobs, findings, reports, threat intelligence. Cannot annotate or submit scans. |
| **Analyst** | Security analysts | Everything a Viewer can do, plus: submit scans, annotate findings, trigger IOC enrichment, manage targets and domain groups, run username searches, delete jobs. |
| **Org Admin** | Team leads, security managers | Everything an Analyst can do, plus: invite users, manage team members, configure integration keys, edit organisation settings. |
| **Super Admin** | White Hawk Labs staff only | Full platform access across all organisations. Not assigned to customer accounts. |

> If you need to perform an action and see an "Access denied" message,
> you do not have the required role. Contact your Org Admin.

---

## 17. Frequently Asked Questions

**How long does a scan take?**
Most scans complete in 2–5 minutes. Scans with many director names
or VIPs (triggering more email, social, and username lookups) may
take up to 10 minutes.

**Can I scan the same target twice?**
Yes. Each scan is a separate job. If you have saved the target, the
second scan's Changes tab will show what is new or resolved since the
first scan.

**Why doesn't the platform find director names automatically?**
Director discovery depends on the registry available for your target.
UK companies: Companies House is queried automatically. US-listed
companies: SEC EDGAR is queried automatically. All other jurisdictions:
either provide director names manually in the scan form, or your
admin can configure an OpenCorporates integration key for broader
global coverage.

**What does the risk score actually measure?**
The score is calculated from every finding's risk weight, summed and
normalised to 0–100. Higher-severity findings (JARM C2 matches,
critical CVEs) contribute more than informational findings (detected
technologies). The score is also adjusted upward when attributed
threat actors are currently active in live intelligence feeds — the
Threat Climate multiplier.

**Why is a finding marked as a False Positive?**
Some findings require context the platform cannot automatically
determine. A cloud storage bucket that belongs to your own
infrastructure is legitimately exposed but intentionally so. Mark
it as **Known Infrastructure** or **Confirmed False Positive** so
it is excluded from the risk score and your team knows not to action
it in future rescans.

**What is a typosquat domain?**
A domain registered to look like yours — for example, if your domain
is `acmecorp.com`, a typosquat might be `acmec0rp.com` (zero instead
of O) or `acme-corp.com`. These are used in phishing campaigns. When
the platform finds one and you confirm it as a True Positive, it
automatically investigates the domain's registration, DNS, and threat
intelligence presence.

**What is JARM?**
JARM is a TLS fingerprinting technique that identifies what software
is running a TLS server based on how it responds to specific TLS
handshakes. Different C2 frameworks (Cobalt Strike, Metasploit,
Sliver) produce distinctive JARM fingerprints. A `jarm_c2_match`
finding means the platform detected infrastructure matching known
malware C2 patterns.

**What is an IOC cross-match?**
When the platform's intelligence feed detects an IOC (IP, domain,
CVE, hash) that also appears in one of your scan results, it sends
a notification. This means a live threat intelligence signal is
directly relevant to your organisation's environment.

**Why does the Sector Reports panel show "Low Confidence" for some actors?**
Confidence levels reflect evidence quality:
- **Confirmed** — confirmed incident report in this sector within
  18 months
- **High Confidence** — a real report exists but is older than 18
  months
- **Low Confidence** — only ATT&CK historical profiling data, no
  confirmed recent incident reports
- **Suspected** — minimal evidence

The platform is transparent about this so analysts know when they
are looking at confirmed intelligence versus historical profiling.

**How do I check if an email address has been breached?**
Open any `harvested_email` or `predicted_email` finding in the
Annotation Panel. If your administrator has configured a Have I Been
Pwned API key (via Admin → Integrations), you will see a
**Check HIBP** button. Click it to run an on-demand breach check.
The result shows which data breaches included that email address and
what data was exposed — passwords exposed are flagged with a red
**PASSWORD** badge.

**What company registries does the platform support?**
Three registries are integrated:
- **UK Companies House** — automatic for UK-registered companies,
  returns directors, PSC data, and filing history
- **SEC EDGAR** — automatic for US-listed companies and international
  companies with SEC filings, returns registration data
- **OpenCorporates** — requires an org API key, covers US state
  registries, EU national registries, and 100+ other jurisdictions,
  returns directors and registration data

**Can I export to my SIEM?**
Yes — use the STIX 2.1 export. STIX is supported by most major SIEM
and TIP platforms. The export includes your organisation as the bundle
creator so your SIEM can attribute the intelligence to the correct
source.

**What happens to my data?**
All scan data is stored in your organisation's isolated workspace.
No data is shared between organisations. The platform is hosted on
Hetzner infrastructure in Europe with Cloudflare for edge security.
Scan reports and quarterly report PDFs are stored in Cloudflare R2
object storage.

**How do I get help?**
Contact the White Hawk Labs team directly. For urgent platform issues,
your Org Admin can use the Platform Admin panel to check platform
status and raise support requests.
