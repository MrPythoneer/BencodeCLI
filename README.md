# BencodeCLI "GoBen"
CLI tool for decoding torrent files and encoding json into torrent file format  

# Usage
```
goben [-e | -d [-i input_file]] [-o output_file] [text]
        -d - Set mode to decode
        -e - Set mode to encode
        -i filepath - input file
        -o filepath - redirects stdout to file
        -h - help
```

# Example
## Encoding
Encoding a json string to bencode
```bash
$ goben -e '["hello", "world", 12345, {"type": 1, "animal": "cat"}]'
l5:hello5:worldi12345ed6:animal3:cat4:typei1eee
```
***
Encoding a json file to bencode
```bash
$ goben -e -i sample.json
d8:glossaryd5:title16:example glossary8:GlossDivd5:title1:S9:GlossListd10:GlossEntryd8:GlossSee6:markup2:ID4:SGML6:SortAs4:SGML9:GlossTerm36:Standard Generalized Markup Language7:Acronym4:SGML6:Abbrev13:ISO 8879:19868:GlossDefd12:GlossSeeAlsol3:GML3:XMLe4:para72:A meta-markup language, used to create markup languages such as DocBook.eeeeee
```
***
Encoding a json file to bencode and save to *output.torrent*
```bash
$ goben -e -i sample.json -o output.torrent
```

## Decoding
Decode a bencode string
```bash
$ goben -d 'l5:hello5:worldi12345ed6:animal3:cat4:typei1eee'
["hello", "world", 12345, {"type": 1, "animal": "cat"}]
```
***
Decode a bencoded file
```bash
$ goben -d -i sample.torrent
{"info": {"name": "sample.txt", "piece length": 65536, "pieces": "", "private": 1, "length": 20}, "announce": "udp://tracker.openbittorrent.com:80", "creation date": 1327049827}
```
***
Decode a bencoded file and save tp *output.json*
```bash
$ goben -d -i sample.torrent -o output.json
```
