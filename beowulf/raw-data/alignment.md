
In `aligned.txt` and elsewhere, I make use of **token identifiers** that look like `0003a2`.

These identifiers consist of a four-digit number (padded with inital zeros to ensure exactly four digits) followed by an `a` or `b` followed by a single digit. The four-digit number is the (long) line number of the token in a particular edition; `a` and `b` refer to the on and off half-lines in that long line; and the final digit is the offset of the token within the half-line.

So `0003a2` means the second token in the on half-line of the third line. One might then say that, in the Perseus 1922 Klaeber edition, `0003a2` is `ðā`.

`aligned.txt` attempts to align all the tokens in five electronic editions of Beowulf (not all of which are freely distributable and so neither is `aligned.txt`). The five are referred to here as:

- `mit`
- `mcmaster`
- `heorot`
- `ebeowulf`
- `perseus`

based on the domain name they came from.

A line of `aligned.txt` consists of ten space-separated columns like:

```
0003a2 0003a2 0003a2 0003a2 0003a2 ða ða ðá ða ðā
```

Each line represents a **token alignment**. Sometimes this might map one-to-one to a single token in a particular edition but sometimes zero tokens or more than one as we shall soon see.

The first five columns are the token identifiers for the token alignment in question in each of the five electronic editions. The next five columns indicate, for each edition, the zero or more tokens that make up this particular token alignment.

So the line of `aligned.txt` above says that second token of the on half-line of the third line is `ða` in `mit`, `mcmaster`, `ebeowulf`; `ðá` in `heorot`; and `ðā` in `perseus`.

As one can see, different editions might have different length diacritics but they may also have different capitalisation and punctuation. For example:

```
0001a1 0001a1 0001a1 0001a1 0001a1 Hwæt! Hwæt! Hwæt! HWÆT: Hwæt,
```

It is not required that the token identifier be the same in all editions. For example:

```
0009a2 0009a2 0009a3 0009a3 0009a3 him him him him him
```

Note that, even though each addition has `him` in the on half (`a`) of line nine (`0009`), in `mit` and `mmcmaster` it is token number `2` and in the other three editions it is token number `3`.

This is what line 9 looks like in `mit`:

```
oðþæt him æghwylc     þara ymbsittendra
```

and here is what it looks like in `heorot`:

```
oð þæt him aéghwylc     þára ymbsittendra
```

Notice that the reason `him` is token `3` in `heorot` but token `2` in `mit` is because `oðþæt` is one word in `mit` but two words in `heorot`.

Here is how the half-line is represented in `aligned.txt`:

```
0009a1 0009a1 0009a1 0009a1 0009a1 oðþæt oðþæt oð_þæt oð_þæt oð_þæt
0009a2 0009a2 0009a3 0009a3 0009a3 him him him him him
0009a3 0009a3 0009a4 0009a4 0009a4 æghwylc æghwylc aéghwylc æghwylc ǣghwylc
```

Notice the use of `_` in `oð_þæt` to indicate that, even though the edition has two separate words, it is being aligned as a single unit in this token alignment. Notice also that those texts with the `_` jump from `0009a1` to `0009a3`. Technically there is still a `0009a2`, namely `þæt` but that cannot be aligned to `oðþæt` by itself so appears only as part of `oð_þæt` which starts at `0009a1`. From this file, though, it is possible to extract just the tokens for a single edition, along with their identifiers and, in that case, `þæt` would appear on its own with the identifier `0009a2`.

It is also possible that an edition lacks anything that can be aligned to tokens in the other editions. We need look no further than the off half-line of the same line for an example:

```
0009b1 0009b1 0009b1 0009b1 0009b1 þara þara þára þara @
0009b2 0009b2 0009b2 0009b2 0009b1 ymbsittendra ymbsittendra ymbsittendra ymbsittendra ymbsittendra
```

Line 9 in `perseus` reads as follows:

```
oð þæt him ǣghwylc     ymbsittendra
```

Compare this with the `mit` and `heorot` examples earlier. There is no `þara` in the `perseus` text and so nothing can be aligned to it. The `@` indicates this. Notice that we still show `0009b1` as the identifier but that the very next alignment is also `0009b1` for `perseus`.

`0009b1` is `ymbsittendra` in `perseus` but `þara` (or `þára`) in the other four. `ymbsittendra` is `0009b2` in those editions.

Note that again it is possible to fully reconstruct the text of any edition from the two relevant columns in `aligned.txt`. Any `_` need to be converted to spaces, `@` needs to be ignored, and the change in the identifier indicates when a caesura or line break occurs in that edition.

Editions may differ in where they put the caesura. For example, most of the editions have:

```
se þe him bealwa to     bote gelyfde,
```

whereas `heorot` and `ebeowulf` have:

```
se þe him bealwa     to bote gelyfde,
```

Here is `aligned.txt` for this:

```
0909a1 0909a1 0909a1 0908a1 0909a1 se se sé se sē
0909a2 0909a2 0909a2 0908a2 0909a2 þe þe þe þe þe
0909a3 0909a3 0909a3 0908a3 0909a3 him him him him him
0909a4 0909a4 0909a4 0908a4 0909a4 bealwa bealwa bealwa bealwa bealwa
0909a5 0909a5 0909b1 0908b1 0909a5 to to tó to tō
0909b1 0909b1 0909b2 0908b2 0909b1 bote bote bóte bote bōte
0909b2 0909b2 0909b3 0908b3 0909b2 gelyfde, gelyfde, gelýfde gelyfde, gelȳfde,
```

(Note also that here `ebeowulf` is off by one in its line-numbering. The reason will be seen shortly.)

Editions may also differ in where they put the line break:

```
0515b1 0515b1 0515b1 0514b1 0515b1 geofon geofon geofon Geofon geofon
0515b2 0515b2 0515b2 0514b2 0515b2 yþum yþum ýþum yþum ȳpum
0515b3 0515b3 0516a1 0514b3 0515b3 weol, weol, wéol weol wēol,
```

where `heorot` puts `wéol` on a new line (at the start of `0516a`) rather than the end of `0515b` like the other editions.

In a more complicated example, lines 389 and 390 of `mit` are:

```
389 Deniga leodum."
390      word inne abead:
391 "Eow het secgan     sigedrihten min,
```

and the corresponding lines of `ebeowulf` are:

```
389 Deniga leodum."     Word inne abead:
390 "Eow het secgan,     sigedrihten min,
```

Notice that the `mit` edition lacks the off half-line on line 389 and the on half-line in line 390. `ebeowulf`. on the other hand, continues straight on which means that line numbers are off-by-one from this point on (until the next case of different line breaks).

Before we look at how `aligned.txt` models this, let's look at what `perseus` has:

```
389 Deniga lēodum.'     [þā wið duru healle
390 Wulfgār ēode,]     word inne ābēad:
391 'ēow hēt secgan     sigedrihten mīn,
```

Notice that the "missing" half-lines have been filled in.

This is what `aligned.txt` has for all this:

```
0389a1 0389a1 0389a1 0389a1 0389a1 Deniga Deniga Deniga Deniga Deniga
0389a2 0389a2 0389a2 0389a2 0389a2 leodum." leodum." léodum.' leodum." lēodum.'
0389b1 0389b1 0389b1 0389b1 0389b1 @ @ @ @ [þā
0389b1 0389b1 0389b1 0389b1 0389b2 @ @ @ @ wið
0389b1 0389b1 0389b1 0389b1 0389b3 @ @ @ @ duru
0389b1 0389b1 0389b1 0389b1 0389b4 @ @ @ @ healle
0390a1 0390a1 0390a1 0389b1 0390a1 @ @ @ @ Wulfgār
0390a1 0390a1 0390a1 0389b1 0390a2 @ @ @ @ ēode,]
0390b1 0390b1 0390b1 0389b1 0390b1 word word Word Word word
0390b2 0390b2 0390b2 0389b2 0390b2 inne inne inne inne inne
0390b3 0390b3 0390b3 0389b3 0390b3 abead: abead: ábéad: abead: ābēad:
0391a1 0391a1 0391a1 0390a1 0391a1 "Eow "Eow 'Éow "Eow 'ēow
0391a2 0391a2 0391a2 0390a2 0391a2 het het hét het hēt
0391a3 0391a3 0391a3 0390a3 0391a3 secgan secgan secgan secgan, secgan
0391b1 0391b1 0391b1 0390b1 0391b1 sigedrihten sigedrihten sigedrihten sigedrihten sigedrihten
0391b2 0391b2 0391b2 0390b2 0391b2 min, min, mín min, mīn,
```

While this may look complicated, you can follow it through and see that it correct captures all the tokens in each individual edition and aligns those common across editions.

There are some cases where different editions will split a word differently, `mægen Hreðmanna.` versus `mægenhreð manna.`. Hence:

```
0445a1 0445a1 0445a1 0444a1 0445a1 mægen_Hreðmanna. mægen_Hreðmanna. mægenhréð_manna. mægenhreð_manna. mægenhrēð_manna.
```

Or `oþðe_nipende` versus `oþ_ðe_nipende` versus `oþðenīpende`:

```
0649a1 0649a1 0649a1 0648a1 0649a1 oþðe_nipende oþðe_nipende oþðe_nípende oþ_ðe_nipende oþðenīpende
```

In some cases word order is flipped:

```
1328b2 1328b2 1328b2 1330b2 1328b2 scolde_eorl scolde_eorl eorl_scolde eorl_scolde scolde_eorl
```

Having this aligned file allows us to very easily compare how the same word is normalised differently in different editions, or how the editors have filled in illegible portions differently, or where they've chosen line breaks differently.
