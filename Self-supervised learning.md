https://ai.facebook.com/blog/self-supervised-learning-the-dark-matter-of-intelligence/

## Self-supervised learning: The dark matter of intelligence ##

Supervised learning is a bottleneck for building more intelligent generalist models that can do multiple tasks and acquire new skills without massive amounts of labeled data.

A working hypothesis is that generalized knowledge about the world, or common sense, forms the bulk of biological intelligence in both humans and animals. In a way, common sense is the dark matter of artificial intelligence.

We believe that self-supervised learning (SSL) is one of the most promising ways to build such background knowledge and approximate a form of common sense in AI systems.

  -Natural Language Processing (NLP), Collobert-Weston, Word2Vec, GloVe, fastText
  
  -BERT, RoBERTa, XLM-R

Our latest research project SEER leverages SwAV and other methods to pretrain a large network on a billion random unlabeled images, yielding top accuracy on a diverse set of vision tasks. This progress demonstrates that self-supervised learning can excel at CV (ComputerVision) tasks in complex, real-world settings as well.

## Self-supervised learning is predictive learning ##

Self-supervised learning obtains supervisory signals from the data itself, often leveraging the underlying structure in the data.

Unsupervised learning is an ill-defined and misleading term that suggests that the learning uses no supervision at all. In fact, self-supervised learning is not unsupervised, as it uses far more feedback signals than standard supervised and reinforcement learning methods do.

## Self-supervised learning for language versus vision ##

It is considerably more difficult to represent uncertainty in the prediction for images than it is for words. When the missing word cannot be predicted exactly, the system can associate a score or a probability to all possible words in the vocabulary.

We do not know how to efficiently represent uncertainty when we predict missing frames in a video or missing patches in an image. We cannot list all possible video frames and associate a score to each of them, because there is an infinite number of them.

New SSL techniques such as SwAV are starting to beat accuracy records in vision tasks. This is best demonstrated by the SEER system that uses a large convolutional network trained with billions of examples.

## Modeling the uncertainty in prediction ##

In CV, the analogous task of predicting 'missing' frames in a video, missing patches in an image, or a missing segment in a speech signal involves a prediction of high-dimensional continuous objects rather than discrete outcomes. 

There are an infinite number of possible video frames that can plausibly follow a given video clip. It is not possible to explicitly represent all the possible video frames and associate a predcition score to them.

In fact, we may never have techniques to represent suitable probability distributions over high-dimensional continuous spaces, such as the set of all possible video frames.

## A unified view of self-supervised methods ##

An EBM (energy-based model) is a trainable system that, given two inputs, x and y, tells us how incompatible they are with each other. To indicate the incompatibility between x and y, the machine produces a single number, called an energy. If the energy is low, x and y are deemed compatible; if it is high, they are deemed incompatible.

Training an EBM consists of two parts:

1. Showing examples of x and y that are compatible and training it to produce a low energy.

2. Finding a way to ensure, that for a particular x, the y values that are incompatible with x produce a higher energy than the values that are compatible with x.

### Joint embedding, Siamese networks ###

A particular well-suited deep learning architecture to do so is the so-called Siamese networks or joint embedding architecture.

A joint embedding architecture is composed of two identical (or almost identical) copies of the same network. The networks produce output vectors (embeddings), which represent x and y. A third module, joining the networks at the head, computes the energy as the distance between the two embedding vectors.

The parameters of the networks can easily be adjusted so that their outputs move closer together. This will ensure that the network will produce nearly identical representations (or embeddings) of an object, regardless of the particular view of that object.

The difficulty is to make sure that the networks produce high energy, i.e. different embedding vectors, when x and y are different images. Without a specific way to do so, the two networks could happily ignore their inputs and always produce identical output embeddings. This phenomenon is called a collapse. When a collapse occurs, the energy is not higher for nonmatching x and y than it is for matching x and y.

### Contrastive energy-based SSL ###

Contrastive methods are based on the simple idea of constructing pairs of x and y that are not compatible, and adjusting the parameters of the model so that the corresponding output energy is large.

Contrastive methods have a major issue: They are very inefficient to train. In high-dimensional spaces such as images, there are many ways one image can be different from another. Finding a set of contrastive images that cover all the ways they can differ from a given image is a nearly impossible task.

### Non-contrastive energy-based SSL ### 

Non-contrastive methods applied to joint embedding architectures is possibly the hottest topic in SSL for vision at the moment. The domain is still largely unexplored, but it seems very promising.

Non-contrastive methods for join-embedding include DeeperCluser, ClusterFit, MoCo-v2, SwAV, SimSiam, Barlow Twins, BYOL from DeepMind and a few others. They use various tricks, such as computing virtual target embeddings for groups of similar images or making the two joing embedding architectures slightly different through the architecture or the parameter vector.

Perhaps a better alternative in the long run will be to devise non-contrastive methods with latent-variable predictive models.

The challenge of the next few years may be to devise non-contrastive methods for latent-variable energy-based model that successfully produce good representations of image, video, speech and other signals and yield top performance in downstream supervised tasks without requiring large amounts of labeled data.

## Advancing self-supervised learning for vision ##

Most recently, we've created and open sourced a new billion-parameter self-supervised CV model called SEER that's proven to work efficiently with complex, high-dimensional image data. It is based on the SwAV method applied to a convolutional network architecture (ConvNet) and can be trained from a vast number of random images without any metadata or annotations.

