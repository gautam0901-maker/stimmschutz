# Method

This document explains how Stimmschutz is planned to work and why.

## 1. Why simple voice changing fails

Scientists describe the voice with the **source-filter model**:

- **Source (vocal folds):** pitch (F0) and small irregularities (jitter, shimmer).
- **Filter (throat, mouth, nose):** resonances called formants and the overall timbre. Higher formants depend strongly on a person's anatomy.
- **Behaviour:** rhythm, pauses and how long each sound lasts.

Pitch shifting changes frequencies with a fixed rule. A fixed rule can often be reversed, and most identity information (timbre, formant pattern, rhythm) stays. Modern speaker recognition models (x-vectors, ECAPA-TDNN) learn exactly these patterns.

**Principle:** you cannot reverse what is no longer there. Stimmschutz throws the identity away and rebuilds the speech, instead of only modifying it.

## 2. Pipeline

### Stage 1 – Analyze
- Read audio or video (FFmpeg).
- Speaker diarization: find the segments spoken by the person to protect, so other voices (e.g. the journalist) stay unchanged.
- Extract content features with a self-supervised speech model (WavLM), the pitch contour with a pitch tracker, and a speaker embedding (ECAPA-TDNN) used only for testing.

### Stage 2 – Remove identity
- **Pitch normalization:** convert the melody to values relative to the speaker's own average, drop the personal average, map it onto the new voice's range. Emotion and intonation stay; the personal pitch level disappears.
- Remove micro-irregularities.
- **Rhythm perturbation:** slightly vary phoneme durations. Research shows that duration patterns can re-identify speakers even after anonymization ([Tomashenko et al., Interspeech 2025](https://www.isca-archive.org/interspeech_2025/tomashenko25_interspeech.pdf)).

### Stage 3 – New voice
- **kNN-VC** ([Baas et al., Interspeech 2023](https://www.isca-archive.org/interspeech_2023/baas23_interspeech.html)): each small piece of speech is replaced by the most similar piece from a pool of many different speakers. The result is a mixture voice that belongs to no single person.
- The pseudo-voice is checked to be far from the original and from the voices in the pool.

### Stage 4 – Rebuild
- A neural vocoder (HiFi-GAN) turns the converted features into clear, natural audio.

### Stage 5 – Check
The program attacks its own result:
1. **Standard attacker:** speaker recognition compares original and result.
2. **Informed attacker:** the attacker knows Stimmschutz was used and processes the original the same way before comparing (VoicePrivacy evaluation standard, see [VoicePAT](https://arxiv.org/pdf/2309.08049)).
3. **Rhythm attacker:** compares duration and melody patterns.

Quality checks: speech recognition (Whisper) checks the words; pitch correlation checks that emotion is preserved.
The risk rating also considers recording length, because longer recordings are easier to link ([Dufour et al., 2026](https://arxiv.org/abs/2606.07210)).

Output: 🟢 safe / 🟡 unsure / 🔴 not safe, with the reason. Hidden file metadata (device, location, date) is removed on export.

## 3. Running offline on a normal laptop

- All models are shipped with the program; no network access.
- Models are exported to ONNX and compressed with INT8 quantization.
- Planned benchmark: how small and fast can the models become on a laptop CPU before privacy or quality drops (e.g. WavLM Large vs. WavLM Base+, FP32 vs. INT8)?

## 4. What is new

No single component is new science. The contribution is the combination in one offline, CPU-only, open-source tool for non-experts:
speaker selection + kNN-VC pseudo-voice + pitch normalization + phoneme-level rhythm perturbation + multi-attacker risk estimate + metadata removal.

## 5. Licences to check

Each model and code base will be checked before reuse (e.g. Whisper: MIT; SpeechBrain models: Apache 2.0; University of Stuttgart speaker-anonymization code: GPL-3.0).
