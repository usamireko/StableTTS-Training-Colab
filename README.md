# StableTTS-Training-Colab
A StableTTS notebook created for training StableTTS v1.1 models in Google Colab as easily as my knowledge allows me :)

Any improvements are welcome!!

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/usamireko/StableTTS-Training-Colab/blob/main/StableTTS_Training.ipynb)



# Instructions of usage

- # Step 1

![image](https://github.com/user-attachments/assets/f415c7e8-7b6c-4c03-9edb-729127f68c00)

Run the Installation cell, it will prompt you to connect your Google Drive to the notebook and manage the training files there, it shouldnt take more than 5 minutes to install.

- # Step 2
![image](https://github.com/user-attachments/assets/fdc7fe1f-20b5-4bdd-a7ca-fbe88171229c)

In this step, the cell asks you for a project name, provide a name for your training session (could be the name of the dataset for example), then the cell will create the folder with the name "StableTTS" under the root of your Google Drive, then it´ll create a folder with the name you chose and inside it will create 3 folders with the name "checkpoints" (in this one the cell will download the pretrained model), "logs" and "wavs".

*This step is not needed when resuming training*

- # Step 3

Here is time to upload your files to your Google Drive, your wavs shall be uploaded to the "wavs" folder, and your list with the transcriptions in the root of the folder created for that training session *(Could be anywhere the upload of the filelist but I suggest at the root to keep tracking of the files in case of making more than one training session)*

*This step is not needed when resuming training*


- # Step 3.5

![image](https://github.com/user-attachments/assets/ecb320e9-4e6a-40c6-a896-5973e91d3362)


This cell is especially created for the filelists created for Tacotron2 datasets, if your filelist follows the format "wavs/xxx.wav|", use this cell to convert your filelist to the format needed for StableTTS *That´s why the Step 2 creates a wavs folder :)*

This will overwrite your filelist to give you one adapted for StableTTS so keep an untouched copy somewhere else 

*This step is not needed when resuming training*

- # Step 4
![image](https://github.com/user-attachments/assets/0609934e-d64d-4d59-8c17-e2c830d0f2a2)

Run this cell to download the vocoder to the needed directory

- # Step 5
![image](https://github.com/user-attachments/assets/c7d87dfe-ba86-4676-8d5f-94ed66109cc9)

This is the where we modify the needed settings to preprocess the dataset

- input_filelist_path: Path of your filelist, copy it here.
  
- output_filelist_path: Path of a new filelist with the required settings (Its totally different than your original filelist), you can save it everywhere, but I recommend alongside your original filelist, in all cases you **MUST** follow this format "/path/to/the/filelist/any_name.json".
  
- output_feature_path: Path where the mels will be saved, it´ll create a folder named "mels", Recommended: The root folder of your training session.
  
- language: What language your dataset is, currently available: Japanese, English and Chinese.

- Resample: It´ll save resampled wav files, this is not needed to enable.


- # Step 6

![image](https://github.com/user-attachments/assets/fcd0622b-0466-4150-a51f-6b2a772fceb8)

Run this cell to preprocess your dataset.

*Sometimes it might throw warnings of not founding some wavs, seems to be that Colab takes a bit of time to notice all the wavs, if that happens, run again the cell, or just wait a few minutes for Colab noticing the files*


If all was followed corrected up to this point, you should have these files and folders in your Drive under the folder "StableTTS/name_of_project"

![image](https://github.com/user-attachments/assets/4f442628-0a60-47c9-ade1-731a0f66ede9)


- # Step 7

![image](https://github.com/user-attachments/assets/a1667ab1-001b-4da7-9fe9-43c071541b1f)

This cell is for modifying the configs of the training:

- train_dataset_path: Path of your JSON file
- test_dataset_path: Path of your JSON file (according to the repo this isnt needed for training, so you can skip this or do the copy-paste)
- batch_size: This explains itself, default is 32, but you can modify it if you go OOM or any reason you have to change this value.
- num_epochs: This will limit the maximum amounts of epochs trained, default is 10,000 epochs, after this number the training will stop automatically.
- model_save_path: Path of the checkpoints folder that was created on Step 2.
- log_dir: Path of the logs folder created in Step 2.
- log_interval: Explains itself (How many epochs it´ll save logs of it)
- save_interval: Interval of epochs to save a checkpoint in the folder.

- # Step 8

![image](https://github.com/user-attachments/assets/ca2bf228-cc34-4082-9e25-c143e001cc33)

Just copy-paste the logs folder path to this cell if you want to see the logs in a Tensorboard window.

If all runs smoothly you will see that the training is starting, usually around at 200 epochs you can have usable results, but that greatly depends of your dataset and/or voice. When you wanna test the model or feel thats enough, just stop the cell and congratulations, you trained a StableTTS model!


- # Extra steps: Inference time!

Although this notebook isnt focused for inference (there´s already one in the StableTTS repo), this is useful for testing models.

![image](https://github.com/user-attachments/assets/0f612b8d-65df-41fe-a266-a5a433536155)

- tts_model_path: Path of the checkpoint you want to test.


![image](https://github.com/user-attachments/assets/1a62757e-e2a6-42d1-89fd-4985952e7078)

In this cell is where the inference will occur!

- text: What you want the model to say.
- ref_audio: Reference Audio, copy any wav of your dataset (swap between these to see what generation you like the most!)
- language: In what language the text is.
- solver: You can choose between dopri5, euler and midpoint (swap between these to see whats better for your output)
- steps: Similar to Stable Diffusion, how many steps you´ll give to your output, more isn´t always better! (Default: 30)
- cfg: Classifier-Free Guidance, play with values around 1-4 (Default: 3)










# Version of notebook: v1.2

# Changelog

- v1.2: Added the ability to convert Tacotron2-style lists (wavs/xxx.wav) to the required format for StableTTS (full path of the wavs).
- v1.1: Added the ability to modify settings and paths inside colab, manual modification of preprocess.py and config.py is no longer needed for normal usage.
- v1.0: Initial Release.


## Credits
+ [StableTTS](https://github.com/KdaiP/StableTTS)

