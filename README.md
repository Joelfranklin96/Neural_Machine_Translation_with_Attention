# Neural Machine Translation with Attention

1) Neural Machine Translation with Attention model has been built for the date translation task where the (input,ouput) pairs are as follows :-
 ('27 november 1980', '1980-11-27')
 ('friday september 13 2019', '2019-09-13')
 ('tuesday july 17 2018', '2018-07-17')
 ('4/10/19', '2019-04-10')
2) The model consists of 2 components - Encoder and Decoder.
3) The Encoder is a Pre-Attention Bidirectional-LSTM which takes the entire input sequence (human-readable date) as input and returns a sequence of hidden states.
4) The Decoder is a Post-Attention LSTM which generates the output sequence (machine-readable date) one timestep at a time using a context vector derived from the Attention mechanism.
5) One of the important aspects of the model is the Attention mechanism. The attention mechanism helps to generate the output by paying more attention to relevant parts of the input.
6) Attention Mechanism
- Calculating Intermediate Energies 'e': The intermediate energies 'e' are calculated using a small neural network (a Dense layer), which takes as input a concatenated vector of the encoder's hidden state and the     decoder's previous hidden state. Specifically, for each timestep 't' in the encoder's output, the hidden state 'a<t>' is concatenated with the decoder's previous hidden state 's<t-1>', and this concatenated         vector is fed into the Dense layer. The output of this Dense layer, 'e', represents the "intermediate energies" between the encoder states and the current decoder state.
  
- Calculating 'Energies': The 'energies' are obtained by passing the intermediate energies 'e' through another small neural network (another Dense layer), which further processes them to produce a single scalar       value for each timestep of the encoder's output. This scalar represents the unnormalized attention score for each encoder state, indicating its relevance to the current decoder state.

- Calculating 'Alphas' (Attention Weights): The 'alphas', or attention weights, are calculated by applying a softmax function to the 'energies'. The softmax function ensures that all attention weights sum up to 1     and that they are normalized between 0 and 1. These weights represent the degree to which each encoder state should contribute to the decoder's current state, essentially showing where the decoder should pay        attention in the encoder's output.

- Calculating 'Context' Vector: The 'context' vector is the weighted sum of the encoder's hidden states, with the weights being the attention weights 'alphas'. For each encoder state, its hidden state 'a<t>' is       multiplied by its corresponding attention weight. The resulting vectors are then summed up across all timesteps to produce the 'context' vector. This 'context' vector serves as a summary of the encoder output,      focusing on the parts that are most relevant to the current timestep in the decoder. It is then used in the decoder's subsequent computations for generating the output.
