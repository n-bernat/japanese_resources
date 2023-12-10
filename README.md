# Japanese Resources

Japanese resources organized in a developer-friendly way.

## Repository structure

- `/data` - Resources that are a part of input data, but are not available as a repository that can be added as a submodule.
- `/output` - Generated output files with resources.
- `/src` - Source code for output generators.
- `/submodules` - Git datasets that are used to generate files in `/output`.

## Data structure

### Kanji List

- `output/kanji_list/kanji_en.db`
- `output/kanji_list/kanji_pl.db`

Each file is a SQLite database with the following structure:

| Column name       | Type      | Comments                                                                                                                                                                                                                                                                                                                  |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `character`       | `TEXT`    | Single kanji character ([Primary key](https://en.wikipedia.org/wiki/Primary_key)).                                                                                                                                                                                                                                        |
| `kunyomi`         | `TEXT`    | Japanese readings from the jōyō kanji list. Written in hiragana.                                                                                                                                                                                                                                                          |
| `onyomi`          | `TEXT`    | Sino-Japanese readings from the jōyō kanji list. Written in katakana.                                                                                                                                                                                                                                                     |
| `other_kunyomi`   | `TEXT`    | Japanese readings that are not on the jōyō kanji list. Written in hiragana.                                                                                                                                                                                                                                               |
| `other_onyomi`    | `TEXT`    | Sino-Japanese readings that are not on the jōyō kanji list. Written in katakana.                                                                                                                                                                                                                                          |
| `nanori`          | `TEXT`    | Readings found only in names. Written in hiragana.                                                                                                                                                                                                                                                                        |
| `translations`    | `TEXT`    | Translations of this character in a particular language (e.g. in Polish for `kanji_pl.db`).                                                                                                                                                                                                                               |
| `translations_en` | `TEXT`    | Fallback translations in English. For easier parsing in case of English it's present, but empty.                                                                                                                                                                                                                          |
| `grade`           | `INTEGER` | The "grade" of the kanji. See [KANJIDIC's documentation](http://www.edrdg.org/wiki/index.php/KANJIDIC_Project#Content_&_Format) for mode details.                                                                                                                                                                         |
| `jlpt`            | `INTEGER` | The pre-2010 level of the Japanese Language Proficiency Test (JLPT) in which the kanji occurs ([source](http://www.edrdg.org/wiki/index.php/KANJIDIC_Project)). Zero indicates that this character is not a part of the Japanese-Language Proficiency Test, other values indicate the level (e.g. number `1` is JLPT N1). |
| `strokes`         | `INTEGER` | The number of strokes.                                                                                                                                                                                                                                                                                                    |

Notes:

- All readings use the [Katakana Middle Dot](https://www.compart.com/en/unicode/U+30FB) (`U+30FB`) to separate [okurigana](https://en.wikipedia.org/wiki/Okurigana) in [kun'yomi](<https://en.wikipedia.org/wiki/Kanji#Kun'yomi_(native_reading)>) readings. Despite being called "Katakana Middle Dot" by the Unicode Consortium, it's actually the standard full-width middle dot ([中黒](https://ja.wikipedia.org/wiki/中黒#日本語)) which is used in the Japanese language in general, and not only in case of katakana.
- All readings and translations are separated using the [Information Separator One (US)](https://www.compart.com/en/unicode/U+001F) character (`U+001F`). It's a delimited commonly used for [dividing plain-text data items](https://en.wikipedia.org/wiki/C0_and_C1_control_codes#Field_separators).
- `kunyomi` and `onyomi` columns contain only readings that are officially recognised in the [jōyō kanji](https://en.wikipedia.org/wiki/Jōyō_kanji) list. Characters that are not on the jōyō kanji list have only `other_kunyomi` and `other_onyomi` data provided.

### Sources & Licenses

- Kanji List
  - [常用漢字表](https://www.bunka.go.jp/kokugo_nihongo/sisaku/joho/joho/kijun/naikaku/kanji/joyokanjisakuin/index.html)
    - from Agency for Cultural Affairs (bunka.go.jp)
    - Exported to `data/jouyou_kanji.csv` in [Numbers](<https://en.wikipedia.org/wiki/Numbers_(spreadsheet)>) on December 9, 2023
  - [KANJIDIC2](http://www.edrdg.org/wiki/index.php/KANJIDIC_Project) by [Electronic Dictionary Research and Development Group](http://www.edrdg.org) under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0)
  - (Polish-only) [JaponskiSlownik](https://github.com/dedyk/JaponskiSlownik) by [dedyk](https://github.com/dedyk) under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0)
