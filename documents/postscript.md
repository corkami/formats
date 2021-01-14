# PostScript

- Adobe's [PostScript Language Reference Manual](https://www.adobe.com/content/dam/acom/en/devnet/actionscript/articles/psrefman.pdf).
- [PoCorGTFO 13](https://github.com/angea/pocorgtfo#0x13), a PS/PDF polyglot.


The whole file is parsed from offset `0`, but the signature doesn't need to be at offset `0`

- Signature: `%!PS`
- Line comment declaration: `%`
- Multi-line comment: an unused function
```
/{(
)}
```
- Terminator: `stop`


# [GhostScript](https://www.ghostscript.com/)

- Signature not necessary
- Whitespace: all control codes `0x0-0x1F` (!)
- Comment parasite shouldn't contain newline/FormFeed (0xA, 0xC or 0xD).
- Function parasite should contain balanced parenthesis (that's all !)


## File structure

```
File ::= Junk* ( Statement | Junk )* AppData?

AppData ::= 'stop' .*

Junk ::= whitespace | ComParasite | FuncParasite

whitespace ::= ControlCodes

ComParasite ::= '%' NoNewLine* NewLine

NoNewLine ::= [^#xA#xC#xD]

NewLine ::= #xA | #xC | #xD

FuncParasite ::= '/{(' BalancedParenthesis* ')}'

BalancedParenthesis ::= [^()]* | '(' [^()]* ')'
```

So in a PS, junk is:
- `<all 00-1F>`
- `%` `<all 00-FF except A, C, D>`
- `/{(` `<all 00-FF except parenthesis unless balanced>)}`


## Crypto-parasites

- How early can the other format declare a comment?
- Does it contain a newline before that comment (Ex: `0xC` in Gzip, PNG, JP2)
- How much of the other files contains balanced parenthesis ? 

If it's not possible to declare a comment early before a newline,
if it contains an unbalanced parenthesis,
it might be impossible to do a crypto-polyglot.
