project on github:https://github.com/ashnkumar/sketch-code

Setup:
Prerequisites:
Python 3 (not compatible with python 2)
pip

Install dependencies:
$ pip install -r requirements.txt

Example Usage:
Download the data and pretrained weights:
# Getting the data, 1,700 images, 342mb
git clone https://github.com/ashnkumar/sketch-code.git
cd sketch-code
cd scripts

# Get the data and pretrained weights
sh get_data.sh
sh get_pretrained_model.sh
# get_data.sh mkdir data/ and then downloads all_data.zip and unzip.
# get_pretrained_model.sh mkdir bin/ and then download model_json.json and weights.h5 to it.
# in case of the provider server offline ,those files were downloaded and save to onedrive, id is dontworrylee.


General Usage:
Converting a single image into HTML code, using weights:
cd src
python convert_single_image.py --png_path {path/to/img.png} \
      --output_folder {folder/to/output/html} \
      --model_json_file {path/to/model/json_file.json} \
      --model_weights_file {path/to/model/weights.h5}

eg:
python convert_single_image.py --png_path ../workspace/pic/TTTest.png \
      --output_folder ../workspace/html \
      --model_json_file ../bin/model_json.json \
      --model_weights_file ../bin/weights.h5

Converting a batch of images in a folder to HTML:
cd src
python convert_batch_of_images.py --pngs_path {path/to/folder/with/pngs} \
      --output_folder {folder/to/output/html} \
      --model_json_file {path/to/model/json_file.json} \
      --model_weights_file {path/to/model/weights.h5}

Train the model:
cd src
# training from scratch
# <augment_training_data> adds Keras ImageDataGenerator augmentation for training images
python train.py --data_input_path {path/to/folder/with/pngs/guis} \
      --validation_split 0.2 \
      --epochs 10 \
      --model_output_path {path/to/output/model}
      --augment_training_data 1
# training starting with pretrained model
python train.py --data_input_path {path/to/folder/with/pngs/guis} \
      --validation_split 0.2 \
      --epochs 10 \
      --model_output_path {path/to/output/model} \
      --model_json_file ../bin/model_json.json \
      --model_weights_file ../bin/pretrained_weights.h5 \
      --augment_training_data 1

Evalute the generated prediction using the BLEU score:
cd src
# evaluate single GUI prediction
python evaluate_single_gui.py --original_gui_filepath  {path/to/original/gui/file} \
      --predicted_gui_filepath {path/to/predicted/gui/file}
# training starting with pretrained model
python evaluate_batch_guis.py --original_guis_filepath  {path/to/folder/with/original/guis} \
      --predicted_guis_filepath {path/to/folder/with/predicted/guis}

