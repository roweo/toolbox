# Build scripts

## HTML

`docker run --rm --volume "${PWD}:/data" pandoc/core:2.13 -s -f markdown -t html -o cardene.html cardene.md`

## ICML

`docker run --rm --volume "${PWD}:/data" pandoc/core:2.13 -s -f markdown -t icml -o cardene.icml cardene.md`

## Word (with template)

`pandoc -f markdown -t docx -o cardene.docx cardene.md`