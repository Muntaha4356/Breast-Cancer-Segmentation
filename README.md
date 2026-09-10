# Breast-Cancer-Segmentation

## Metrices when alpha = 0.7 and beta = 0.3 in travesky loss
<img width="259" height="73" alt="image" src="https://github.com/user-attachments/assets/0c01cfac-7308-4683-b568-3460d33e297a" />
<img width="298" height="397" alt="image" src="https://github.com/user-attachments/assets/603c9323-8f2c-47c3-88e7-77db5dd991ee" />

## Metrices after alpha = 0.5 and beta = 0.5
<img width="314" height="112" alt="image" src="https://github.com/user-attachments/assets/9c1c211c-1bc8-40b4-920e-d15aaf9faefd" />

<img width="298" height="397" alt="image" src="https://github.com/user-attachments/assets/5fa49358-b798-4ae5-935f-47a292506d2d" />

Row 1: Ground truth is an irregular hand-shaped blob. Prediction is now an irregular, branching organic shape too — no rectangle. It's not a perfect match (some extra red below-left that isn't in the green), but it's clearly tracing structure now, not painting a box.

Row 2: Ground truth is a tight cluster of small dots. Prediction is now small scattered dot-like blobs too, roughly in the right neighborhood — a few stray ones off to the side, but this is a completely different failure mode than the giant square you had before.

Row 3: Ground truth is two tiny dots near the breast edge. Prediction shows two separate irregular blobs, in roughly the same region but shifted further into the tissue and oversized relative to the true dots. Location is closer than before, but still not tight.
Row 4: This one's the interesting trade-off. Ground truth is almost the entire frame (a large, diffuse mass/dense region). Prediction now shows several small scattered patches instead of covering the bulk of the region. Under the old model this case looked "good" only because it defaulted to painting most of the frame regardless — now that it's not doing that reflexively, it's under-segmenting genuinely large regions. This is your recall trade-off from the loss rebalance showing up visually, not a new bug.
Bottom line: the blockiness is gone — that confirms the loss imbalance (root cause #1) was the dominant driver of the rectangular over-segmentation you originally saw. What's left now is a real but much smaller problem: predictions are shape-appropriate but not tightly localized (shifted, slightly oversized for small lesions, undersized for large diffuse ones).
https://www.kaggle.com/datasets/muntahapolaris/final-crop-attn-unet-v2

