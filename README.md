# SpeakerVerification
Speaker Verification system implemented in JAVA.

This speaker verification system uses mel-frequency cepstral coefficients (MFCC) and a Dynamic Time Warping (DTW) algorithm to compute and compare voice features of an enrolled user to those of a user seeking verification.

Note: Currently, this system is sensitive to the loudness of a voice and ambient environment. Alsothe system is text-dependent (same phrase used to enroll must be used during verification).

# Usage

To be able to properly use this speaker verification system,
one needs to make sure they have access to a voice recording
device capable of producing PCM-encoded signal streams.
**Note: the PCM-encoding used must produce either IEEE float
      sequences of the sampled voice or IEEE double sequences.**

## Enrollment
1. Capture user's ID or any other form of identification that can easily be associated with the user's voice features
2. Record user's voice and retrieve the audio data as an IEEE double-precision floating-point array
If the recorded sequence is available only as an IEE single-precision floating-point array (float), then one must convert this array to a double array. **This can be accomplished by calling `edu.gatech.team4180.dsp.DSP.float_to_double_array(your float array)`**
3. Get voice features from the signal. This can done in the following manner:
**`edu.gatech.team4180.dsp.SpeakerFeatures reference = new edu.gatech.team4180.dsp.SpeakerFeatures(your double array containing samples of the voice signal);`**
4. Convert the obtained features into a format that can easily be saved into a file.
This can be done by calling: **`double[] savable_format = reference.toStorableArray();`** where `reference` was obtained from Step 3. 
5. Store the resulting feature array into a file.

Note: The feature array returned from Step 4 contains the features of the voice and some important metadata.

## Verification
1. Capture user's ID in the same manner as during enrollment
2. Record user's voice and retrieve the audio data as an IEEE double-precision floating-point array
If the recorded sequence is available only as an IEE single-precision floating-point array (float), then one must convert this array to a double array. **This can be accomplished by calling `edu.gatech.team4180.dsp.DSP.float_to_double_array(your float array)`**
3. Get voice features from the signal. This can done in the following manner:
**`edu.gatech.team4180.dsp.SpeakerFeatures test = new edu.gatech.team4180.dsp.SpeakerFeatures(your double array containing samples of the voice signal);`**
4. Load the reference features. This can be accomplished by first reading the saved features from the file to a double array; then use the overloaded constructor of the SpeechFeatures class to reconstruct the features from the array. `edu.gatech.team4180.dsp.SpeakerFeatures reference = new edu.gatech.team4180.dsp.SpeakerFeatures(array of features saved into the file)`
5. Compare the two feature sets. This can be done by calling `reference.compare(test)`. To learn about how to change the dissimilarity threshold value used in comparing the two feature sets, please refer to the documentation.



For further questions/suggestions/comments, please contact me at nyengele@gatech.edu.
