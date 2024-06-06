# File Sharing in Command Line direct share

## [`0x0.st`](https://0x0.st/) - THE NULL POINTER

<https://0x0.st/>

```sh
# HTTP POST files here:
curl -F'file=@yourfile.png' https://0x0.st

# You can also POST remote URLs:
curl -F'url=http://example.com/image.jpg' https://0x0.st

# If you don't want the resulting URL to be easy to guess:
curl -F'file=@yourfile.png' -Fsecret= https://0x0.st
curl -F'url=http://example.com/image.jpg' -Fsecret= https://0x0.st

# It is possible to append your own file name to the URL:
#    https://0x0.st/aaa.jpg/image.jpeg

# File URLs are valid for at least 30 days and up to a year (see below).

# Files can be set to expire sooner by adding an "expires" parameter (in hours)
curl -F'file=@yourfile.png' -Fexpires=24 https://0x0.st

# OR by setting "expires" to a timestamp in epoch milliseconds
curl -F'file=@yourfile.png' -Fexpires=1681996320000 https://0x0.st

# Expired files won't be removed immediately but within the next minute.

# Whenever a file that does not already exist or has expired is uploaded,
# the HTTP response header includes an X-Token field. You can use this
# to perform management operations on the file.

# When using cURL, you can add the -i option to view the response header.

# To delete the file immediately:
curl -Ftoken=token_here -Fdelete= https://0x0.st/abc.txt

# To change the expiration date (see above):
curl -Ftoken=token_here -Fexpires=3 https://0x0.st/abc.txt
```

## [`transfer.sh`](https://transfer.sh/) *Older Service*

<https://transfer.sh/>

 Here are some significant features that `transfer.sh` offers:

- Requires no GUI, uses the command line.
- Upload files with sizes up to 10GB.
- Files are only stored for 14 days.
- Optionally encrypt the files with GPG before transfer.
- Limit the number of downloads and days for which the file will be available.

```sh
# Uploading a File via cURL
curl --upload-file <path-to-file> https://transfer.sh

# You can tweak the above command to change the name and extension
# of the uploaded file in this manner:
curl --upload-file <path-to-file> https://transfer.sh/<file_name.extension>

# Uploading via Shell Function
transfer(){ if [ $# -eq 0 ];then echo "No arguments specified.\nUsage:\n transfer <file|directory>\n ... | transfer <file_name>">&2;return 1;fi;if tty -s;then file="$1";file_name=$(basename "$file");if [ ! -e "$file" ];then echo "$file: No such file or directory">&2;return 1;fi;if [ -d "$file" ];then file_name="$file_name.zip" ,;(cd "$file"&&zip -r -q - .)|curl --progress-bar --upload-file "-" "https://transfer.sh/$file_name"|tee /dev/null,;else cat "$file"|curl --progress-bar --upload-file "-" "https://transfer.sh/$file_name"|tee /dev/null;fi;else file_name=$1;curl --progress-bar --upload-file "-" "https://transfer.sh/$file_name"|tee /dev/null;fi;}

```

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
