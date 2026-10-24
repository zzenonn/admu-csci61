# Lab 08: The Sleuth Kit and Autopsy

## Objective
Take a seized disk image from untouched evidence to written findings. You will prove the image is unchanged, walk its layers with The Sleuth Kit, analyse it in Autopsy, and write a short findings memo.

## The Case
Halcyon Motors suspects an engineer, Rico Valdez, of leaking the design of its new gearbox (project KESTREL) to a competitor, Vantaro. Security seized his company USB drive on 15 September 2026 and made a raw image of it. You are the examiner.

Answer three questions:
1. Was the KESTREL design on this drive?
2. Is there evidence it left the company? How?
3. When did it happen?

## Prerequisites
- Your Kali Linux VM from earlier labs (8 GB RAM, 20 GB free disk recommended)
- The evidence image: [`lab08/rvaldez_usb.dd.gz`](lab08/rvaldez_usb.dd.gz)
- About 3 hours

## Rules for This Lab
- Work on the image only. Never edit it.
- Record every hash you compute.
- Every finding in your memo must point to something another examiner can check: a file, an entry number, a hash, or a timestamp.

---

## Part 0: Setup (do this before the lab)

### Kali on x86-64 (Windows PCs, Intel Macs)
Install Autopsy from its official snap:

```bash
sudo apt update
sudo apt install -y snapd sleuthkit
sudo systemctl enable --now snapd.socket snapd.service
sudo systemctl enable --now apparmor snapd.apparmor
sudo snap wait system seed.loaded
sudo snap install autopsy
```

Log out and back in, then start Autopsy:

```bash
autopsy
```

If `autopsy` is not found, run `/snap/bin/autopsy`.

### Apple-silicon Macs (M1 and later)
The Autopsy snap is x86-64 only. Split the work:

- **Parts 1, 2 and 4:** in your Kali ARM VM. Install the command-line tools:
  ```bash
  sudo apt update
  sudo apt install -y sleuthkit
  ```
- **Part 3:** in Autopsy for macOS, from the community Homebrew tap `markmckinnon/sleuthkit`. In Terminal on the Mac:
  ```bash
  curl -fsSLO https://raw.githubusercontent.com/markmckinnon/homebrew-sleuthkit/main/install_macos_autopsy_aarch64.sh
  bash install_macos_autopsy_aarch64.sh
  ```
  Then open **Autopsy** from Applications.

> The macOS install has not been tested for this course yet. If it fails, pair with a classmate on x86-64 for Part 3.

### First Start
Autopsy may ask about the Central Repository on first start. Click **OK** to accept the default.

---

## Part 1: Verify the Evidence

### Step 1: Get the Image
```bash
mkdir -p ~/lab08 && cd ~/lab08
cp ~/Downloads/rvaldez_usb.dd.gz .
gunzip -k rvaldez_usb.dd.gz
ls -l
```

### Step 2: Hash It
```bash
sha256sum rvaldez_usb.dd
```

Compare the result with the custody form below. If it does not match, stop and download it again.

### Chain of Custody Form

| # | Date and time | Action | By | SHA-256 |
|---|---|---|---|---|
| 1 | 2026-09-15 09:40 | USB drive seized from desk 4F-12 | J. Ramos, Security | – |
| 2 | 2026-09-15 10:15 | Raw image made through a write blocker | J. Ramos, Security | `563cea916390f37cd5549c4816c1be0a7de0282dcc0e66cfb3d61c83075cdf6b` |
| 3 | | Image received and verified | *you* | |
| 4 | | Image verified after analysis | *you* | |

Fill in row 3 now. You fill in row 4 at the end.

---

## Part 2: Walk the Layers

A disk has layers: **partition table → file system → files**. Each Sleuth Kit command reads one layer.

### Step 1: Partition Table
```bash
mmls rvaldez_usb.dd
```

Note the **Start** sector of each partition. You need it as the `-o` offset in every command below.

### Step 2: File System
```bash
fsstat -o 2048 rvaldez_usb.dd | head -15
```

### Step 3: Files
List the top level, then everything, then only deleted entries:

```bash
fls -o 2048 rvaldez_usb.dd
fls -r -o 2048 rvaldez_usb.dd
fls -r -d -o 2048 rvaldez_usb.dd
```

A `*` marks a deleted entry. The number before the `:` is its entry (inode) number.

### Step 4: Recover a Deleted File
Replace `ENTRY` with the entry number of the deleted PDF:

```bash
icat -o 2048 rvaldez_usb.dd ENTRY > recovered.pdf
file recovered.pdf
sha256sum recovered.pdf
```

Open `recovered.pdf` and look at it.

### Step 5: The Second Partition
Use the Start sector of the Linux partition from Step 1:

```bash
fls -r -o 83968 rvaldez_usb.dd
```

Find `.bash_history`, note its entry number, and read it:

```bash
icat -o 83968 rvaldez_usb.dd ENTRY
```

### Step 6: Timeline
```bash
fls -r -m / -z Asia/Manila -o 2048 rvaldez_usb.dd > p1.body
fls -r -m / -o 83968 rvaldez_usb.dd > p2.body
cat p1.body p2.body | mactime -b - -z Asia/Manila -d > timeline.csv
grep "Sep 14 2026" timeline.csv | less
```

### Part 2 Questions
1. How many partitions are there? Give each one's type and start sector.
2. What is the FAT32 volume label?
3. List every deleted file on partition 1 with its entry number.
4. One deleted file's name starts with `_`. Why is the first letter missing?
5. Give the SHA-256 of `recovered.pdf`. What is the document?
6. List the commands in `.bash_history` that relate to the KESTREL files, and say what each one did.

---

## Part 3: Analyse in Autopsy

### Step 1: Create the Case
1. **New Case**. Case name: `lab08-<your-surname>`.
2. Case number: `HM-2026-014`. Examiner: your name.

### Step 2: Add the Image
1. Choose **Disk Image or VM File** and select `rvaldez_usb.dd`.
2. Set **Time zone** to `Asia/Manila`.
3. Click **Next**.

### Step 3: Choose Ingest Modules
1. **Untick** these three. They only work on Windows and stop ingest on Linux and macOS:
   - **YARA Analyzer**
   - **Android Analyzer (aLEAPP)**
   - **iOS Analyzer (iLEAPP)**
2. Select **Extension Mismatch Detector** and set it to **Check all file types**.
3. Leave the rest ticked. Click **Next**, then **Finish**.

Wait for the progress bar at the bottom right to finish.

> If **Extension Mismatch Detected** stays empty, open **Views → File Types → By MIME Type** and compare each file's name with its type.

### Step 4: Search for Keywords
In the **Keyword Search** box at the top right, search for each of these:
- `KESTREL`
- `vantaro`

### Step 5: Find the Evidence
Use the tree on the left:

| Look in | You are looking for |
|---|---|
| **Views → Deleted Files** | Files someone tried to remove |
| **Data Artifacts → Extension Mismatch Detected** | Files whose name hides their real type |
| **Data Artifacts → EXIF Metadata** | Where and when photos were taken |
| **Data Artifacts → Metadata** | Who wrote a document, and when |
| **Data Artifacts → Web History** and **Web Searches** | What the user looked up and visited |
| **Keyword Hits** | Your Step 4 searches |

Tag each item you will cite: right-click → **Add File Tag** → **Notable Item**.

### Step 6: Build the Timeline
Open **Timeline** (toolbar). Zoom to **14 September 2026, 20:00–22:00**. Line up your tagged items in order.

### Step 7: Export the Report
**Generate Report** → **HTML Report** → **Tagged Results**. Save it in `~/lab08`.

### Part 3 Questions
7. Which file has an extension that does not match its content? What is it really, and what is inside?
8. Where and when was `IMG_2041.jpg` taken? What does it show?
9. List the web searches and visits from 14 September 2026, with times.
10. Give a timeline of the leak on 14 September: at least six events, each with its time and source artefact.

---

## Part 4: Report

### Step 1: Re-verify the Image
```bash
sha256sum rvaldez_usb.dd
```

Fill in row 4 of the custody form. The hash must still match row 2.

### Step 2: Write the Findings Memo
One page, using these headings:

1. **Request:** who asked, what question, and when.
2. **Evidence:** the image name and its SHA-256.
3. **Tools:** names and versions (Autopsy 4.22.1, The Sleuth Kit 4.14).
4. **Findings:** answer the three case questions. Cite an artefact for each finding.
5. **Timeline:** the key events from Question 10.
6. **Limits:** what this image cannot show, and what other evidence would settle it.

Keep three things apart:
- **Fact:** what the artefact shows.
- **Inference:** what you conclude from it.
- **Opinion:** only if asked, and labelled.

---

## Submission
Submit one PDF containing:
- The completed custody form (rows 3 and 4)
- Answers to Questions 1–10
- The findings memo
- The Autopsy HTML report, zipped, as a separate file

## Grading

| Part | Weight |
|---|---|
| Custody form and hashes | 20% |
| Questions 1–10 | 30% |
| Findings memo: findings cite artefacts, facts are kept apart from inferences, limits are stated | 50% |
