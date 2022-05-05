# COSC6364_Project
This project implementd fast MRI with U-Net and k-sapce correction using Keras.

Dataset: https://fastmri.org/dataset/

Reference:
[1] fast MRI: An Open Dataset and Benchmarks for Accelerated MRI
[2] Deep learning for undersampled MRI reconstruction 

How to use:
1. MRI_unet_with_k_correction.ipynb is the core code to implement the u-net, k-space correction and evaluation method:
2. Using steps:
  a. u_net_model = build_unet()
  
  b. train_model_with_frequency(u_net_model, train_ds, val_ds) or train_baseline_model(u_net_model, train_ds,val_ds)
 
  c. preds_test = u_net_model.predict(x, verbose=1)  // after training the model, we can use the predict to check the reconstructed image
  
     <img width="251" alt="image" src="https://user-images.githubusercontent.com/36893335/166965300-b16265f4-078a-47a3-ba49-e6144a1cf781.png">
  
  d. then you can use these lines to get the final reconstruction image after k-correction: 
  
      pred_test = np.squeeze(pred_test)
      gt_k_space = calculate_k_space(gt_test)
      pred_k_space = calculate_k_space(pred_test)
      correct_k_space = k_space_correction(gt_k_space, pred_k_space)
      correct_img = calculate_image_from_kspace(correct_k_space)
      
  e. evaluation the results: 
  
     psnr = psnr_metrix_test(gt_test, correct_img)
     ssim = ssim_metrix_t(gt_test, correct_img)
     nmse = nmse_metrix(gt_test, correct_img)
     
