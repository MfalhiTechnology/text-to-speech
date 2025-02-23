---

copyright:
  years: 2015, 2021
lastupdated: "2021-04-29"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:beta: .beta}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Release notes
{: #release-notes}

The following sections document the new features and changes that were included for each release and update of the {{site.data.keyword.texttospeechfull}} service. The information includes any known limitations. Unless otherwise noted, all changes are compatible with earlier releases and are automatically and transparently available to all new and existing applications.
{: shortdesc}

## Known limitations
{: #limitations}

The service has the following known limitations:

-   When you specify the `audio/ogg;codecs=opus` audio format, you can optionally specify a sampling rate other than the default 48,000 Hz. However, although the service accepts `48000`, `24000`, `16000`, `12000`, or `8000` as a valid sampling rate, it currently disregards a specified value and always returns the audio with a sampling rate of 48 kHz.
-   Cross-Origin Resource Sharing (CORS) support is not available from the Mozilla Firefox&trade; browser for voices in the following languages: Arabic, Australian English, Chinese, Dutch, and Korean.

## 12 April 2021
{: #April2021}

### New Canadian French voice
{: #April2021-new-voice}

The service now supports Canadian French with the enhanced neural voice `fr-CA_LouiseV3Voice`. The Canadian French voice supports customization and is generally available (GA) for production use.

-   To hear a sample of the new voice, see [Supported language and voice](/docs/text-to-speech?topic=text-to-speech-voices#languageVoices).
-   For more information about the phonetic symbols and Unicode values that are available for the Canadian French language, see [French (Canadian) symbols](/docs/text-to-speech?topic=text-to-speech-frCaSymbols).

### New Tune by Example feature
{: #April2021-tbe}

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

The new Tune by Example feature lets you control how specified text is spoken by the service. The feature has two components:

-   *Custom prompts* include the written text that is to be spoken and recorded audio that speaks the text as you want to hear it. The audio specifies the intonation, cadence, and stress of the synthesized text. The prompt can emphasize different syllables or words, introduce pauses, and generally make the synthesized audio sound more natural and appropriate for its context.
-   *Speaker models* provide enrollment audio for a user who speaks one or more prompts. A speaker model provides an audio sample of a user's voice. The service trains itself on the voice, which can help it to produce higher-quality prompts for that speaker.

You specify a custom prompt with a speech synthesis request to indicate how the service's voice is to pronounce the text. To specify a prompt, you use the SSML extension `<ibm:prompt id="{prompt_id}"/>`. The synthesized audio duplicates the prosody of the prompt.

For more information about using the Tune by Example feature, see the following topics:

-   [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro)
-   [Rules for creating custom prompts and speaker models](/docs/text-to-speech?topic=text-to-speech-tbe-rules)
-   [Creating a custom prompt](/docs/text-to-speech?topic=text-to-speech-tbe-create)
-   [Using a custom prompt](/docs/text-to-speech?topic=text-to-speech-tbe-use)
-   [Managing custom prompts](/docs/text-to-speech?topic=text-to-speech-tbe-custom-prompts)
-   [Managing speaker models](/docs/text-to-speech?topic=text-to-speech-tbe-speaker-models)

The service includes eight new methods for working with the Tune by Example feature. The descriptions of the new methods that follow provide links to their entries in the API & SDK reference. You might need to select the `Curl` tab of the reference to see the new methods.

-   The service includes four methods for working with custom prompts:

    -   [Add a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#addcustomprompt){: external}: `POST /v1/customizations/{customization_id}/prompts/{prompt_id}`
    -   [List custom prompts](https://{DomainName}/apidocs/text-to-speech/text-to-speech#listcustomprompts){: external}: `GET /v1/customizations/{customization_id}/prompts`
    -   [Get a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#getcustomprompt){: external}: `GET /v1/customizations/{customization_id}/prompts/{prompt_id}`
    -   [Delete a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#deletecustomprompt){: external}: `DELETE /v1/customizations/{customization_id}/prompts/{prompt_id}`

-   The service includes four methods for working with speaker models:

    -   [Create a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#createspeakermodel){: external}: `POST /v1/speakers`
    -   [List speaker models](https://{DomainName}/apidocs/text-to-speech/text-to-speech#listspeakermodels){: external}: `GET /v1/speakers`
    -   [Get a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#getspeakermodel){: external}: `GET /v1/speakers/{speaker_id}`
    -   [Delete a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#deletespeakermodel){: external}: `DELETE /v1/speakers/{speaker_id}`

Activity Tracker actions are available for all new Tune by Example events. For more information, see [Tune by Example events](/docs/text-to-speech?topic=text-to-speech-at-events#at-events-tbe).

### Updates to Activity Tracker actions for customization
{: #April2021-at-updates}

The names of the actions for the Activity Tracker events for the customization methods have changed. The actions now include the string `custom-model` instead of `custom-voice`. The old names of the actions are deprecated. The old names are still available for use but will be removed at a future date. Migrate to the new names that are listed in [Customization events](/docs/text-to-speech?topic=text-to-speech-at-events#at-events-custom) at your earliest convenience.

#### Create events
{: #April2021-at-updates-create}

| Deprecated action name | New action name |
|------------------------|-----------------|
| `text-to-speech.custom-voice.create` | `text-to-speech.custom-model.create` |
| `text-to-speech.custom-voice-word-list.create` | `text-to-speech.custom-model-word-list.create` |
| `text-to-speech.custom-voice-word.create` | `text-to-speech.custom-model-word.create` |
{: caption="Table 1. Names of actions for create events"}

#### Read events
{: #April2021-at-updates-read}

| Deprecated action name | New action name |
|------------------------|-----------------|
| `text-to-speech.custom-voice-list.read` | `text-to-speech.custom-model-list.read` |
| `text-to-speech.custom-voice.read` | `text-to-speech.custom-model.read` |
| `text-to-speech.custom-voice-word-list.read` | `text-to-speech.custom-model-word-list.read` |
| `text-to-speech.custom-voice-word.read` | `text-to-speech.custom-model-word.read` |
{: caption="Table 2. Names of actions for read events"}

#### Update event
{: #April2021-at-updates-update}

| Deprecated action name | New action name |
|------------------------|-----------------|
| `text-to-speech.custom-voice.update` | `text-to-speech.custom-model.update` |
{: caption="Table 3. Names of actions for update event"}

#### Delete events
{: #April2021-at-updates-delete}

| Deprecated action name | New action name |
|------------------------|-----------------|
| `text-to-speech.custom-voice.delete` | `text-to-speech.custom-model.delete` |
| `text-to-speech.custom-voice-word.delete` | `text-top-speech.custom-model-word.delete` |
{: caption="Table 4. Names of actions for delete events"}

## 2 December 2020
{: #December2020}

The voices offered by the service have undergone significant change. The service supports new languages and voices, has improved the quality of many voices, and has deprecated many older voices. In addition, all of the service's voices are now customizable and generally available (GA) for production use.

### Neural and enhanced neural voices
{: #December2020-neural-voices}

To optimize the overall quality of voice synthesis, all available voices are now based on neural technology. The service offers two types of voices that are based on neural technology:

-   *Neural voices*, which do *not* include the string `V3` in their names, are now available for Arabic, Australian English, Chinese, Dutch, and Korean. Neural voices support the use of the International Phonetic Alphabet (IPA) with the Speech Synthesis Markup Language (SSML) `<phoneme>` element.
-   *Enhanced neural voices*, which include the string `V3` in their names, are now available for Brazilian Portuguese, United Kingdom and United States English, French, German, Italian, Japanese, and Spanish (all dialects). Enhanced neural voices support the use of both IPA and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) with the SSML `<phoneme>` element. Enhanced neural voices also achieve a slightly higher degree of natural-sounding speech. And further customization capabilities will be exposed for enhanced neural voices in the coming months.

The service no longer offers standard voices for any language. Standard voices used concatenative synthesis to assemble segments of recorded speech to generate the requested audio. For more information, see

-   [Supported languages and voices](/docs/text-to-speech?topic=text-to-speech-voices#languageVoices)
-   [Neural voice technology](/docs/text-to-speech?topic=text-to-speech-voices#neuralVoices)

### New voices
{: #December2020-new-voices}

The following voices are new:

-   The service now supports Australian English with the following two neural voices: `en-AU_CraigVoice` and `en-AU_MadisonVoice`. For about the IPA symbols and Unicode values that are now available for the Australian language, see [English (Australian) symbols](/docs/text-to-speech?topic=text-to-speech-auSymbols).
-   The service now supports two new Korean neural voices: `ko-KR_HyunjunVoice` and `ko-KR_SiWooVoice`. For information about the IPA symbols and Unicode values for the Korean language, see [Korean symbols](/docs/text-to-speech?topic=text-to-speech-koSymbols).

### Improved voices
{: #December2020-improved-voices}

The voices for the existing Arabic, Chinese, Dutch, and Korean languages, all of which were concatenative, are now neural:

-   `ar-MS_OmarVoice`
-   `ko-KR_YoungmiVoice`
-   `ko-KR_YunaVoice`
-   `nl-NL_EmmaVoice`
-   `nl-NL_LiamVoice`
-   `zh-CN_LiNaVoice`
-   `zh-CN_WangWeiVoice`
-   `zh-CN_ZhangJingVoice`

The following additional changes have also been made:

-   The Arabic voice is now named `ar-MS_OmarVoice`. The former name, `ar-AR_OmarVoice`, is deprecated. It will continue to function for at least one year but might be removed at a future date. You are encouraged to migrate to the new name at your earliest convenience.
-   The Arabic language now supports the use of IPA symbols and Unicode values with the SSML `<phoneme>` element. To create a custom model for Arabic, you must use the language identifier `ar-MS`. The identifier `ar-AR` is not supported for customization.
-   The IPA symbols for the Arabic language are new. The previously documented symbols have been completely replaced. For more information about the supported IPA symbols and Unicode values, see [Arabic symbols](/docs/text-to-speech?topic=text-to-speech-arSymbols).
-   The IPA symbols for the Dutch language have been changed as follows:
    -   Dutch no longer supports the following IPA symbols: <code>&#116;&#690;</code> (`0074+02B2`), <code>&#626;</code> (`0272`), <code>&#678;</code> (`02A6`), and <code>&#660;</code> (`0294`).
    -   Dutch now supports the following IPA symbol: <code>&#611;</code> (`0263`).

    For more information about the supported IPA symbols and Unicode values, see [Dutch symbols](/docs/text-to-speech?topic=text-to-speech-nlSymbols).
-   Cross-Origin Resource Sharing (CORS) support is now available for all voices from the Google Chrome&trade; and Apple&reg; Safari browsers. It is *not* available from the Mozilla Firefox&trade; browser for voices in the following languages: Arabic, Australian English, Chinese, Dutch, and Korean. For more information, see [Leveraging CORS support](/docs/text-to-speech?topic=text-to-speech-service-features#features-cors).

### Deprecated voices
{: #December2020-deprecated-voices}

The following standard concatenative voices are now deprecated:

-   `de-DE_BirgitVoice`
-   `de-DE_DieterVoice`
-   `en-GB_KateVoice`
-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`
-   `es-ES_EnriqueVoice`
-   `es-ES_LauraVoice`
-   `es-LA_SofiaVoice`
-   `es-US_SofiaVoice`
-   `fr-FR_ReneeVoice`
-   `it-IT_FrancescaVoice`
-   `ja-JP_EmiVoice`
-   `pt-BR_IsabelaVoice`

All of the standard voices that have been deprecated have equivalent neural counterparts, so no voice is being taken away. Rather, you can change to the equivalent neural version of the voice (for example, from `de-DE_BirgitVoice` to `de-DE_BirgitV3Voice`) for better speech-synthesis results.

These deprecated voices are removed from the published documentation. They will continue to function for at least one year but might be removed at a future date. You are encouraged to migrate to the equivalent neural voices at your earliest convenience. For more information about moving from a deprecated standard voice to a neural voice, see [Migrating from standard to neural voices](/docs/text-to-speech?topic=text-to-speech-voices#migrateVoice).

If you omit the optional `voice` parameter from a speech synthesis request, the service uses `en-US_MichaelV3Voice` by default. This neural voice replaces the now-deprecated `en-US_MichaelVoice` standard voice that was the previous default.
{: note}

### Deprecated features
{: #December2020-deprecated-features}

The following features were available only for standard concatenative voices. They are deprecated and have been removed from the published documentation. They will continue to function for at least one year but might be removed at a future date. You are encouraged to remove these features from your applications and to migrate to neural voices at your earliest convenience.

-   *Expressive SSML.* This was an IBM extension to SSML that was supported only for the `en-US_AllisonVoice` voice.
-   *Voice transformation SSML.* This was an IBM extension to SSML that was supported only for the `en-US_AllisonVoice`, `en-US_LisaVoice`, and `en-US_MichaelVoice` voices.
-   *The `volume` attribute of the `<prosody>` element.* This attribute was available for all standard voices.

Including these SSML elements with a synthesis request for a neural voice generates an HTTP 400 response code because the request fails SSML validation.

-   For more information about SSML validation, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#errors).
-   For more information about moving from a deprecated standard voice to a neural voice, see [Migrating from standard to neural voices](/docs/text-to-speech?topic=text-to-speech-voices#migrateVoice).

## 10 September 2020
{: #September2020b}

**Defect fix:** For the `ja-JP_EmiV3Voice` voice, the service now correctly parses SSML input text that includes a prosody rate specification. Previously, the following use of the `<prosody>` element worked properly:

<code>&lt;speak&gt;&#25104;&#21151;&#12377;&#12427;&#47;&#32321;&#26628;&#12377;&#12427;&lt;/speak&gt;</code>

But the following use of the `rate` attribute with the `<prosody>` element caused the service to read and speak the embedded SSML notation:

<code>&lt;speak rate="fast"&gt;&#25104;&#21151;&#12377;&#12427;&#47;&#32321;&#26628;&#12377;&#12427;&lt;/speak&gt;</code>

The service now correctly parses and applies the `rate` attribute of the `<prosody>` element for Japanese input.

## Older releases
{: #older}

-   [4 September 2020](#September2020a)
-   [24 June 2020](#June2020)
-   [1 April 2020](#April2020)
-   [24 February 2020](#February2020)
-   [18 December 2019](#December2019b)
-   [12 December 2019](#December2019a)
-   [12 November 2019](#November2019)
-   [1 October 2019](#October2019)
-   [22 August 2019](#August2019)
-   [30 July 2019](#July2019)
-   [24 June 2019](#June2019)
-   [24 March 2019](#March2019c)
-   [21 March 2019](#March2019b)
-   [4 March 2019](#March2019a)
-   [28 January 2019](#January2019)
-   [13 December 2018](#December2018)
-   [7 November 2018](#November2018)
-   [30 October 2018](#October2018)
-   [12 June 2018](#June2018)
-   [15 May 2018](#May2018)
-   [2 October 2017](#October2017)
-   [14 July 2017](#July2017)
-   [10 April 2017](#April2017)
-   [1 December 2016](#December2016)
-   [22 September 2016](#September2016)
-   [23 June 2016](#June2016)
-   [10 March 2016](#March2016)
-   [22 February 2016](#February2016)
-   [17 December 2015](#December2015)
-   [21 September 2015](#September2015)
-   [1 July 2015](#July2015)

### 4 September 2020
{: #September2020a}

The customization interface is now generally available. Customization is no longer beta functionality. You can use the customization interface to specify how the service pronounces unusual words that occur in your input text by creating language-specific custom dictionaries. It can be used with all generally available and beta voices. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

### 24 June 2020
{: #June2020}

-   The service now offers three new neural voices:
    -   UK English: `en-GB_CharlotteV3Voice` and `en-GB_JamesV3Voice`
    -   French: `fr-FR_NicolasV3Voice`

    It also offers an improved version of the existing UK neural voice, `en-GB_KateV3Voice`. For more information about these and all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).
-   The service now supports the `digits` attribute of the SSML `<say-as>` element with its Japanese voice. For more information, see [The say-as element](/docs/text-to-speech?topic=text-to-speech-elements#say-as_element).

### 1 April 2020
{: #April2020}

-   The service now supports two standard female Korean voices: `ko-KR_YoungmiVoice` and `ko-KR_YunaVoice`. The following information applies to both Korean voices:
    -   The voices are beta functionality. They might not be ready for production use and are subject to change. They are initial offerings that are expected to improve in quality with time and usage.
    -   The voices support customization and the `/v1/pronunciation` method.
    -   The voices support the `<mark>` element and the `timings` parameter that are available with the WebSocket interface.
    -   The voices support all Speech Synthesis Markup Language (SSML) elements except for expressive SSML and voice transformation SSML.
    -   The voices support only the International Phonetic Alphabet (IPA), not {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR), with the `<phoneme>` element.
-   The beta Arabic, Chinese, and Dutch voices now support the following features:
    -   Customization and the `/v1/pronunciation` method.
    -   The `<mark>` element and the `timings` parameter that are available with the WebSocket interface.

See the following sections for additional information:

-   For more information about all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).
-   For more information about customization, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
-   For more information about the use of IPA and SPR with customization, see [Using phonetic symbols](/docs/text-to-speech?topic=text-to-speech-sprs).

The IPA symbols for the Arabic, Chinese, Dutch, and Korean languages are not yet documented. This documentation will be made available soon.
{: note}

### 24 February 2020
{: #February2020}

-   The service now supports five new neural voices:

    -   US English: `en-US_EmilyV3Voice`, `en-US_HenryV3Voice`, `en-US_KevinV3Voice`, and `en-US_OliviaV3Voice`
    -   German: `de-DE_ErikaV3Voice`

    The new voices do not support the following SSML elements:

    -   Expressive SSML with the `<express-as>` element
    -   Voice Transformation with the `<voice-transformation>` element
    -   The `volume` attribute of the `<prosody>` element

    For more information about these and all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).
-   The service now supports the use of Activity Tracker events for all customization operations. {{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in IBM Cloud. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. For more information, see [Activity Tracker events](/docs/text-to-speech?topic=text-to-speech-at-events).

### 18 December 2019
{: #December2019b}

The service now supports six new standard voices in three new languages:

-   *Arabic:* `ar-AR_OmarVoice`
-   *Chinese (Mandarin):* `zh-CN_LiNaVoice`, `zh-CN_WangWeiVoice`, and `zh-CN_ZhangJingVoice`
-   *Dutch:* `nl-NL_EmmaVoice` and `nl-NL_LiamVoice`

The following information applies to these new standard voices:

-   The new voices are beta functionality. The voices might not be ready for production use and are subject to change. They are initial offerings that are expected to improve in quality with time and usage.
-   The voices do not support the `<mark>` element and `timings` parameter that are available with the WebSocket interface.
-   The voices do not support customization or the `/v1/pronunciation` method.
-   The voices do not support expressive SSML or voice transformation SSML.
-   The voices do support all other SSML elements. However, they support only the International Phonetic Alphabet (IPA), not {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR), with the `<phoneme>` element.

For more information about these and all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

### 12 December 2019
{: #December2019a}

-   **Full support for IBM Cloud IAM**
    -   The {{site.data.keyword.texttospeechshort}} service now supports the full implementation of {{site.data.keyword.cloud}} Identity and Access Management (IAM). API keys for Watson services are no longer limited to a single service instance. You can create access policies and API keys that apply to more than one service, and you can grant access between services. For more information about IAM, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).
    -   To support this change, the API service endpoints use a different domain and include the service instance ID. The pattern is `api.{location}.text-to-speech.watson.cloud.ibm.com/instances/{instance_id}`.

        -   Example HTTP URL for an instance hosted in the Dallas location:

            `https://api.us-south.text-to-speech.watson.cloud.ibm.com/instances/6bbda3b3-d572-45e1-8c54-22d6ed9e52c2`

        -   Example WebSocket URL for an instance hosted in the Dallas location:

            `wss://api.us-south.text-to-speech.watson.cloud.ibm.com/instances/6bbda3b3-d572-45e1-8c54-22d6ed9e52c2`

        For more information about the URLs, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech/text-to-speech#service-endpoint){: external}.

        These URLs do not constitute a breaking change. The new URLs work for both your existing service instances and for new instances. The original URLs continue to work on your existing service instances for at least one year, until December 2020.
-   **New network and data security features** for users of Premium plans:
    -   *Support for data encryption with customer-managed keys*
        -   You can integrate {{site.data.keyword.keymanagementservicefull}} with the {{site.data.keyword.texttospeechshort}} service to encrypt your data and manage encryption keys. For more information, see [Protecting sensitive information in your Watson service](/docs/watson?topic=watson-keyservice).
    -   *Support for private network endpoints*
        -   You can create private network endpoints to connect to the {{site.data.keyword.texttospeechshort}} service over a private network. Connections to private network endpoints do not require public internet access. For more information, see [Public and private network endpoints](/docs/text-to-speech/?topic=watson-public-private-endpoints).

### 12 November 2019
{: #November2019}

The service is now available in the {{site.data.keyword.cloud_notm}} Seoul location (**kr-seo**). As with other locations, the {{site.data.keyword.cloud_notm}} location uses token-based IAM authentication. All new services instances that you create in this location use IAM authentication.

### 1 October 2019
{: #October2019}

US HIPAA support is available for Premium plans that are hosted in the Washington, DC, location and are created on or after 1 April 2019. For more information, see [US Health Insurance Portability and Accountability Act (HIPAA)](/docs/text-to-speech?topic=text-to-speech-information-security#hipaa).

### 22 August 2019
{: #August2019}

The service was updated for small defect fixes and improvements.

### 30 July 2019
{: #July2019}

The service now offers a neural voice in Japanese: `ja-JP_EmiV3Voice`. Both standard and neural versions of all available voices in all supported languages are now available. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

### 24 June 2019
{: #June2019}

-   The service now offers two versions of most of its available voices:
    -   *Standard voices* that use concatenative synthesis to assemble segments of recorded speech to generate audio. Standard voices do not include a version string in their name (for example, `en-US_AllisonVoice`).
    -   *Neural voices* that use Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. Neural voices include a version string (`V3`) in their name (for example, `en-US_AllisonV3Voice`).

    Neural versions are available for all standard voices except for the `ja-JP_EmiVoice` voice, which is pending and will be available soon. You cannot use the SSML `<express-as>` and `<voice-transformation>` elements with the neural voices, and you cannot use the `volume` attribute of the `<prosody>` element with the neural voices.

    -   For more information about all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).
    -   For more information about neural voices, see [Neural voice technology](/docs/text-to-speech?topic=text-to-speech-voices#neuralVoices).
-   The service no longer includes the `V2` DNN voices that were previously available. If you use a `V2` voice in your application, the service automatically uses the equivalent `V3` voice instead.

### 24 March 2019
{: #March2019c}

-   The service now offers `V2` Deep Neural Network (DNN) versions of its German voices:
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    For more information about DNN-based voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).
-   All of the service's DNN-based voices now support the `pitch` and `rate` attributes of the SSML `<prosody>` element. The DNN-based voices do not support the `volume` attribute of the `<prosody>` element. For more information, see [The prosody element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).

### 21 March 2019
{: #March2019b}

Users can now see only service credential information that is associated with the role that has been assigned to their {{site.data.keyword.cloud_notm}} account. For example, if you are assigned a `reader` role, any `writer` or higher levels of service credentials are no longer visible.

This change does not affect API access for users or applications with existing service credentials. The change affects only the viewing of credentials within {{site.data.keyword.cloud_notm}}.

### 4 March 2019
{: #March2019a}

The service now offers four new `V2` voices that use deep-learning synthesis to generate audio:

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

These new voices use machine learning and a DNN to synthesize text to speech. Deep-learning, or Deep Neural Network (DNN)-based, synthesis produces audio with a more natural prosody and a more consistent overall quality.

But the new voices also produce audio with different signal qualities from the existing voices, so they might not be appropriate for all applications. Also, the new voices do not support the SSML elements `<prosody>`, `<express-as>`, and `<voice-transformation>`.

For more information about these DNN-based voices and how they differ from the existing voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

### 28 January 2019
{: #January2019}

The WebSocket interface now supports token-based Identity and Access Management (IAM) authentication from browser-based JavaScript code. The limitation to the contrary has been removed. To establish an authenticated connection with the WebSocket `/v1/synthesize` method:

-   If you use IAM authentication, include the `access_token` query parameter.
-   If you use Cloud Foundry service credentials, include the `watson-token` query parameter.

For more information, see [Open a connection](/docs/text-to-speech?topic=text-to-speech-usingWebSocket#WSopen).

### 13 December 2018
{: #December2018}

The {{site.data.keyword.texttospeechshort}} service is now available in the {{site.data.keyword.cloud}} London location (**eu-gb**). Like all locations, London uses token-based Identity and Access Management (IAM) authentication. All new services instances that you create in this location use IAM authentication.

### 7 November 2018
{: #November2018}

The {{site.data.keyword.texttospeechshort}} service is now available in the {{site.data.keyword.cloud}} Tokyo location (**jp-tok**). Like all locations, Tokyo uses token-based Identity and Access Management (IAM) authentication. All new services instances that you create in this location use IAM authentication.

### 30 October 2018
{: #October2018}

The {{site.data.keyword.texttospeechshort}} service has migrated to token-based Identity and Access Management (IAM) authentication for all locations. All {{site.data.keyword.cloud_notm}} services now use IAM authentication. The {{site.data.keyword.texttospeechshort}} service migrated in each location on the following dates:

-   Dallas (**us-south**): October 30, 2018
-   Frankfurt (**eu-de**): October 30, 2018
-   Washington, DC (**us-east**): June 12, 2018
-   Sydney (**au-syd**): May 15, 2018

The migration to IAM authentication affects new and existing service instances differently:

-   *All new service instances that you create in any location* now use IAM authentication to access the service. You can pass either a bearer token or an API key: Tokens support authenticated requests without embedding service credentials in every call; API keys use HTTP basic authentication. When you use any of the {{site.data.keyword.ibmwatson}} SDKs, you can pass the API key and let the SDK manage the lifecycle of the tokens.
-   *Existing service instances that you created in a location before the indicated migration date* continue to use the `{username}` and `{password}` from their previous Cloud Foundry service credentials for authentication until you migrate them to use IAM authentication. For more information about migrating to IAM authentication, see [Migrating Watson services from Cloud Foundry](/docs/text-to-speech?topic=watson-migrate).

For more information, see the following documentation:

-   To learn which authentication mechanism your service instance uses, view your service credentials by clicking the instance on the [{{site.data.keyword.cloud_notm}} dashboard](https://{DomainName}/dashboard/apps){: external}.
-   For more information about using IAM tokens with {{site.data.keyword.watson}} services, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).
-   For examples that use IAM authentication, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

### 12 June 2018
{: #June2018}

The following features are enabled for applications that are hosted in Washington, DC (**us-east**):

-   The service now supports a new API authentication process. For more information, see the [30 October 2018 service update](#October2018).
-   The service now supports the `X-Watson-Metadata` header and the `DELETE /v1/user_data` method. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

### 15 May 2018
{: #May2018}

The following features are enabled for applications that are hosted in Sydney (**au-syd**):

-   The service now supports a new API authentication process. For more information, see the [30 October 2018 service update](#October2018).
-   The service now supports the `X-Watson-Metadata` header and the `DELETE /v1/user_data` method. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

### 2 October 2017
{: #October2017}

For the `audio/l16` format, you can now optionally specify the endianness of the audio that is returned. (You must already specify the sampling rate.) Examples are `audio/l16;rate=22050;endianness=big-endian` and `audio/l16;rate=22050;endianness=little-endian`; the default is big endian. For more information, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).

### 14 July 2017
{: #July2017}

The service now supports the MP3 or Motion Picture Experts Group (MPEG) audio format. For more information about supported audio formats, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).

### 10 April 2017
{: #April2017}

-   The service now supports the Web Media (WebM) audio format with the Opus or Vorbis codec. The service now also supports the Ogg audio format with the Vorbis codec in addition to the Opus codec. For more information about supported audio formats, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).
-   The service now supports Cross-Origin Resource Sharing (CORS) to allow browser-based clients to call the service directly. For more information, see [Leveraging CORS support](/docs/text-to-speech?topic=text-to-speech-service-features#features-cors).
-   The HTTP response codes for successful completion of some methods of the customization interface changed:
    -   The `POST /v1/customizations` method now returns 201 (instead of 200).
    -   The `POST /v1/customizations/{customization_id}` method now returns 200 (instead of 201).
    -   The `POST /v1/customizations/{customization_id}/words` method now returns 200 (instead of 201).
    -   The `PUT /v1/customizations/{customization_id}/words/{word}` method now returns 200 (instead of 201).
-   The `POST /v1/customizations/{custom_id}/words` and `PUT /v1/customizations/{customization_id}/words/{word}` methods now return HTTP response code 400 with the error message `Part of speech is supported for ja-JP language only` if you attempt to specify a `part_of_speech` for a language other than Japanese.
-   The `POST /v1/customizations/{custom_id}/words` method now returns an empty response body (`{}`).

### 1 December 2016
{: #December2016}

-   The service includes a new voice, `es-LA_SofiaVoice`, which is the Latin American equivalent of the `es-US_SofiaVoice` voice. The most significant difference between the two voices concerns how they interpret a `$` (dollar sign): The Latin American version uses the term *pesos*; the North American version uses the term *dolares*. Other minor differences might also exist between the two voices.
-   In addition to the `en-US_AllisonVoice`, two more voices are now transformable with SSML voice transformation: `en-US_LisaVoice` and `en-US_MichaelVoice`. For more information about voice transformation, see [Voice transformation SSML](/docs/text-to-speech?topic=text-to-speech-transformation).
-   When you use the customization interface with Japanese, the service now matches the longest word from the word/translation pairs that are defined for a custom model. For example, consider the following two entries for a custom model:

    <pre><code>{
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    If the service finds the string <code>&#65326;&#65337;&#65315;</code> in the input text, it matches that word because it is a longer match than <code>&#65326;&#65337;</code>. Previously, the service would have matched the string <code>&#65326;&#65337;</code>. For more information about working with Japanese entries for a custom model, see [Working with Japanese entries](/docs/text-to-speech?topic=text-to-speech-rules#jaNotes).

### 22 September 2016
{: #September2016}

-   The customization interface, which includes the customization and `GET /v1/pronunciation` methods, is now available for all languages that are supported by the service. The interface remains a beta release. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
-   The service now supports SSML for Japanese. For general information about SSML support, see [Using SSML](/docs/text-to-speech?topic=text-to-speech-ssml). For information about Japanese SPR and IPA symbols, see [Japanese symbols](/docs/text-to-speech?topic=text-to-speech-jaSymbols). Extra considerations and a `part_of_speech` field apply when creating entries for words in a Japanese custom model. For more information, see [Working with Japanese entries](/docs/text-to-speech?topic=text-to-speech-rules#jaNotes).
-   The service now offers SSML voice transformation via the new `<voice-transformation>` element. You can expand the range of possible voices by creating custom transformations that modify the pitch, pitch range, glottal tension, breathiness, rate, and timbre of a voice. The service also offers two built-in virtual voices, *Young* and *Soft*. The service currently supports voice transformation only for the US English Allison voice. For more information, see [Voice transformation SSML](/docs/text-to-speech?topic=text-to-speech-transformation).
-   The service can now return word timing information for all strings of the input text that you pass to the WebSocket interface. To receive the start and end time of every string in the input, specify an array that includes the string `words` for the optional `timings` parameter of the JSON object that you pass to the service. The feature is not currently available for Japanese input text. For more information, see [Word timings](/docs/text-to-speech?topic=text-to-speech-timing).
-   The service now validates all SSML elements that you submit in any context. If it finds an invalid tag, the service reports an HTTP 400 response code with a descriptive message, and the method fails. In previous releases, the service handled errors inconsistently; specifying an invalid word pronunciation, for example, could lead to unpredictable or inconsistent behavior. For more information, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#errors).
-   The use of `spr` is deprecated as an argument to the `format` option of the `GET /v1/pronunciation` method and for use with the `alphabet` attribute of an SSML `<phoneme>` element. To use {{site.data.keyword.IBM_notm}} SPR notation, use the `ibm` argument instead of `spr` in all cases.
-   The list of supported audio formats now includes `audio/mulaw;rate=8000`. Like `audio/basic`, this format provides single-channel audio that is encoded by using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).
-   The `GET /v1/voices` and `GET /v1/voices/{voice}` methods now return a `supported_features` object as part of their output for each voice. The object describes whether the voice supports customization and the SSML `<voice_transformation>` element. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

### 23 June 2016
{: #June2016}

-   The service now offers a WebSocket interface for synthesizing text to speech. The interface offers the same features as the `/v1/synthesize` method of the HTTP interface. It accepts plain text or text that is marked up with SSML. In addition, it also supports use of the SSML `<mark>` element to identify the time in the audio at which it finishes synthesizing all text that precedes the mark. For more information, see [The WebSocket interface](/docs/text-to-speech?topic=text-to-speech-usingWebSocket).
-   The service now offers support for text that is annotated with SSML for the languages Castilian and North American Spanish, Italian, and Brazilian Portuguese. The service already supported the use of SSML for US and UK English, French, and German. As of this update, the service supports SSML for all languages but Japanese. Moreover, you can use both {{site.data.keyword.IBM_notm}} SPR and IPA notations to define word pronunciations with the SSML `<phoneme>` element. For more information, see [Using SSML](/docs/text-to-speech?topic=text-to-speech-ssml) and [Using phonetic symbols](/docs/text-to-speech?topic=text-to-speech-sprs).

    For US English, you can also use the SSML `<phoneme>` element to create word entries in a custom model; customization is supported only for US English. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
-   The service features improved expressiveness and naturalness for the most frequently used voices. The improvements are based on Recursive Neural Network (RNN)-based prosody prediction from input text. They are made available as a new service engine and voice-model updates for the following languages:

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   The `GET /v1/pronunciation` method now accepts an optional `customization_id` query parameter. The parameter obtains a word translation from a specified custom model. If the custom model does not contain the word, the method returns the word's default pronunciation. For more information, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

    When using the `GET /v1/pronunciation` method without a customization ID and for a language other than US English, you can request a word's pronunciation only in {{site.data.keyword.IBM_notm}} SPR notation. For a language other than US English, you must specify `spr` with the method's `format` option.
    {: note}
-   The list of supported audio formats now includes `audio/basic`, which provides single-channel audio that is encoded using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).
-   The HTTP and WebSocket `/v1/synthesize` methods can return a `warnings` response that includes messages about invalid query parameters or JSON fields that are included with a request. The format of the warnings changed. The following example shows the previous format:

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    The same warning now has the following format:

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 10 March 2016
{: #March2016}

-   The `GET` and `POST /v1/synthesize` methods can now return a `Warnings` response header that includes a list of warning messages about invalid query parameters or JSON fields that are included with the request. Each element of the list includes a string that describes the nature of the warning followed by an array of invalid argument strings; for example, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}'].` For more information, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.
-   The beta *{{site.data.keyword.watson}} Speech Software Development Kit (SDK) for the Apple&reg; iOS operating system* is deprecated and replaced by the *{{site.data.keyword.watson}} Swift SDK*. The new SDK is available from the [swift-sdk repository](https://github.com/watson-developer-cloud/swift-sdk){: external} in the `watson-developer-cloud` namespace on GitHub.

### 22 February 2016
{: #February2016}

The service was updated with a new expressive SSML feature. The service extends SSML with an `<express-as>` element that you can use to indicate expressiveness in one of three speaking styles: `GoodNews`, `Apology`, or `Uncertainty`. You can apply the element to the entire body of the text, a sentence, a phrase, or a word. The service currently supports expressiveness only for the US English Allison voice (`en-US_AllisonVoice`). For more information, see [Expressive SSML](/docs/text-to-speech?topic=text-to-speech-expressive).

### 17 December 2015
{: #December2015}

-   The service offers a new customization interface that you can use to specify how it pronounces unusual words that occur in your input. The interface includes a number of new methods that you can use to create and manage custom models and the word/translation pairs that they contain. You can then use your custom models when synthesizing text to audio.

    The service supports sounds-like translations and phonetic translations. Phonetic translations can use either the standard International Phonetic Alphabet (IPA) representation or the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). You use SSML to specify phonetic translations.

    The customization interface includes a collection of new HTTP methods that have the names `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words`, and `PUT /v1/customizations/{customization_id}/words/{word}`. The service also provides a new `GET /v1/pronunciation` method that returns the pronunciation for any word and a new `GET /v1/voices/{voice}` method that returns detailed information about a specific voice. In addition, existing methods of the service's interface now accept custom model parameters as needed.

    For more information about customization and its interface, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro) and the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

    The customization interface is a beta release that currently supports US English only. All customization methods and the `GET /v1/pronunciation` method can currently be used to create and manipulate custom models and word translations only in US English.
    {: note}
-   The service supports a new voice, `pt-BR_IsabelaVoice`, to synthesize audio in Brazilian Portuguese with a female voice. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

### 21 September 2015
{: #September2015}

-   Two new beta mobile Software Development Kits (SDKs) are available for the speech services. The SDKs enable mobile applications to interact with both the {{site.data.keyword.texttospeechshort}} and {{site.data.keyword.speechtotextshort}} services. You can use the SDKs to send text to the {{site.data.keyword.texttospeechshort}} service and receive an audio response.
    -   The *{{site.data.keyword.watson}} Swift SDK* is available from the [swift-sdk repository](https://github.com/watson-developer-cloud/swift-sdk){: external} in the `watson-developer-cloud` namespace on GitHub.
    -   The *{{site.data.keyword.watson}} Speech Android SDK* is available from the [speech-android-sdk repository](https://github.com/watson-developer-cloud/speech-android-sdk){: external} in the `watson-developer-cloud` namespace on GitHub.

    Both SDKs support authenticating with the speech services by using either your {{site.data.keyword.cloud_notm}} service credentials or an authentication token.

    Because the SDKs are beta functionality, they are subject to change in the future.
    {: note}
-   The service supports a new language, Japanese. The voice `ja-JP_EmiVoice` is a Japanese female voice.

### 1 July 2015
{: #July2015}

The service moved from beta to general availability (GA) on July 1, 2015. The following differences existed between the beta and GA versions of the {{site.data.keyword.texttospeechshort}} API. The GA release required that users upgrade to the new version of the service.

-   A new programming model supports direct interaction between a client and the service. By using this model, a client can obtain an authentication token for communicating directly with the service. By using the token, the client can bypass the need for a server-side proxy application in {{site.data.keyword.cloud_notm}} to call the service on its behalf. Tokens are the preferred means for clients to interact with the service.

    The service continues to support the old programming model that relied on a server-side proxy to relay communications and data between the client and the service. But the new model is more efficient and provides higher throughput.
-   You can now pass SSML to the HTTP `GET` and `POST` versions of the `/v1/synthesize` method. SSML is an XML-based markup language that is designed to provide annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. For more information about passing SSML input to the service, see [Specifying input text](/docs/text-to-speech?topic=text-to-speech-usingHTTP#input).

    The service initially supports the use of SSML only for the UK and US English, French, and German languages. The service does not support SSML for use with Italian and Spanish. When you use SSML, make sure that you do not select a voice for the audio in one of the unsupported languages. Results in this case are not meaningful.
-   The voices that are supported for synthesized speech changed and expanded. The service now supports a number of additional voices, languages, and dialects with the `/v1/synthesize` methods. For more information about supported voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

    The three voices that were available at beta are renamed for GA:
    -   `VoiceEnUsMichael` is now `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` is now `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` is now `es-ES_EnriqueVoice`

    The previous names of the voices continue to work with the beta version of the service (via `-beta` API endpoints) while that version remains available. However, you must use the new names with the GA version of the service.
-   You can now request the service to return audio in the Free Lossless Audio Codec (FLAC) format. The service can still return audio in the Ogg format with the Opus codec (the default) and in the Waveform Audio File Format (WAV). For more information about using audio formats with the `/v1/synthesize` methods, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).
-   The text that you send to the `/v1/synthesize` method in the URL of an HTTP `GET` request or in the body of an HTTP `POST` request is now limited to a maximum of 5 KB. The text had a maximum size of 4 MB for the beta version.
-   The `/v1/synthesize` methods now include the header `X-WDC-PL-OPT-OUT` to control whether the service uses the text and audio results from an operation to improve future results. Specify a value of `1` for the header to prevent the service from using text and audio results. The parameter applies only to the current request. The new header replaces the `X-logging` header from the beta methods. For more information, see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/watson?topic=watson-gs-logging-overview).
-   For the `/v1/synthesize` methods, the following error codes changed:
    -   Error code 406 ("Not acceptable. Unsupported MIME type.") is removed.
    -   Error code 415 ("Unsupported Media Type") is added.
    -   Error code 503 ("Service Unavailable") is added.
-   For the `GET /v1/voices` method, the following error codes changed:
    -   Error code 406 ("Not acceptable. Unsupported MIME type.") is removed.
    -   Error code 415 ("Unsupported Media Type") is added.
