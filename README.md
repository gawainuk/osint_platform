# White Hawk Labs OSINT Platform
## User Guide

---

## Table of Contents

1. [What is the Platform?](#1-what-is-the-platform)
2. [Getting Access](#2-getting-access)
3. [Your Dashboard at a Glance](#3-your-dashboard-at-a-glance)
4. [Running Your First Scan](#4-running-your-first-scan)
5. [Understanding Your Results](#5-understanding-your-results)
6. [Working with Findings](#6-working-with-findings)
7. [Annotating and Triaging Findings](#7-annotating-and-triaging-findings)
8. [Targets and Monitoring](#9-targets-and-monitoring)
9. [Username Enumeration](#10-username-enumeration)
10. [Threat Intelligence](#11-threat-intelligence)
11. [Quarterly Reports](#12-quarterly-reports)
12. [Exporting Data](#13-exporting-data)
13. [Account and Team Management](#14-account-and-team-management)
14. [User Roles and Permissions](#15-user-roles-and-permissions)
15. [Frequently Asked Questions](#16-frequently-asked-questions)

---

## 1. What is the Platform?

White Hawk Labs OSINT Platform is a professional threat intelligence and
open-source intelligence (OSINT) tool designed for security teams,
analysts, and investigators.

You provide a target — a company domain, organisation name, or person
of interest — and the platform automatically gathers intelligence from
hundreds of public sources in parallel:

- **Infrastructure** — open ports, exposed services, cloud storage
  buckets, TLS certificates, JARM fingerprints
- **Domain threats** — typosquatting domains designed to impersonate
  your brand, IDN homograph attacks, newly registered lookalike domains
- **Technology exposure** — what software is running on the target's
  web presence and whether it has known CVEs
- **People** — company directors, significant persons, LinkedIn
  profiles, GitHub employees
- **Email** — harvested email addresses, predicted email patterns for
  known directors, breach exposure via Have I Been Pwned
- **Reputation** — VirusTotal checks, Spamhaus listings, AbuseIPDB
  scores, ThreatFox C2 intelligence
- **Threat actor attribution** — whether findings match known threat
  actor tactics, techniques, and infrastructure

All findings are scored, risk-weighted, and presented in a structured
report that an analyst can review, annotate, and export.

---

## 2. Getting Access

### Accepting your invitation

Your administrator will send you an invitation email from
`noreply@whitehawklabs.com`. The email contains an **Accept Invitation**
button and a backup URL.

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
| **🔍 Jobs** | All scan jobs — running, complete, and historical |
| **🎯 Targets** | Saved targets with monitoring and history |
| **🧠 Threat Intelligence** | IOC feed, threat actors, sector reports |
| **⚙ Admin** | Organisation settings, users, API keys |
| **🛡 Platform Admin** | Super admin only — all organisations |

The bell icon (🔔) in the top right shows your notifications — alerts
from monitoring rescans, IOC cross-matches, and digest activity.

---

## 4. Running Your First Scan

### Step 1 — Go to Jobs

Click **🔍 Jobs** in the navigation. Click the **+ New Scan** button.

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
> can automatically retrieve director names from Companies House.
> Just provide the domain and organisation name — director discovery
> runs automatically as part of the scan.

### Step 3 — Submit and wait

Click **Run Scan**. The platform will:

1. Accept your job and show it as **Pending**
2. Dispatch parallel intelligence modules (typically 6–8 modules running
   simultaneously)
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
A multiplier applied when threat actors who have recently appeared in
live intelligence feeds are attributed to findings in this scan. A
lightning bolt (⚡) on a finding means its risk score has been elevated
because the attributed threat actor is currently active in real-world
attacks.

**Finding summary**
A breakdown of findings by category — Infrastructure, Domain Threats,
Technology, People, Email, Reputation — with counts and risk
contribution per category.

**Risk score timeline**
If this target has been scanned before, a sparkline shows how the risk
score has changed across scans.

### The Findings tab

All individual findings are listed here, sorted by risk weight
(highest first by default). Each finding shows:

- **Type** — what kind of finding it is (e.g. `typosquat_domain`,
  `technology_cve_exposure`, `jarm_c2_match`)
- **Value** — the discovered data (a domain, IP, email, CVE ID, etc.)
- **Confidence** — how certain the platform is about this finding
  (0–100%)
- **Risk weight** — contribution to the overall risk score
- **Status** — whether an analyst has reviewed it

### The Changes tab

If this is not the first scan of this target, the Changes tab shows
what is **new**, what has **disappeared**, and what has **changed**
compared to the previous scan. This is the most important tab for
monitoring workflows — it tells you exactly what changed in the target's
exposure profile since you last looked.

### The Graph tab

An interactive visualisation of all findings grouped by category.
Nodes represent finding types; edges show relationships between them.
Click any node to highlight related findings.

---

## 6. Working with Findings

### Filtering findings

Above the findings list, use the filter bar to narrow results:

- **Category** — filter by Infrastructure, Domain Threats, Technology,
  People, Email, or Reputation
- **Status** — show only unreviewed, under review, or reviewed findings
- **Priority** — filter by analyst priority (Critical, High, Medium,
  Low)
- **Search** — search by finding value, e.g. type a domain or IP

### Opening a finding

Click any finding row to open the **Annotation Panel** on the right.
This shows:

- The full finding value and metadata
- Confidence score and risk weight
- Any IOC enrichment results (ThreatFox, AbuseIPDB)
- ATT&CK attribution badges if threat actors were identified
- For email findings — a **Check HIBP** button to check breach exposure
- Analyst annotation fields (see section 7)
- Full annotation history — every change ever made to this finding,
  by whom, and when

### IOC Enrichment

For findings that represent potential indicators of compromise (IP
addresses matching C2 infrastructure, suspicious domains), you will see
an **Enrich IOC** button. Clicking this queries:

- **ThreatFox** — checks whether this IOC is a known malware C2
  indicator, including the malware family and confidence score
- **AbuseIPDB** — for IP addresses, checks the abuse confidence
  percentage and report count from the community database

Enrichment results are cached for 24 hours. If you enrich an IOC today
and open the finding tomorrow, the cached result is shown with a
timestamp.

### JARM C2 matches

If the platform detects that a service's TLS fingerprint (JARM hash)
matches known command-and-control infrastructure, a `jarm_c2_match`
finding appears with a red badge. These are automatically enriched
and ATT&CK-attributed where possible. A JARM C2 match is one of the
highest-confidence finding types the platform produces — it indicates
the target is communicating with or running infrastructure that matches
known malware C2 patterns.

### Typosquat deep dive

When you confirm a `typosquat_domain` finding as a true positive
(see section 7), the platform automatically runs a deep-dive
investigation on that domain:

- WHOIS registration data
- DNS resolution (does it resolve? where does it point?)
- ThreatFox and AbuseIPDB IOC checks
- Technology fingerprinting of the typosquat domain itself

Results appear in the finding's annotation panel under **Typosquat
Intelligence** within 30–60 seconds.

---

## 7. Annotating and Triaging Findings

Annotation is how analysts record their assessment of each finding.
All annotation changes are permanently recorded in the audit history —
they cannot be deleted or altered.

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
| **Known Infrastructure** | This is our own infrastructure or a known-good asset |

> **Important:** Setting a finding to **Confirmed True Positive**
> triggers automatic follow-up actions. For typosquat domains, this
> launches the deep-dive investigation. The finding is also reflected
> correctly in any STIX exports.

### Analyst priority

Your assessment of how urgently this needs addressing:

| Priority | Meaning |
|----------|---------|
| **Critical** | Immediate action required |
| **High** | Address within 24 hours |
| **Medium** | Address within the week |
| **Low** | Monitor — no immediate action |
| **Accepted** | Risk accepted — will not be addressed |

### Action tags

36 pre-defined tags organised into 8 categories let you label findings
with specific actions or observations. Examples:

- `block_ip`, `block_domain`, `sinkhole_domain`
- `notify_registrar`, `submit_takedown`
- `patch_immediately`, `update_software`
- `monitor_closely`, `watchlist_added`
- `ioc_found_threatfox`, `tor_exit_node`, `malware_infrastructure`

Some tags are applied automatically based on finding type and
enrichment results.

### Analyst notes

A free-text field for any observations, investigation notes, or
context you want to record. Notes are included in the annotation
history.

---

## 8. Targets and Monitoring

### What is a Target?

A Target is a saved scan profile for an organisation you want to
track over time. Instead of manually submitting a new scan job each
time, you save the target once and the platform rescans it
automatically on your chosen schedule.

### Creating a Target

From the **🎯 Targets** tab, click **+ New Target**. Fill in the same
fields as a scan job (domain, organisation name, optional directors
and VIPs). The target is saved and you can scan it on demand or enable
monitoring.

### Enabling monitoring

On any target card, toggle **Monitoring**. You will be asked to choose
a scan interval:

| Interval | Availability |
|----------|-------------|
| Daily | Professional and Enterprise plans |
| Weekly | All plans |
| Fortnightly | All plans |
| Monthly | All plans |

The schedule block on the target card shows:
- Next scheduled scan date
- Last scan date
- Last risk score (colour-coded)

### Monitoring notifications

When an automated rescan completes, you receive a notification if
anything changed — new findings appeared or previous findings
disappeared. The notification links directly to the **Changes** tab
of that scan so you can see exactly what shifted.

> Rescans with no changes produce no notification — you are only
> interrupted when something actually changed.

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

## 9. Username Enumeration

Username enumeration searches for a given username across 600+ social
media platforms and websites to identify where a person has a presence.

### Running a username search

On any target card in the **🎯 Targets** tab, click the **🔍** button.
A search modal opens pre-populated with a suggested username derived
from the target's domain.

Enter one or more usernames (up to 5 at once, separated by commas or
new lines) and click **Search**.

Progress is shown in real time as sites are checked. When complete:
- Found profiles appear as a grid of clickable links
- Each link opens the discovered profile in a new tab
- Download a CSV of all results with the **📥 CSV** button

### Limitations

- Maximum 5 usernames per batch search
- One search per username per organisation per 24 hours (deduplication)
- Maximum 5 concurrent searches per organisation

Username searches also run automatically as part of a full scan when
director or VIP names are provided — results appear as `social_handle`
findings in the job results.

---

## 10. Threat Intelligence

The **🧠 Threat Intelligence** section has five tabs.

### Threat Actors tab

A searchable database of 174+ threat actors from the MITRE ATT&CK
Enterprise framework. Each actor profile shows:

- ATT&CK ID, aliases, and suspected country of origin
- Known techniques (TTPs) with MITRE ATT&CK links
- Associated malware and tools
- Sector targeting — which industries this group is known to target
- Confidence level — whether targeting is confirmed by recent reports
  or inferred from ATT&CK historical data

Click any actor to open their full profile. This database is
automatically synchronised with MITRE ATT&CK every Sunday.

### Sector Reports tab

Threat intelligence organised by industry sector. Expand any sector
to see which threat actors are known to target it, with:

- **Confidence badge** — Confirmed (red), High Confidence (amber),
  Low Confidence (blue), or Suspected (grey)
- **Last reported date** — when the most recent report citing this
  actor in this sector was published
- **Source link** — click to open the original advisory or report

Click any ATT&CK ID or actor name to jump to their full profile.

### IOC Feed tab

A live feed of indicators of compromise (IOCs) gathered from 20+
intelligence sources every 6 hours. Sources include CISA KEV, CISA
CSAF advisories, ThreatFox, Cisco Talos, Securelist, NCSC UK, FBI
IC3, Kaspersky ICS CERT, and others.

The feed shows IOC type, value, attributed threat actor, and source.
A **cross-match** badge appears on any IOC that matches a finding in
one of your organisation's scans — this is a direct link between a
live threat intelligence signal and your specific exposure.

### Quarterly Reports tab

Downloadable threat intelligence reports. This tab shows two types:

**Curated Intelligence Reports** (marked with a blue PLATFORM badge)
— Human-curated PDF reports uploaded by the White Hawk Labs team,
covering confirmed incidents, active threat groups, and recommended
actions for specific sectors and quarters. These are available to all
organisations on the platform.

**AI-Generated Reports** — Reports generated on demand by Claude AI,
synthesising your platform's accumulated intelligence data for a
specific sector and quarter. To generate one:

1. Select a sector (Finance, Healthcare, Energy, Government, etc.)
2. Select the quarter and year
3. Click **📋 Generate Report**
4. Wait 30–90 seconds while the report is compiled and synthesised
5. The PDF downloads automatically when complete

AI-generated reports distinguish clearly between **confirmed
intelligence** (from uploaded incident reports) and **ATT&CK profile
data** (historical targeting patterns). The report includes an
Executive Summary, Confirmed Incidents section, Active Threat Groups,
Key Vulnerabilities, Recommended Actions, and full source citations.

### Status tab *(super admin only)*

System status for the intelligence pipeline — IOC digest schedule,
last run statistics, MITRE ATT&CK sync status, and email delivery
status.

---

## 11. Exporting Data

### PDF Report

From any completed scan job, click **Export → PDF**. The PDF report
includes the risk score, finding summary by category, and all findings
with their metadata. Suitable for sharing with management or including
in incident reports.

### CSV Export

Click **Export → CSV** to download all findings as a spreadsheet.
Useful for importing into ticketing systems or further analysis.

### STIX 2.1 Bundle

Click **Export → STIX** to download a STIX 2.1 JSON bundle. This is
a machine-readable threat intelligence format compatible with SIEMs,
threat intelligence platforms (TIPs), and security orchestration tools.

The STIX bundle includes:
- Indicator objects for each finding
- Vulnerability objects for CVE findings with NVD references
- Software objects for detected technologies
- Identity objects for people and organisations discovered
- Threat actor / intrusion set objects when ATT&CK attribution exists
- Relationship objects linking indicators to attributed actors
- Your organisation's identity as the bundle creator

---

## 12. Account and Team Management

### Accessing settings

Click **⚙ Admin** in the navigation. This is your organisation's
settings panel.

### Inviting team members

Go to **⚙ Admin → Users → Invite User**. Enter their email address
and select their role (see section 14 for role descriptions). They
will receive an invitation email with a link to create their account.

If an invitation expires before being accepted, use **Resend Invite**
on that user's row.

### Managing users

The Users panel shows all members of your organisation with their role,
last login date, and status. Org admins can:

- Invite new users
- Resend invitations
- Send password reset emails to users who are locked out

### API keys

Go to **⚙ Admin → API Keys** to create a machine-readable API key for
your organisation. API keys allow programmatic access to the platform
for integration with other tools. Treat API keys like passwords — do
not share them or commit them to source code.

---

## 13. User Roles and Permissions

| Role | Who it is for | What they can do |
|------|--------------|-----------------|
| **Viewer** | Stakeholders, read-only access | View jobs, findings, reports, threat intelligence. Cannot annotate or submit scans. |
| **Analyst** | Security analysts | Everything a Viewer can do, plus: submit scans, annotate findings, trigger IOC enrichment, delete completed jobs. |
| **Org Admin** | Team leads, security managers | Everything an Analyst can do, plus: invite users, manage team members, edit organisation settings. |
| **Super Admin** | White Hawk Labs staff only | Full platform access across all organisations. Not assigned to customer accounts. |

> If you need to perform an action and see an "Access denied" message,
> you do not have the required role. Contact your Org Admin to request
> a role change.

---

## 14. Frequently Asked Questions

**How long does a scan take?**
Most scans complete in 2–5 minutes. Scans with many director names
(triggering more email and social lookups) may take up to 10 minutes.

**Can I scan the same target twice?**
Yes. Each scan is a separate job. If you have saved the target, the
second scan's results will appear in the Changes tab showing what
is new or resolved since the first scan.

**What does the risk score actually measure?**
The score is calculated from every finding's risk weight, summed and
normalised to 0–100. Higher-severity findings (like JARM C2 matches
or critical CVEs) contribute more than informational findings (like
detected technologies). The score is also adjusted upward when
attributed threat actors are currently active in live intelligence
feeds.

**Why is a finding marked as a False Positive?**
Some findings require context that the platform cannot automatically
determine. For example, a cloud storage bucket might belong to your
own organisation's infrastructure — the platform flags it as exposed,
but you know it is intentional. Mark it as **Known Infrastructure**
or **Confirmed False Positive** so it is not counted against the risk
score in future and your team knows not to action it again.

**What is a typosquat domain?**
A domain registered to look like yours — for example, if your domain
is `acmecorp.com`, a typosquat might be `acmec0rp.com` (zero instead
of O) or `acme-corp.com`. These are used in phishing campaigns.
When the platform finds one, confirm it as a True Positive and the
platform will automatically investigate its registration, DNS
configuration, and whether it appears in threat intelligence feeds.

**What is JARM?**
JARM is a TLS fingerprinting technique that identifies what software
is running a TLS server based on how it responds to specific TLS
handshakes. Different C2 frameworks (Cobalt Strike, Metasploit,
Sliver, etc.) produce distinctive JARM fingerprints. A `jarm_c2_match`
finding means a service the platform discovered produces a JARM
fingerprint matching known malware infrastructure.

**What is an IOC cross-match?**
When the platform's intelligence feed detects an IOC (IP address,
domain, CVE, hash) that also appears in one of your scan results,
it sends a notification. This means a piece of threat intelligence
published today is directly relevant to something found in your
organisation's environment.

**Why does the Sector Reports panel show "Low Confidence" for some actors?**
Confidence levels reflect the quality of available evidence:
- **Confirmed** — the actor has a confirmed, recent incident report
  in this sector
- **High Confidence** — a real report exists but it is more than
  18 months old
- **Low Confidence** — only MITRE ATT&CK historical profiling data
  exists, with no confirmed recent incident reports
- **Suspected** — minimal evidence, ATT&CK profile has limited detail

The platform is transparent about this distinction so analysts know
when they are looking at confirmed intelligence versus historical
profiling.

**How do I get Have I Been Pwned results?**
HIBP breach checking requires an API key that your administrator must
configure. If breach checking is active, you will see a **Check HIBP**
button when you open an email finding (harvested email or predicted
email) in the annotation panel. Email breach checks also run
automatically during full scans when the API key is configured.

**Can I export to my SIEM?**
Yes — use the STIX 2.1 export. STIX is supported by most major SIEM
and TIP platforms including Splunk, Microsoft Sentinel, IBM QRadar,
and MISP. The export includes your organisation as the bundle creator
so your SIEM can attribute the intelligence to the correct source.

**What happens to my data?**
All scan data is stored in your organisation's isolated workspace.
No data is shared between organisations. The platform is hosted on
Hetzner infrastructure in Europe with Cloudflare for edge security.
Scan reports are stored in Cloudflare R2 object storage.

**How do I get help?**
Contact the White Hawk Labs team directly. For urgent platform issues,
your Org Admin can raise a support request.

---

*White Hawk Labs OSINT Platform — User Guide*
*For platform administrators, see the separate Admin Guide.*
