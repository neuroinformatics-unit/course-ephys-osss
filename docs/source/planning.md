# Planning

(wrap up discussion is a nice idea)

This document contains a (tentative) plan for the course. Some general notes and thoughts on the course content:

- The focus is hands-on, with most of the time spend on them implementing / exploring the data and code
- During the coding periods, we will talk through the code step-by-step the core pipeline, and have periods
for those to do targetted exploration (e.g. 'Use get traces to get scaled and uscaled raw data', 'Plot data before and after whitening' etc.
The code will be presented through  Quarto, either through slides (e.g. here) or a book-like format (e.g. here). The benefit of the latter is we 
end up with a really nice handbook that should be generally useful. 
- There is likely to be people with a range of background and experience on the course. Therefore,
we can have stretch-objectives for the targetted exploration periods (e.g. Plot the fourier transform of the 
AP channel, of waveforms, etc.). Some advanced users may go ahead and complete the step-by-step core pipeline quickly 
so we can have a lot of extras for them to do.
- The coding periods will be interleaved with short (20-30 minute) lectuers to discuss the theory.
- We can anticipate that they can use Python through an IDE, install environments, packages etc. as they will have
completed an 'Introduction to Python' course prior, if necessary. However, they may be begginers, to either Python /
extracellular ephys / neuroscience. So we cannot assume any advanced computer science / neuroscience / DSP experience,
which is okay, we can still work with advanced concepts, we just need to build them from the ground-up and not assume knowledge.
- Their laptops may range in performance, where possible we should endeavour to use the smallest example data possible

## Monday Afternoon (2 - 5pm) : Introduction

**Goal:** : 
- Provide a high-level overview of the main concepts in electrophysiology,
of which we will fill in the details over the next few days. 
- Give a general introduction to SpikeInterface
- Provide a simple, full SpikeInterface pipeline that they can use for reference of the coming days

**Plan:**

*10:00 - 10:15* : Welcome, housekeeping, overview of the course, downloading the example data

*10:15 - 10:45* : A high-level introduction to extracellular electrophysiology:
- Purpose of electrophysiology recordings (+ some famous results)
- Probe evolution (tetrode to high-density.
- Introduction to the data (probe channels -> timeseries, time x channel data)
- Very brief overview of the pipeline (preprocessing, sorting, quality metrics). What they steps are,
why we do them and how they result in data that we use in papers.

*10:45 - 11:45* : Coding up a very simple pipeline and exploring the data.
- Quick introduction to SpikeInterface (e.g. history and purpose)
- Loading data in SpikeInterface
- Spikeinterface objects
- Loading and visualising the probe
- Visualising the raw data
- Implementing a simple preprocessing pipeline (phase shift, filter, CMR)

*11:45 - 12:05* : A deeper introduction to electrophysiological data
- ADC sampling, sampling theory (quick introduction to sine, cosine functions and the Fourier transform / Power spectrum)
- Saturation and bit depth

*12:05 - 13:00* :  Implement the rest of the pipeline (sorting, sorting analyzer, quality metrics)

(depending on how things are going, we could swap the last two, having a very long coding period and ending on the lecture)

**Example data required** 

A very short (1-2 s) recording that can be quickly run through the entire pipeline.

## Tuesday Morning (10am - 1pm) : Preprocessing

**Goal:**

They should have a good understanding of how to implement common and SOTA preprocessing
steps, and at least some intuition as to the underlying theory.

**Plan:**

*10:00-10:30* : Talk on preprocessing theory 
- phase shift, bandpass, CMR
- whitening
- drift correction
- running preprocessing steps in SpikeInterface vs. the sorter (e.g. kilosort)
- filter edge effects, chunking
- lazy data access
- always look at your data

*10:30 - 11:30* : Add whitening and drift correction to the pipeline. Visualise before vs. after.
Exploring motion outputs (e.g. drift maps)
If this is too much time, a stretch goal can be a quick talk on 
spatial highpass filter, and running it in SpikeInterface.

*11:30 - 12:00* : Lecture on advanced preprocessing (bad channel detection, 
raw data quality metrics, saturation detection)

*12:00 - 13:00* : Adding these steps to the pipeline.

**Example data required**

We could use the same as Monday, but for this data it's not necessary it needs to be sortable.
Maybe a good example for bad-channel detection, saturation or raw-data quality metrics would be good.
We could have a good example and a bad example.


## Tuesday Afternoon (2 - 5pm) : Sorting

**Goal:**

By the end of this session they should have a strong idea on the purpose of sorting, 
key concepts (spike times, unit assignment, templates, waveforms / snippets). 
Know the names of a few different sorters and how to compare them. 
Understand the possible approaches to multi-session recordings, gain experience with UnitMatch.

**Plan:**

*14:00 - 14:30* : Overview of sorting
- Why we need to do it
- The key outputs (spike times, unit assignment, templates (also can mention waveforms / snippets))
- It is a hard problem - many sorters exist
- We can use spikeinterface to run and compare various sorters

*14:30 - 15:30* : Run a couple of different sorters in spikeinterface and compare the outputs using sorting comparison.
We can leave it a little up to the user, but KS4 and Lupin seem a good pair to use in the example.
We can go into more detail here the options to run preprocessing steps in spikeinterface vs. the sorter,
as well as introduce sorting components.

*15:30 - 16:00* : Deep dive into the black box, the general steps behind a sorter 
(peak detection, clustering, template matching etc.)

*16:00 - 17:00*: UnitMatching
A 20-minute talk and 40 minute implementation?

**Example data required**

Here we can use short data that sorts quickly, but it would be nice if it wasn't all junk units.
We could try and use the same data as on Monday. 
For UnitMatching, I think the sorting outputs for two sessions would work. 

## Wednesday Morning (10am - 1pm) : Assessing Sorting Quality

**Goal:**

- Understand why we need to sort and key concepts (e.g. splits, merges)
- Understand a few of the main quality metrics
- Know how to compute / threshold quality metrics in SpikeInterface and 
perform manual curation in the spikeinterface-gui

**Plan:**

*10:00 - 10:30* : Introduction to assessing sorting quality
- Why we need to do it, splits and merges, good/noise/mua clusters
- Quality metrics, and some detail on the main ones (e.g. refractory period, amplitude cutoff, cluster space metrics)

*10:30 - 11:45* : Coding period
- use sorting analyzer to compute metrics
- using Bombcell through SpikeInterface
- using UnitRefine through SpikeInterface

*11:45 - 12:05* : Overview of SpikeInterface GUI (e.g. what the different plots mean)

*12:05 - 13:00* : walkthrough / free time to curate a dataset in spikeinterface-gui


**Example data required**

We will need a small toy dataset that they can quickly create and run a sorting analyzer on.
But it should have a few good units, so will be as small as possible while being useful.
for spikeinterface-GUI, we can just the sorting output of a larger dataset.

## Wednesday Afternoon (2 - 5pm) : Analysing Outputs

**Plan:**

Very open here, something like:

- 20-30 minute talk on electrophysiology analysis. Some real use cases / papers
- 20 minutes on walkthrough time alignment
- 30 minutes: give a sorting output and some behavioural event times, construct a histogram 'by hand'
- rest of the session (~2h) on using pynapple?
- 
**Example data required**

**Goal:**




```{toctree}
:maxdepth: 2
:caption: Sections

```
