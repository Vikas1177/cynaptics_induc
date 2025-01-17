# TASK - 3
This is a fine-tuned model for hypothetical conversation between two personas.
In scripts you can find my code for fine tuning - persona-chat-llm and code for inference - example_run.

## Aproach
### Choice of LLM
I have used Llama-3.2-1B model because-
1. With 1 billion parameters, Llama 3.2-1B is significantly smaller than larger models like Llama 3.2-7B or Llama 3.2-13B. This makes it more resource-efficient.
2. Requires less GPU/CPU memory for training and inference.
3. Fine-tuning is faster compared to larger models.
4. Faster response times during deployment, which is crucial for real-time applications.
5. While Llama 3.2-1B is smaller, it still benefits from the LLaMA architecture's efficiency.
6. Since my [dataset](https://huggingface.co/datasets/Cynaptics/persona-chat) contains 20k rows so smaller model avoids overfitting.

### Choice of fine-tuning method
I used unsloth for fine-tuning beacuse it makes fine-tuning more faster by applying 4-bit precision format.
I targetted the attention and feed forward layers of model which is best for LoRA training.
The ratio of lora_alpha and rank here is 1 which by experimenting works best for me.
Used Peft provided by usloth to update only a small subset of parameters which is efficient for fine-tuning.

### Justifications
Learning Rate: 2e-4 (chosen for stable convergence).
Batch Size: 2 (optimized for GPU memory constraints).
Epochs: 1 (Only in 1 epoch it gave desired results).

### [Link to model weight](https://huggingface.co/vikas117/Llama-3.2-1B-persona-chat)

### Text template for running
use example_run in scripts folder for running.
input_text = """Below is a persona information of a Person B, followed by a conversation between two individuals, Person A and Person B.
Please carefully consider the flow and context of the conversation below, and use the Person B's Persona information appropriately to generate a response that you think are
the most appropriate replying for Person B.

Persona: { My name is David and I'm a 35 year old math teacher.
 I like to hike and spend time in the nature.
 I'm married with two kids.
}
Conversation: {"persona_b" = [
    "I am most proud of my ability to connect with nature and animals.",
    "I have never been arrested, but my stories might make you think otherwise.",
    "i love family time.",
    "my parents both are school teachers.",
    "I'm afraid of being in a situation where I can't communicate with my wife."
],

"dialogue" = [
    "Persona A: I run every morning before work, it helps me to relieve stress.",
    "Persona B: I can see how that would help:,I do much hiking and camping; it helps me to clear my heade's up with nature.",
    "Persona A: That sounds like a lot of fun and I've always wanted to go camping!",
    "Persona B: It is really great and you should definitely try it sometime.",
    "Persona A: I will, as to my dogs - it would be lovely.",
    "Persona B: I bet he would. Also, we have dogs and his love goes camping with me",
    "Persona A: What kind of dog do you have?"
]}
"""
     
