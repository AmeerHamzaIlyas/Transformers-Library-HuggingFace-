Hugging Face Transformers – Basic Notes

1. What is Transformers?

Transformers is a Python library developed by Hugging Face for working with pre-trained AI models.

It supports tasks such as:

- Text generation
- Text classification
- Translation
- Question answering
- Summarization
- Named Entity Recognition (NER)
- Image classification
- Speech recognition
- Multimodal AI

Install the library:

pip install transformers



2. Basic Model Workflow

The basic workflow is:

Hugging Face Model
       ↓
Load Model
       ↓
Load Tokenizer / Processor
       ↓
Provide Input
       ↓
Model Inference
       ↓
Output



3. What is a Pre-trained Model?

A pre-trained model is an AI model that has already been trained on a large dataset.

Instead of training a model from zero, we can download and use an existing model from Hugging Face.

Example:

from transformers import pipeline

generator = pipeline(
    "text-generation",
    model="gpt2"
)

result = generator("Artificial Intelligence is", max_new_tokens=30)

print(result)



4. Pipeline

"pipeline()" is the easiest way to use Transformers models.

Example:

from transformers import pipeline

classifier = pipeline("sentiment-analysis")

result = classifier("I love Artificial Intelligence!")

print(result)

Output will be similar to:

[{'label': 'POSITIVE', 'score': 0.99}]

Common Pipelines

text-generation
sentiment-analysis
text-classification
translation
summarization
question-answering
image-classification
automatic-speech-recognition
object-detection



5. Model

A model is the actual neural network that performs the AI task.

Example:

from transformers import AutoModel

model = AutoModel.from_pretrained("bert-base-uncased")

For a specific task, use the appropriate AutoModel class.

Example:

from transformers import AutoModelForSequenceClassification

model = AutoModelForSequenceClassification.from_pretrained(
    "bert-base-uncased"
)



6. Tokenizer

A tokenizer converts text into numbers/tokens that the model can understand.

from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")

text = "Hello, how are you?"

tokens = tokenizer(text)

print(tokens)

Conceptually:

Text
 ↓
Tokenizer
 ↓
Tokens / Token IDs
 ↓
Model
 ↓
Prediction



7. Auto Classes

Hugging Face provides "Auto" classes so we don't always need to know the exact model architecture.

Common classes:

AutoTokenizer
AutoModel
AutoModelForCausalLM
AutoModelForSequenceClassification
AutoModelForQuestionAnswering
AutoModelForImageClassification

Example:

from transformers import AutoTokenizer, AutoModel

model_name = "bert-base-uncased"

tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModel.from_pretrained(model_name)



8. "from_pretrained()"

"from_pretrained()" loads an existing model or tokenizer.

tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")

model = AutoModel.from_pretrained("bert-base-uncased")

The model can come from the Hugging Face Hub.



9. Text Generation

For text-generation models:

from transformers import pipeline

generator = pipeline(
    "text-generation",
    model="gpt2"
)

output = generator(
    "Machine learning is",
    max_new_tokens=50
)

print(output[0]["generated_text"])

Useful generation parameters:

max_new_tokens
temperature
top_k
top_p
do_sample
num_return_sequences

Example:

output = generator(
    "AI will change",
    max_new_tokens=50,
    temperature=0.7,
    top_p=0.9
)



10. Inference

Inference means using a trained model to produce an output.

Input
  ↓
Pre-processing
  ↓
Model
  ↓
Inference
  ↓
Output

Example:

result = classifier("This product is excellent!")

The model is not being trained here. It is simply making a prediction.



11. CPU vs GPU

Models can run on CPU or GPU.

CPU:

pipeline(
    "text-generation",
    model="gpt2",
    device=-1
)

GPU:

pipeline(
    "text-generation",
    model="gpt2",
    device=0
)

GPU is generally much faster for large AI models.



12. Using a Model Directly

Instead of using "pipeline()", we can directly use the tokenizer and model.

import torch
from transformers import AutoTokenizer, AutoModelForSequenceClassification

model_name = "distilbert-base-uncased"

tokenizer = AutoTokenizer.from_pretrained(model_name)

model = AutoModelForSequenceClassification.from_pretrained(
    model_name
)

text = "I like this course."

inputs = tokenizer(
    text,
    return_tensors="pt"
)

with torch.no_grad():
    outputs = model(**inputs)

print(outputs.logits)

This approach gives us more control than "pipeline()".



13. Pipeline vs Direct Model

Method| Best For
"pipeline()"| Beginners and quick experiments
"AutoModel"| More control
"AutoTokenizer"| Custom preprocessing
Direct PyTorch| Advanced applications
FastAPI + Model| Production/API deployment



14. Model Files

When a model is downloaded, it may contain files such as:

config.json
model.safetensors
tokenizer.json
tokenizer_config.json
special_tokens_map.json

Important:

- "config.json" → Model configuration
- "model.safetensors" → Model weights
- "tokenizer.json" → Tokenizer information
- "tokenizer_config.json" → Tokenizer configuration



15. Hugging Face Model Hub

Hugging Face provides a large collection of models.

A model repository generally contains:

Model
 ├── Model weights
 ├── Configuration
 ├── Tokenizer
 ├── Documentation
 └── License

Before using a model in a real project, always check its:

- License
- Model card
- Intended use
- Limitations
- Hardware requirements



16. Basic Project Structure

A simple Transformers project can look like:

transformers-project/
│
├── README.md
├── requirements.txt
├── app.py
├── model.py
├── inference.py
└── models/

For an API-based project:

Frontend
    ↓
FastAPI
    ↓
Transformers Model
    ↓
Inference
    ↓
Response



17. Requirements

Example "requirements.txt":

transformers
torch
accelerate
sentencepiece

Install:

pip install -r requirements.txt



18. Important Terms

Model

Neural network that performs the AI task.

Tokenizer

Converts text into tokens/numbers.

Pipeline

High-level API for quickly using models.

Inference

Using a trained model to generate predictions.

Pre-trained Model

A model already trained on a large dataset.

Fine-tuning

Training a pre-trained model further on a specific dataset/task.

Model Hub

Online repository where models are hosted.

GPU

Hardware that can accelerate AI model inference and training.


19. Recommended Learning Path

1. Install Transformers
        ↓
2. Use pipeline()
        ↓
3. Load a pre-trained model
        ↓
4. Understand tokenizer
        ↓
5. Understand model
        ↓
6. Run inference
        ↓
7. Learn generation parameters
        ↓
8. Use AutoModel
        ↓
9. Build FastAPI API
        ↓
10. Connect frontend
        ↓
11. Deploy application

20. Minimal Example

from transformers import pipeline

generator = pipeline(
    "text-generation",
    model="gpt2"
)

prompt = "Artificial Intelligence"

result = generator(
    prompt,
    max_new_tokens=30
)

print(result[0]["generated_text"])

Key Idea

Hugging Face Model
       +
Transformers Library
       ↓
Load Model
       ↓
Input
       ↓
Inference
       ↓
AI Output

This is the basic foundation for integrating Hugging Face pre-trained models into real-world Python applications.


