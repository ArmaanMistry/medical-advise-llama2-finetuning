# Medical Advisor Chatbot
<p align="center">
  ⚠️ <strong> Project in Progress </strong> <br>
  >> <i> not yet completed </i>
</p>

This project involves fine-tuning the Llama2 model from Huggingface on the `lavita/ChatDoctor-HealthCareMagic-100k` dataset.

> The dataset contains 100k healthcare-related question-answer pairs. It includes real-world user questions posed to medical professionals and their corresponding answers. You can find the dataset [here](https://huggingface.co/datasets/lavita/ChatDoctor-HealthCareMagic-100k)

### 🔧 The Fine-tuned Model:

Since I was using Colab's GPU, I needed to be mindful of resource usage. To address this challenge, I implemented the following methods in the project:
- **4-bit Quantization:**
     This method reduces the model's memory footprint while maintaining both inference speed and accuracy by using 4-bit quantization.
- **LoRA (Low-Rank Adaptation):**
      LoRA is applied to fine-tune only specific layers of the model, such as projection layers, while keeping the core parameters frozen. This approach allows efficient fine-tuning with a smaller number of trainable parameters.

These settings enable the model to perform well in low-resource environments while maintaining the quality of its responses to medical questions.

## 🔄 Flow of the Agent
<img src="https://github.com/user-attachments/assets/4be8e9ef-5435-48f0-a8c9-606c7d1991d4" alt="download" height="500"/>

Explanation of the Flow:
1. **Start:** The conversation begins when the user submits a question.
2. **ask_user:** The system prompts users to provide their questions or input.
3. **check_medical:** The system analyzes the input to determine if the question is healthcare-related using Word2Vec similarity comparison.
    - If the query is medical, the flow moves to the ask_doctor node.
    - If not, the system checks for greeting intent.
4. **check_greeting:** If the system detects a greeting from the user, it moves to the ans_greeting node.
    - If the input is neither medical nor a greeting, it directs the user to a fallback response (static_idk_msg), where the system acknowledges that it doesn't understand the input.
5. **ask_doctor / ans_greeting / static_idk_msg:** Based on the user’s input, the system provides a response:
   - **ask_doctor:** For healthcare-related queries, the system gives medical advice.
   - **ans_greeting:** For greetings, the system replies with a greeting.
   - **static_idk_msg:** If the input is unclear, the system provides a message stating it doesn't understand the question.
6. **End:** Once the appropriate response is delivered, the conversation ends.
