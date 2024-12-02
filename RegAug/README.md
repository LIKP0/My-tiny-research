# RegAug: Brain MRI data augmentation based on registration learning

[Paper Link](https://kns.cnki.net/kcms2/article/abstract?v=ifIT5_n5_GfWGlsI1rA4rWoo2b818SX-SaQzTANQU71PepTEVXhl2Txdhd9Y9V-BGlKBroslm3nyZ4uUX48SVIkfADvynbYGiXwA8ZLDTE7XIIrF0VSl3ugEmB30b-2d9o8-h6Cw-hKmY4oSHWn8-E6C5nkaoyXAUMGVL4zwFKaAAg7YqYGNASxJO4dPv40YL7myOzZId6vJNqk6d-vRbw==&uniplatform=NZKPT). You can access the file directly in this directory.

This is my first formal research in 2022 and I aim to improve the framework of DataAug. Unfortunately, the work was almost finished when I found another work (MPDUD) with very similar ideas, had been published. :cry: So I had to further develop it but the innovations didn't work well. I had to give it up after one year's struggling. At least, I got a lot of experiences on the "learning registration to learn segmentation (LRLS)" framework and I never cheat. :smile:

## Experiences
1. The core of LRLS is: A deformation field can transform an image A to another image B, and the ground truth label of A can also be transformed to generate pseudo lables of B (**"propagate"**). The training of registration network to generate deformation fields is unsupervised so the total need is one ground truth label of atlas. ==> one-shot
2. In my **own** opinion and experiments, the apperance transform branch in DataAug and MPDUD contributes **little** improvement to the data augmentation, if the downstream segmentation work is robust enough to the contrast noise (like [nnUNet](https://github.com/MIC-DKFZ/nnUNet)).
3. Based on point 2, DO NOT USE advanced segmentation network if you want to show obvious improvement in LRLS :sweat_smile:: In DataAug and MPDUD, they employ a simple 2D UNet.
4. The deformation fields are easier to learn for networks compared with direct reconstruction in image space.
5. I trust "deformation" is more suitable for the real pathological change like ventrical enlargement and cortex atrophy. I believe the **potential** of "deformation" in medical image synthesis.

## 1 Motivations
1. One-shot brain MRI segmentation
2. Better performance than previous works.

## 2 Related work
1. [DataAug](https://openaccess.thecvf.com/content_CVPR_2019/html/Zhao_Data_Augmentation_Using_Learned_Transformations_for_One-Shot_Medical_Image_Segmentation_CVPR_2019_paper.html): The first work of LRLS framework. First, synthesize spatial transform fields and apperance fields with methods very similar to medical registration work like [VoxelMorph](https://arxiv.org/abs/1809.05231). Then, generate MRIs and related pseudo labels with the combination of spatial and apperance fields. Finally, train a segmentation network with the augmented data.
2. [MPDUD](https://ojs.aaai.org/index.php/AAAI/article/view/16212): This work is very similar to my previous idea... The main development compared with DataAug is replacing the process of **"combination"** with VAE to improve the diversity.
3. [BRBS](https://ieeexplore.ieee.org/abstract/document/9842340): Latest LRLS framework. Congratulations to them! :+1:

## 3 RegAug
1. Try to replace the VAE in MPDUD with a conditional VAE to improve diversity.
2. <1% improvement than MPDUD and 3% improvement than DataAug... Too little to be qualified for publication on international conference.
3. The improvement is so little that I have to change to another story "atlas-based segmentation" for the paper, and ignore the comparisions with DataAug and MPDUD. :pensive:

## 4 Results 
![分割结果可视化对比](https://github.com/user-attachments/assets/6c66a0de-e245-43a5-bd32-e37b9efa4ec8)

## 5 Acknowledgement
This article aims to share experience and represents only personal opinions. Corrections are welcomed. **The article respects and appreciates all the works mentioned above**.



