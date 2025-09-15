import os
import shutil

# ---------------- CONFIG ----------------
faces_folder = os.path.dirname(os.path.abspath(__file__))  # folder where script runs
config_file = os.path.join(faces_folder, "config.xml")
backup_file = os.path.join(faces_folder, "backupconfig.xml")
skipped_file = os.path.join(faces_folder, "skipped_log.txt")
valid_exts = {".png", ".jpg", ".jpeg"}

header = "<record>\n\t<boolean id=\"preload\" value=\"false\"/>\n\t<boolean id=\"amap\" value=\"false\"/>\n\t<list id=\"maps\">"
footer = "\t</list>\n</record>"

# ---------------- BACKUP ----------------
if os.path.exists(config_file) and os.path.getsize(config_file) > 0:
    shutil.copy2(config_file, backup_file)
    print(f"Backup created: {backup_file}")
else:
    print("No existing config.xml to backup.")

# ---------------- SCAN FACES ----------------
records = []
skipped = []

all_files = list(os.scandir(faces_folder))
total_files = len(all_files)
print(f"\nScanning {total_files} files for valid face images...\n")

with open(skipped_file, "w", encoding="utf-8") as log:
    for i, entry in enumerate(all_files, 1):
        if entry.is_file():
            name, ext = os.path.splitext(entry.name)
            ext = ext.lower()
            if ext in valid_exts and name.isdigit():
                records.append(f'\t\t<record from="{name}" to="graphics/pictures/person/{name}/portrait"/>')
            elif ext in valid_exts:
                skipped.append(f"{entry.name} → bad filename")
                log.write(f"{entry.name} → bad filename\n")
            else:
                skipped.append(f"{entry.name} → unsupported extension")
                log.write(f"{entry.name} → unsupported extension\n")

        # show progress every 50k files or at the end
        if i % 50000 == 0 or i == total_files:
            print(f"   → Processed {i}/{total_files} files")

# sort records by numeric ID
records.sort(key=lambda r: int(r.split('"')[1]))

# ---------------- WRITE CONFIG ----------------
with open(config_file, "w", encoding="utf-8") as f:
    f.write(header + "\n")
    f.write("\n".join(records) + "\n")
    f.write(footer)

print(f"\n✅ Config.xml generated with {len(records)} records at '{config_file}'")

if skipped:
    print(f"⚠ Skipped {len(skipped)} files (full list saved to {skipped_file}):")
    for s in skipped:
        print("   -", s)

input("\nPress Enter to exit...")  # keep terminal open
