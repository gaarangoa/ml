## Docker for model Search from google

Download the forked version from here: https://github.com/gaarangoa/model_search

Inside your project folder containing model_search run: 

```bash

    protoc --python_out=./ model_search/proto/phoenix_spec.proto
    protoc --python_out=./ model_search/proto/hparam.proto
    protoc --python_out=./ model_search/proto/distillation_spec.proto
    protoc --python_out=./ model_search/proto/ensembling_spec.proto
    protoc --python_out=./ model_search/proto/transfer_learning_spec.proto

```

#### Running Example
There are few things that need to be added in order to get the code running:

```python 

    import model_search
    from model_search import constants
    from model_search import single_trainer
    from model_search.data import csv_data
    import sys
    from absl import app
    from absl import flags
    from absl import logging

    FLAGS = flags.FLAGS

    sys.argv = sys.argv[:1]
    try:
        app.run(lambda argv: None)
    except:
        pass

    trainer = single_trainer.SingleTrainer(
        data=csv_data.Provider(
            label_index=0,
            logits_dimension=2,
            record_defaults=[0, 0, 0, 0],
            filename="model_search/data/testdata/csv_random_data.csv"),
        spec='./model_search/configs/dnn_config.pbtxt')


    trainer.try_models(
        number_models=200,
        train_steps=1000,
        eval_steps=100,
        root_dir="./",
        batch_size=32,
        experiment_name="example",
        experiment_owner="model_search_user")

```