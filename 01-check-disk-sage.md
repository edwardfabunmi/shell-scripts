# Check Disk Usage in Linux System

````
#!/bin/bash

echo "Check Disk Usage in Linux System"

# Fetch usage percentage for the root filesystem (/)
disk_size=$(df /dev | awk 'NR==2 {print $5}' | tr -d '%')

echo "${disk_size}% of disk is filled"

if [ "$disk_size" -gt 80 ]; then
    echo "Disk utilization is more than 80%, expand or delete some unused files to give more storage."
else
    echo "Enough disk space is available."
fi
````


---

### Key Improvements Made:

* **`df /`**: Specifically targets the root mount point so `disk_size` always receives a **single integer value**.
* **`NR==2`**: Ensures `awk` only reads the second line (skipping the header row).
* **`tr -d '%'`**: Cleaner way to strip the `%` symbol compared to `cut -d '%' -f1`.
* **Quoted `"$disk_size"**`: Prevents crash errors if the variable ever ends up empty.


In the Linux command line, `tr` stands for **Translate** (or **Transform**), and the `-d` flag stands for **Delete**.

---

### Breakdown:

* **`tr`** = **Translate**
A utility used to translate, squeeze, or delete characters from standard input.
* **`-d`** = **Delete**
An option that tells `tr` to **delete** any characters that match the set you provide instead of translating them.

---

### Example:

```bash
echo "84%" | tr -d '%'

```

* **Input:** `84%`
* **Action:** Delete (`-d`) the `%` character.
* **Output:** `84`
