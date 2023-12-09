# Japanese Resources

Japanese resources organized in a developer-friendly way.

## Repository structure

- `/bin` - Binaries that generate output in `/output`
- `/data` - Resources that are a part of input data, but are not available as a repository that can be added as a submodule
- `/output` - Generated output files with resources
- `/src` - Source code for binary files
- `/submodules` - Git datasets that are used to generate files in `/output`

## Data structure

### Kanji List

- `output/kanji/kanji_en.db`
- `output/kanji/kanji_pl.db`

Each file is a SQLite database with the following structure:

| Column name     | Type      | Comments                                                                                                                                                                         |
| --------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `character`     | `TEXT`    | Single kanji character                                                                                                                                                           |
| `kunyomi`       | `TEXT`    | Japanese readings from the jōyō kanji list                                                                                                                                       |
| `onyomi`        | `TEXT`    | Sino-Japanese readings from the jōyō kanji list                                                                                                                                  |
| `other_kunyomi` | `TEXT`    | Japanese readings from the jōyō kanji list                                                                                                                                       |
| `other_onyomi`  | `TEXT`    | Sino-Japanese readings from the jōyō kanji list                                                                                                                                  |
| `jlpt`          | `INTEGER` | Value between 0 and 5. Zero indicates that this character is not a part of the Japanese-Language Proficiency Test, other values indicate the level (e.g. number `3` is JLPT N3). |
| `translations`  | `TEXT`    | Meanings of this character                                                                                                                                                       |

Notes:

- All readings use the [Katakana Middle Dot](https://www.compart.com/en/unicode/U+30FB) (`U+30FB`) to separate [okurigana](https://en.wikipedia.org/wiki/Okurigana) in [kun'yomi](<https://en.wikipedia.org/wiki/Kanji#Kun'yomi_(native_reading)>) readings. Despite being called "Katakana Middle Dot" by the Unicode Consortium, it's actually the standard full-width middle dot ([中黒](https://ja.wikipedia.org/wiki/中黒#日本語)) which is used in the Japanese language in general, and not only in case of katakana.
- All readings and translations are separated using the [Information Separator One (US)](https://www.compart.com/en/unicode/U+001F) character (`U+001F`). It's a delimited commonly used for [dividing plain-text data items](https://en.wikipedia.org/wiki/C0_and_C1_control_codes#Field_separators).
- `kunyomi` and `onyomi` columns contain only readings that are officially recognised in the [jōyō kanji](https://en.wikipedia.org/wiki/Jōyō_kanji) list. Characters that are not on the jōyō kanji list have only `other_kunyomi` and `other_onyomi` data provided.

### Sources & Licenses

- Kanji List
  - (Polish) [JaponskiSlownik by dedyk](https://github.com/dedyk/JaponskiSlownik) under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/deed.en)
  - Tamaoka, K., Makioka, S., Sanders, S. & Verdonschot, R.G. (2017). [www.kanjidatabase.com](https://www.kanjidatabase.com): A new interactive online database for psychological and linguistic research on Japanese kanji and their compound words. Psychological Research. 81, 696-708.
