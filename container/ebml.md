Extensible Binary Meta Language

- http://matroska-org.github.io/libebml/specs.html
- https://github.com/cellar-wg/matroska-specification/blob/master/ebml_matroska.xml


# Tools
- dissection with `mkvinfo -a -o -p -X`
- attachments with:
 - `mkvpropedit matroska.mkv --add-attachment zip.zip`
 - `ffmpeg -i matroska.mkv -vcodec copy -acodec copy -attach pdf.pdf -metadata:s:1 mimetype=application/pdf polyglot.mkv`

cf https://github.com/QBobWatson/python-ebml
