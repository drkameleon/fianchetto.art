
<p align="center"><img align="center" width="500" src="https://raw.githubusercontent.com/drkameleon/fianchetto.art/main/icon.png"/></p>
<p align="center">
  <b>Chess-aware components / custom types,<br>and more...</b>
  <br><br>
    <img src="https://img.shields.io/github/license/arturo-lang/grafito?style=for-the-badge">
  <img src="https://img.shields.io/badge/language-Arturo-orange.svg?style=for-the-badge">
  
  


</p>

<!--<p align="center"><img width="90%" align="center" src="https://raw.githubusercontent.com/drkameleon/tabular.art/main/screenshot.png"/></p>-->

--- 
 
<!--ts-->

* [What does this package do?](#what-does-this-package-do)
* [How do I use it?](#how-do-i-use-it)
* [Type Reference](#type-reference)
   * [chessCoords](#chesscoords)
   * [chessPiece](#chesspiece)
   * [chessMove](#chessmove)
   * [chessBoard](#chessboard)
   * [chessPosition](#chessposition)
   * [chessGame](#chessgame) 
* [License](#license)   

<!--te-->
 
---

### What does this package do?

This package includes different useful types for chess programming & analysis: pieces, boards, moves, positions, games. It also comes with FEN & PGN parsing/output capabilities and can - potentially - serve as the foundation of other chess-related apps & packages.

### How do I use it?

Simply `import` it and use any of the provided helper functions or types:

```red
import .withHelpers "fianchetto"!

; Let's create a new chess game!
game: newGame ø!

; What about showing the FEN string?
print ["Initial FEN:" game\position]

; Make moves using coordinates
game\makeMove "e2e4"
game\makeMove "e7e5"
game\makeMove "g1f3"

; and... let's print board!
print "Final position:"
print game\position\board
```

Will produce:

```
Initial FEN: rnbkqbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBKQBNR w KQkq - 0 1 
Final position:
+---+---+---+---+---+---+---+---+
| r | n | b | q | k | b | n | r |
| p | p | p | p | - | p | p | p |
| - | - | - | - | - | - | - | - |
| - | - | - | - | p | - | - | - |
| - | - | - | - | P | - | - | - |
| - | - | - | - | - | N | - | - |
| P | P | P | P | - | P | P | P |
| R | N | B | Q | K | B | - | R |
+---+---+---+---+---+---+---+---+
```

### Type reference

#### chessCoords

Mainly used to hold square coordinates, or a file-rank pair.

##### constructor

<pre>
<b>to :chessCoords</b> [<ins>coords</ins> <i>:string :block :integer</i>]
</pre>

##### fields

- `\file`
- `\rank`

##### methods

- `\index`

#### chessPiece

The main chess piece representation

##### constructor

<pre>
<b>to :chessPiece</b> [<ins>ch</ins> <i>:char :literal :string</i>]
</pre>

##### fields

- `\color`
- `\kind`

##### methods

- `\white?`
- `\getMovePattern [fromSq :chessCoords, toSq :chessCoords]`

#### chessMove

A move type, encapsulating an origin and a target square.

##### constructor

<pre>
<b>to :chessMove</b> [<ins>coordset</ins> <i>:string :block</i>]
</pre>

##### fields

- `\fromSq`
- `\toSq`

#### chessBoard

The main chess board

##### constructor

<pre>
<b>to :chessBoard</b> []
</pre>

##### fields

- `\squares`

##### methods

- `\getPiece [coords :chessCoords]`
- `\setPiece [coords :chessCoords piece :null :chessPiece]`

#### chessPosition

A given chess position

##### constructor

<pre>
<b>to :chessPosition</b> [<ins>source</ins> <i>:string :null</i>]
</pre>

##### fields

- `\board`
- `\activeColor`
- `\castling`
- `\enPassant`
- `\halfmove`
- `\fullmove`

##### methods

- `\validateMove [newMove :chessMove]`
- `\applyMove [newMove :chessMove]`

> [!TIP]
> You can initialize a `:chessPosition` by directly using a FEN string; or exporting a given position back to FEN, using `to :string`. 😉

#### chessGame

The main chess game container

##### constructor

<pre>
<b>to :chessGame</b> [<ins>source</ins> <i>:string :null</i>]
</pre>

##### fields

- `\position`
- `\moves`
- `\result`
- `\metadata`

##### methods

- `\makeMove: [coords :chessMove :string]`

> [!WARNING]
> Although the future goal of the `:chessGame` constructor is to fully support any type of PGN file input, right now support should be considered extremely limited!

<hr/>

### License

MIT License

Copyright (c) 2024 Yanis Zafirópulos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
