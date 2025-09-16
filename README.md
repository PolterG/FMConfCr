# FMConfigCreator

I was running into facepack issues when I tried to add some of my own images. I found that the `config.xml` was not being generated correctly by the software I was using. It also struggled with large facepacks.

So I wrote FMConfigCreator — a Python script that generates the `config.xml` file for Football Manager quickly, reliably, and foolproof!

---

## Description

**FMConfigCreator** scans the folder it is run in for valid face images and writes them into the correct format for Football Manager. It works in seconds, even with very large facepacks.

It ensures all valid images are included, creates a backup of any existing config, and logs skipped files for your reference. 
⚠ Note: The script has only been tested with facepacks, not with other types of graphics mods.

---

## Features

- Scans the current folder for face images (`.png`, `.jpg`, `.jpeg`) with **numeric filenames only**.  
- Creates a backup of any existing `config.xml` (`backupconfig.xml`) before overwriting.  
- Generates `config.xml` with **sorted records** for all valid faces.  
- Logs all **skipped files** (invalid names or unsupported extensions) into `skipped_log.txt`.  
- Displays a **progress counter** while scanning large numbers of files.  
- Keeps the **terminal open** after finishing so you can review the results.

---

## Requirements

- Python 3.x installed  
- Basic knowledge of running Python scripts in terminal/command prompt
- Image files named using their in-game ID

---

## Setup

1. Download `FMConfigCreator.py` and place it in the folder with your facepack images.  
2. Make sure Python is installed and available in your system PATH.  

---

## Usage

Open a terminal / command prompt in the folder containing your face images and the script.

Then run the script:

```python3 FMConfigCreator.py```

The script will automatically create a backup (backupconfig.xml) if config.xml already exists.

After scanning, it will generate config.xml with all valid faces.

```
Skipped files are logged in skipped_log.txt and displayed in the terminal.
Example Output
🗂 Backup created: backupconfig.xml
🔍 Scanning 12,345 files for valid face images...

   → Processed 5,000/12,345 files
   → Processed 10,000/12,345 files
   → Processed 12,345/12,345 files

✅ Config.xml generated with 12,312 records at 'config.xml'
⚠ Skipped 33 files (full list saved to skipped_log.txt):
   - 12345-.png → invalid filename
   - 67890 L.jpg → invalid filename
   - oldface.png → unsupported extension

Press Enter to exit...
```
## Notes

-Only numeric filenames are included in config.xml. Files with letters, dashes, or spaces are logged in skipped_log.txt.

-The script does not delete, move or alter skipped files; it only logs them.

-The terminal stays open at the end so you can check results and skipped files.

---

## License

This project is released under the MIT License. See LICENSE file for details.
  
---

