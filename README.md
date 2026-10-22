[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on005489-blue)](https://doi.org/10.82901/nemar.on005489)

### Free Recall with Open-Loop Stimulation at Encoding

#### Description
This dataset contains behavioral events and intracranial electrophysiological recordings from a delayed free recall task with open-loop stimulation at encoding.  The experiment consists of participants studying a list of words, presented visually one at a time, completing simple arithmetic problems that function as a distractor, and then freely recalling the words from the just-presented list in any order.  The data was collected at clinical sites across the country as part of a collaboration with the Computational Memory Lab at the University of Pennsylvania.  This dataset is an open-loop stimulation version of the [FR1](https://openneuro.org/datasets/ds004789) dataset.

This study contains open-loop electrical stimulation of the brain during encoding.  There is no stimulation during the distractor or retrieval phases.  Stimulation is delivered to a single electrode at a time, with locations chosen in the hippocampus and entorhinal cortex.  Stimulation parameters are included in the behavioral events tsv files, denoting the anode/cathode labels, amplitude, pulse frequency, pulse width, and pulse count.  

20 of the 25 lists in a session are randomly assigned as stimulation lists.  On these lists, stimulation occurs on alternating two-word blocks, meaning 6 of the 12 words are presented with stimulation.  Stimulation starts 200 ms prior to the onset of the first word in the block and lasts for 4.6 seconds, ending 200-450 ms after the offset of the second word (depending on the inter-stimulus interval).  Half of the stimulation lists begin with a stimulation on pair and half begin with a stumulation off pair, but the order of these conditions is random.  A stimulation list that begins with a stimulation on pair would look as follows (with bold indicating stimulation):

**1 - 2** | 3 - 4 | **5 - 6** | 7 - 8 | **9 - 10** | 11 - 12


#### To Note
* The iEEG recordings are labeled either "monopolar" or "bipolar."  The monopolar recordings are referenced (typically a mastoid reference), but should always be re-referenced before analysis.  The bipolar recordings are referenced according to a paired scheme indicated by the accompanying bipolar channels tables.
* Each subject has a unique montage of electrode locations.  MNI and Talairach coordinates are provided when available.
* Recordings done with the Blackrock system are in units of 250 nV, while recordings done with the Medtronic system are estimated through testing to have units of 0.1 uV.  We have completed the scaling to provide values in V.

#### Contact
For questions or inquiries, please contact sas-kahana-sysadmin@sas.upenn.edu.

## Channel names follow the data headers (18 Oct 2026)

In 2 recordings the channel list of channels.tsv did not equal the data-file header (names, order or count). In the 2 with a different channel count, `mne_bids.read_raw_bids` warned and kept the header names, so the channels.tsv types and bad-channel status reached only the channels whose names happen to be identical; a reader that applies the channels.tsv rows by position gives wrong labels wherever the two lists are not aligned. Since 18 Oct 2026 every channels.tsv lists exactly the header channels, in header order, with the header names (MNE names: duplicated header labels numbered -0, -1).

Rows were matched to header channels BY NAME, never by position (exact; then case/whitespace; then the recorder prefix 'EEG '/'POL ', '_' and zero padding; then a trailing '-<reference>' token). Matched rows keep all their columns (type, units, status, ...); 0 rows took the header name.

2 channels.tsv rows had no channel in the data file (2 files) and were removed; they are kept verbatim under `sourcedata/channels-removed-2026-10-18/` (same relative path). Examples: `sub-R1006P_ses-0_task-FR2_acq-bipolar_ieeg.edf`: P2-P6; `sub-R1006P_ses-1_task-FR2_acq-bipolar_ieeg.edf`: P2-P6.

Applied by position, the former rows would have given wrong labels to 40 channels in 2 files (rows missing, extra or out of order before that position).
