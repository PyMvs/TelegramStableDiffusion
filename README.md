# TelegramStableDiffusion
*In order to run this repository it is necessary to have created your own model in [Hugging Face](https://huggingface.co/) to be able to access it*

*TelegramStableDiffusion* is a way to get results in a much more visual, fast and direct way for many more people, since it is not necessary to interact with any online platform or run anything in the cloud. It is necessary to emphasize that for the execution of the AI in telegram, logically it must be running in google colab, if you close the session you will not be able to obtain any type of result. 

in this example, as in the inference, my dog *Urko* has been used to obtain images:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/18FZvTBNm600LV4yBj6VLIAnTHExCoiu4#scrollTo=fkV_XKgx1mzb)

## Requirements
You need it to update, install and run *Hugging Face, diffusers and telegram-bot*

```python
diffusers==0.7.2
transformers==4.24.0
scipy==1.7.3
ftfy==6.1.1
python-telegram-bot>=20.0a2
python-dotenv>=0.20.0
huggingface_hub==0.10.1
```

## Hugging Face

1. Register in [Hugging Face](https://huggingface.co/) and create a [token](https://huggingface.co/settings/tokens) with write access. 
For more information: https://huggingface.co/docs/hub/security-tokens

2. Create a Model in your profile using [Diffusers](https://huggingface.co/spaces/diffusers/convert-sd-ckpt). Convert your Stable Diffusion `.ckpt` file to Hugging Face Diffusers (Select *Host the model on the Hugging Face Hub* in 2nd step)

3. Upload your `.ckpt` in your Hugging Face model:

![image](https://user-images.githubusercontent.com/23172965/204022430-31714cd5-ca1e-4e2c-adc3-a0d34988cc2c.png)

4. Use your model name for your `model_id` later:

![image](https://user-images.githubusercontent.com/23172965/204022618-23b26ee1-4075-422b-a230-19dc71896e9d.png)

5. Talk to BotFather and create a bot [FatherBot](https://t.me/BotFather).

6. It is recommended to create an .env file to hide all the private and personal information to be used in the project

7. Install libraries from ```requirements.txt``` (*search in the code of Google Collab for more information to execute the .py*)

8. ```!python TelegramStableDiffusion/telegram_bot.py```

## Configuration

```python
TG_TOKEN = os.getenv('TG_TOKEN') #OUR TELEGRAM TOKEN (XXXXXXXXXXX:XXXXXXXXXXXXXX-XXXXXXXXXXXXX)
MODEL_DATA = os.getenv('MODEL_DATA', 'runwayml/stable-diffusion-v1-5') #(PROFILE NAME/MODEL NAME) IN HUGGINGFACE
LOW_VRAM_MODE = (os.getenv('LOW_VRAM', 'true').lower() == 'true')
USE_AUTH_TOKEN = (os.getenv('USE_AUTH_TOKEN', 'true').lower() == 'true')
SAFETY_CHECKER = (os.getenv('SAFETY_CHECKER', 'true').lower() == 'true')
HEIGHT = int(os.getenv('HEIGHT', '512')) #MAKE SURE HEIGHT & WIDHT ARE BOTH MULTIPLES OF 8 
WIDTH = int(os.getenv('WIDTH', '512')) #GOING BELOW 512 IN SOME OF THEM MIGHT RESULT IN LOWER QUAILITY IMAGE
NUM_INFERENCE_STEPS = int(os.getenv('NUM_INFERENCE_STEPS', '50')) #GOOD QUALITY WITH 50 (20 TO TESTING PROMPTS)
STRENTH = float(os.getenv('STRENTH', '0.75'))
GUIDANCE_SCALE = float(os.getenv('GUIDANCE_SCALE', '7.5'))
```

## CPU to CUDA 

It is important to emphasize that if a graphics card is used, it is necessary to change the use of "cpu" to "cuda" , although said change is already made in the uploaded code. If you want the other way around, use "cpu" instead.

### Individual image 🏞
```python
pipe.to("cuda")
img2imgPipe.to("cuda")
```

### Typical problems

```python
#revision = "fp16" if LOW_VRAM_MODE else None
revision = None
torch_dtype = torch.float16 if LOW_VRAM_MODE else None
```

If you don't have a branch with ```LOW_VRAM_MODE``` called *fp16*, you need to use  ```revision = None``` for it to work properly


## RESULTS

![image](https://user-images.githubusercontent.com/23172965/205283774-2d37dc07-22f5-429e-86c5-3752133dbb7c.png)

![image](https://user-images.githubusercontent.com/23172965/205283843-daf2ee4b-b211-404d-b7f3-3a334e6385c9.png)


Credits:

● [Jossalgon](https://github.com/jossalgon/StableDiffusionTelegram) (source of .py)

● [Diffusers](https://github.com/huggingface/diffusers)

● [PythonBot](https://github.com/python-telegram-bot/python-telegram-bot)

● [SD](https://github.com/CompVis/stable-diffusion)
