# Digitial Forensics Notes

## Metadata
- ```pdfinfo DOCUMENT.pdf``` (displays various metadata related to pdf file)
- ```exiftool IMAGE.jpg``` (displays to read and write metadata in various file types, such as JPEF images)

## picoCTF Forensics Challenges

Link to picoCTF folder: [picoCTF]{https://github.com/esteban-Bayern25/Cyber-Training/tree/main/Forensics/picoCTF}

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
