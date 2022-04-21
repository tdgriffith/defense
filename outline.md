# Title slide

# Outline

# 1. Intro and motivation
- Paradigm shift
- Improved sensing, path planning, decision making
- Lots of human to computer, less computer to human
- Automation conundrum and teaming, bi-directional flow
- Are you paying attention???


---

### Endsley quote
- Historically simulation questionnaire
- Sensors and modeling moving towards physiological measures of human state/cognition

---

### Cognition is the black box
- Improved modeling is needed
- Use canonical engineering approach
- Cognition acts on physiology, which is loosely tied to EEG

---

### State of the art
- Nonstationary signals make the ***dynamics*** tricky
- Phase and traveling waves
- This work seeks a method to address in engineering dynamics terms 
    - with eye towards cognitive outcomes

---

### Guardrails
What we're not saying:
- this models the brain
- this models the cellular activity

What we are saying
- Beam and atoms vs. brain waves and neurons

---

# 2. A Dynamic Systems view
- start to introduce the structure and approach

---

### Important EEG details
- EEG is only loosely tied to outcomes
- Linear, nonlinear, and noise
- Channel cross talk
- Variety of referencing techniques

---

### A canonical approach
- Have these difficult signals, nonlinear and not independent and nonstationary
- We impose this structure, consider $A(t)$

### level is an unsolved
- We can't not know everything
 - but we do
- SO
    - first identify the linear structure
    - ***around an operating point***
    - realizing that the unknown input and nonlinear leaks thru
    - uncertainty in A_m bc C_m would be equivalent

### treating nonlinear
- Lots of works says this is a nonlinear nonstationary system
- We introduce a nonlinear nonstationary estimator that updates the model in real time

### Modes elegantly capture
- Giant (A,B,C) isn't useful for analysis
- modal transform is equivalent
- similarity 
- yields discrete set of spatio-temporal modes which have...

---

# 3. Sys Id using EEG
With that overview, how do we extract that first step, the linear operating point...

### Considered algorithms
- We want to extract those ***linear*** patterns from the data
- Looked at 4 that give right structure
- For time, OMA only bc
    - classification
    - consistency
    - Numerical algorithm for Subspace State Space System IDentification

### OMA theory
- A discrete time plant looks like this
- If we knew size of C and initial condition... 
- So we vary the size and check SVD
    - ***FILLING IN THE DISTRIBUTION***

### Truncation
- We don't need to work with full order model
- about ***40-50 modes for EEG stuff***

### EX
- see that it works 
- see that it yields physically interesting models

---
# 4. Modal Analysis of Brain Wave Dynamics
- Remember, linear model of nonlinear system
    - Is it useful???
- Analysis

### Traveling vs standing
- When do waves reach peak?
- a function of uneven damping
- negative damping
- indicates different regions doing different tasks

### Common modes
- Find four out of 40 to be task independent

### Interindividual
- use modes to id individual 
- seem to act as a finger print
    - ***on our data***

### BUT
- they don't match the future dynamics
- if you can go back in time, vs forward

---
# 5. aUIO
we've got a problem. address with full architecture
***somewhat removed from EEG***

### Est overview
- u is exogenous, ***determenistic***, something modes can't generate
- v_x is a nonlinear, nonstationary
    - not restricting it to white 

### modeling ui
- it's too much to simply id the waveform
- select basis ***persistent*** based on engineering
- id coefs instead of waveform

### arch and estimator error
- recover A
    - update based on error
    - alpha is a filter on update
    - gamma_e is a tunable positive matrix
- know little about top 

### arch
- given ASD, stable transmission zeros you can find this 
- notice, bound on v and alpha define convergence rate

### lil example

---
# 6. Reconstructing the Brain’s Unknown Input 

### First things
***this really really works***

### it's bc of the adaptation in the modes

### details
- ui acts evenly, Linear ind and smearing
- sine cos is physically sig
- LQR gains

### curious
- modes from another person
- not any hurwitz, but any eeg modes
- ***you can tolerate some slop in the modes***
    - convergence is the primary effect

### classification
- We hypothesize 
    - modes are correlated with human state/cognition, so
    - same state should have similar modes, so
    - you can take the average modes in a state,
    - and the estimator will perform better than the other state
- DEAP dataset and self report
- binary and interindividual

### results
- on par with modern DL
- computation much less
- analysis much more
    - more than total lifetime footprint of 5 cars

---
# 7. Konks

--- 
# Ack
