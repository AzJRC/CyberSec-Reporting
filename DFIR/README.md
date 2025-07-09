# Incident Response and Digital Forensics (DFIR) Reporting

This documents presents DFIR reporting suggestions based on widely accepted standards ([NIST SP 800-86](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-86.pdf)).

## Typical Digital Forensics Report Structure

| **#**| **Section** | **Description** |
|---|---|---|
| **1** | **Cover Page** | Title, client/lab name, analyst(s), date, case reference. |
| **2** | **Executive Summary** | Short non-technical summary of findings, relevance, conclusions. |
| **3** | **Scope & Objectives** | Defines scope, goals, what was (and wasn’t) analyzed. |
| **4** | **Methodology & Tools** | Procedures followed, software (*Autopsy, FTK, etc*), chain of custody. |
| **5** | **Detailed Findings** | Detailed technical results — organized by artifact category (*users, hashes, network, bookmarks, suspicious files, etc*). |
| **6** | **Analysis & Interpretation** | Explanation of the significance of findings — what they indicate. |
| **7** | **Conclusion & Recommendations** | Final assessment, next steps (*e.g., further acquisition, malware analysis*). |
| **8** | **Appendices** | Hash lists, command outputs, logs, or supporting screenshots. |

## Best Practices for DFIR Reporting

### Structure & style

The document must be clear, neutral, adn factual. Avoid slang or informal phrases common in CTF WriteUps. Start general, then specific: always explain why a piece of data is important. Repeat important values (*hashes, IPs*) in appendix tables for clarity.

### Level of Detail of the Report

Knowing the audience that will read the report is important. Law enforcement readers might require highly detailed reports, while senior management may only need a high-level overview of what happen to take a quick decision. The following list presents plausible target audience profiles:

- **Senior Management**:
Executives and decision-makers who need concise, strategic information to assess business impact and approve resources or policy changes. They are generally interested in summaries, risks, and recommendations rather than technical specifics.
- **Technical Staff**:
System administrators, security engineers, or IT teams who need actionable technical details to remediate issues, apply patches, or reconfigure systems. They require enough depth to reproduce findings and implement countermeasures.
- **Incident Review Teams**:
Internal or external groups (e.g., cybersecurity consultants, audit teams) who conduct post-incident reviews to understand causes, improve controls, or ensure compliance. They look for detailed timelines, correlation of artifacts, and root cause analysis.
- **Legal Counsel**:
Corporate or external attorneys evaluating legal exposure, contractual obligations, or preparing for litigation. They focus on chain of custody, alternative explanations, and clarity of evidence to support or defend legal actions.
- **Law Enforcement**:
Investigators or prosecutors who may use the report in criminal proceedings. They require highly detailed, reproducible documentation including complete artifacts, validated hashes, and procedural transparency to meet evidentiary standards.

The following table can help you decide what to include and what not based on the target audience:

| **Content** | **Detail Level** | **Requirement** | **Audience** | **Notes** | **Example** |
|---|---|---|---|---|---|
| **Indicators of Compromise (IoCs)** | Low | Describe affected systems and artifacts | Senior Management | Provide a high-level overview linking IoCs to key findings. | “Several user accounts were compromised via phishing.” |
|  | Medium | List IoCs with hashes and paths | Technical Staff, Legal Counsel | Include an appendix mapping files, hashes, and systems affected. | Table listing suspicious executables & their hashes. |
|  | High | Full artifacts + hash verification | Law Enforcement, Expert Witness | Provide actual files, hashes, and documented verification procedures. | Disk images with SHA-256 hashes and `sha256sum` instructions. |
| **Statistics & Graphs** | Low | Simplified visuals to support decisions | Senior Management | Use clear diagrams with captions explaining the impact or trend. | Pie chart of user login failures by month. |
|  | Medium | Detailed tables & descriptive analysis | Technical Staff | Include tables showing packet counts, login attempts, etc. | Table of network port usage over 30 days. |
|  | High | Raw data & methodology | Law Enforcement, Incident Review | Explain data sources, collection methods, sampling intervals. | Raw NetFlow data with a detailed capture methodology. |
| **Timelines** | Low | Basic incident progression overview | Senior Management | Timeline with key milestones for situational awareness. | “Day 1: Breach detected; Day 3: Containment complete.” |
|  | Medium | Detailed event chronology | Technical Staff | Include timestamps of log entries, file modifications, user activity. | Table correlating syslog events & file writes. |
|  | High | Exact time offsets & clock references | Law Enforcement | Detail system clock sources and any time skew issues. | Description of NTP drift on suspect machine. |
| **Alternative Explanations** | Medium | List plausible alternative scenarios | Technical Staff, Legal Counsel | Summarize competing hypotheses with a short rationale. | “Could be malware activity or insider exfiltration.” |
|  | High | Detailed exploration & supporting data | Law Enforcement | Methodically prove or disprove each hypothesis with supporting artifacts. | Directory listings showing no external malware present. |
| **Recommendations & Actionable Info** | Low | Strategic mitigation suggestions | Senior Management | Focus on what decisions or investments are required. | “Implement MFA across critical systems.” |
|  | Medium | Operational steps & quick wins | IT Operations | Include prioritized patch lists or user access reviews. | Table of vulnerable systems needing updates. |
|  | High | Detailed technical playbooks | Technical Response Teams | Provide scripts, firewall rules, forensic preservation steps. | `iptables` commands for immediate blocking. |

- For high-detail audiences (*e.g., law enforcement*), always ensure every finding can be independently verified using provided hashes, tool logs, and methodology steps.
- The table above is derived from principles outlined in [NIST SP 800-86](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-86.pdf) (*Guide to Integrating Forensic Techniques into Incident Response*), which highlights the importance of tailoring reporting to the intended audience, balancing brevity for executives with detailed evidence trails for legal proceedings.

### Reproducibility

- Document versions of tools used.
- Include hashes of evidence files.
- Document any filters or exclusions.

### References & attribution

For academic or formal work, cite any resource and tool documentation (*Autopsy User Guide, Sleuth Kit docs, etc*) used.

### Clear visuals

- Screenshots of key findings, with captions explaining relevance.
- Tables for multiple data points (*e.g., listing all user accounts or hacking tools*).