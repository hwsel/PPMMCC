# $PMC^2$ - NOSSDAV '25

This is the code for our NOSSDAV '25 paper:

Zhongze Tang, Zichen Zhu, Mengmei Ye, Yao Liu, and Sheng Wei. 2025.
Privacy-Preserving Multimedia Mobile Cloud Computing Using Cost-Effective Protective Perturbation. https://doi.org/10.1145/3712678.3721879

# Baseline System (PP) Setup

The baseline system is based on our previous MMSys '23 paper: 

>Mengmei Ye, Zhongze Tang, Huy Phan, Yi Xie, Bo Yuan, Sheng Wei. Visual Privacy Protection in Mobile Image Recognition Using Protective Perturbation. ACM Multimedia Systems Conference (MMSys), June 2022.

Its implementation can be found at https://github.com/hwsel/ProtectivePerturbation. We highly recommend you follow this link to setup the baseline system first.

# $PMC^2$ Setup

![](/pics/pmc_sys.png)

## Mobile Client

The *mobile client* compresses the privacy-sensitive images using JPEG and offloads them to the trusted *secure edge server* via an in-domain HTTPS link. It's modified from the baseline system version directly.

## Secure Edge Server

On the *secure edge server*, a perturbation generator
runs inside the confidential container to securely inject protective perturbations to the received user images in real time; then, the perturbed images are compressed by a perturbation-aware neural encoder and transferred to the cloud server for image recognition via the cross-domain HTTPS link.

We rent an AMD EPYC 7443P bare metal machine from [Vultr](https://vultr.com) and setup the [Confidential Container](https://github.com/confidential-containers/confidential-containers) with k8s operator following their offical guidance.

Deploy the Perturbation Generator and Neural Encoder inside. Code to be available soon.

## Cloud Server

The *cloud server* decodes the compressed images using a neural decoder. The reconstructed images are then fed into the machine learning-based image recognition model for computation-intensive classifications. Finally, the image recognition results are returned to the *mobile client* via the *secure edge server*.

We rent an GPU machine from Vultr and deployed the image recognition model on it directly with CUDA acceleration.

# Contact

If you have any questions, please send email to Zhongze Tang (zhongze.tang@rutgers.edu) or Zichen Zhu (zichen.zhu@rutgers.edu).

# License

MIT
