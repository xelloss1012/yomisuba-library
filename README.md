# Yomisuba library

Free Japanese books, in the public domain or under a Creative Commons licence, that [Yomisuba](https://github.com/xelloss1012/yomisuba) (読みの素晴らしい世界に祝福を！), an EPUB reader for vertical Japanese, lists in its **free library** screen. The reader downloads a book only when its user chooses it, straight from this repository.

| File | What it is |
|---|---|
| `catalog.json` | The list the app reads: title, author, genres, descriptions (Japanese, Spanish, English), size, estimated difficulty, source, licence and a SHA-256 checksum per book |
| `books/*.epub` | The books, ready to read, with furigana and the edition credits on the last page |
| `covers/*.png` | Covers (the source texts have none), drawn by the build script |
| `sources.json` | The curated list the catalog is built from |
| [`ATTRIBUTION.md`](ATTRIBUTION.md) | Credits for every book: source edition and the volunteers who typed and proofread it |

## Licences

- **Public-domain works.** They come from [Aozora Bunko (青空文庫)](https://www.aozora.gr.jp/), the volunteer digital library. Only authors who **died in 1945 or earlier** are included: their copyright has expired in Japan, the United States, the European Union and Spain. A few countries have longer terms (Mexico, for one), so check yours before redistributing.
- **Creative Commons works.** Modern translations of classics (the originals are in the public domain, so the licence covers the translation) and works by contemporary authors, which their rights holders published on Aozora Bunko under **CC BY** or **CC BY-SA**. Those licences allow copying, adapting and redistributing with credit (BY-SA under the same licence). The licence, the credit and a note of what changed (a cover, a title page and a colophon were added; the text is unchanged, and illustrations over 1 MB are left out) are on the last page of each EPUB and in [`ATTRIBUTION.md`](ATTRIBUTION.md). Works under NonCommercial (NC) or NoDerivatives (ND) terms are not included.
- **The catalog, the descriptions and the covers** are dedicated to the public domain under [CC0 1.0](LICENSE).

Aozora Bunko asks that the source edition and the names of the typists and proofreaders be kept; every EPUB includes them and [`ATTRIBUTION.md`](ATTRIBUTION.md) lists them.

## Difficulty

Each book has a difficulty from 1 (most accessible) to 5 (hardest). It is an **estimate**, not an official level: the text is split into words and the share that is JLPT N2 or easier (the JLPT and frequency lists the app ships) is measured over fixed-size windows, so a long novel is not rated harder than a short story. Aozora's literature is never beginner material, so the scale only orders these books among themselves. The `characters` figure is exact; `pages` is `characters / 600`, the size of a paperback page, because an EPUB has no fixed pages.

## Adding or rebuilding books

The files are generated with the scripts of the app repository (needs Node 22+ and Google Chrome or Edge to draw the covers):

```sh
# in the yomisuba repository, with this repository cloned next to it
node scripts/build-library.mjs ../yomisuba-library          # every book in sources.json
node scripts/build-library.mjs ../yomisuba-library botchan  # just one
node scripts/check-library.mjs ../yomisuba-library          # validates the result
```

To add a book, append an entry to `sources.json` (the Aozora work id, its genres and a short description in `ja`, `es` and `en`) and run the build. It reads the rights from Aozora's catalogue and from the file itself, and refuses a work unless either everyone credited died by 1945 and the copyright flags are clear, or the file states a CC BY / CC BY-SA licence (and, for a translation, its original author died by 1945). Genres: `fantasy`, `scifi`, `mystery`, `horror`, `romance`, `historical`, `humor`, `drama`, `children`, `nonfiction`.

Works on commercial web-novel sites (Shōsetsuka ni Narō, Kakuyomu and the like) are not here: their authors keep the copyright and the sites grant readers no licence to redistribute. A work from such a site can only be added if its author states a CC BY (or CC0) licence for it.
