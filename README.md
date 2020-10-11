# libri-json
JSON formatted Class A Thelemite texts

## Standard Format

```
    title: String
    number: Int - The text's sub figurâ
    subtitle: String (Optional)
    enTitle: String (Optional) - Translated English title
    enSubtitle: String (Optional) - Translated English subtitle
    description: String (Optional) - Brief description of the book
    chapters: Array of Objects
        title: String (Optional)
        number: Int (Optional)
        sections: Array of Objects
            title: String (Optional)
            number: Int (Optional)
            lines: Array of Objects - Note that despite the name, some lines may be multi-line. Blame Crowley
                number: String (Optional) - Some texts are 0-indexed, some do not have line numbers at all
                text: String
                image: String (Optional) - Some lines have reference images
                letter: String (Optional) - Used only in Liber Trigrammaton to represent the correspondence of each trigram
```

## Notes

This format was designed around Liber AL, being the most complex text with chapters and subsections. Consumption of this JSON should assume that the chapter and section arrays may contain only a single object without a title or chapter number.

Whitespace should be observed in the line text - some "lines" are multiple lines, and some of those lines should be indented. Note that this makes the JSON itself horrifyingly unreadable.

Lines may have a "line number" independent of their position in the array - this is because the texts have varying formats between each text and even within some of the texts. The numbers are provided as an independent string rather than included in the text string as they can be valuable data on their own. They are a string not an integer as there is frustratingly one text that has '00' as a line number. Keep that in mind if you convert these numbers to integers. *This is inconsistent with chapter and section numbers, which are integers.* Chapter and section numbers may be rendered as Roman numerals where appropriate.

### 27 - Liber Trigrammaton

This book is formatted slightly different in that it is not an _exact_ reproduction of the original text, but rather a codified version. The line number is given as a trinary (base-3) representation of the trigram's image. With `0` being `.` (Tao), `1` being `---` (Yang), and `2` being `- -` (Yin). This number should be rendered as an image above the accompanying text. The `letter` field is included for easier reference to Liber 777 (except for `222` which has no correspondence).

Line 021 has another trigram embedded in it, this is formatted as `{210}` in the text and should be replaced with the equivalent image.

### Source

* Texts sourced from the OTO USA library: https://lib.oto-usa.org/libri/byclass.html
* English translations of book names: https://www.thelemistas.org/en/MSS/Bjorge/SpiritualExercises/06-holy-books