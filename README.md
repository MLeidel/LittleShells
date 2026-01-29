# LittleShells
collection of handy little bash scripts

-----

## notfil.sh 

**Description:**  

Opens a (zenity --text-info) text editor, which when closed, saves the text
to a standerd date-time stamped text file, like **`notes_2025-05-01-163902.txt`**
on the Desktop.

**Code:**
    
        #!/bin/sh
        
        TIMESTAMP=$(date +"%Y-%m-%d-%H%M%S")
        FILE="notes_${TIMESTAMP}.txt"
        touch "/home/${USER}/Desktop/${FILE}"
        
        zenity --text-info \
               --title="Notes" \
               --editable > "/home/${USER}/Desktop/${FILE}"
        
        zenity --notification\
            --window-icon="info" \
            --text="File created on Desktop!"
        
        
**Requires:** "zenity"

        sudo apt install zenity  
        
-----

## clip2file.sh

**Description:**  

Saves Text from clipboard to a standerd date-time stamped text file, 
like **`clip_2025-05-01-163902.txt`** on the Desktop.

**Code**

        #!/bin/bash
        
        # Get the content from system clipboard
        CLIP_CONTENT=$(xclip -o -selection clipboard)
        
        # Get the current date and time
        TIMESTAMP=$(date +"%Y-%m-%d-%H%M%S")
        
        # Create the output filename
        FILENAME="/home/${USER}/Desktop/clip_${TIMESTAMP}.txt"
        
        # Write the clipboard content to the file
        echo "$CLIP_CONTENT" > "$FILENAME"
        
        zenity --notification \
            --window-icon="info" \
            --text="File created on Desktop!"

**Requires:** "zenity" and "xclip"

        sudo apt install zenity xclip

----
    
## ClipAppend.sh

**Description**
    
Saves (appends) text (with datetime) from clipboard to file "~/clips.txt"

**Code**

        #!/bin/bash
        
        CLIP_CONTENT=$(xclip -o -selection clipboard)
        
        # Create the output path & filename
        FILENAME="/home/${USER}/clips.txt"
        
        # Get the current date and time
        TIMESTAMP=$(date +"%Y-%m-%d-%H%M%S")
        
        # Write the clipboard content to the file
        printf "%s\n%s\n\n" "$TIMESTAMP" "$CLIP_CONTENT" >> "$FILENAME"
        
        zenity --notification \
            --window-icon="info" \
            --text="Clip Appended to clips.txt"
        
**Requires:** "zenity"

        sudo apt install zenity

---
