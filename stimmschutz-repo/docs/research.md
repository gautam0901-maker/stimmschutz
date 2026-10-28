# Research and evidence

Sources behind every claim in this project. Checked October 2026.

## The problem is real

- **BBC Panorama case:** an anonymous source's face was hidden but his real voice was kept; friends recognized him. Ofcom upheld his privacy complaint and the BBC apologized.
  [Press Gazette (2013)](https://pressgazette.co.uk/publishers/broadcast/panorama-breached-privacy-identifying-anonymous-gambling-addict-source/) · [iMediaEthics](https://www.imediaethics.org/bbcs-interview-with-anonymous-source-wasnt-so-anonymous-used-his-real-voice-uk-regulator-calls-out-invasion-of-privacy/)
- **Real user requests:** filmmakers asking how to disguise an informant's voice so it "can't be altered back" (2017) and noting that pitch shifting is easy to reverse (2020).
  [Adobe Community 2017](https://community.adobe.com/questions-544/confidential-informant-voice-change-that-can-t-be-altered-back-to-normal-165005) · [Adobe Community 2020](https://community.adobe.com/questions-729/how-to-distort-voice-from-anonymous-source-in-pr-no-pitch-shifter-1369596)
- **Simple methods are weak:** early methods such as pitch changes offer limited protection against modern speaker verification.
  [PPX-Anon, SPSC 2025](https://www.isca-archive.org/spsc_2025/thebaud25_spsc.pdf) · [kalika.de (Aug 2026, German)](https://www.kalika.de/posts/what-are-some-good-free-linux-friendly-open-source-voice-cha/)
- **Germany protects whistleblowers' identity by law:** [§ 8 HinSchG](https://www.gesetze-im-internet.de/hinschg/__8.html)
- **Automated voice analysis by police:** [netzpolitik.org (2017)](https://netzpolitik.org/2017/eu-projekte-zur-sprachbiometrie-forschen-fuer-polizei-und-geheimdienst/)
- **Current surveillance debate:** DJV warns that planned powers include AI and biometrics (23 Sep 2026).
  [DJV press release](https://www.djv.de/news/pressemitteilungen/press-detail/besserer-informantenschutz-gefordert)

## Existing tools

| Tool | Type | Gap |
|---|---|---|
| [VoiceShield](https://kianattar.github.io/voiceshield/) | Open source, local, desktop | Pitch/formant shift + effects only; no risk check |
| [Nijta](https://www.nijta.com/) | Commercial, on-device | Closed source; no visible risk score |
| [VOXPROTECT](https://www.aap.com.au/aapreleases/cision20220712ae79586) | Commercial plug-in (2022) | Closed; status unknown |
| [RVC](https://github.com/satiricalguru/RVC-Voicechanger) / w-okada voice changer | Open source, local AI | Made for cloning real voices; needs GPU and setup |
| [bgblur](https://www.bgblur.com/en/features/voice-anon), vidio.ai | Online services | Original recording must be uploaded |
| [Stuttgart speaker-anonymization](https://github.com/DigitalPhonetics/speaker-anonymization), [VoicePAT](https://github.com/DigitalPhonetics/VoicePAT), [V-Cloak](https://www.usenix.org/conference/usenixsecurity23/presentation/deng-jiangyi-v-cloak) | Research code | Built for researchers, not end users |

## Research the method builds on

- [Third VoicePrivacy Challenge](https://arxiv.org/html/2601.11846)
- [kNN-VC – Voice Conversion With Just Nearest Neighbors (Interspeech 2023)](https://www.isca-archive.org/interspeech_2023/baas23_interspeech.html)
- [kNN-VC for anonymization (SPSC 2024)](https://www.isca-archive.org/spsc_2024/das24b_spsc.pdf)
- [Duration features re-identify anonymized speakers (Interspeech 2025)](https://www.isca-archive.org/interspeech_2025/tomashenko25_interspeech.pdf)
- [Target speaker anonymization in multi-speaker recordings (2025)](https://arxiv.org/html/2510.09307v1)
- [VoicePAT evaluation toolkit](https://arxiv.org/pdf/2309.08049)
- [Per-speaker re-identification risk (2026)](https://arxiv.org/abs/2606.07210)
- [Linguistic content as an attack vector (2025)](https://alphaxiv.org/abs/2506.09521)
