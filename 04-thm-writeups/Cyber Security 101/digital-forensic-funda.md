# Digital Forensics Fundamentals
## Intro
* **Overview:** Introduces digital forensics as the branch of forensics focused on investigating and solving cybercrimes by thoroughly analyzing digital devices for legal evidence.
* **Case Scenario:** Illustrates how law enforcement hands seized digital devices (laptops, mobile phones, hard drives, and USBs) from a criminal raid over to a specialized forensics team.
* **Types of Evidence Recovered:** Highlights examples of digital evidence that can be uncovered, such as digital maps, planning documents, security bypass notes, media files, and chat logs.
* **Learning Objectives:** Outlines the core topics covered in the room, including the phases and types of digital forensics, evidence acquisition procedures, Windows forensics, and a practical case study.

## Digital Forensics Methodology
* **Overview:** Details the standard four-phase digital forensics framework defined by the National Institute of Standards and Technology (NIST), outlining how cases are systematically handled from evidence gathering to final reporting.

![digital-Forensics](../images/digital-forensics-1.png)
* **The Four Phases of Digital Forensics:**
    * **Collection:** Identifying and seizing digital evidence sources (computers, laptops, digital cameras, USBs) at a crime scene while ensuring original data is untampered and meticulously documented.
    * **Examination:** Filtering and extracting specific data of interest from overwhelming volumes of collected raw data (such as isolating media files from a precise date or extracting a single user's records).
    * **Analysis:** Correlating multiple pieces of evidence chronologically to draw conclusions, reconstruct timelines, and map out activities relevant to the case.
    * **Reporting:** Compiling a detailed final document outlining the investigation's methodology, findings, and recommendations, complete with executive summaries tailored for law enforcement and management.

![digital-Forensics](../images/digital-forensics-2.png)
* **Common Types of Digital Forensics:**
    * **Computer Forensics:** Investigating compromised or seized computers and standard digital hardware.
    * **Mobile Forensics:** Extracting mobile device evidence such as text messages, call logs, and GPS location history.
    * **Network Forensics:** Analyzing network traffic logs to uncover unauthorized activities across a broader network infrastructure.
    * **Database Forensics:** Investigating backend databases following security intrusions, data modifications, or exfiltration.
    * **Cloud Forensics:** Investigating data and activity stored across cloud infrastructures.
    * **Email Forensics:** Analyzing email communications to identify phishing campaigns or fraudulent activities.

## Evidence Acquisition
* **Overview:** Focuses on the secure collection and preservation of digital evidence from a crime scene without altering or tampering with original data sources.
* **Chain of Custody:** A formal, mandatory document used to track the lifecycle of every collected piece of evidence. It details the item's description, the names of the collectors, timestamps, storage locations, and a complete access log to prove integrity and ensure admissibility in a court of law.
* **Write Blockers:** Essential hardware or software tools used during data collection to prevent any accidental modification, writing, or alteration of data on suspect storage drives.
* **Secure Handling & Transport:** Devices (such as smartphones) are isolated in secure containers or Faraday bags to block network connectivity and prevent remote data wiping before being transported to the forensics laboratory.
* **Lab Processing:** Once at the lab, investigators retrieve items from secure storage to create precise forensic duplicates (images), ensuring that all analysis is performed on copies rather than original evidence.

## Windows Forensics
* **Overview:** Focuses on the acquisition and analysis of Windows operating systems, detailing the differences between non-volatile storage and volatile system memory.
* **Types of Forensic Images:**
    * **Disk Image:** Captures non-volatile data stored on physical drives (HDDs, SSDs) such as media files, documents, and browsing history, which persist even after system reboots.
    * **Memory Image:** Captures volatile data stored inside the system's RAM, including open files, running processes, and active network connections. Because RAM is lost upon shutdown or restart, memory acquisition is always prioritized.
* **Popular Windows Forensics Tools:**
    * **FTK Imager:** A widely used tool with a user-friendly graphical interface for acquiring and analyzing disk images.
    * **Autopsy:** An open-source digital forensics platform used to analyze imported disk images, offering features like keyword searches, deleted file recovery, and metadata inspection.
    * **DumpIt:** A command-line utility used to quickly capture memory images from Windows systems in various formats.
    * **Volatility:** A powerful open-source framework for analyzing memory images using specialized plugins across Windows, Linux, macOS, and Android.

## Practical Example of Digital Forensics
* **Overview:** Provides a hands-on practical case study where an investigator must solve a kidnapping scenario (saving a cat named Gado) by inspecting file metadata and image EXIF data.
* **Document Metadata Analysis (`pdfinfo`):**
    * Examines documents like the ransom letter (`ransom-letter.pdf`) using command-line tools like `pdfinfo` to extract embedded document properties.
    * Reveals hidden metadata such as the author, creator application (e.g., Microsoft Word for Office 365), and exact creation/modification timestamps.
* **Image EXIF Data Analysis (`exiftool`):**
    * Inspects embedded metadata within attached digital photographs using tools like `exiftool`.
    * Extracts hardware details, such as the specific smartphone or camera model used to capture the image.
    * Uncovers embedded GPS coordinates (latitude and longitude) that can be queried on map services like Google Maps or Microsoft Bing Maps to pinpoint the exact street where the photo was taken.