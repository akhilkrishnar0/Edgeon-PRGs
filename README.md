# Edgeon-PRGs
===================

Weak Areas and Explanations:
Potential Overfitting Risk:

Issue: The model architecture is complex with a high number of parameters (e.g., two fully connected layers with 4096 neurons each), which may lead to overfitting, especially if the dataset is small.
Solution: Introduce techniques such as early stopping, L2 regularization, or reduce the network size.
Memory Usage Concerns:

Issue: Loading and storing the entire dataset in memory (np.array([...])) might cause memory overflow if the dataset is large.
Solution: Use a generator-based approach (flow_from_directory) to load images in batches instead of loading all at once.
Image Preprocessing Limitations:

Issue: The preprocessing step lacks robust normalization techniques beyond simple max-scaling. If the FITS images have outliers or varying intensities, this might not be optimal.
Solution: Use techniques like MinMaxScaler or standardization (mean subtraction and division by standard deviation).
Resizing with Potential Data Loss:

Issue: The use of cv2.resize may introduce interpolation artifacts and data loss, affecting feature extraction.
Solution: Consider using astronomical tools such as astropy.ndimage.zoom for better preservation of scientific data.
Lack of Channel Adaptation:

Issue: The model expects grayscale (single-channel) inputs, but if FITS images contain multiple layers (e.g., different wavelengths), important information might be lost.
Solution: Ensure multi-channel stacking if different filters are available.
Limited Data Augmentation Diversity:

Issue: The augmentation settings (rotation, flip, brightness) might not fully capture variations seen in astronomical images, which can have distortions, noise, or varying PSFs.
Solution: Add transformations like Gaussian noise, contrast changes, and shear.
Evaluation Metric Choice:

Issue: Only accuracy is used as an evaluation metric, which might not be sufficient for imbalanced datasets.
Solution: Include precision, recall, and F1-score for better performance analysis.
Missing Model Checkpointing:

Issue: No model checkpointing is used, meaning if training is interrupted, progress is lost.
Solution: Use ModelCheckpoint to save the best-performing model.
Lack of Learning Rate Scheduling:

Issue: A fixed learning rate of 0.0001 might not be optimal for the entire training duration.
Solution: Use learning rate decay or adaptive optimizers to adjust the learning rate dynamically.
Inconsistent Data Directory Handling:

Issue: The code assumes specific directory structures (forML/images/prg/gband/), which may break portability.
Solution: Make the data paths configurable or check dynamically for directories.
