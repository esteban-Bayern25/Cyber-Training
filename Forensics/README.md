# Digitial Forensics Notes

## Metadata
- ```pdfinfo DOCUMENT.pdf``` (displays various metadata related to pdf file)
- ```exiftool IMAGE.jpg``` (displays to read and write metadata in various file types, such as JPEF images)

## picoCTF Forensics Challenges

Link to picoCTF folder: [picoCTF](https://github.com/esteban-Bayern25/Cyber-Training/tree/main/Forensics/picoCTF)

### Riddle Registry
1. download the pdf
2. investigate the pdf using the pdfinfo tool
3. Author seems suspicous or at least encrypted
4. Needed to decrypt the message so I use echo the aurthor name onto a txt file in which I decrypted
5. using the command ```base64 -D -i catBase64.txt``` this allows you to find the flag hidden within the pdf

### Hidden in plainsight
1. Download the jpg file
2. Using the metadata command for jpg exiftool
3. Cafeful observation and it appears the the comment might be encoded via Huffman
4. Well the comments when you use Base64 appears to be saying to use maybe steghide: cEF6endvcmQ=% 
5. This appears to be yet another type of encryption
6. Intresting enought we do get pAsszword when we decrypt 64 meaning we must now use the steghide
7. Using Ubuntuu I use the steghide command in which I am able to to then use these following commands
 - ``` steghide --info img.jpg ```
 - ``` steghide extract -sf img.jpg -xf flag.txt ``` 
where I then can use the cat command on the flag.txt file to get the hidden flag

### Corrupted File
1. observe the file using the tools
2. notice that the hexdump is performed to determine the file type we must restore in this case its a jpeg
3. Since the file is corrupruted or changed, we must use file and hexdump coammnds to analye the file type and contents
3. There is a special command that must be in use: 
``` (printf '\xff\xd8' && tail -c +3 file) > repair.jpg```
this allows the image to be repaired
4. Once the jpg file is repared you are then able to see the flag in the actual image