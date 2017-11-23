# Docker-Pandoc

[![](https://images.microbadger.com/badges/version/knsit/pandoc.svg)](https://microbadger.com/images/knsit/pandoc "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/knsit/pandoc.svg)](https://microbadger.com/images/knsit/pandoc "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/commit/knsit/pandoc.svg)](https://microbadger.com/images/knsit/pandoc "Get your own commit badge on microbadger.com")

## Usage

The easiest way to use this container is to mount a volume into the container and run pandoc afterwards:

```bash
docker run --rm -v /path/to/markdown/files:/home/pandoc baez90/docker-pandoc:latest pandoc my-markdown.md -o my-pdf.pdf
```

Or to convert multiple files at once you could run a script like that:

```bash
docker run --rm -v /path/to/markdown/files:/home/pandoc baez90/docker-pandoc:latest /bin/sh build-pdfs.sh
```

where the `build-pdfs.sh` could look like this

```bash
#!/bin/sh
[ -d pdf_out ] || mkdir pdf_out
find . -name "*.md" -type f | while IFS='' read -r PATHNAME; do
	OUTFILE="${PATHNAME/.md/.pdf}"
	pandoc $PATHNAME --pdf-engine=pdflatex -o pdf_out/$OUTFILE
done
```

to convert all markdown files in the current folder to PDF files.

You may also use it interactive:

```bash
docker run --rm -ti -v /path/to/markdown/files:/home/pandoc baez90/docker-pandoc:latest
```
