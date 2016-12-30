<!-- This file was auto-generated by the 'readme' makefile target. -->

Prettyprinter à la Wadler/Leijen
================================



Master build: [![status](https://travis-ci.org/quchen/prettyprinter.svg?branch=master)](https://travis-ci.org/quchen/prettyprinter)

This module defines a prettyprinter to format text in a flexible and convenient
way. The idea is to combine a document out of many small components, then using
a layouter to convert it to an easily renderable simple document, which can then
be rendered to a variety of formats, for example plain `Text`, or Markdown.
**What you are reading right now was generated by this library.** Don't believe
me? Well, the source code is added at the very bottom.

`wl-pprint` is the core of a collection of modules. It defines the language to
generate nicely laid out documents, which can then be given to renderers to
display them in various ways, e.g. HTML, plain text, or ANSI terminal. There are
also compatibility modules to make transition from old versions of the
`wl-pprint` libraries easier.

Differences to the old Wadler/Leijen prettyprinter
--------------------------------------------------

The library started as a fork of ansi-wl-pprint until every line had been
touched. The result is still in the same spirit as its predecessors, but
modernized to match the current ecosystem and needs.

The most significant changes are:

  1. `(<$>)` is removed as an operator, since it clashes with the common alias
     for `fmap`.
  2. All but the essential `<>` and `<+>` operators were replaced by ordinary
     names.
  3. Everything extensively documented, with references to other functions and
     runnable code examples.
  4. Use of `Text` instead of `String`.
  5. An `optimize` function to fuse text together before rendering for
     efficiency.
  6. Instead of providing an own colorization function for each
     color/intensity/layer combination, they have been combined in 'color',
     'colorDull', 'bgColor', and 'bgColorDull' functions.



Migration guide
---------------

If you're coming from (ansi-)wl-pprint, you should feel right at home. Some
definitions have changed though, so the Haddock documentation features a
paragraph about this at the very bottom.If you just want to use this package
without worrying about how to adapt to the new functionality, there are
compatibility modules available:

  - Old wl-pprint: wl-pprint-compat-old
  - Old wl-pprint-ansi: wl-pprint-compat-old-ansi



Code that generated this
------------------------

As promised in the first paragraph, here's the source code that generated this
readme.

```haskell
{-# LANGUAGE OverloadedStrings #-}

module Main (main) where



import Prelude hiding (words)

import           Data.Text                             (Text)
import qualified Data.Text                             as T
import qualified Data.Text.IO                          as T
import           Data.Text.Prettyprint.Doc
import           Data.Text.Prettyprint.Doc.Render.Text



main :: IO ()
main = do
    selfSource <- T.readFile "wl-pprint/app/GenerateReadme.hs"
    (T.writeFile "README.md" . renderStrict . layoutPretty 1 80 . (<> hardline)) (readmeContents selfSource)

readmeContents :: Text -> Doc
readmeContents selfSource = mconcat
    [ htmlComment "This file was auto-generated by the 'readme' makefile target."

    , h1 "Prettyprinter à la Wadler/Leijen"

    , line <> line
    , "Master build: [![status](https://travis-ci.org/quchen/prettyprinter.svg?branch=master)](https://travis-ci.org/quchen/prettyprinter)"
    , line <> line

    , paragraph "This module defines a prettyprinter to format text in a\
        \ flexible and convenient way. The idea is to combine a document out\
        \ of many small components, then using a layouter to convert it to an\
        \ easily renderable simple document, which can then be rendered to a\
        \ variety of formats, for example plain `Text`, or Markdown. **What you\
        \ are reading right now was generated by this library.** Don't believe\
        \ me? Well, the source code is added at the very bottom."
    , line <> line
    , paragraph "`wl-pprint` is the core of a collection of modules. It\
        \ defines the language to generate nicely laid out documents, which can\
        \ then be given to renderers to display them in various ways, e.g.\
        \ HTML, plain text, or ANSI terminal. There are also compatibility\
        \ modules to make transition from old versions of the `wl-pprint`\
        \ libraries easier."

    , h2 "Differences to the old Wadler/Leijen prettyprinter"

    , paragraph  "The library started as a fork of ansi-wl-pprint until\
        \ every line had been touched. The result is still in the same spirit\
        \ as its predecessors, but modernized to match the current ecosystem \
        \ and needs."
    , line <> line
    , paragraph  "The most significant changes are:"
    , line <> line
    , (indent 2 . orderedList . map paragraph)
        [ "`(<$>)` is removed as an operator, since it clashes with the common alias for `fmap`."
        , "All but the essential `<>` and `<+>` operators were replaced by ordinary names."
        , "Everything extensively documented, with references to other functions and runnable code examples."
        , "Use of `Text` instead of `String`."
        , "An `optimize` function to fuse text together before rendering for efficiency."
        ]


    , h2 "Migration guide"

    , paragraph "If you're coming from (ansi-)wl-pprint, you should feel right\
        \ at home. Some definitions have changed though, so the Haddock\
        \ documentation features a paragraph about this at the very bottom."

    , paragraph "If you just want to use this package without worrying about\
        \ how to adapt to the new functionality, there are compatibility\
        \ modules available:"
    , line <> line
    , (indent 2 . unorderedList . map paragraph)
        [ "Old wl-pprint: wl-pprint-compat-old"
        , "Old wl-pprint-ansi: wl-pprint-compat-old-ansi"
        ]

    , h2 "Code that generated this"

    , paragraph "As promised in the first paragraph, here's the source code\
        \ that generated this readme."
    , line <> line
    , "```haskell" <> hardline <> pretty selfSource <> "```"
    ]

paragraph :: Text -> Doc
paragraph = fillSep . map pretty . T.words

h1 :: Doc -> Doc
h1 = underlineWith "="

h2 :: Doc -> Doc
h2 = underlineWith "-"

underlineWith :: Text -> Doc -> Doc
underlineWith symbol x = hardline <> hardline <> content <> hardline <> hardline
  where
    content = align (width x (\w ->
        hardline <> pretty (T.take w (T.replicate w symbol))))

orderedList :: [Doc] -> Doc
orderedList = align . vsep . zipWith (\i x -> pretty i <> dot <+> align x) [1::Int ..]

unorderedList :: [Doc] -> Doc
unorderedList = align . vsep . map ("-" <+>)

htmlComment :: Doc -> Doc
htmlComment = enclose "<!-- " " -->"
```
