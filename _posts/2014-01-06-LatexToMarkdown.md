---
layout: post
title: LaTeX to Markdown
---
# LaTeX to Markdown
Ich habe vor einiger Zeit eine wissenschaftliche Arbeit mit LaTeX geschrieben.
Nun wollte ich sie bei leanpub veröffentlichen. Ich dachte, das könne doch
nicht so schwer sein. Schwer war es nicht, aber doch eine ziemliche Viecherei.
Vieles ließ sich aber durch Ersetzungen mit vim erledigen.

Die Arbeit enthält einiges an mathematischen Formeln. Da war es ganz nett, dass
Markdown auch Formeln aus LaTeX versteht, allerdings sind die Marker zum
Begrenzen des mathematischen Modus etwas anders. Der folgende Befehl ersetzt
durch $ abgegrenzte Inline-Formeln durch die entsprechende Markdown-Version in
`{$$}...{/$$}`.

    :%g/\$/ . s/\([^$]\|^\)\$\([^$]\{-1,}\)\$\([^$]\|$\)/\1{$$}\2{\/$$}\3/g
Abgesetzte Formeln stehen in einer `equation`- bzw. `eqnarray`-Umgebung. Das etwas
längliche `\begin{equation}` und Konsorten hatte ich damals durch `\beq` usw.
ersetzt. Die werden jetzt mit

    :%s/\\\(be[aq]\|[\[(]\)/{$$}/
    :%s/\\\(ee[aq]\|[\])]\)/{\/$$}/
durch die Markdown-Entsprechung ersetzt. Vor dem `begin`-Tag muss allerdings ggf.
noch eine Leerzeile eingefügt werden. Ganz blöd ist, dass `eqnarrays` gar nicht
gehen, die müssen zu einzelnen Gleichungen umgestellt werden.

Hervorhebungen mit `\emph` werden in * eingeschlossen:

    :%s/\\emph{\(.\{-\}\)}/*\1*/g
Mit den Literaturverweisen bin ich noch nicht zufrieden. Ich habe Fuß- bzw.
Endnoten probiert, aber erstens sind die Zahlen zu klein und zweitens - was
viel schlimmer ist - man kann nur einmal referenzieren. Wenn man ein zweites
mal auf die gleiche Endnote referenziert, wird kein Link auf die Endnote
erzeugt.
