<!-- TODO: Replace with the official project/repository name and acronym once defined. The source paper does not specify a project acronym. -->

# Bilateral sEMG Trunk-Stabilizer Asymmetry During Simulated Public Transport Load Carriage

**A pilot surface electromyography (sEMG) study of upper trapezius activation and bilateral muscular asymmetry during backpack load carriage under simulated public transport conditions.**

<!-- TODO: Add CI badge once a build/test pipeline exists -->
[![Build Status](https://img.shields.io/badge/build-TODO-lightgrey.svg)]()
[![License](https://img.shields.io/badge/license-TODO-lightgrey.svg)](LICENSE)
[![Python Version](https://img.shields.io/badge/python-TODO-blue.svg)]()
[![Status](https://img.shields.io/badge/status-pilot--study-yellow.svg)]()
[![DOI](https://img.shields.io/badge/DOI-TODO-blue.svg)]()

---

## Overview

This repository documents a pilot study that uses **surface electromyography (sEMG)** to evaluate bilateral activation and asymmetry of the trunk-stabilizer musculature — specifically the **upper trapezius** — during simulated public transport load carriage.

Five university students (four men, one woman), all seventh-cycle students at the Universidad Peruana Cayetano Heredia (La Molina campus), were divided into two groups based on their habitual mode of daily transportation to the university: **habitual public transport users** and **habitual private transport users**. Each participant was evaluated under three conditions — baseline (seated, unloaded), two-strap backpack carriage (bilateral load), and single-strap backpack carriage (unilateral load) — while standing and holding an overhead handrail, simulating standing passenger conditions on a public transport bus.

Bilateral sEMG signals were acquired from the upper trapezius using a **BITalino (PLUX)** two-channel acquisition system, processed through a standard sEMG conditioning chain, and quantified using the **Root Mean Square (RMS)** of muscle activation and a **Muscular Asymmetry Index (MAI)**.

This project is intended for:

- Researchers in biomechanics, kinesiology, and occupational ergonomics studying load carriage and postural control.
- Biomedical engineering students and educators interested in low-cost sEMG acquisition and signal processing pipelines.
- Clinicians and physical therapists interested in musculoskeletal load asymmetry associated with habitual transport mode.
- Contributors seeking to extend sEMG-based asymmetry analysis to larger cohorts or additional muscle groups.

<!-- TODO: Add GIF or image of the experimental setup -->

---

## Motivation

Load carriage (LC) is a common biomechanical demand encountered during daily, recreational, and occupational activities. Carrying an external load displaces the body's center of mass and increases the physiological and metabolic demand required to maintain balance, which can accelerate the onset of muscular fatigue under prolonged or repetitive exposure.

Public transportation adds a further layer of complexity: passengers are continuously exposed to unpredictable accelerations, braking events, and lateral movements that demand rapid neuromuscular responses to preserve postural stability. Forces generated during acceleration and braking while standing have been reported to reach up to approximately 165% of body weight without support, and approximately 120% even while holding a handrail. When an external load — such as a backpack — is carried simultaneously, the musculoskeletal system must compensate for the displaced center of mass while continuously responding to these external perturbations.

Prior research has shown that load carriage increases the demand on trunk-stabilizer muscles and modifies postural control strategies, and that asymmetric load distribution (e.g., single-strap versus two-strap backpacks, or shoulder bags) can produce asymmetric muscle activation patterns between the ipsilateral and contralateral sides of the body. However, most existing studies have been conducted under controlled experimental conditions focused on load and backpack characteristics, with limited attention paid to the influence of the dynamic, unpredictable environment characteristic of everyday public transport.

This project addresses that gap by using bilateral sEMG monitoring to compare neuromuscular asymmetry responses to backpack load carriage between habitual public transport users and habitual private transport users, motivated by the hypothesis that habitual exposure to unpredictable transport perturbations may induce distinct neuromuscular adaptation strategies.

---

## Key Features

- **Bilateral surface EMG acquisition** from the upper trapezius using two synchronized channels.
- **Standardized electrode placement** following the SENIAM protocol, with electrodes positioned symmetrically over the upper trapezius at clavicle height and a ground electrode placed on the iliac crest.
- **Multi-condition acquisition protocol**: baseline (unloaded, seated), two-strap backpack (bilateral load, standing), and single-strap backpack (unilateral load, standing), each simulating standing passenger posture in public transport.
- **Standard sEMG conditioning pipeline**: band-pass filtering, notch filtering for line interference, and RMS moving-window smoothing.
- **Quantitative activation metric (RMS)** computed per condition and per channel.
- **Muscular Asymmetry Index (MAI)** to quantify bilateral asymmetry in trapezius activation as a function of load condition.
- **Frequency-domain validation** of signal quality via Fast Fourier Transform (FFT) and Welch periodogram analysis.
- **Comparative group design** contrasting habitual public transport users against habitual private transport users.

---

## System Architecture

The system described in the paper consists of a single acquisition layer feeding into an offline signal-processing and analysis workflow. No cloud, wireless telemetry, or real-time visualization layer is described in the source paper.

**Acquisition layer**
- Two-channel sEMG acquisition using a BITalino (PLUX) device.
- Ag/AgCl surface electrodes placed bilaterally on the upper trapezius (clavicle-level, symmetric placement), with a ground/reference electrode on the iliac crest.
- Signals are recorded during three experimental conditions (baseline, two-strap backpack, single-strap backpack), each with a defined pre-recording stabilization period followed by a one-minute recording window.

**Processing and analysis layer**
- Raw sEMG signals are conditioned using band-pass and notch filtering to remove line interference and out-of-band noise.
- Filtered signals are smoothed using an RMS moving window.
- Average RMS values are computed per condition and per channel (left and right upper trapezius).
- The Muscular Asymmetry Index (MAI) is computed from the paired RMS values to quantify bilateral asymmetry per condition and participant.
- Frequency-domain characterization (FFT, Welch periodogram) is used to confirm that signal energy is concentrated within the expected sEMG frequency band.

<!-- TODO: Add architecture diagram illustrating acquisition -> filtering -> RMS/MAI computation -> analysis -->

The paper does not describe a distinct host/local interface layer, cloud layer, wireless communication protocol, or biofeedback mechanism; these should be marked as TODO if adopted in future iterations of the project.

---

## Hardware

| Component | Purpose | Module / Location |
|---|---|---|
| BITalino (PLUX) acquisition unit | Two-channel bilateral sEMG signal acquisition | Worn by participant during recording |
| Ag/AgCl surface electrodes (×2 channels, bilateral) | Bilateral sEMG signal detection | Upper trapezius, bilaterally, at clavicle height (symmetric placement, SENIAM protocol) |
| Ground/reference electrode | Reference for sEMG signal acquisition | Iliac crest |
| Standardized backpack | Standardized external load application | 6 kg load, two-strap and single-strap (dominant side) configurations |
| Overhead handrail / elevated tube | Simulated public transport standing support | Held overhead by standing participant during load conditions |

<!-- TODO: Specify exact BITalino model/version, electrode brand, sampling rate, and ADC resolution if available -->

---

## Signal Processing Pipeline

The signal processing chain described in the paper follows the standard sEMG conditioning workflow:

1. **Raw sEMG acquisition**: Bilateral upper trapezius signals recorded via BITalino during each experimental condition (baseline, two-strap backpack, single-strap backpack), one minute of recording per condition.
2. **Band-pass filtering**: Applied to isolate the physiologically relevant sEMG frequency content.
3. **Notch filtering**: Applied to remove line interference (powerline noise).
4. **RMS moving-window smoothing**: The filtered signal is smoothed using a moving RMS window.
5. **RMS computation**: The Root Mean Square is computed by squaring each sample of the signal, averaging the squared values, and taking the square root of the result. RMS quantifies the energy of muscular activity and enables objective comparison of activation intensity between a muscle pair. Higher RMS values indicate greater signal amplitude and, consequently, greater recorded muscular activation.
6. **Average RMS per condition and channel**: RMS values are computed and averaged separately for each condition (baseline, two-strap, single-strap) and each channel (left and right upper trapezius).
7. **Muscular Asymmetry Index (MAI) computation**: Bilateral asymmetry between the left and right upper trapezius is quantified using:
   
   Expressed textually:

   ```
   MAI = ((RMS_greater - RMS_lesser) / RMS_greater) * 100
   ```

   where `RMS_greater` and `RMS_lesser` denote the higher and lower RMS values, respectively, between the left and right upper trapezius for a given condition. A lower MAI value indicates greater symmetry between the trapezius muscles, while a higher value indicates greater bilateral imbalance.

9. **Frequency-domain validation**: Fast Fourier Transform (FFT) and Welch periodogram analysis are applied post-filtering to verify that the majority of signal energy is concentrated within the expected sEMG frequency band (20–150 Hz).

No amplitude normalization method (e.g., %MVIC or %MVC), feature extraction for classification, or signal transmission/storage protocol is described in the paper.

---

## Installation

```bash
python -m venv venv
source venv/bin/activate      # En Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Execution

```bash
streamlit run app.py
```
La aplicación se abrirá automáticamente en el navegador
(por defecto en `http://localhost:8501`).
---

## Usage

Based on the experimental protocol described in the paper, the system is used as follows:

1. Attach bilateral Ag/AgCl surface electrodes over the upper trapezius (clavicle height, symmetric placement) following the SENIAM protocol, and place a ground electrode on the iliac crest.
2. Record a one-minute **baseline** sEMG signal with the participant seated, at rest, and unloaded.
3. Have the participant stand while holding an elevated overhead handrail (simulating a public transport bus), wearing a standardized 6 kg **two-strap backpack**. Allow one minute of unrecorded stabilization in this position, followed by one minute of sEMG recording.
4. Allow a two-minute seated rest period without the backpack.
5. Repeat the standing protocol with the backpack reconfigured to a **single strap on the dominant side**, again allowing one minute of unrecorded stabilization followed by one minute of sEMG recording.
6. Apply the signal processing pipeline (band-pass filtering, notch filtering, RMS smoothing) to each recorded segment.
7. Compute average RMS per condition and channel, and derive the MAI for each condition and participant.
8. Compare RMS and MAI values across conditions (baseline, two-strap, single-strap) and between participant groups (habitual public transport users versus habitual private transport users).

<!-- TODO: Add example commands / scripts once the processing codebase is published -->

---

## Validation

**Study design**: Observational, comparative pilot study.

**Sample**: n = 5 participants (4 men, 1 woman), all seventh-cycle students at Universidad Peruana Cayetano Heredia (La Molina), divided into two groups:

| Group | Participant ID | Age | Transport frequency |
|---|---|---|---|
| Habitual public transport | PUBL1 (AV) | 22 | 3–4 days/week, 4 h/week |
| Habitual public transport | PUBL2 (AF) | 20 | 5–6 days/week, 3 h/week |
| Habitual private transport | PRIV1 (RB) | 20 | 2–3 days/week |
| Habitual private transport | PRIV2 (AP) | 20 | 3–4 days/week |
| Habitual private transport | PRIV3 (AL) | 20 | 3–4 days/week |

**What was evaluated**: Bilateral upper trapezius RMS and Muscular Asymmetry Index (MAI) across three load conditions (baseline, two-strap backpack, single-strap backpack) for each participant, compared between the public and private transport groups.

**Results**:

| ID | Condition | RMS left | RMS right | MAI (%) |
|---|---|---|---|---|
| PUBL1 | Baseline | 0.004362 | 0.011370 | 89.10 |
| PUBL1 | Two-strap | 0.105219 | 0.050098 | 70.98 |
| PUBL1 | Single-strap | 0.068343 | 0.063203 | 7.81 |
| PUBL2 | Baseline | 0.003655 | 0.000826 | 126.28 |
| PUBL2 | Two-strap | 0.003857 | 0.000823 | 129.66 |
| PUBL2 | Single-strap | 0.013981 | 0.066526 | 130.53 |
| PRIV1 | Baseline | 0.003647 | 0.003499 | 4.13 |
| PRIV1 | Two-strap | 0.027248 | 0.090361 | 107.33 |
| PRIV1 | Single-strap | 0.048160 | 0.010504 | 128.38 |
| PRIV2 | Baseline | 0.034712 | 0.032522 | 6.51 |
| PRIV2 | Two-strap | 0.004563 | 0.008761 | 63.02 |
| PRIV2 | Single-strap | 0.004633 | 0.027452 | 142.24 |
| PRIV3 | Baseline | 0.004113 | 0.003933 | 4.47 |
| PRIV3 | Two-strap | 0.004762 | 0.007837 | 48.82 |
| PRIV3 | Single-strap | 0.021423 | 0.022904 | 6.69 |

Key observations reported in the paper:

- Baseline MAI was markedly higher for the public transport group (PUBL1 = 89.10%, PUBL2 = 126.28%) than for the private transport group (4.13%–6.51%). Because baseline was recorded seated, at rest, and unloaded, the authors attribute this difference primarily to a possible signal acquisition artifact (e.g., partial electrode detachment for PUBL2) rather than to a persistent asymmetric muscular tone attributable to habitual public transport exposure.
- Private transport users generally showed the expected pattern of progressively increasing asymmetry as the load became more asymmetric (PRIV1: 4.13% to 107.33% to 128.38%; PRIV2: 6.51% to 63.02% to 142.24%), with PRIV3 as a notable exception (48.82% to 6.69%).
- Public transport users showed two distinct patterns: PUBL2 maintained a high and stable asymmetry across all three conditions (126.28% to 129.66% to 130.53%), while PUBL1 showed a progressive decrease in asymmetry (89.10% to 70.98% to 7.81%), becoming the participant with the lowest asymmetry of the entire study under the highest-asymmetry load condition (single-strap).
- FFT and Welch periodogram analysis confirmed that the majority of acquired sEMG signal energy fell within the expected 20–150 Hz band.

The authors emphasize that the MAI pattern was not uniform across backpack configurations or between groups, and identify this heterogeneity — rather than a confirmed group effect — as the most relevant finding of the pilot study. Results should be interpreted as preliminary and hypothesis-generating rather than confirmatory, given the small sample size and potential signal acquisition artifacts.

---

## Current Limitations

The following limitations are explicitly stated in the source paper:

- Small sample size (n = 5), which precludes establishing causal relationships or generalizing the observed asymmetry patterns.
- Heterogeneity between participants within the same group (e.g., PUBL1 versus PUBL2, or PRIV3 versus the rest of the private transport group), suggesting that individual factors (dominant side, specific frequency/type of transport exposure, prior postural strategies) may influence results as much as, or more than, the group variable itself.
- Possible signal acquisition artifacts, specifically suspected partial electrode detachment for participant PUBL2, which may explain an elevated baseline asymmetry not attributable to physiological factors.
- Load conditions were not randomized in order, and no extended rest period was implemented between trials beyond the specified two-minute rest, so an accumulated fatigue effect or task familiarization effect cannot be ruled out.
- Only the upper trapezius (and, in the introduction/discussion, references to erector spinae from prior literature) was targeted; the number of evaluated muscle groups was limited.
- No amplitude normalization (e.g., %MVIC/%MVC) was applied to the acquired signals.

---

## Future Work

Roadmap items derived from the paper's discussion and conclusion sections:

- [ ] Increase sample size to enable statistically robust and generalizable conclusions.
- [ ] Randomize the order of load conditions (baseline, two-strap, single-strap) across participants.
- [ ] Implement stricter signal quality verification procedures to detect and mitigate electrode detachment or acquisition artifacts.
- [ ] Expand the number of evaluated muscle groups beyond the upper trapezius (e.g., erector spinae).
- [ ] Adopt longitudinal study designs to assess whether observed neuromuscular strategies translate into long-term musculoskeletal fatigue or pain.
- [ ] Further investigate whether habitual transport mode (public versus private) is a determining factor in neuromuscular control strategies for trunk stabilization during load carriage.

---

## License

<!-- TODO: Confirm final license selection with all authors before publishing -->

For the software components of this repository (signal processing scripts, analysis notebooks), an **MIT License** is recommended. It is a permissive, widely adopted license in the open-source biomedical engineering and research software community, imposes minimal restrictions on reuse, and facilitates adoption by both academic and industry collaborators.

No custom hardware designs (schematics, PCB layouts, enclosures) are described in the source paper — the study uses a commercial off-the-shelf BITalino (PLUX) acquisition device. If custom hardware artifacts are added to this repository in the future, a **CERN Open Hardware Licence (CERN-OHL)** is recommended for those components, as it is purpose-built for open hardware documentation and design files.

For non-code research outputs (documentation, figures, derived datasets), a **Creative Commons Attribution 4.0 (CC BY 4.0)** license is recommended to ensure proper attribution while allowing reuse for research and educational purposes.

---

## Authors

| Name | Affiliation | Contact |
|---|---|---|
| Renzo Alvaro Bazalar Gutierrez | Facultad de Ciencias e Ingeniería, Universidad Peruana Cayetano Heredia, Lima, Perú | renzo.bazalar@upch.pe |
| Andre Vallejo Canchanya | Facultad de Ciencias e Ingeniería, Universidad Peruana Cayetano Heredia, Lima, Perú | andre.vallejo@upch.pe |
| Leonardo Gabriel Samillan García | Facultad de Ciencias e Ingeniería, Universidad Peruana Cayetano Heredia, Lima, Perú | leonardo.samillan@upch.pe |
| Enmanuel Vega Jauregui | Facultad de Ciencias e Ingeniería, Universidad Peruana Cayetano Heredia, Lima, Perú | enmanuel.vega@upch.pe |
| Yandra Melissa Purisaca Tesen | Facultad de Ciencias e Ingeniería, Universidad Peruana Cayetano Heredia, Lima, Perú | yandra.purisaca@upch.pe |

---

## Acknowledgements

- Universidad Peruana Cayetano Heredia, Facultad de Ciencias e Ingeniería (La Molina campus), for institutional support of this pilot study.
- The five volunteer participants who took part in the sEMG data collection protocol.
- Electrode placement and sEMG acquisition procedures followed the **SENIAM** (Surface ElectroMyoGraphy for the Non-Invasive Assessment of Muscles) recommendations for sensor placement.
- The Muscular Asymmetry Index (MAI) methodology applied in this study is based on the asymmetry quantification approach proposed by Castagneri et al. (2019), *IEEE Transactions on Neural Systems and Rehabilitation Engineering*.

<!-- TODO: Add funding source or grant acknowledgement if applicable -->

## Live Demo

Try the application directly in your browser without any installation.

**Web Application:** https://semgineers.streamlit.app/

> The online version is deployed using Streamlit Community Cloud and includes the complete interactive interface for EMG visualization, signal processing, spectral analysis, bilateral asymmetry assessment, and CSV export.
