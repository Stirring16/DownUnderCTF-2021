# rabbit

>Can you find Babushka's missing vodka? It's buried pretty deep, like 1000 steps, deep.

> Author: Crem + z3kxTa


[flag.txt](https://github.com/Stirring16/DownUnderCTF-2021/files/7243085/flag.txt)


# Solution

 this file is actually a compressed file of either bzip2, zip, gzip or xz format. And, as the description for the challenge suggests, it contains another compressed file of the same type and so on. decompressing each file manually is possible but will require a lot of work, so we can automate the process by scripting.
 
 
 We can use 7zip and [Auto Click](https://autoclicker.fr.uptodown.com/windows)
 Like this :D


https://user-images.githubusercontent.com/62060867/135070363-4f421f6d-4f0f-4e0e-89e3-3264f8e10c4c.mp4

or we can use this script which I refer to in another article

```
#!/bin/bash
get_flag() {
	for filename in $(pwd)/*; do
		echo "$filename"
		if [[ $(file --mime-type -b "$filename") == "application/x-bzip2" ]]
		then
			bunzip2 "$filename"
			rm "$filename"
			get_flag
			return
		elif [[ $(file --mime-type -b  "$filename") == "application/zip" ]]
		then
			mv $filename flag.zip
			unzip flag.zip
			rm flag.zip
			get_flag
			return
		elif [[ $(file --mime-type -b  "$filename") == "application/x-xz" ]]
		then
			mv $filename flag.xz 
			unxz -f flag.xz
			rm flag.xz
			get_flag
			return
		elif [[ $(file --mime-type -b  "$filename") == "application/gzip" ]]
		then
			mv $filename flag.gz
			gunzip flag.gz
			rm flag.gz
			get_flag
			return
		else
			cat "$filename"
			return
		fi
	done
}

get_flag
```

