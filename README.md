# Implementing a transformer model: Adapting BERT for audio embeddings
I used just the BERT model starting from the code provided in the official repo available [here](https://github.com/codertimo/BERT-pytorch/tree/master) adjusting it to accomplish the following tasks in the audio setting:
- **Audio generation**: In order to accomplish this task, the model is feed a sequence of audio embeddings produced by the VQ-VAE, which represents a small portion of an audio track. Such a sequence could be masked in the center, this way we can observe how BERT model fill in the gap. For example a sequence could be the following in which the two tokens SOA and EOA mark, respectively, the beginning and the end of the audio sequence.
$$\langle SOA\rangle, e_1, e_2,…, e_i ,\langle mask_1\rangle, \langle mask_2\rangle, …, \langle mask_k\rangle,e_{N-i-k}, …, e_N, \langle EOA \rangle $$

- **Stem separation**: In this case, we want to separate a stem instrument, e.g., a guitar, whose embeddings we denote with $e^G$, from the mixture, whose embeddings are denoted by $e^M$. So we feed the model a sequence like this:
$$\langle SOA\rangle e^M_1,…, e^M_{N_M},\langle SEP \rangle,e^G_{1}, e^G_2, …, e^G_{N_G} \langle EOA \rangle$$

# BERT Vocabulary
To train BERT, a vocabulary of tokens is first built. In our case, the tokens are simply the indeces of the embeddings produced by VQ-VAE.
