# vllm-gh200-vs-h100

This repo contains code used for benchmarking inference on both the gh200 and h100 with the Llama 3.1 70B model.

# Set Up - GH200

See [https://docs.lambdalabs.com/public-cloud/on-demand/serving-llama-31-vllm-gh200/#set-up-your-python-virtual-environment](https://docs.lambdalabs.com/public-cloud/on-demand/serving-llama-31-vllm-gh200/#setting-up-your-environment)

# Set Up - H100

Install pytorch and vllm as normal

# Running the benchmark

- GH200: `python bench.py --cpu-offload-gb 60 --max-model-len 4096 --num-tokens 1024`
- H100: `python bench.py --cpu-offload-gb 75 --max-model-len 4096 --num-tokens 1024`

Results:

| GPU | Tokens/s | 
| --- | -------- |
| H100 | 0.57 |
| GH200 | 4.33|

The reason for this is because neither GPU can entirely fit the 70B model in memory, we need to utilize cpu offloading (via `--cpu-offload-gb`). Not only does the GH200 have a little bit more GPU memory, so we can offload less, but the GH200 also has a much faster CPU<>GPU transfer bandwidth, meaning it is just faster overall.
