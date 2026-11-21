# Awesome-Audio-Processing-Noise-Suppression

## Top Audio Processing & Noise Suppression Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Real-Time Noise Cancellation, AI Audio Restoration & Self-Hosted DSP Engines*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Audio Processing & Noise Suppression**. These tools help creators, developers, and call participants clean up speech—removing background noise, echo, and artifacts in real time or from recorded files, covering everything from browser-based AI enhancers to low-latency neural models you can embed directly in your application.

**Examples** include Krisp, Adobe Podcast, Auphonic, Cleanvoice AI, DTLN, DeepFilterNet, and RNNoise (the category leaders).

**Open-source emphasis**: This section highlights every major active project for self-hosted noise suppression, open-source neural speech enhancement, and community-driven DSP tooling—ideal for developers seeking to embed noise cancellation directly into their products without per-minute fees or cloud dependency. The open-source landscape is genuinely functional: **DTLN** provides a lightweight dual-LSTM model that runs in-process at ~8ms latency [citation:2], **DeepFilterNet 3** delivers competitive suppression quality via a browser-based WASM package [citation:3], and **RNNoise** remains the battle-tested lightweight baseline available across platforms [citation:9].

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-products)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Krisp](https://krisp.ai/)**  
  **Real-time noise cancellation for live calls** on Zoom, Teams, Meet, Webex, and Slack. Sits between your microphone and the call app as a virtual device, removing background noise, other voices, and echo as you speak [citation:1][citation:8]. **$8/month per user on annual billing ($16 monthly) after a 7-day trial** [citation:1][citation:8]. Best for individuals and teams wanting noise-free calls without infrastructure management.

- **[Adobe Podcast Enhance Speech](https://podcast.adobe.com/enhance)**  
  **The go-to free tool for rescuing one bad recording.** Browser-based AI enhancement that removes background noise and echo, making voice sound richer and fuller [citation:6][citation:8]. **Free tier supports files up to 30 minutes and 500MB, with 1 hour of optimization per day** [citation:13]. Premium adds video support and higher limits via Adobe Express Premium (~$12.99/mo) [citation:13]. Best for one-off rescues where no budget is available.

- **[Auphonic](https://auphonic.com/)**  
  **Built for producers who publish on a schedule.** Every plan—including the **free 2 hours/month**—includes Intelligent Leveler, noise and reverb reduction, loudness targets for podcast/broadcast specs, filler-word and silence cutting, video support, and audiograms [citation:1][citation:4]. **Paid plans: ~$11/month for 9 hours (yearly) or $13 monthly; one-time credits from $12 for 5 hours ($2.40/hr) down to $1.71/hr at 100 hours** [citation:4][citation:11]. Best for weekly podcasts needing levelling and loudness compliance.

- **[Cleanvoice AI](https://cleanvoice.ai/)**  
  **Focuses on the edits that take longest by hand**: removing filler words, background noise, mouth sounds, and breaths—including on video podcasts [citation:1][citation:5]. **Free trial: 30 minutes, no card required.** **Paid: $11/month for 10 hours (~$1.10/hr) or $28/month for 30 hours (~$0.93/hr)**; pay-as-you-go credits valid for 2 years [citation:1][citation:5]. Subscription credits roll over up to 3x the monthly limit [citation:5]. Best when filler-word removal is the primary pain point.

- **[Descript Studio Sound](https://www.descript.com/)**  
  Integrated audio cleanup within the Descript editing workflow. Best for teams already editing in Descript—no separate processing step required [citation:1].

- **[ElevenLabs Voice Isolator](https://elevenlabs.io/)**  
  AI voice isolation tool available as part of ElevenLabs' platform. Free for normal use according to 2026 comparisons [citation:8]. Best for isolating speech from heavily noisy recordings where other tools struggle.

## Open-Source GitHub Projects

- **[DTLN (Dual-Signal Transformation LSTM Network)](https://github.com/breizhn/DTLN)**  
  **The most practical open-source model for embedding real-time noise suppression into applications.** **Fully self-hosted, in-process**—runs via ONNX Runtime with **no cloud API, no per-minute fees, and no proprietary binaries** [citation:2]. **~8ms latency** (one block shift), **audio never leaves your server** [citation:2]. **Two sequential LSTM models**: spectral masking followed by time-domain refinement, with stateful hidden states that persist across frames for temporal context [citation:2]. **LiveKit plugin available** (`livekit-plugins-dtln`) with tuning via `strength` (0.0–1.0 wet/dry blend) and debug logging for over-suppression diagnosis [citation:2]. **Best for developers building voice agents or real-time communication platforms** who need privacy-preserving, zero-latency noise cancellation without vendor dependency.

- **[DeepFilterNet 3](https://github.com/Rikorose/DeepFilterNet)**  
  **Competitive neural suppression quality with browser deployment.** **`denoise-voice-clarity`** NPM package wraps DeepFilterNet 3 in an **AudioWorklet + WebAssembly** package—runs **100% client-side**, no audio leaves the device, no per-seat fees [citation:3]. **MIT licensed** [citation:3]. **~10ms latency** (one 480-sample frame at 48kHz), **full WASM model is large (~18MB)** so dynamic import is required [citation:3]. Includes a **voice-clarity chain** (high-pass → presence EQ → AGC → soft compressor) beyond pure denoising [citation:3]. **Trade-off**: DNSMOS P.835 scores place DeepFilterNet 3 below DPDFNet and above Krisp on overall quality, background noise reduction, and speech quality in independent testing [citation:10]. **Best for browser-based applications** needing free, client-side noise suppression with voice clarity enhancements.

- **[RNNoise](https://github.com/xiph/rnnoise)**  
  **The battle-tested lightweight baseline for real-time noise suppression.** **BSD licensed**, extremely small and fast. **ClearVox** wraps RNNoise in a Go-based macOS app with a professional PKG installer, bundling RNNoise and PortAudio libraries and optionally installing BlackHole as a virtual microphone [citation:9]. **DNSMOS scores**: RNNoise scores **2.01 overall** in independent testing—lower than DeepFilterNet 3 (2.97) and DPDFNet (3.20), but still a significant improvement over unprocessed input (1.49) [citation:10]. **Best for resource-constrained environments** or when a proven, widely-deployed baseline is sufficient.

- **[DPDFNet (HushMic)](https://github.com/ceva-ip/DPDFNet)**  
  **The highest-scoring open-source model in independent DNSMOS testing.** **Apache-2.0 licensed** by Ceva [citation:10]. **Scores 3.20 overall, 4.15 background noise reduction, 3.43 speech quality**—the only model that maintains its score on the challenging café noise clip where others drop [citation:10]. **CPU cost**: native engine runs at ~0.1× real time on one desktop core (0.07 with AVX-VNNI); ONNX Runtime at ~0.3× [citation:10]. **80ms latency** [citation:10]. **Trade-off**: newer and less widely deployed than DeepFilterNet or RNNoise. **Best for applications where suppression quality is the top priority** and 80ms latency is acceptable.

### Additional Strong Open-Source Options

- **[denoise-voice-clarity](https://www.npmjs.com/package/denoise-voice-clarity)** — NPM package providing a complete browser-based noise suppression + voice clarity pipeline using DeepFilterNet 3 WASM, with a thin LiveKit adapter and MIT licensing [citation:3].
- **[livekit-plugins-dtln](https://pypi.org/project/livekit-plugins-dtln/)** — Python LiveKit plugin for DTLN noise suppression, bundled with pretrained ONNX weights (~4MB), installable via pip [citation:2].
- **Community RNNoise wrappers** (ClearVox, EasyEffects RNNoise plugin) for desktop and Linux audio pipelines [citation:9].

**Frameworks for building custom systems**: Combine **DTLN** for in-process real-time suppression in voice applications, **DeepFilterNet 3** for browser-based client-side denoising with voice clarity, and **DPDFNet** when maximum suppression quality justifies 80ms latency. For recorded file cleanup, the SaaS tools (Adobe Podcast, Auphonic, Cleanvoice) remain more convenient than assembling an open-source pipeline.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Noise suppression tools process potentially sensitive voice communications; **self-hosted models keep audio on your infrastructure**, while SaaS tools transmit audio to third parties. Review data handling policies before processing confidential calls or recordings.
- **Tool choice depends on whether you need real-time call cleanup, recorded file restoration, or embedded DSP.** **Krisp is the real-time call standard** but requires a subscription and runs as a virtual device [citation:1]. **Adobe Podcast is the best free option for one-off rescues** with 30-minute file limits [citation:13]. **Auphonic and Cleanvoice are cheapest per hour for recurring podcast production** (~$1–$1.50/hr) but serve different strengths: Auphonic for levelling/loudness, Cleanvoice for filler-word removal [citation:1]. **Open-source models have different quality/latency trade-offs**: DTLN is the lowest-latency (~8ms) and most practical for embedding [citation:2]; DeepFilterNet 3 offers competitive quality with browser deployment but scores below DPDFNet [citation:10]; RNNoise is the lightweight baseline but significantly lower quality [citation:10]; DPDFNet scores highest but at 80ms latency [citation:10]. **Validate whether you need SaaS convenience (Krisp, Adobe Podcast) or embedded open-source DSP (DTLN, DeepFilterNet)** before committing.

---

**Made for audio developers, podcast producers, and engineers building noise suppression infrastructure.**  
Let's make audio processing and noise suppression more open, privacy-preserving, and accessible.
