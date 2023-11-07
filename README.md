## Question-Answering-System--NER-model

Encompasses the development of a Named Entity Recognition (NER) system using transformer-based models, focusing on ALBERT, RoBERTa, and DistilBERT architectures. The project begins with the installation of essential libraries such as transformers, datasets, tokenizers, and seqeval. After that, it loads the ConLL 2003 dataset, a widely used dataset for NER tasks, and examines its structure. The code then utilizes a BERT-based tokenizer for tokenizing text inputs. A custom function tokenize_and_align_labels is defined to align tokens with their respective labels, incorporating logic to handle sub-words and special tokens. This function is then applied to the entire dataset. The model architecture for token classification is selected and fine-tuned using transfer learning on the processed data. Training arguments and metrics for evaluation are specified, followed by the training process using the Trainer class from the transformers library. The trained model is saved along with its associated tokenizer and configuration. Finally, the model is loaded for inference, and a named entity recognition pipeline is created to extract entities from provided text examples. The results are then printed, demonstrating the effectiveness of the NER system. This provides a comprehensive framework for training and deploying NER models using transformer-based architectures.
 
#Introduction
The amount of data being generated in today’s world has risen tenfold in the past couple of years. This ever-growing data contains everything from transactional data, research data, social media posts, and open-source information. Much of this data is unstructured and majorly text. With such a vast resource, searching for specific information on the web has also become a cumbersome task. A solution to this problem is a Question Answering System which has applications in customer support, Legal QA, conversational chatbots, and also getting instant answers to questions over search. Question Answering (QA) is the task of finding an answer to a posed question from a given context if it’s provided. Question Answering systems allow users to pose a question and get an answer from the respective document or article. QA systems are mainly of 2 types namely, Extractive Question Answering where answers are extracted from the given context and Generative Question Answering where a newly generated text serves as the answer for the posed. A typical approach to develop a QA system has been using rule-based systems, Information retrieval systems, Machine Learning based approaches, and neural network-based approaches such as RNNs, and CNNs. But a major downside of these methods was their inability to handle long range text sequences and contextual understanding. With the development of Transformer Models based on self-attention mechanism that enables models to capture log-term dependencies and contextual relationships in unstructured text. For this project, we implement Transformer based models namely, ALBERT, RoBERTa, and DistilBERT to develop a Question Answering System. The models are trained and evaluated on the training and evaluation set of the SQuAD 2.0 dataset. The mentioned models were chosen for their low computational requirements and high performance relative to state-of-art Large Language models like BERT, GPT, LLaMA, etc. These models have initially been trained on large amounts of text data using unsupervised pre-training mainly on 2 tasks, Masked Language Modelling and Next Sentence Prediction. These pre-trained models enable transfer learning as these pre-trained models can then be fine-tuned on specific downstream NLP tasks such as Question answering. To enable model training, new features such as answer start and answer end were created. Following this, tokenization and encoding using the AutoTokenizer function using the base versions of the pre-trained models was carried out. The models were then trained utilizing the AdamW optimizer with weight decay and a lookahead wrapper optimizer and then evaluated on the valid set.

2.1 DistilBERT
DistilBERT is a smaller version of BERT developed by Google. Main difference between BERT and DistilBERT is the Size and Computation Resources they use. DistilBERT is nearly half the size of the BERT and require few computation resources to train and run.

BERT:
BERT stands for Bidirectional Encoder Representation from Transformers is a Pre trained NLP model developed by Google in 2018. BERT is based on Transformer architecture which is an attention mechanism that learns contextual relationships between words in a text. BERT is Pretrained on large Unsupervised Data using two tasks: Masked Language Modeling (MLM) and Next Sentence Prediction (NSP). In MLM tasks BERT learns to predict masked word in a sentence using surrounding words, in NSP task the model learns to predict if two sentences are consecutive or not. This allows BERT to learn complex patterns which can be fine-tuned for specific NLP tasks like Question Answering System. BERT uses two special types of token inputs [CLS] and [SEP]. [CLS] is there to represent sentence level classification and is used when classifying. [SEP] is used to separate two pieces of text. BERT also uses Segment Embeddings to differentiate a question from text and Position Embeddings that helps in positioning the words in sequence. These three are the inputs to the first layer. The Output of these Transformer Layers is the word embeddings that are multiplied by weight vectors and passed on to SoftMax Function to get the probability distribution of all the words. The word with the highest probability is assigned as the Start word. Similar process is followed to generate probability distribution of End word.

2.2 ALBERT (A Lite BERT)
ALBERT is the variant of BERT developed to reduce limitations of BERT like the computation and memory requirements. ALBERT Specifically implement two parameter reduction techniques to reduce computation and increase performance. Factorized Embedding Parameterization: ALBERT divides the embedding matrix into two pieces to ensure the size of hidden layers and embedding dimensions are different. This increases the size of hidden layer without modifying the size of embedding dimension. Alberta adds a linear layer to the embedding matrix after the embedding phase is done. Cross Layer Parameter Sharing: Alberta has 12 encoder blocks each that shares all the parameters. This process reduces the parameter size and also adds regularization to the model. In Alberta masked inputs are generated using n-gram masking with maximum n-gram span of 3. Alberta also uses Sentence Order Prediction (SOP) rather than NSP that helps in achieving the goal better.

2.3 ROBERTa (Robustly Optimized BERT)
Roberta is developed by Facebook AI as an improved version of BERT. Roberta differs from BERT in the following aspects. Training Data: Roberta uses 160GB of text for pre-training which is more than what BERT is trained on. Pretraining Duration: Training Process of Roberta is longer and uses more Optimization Steps which contributes to improved performance. Training Batch Size: Roberta uses larger batch sizes during training which helps in achieving more stable gradients and better model convergence. Byte-Pair Encoding: Roberta uses Byte-Pair Encoding for tokenization which is more efficient to handle out-of vocabulary words compared to Word Piece tokenization used by BERT.
