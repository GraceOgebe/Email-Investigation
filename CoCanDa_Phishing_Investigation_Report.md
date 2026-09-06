# CoCanDa Phishing and File Analysis Investigation

## Executive Summary

An Army Major representing CoCanDa received a suspicious email after multiple citizens and the Planetary President's daughter were abducted. The sender claimed to know where the victims were being held and directed the Major to solve an attached puzzle before arranging a payment of one billion CoCanDs.

Analysis of the email headers identified sender-address inconsistencies, a failed SPF check, and delivery through the Emkei fake mail service from `93.99.104.210`. Examination of the attachment revealed misleading file extensions and embedded files. File signatures identified a JPEG image, a PDF document, and an Excel workbook. A Base64-encoded value recovered from the workbook revealed the location: **The Martian Colony, beside the Interplanetary Spaceport**.

The attacker combined technical deception with social engineering. Fear, urgency, pride, curiosity, and responsibility were used alongside public unrest, political pressure, and the abduction of the President's daughter to influence the Major's decisions.

## Findings

| Evidence | Finding |
|---|---|
| Recipient | `themajoronearth@gmail.com` |
| Display name | `Bill` |
| From address | `billjobs@microapple.com` |
| Return-Path | `billjobs@microapple.com` |
| Reply-To address | `negeja3921@pashter.com` |
| Sending service | `emkei.cz` |
| Source IP address | `93.99.104.210` |
| SPF result | Fail |
| Subject | `A Hope to CoCanDa` |
| Message date | 26 January 2021 at 01:41:18 EST |
| Normalized time | 26 January 2021 at 06:41:18 UTC |
| Claimed attachment type | PDF |
| Observed attachment type | ZIP-compatible data identified by `50 4B 03 04` |
| Extracted file 1 | `DaughtersCrown`, identified as JPEG by `FF D8 FF E0` |
| Extracted file 2 | `GoodJobMajor`, identified as PDF by `25 50 44 46` |
| Extracted file 3 | `Money.xlsx`, identified as an OOXML file by `50 4B 03 04` |
| Final decoded location | The Martian Colony, beside the Interplanetary Spaceport |

## Key Red Flags

1. The `From` and `Reply-To` addresses used different domains.
2. The domain `microapple.com` did not authorize `93.99.104.210` to send the message.
3. The SPF authentication check failed.
4. The message passed through `emkei.cz`, a service associated with fake email generation.
5. The attachment was presented as a PDF, while its magic bytes showed ZIP-compatible content.
6. Extracted files lacked extensions, hiding their true formats.
7. The sender demanded a large payment and attempted to direct the recipient through several decoding steps.
8. The message used emotionally charged claims about abducted citizens and the President's daughter.
9. The attacker taunted the Major and challenged the competence of CoCanDa's investigators.

## Investigation Summary

On 26 January 2021 at 06:41:18 UTC, the CoCanDa Army Major received an email titled `A Hope to CoCanDa`. The sender used the display name `Bill` and the address `billjobs@microapple.com`, while replies were directed to `negeja3921@pashter.com`.

Header analysis showed the message originated from `93.99.104.210` through `emkei.cz`. SPF failed because `microapple.com` did not authorize the source IP to send email on its behalf. These findings indicate sender spoofing and reduce confidence in the claimed identity.

The email contained Base64-encoded content. Decoding it in CyberChef produced a message stating that the attacker held the missing CoCanDians and the President's daughter. The attacker demanded one billion CoCanDs in cash, requested a spaceship, and instructed the Major to solve the attached puzzle. The message included the phrase `Don't trust your Eyes`, which hinted that the visible filenames and extensions were unreliable.

The attachment began with the bytes `50 4B 03 04`, a ZIP and Microsoft OOXML signature. After extraction with 7-Zip, three files were recovered: `DaughtersCrown`, `GoodJobMajor`, and `Money.xlsx`.

HxD and the Gary Kessler file-signature reference were used to identify the hidden formats:

- `DaughtersCrown` began with `FF D8 FF E0`, identifying it as a JPEG image. Renaming it with a `.jpeg` extension displayed a crown image.
- `GoodJobMajor` began with `25 50 44 46`, identifying it as a PDF. The document stated that the CoCanDians were safe, referred to `DaughtersCrown` as proof, and directed the Major to `Money.xlsx` for the payment location.
- `Money.xlsx` began with `50 4B 03 04`, which matched Microsoft OOXML content. The workbook stated that the earlier ransom story was a deception and declared the beginning of a war with CoCanDa. It also contained a Base64-encoded string.

The final string was decoded in CyberChef. It revealed: **The Martian Colony, beside the Interplanetary Spaceport**.

## Who, What, When, Where, Why, and How

### Who

- Target: CoCanDa's Army Major on Earth.
- Threatened parties: Abducted CoCanDians and the Planetary President's daughter.
- Sender: An unidentified actor using the name `Bill`.
- Sender infrastructure: `emkei.cz` and source IP `93.99.104.210`.

### What

The attacker sent a spoofed phishing email containing an encoded message and a disguised archive. The archive led the Major through several hidden files and ended with a decoded location. The apparent ransom demand was later presented as a deception connected to a wider conflict with CoCanDa.

### When

The message was dated 26 January 2021 at 01:41:18 EST, equivalent to 06:41:18 UTC. The evidence does not establish whether the activity continued after the message was received.

### Where

- Email destination: the Army Major's Gmail mailbox.
- Apparent source infrastructure: `emkei.cz`, IP `93.99.104.210`.
- Location disclosed by the final decoded clue: The Martian Colony, beside the Interplanetary Spaceport.

### Why

The initial message presented financial extortion as the motive. The workbook later stated that the money request was false and that the attack marked the beginning of a war with CoCanDa. Based on the supplied evidence, coercion, intimidation, and conflict appear more likely than financial gain alone.

### How

The attacker used a spoofed email, failed sender authentication, mismatched reply details, Base64 encoding, misleading file presentation, hidden file extensions, and nested clues. The attack relied on emotional pressure to encourage the Major to open and inspect the attachment.

## Social Engineering Analysis

### Internal Human Characteristics Exploited

| Human characteristic | How the attacker used it |
|---|---|
| Fear | The attacker claimed to control the safety of abducted citizens and the President's daughter. Fear of harm encouraged immediate action. |
| Urgency | The ongoing disappearances and lack of progress created pressure to act before checking the message fully. |
| Pride and ego | The attacker referred to CoCanDa's `best brains` and challenged them to solve the puzzle. This encouraged the Major to prove his competence. |
| Curiosity | Encoded content, disguised files, and puzzle instructions encouraged continued interaction with the attachment. |
| Duty and responsibility | As an Army Major, the recipient had a professional and moral duty to protect citizens and support the President. |
| Hope | The subject `A Hope to CoCanDa` suggested the message contained a possible route to rescuing the victims. |
| Trust in visual cues | The attacker relied on filenames and apparent file types to influence the recipient. The clue `Don't trust your Eyes` confirmed the use of visual deception. |
| Desire for resolution | After days without clues or a ransom demand, the recipient was more likely to treat the first apparent lead as important. |
| Response to taunting | Phrases challenging the Major and CoCanDians were intended to provoke an emotional response and weaken careful judgment. |

### External Influences and Pressures

| External influence | Effect on the target |
|---|---|
| Repeated citizen abductions | Created an ongoing crisis and raised the perceived value of any new information. |
| Abduction of the President's daughter | Added political importance and a personal connection for national leadership. |
| Public riots | Increased pressure on officials and security teams to produce fast results. |
| Pressure from citizens | The demand for the safe return of missing people reduced the time available for careful decision-making. |
| Presidential war room | Created expectations for the Major and investigators to demonstrate progress. |
| Two days without evidence | Increased frustration, uncertainty, and willingness to follow a new lead. |
| Ransom and rescue demand | Forced the recipient to consider financial and operational decisions under pressure. |
| Threat of war | Raised the perceived consequences of delay or failure. |
| Claimed remote location | The reference to a distant location and spaceship introduced logistical pressure and limited response options. |

## Attack Technique

The activity is consistent with **MITRE ATT&CK T1566.001, Phishing: Spearphishing Attachment**. The attacker sent a targeted email containing an attachment designed to make the recipient interact with concealed content. The sender also used spoofing, encoding, and file-type deception to reduce suspicion and delay analysis.

## Tools Used

| Tool | Purpose |
|---|---|
| Windows 10 virtual machine | Isolated analysis environment |
| Notepad++ | Email-source and header review |
| CyberChef | Base64 decoding and byte inspection |
| 7-Zip | Archive extraction |
| HxD | Hexadecimal inspection and magic-byte identification |
| Gary Kessler File Signatures | File-signature reference |
| ExifTool | Metadata inspection where required |
| Blue Team Labs Online | Investigation scenario and challenge environment |

## Recommendations

1. Quarantine the message and preserve the original `.eml` file, attachments, headers, and hashes for further investigation.
2. Search mail logs for messages from `billjobs@microapple.com`, `negeja3921@pashter.com`, `emkei.cz`, and `93.99.104.210`.
3. Block confirmed malicious sender addresses, domains, and source infrastructure after checking for business impact.
4. Review whether any recipient opened, extracted, renamed, or executed content from the attachment.
5. Isolate affected endpoints if attachment execution or suspicious child processes are identified.
6. Run endpoint searches for the extracted filenames and their calculated hashes.
7. Enforce SPF, DKIM, and DMARC controls and quarantine messages that fail authentication checks.
8. Configure email security controls to detect misleading extensions, extensionless files, nested archives, and encoded payloads.
9. Train staff to verify urgent messages through a separate trusted channel, especially when the sender requests money, secrecy, or attachment interaction.
10. Include emotional manipulation in phishing exercises. Focus on fear, urgency, authority, pride, curiosity, and responsibility.
11. Require a second-person review before staff act on ransom, payment, rescue, or crisis-related instructions.
12. Record all indicators and findings in the incident-management system for threat hunting and future correlation.

## Investigation Limitations

- No endpoint telemetry was supplied to confirm whether the attachment was executed.
- No malware sample or process evidence was identified in the supplied screenshots.
- The owner of `93.99.104.210` was not attributed from the available evidence.
- The final location came from attacker-controlled content and should be treated as unverified intelligence until corroborated.
- File hashes were not supplied and should be calculated before IOC searches or blocking decisions.

## Conclusion

The investigation identified a targeted phishing message using sender spoofing, Base64 encoding, deceptive file types, and nested clues. The technical evidence exposed the message's true source and the formats of the hidden files. The social-engineering element relied on fear, urgency, pride, curiosity, duty, and hope. External pressure from public unrest, repeated abductions, political expectations, and the disappearance of the President's daughter increased the likelihood of rushed action.

Challenge completion: [Blue Team Labs Online achievement](https://blueteamlabs.online/achievement/share/challenge/175068/10)
