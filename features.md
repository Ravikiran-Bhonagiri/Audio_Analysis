# **Audio Feature Extraction for Industrial Fan Anomaly Detection**

This writeup explains the features extracted for audio analysis of **industrial fan sounds** to detect anomalies. The features are grouped into different categories: time-domain, frequency-domain, harmonic, and statistical features.

---

## **1. Zero Crossing Rate (ZCR)**  
- **Description:** ZCR represents the rate at which the signal changes its sign (crosses the zero amplitude axis).  
- **Formula:**  
  $$
  ZCR = \frac{1}{N-1} \sum_{n=1}^{N-1} \mathbb{1}(y[n] \cdot y[n-1] < 0)
  $$
  where $\mathbb{1}$ is an indicator function, and $N$ is the number of samples.
- **Use Case:** High ZCR indicates sharp transitions in the sound (e.g., percussive or noisy components), while low ZCR indicates smooth or continuous sound (e.g., hums).

---

## **2. Spectral Centroid**  
- **Description:** Represents the "center of mass" of the frequency spectrum. It indicates where the majority of the spectral energy is concentrated.
- **Formula:**  
  $$
  \text{Centroid} = \frac{\sum_{f} f \cdot S(f)}{\sum_{f} S(f)}
  $$
  where $S(f)$ is the spectral magnitude at frequency $f$.
- **Interpretation:**  
  - **Low values:** Indicate bass-heavy sounds or hums.  
  - **High values:** Indicate bright or high-pitched sounds (e.g., squeals, whistles).

---

## **3. Spectral Rolloff**  
- **Description:** The frequency below which a certain percentage (usually 85%) of the total spectral energy lies.  
- **Use Case:** Helps determine whether the sound is dominated by low or high frequencies. Anomalous fans may show shifts in rolloff due to mechanical wear.

---

## **4. Spectral Bandwidth**  
- **Description:** Measures the spread of frequencies around the spectral centroid, indicating how "wide" the frequency spectrum is.  
- **Formula:**  
  $$
  \text{Bandwidth} = \sqrt{\frac{\sum_{f} (f - \text{Centroid})^2 S(f)}{\sum_{f} S(f)}}
  $$
- **Interpretation:**  
  - **Narrow bandwidth:** Indicates pure tones (e.g., motor hum).  
  - **Wide bandwidth:** Indicates noise or mechanical failure sounds.

---

## **5. Root Mean Square (RMS) Energy**  
- **Description:** Represents the average power (energy) of the audio signal over time.  
- **Formula:**  
  $$
  \text{RMS} = \sqrt{\frac{1}{N} \sum_{n=1}^{N} y[n]^2}
  $$
  where $N$ is the number of samples, and $y[n]$ is the amplitude at sample $n$.
- **Interpretation:** Higher RMS values indicate louder sounds, while lower values indicate quieter audio.

---

## **6. Mel-Frequency Cepstral Coefficients (MFCCs)**  
- **Description:** MFCCs represent the short-term power spectrum of sound on a Mel scale, mimicking human auditory perception.  
- **Use Case:** Commonly used for speech and audio classification tasks.
- **Interpretation:**  
  - **MFCC 1:** Often corresponds to the overall energy in the signal.  
  - Higher-order MFCCs capture finer details like brightness and timbre.

---

## **7. Chroma Features (STFT)**  
- **Description:** Represents the energy distribution among 12 pitch classes (notes in the musical octave).  
- **Use Case:** Useful for detecting harmonic content.

---

## **8. Spectral Contrast**  
- **Description:** Measures the difference in amplitude between peaks (harmonic components) and valleys (noise).  
- **Interpretation:** Higher spectral contrast values indicate more dynamic sounds, while lower values indicate more uniform spectral energy.

---

## **9. Tonnetz (Tonal Centroid Features)**  
- **Description:** Represents harmonic relationships such as chords and keys.  
- **Use Case:** Useful for detecting subtle tonal shifts that may indicate mechanical imbalance or wear.

---

## **10. Onset Strength**  
- **Description:** Measures the sudden changes in energy, indicating the occurrence of transients (onsets of new events such as motor vibrations or impacts).  
- **Use Case:** Helps detect irregular impulses or impacts in fan sounds.

---

## **11. Harmonic and Percussive RMS**  
- **Description:** Separates the audio into harmonic (melodic/tonal) and percussive (rhythmic/transient) components.
  - **Harmonic RMS:** Energy of tonal components (e.g., motor hum).  
  - **Percussive RMS:** Energy of noise or impacts (e.g., rattling or knocking).

---

## **12. Pitch (Fundamental Frequency)**  
- **Description:** Represents the estimated fundamental frequency (pitch) of the sound.  
- **Use Case:** Changes in pitch may indicate worn bearings or other mechanical faults.

---

## **13. Tempo (BPM)**  
- **Description:** Represents the beats per minute (BPM) of the sound. In industrial sounds, irregular tempo or changes in periodicity may indicate anomalies.

---

## **14. Chromagram (CQT)**  
- **Description:** Similar to chroma features but uses a constant-Q transform for better resolution in detecting pitch-related changes.  
- **Use Case:** Useful for analyzing frequency shifts across different time frames.

---

## **15. Spectral Flatness**  
- **Description:** Measures how noise-like the sound is by comparing the geometric mean to the arithmetic mean of the power spectrum.  
- **Formula:**  
  $$
  \text{Spectral Flatness} = \frac{\text{Geometric Mean of } S(f)}{\text{Arithmetic Mean of } S(f)}
  $$
- **Interpretation:**  
  - **Low values:** Indicate tonal sound.  
  - **High values:** Indicate noise or broadband sound.

---

## **16. Spectral Entropy**  
- **Description:** Quantifies the randomness or complexity of the frequency spectrum.  
- **Use Case:** Anomalous sounds often have higher entropy due to irregular noise patterns.

---

## **17. Crest Factor**  
- **Description:** Ratio of the peak amplitude to the RMS value.  
- **Formula:**  
  $$
  \text{Crest Factor} = \frac{\text{Peak Amplitude}}{\text{RMS Value}}
  $$
- **Use Case:** High crest factors indicate sharp transient peaks (e.g., impacts or clanks).

---

## **18. Attack Time and Decay Time**  
- **Description:**  
  - **Attack Time:** Time taken for the signal to rise to its peak.  
  - **Decay Time:** Time taken for the signal to decay to its baseline.
- **Use Case:** Sudden increases or decreases in attack/decay times may indicate mechanical faults.

---

## **19. Skewness and Kurtosis**  
- **Description:**  
  - **Skewness:** Measures the asymmetry of the amplitude distribution.  
  - **Kurtosis:** Measures the "peakedness" of the amplitude distribution.
- **Use Case:** Helps detect deviations from normal amplitude distribution patterns caused by anomalies.

---

### **Summary:**
These features provide a comprehensive representation of the sound characteristics, capturing:
1. **Temporal changes:** Features like ZCR, RMS, and onset strength.
2. **Spectral properties:** Features like spectral centroid, bandwidth, and flatness.
3. **Harmonic vs percussive content:** Using harmonic/percussive RMS.
4. **Statistical properties:** Skewness and kurtosis help detect unusual patterns.
