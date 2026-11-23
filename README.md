# UnScam - Offline On-Device Scam SMS Detector

UnScam is an Android prototype for detecting scam and phishing SMS messages. It runs a fine-tuned Llama model locally to classify pasted messages as SCAM or SAFE and give a short explanation. Local inference has been demonstrated on a physical Android phone, but reliability and network-off behavior still need controlled testing. A SAFE result is not proof that a message is safe.

## How it works

1.⁠ ⁠Paste a suspicious SMS into the app
2.⁠ ⁠The on-device model analyzes it in seconds
3.⁠ ⁠You get a verdict - SCAM or SAFE - plus a one-line reason

## Model

•⁠  ⁠Base: Llama-3.2-1B-Instruct (Meta)
•⁠  ⁠Fine-tuning: LoRA (r=16) with Hugging Face transformers + peft
•⁠  ⁠Dataset: 1,638 labeled SMS (public SMS phishing research dataset + collected Indian scam specimens)
•⁠  ⁠Held-out evaluation: 98.8% accuracy (162/164 messages)
•⁠  ⁠Deployment: ExecuTorch 1.1.0, int4 quantization (2.47 GB to 765 MB), XNNPACK backend on Arm CPU, 512-token context, deterministic output (temperature 0)

## App

•⁠  ⁠Built on the ExecuTorch LlamaDemo Android app
•⁠  ⁠Model loading and local inference demonstrated on a physical Android phone
•⁠  ⁠Designed for local processing of pasted SMS; network-off behavior was not independently verified in the recorded phone trial

## Deliverables

•⁠  ⁠Source code: this repository
•⁠  ⁠Final two-minute physical-phone demonstration: [Watch on Google Drive](https://drive.google.com/file/d/16uHGoSeMJl6dsN9wBgrufbqUW0iRd3zB/view?usp=sharing)
•⁠  ⁠Historical emulator demonstration: demo.mp4
•⁠  ⁠Final technical report: [report unscam.pdf](report%20unscam.pdf)

## Limitations

•⁠  ⁠The 98.8% held-out result (162/164) is from the same dataset family as training, not a physical-phone or field-accuracy measurement
•⁠  ⁠Two synthetic phone tests produced one missed PIN/OTP scam and one correctly detected link-based scam; these examples do not establish general accuracy
•⁠  ⁠Physical-device latency, memory use and network-off behavior still need controlled evaluation
•⁠  ⁠English-language SMS only; 512-token context limit

## Next steps

•⁠  ⁠Investigate the observed false negative and evaluate physical-device accuracy, latency, memory use and network-off behavior
•⁠  ⁠Expand dataset with more real Indian scam SMS
•⁠  ⁠Hindi and regional-language SMS support
•⁠  ⁠Automatic scanning of the SMS inbox
