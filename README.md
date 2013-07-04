exist-stanford-ner
==================

Integrate the Stanford Named Entity Recognizer into eXist-db.

## Compile and install

1) clone the github repository: https://github.com/wolfgangmm/exist-stanford-ner
2) edit build.properties and set exist.dir to point to your eXist install directory
3) call "ant" in the directory to create a .xar
4) upload the xar into eXist using the dashboard

## Functions

There are only two functions:

ner:classify-string($classifier as xs:anyURI, $text as xs:string) - processes a single string of text and returns a sequence of text nodes and elements (person, location, organization)

ner:classify-node($classifier as xs:anyURI, $node as node()) as node() - returns an in-memory copy of $node with all named entities wrapped into inline elements.

## Usage example

```xquery
xquery version "3.0";

import module namespace ner="http://exist-db.org/xquery/stanford-ner";

let $classifier := xs:anyURI("/db/apps/stanford-ner/resources/classifiers/english.all.3class.distsim.crf.ser.gz")
let $text := <p>The fate of Lehman Brothers, the beleaguered investment bank,
   hung in the balance on Sunday as Federal Reserve officials and the leaders
   of major financial institutions continued to gather in emergency meetings
   trying to complete a plan to rescue the stricken bank.  Several possible
   plans emerged from the talks, held at the Federal Reserve Bank of New York
   and led by Timothy R. Geithner, the president of the New York Fed, and
   Treasury Secretary Henry M. Paulson Jr.</p>
return
 ner:classify-node($classifier, $text)
```
