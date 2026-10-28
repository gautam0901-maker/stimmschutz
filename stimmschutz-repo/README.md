# Stimmschutz

**Offline voice anonymization you can verify.**

Stimmschutz ("voice protection") will be a free, open-source desktop program that replaces a person's voice in audio or video recordings with an artificial voice that belongs to nobody – and then tests how recognizable the person still is.

> **Status:** Research phase completed (October 2026). No release yet. This repository documents the problem, the planned method and the roadmap.

---

## The problem

Journalists, researchers and NGOs record people who must stay anonymous: whistleblowers, informants, victims of violence, refugees, research participants. Their voice alone can reveal them.

Current ways to hide a voice have serious gaps:

| Method | Problem |
|---|---|
| Pitch shifting / robot effects | Can often be reversed; offers little protection against modern speaker recognition |
| Online AI voice changers | The original, unprotected recording must be uploaded to a company's server |
| Local AI voice changers (e.g. RVC) | Built to copy real people's voices; need a graphics card and technical setup |
| Re-recording with another speaker | Costs time and loses the original emotion |
| All of the above | Nobody tells the user whether the result is actually safe |

A documented example: in a BBC Panorama programme, an anonymous source's face was hidden but his real voice was kept – friends recognized him, and the UK regulator Ofcom upheld his privacy complaint. More evidence: [docs/research.md](docs/research.md).

---

## The planned solution

Stimmschutz runs **completely offline** on a normal laptop. Nothing is uploaded.

```
Recording (audio or video)
   ↓  1. Analyze      – find where the protected person speaks (speaker diarization)
   ↓                    and separate WHAT is said, HOW it is said, WHO says it
   ↓  2. Remove       – discard the voice identity, normalize the personal pitch level,
   ↓                    slightly vary sound durations (rhythm can identify people)
   ↓  3. New voice    – rebuild speech from tiny pieces of many speakers (kNN-VC)
   ↓                    → a natural voice that belongs to nobody
   ↓  4. Rebuild      – a neural vocoder (HiFi-GAN) produces clear audio
   ↓  5. Check        – independent attacker tests try to re-identify the speaker;
                        speech recognition checks the words are correct
Result: 🟢 safe   🟡 unsure   🔴 not safe   (+ hidden file metadata removed)
```

Details: [docs/method.md](docs/method.md)

**Design principles**
- **Offline only** – no network connection, models are shipped with the program
- **No voice cloning** – outputs only artificial voices of nobody, never a real person's voice
- **Honest** – shows an estimated risk, never promises "100 % anonymous"
- **Runs on normal laptops** – models exported to ONNX and compressed with INT8 quantization
- **Open source** – everyone can verify what the program does

---

## Who it is for

- Freelance journalists, local newsrooms, podcasters and documentary makers
- NGOs working with refugees or victims of violence
- Researchers who must anonymize interview recordings
- Whistleblower support organizations

---

## Roadmap (planned)

- [x] Problem and user research
- [x] Analysis of existing tools and research
- [x] Method selection
- [ ] First CPU test: anonymize sample recordings and measure speaker similarity
- [ ] Offline pipeline (analysis → anonymization → vocoder)
- [ ] Rhythm (duration) perturbation
- [ ] Built-in risk test with several attacker models
- [ ] Speaker selection for interviews (diarization)
- [ ] Video support and metadata removal
- [ ] Model compression (ONNX + INT8) and CPU benchmarks
- [ ] Simple desktop interface
- [ ] User tests with journalists and NGOs
- [ ] Packaged releases for Windows and Linux (macOS planned)

---

## Limitations (honest)

- No tool can make a voice perfectly unidentifiable. Stimmschutz estimates the risk; it does not guarantee anonymity.
- Word choice, speaking style and the content itself can still reveal a person.
- First languages: German and English.

---

## Built on research

Stimmschutz does not reinvent voice anonymization. It builds on published research, including the [VoicePrivacy Challenge](https://arxiv.org/html/2601.11846), [kNN-VC](https://www.isca-archive.org/interspeech_2023/baas23_interspeech.html) and [VoicePAT](https://github.com/DigitalPhonetics/VoicePAT). Full list: [docs/research.md](docs/research.md).

---

## Author

Gautam Ramesh – M.Sc. Business Intelligence & Data Analytics, Hochschule Emden/Leer. Background in speech ML ([chola-compressor](https://huggingface.co/Gautam0901/chola-compressor)), edge AI on NVIDIA Jetson and model quantization.

## License

To be decided before the first code release (likely GPL-3.0, to stay compatible with reused research code).
