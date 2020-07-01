---

copyright:
  years: 2015, 2020
lastupdated: "2020-05-14"

subcollection: text-to-speech

---

{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}
{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Using phonetic symbols
{: #sprs}

The {{site.data.keyword.texttospeechfull}} service supports both the standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM}} Symbolic Phonetic Representation (SPR) notations to represent the sounds of words. Both notations provide phonetic coding that represents the pronunciation of a word, the sounds that make up the word, how the sounds are divided into syllables, and which syllables are stressed. [Language support for SPR and IPA](#supportedLanguages) provides links to pages that document the allowable phonetic symbols for each language.
{: shortdesc}

## Defining a word pronunciation
{: #define-pronunciation}

To define the phonetic pronunciation for a word, either within input text or for a custom voice model, you use the `<phoneme>` element of the Speech Synthesis Markup Language (SSML) or equivalent method parameters. The `<phoneme>` element has two attributes:

-   The `alphabet` attribute specifies the notation of the pronunciation. Use the value `ibm` to indicate that the pronunciation is defined in SPR. Use the value `ipa` to indicate that the pronunciation is defined in IPA.
-   The `ph` attribute defines the pronunciation. It consists of a sequence of allowable symbols for a given language. The symbols define how the word that is enclosed in the `<phoneme>` element is to be pronounced.

Follow these rules when you define a pronunciation:

-   Use only the documented SPR or IPA symbols. The service considers invalid any definition that contains phonetic symbols that are not allowed in a language. An SPR or IPA entry that does not conform to the required specification is invalid.
-   When multiple IPA symbols (or symbol combinations) are documented for an SPR symbol, all of the IPA symbols are equivalent to the single SPR symbol. The service treats all of these IPA symbols the same and does not realize the subtle or regional differences that IPA is meant to describe.

For more information, see

-   [The phoneme element](/docs/text-to-speech?topic=text-to-speech-elements#phoneme_element)
-   [Rules for creating custom entries](/docs/text-to-speech?topic=text-to-speech-rules)
-   [Creating and managing custom entries](/docs/text-to-speech?topic=text-to-speech-customWords)

## Working with IBM SPR
{: #intro-SPRs}

IBM SPR is an alternative representation to standard IPA. Here are examples of valid SPR notations for the words *through* and *shocking* in US English:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

In the definitions, the letters represent specific sounds of US English speech. A `.` (period) signals the beginning of a new syllable, and the digits `1` and `0` indicate syllable stress. For more information, see [Specifying syllables](#syllables).

### Speech sound symbols
{: #intro-SPRs-symbols}

Each language uses its own inventory of SPR symbols to represent the speech sounds of that language. The following rules apply to specifying an SPR symbol:

-   Letters are case-sensitive, so `e` and `E`, for example, represent two different sounds.
-   Two- and three-character symbols must be contained in single quotes. For example, the symbol `aj` in the German word *heim* is specified as `"h'aj'm"`.

Also consider the following when defining a word's pronunciation in SPR format:

-   The sounds of every language have specific distributional patterns within that language. For example, in all dialects of English, the sound `G` in *sing* (`".1sIG"`) does not occur at the beginning of a word. Other US English sounds that have a particularly narrow distribution are the glottal stop (`?`), the flap (`F`), and the syllabic nasal (`N`). If you enter a sound symbol in a context in which it does not normally occur, the resulting speech might sound unnatural.
-   The service applies a sophisticated set of linguistic rules to its input to reflect the processes by which sounds change in specific contexts in natural language. For example, in US English, the sound `t` of the word *write* (`".1r1Yt"`) is pronounced as a flap (`F`) in *writer* (`".1rY.0FR"`). SPR input undergoes these modifications just as ordinary input text does. In this example, whether you enter `".1rY.0tR"` or `".1rY.0FR"` does not affect the speech that is generated.

## Working with IPA
{: #intro-ipa}

You can define IPA pronunciations by using phonetic symbols or Unicode values. The following are examples of valid IPA notations for the word *tomato* in phonetic symbols and Unicode:

<pre><code>&lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
&lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;</code></pre>

IPA is an industry standard notation. For more information, see the following pages:

-   For more information about IPA, see [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.
-   For more information about phonetic symbols for Unicode, see [Phonetic symbols in Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}.

## Specifying syllables
{: #syllables}

You can specify syllable boundaries and stress in both SPR and IPA.

### Syllable boundaries
{: #syllables-boundaries}

You can use a `.` (period) to mark the beginning of each syllable. However, to preserve the valid phonetics of a language, the service can elect not to honor periods in some cases (for example, if a syllable boundary is placed at an illegal or unnatural position for a language). In general, in cases where the user can indicate a valid preference for a syllable boundary or other aspect of a word's pronunciation, the service honors such requests.

### Syllable stress
{: #syllables-stress}

Table 1 identifies the symbols that you can use to indicate syllable stress for a pronunciation. {{site.data.keyword.IBM_notm}} recommends that you indicate primary stress for pronunciations in either SPR or IPA. However, indicating syllable stress is optional for both formats; the service determines where stress occurs if you do not indicate it.

<table style="width:80%">
  <caption>Table 1. Syllable stress</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      SPR symbol
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Meaning
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <code>&#712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      Primary stress
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      <code>&#716;</code>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      Secondary stress
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">No symbol</td>
    <td style="text-align:center">No value</td>
    <td>
      No stress
    </td>
  </tr>
</table>

You must place a syllable stress marker within a syllable boundary but always to the left of the syllable's vowel. You can place a marker anywhere to the left of the stressed vowel. For example, each of the following SPR examples places the primary stress on the correct vowel of the word *construction*:

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

### Language-specific rules for using syllable stress
{: #syllables-languages}

Table 2 lists language-specific considerations that apply to specifying syllable stress. Unless the table qualifies the rules for a language, you can use the syllable stress symbols described in the previous section.

<table style="width:90%">
  <caption>Table 2. Language-specific rules for using syllable stress</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Language
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Notation
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Language-specific rules
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      Arabic
    </td>
    <td style="text-align:center">
      IPA
    </td>
    <td>
      The secondary stress symbol is ignored, but including the symbol
      may produce undesired results.
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      French
    </td>
    <td style="text-align:center">
      SPR
    </td>
    <td>
      All syllable stress symbols are honored. But syllable stress must
      immediately precede the vowel of the syllable. Syllable stress for
      French is much stricter than for other languages. An error occurs
      if you place the stress symbol in an invalid location.
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      French
    </td>
    <td style="text-align:center">
      IPA
    </td>
    <td>
      All syllable stress symbols are ignored.
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Italian
    </td>
    <td style="text-align:center">
      SPR
    </td>
    <td>
      You can specify only `1` (primary stress). An error occurs if you
      specify secondary or no stress.
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Japanese
    </td>
    <td style="text-align:center">
      SPR
    </td>
    <td>
      You can specify only `1` (primary stress) and `0` (no stress). An
      error occurs if you specify secondary stress.
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Korean
    </td>
    <td style="text-align:center">
      IPA
    </td>
    <td>
      All syllable stress symbols are ignored, but including the symbols
      may produce undesired results.
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Spanish
    </td>
    <td style="text-align:center">
      SPR
    </td>
    <td>
      You can specify only `1` (primary stress). An error occurs if you
      specify secondary or no stress.
    </td>
  </tr>
</table>

## Language support for SPR and IPA
{: #supportedLanguages}
{: help}
{: support}

Table 3 shows the service's language support for SPR and IPA symbols. The table provides links to pages that document the supported SPR symbols, IPA symbols, and equivalent IPA Unicode values that can be used with all voices for each language. The pages provide examples of each symbol in words from the language. Because of dialectal differences, the examples might not always match your pronunciation.

<table style="width:80%">
  <caption>Table 3. Language support for phonetic symbols</caption>
  <tr>
    <th width="50" style="text-align:left">Language</th>
    <th width="25%" style="text-align:center">Supports SPR</th>
    <th width="25%" style="text-align:center">Supports IPA</th>
  </tr>
  <tr>
    <td style="text-align:left">[Arabic symbols](/docs/text-to-speech?topic=text-to-speech-arSymbols)</th>
    <td style="text-align:center">No</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[Brazilian Portuguese symbols](/docs/text-to-speech?topic=text-to-speech-ptSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[Chinese (Mandarin) symbols](/docs/text-to-speech?topic=text-to-speech-zhSymbols)</th>
    <td style="text-align:center">No</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[Dutch symbols](/docs/text-to-speech?topic=text-to-speech-nlSymbols)</th>
    <td style="text-align:center">No</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[English (United Kingdom) symbols](/docs/text-to-speech?topic=text-to-speech-gbSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[English (United States) symbols](/docs/text-to-speech?topic=text-to-speech-usSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[French symbols](/docs/text-to-speech?topic=text-to-speech-frSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[German symbols](/docs/text-to-speech?topic=text-to-speech-deSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[Italian symbols](/docs/text-to-speech?topic=text-to-speech-itSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[Japanese symbols](/docs/text-to-speech?topic=text-to-speech-jaSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[Korean symbols](/docs/text-to-speech?topic=text-to-speech-koSymbols)</th>
    <td style="text-align:center">No</th>
    <td style="text-align:center">Yes</th>
  </tr>
  <tr>
    <td style="text-align:left">[Spanish symbols](/docs/text-to-speech?topic=text-to-speech-esSymbols)</th>
    <td style="text-align:center">Yes</th>
    <td style="text-align:center">Yes</th>
  </tr>
</table>

Use of the Speech Synthesis Markup Language (SSML) `<phoneme>` element and International Phonetic Alphabet (IPA) symbols or Unicode values with the Arabic voice `ar-AR_OmarVoice` is not currently supported. For more information, see [Known limitations](/docs/text-to-speech?topic=text-to-speech-release-notes#limitations).
{: important}