# vllm-cpu-arm

Build [vLLM](https://github.com/vllm-project/vllm) for CPU inference on ARM64 (aarch64).

```
        _ _ _                                                
 __   _| | | |_ __ ___         ___ _ __  _   _        __ _ _ __ _ __ ___  
 \ \ / / | | | '_ ` _ \ _____ / __| '_ \| | | |_____ / _` | '__| '_ ` _ \ 
  \ V /| | | | | | | | |_____| (__| |_) | |_| |_____| (_| | |  | | | | | |
   \_/ |_|_|_|_| |_| |_|      \___| .__/ \__,_|      \__,_|_|  |_| |_| |_|
                                   |_|                                      
```

## What

A GitHub Actions workflow that builds the upstream vLLM CPU image natively on ARM runners and pushes to Quay.io. No QEMU, no cross-compilation -- just native ARM64 builds.

## Why

The upstream vLLM CPU images and RHAII `vllm-cpu-rhel9` are x86-only (AVX2). The PyPI aarch64 wheel ships with CUDA dependencies. Running LLMD CPU tests on ARM clusters needs an image built from source with `VLLM_TARGET_DEVICE=cpu`.

## Usage

Trigger the workflow manually from the Actions tab:

- **vllm_version**: upstream tag to build (e.g. `v0.18.0`)
- **image_tag**: tag for the output image (e.g. `3.4`)

### Required secrets

| Name | Description |
|------|-------------|
| `QUAY_USER` | Quay.io username |
| `QUAY_PASSWORD` | Quay.io password or robot token |
| `QUAY_OWNER` (variable) | Quay.io organization/namespace |
